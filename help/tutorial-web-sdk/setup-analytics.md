---
title: Configurar o Adobe Analytics usando o SDK da Web do Experience Platform
description: Saiba como configurar o Adobe Analytics usando o SDK da Web do Experience Platform. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
solution: Data Collection, Analytics
exl-id: de86b936-0a47-4ade-8ca7-834c6ed0f041
source-git-commit: 15bc08bdbdcb19f5b086267a6d94615cbfe1bac7
workflow-type: tm+mt
source-wordcount: '3473'
ht-degree: 1%

---

# Configurar o Adobe Analytics com o SDK da Web da plataforma


>[!CAUTION]
>
>Esperamos publicar grandes alterações neste tutorial na terça-feira, 23 de abril de 2024. Depois desse ponto, muitos exercícios serão alterados e talvez seja necessário reiniciar o tutorial desde o início para concluir todas as lições.

Saiba como configurar o Adobe Analytics usando o [Experience Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/overview.html), crie regras de tag para enviar dados ao Adobe Analytics e valide se o Analytics está capturando dados conforme esperado.

[Adobe Analytics](https://experienceleague.adobe.com/docs/analytics.html?lang=pt-BR) O é um aplicativo líder do setor que faz você ser capaz de entender seus clientes como pessoas e de orientar seus negócios com informações de inteligência de clientes.

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Configure um esquema XDM para o Adobe Analytics e entenda a diferença entre variáveis XDM mapeadas automaticamente e manualmente para o Analytics
* Configurar um fluxo de dados para ativar o Adobe Analytics
* Mapear elementos de dados de matriz individuais ou inteiros para o objeto XDM
* Capturar exibições de página no Adobe Analytics com o objeto XDM
* Capturar dados de comércio eletrônico com o objeto XDM para a cadeia de caracteres do produto Adobe Analytics
* Valide se as variáveis do Adobe Analytics são definidas com o objeto XDM usando o Experience Platform Debugger
* Usar as regras de processamento do Adobe Analytics para definir variáveis personalizadas
* A validação de dados é capturada pelo Adobe Analytics usando Relatórios em tempo real

## Pré-requisitos

Você está familiarizado com tags, Adobe Analytics e [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} funcionalidade de logon e compra.

Você precisa de pelo menos uma ID de conjunto de relatórios de teste/desenvolvimento. Se você não tiver um conjunto de relatórios de teste/desenvolvimento que pode ser usado para este tutorial, [crie um](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html).

Você deve ter concluído todas as etapas das seções anteriores no tutorial:

* Configuração inicial
   * [Configurar permissões](configure-permissions.md)
   * [Configurar um esquema XDM](configure-schemas.md)
   * [Configurar um namespace de identidade](configure-identities.md)
   * [Configurar uma sequência de dados](configure-datastream.md)
* Configuração de tags
   * [Instalação da extensão do SDK da Web](install-web-sdk.md)
   * [Criar elementos de dados](create-data-elements.md)
   * [Criar uma regra de tag](create-tag-rule.md)
   * [Validar com o Adobe Experience Platform Debugger](validate-with-debugger.md)

## Esquemas XDM e variáveis do Analytics

Parabéns! Você já configurou um esquema compatível com o Adobe Analytics no [Configurar um esquema](configure-schemas.md) lição!

A implementação do SDK da Web da Platform deve ser o mais independente de produto possível. Para o Adobe Analytics, o mapeamento de eVars, props e eventos não ocorre durante a criação do esquema nem durante a configuração das regras de tag, como tem sido feito tradicionalmente. Em vez disso, cada par de valor-chave XDM se torna uma Variável de dados de contexto que mapeia para uma variável do Analytics de uma das duas formas a seguir:

1. Variáveis mapeadas automaticamente usando campos XDM reservados
1. Variáveis mapeadas manualmente usando regras de processamento do Analytics

Para entender quais variáveis XDM são mapeadas automaticamente para o Adobe Analytics, consulte [Variáveis mapeadas automaticamente no Analytics](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=en). Qualquer variável que não seja mapeada automaticamente deve ser mapeada manualmente.

O esquema criado na variável [Configurar um esquema](configure-schemas.md) A lição contém algumas variáveis mapeadas automaticamente para o Analytics, conforme descrito nesta tabela:

| Variáveis mapeadas automaticamente do XDM para o Analytics | variável do Adobe Analytics |
|-------|---------|
| `identitymap.ecid.[0].id` | mid |
| `web.webPageDetails.pageViews.value` | uma chamada s.t() de exibição de página |
| `web.webPageDetails.name` | s.pageName |
| `web.webPageDetails.server` | s.server |
| `web.webPageDetails.siteSection` | s.channel |
| `commerce.productViews.value` | prodView |
| `commerce.productListViews.value` | scView |
| `commerce.checkouts.value` | scCheckout |
| `commerce.purchases.value` | Aquisição |
| `commerce.order.currencyCode` | s.currencyCode |
| `commerce.order.purchaseID` | s.purchaseID |
| `productListItems[].SKU` | s.products=;nome do produto;;; (principal - consulte a Observação abaixo) |
| `productListItems[].name` | s.products=;nome do produto;;;; (fallback - consulte a Observação abaixo) |
| `productListItems[].quantity` | s.products=;;quantidade do produto;;; |
| `productListItems[].priceTotal` | s.product=;;;preço do produto;; |

>[!NOTE]
>
>As seções individuais da cadeia de caracteres do produto Analytics são definidas por meio de diferentes variáveis XDM na `productListItems` objeto.
>Em 18 de agosto de 2022, `productListItems[].SKU` tem prioridade para mapear para o nome do produto na variável s.products.
>O valor definido como `productListItems[].name` é mapeado para o nome do produto somente se `productListItems[].SKU` não existe. Caso contrário, ele não será mapeado e estará disponível nos dados de contexto.
>Não defina uma cadeia de caracteres vazia ou nula como  `productListItems[].SKU`. Isso tem o efeito indesejado de mapear para o nome do produto na variável s.products.


## Configurar o fluxo de dados

O SDK da Web da Platform envia dados do seu site para o Platform Edge Network. Seu fluxo de dados informa à Platform Edge Network para onde encaminhar esses dados, neste caso, qual dos seus conjuntos de relatórios do Adobe Analytics.

1. Ir para [Coleta de dados](https://experience.adobe.com/#/data-collection){target="blank"} interface
1. Na navegação à esquerda, selecione **[!UICONTROL Datastreams]**
1. Selecione o criado anteriormente `Luma Web SDK` sequência de dados

   ![Selecione a sequência de dados do SDK da Web Luma](assets/datastream-luma-web-sdk.png)

1. Selecionar **[!UICONTROL Adicionar serviço]**
   ![Adicionar um serviço à sequência de dados](assets/analytics-addService.png)
1. Selecionar **[!UICONTROL Adobe Analytics]** como o **[!UICONTROL Serviço]**
1. Insira o  **[!UICONTROL ID do conjunto de relatórios]** do seu conjunto de relatórios de desenvolvimento
1. Selecionar **[!UICONTROL Salvar]**

   ![Análise de salvamento de sequência de dados](assets/analytics-datastream-save.png)

   >[!TIP]
   >
   >Adicionar mais conjuntos de relatórios selecionando **[!UICONTROL Adicionar conjunto de relatórios]** é equivalente à marcação de vários conjuntos.

>[!WARNING]
>
>Neste tutorial, você só configura o conjunto de relatórios de desenvolvimento do Adobe Analytics. Ao criar fluxos de dados para seu próprio site, você criaria fluxos de dados adicionais e conjuntos de relatórios para seus ambientes de preparo e produção.


## Criar elementos de dados adicionais

Em seguida, capture dados adicionais da camada de dados do Luma e envie-os para o Edge Network da plataforma. Embora a lição se concentre em requisitos comuns do Adobe Analytics, todos os dados capturados podem ser facilmente enviados para outros destinos com base na configuração do fluxo de dados. Por exemplo, se você concluiu a lição do Adobe Experience Platform, os dados adicionais capturados nesta lição também serão enviados para a Platform.

### Criar elementos de dados de comércio eletrônico

Durante a lição Criar elementos de dados, você [elementos de dados JavaScript criados](create-data-elements.md#create-data-elements-to-capture-the-data-layer) que capturou o conteúdo e os detalhes de identidade. Agora você criará elementos de dados adicionais para capturar dados de comércio eletrônico. Como a variável [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} O usa diferentes estruturas de camada de dados para páginas de detalhes do produto e produtos no carrinho. Você deve criar elementos de dados para cada cenário. Você terá que criar alguns elementos de dados de código personalizado para coletar o que precisa da camada de dados do Luma, que pode ou não ser necessária ao implementar no seu próprio site. Nesse caso, você precisa percorrer uma variedade de itens do carrinho de compras para coletar detalhes específicos de cada produto. Use os trechos de código fornecidos abaixo:

1. Abra a propriedade de tag que você está usando no tutorial
1. Ir para **[!UICONTROL Elementos de dados]**
1. Selecionar **[!UICONTROL Adicionar elemento de dados]**
1. Nomear como **`product.productInfo.sku`**
1. Use o **[!UICONTROL Custom Code]** **[!UICONTROL Tipo de elemento de dados]**
1. Deixe caixas de seleção para **[!UICONTROL Forçar valor de minúsculas]** e **[!UICONTROL Texto limpo]** desmarcado
1. Sair `None` como o **[!UICONTROL Duração do armazenamento]** já que esse valor é diferente em cada página
1. Selecionar **[!UICONTROL Abrir editor]**

   ![Elemento de dados do código personalizado](assets/data-element-open-editor.jpg)

1. Copie e cole o código a seguir

   ```javascript
   var cart = digitalData.product;
   var cartItem;
   cart.forEach(function(item){
   cartItem = item.productInfo.sku;
   });
   return cartItem;
   ```

1. Selecionar **[!UICONTROL Salvar]** para salvar o código personalizado

   ![SKU do produto de código personalizado](assets/data-element-products-sku-custom-code.jpg)

1. Selecionar **[!UICONTROL Salvar]** para salvar o elemento de dados

Siga as mesmas etapas para criar esses elementos de dados adicionais:

* **`product.productInfo.title`**

  ```javascript
  var cart = digitalData.product;
  var cartItem;
  cart.forEach(function(item){
  cartItem = item.productInfo.title;
  });
  return cartItem;
  ```

* **`cart.productInfo`**

  ```javascript
  var cart = digitalData.cart.cartEntries;
  var cartItem = [];
  cart.forEach(function(item, index, array){
  var qty = parseInt(item.qty);
  var price = parseInt(item.price);
  cartItem.push({
  "SKU": item.sku,
  "name":item.title,
  "quantity":qty,
  "priceTotal":price
  });
  });
  return cartItem;
  ```

Depois de adicionar esses elementos de dados e criar os anteriores no [Criar elementos de dados](create-data-elements.md) , você deve ter os seguintes elementos de dados:

| Elementos de dados |
-----------------------------|
| `cart.orderId` |
| `cart.productInfo` |
| `identityMap.loginID` |
| `page.pageInfo.hierarchie1` |
| `page.pageInfo.pageName` |
| `page.pageInfo.server` |
| `product.productInfo.sku` |
| `product.productInfo.title` |
| `user.profile.attributes.loggedIn` |
| `user.profile.attributes.username` |
| `xdm.content` |

>[!IMPORTANT]
>
>Neste tutorial, você criará um objeto XDM diferente para cada evento. Isso significa que você deve remapear variáveis que seriam consideradas &quot;globalmente&quot; disponíveis em cada ocorrência, como nome de página e identityMap. No entanto, você pode [Mesclar objetos](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/core/overview.html#merged-objects) ou use [Mapeamento de Tabelas](https://exchange.adobe.com/experiencecloud.details.103136.mapping-table.html) gerenciar os objetos XDM com mais eficiência em uma situação real. Para esta lição, as variáveis globais são consideradas como:
>
>* **[!UICONTROL identityMap]** para capturar a ID autenticada de acordo com a [Criar elemento de dados do Mapa de identidade](create-data-elements.md#create-identity-map-data-element) exercício no [Criar elementos de dados](create-data-elements.md) lição.
>* **[!UICONTROL web]** objeto para capturar conteúdo de acordo com a [objeto XDM de conteúdo](create-data-elements.md#map-content-data-elements-to-XDM-Schema-individually) exercício no [Criar elementos de dados](create-data-elements.md) lição sobre cada elemento de dados acima.

### Incrementar visualizações de página

Na lição Criar elementos de dados, você [criou um `xdm.content` elemento de dados](create-data-elements.md#map-content-data-elements-to-xdm-schema-individually) para capturar dimensões de conteúdo. Como agora você está enviando dados para o Adobe Analytics, também deve mapear um campo XDM extra para indicar que um beacon deve ser processado como uma exibição de página do Analytics.

1. Abra o `xdm.content` elemento de dados
1. Role para baixo e selecione para abrir até `web.webPageDetails`
1. Selecione para abrir o **[!UICONTROL pageViews]** objeto
1. Definir **[!UICONTROL value]** para `1`
1. Selecionar [!UICONTROL **Salvar**]

   ![Objeto XDM de Exibições de página](assets/analytics-xdm-pageviews.png)

>[!TIP]
>
>Este campo equivale a enviar uma **`s.t()`** sinal de exibição de página do Analytics `AppMeasurement.js`. Para um beacon de clique em links, defina o `webInteraction.linkClicks.value` para `1`


### Definir a cadeia de caracteres do produto

Antes de mapear para a string do produto, é importante entender que há dois objetos principais no esquema XDM usados para capturar dados de comércio eletrônico que têm relacionamentos especiais com o Adobe Analytics:

1. A variável `commerce` conjuntos de objetos eventos do Analytics, como `prodView`, `scView`, e `purchase`
1. A variável `productListItems` conjuntos de objetos dimensões do Analytics, como `productID`.

Consulte [Coletar dados do Commerce e de produtos](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html?lang=en) para obter mais detalhes.

Também é importante entender que você pode **[!UICONTROL fornecer atributos individuais]** a campos XDM individuais ou **[!UICONTROL fornecer um array inteiro]** para um objeto XDM.

![Objeto XDM de Exibições de página](assets/analytics-xdm-population.png)

### Mapear atributos individuais para um objeto XDM

Você pode mapear para variáveis individuais para capturar dados na página de detalhes do produto do site de demonstração Luma:

1. Criar um **[!UICONTROL Objeto XDM]** **[!UICONTROL Tipo de elemento de dados]** nomeado **`xdm.commerce.prodView`**
1. Selecione a mesma sandbox da Platform e o esquema XDM usados nas lições anteriores
1. Abra o **[!UICONTROL comércio]** objeto
1. Abra o **[!UICONTROL productViews]** object e set **[!UICONTROL value]** para `1`

   ![Mapeamento de elemento de dados para objeto XDM](assets/analytics-commerce-prodView.png)

   >[!TIP]
   >
   >Esta etapa é equivalente à configuração `prodView` evento no Analytics


1. Role para baixo e selecione `productListItems` matriz
1. Selecionar **[!UICONTROL Fornecer itens individuais]**
1. Selecionar **[!UICONTROL Adicionar item]**

   ![Configuração do evento de exibição de produto](assets/data-element-xdm-productlistitem.png)

   >[!CAUTION]
   >
   >A variável **`productListItems`** é um `array` tipo de dados para que espere que os dados entrem como uma coleção de elementos. Devido à estrutura da camada de dados do site de demonstração Luma e como é possível visualizar apenas um produto de cada vez no site Luma, você adicionará itens individualmente. Ao implementar o em seu próprio site, dependendo da estrutura da camada de dados, talvez você possa fornecer um storage inteiro.

1. Selecione para abrir **[!UICONTROL Item 1]**
1. Mapear as seguintes variáveis XDM para elementos de dados

   * **`productListItems.item1.SKU`** para `%product.productInfo.sku%`
   * **`productListItems.item1.name`** para `%product.productInfo.title%`

   ![Variável de objeto XDM do SKU do produto](assets/data-element-xdm-productlistitem-sku.png)

   >[!IMPORTANT]
   >
   >Antes de salvar esse objeto XDM, defina as variáveis &quot;globais&quot; e o incrementador de exibição de página também:
   >![Redefinição de variáveis globais no XDM](assets/analytics-global-xdm.png)

1. Selecionar **[!UICONTROL Salvar]**

### Mapear uma matriz inteira para um objeto XDM

Como observado anteriormente, o site de demonstração da Luma usa uma estrutura de camada de dados diferente para os produtos no carrinho. O elemento de dados do código personalizado `cart.productInfo` o elemento de dados criado anteriormente faz loop pela variável `digitalData.cart.cartEntries` objeto de camada de dados e traduz no esquema de objeto XDM necessário. O novo formato **deve corresponder exatamente** o schema definido pelo `productListItems` objeto do esquema XDM.

Para ilustrar, consulte a comparação abaixo da camada de dados do site Luma (esquerda) com o elemento de dados traduzido (direita):

![Formato da matriz de objetos XDM](assets/data-element-xdm-array.png)

Compare o elemento de dados com o `productListItems` estrutura (dica, deve corresponder).

>[!IMPORTANT]
>
>Observe como as variáveis numéricas são convertidas, com valores de string na camada de dados, como `price` e `qty` reformatada para números no elemento de dados. Esses requisitos de formato são importantes para a integridade dos dados na Platform e são determinados durante o [configurar schemas](configure-schemas.md) etapa. No exemplo, **[!UICONTROL quantidade]** usa o **[!UICONTROL Integer]** tipo de dados.
> ![Tipo de dados de esquema XDM](assets/schema-data-type.png)

Agora volte a mapear o objeto XDM para uma matriz inteira. Crie um elemento de dados de objeto XDM para capturar produtos na página do carrinho:

1. Criar um **[!UICONTROL Objeto XDM]** **[!UICONTROL Tipo de elemento de dados]** nomeado **`xdm.commerce.cartView`**
1. Selecione a mesma sandbox da Platform e o esquema XDM que você está usando para este tutorial
1. Abra o **[!UICONTROL comércio]** objeto
1. Abra o **[!UICONTROL productListViews]** object e set `value` para `1`

   >[!TIP]
   >
   >Esta etapa é equivalente à configuração `scView` evento no Analytics

1. Role para baixo e selecione **[!UICONTROL productListItems]** matriz
1. Selecionar **[!UICONTROL Fornecer todo o array]**
1. Mapear para **`cart.productInfo`** elemento de dados

   ![Mapeamento de toda a matriz para o objeto XDM](assets/data-element-xdm-provide-array.png)

   >[!IMPORTANT]
   >
   >Antes de salvar esse objeto XDM, defina as variáveis &quot;globais&quot; e o incrementador de exibição de página também:
   >![Redefinição de variáveis globais no XDM](assets/analytics-global-xdm.png)

1. Selecionar **[!UICONTROL Salvar]**

Criar outro **[!UICONTROL Objeto XDM]**  **[!UICONTROL Tipo de elemento de dados]** para check-outs chamados `xdm.commerce.checkout`. Desta vez, defina o **[!UICONTROL commerce.checkouts.value]** para `1`, mapa **[!UICONTROL productListItems]** para **`cart.productInfo`** como você acabou de fazer, e adicione as variáveis &quot;globais&quot; e o contador de visualização de página.

>[!TIP]
>
>Esta etapa é equivalente à configuração `scCheckout` evento no Analytics


Existem etapas adicionais para capturar a variável `purchase` evento:

1. Criar outro  **[!UICONTROL Objeto XDM]**  **[!UICONTROL Tipo de elemento de dados]** para compras chamadas `xdm.commerce.purchase`
1. Abertura **[!UICONTROL comércio]** objeto
1. Abra o **[!UICONTROL pedido]** objeto
1. Mapa **[!UICONTROL purchaseID]** para o `cart.orderId` elemento de dados
1. Definir **[!UICONTROL currencyCode]** ao valor codificado `USD`

   ![Configuração de purchaseID para o Analytics](assets/analytics-commerce-purchaseID.png)

   >[!TIP]
   >
   >É equivalente à configuração `s.purcahseID` e `s.currencyCode` variáveis no Analytics

1. Selecione para abrir o `purchases` object e set `value` para `1`
   >[!TIP]
   >
   >É equivalente à configuração `purchase` evento no Analytics

   >[!IMPORTANT]
   >
   >Antes de salvar esse objeto XDM, defina as variáveis &quot;globais&quot; e o incrementador de exibição de página também:
   >![Redefinição de variáveis globais no XDM](assets/analytics-global-xdm.png)

1. Selecionar **[!UICONTROL Salvar]**

Ao final dessas etapas, você deve ter os cinco elementos de dados de objeto XDM a seguir criados:

| Elementos de dados do objeto XDM |
-----------------------------|
| `xdm.commerce.cartView` |
| `xdm.commerce.checkout` |
| `xdm.commerce.prodView` |
| `xdm.commerce.purchase` |
| `xdm.content` |



## Criar regras adicionais para o SDK da Web da plataforma

Com vários elementos de dados de objetos XDM criados, você está pronto para definir os sinais usando regras. Neste exercício, você cria regras individuais por evento de comércio eletrônico e usa condições para que as regras sejam acionadas nas páginas certas. Vamos começar com um evento de Exibição de produto.

1. Na navegação à esquerda, selecione **[!UICONTROL Regras]** e selecione **[!UICONTROL Adicionar regra]**
1. Nomear como  [!UICONTROL `product view - library load - AA`]
1. Em **[!UICONTROL Eventos]**, selecione **[!UICONTROL Biblioteca carregada (início da página)]**
1. Em **[!UICONTROL Condições]**, selecione para **[!UICONTROL Adicionar]**

   ![Regras XDM do Analytics](assets/analytics-rule-product-view-event.png)

1. Sair **[!UICONTROL Tipo de lógica]** as **[!UICONTROL Regular]**
1. Sair **[!UICONTROL Extensões]** as **[!UICONTROL Núcleo]**
1. Selecionar **[!UICONTROL Tipo de condição]** as **[!UICONTROL Caminho sem cadeia de caracteres de consulta]**
1. À direita, ative a opção **[!UICONTROL Regex]** alternar
1. Em **[!UICONTROL caminho igual a]** set `/products/`. Para o site de demonstração Luma, ele garante que a regra seja acionada somente nas páginas do produto
1. Selecionar **[!UICONTROL Manter alterações]**

   ![Regras XDM do Analytics](assets/analytics-tags-prodView.png)

1. Em **[!UICONTROL Ações]** selecionar **[!UICONTROL Adicionar]**
1. Selecionar **[!UICONTROL Adobe Experience Platform Web SDK]** extensão
1. Selecionar **[!UICONTROL Tipo de ação]** as **[!UICONTROL Enviar evento]**
1. A variável **[!UICONTROL Tipo]** O campo tem uma lista suspensa de valores para escolher. Selecionar `[!UICONTROL commerce.productViews]`

   >[!TIP]
   >
   >O valor selecionado aqui não afeta como os dados são mapeados para o Analytics. No entanto, é recomendável aplicar essa variável cuidadosamente, pois ela é usada na interface do construtor de segmentos do Adobe Experience Platform. O valor selecionado está disponível para uso no `[!UICONTROL c.a.x.eventtype]` downstream da variável de dados de contexto.

1. Em **[!UICONTROL Dados XDM]**, selecione o `[!UICONTROL xdm.commerce.prodView]` Elemento de dados do objeto XDM
1. Selecionar **[!UICONTROL Manter alterações]**

   ![Regras XDM do Analytics](assets/analytics-rule-commerce-productViews.png)

1. Sua regra deve ser semelhante ao mostrado abaixo. Selecionar **[!UICONTROL Salvar]**

   ![Regras XDM do Analytics](assets/analytics-rule-product-view.png)


Repita o mesmo processo para todos os outros eventos de comércio eletrônico usando os seguintes parâmetros:

**Nome da regra**: exibição do carrinho - carregamento da biblioteca - AA

* **[!UICONTROL Tipo de evento]**: Biblioteca carregada (início da página)
* **[!UICONTROL Condição]**: /content/luma/us/en/user/cart.html
* **Digite o valor no SDK da Web - Enviar ação**: commerce.productListViews
* **Dados XDM para SDK da Web - Ação de envio:** `%xdm.commerce.cartView%`

**Nome da regra**: check-out - carregamento da biblioteca - AA

* **[!UICONTROL Tipo de evento]**: Biblioteca carregada (início da página)
* **[!UICONTROL Condição]** /content/luma/us/en/user/checkout.html
* **Tipo para SDK da Web - Ação Enviar**: commerce.checkouts
* **Dados XDM para SDK da Web - Ação de envio:** `%xdm.commerce.checkout%`

**Nome da regra**: compra - carregamento da biblioteca - AA

* **[!UICONTROL Tipo de evento]**: Biblioteca carregada (início da página)
* **[!UICONTROL Condição]** /content/luma/us/en/user/checkout/order/thank-you.html
* **Tipo para SDK da Web - Ação Enviar**: commerce.purchases
* **Dados XDM para SDK da Web - Ação de envio:** `%xdm.commerce.purchase%`

Quando terminar, você deverá ver as seguintes regras criadas.

![Regras XDM do Analytics](assets/analytics-tags-rule.png)

## Criar seu ambiente de desenvolvimento

Adicione os novos elementos de dados e regras à `Luma Web SDK Tutorial` e recriar seu ambiente de desenvolvimento.


## Validar o SDK da Web da Adobe Analytics para plataforma

No [Depurador](validate-with-debugger.md) lição, você aprendeu a inspecionar o beacon de objeto XDM do lado do cliente com o Platform Debugger e o console de desenvolvimento do navegador, que é semelhante à depuração de um `AppMeasurement.js` Implementação do Analytics. Para validar se o Analytics está capturando dados corretamente por meio do SDK da Web da plataforma, você deve seguir duas etapas adicionais para:

1. Validar como os dados são processados pelo objeto XDM no Edge Network da plataforma usando o recurso Edge Trace do depurador de Experience Platform
1. Valide como os dados são processados pelo Analytics usando Regras de processamento e Relatórios em tempo real.

### Usar o Edge Trace

Saiba como validar se o Adobe Analytics está capturando a ECID, as exibições de página, a sequência de caracteres do produto e os eventos de comércio eletrônico com o recurso Edge Trace do Experience Platform Debugger.

### Validação da ID do Experience Cloud

1. Vá para a [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} e use o Experience Platform Debugger para [alterne a propriedade da tag no site para sua própria propriedade de desenvolvimento](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)

   >[!WARNING]
   >
   >Antes de continuar, verifique se você está conectado ao site Luma.  Se você não estiver conectado, o site Luma não permitirá que você faça check-out.
   >
   > 1. No Luma, selecione o botão de logon na parte superior direita e use credenciais **u: test@adobe.com p: test** para autenticar
   >
   > 1. Você será redirecionado automaticamente para a [Página do produto Didi Sport Watch](https://luma.enablementadobe.com/content/luma/us/en/products/gear/watches/didi-sport-watch.html#24-WG02) no carregamento da próxima página

1. Para ativar o Edge Trace, vá para o Experience Platform Debugger, na navegação à esquerda, selecione **[!UICONTROL Logs]**, em seguida, selecione a **[!UICONTROL Edge]** e selecione **[!UICONTROL Conectar]**

   ![Connect Edge Trace](assets/analytics-debugger-edgeTrace.png)

1. Ficará vazio por enquanto

   ![Rastreamento de Borda Conectado](assets/analytics-debugger-edge-connected.png)

1. Atualize o [Página do produto Didi Sport Watch](https://luma.enablementadobe.com/content/luma/us/en/products/gear/watches/didi-sport-watch.html#24-WG02) e verifique o Experience Platform Debugger novamente, você deverá ver os dados aparecerem. A linha que começa com **[!UICONTROL RSIDs de mapeamento automático do Analytics]** é o sinal do Adobe Analytics
1. Selecione para abrir as opções `[!UICONTROL mappedQueryParams]` e a segunda lista suspensa para exibir as variáveis do Analytics

   ![Rastreamento de borda de beacon do Analytics](assets/analytics-debugger-edge-analytics.png)

   >[!TIP]
   >
   >A segunda lista suspensa corresponde à ID do conjunto de relatórios do Analytics para a qual você está enviando dados. Ele deve corresponder ao seu próprio conjunto de relatórios, não ao da captura de tela.

1. Role para baixo para encontrar `[!UICONTROL c.a.x.identitymap.ecid.[0].id]`. É uma variável de dados de contexto que captura a ECID
1. Continue rolando para baixo até visualizar o Analytics `[!UICONTROL mid]` variável. Ambas as IDs correspondem à ID de Experience Cloud do dispositivo.

   ![Analytics ECID](assets/analytics-debugger-ecid.png)

   >[!NOTE]
   >
   >Depois de fazer logon, valide a ID autenticada `112ca06ed53d3db37e4cea49cc45b71e` para o usuário **test@adobe.com** também é capturado na variável `[!UICONTROL c.a.x.identitymap.lumacrmid.[0].id]`


### Exibições da página de conteúdo

Use o mesmo sinal para validar se as exibições de página de conteúdo são capturadas pelo Analytics.

1. Procure `[!UICONTROL c.a.x.web.webpagedetails.pageviews.value]=1`. Ele lhe diz: `s.t()` o sinal de exibição de página está sendo enviado para o Analytics
1. Role para baixo para ver a `[!UICONTROL gn]` variável. É a sintaxe dinâmica do Analytics para a variável `[!UICONTROL s.pageName]` variável. Ele captura o nome da página da camada de dados.

   ![Sequência de produto do Analytics](assets/analytics-debugger-edge-page-view.png)

### Sequência de caracteres do produto e eventos de comércio eletrônico

Como você já está em uma página de produto, este exercício continua a usar o mesmo Edge Trace para validar se os dados do produto foram capturados pelo Analytics. A sequência de caracteres do produto e os eventos de comércio eletrônico são variáveis XDM mapeadas automaticamente para o Analytics. Contanto que você tenha mapeado para o `productListItem` Variável XDM enquanto [configuração de um esquema XDM para o Adobe Analytics](setup-analytics.md#configure-an-xdm-schema-for-adobe-analytics), o Edge Network da Platform cuida do mapeamento dos dados para as variáveis de análise adequadas.

1. Primeiro, valide se a variável `Product String` está definido
1. Procure `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL sku]`. A variável captura o valor do elemento de dados que você mapeou para o `productListItems.item1.sku` anteriormente nesta lição
1. Role para baixo para ver a `[!UICONTROL pl]` variável. É a sintaxe dinâmica da variável da cadeia de caracteres do produto Analytics
1. Ambos os valores correspondem ao nome do produto disponível na camada de dados

   ![Sequência de produto do Analytics](assets/analytics-debugger-prodstring.png)

O Edge Trace trata `commerce` eventos ligeiramente diferentes de `productList` dimensões. Você não vê uma variável de dados de contexto mapeada da mesma forma que vê o nome do produto mapeado para `[!UICONTROL c.a.x.productlistitem.[0].name]` acima. Em vez disso, o Edge Trace mostra o mapeamento automático do evento final no Analytics `event` variável. O Platform Edge Network o mapeia adequadamente, desde que você o mapeie para o XDM correto `commerce` enquanto [configuração do esquema para o Adobe Analytics](setup-analytics.md#configure-an-xdm-schema-for-adobe-analytics); neste caso, o `commerce.productViews.value=1`.

1. De volta à janela Experience Platform Debugger, role para baixo até a `[!UICONTROL event]` , está definida como `[!UICONTROL prodView]`

   ![Exibição de produto do Analytics](assets/analytics-debugger-prodView.png)

Valide se os demais eventos de comércio eletrônico e cadeias de caracteres de produtos estão definidos para o Analytics.

1. Adicionar [Didi Sport Watch](https://luma.enablementadobe.com/content/luma/us/en/products/gear/watches/didi-sport-watch.html#24-WG02) ao carrinho
1. Vá para a [Página de carrinho](https://luma.enablementadobe.com/content/luma/us/en/user/cart.html), verifique o Edge Trace para `[!UICONTROL events: "scView"]` e a string do produto

   ![Exibição de carrinho do Analytics](assets/analytics-debugger-cartView.png)

1. Prossiga para o check-out, verifique o Edge Trace para `[!UICONTROL events: "scCheckout"]` e a string do produto

   ![Check-out do Analytics](assets/analytics-debugger-checkout.png)

1. Preencha apenas o **Nome** e **Sobrenome** no formulário de entrega e selecione **Continuar**. Na próxima página, selecione **Fazer pedido**
1. Na página de confirmação, verifique o Edge Trace para

   * Evento de compra sendo definido `[!UICONTROL events: "purchase"]`
   * Variável de código de moeda sendo definida `[!UICONTROL cc: "USD"]`
   * ID de compra sendo definida em `[!UICONTROL pi]`
   * Sequência de caracteres do produto `[!UICONTROL pl]` definição do nome do produto, quantidade e preço

   ![Compra no Analytics](assets/analytics-debugger-edge-analytics-purchase.png)

## Regras de processamento e relatórios em tempo real

Agora que você validou os sinais do Analytics com o Edge Trace, também é possível validar se os dados são processados pelo Analytics usando os relatórios em tempo real. Antes de verificar os relatórios em tempo real, é necessário configurar as Regras de processamento do Analytics `props` conforme necessário.

### Regras de processamento para mapeamentos personalizados do Analytics

Neste exercício, você mapeia uma variável XDM para uma prop para que possa visualizá-la nos relatórios em tempo real. Siga estas mesmas etapas para qualquer mapeamento personalizado que precise ser feito para qualquer `eVar`, `prop`, `event`ou variável acessível por meio das Regras de processamento.

1. Na interface do usuário do Analytics, acesse [!UICONTROL Admin] > [!UICONTROL Ferramentas administrativas] > [!UICONTROL Conjuntos de relatórios]
1. Selecione o conjunto de relatórios de desenvolvimento/teste que você está usando para o tutorial > [!UICONTROL Editar configurações] > [!UICONTROL Geral] > [!UICONTROL Regras de processamento]

   ![Compra no Analytics](assets/analytics-process-rules.png)

1. Criar uma regra para **[!UICONTROL Substituir valor de]** `[!UICONTROL Product Name (prop1)]` para `a.x.productlistitems.0.name`. Lembre-se de adicionar a observação sobre o motivo de você estar criando a regra e nomear o título da regra. Selecionar **[!UICONTROL Salvar]**

   ![Compra no Analytics](assets/analytics-set-processing-rule.png)

   >[!IMPORTANT]
   >
   >Na primeira vez que você mapeia para uma regra de processamento, a interface do usuário não mostra as variáveis de dados de contexto do objeto XDM. Para corrigir isso, selecione qualquer valor, Salve e volte para editar. Todas as variáveis XDM agora devem aparecer.

1. Ir para [!UICONTROL Editar configurações] >  [!UICONTROL Tempo real]. Configure todos os três com os seguintes parâmetros mostrados abaixo para que você possa validar exibições de página de conteúdo, exibições de produtos e compras

   ![Compra no Analytics](assets/analytics-debugger-real-time.png)

1. Repita as etapas de validação e você verá que os relatórios em tempo real preenchem os dados adequadamente.

   **Exibições de página**
   ![Conteúdo em tempo real](assets/analytics-real-time-content.png)

   **Visualizações do produto**
   ![Visualizações de produto em tempo real](assets/analytics-real-time-prodView.png)

   **Compras**
   ![Compra em tempo real](assets/analytics-real-time-purchase.png)

1. Na interface do usuário do Workspace, crie uma tabela para visualizar o fluxo de comércio eletrônico completo do produto que você comprou

   ![Fluxo completo de comércio eletrônico](assets/analytics-workspace-ecommerce.png)

Para saber mais sobre como mapear campos XDM para variáveis do Analytics, consulte o vídeo [Mapear variáveis do SDK da Web no Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/analysis-use-cases/internal-site-search/map-web-sdk-variables-into-adobe-analytics.html).

Parabéns! Este é o fim da lição e agora você está pronto para implementar o Adobe Analytics com o SDK da Web da plataforma em seu próprio site.

[Próximo: ](setup-audience-manager.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
