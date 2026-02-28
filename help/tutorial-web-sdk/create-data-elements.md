---
title: Criar elementos de dados para o Platform Web SDK
description: Saiba como criar um objeto XDM e mapear elementos de dados para ele em tags. Esta lição é parte do tutorial Implementar a Adobe Experience Cloud com o SDK da web.
feature: Tags
jira: KT-15401
exl-id: d662ec46-de9b-44ba-974a-f81dfc842e68
source-git-commit: 1feddab414a8a7e49f04b8886c275d06516d0114
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 2%

---

# Criar elementos de dados

Saiba como criar elementos de dados em tags para dados de conteúdo, comércio e identidade no [site de demonstração Luma](https://newluma.enablementadobe.com). Em seguida, preencha os campos no esquema XDM com o tipo de elemento de dados Variável da extensão do Adobe Experience Platform Web SDK.



## Objetivos de aprendizagem

No final desta lição, você poderá:

* Entender diferentes abordagens para mapear uma camada de dados para o XDM
* Criar elementos de dados para capturar dados
* Mapear elementos de dados para um objeto XDM


## Pré-requisitos

Você entende o que é uma camada de dados e concluiu as lições anteriores no tutorial:

* [Configurar um esquema XDM](configure-schemas.md)
* [Configurar um namespace de identidade](configure-identities.md)
* [Configurar uma sequência de dados](configure-datastream.md)
* [Extensão do Web SDK instalada na propriedade da tag](install-web-sdk.md)


>[!IMPORTANT]
>
>Os dados para esta lição vêm da camada de dados `[!UICONTROL adobeDataLayer]` no site Luma. Para exibir a camada de dados, abra o console do desenvolvedor e digite `[!UICONTROL adobeDataLayer]` para ver a camada de dados completa disponível.![camada de dados adobeDataLayer](assets/data-element-data-layer-new.png)


## Abordagens da camada de dados

Há várias maneiras de mapear dados da camada de dados para o XDM usando a funcionalidade de tags do Adobe Experience Platform. Abaixo estão alguns prós e contras de três abordagens diferentes. É possível combinar abordagens, se desejado:

1. Implementar o XDM na camada de dados
1. Mapear para XDM em tags
1. Mapear para XDM no fluxo de dados

>[!NOTE]
>
>Os exemplos neste tutorial seguem a abordagem Mapear para XDM em tags.


### Implementar o XDM na camada de dados

Essa abordagem envolve o uso do objeto XDM totalmente definido como a estrutura da camada de dados. Em seguida, mapeie toda a camada de dados para um elemento de dados de objeto XDM nas tags. Se sua implementação não estiver usando um gerenciador de tags, essa abordagem poderá ser ideal, pois você pode enviar dados para o XDM diretamente do seu aplicativo usando o [comando sendEvent do XDM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/edge/fundamentals/tracking-events#sending-xdm-data). Se você usar tags, poderá criar um elemento de dados de código personalizado capturando toda a camada de dados como um objeto JSON de passagem para o XDM. Em seguida, mapeie o JSON de passagem para o campo do objeto XDM na Ação Enviar evento.

Veja abaixo um exemplo de como a camada de dados seria usada com o formato da Camada de dados do cliente Adobe:

+++Exemplo de XDM na camada de dados

```JSON
window.adobeDataLayer.push({
"eventType": "web.webPageDetails.pageViews",
"web":{
         "webInteraction":{
            "linkClicks":{
               "id":"",
               "value":""
            },
            "URL":"",
            "name":"",
            "region":"",
            "type":""
         },
         "webPageDetails":{
            "pageViews":{
               "id":"",
               "value":"1"
            },
            "URL":"https://newluma.enablementadobe.com/",
            "isErrorPage":"",
            "isHomePage":"",
            "name":"luma:home",
            "server":"enablementadobe.com",
            "siteSection":"home",
            "viewName":""
         },
         "webReferrer":{
            "URL":"",
            "type":""
         }
      }
});
```

+++

Pontos positivos

* Elimina etapas adicionais de remapeamento de variáveis de camada de dados para o XDM
* A implantação pode ser mais rápida se a sua equipe de desenvolvimento na Web também tiver um recurso de marcação de comportamento digital

Pontos negativos

* Confiança total na equipe de desenvolvimento e no ciclo de desenvolvimento para atualizar quais dados vão para o XDM
* Flexibilidade limitada, pois o XDM recebe a carga exata da camada de dados
* Não é possível usar recursos de tags incorporadas, como recursos de raspagem, persistência e implantação rápida
* É mais difícil usar a camada de dados para pixels de terceiros (mas convém mover esses pixels para [encaminhamento de eventos](setup-event-forwarding.md)!
* Não há capacidade de transformar os dados entre a camada de dados e o XDM

### Mapear a camada de dados nas tags

Essa abordagem envolve o mapeamento de variáveis de camada de dados individuais OU objetos de camada de dados para elementos de dados em tags e, por fim, para o XDM. Essa é a abordagem tradicional de implementação usando um sistema de gerenciamento de tags.

#### Pontos positivos

* A abordagem mais flexível, pois você pode controlar variáveis individuais e transformar dados antes que eles cheguem ao XDM
* Pode usar acionadores de tags da Adobe e a funcionalidade de refugo para transmitir dados ao XDM
* Pode mapear elementos de dados para pixels de terceiros no lado do cliente

#### Pontos negativos

* Demora para reconstruir a camada de dados como elementos de dados


>[!TIP]
>
> Camada de dados Google
> 
> Se sua organização já usa a Google Analytics e tem o objeto tradicional dataLayer da Google em seu site, você pode usar a [extensão de Camada de Dados da Google](https://experienceleague.adobe.com/pt-br/docs/experience-platform/tags/extensions/client/google-data-layer/overview) nas tags. Isso permite implantar a tecnologia Adobe mais rapidamente, sem precisar solicitar suporte da sua equipe de TI. O mapeamento da camada de dados do Google para o XDM seguiria as mesmas etapas descritas acima.

### Mapear para XDM no fluxo de dados

Essa abordagem usa uma funcionalidade integrada à configuração de sequência de dados chamada [Preparação de Dados para Coleta de Dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/datastreams/data-prep) e ignora o mapeamento de variáveis de camada de dados para XDM nas marcas.

#### Pontos positivos

* Flexível, pois é possível mapear variáveis individuais para o XDM
* Capacidade de [calcular novos valores](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-prep/functions) ou [transformar tipos de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-prep/data-handling) a partir de uma camada de dados antes que ela vá para o XDM
* Aproveite uma [Interface do usuário de mapeamento](https://experienceleague.adobe.com/pt-br/docs/experience-platform/datastreams/data-prep#create-mapping) para mapear campos nos dados de origem para o XDM com uma interface do tipo apontar-e-clicar

#### Pontos negativos

* Não é possível usar variáveis de camada de dados como elementos de dados para pixels de terceiros do lado do cliente, mas você pode usá-las com o encaminhamento de eventos
* Não é possível usar a funcionalidade de reaproveitamento do recurso de tags do Adobe Experience Platform
* A complexidade de manutenção aumenta se o mapeamento da camada de dados for feito em tags e na sequência de dados



>[!IMPORTANT]
>
>Como observado anteriormente, os exemplos neste tutorial seguem a abordagem Mapear para XDM em tags.

## Criar elementos de dados para capturar a camada de dados

Antes de criar o objeto XDM, crie o seguinte conjunto de elementos de dados para a camada de dados do [site de demonstração Luma](https://newluma.enablementadobe.com){target="_blank"}:

1. Vá para **[!UICONTROL Elementos de Dados]** e selecione **[!UICONTROL Adicionar Elemento de Dados]** (ou **[!UICONTROL Criar Novo Elemento de Dados]** se não houver elementos de dados existentes na propriedade de marca)

   ![Criar Elemento de Dados](assets/data-element-create.png)

1. Nomeie o elemento de dados `Page Name`
1. Use a **[!UICONTROL Variável JavaScript]** **[!UICONTROL Tipo de elemento de dados]** para apontar para um valor na camada de dados da Luma: `adobeDataLayer.0.page.name`

1. Marque as caixas **[!UICONTROL Forçar valor minúsculo]** e **[!UICONTROL Limpar texto]** para padronizar o caso e remover espaços irrelevantes

1. Deixe `None` como a configuração de **[!UICONTROL Duração do Armazenamento]**, pois esse valor é diferente em cada página

1. Selecione **[!UICONTROL Salvar]**

   ![Elemento de dados do nome da página](assets/data-element-pageName.png)

Crie esses elementos de dados adicionais seguindo as mesmas etapas:

* **`User Id`** mapeado para
  `adobeDataLayer.0.user.id`

* **`User Logged In`** mapeado para
  `adobeDataLayer.0.user.loggedIn`

* **`Ecommerce Product Id`** mapeado para `adobeDataLayer.0.ecommerce.detail.products.0.id`
* **`Ecommerce Product Name`** mapeado para `adobeDataLayer.0.ecommerce.detail.products.0.name`
* **`Ecommerce Purchase Id`** mapeado para `adobeDataLayer.0.ecommerce.purchase.actionField.id`
* **`Ecommerce Product Category`** usando o **[!UICONTROL Código personalizado]** **[!UICONTROL Tipo de elemento de dados]** e o seguinte código personalizado:

  ```javascript
  return adobeDataLayer[0].ecommerce.detail.products[0].category+":"+adobeDataLayer[0].ecommerce.detail.products[0].subcategory;
  ```

* **`Ecommerce Cart Products`** usando o seguinte código personalizado:

  ```javascript
  const cartProducts = adobeDataLayer
  .flatMap(evt => Array.isArray(evt?.ecommerce?.cart?.items) ? evt.ecommerce.cart.items : [])
  .filter(item => item && item.id && item.name && item.brand)
  .map(({ id, name, brand }) => ({ id, name, brand }));
  
  return cartProducts;
  ```

* **`Ecommerce Checkout Products`** usando o seguinte código personalizado:

  ```javascript
  const checkoutProducts = adobeDataLayer
  .flatMap(evt => Array.isArray(evt?.ecommerce?.checkout?.products) ? evt.ecommerce.checkout.products : [])
  .filter(item => item && item.id && item.name && item.brand)
  .map(({ id, name, brand }) => ({ id, name, brand }));
  
  return checkoutProducts;
  ```


>[!CAUTION]
>
>O tipo de elemento de dados [!UICONTROL variável JavaScript] trata referências de matriz como pontos em vez de colchetes, portanto, referenciar o elemento de dados username como `adobeDataLayer[0].page.name` **não funcionará**.

## Criar elementos de dados variáveis para XDM e objetos de dados

Os elementos de dados que você acabou de criar serão usados para criar um objeto XDM (para aplicativos da Platform) e um objeto de dados (para o Analytics, Target e Audience Manager). Esses objetos têm seus próprios elementos de dados especiais chamados elementos de dados **[!UICONTROL Variável]**, que são muito fáceis de criar.

Para criar o elemento de dados Variable para XDM, vincule-o ao esquema criado na lição [Configurar um esquema](configure-schemas.md):

1. Selecione **[!UICONTROL Adicionar elemento de dados]**
1. Nomeie seu Elemento de Dados `XDM Variable`. Recomenda-se adicionar um prefixo &quot;xdm&quot; aos Elementos de dados específicos do XDM para organizar melhor a propriedade da tag
1. Selecione a **[!UICONTROL Adobe Experience Platform Web SDK]** como a **[!UICONTROL Extensão]**
1. Selecione a **[!UICONTROL Variável]** como o **[!UICONTROL Tipo de Elemento de Dados]**
1. Selecione **[!UICONTROL XDM]** como a **[!UICONTROL propriedade]**
1. Selecione a **[!UICONTROL Sandbox]** em que você criou o esquema
1. Selecione o **[!UICONTROL Esquema]** apropriado, neste caso `Luma Web Event Data`
1. Selecione **[!UICONTROL Salvar]**

   ![Elemento de dados de variável para XDM](assets/analytics-tags-data-element-xdm-variable.png)

Em seguida, crie o elemento de dados Variable para seu objeto de dados:

1. Selecione **[!UICONTROL Adicionar elemento de dados]**
1. Nomeie seu Elemento de Dados `Data Variable`.
1. Selecione a **[!UICONTROL Adobe Experience Platform Web SDK]** como a **[!UICONTROL Extensão]**
1. Selecione a **[!UICONTROL Variável]** como o **[!UICONTROL Tipo de Elemento de Dados]**
1. Selecione **[!UICONTROL dados]** como a **[!UICONTROL propriedade]**
1. Selecione as soluções da Experience Cloud que deseja implementar como parte deste tutorial
1. Selecione **[!UICONTROL Salvar]**

   ![Elemento de dados de variável para o objeto de dados](assets/data-element-data-variable.png)


Ao final dessas etapas, você deve ter os seguintes elementos de dados criados:

| Elementos de dados da extensão principal | Elementos de dados da extensão do Platform Web SDK |
-----------------------------|-------------------------------
| `Ecommerce Cart Products` | `Data Variable` |
| `Ecommerce Checkout Products` | `XDM Variable` |
| `Ecommerce Checkout Products` | |
| `Ecommerce Product Category` | |
| `Ecommerce Product Id` | |
| `Ecommerce Product Name` | |
| `Ecommerce Purchase Id` | |
| `Page Name` | |
| `User Id` | |
| `User Logged In` | |

Com esses elementos de dados implementados, você estará pronto para começar a enviar dados para o Platform Edge Network com uma regra de tags. Mas primeiro, saiba como coletar identidades com o Web SDK.

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [postagem de discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/adobe-experience-platform-18/tutorial-discussion-implement-adobe-experience-cloud-with-web-sdk-tutorial-248848?profile.language=pt)
