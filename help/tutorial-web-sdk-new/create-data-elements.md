---
title: Criar elementos de dados
description: Saiba como criar um objeto XDM e mapear elementos de dados para ele em tags. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Tags
source-git-commit: 695c12ab66df33af00baacabc3b69eaac7ada231
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 1%

---

# Criar elementos de dados

Saiba como criar os elementos de dados essenciais necessários para capturar dados com o SDK da Web do Experience Platform. Capturar dados de conteúdo e de identidade no [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Saiba como usar o esquema XDM criado anteriormente para coletar dados usando o SDK da Web da plataforma por meio de um novo elemento de dados chamado Objeto XDM.

>[!NOTE]
>
> Para fins de demonstração, os exercícios desta lição baseiam-se no exemplo usado durante [Configurar um esquema](configure-schemas.md) etapa; criação de objetos XDM de exemplo que capturam o conteúdo visualizado e as identidades dos usuários na [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html).

>[!IMPORTANT]
>
>Os dados para esta lição vêm do `[!UICONTROL digitalData]` camada de dados no site Luma. Para visualizar a camada de dados, abra o console do desenvolvedor e digite `[!UICONTROL digitalData]` para ver a camada de dados completa disponível.![camada de dados digitalData](assets/data-element-data-layer.png)


Independentemente do SDK da Web da Platform, você deve continuar criando elementos de dados dentro da propriedade de tag que mapeiam para variáveis de coleção de dados do seu site, como uma camada de dados, atributo HTML ou outros. Depois de criar esses elementos de dados, você deve mapeá-los para o esquema XDM criado durante o [configurar schemas](configure-schemas.md) lição. Para fazer isso, a extensão SDK da Web da Platform disponibiliza um novo tipo de elemento de dados chamado objeto XDM. Portanto, a criação de elementos de dados consiste em duas ações:

1. Mapear variáveis de site para elementos de dados e
1. Mapeamento desses elementos de dados para um objeto XDM

Para a etapa 1, você continua a mapear a camada de dados para elementos de dados da maneira que faz no momento, usando qualquer um dos tipos de elementos de dados da extensão de tag principal. Para a etapa 2, a extensão SDK da Web da Platform cria um conjunto de novos tipos de elementos de dados que não estavam disponíveis anteriormente:

* ID de mesclagem de eventos
* Mapa de identidade
* Objeto XDM

Esta lição se concentra nos tipos de objetos XDM e elementos de dados do mapa de identidade. Você criará objetos XDM para capturar a atividade e o status de autenticação dos visitantes do Luma.

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Criar elementos de dados para capturar conteúdo e dados de ID de logon do usuário
* Criar um elemento de dados do mapa de identidade
* Mapear elementos de dados para um elemento de dados de objeto XDM


## Pré-requisitos

Você entende o que é uma camada de dados, familiarizado com o [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} camada de dados e saiba como fazer referência a elementos de dados em tags. Você deve ter concluído as seguintes etapas anteriores no tutorial

* [Configurar permissões](configure-permissions.md)
* [Configurar um esquema XDM](configure-schemas.md)
* [Configurar um namespace de identidade](configure-identities.md)
* [Configurar uma sequência de dados](configure-datastream.md)
* [Extensão SDK da Web instalada na propriedade da tag](install-web-sdk.md)

>[!IMPORTANT]
>
>A variável [Extensão do Experience Cloud ID Service](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) não é necessário ao implementar o SDK da Web da Adobe Experience Platform, pois a funcionalidade do Serviço de ID é incorporada no SDK da Web da plataforma.

## Criar elementos de dados para capturar a camada de dados

Antes de começar a criar o objeto XDM, crie o seguinte conjunto de elementos de dados mapeando para o [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} camada de dados:

1. Ir para **[!UICONTROL Elementos de dados]** e selecione **[!UICONTROL Adicionar elemento de dados]** (ou **[!UICONTROL Criar novo elemento de dados]** se não houver elementos de dados existentes na propriedade tag )

   ![Criar elemento de dados](assets/data-element-create.jpg)

1. Nomeie o elemento de dados `page.pageInfo.pageName`
1. Use o **[!UICONTROL Variável JavaScript]** **[!UICONTROL Tipo de elemento de dados]** para apontar para um valor na camada de dados do Luma: `digitalData.page.pageInfo.pageName`

1. Marque as caixas para **[!UICONTROL Forçar valor de minúsculas]** e **[!UICONTROL Texto limpo]** para padronizar o caso e remover espaços irrelevantes

1. Sair `None` como o **[!UICONTROL Duração do armazenamento]** já que esse valor é diferente em cada página

1. Selecionar **[!UICONTROL Salvar]**

   ![Elemento de dados do nome da página](assets/data-element-pageName.jpg)

Siga as mesmas etapas para criar esses quatro elementos de dados adicionais:

* **`page.pageInfo.server`**  mapeado para
  `digitalData.page.pageInfo.server`

* **`page.pageInfo.hierarchie1`**  mapeado para
  `digitalData.page.pageInfo.hierarchie1`

* **`user.profile.attributes.username`**  mapeado para
  `digitalData.user.0.profile.0.attributes.username`

* **`user.profile.attributes.loggedIn`** mapeado para
  `digitalData.user.0.profile.0.attributes.loggedIn`

* **`cart.orderId`** mapeado para `digitalData.cart.orderId` (você usará isso durante o [Configurar o Analytics](setup-analytics.md) lição)


>[!CAUTION]
>
>A variável [!UICONTROL Variável JavaScript] o tipo de elemento de dados trata as referências de matriz como pontos em vez de colchetes, de modo que fazer referência ao elemento de dados username como `digitalData.user[0].profile[0].attributes.username` **não funcionará**.

## Criar elemento de dados do Mapa de identidade

Em seguida, você pode criar o elemento de dados Mapa de identidade:

1. Ir para **[!UICONTROL Elementos de dados]** e selecione **[!UICONTROL Adicionar elemento de dados]**

1. **[!UICONTROL Nome]** o elemento de dados `identityMap.loginID`

1. Como a variável **[!UICONTROL Extensão]**, selecione `Adobe Experience Platform Web SDK`

1. Como a variável **[!UICONTROL Tipo de elemento de dados]**, selecione `Identity map`

1. Isso solicita uma área de tela à direita dentro da **[!UICONTROL Interface da coleção de dados]** para configurar a identidade:

   ![Interface da coleção de dados](assets/identity-identityMap-setup.png)

1. Como a variável  **[!UICONTROL Namespace]**, selecione o `Luma CRM Id` que você criou anteriormente na variável [Configurar identidades](configure-identities.md) lição.

   >[!NOTE]
   >
   >    Se você não vir o seu `Luma CRM Id` , verifique se você também o criou na sandbox de produção padrão. Atualmente, somente os namespaces criados na sandbox de produção padrão são exibidos na lista suspensa namespace.

1. Depois que a variável **[!UICONTROL Namespace]** for selecionada, uma ID deverá ser definida. Selecione o `user.profile.attributes.username` elemento de dados criado anteriormente nesta lição, que captura uma ID quando os usuários são conectados ao site Luma.

<!--  >[!TIP]
   >
   >You can verify the **[!UICONTROL Luma CRM ID]** is collected in a data element on the web property by going to the [Luma Demo site](https://luma.enablementadobe.com/content/luma/us/en.html), logging in, [switching the tag environment](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) to your own, and typing `_satellite.getVar("user.profile.attributes.username")` in the web browser developer console.
   >
   >   ![Data Element  ID ](assets/identity-data-element-customer-id.png)
-->

1. Como a variável **[!UICONTROL Estado autenticado]**, selecione **[!UICONTROL Autenticado]**
1. Selecionar **[!UICONTROL Principal]**

1. Selecionar **[!UICONTROL Salvar]**

   ![Interface da coleção de dados](assets/identity-id-namespace.png)

>[!TIP]
>
> Adobe recomenda enviar identidades que representam uma pessoa, como `Luma CRM Id`, como a [!UICONTROL principal] identidade.
>
> Se o mapa de identidade contiver o identificador de pessoa (por exemplo, `Luma CRM Id`), o identificador de pessoa se tornará o [!UICONTROL principal] identidade. Caso contrário, `ECID` torna-se o [!UICONTROL principal] identidade.





<!--
1. Once the data element is configured in **[!UICONTROL Data Collection interface]**, it can be tested on the Luma web property like any other Data Element. Enter the following script in the browser developer console
   
   
   ```
   _satellite.getVar('identityMap.loginID')
   ```  

   ![Data Collection interface](assets/identity-consoleIdentityDataElement.png)
   
   >[!NOTE]
   >
   >ECID identifier will NOT populate in the Data Element, as this is configured already with Platform Web SDK.   
-->

## Mapear elementos de dados para objetos XDM

Todos os elementos de dados criados devem ser mapeados para um objeto XDM. Esse objeto deve estar em conformidade com o esquema XDM criado durante o [Configurar um esquema](configure-schemas.md) lição.

Há diferentes maneiras de mapear elementos de dados para campos de objeto XDM. Você pode mapear elementos de dados individuais para campos XDM individuais ou mapear elementos de dados para objetos XDM inteiros, desde que seu elemento de dados corresponda ao esquema de par de valor-chave exato presente no objeto XDM. Nesta lição, você capturará os dados de conteúdo mapeando para campos individuais. Você aprenderá a [mapear um elemento de dados para um objeto XDM inteiro](setup-analytics.md#Map-an-entire-array-to-an-XDM-Object) no [Configurar o Analytics](setup-analytics.md) lição.

Crie um objeto XDM para capturar dados de conteúdo:

1. Na navegação à esquerda, selecione **[!UICONTROL Elementos de dados]**
1. Selecionar **[!UICONTROL Adicionar elemento de dados]**
1. **[!UICONTROL Nome]** o elemento de dados **`xdm.content`**
1. Como a variável **[!UICONTROL Extensão]** selecionar `Adobe Experience Platform Web SDK`
1. Como a variável **[!UICONTROL Tipo de elemento de dados]** selecionar `XDM object`
1. Selecione a plataforma **[!UICONTROL Sandbox]** no qual você criou o esquema XDM no durante o [Configurar um esquema XDM](configure-schemas.md) lição, neste exemplo `DEVELOPMENT Mobile and Web SDK Courses`
1. Como a variável **[!UICONTROL Esquema]**, selecione o `Luma Web Event Data` esquema:

   ![Objeto XDM](assets/data-element-xdm.content-fields.png)

   >[!NOTE]
   >
   >A sandbox corresponde à sandbox Experience Platform em que você criou o esquema. Pode haver várias sandboxes disponíveis na instância do Experience Platform, portanto, selecione a correta. Sempre trabalhe em desenvolvimento primeiro, depois em produção.

1. Role para baixo até alcançar a **`web`** objeto
1. Selecione para abri-lo

   ![Objeto da Web](assets/data-element-pageviews-xdm-object.png)


1. Mapear as seguintes variáveis XDM da Web para elementos de dados

   * **`web.webPageDetials.name`** para `%page.pageInfo.pageName%`
   * **`web.webPageDetials.server`** para `%page.pageInfo.server%`
   * **`web.webPageDetials.siteSection`** para `%page.pageInfo.hierarchie1%`

   ![Objeto XDM](assets/data-element-xdm.content.png)

1. Em seguida, localize o `identityMap` no esquema e selecione-o

1. Mapear para o `identityMap.loginID` elemento de dados

1. Selecionar **[!UICONTROL Salvar]**

   ![Interface da coleção de dados](assets/identity-dataElements-xdmContent-LumaSchema-identityMapSelect3.png)




Ao final dessas etapas, você deve ter os seguintes elementos de dados criados:

| Elementos de dados da extensão CORE | Elementos de dados do SDK da Web da plataforma |
-----------------------------|-------------------------------
| `cart.orderId` | `identityMap.loginID` |
| `page.pageInfo.hierarchie1` | `xdm.content` |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |

Com esses elementos de dados implementados, você estará pronto para começar a enviar dados para a Platform Edge Network por meio do objeto XDM criando uma regra nas tags.

[Próximo: ](create-tag-rule.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
