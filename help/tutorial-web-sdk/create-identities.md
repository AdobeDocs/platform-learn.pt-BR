---
title: Criar identidades para o SDK da Web da plataforma
description: Saiba como criar identidades no XDM e usar o elemento de dados do Mapa de identidade para capturar IDs de usuários. Esta lição é parte do tutorial Implementar a Adobe Experience Cloud com o SDK da web.
feature: Web SDK, Tags, Identities
jira: KT-15402
exl-id: 7ca32dc8-dd86-48e0-8931-692bcbb2f446
source-git-commit: a8431137e0551d1135763138da3ca262cb4bc4ee
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 3%

---

# Criar identidades

Saiba como capturar identidades com o SDK da web da Adobe Experience Platform. Capture dados de identidade não autenticados e autenticados no [site de demonstração do Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Saiba como usar os elementos de dados criados anteriormente para coletar dados autenticados com um tipo de elemento de dados do SDK da Web da plataforma chamado de Mapa de identidade.

Esta lição se concentra no elemento de dados do Mapa de identidade disponível com a extensão de tags do SDK da Web da Adobe Experience Platform. Você mapeia elementos de dados contendo uma ID de usuário autenticada e um status de autenticação para o XDM.

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Entenda a relação entre a Experience Cloud ID (ECID) e a First Party Device ID (FPID)
* Entender a diferença entre IDs não autenticadas e autenticadas
* Criar um elemento de dados do mapa de identidade

## Pré-requisitos

Você entende o que é uma camada de dados, familiarizou-se com a camada de dados [site de demonstração do Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} e sabe como fazer referência a elementos de dados em tags. Você deve ter concluído as lições anteriores no tutorial:

* [Configurar um esquema XDM](configure-schemas.md)
* [Configurar um namespace de identidade](configure-identities.md)
* [Configurar uma sequência de dados](configure-datastream.md)
* [Extensão SDK da Web instalada na propriedade da tag](install-web-sdk.md)
* [Criar elementos de dados](create-data-elements.md)


## Experience Cloud ID

A [ID de Experience Cloud (ECID)](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/features/ecid) é um namespace de identidade compartilhada usado em aplicativos Adobe Experience Platform e Adobe Experience Cloud. A ECID fornece a base para a identidade do cliente e é a identidade padrão para propriedades digitais. A ECID é o identificador ideal para rastrear comportamentos de usuários não autenticados, pois está sempre presente.

<!-- FYI I commented this out because it was breaking the build - Jack
>[!TIP]
>
> When you use the Experience Platform Web SDK to set up Adobe applications on your digital properties, the ECID is generated at the Adobe Edge server level. As such, ECID is not viewable on the client-side network request payload. You can view the ECID by seeing the Preview tab of the network request, or by using the [Adobe Experience Platform Debugger Edge Trace](set-up-analytics.md#experience-cloud-id-validation).
>![View ECID](assets/validate-dev-console-ecid.png)
-->

Leia mais sobre como [ECIDs são rastreados usando o SDK da Web da plataforma](https://experienceleague.adobe.com/en/docs/experience-platform/edge/identity/overview).

As ECIDs são definidas usando uma combinação de cookies primários e Edge Network da plataforma. Por padrão, os cookies de identidade primários são definidos no lado do cliente pelo SDK da Web. Para levar em conta as restrições do navegador na duração do cookie, você pode optar por definir seus próprios cookies de identidade primários no lado do servidor. Esses cookies de identidade são chamados de IDs de dispositivo primário (FPIDs).

>[!IMPORTANT]
>
>A [extensão do Serviço de ID do Experience Cloud](https://exchange.adobe.com/apps/ec/100160/adobe-experience-cloud-id-launch-extension) não é necessária ao implementar o SDK da Web da Adobe Experience Platform, pois a funcionalidade do Serviço de ID é incorporada no SDK da Web da plataforma.

## ID de dispositivo próprio (FPID)

FPIDs são cookies próprios _você definiu usando seus próprios servidores da Web_, que o Adobe usa para criar a ECID, em vez de usar o cookie próprio definido pelo SDK da Web. Embora o suporte ao navegador possa variar, os cookies primários tendem a ser mais duráveis quando definidos por um servidor que aproveita um registro DNS A (para IPv4) ou registro AAAA (para IPv6), em vez de quando definidos por um código DNS CNAME ou JavaScript.

Depois que um cookie FPID é definido, seu valor pode ser buscado e enviado para o Adobe conforme os dados do evento são coletados. Os FPIDs coletados são usados como seeds para gerar ECIDs no Platform Edge Network, que continuam a ser os identificadores padrão nos aplicativos Adobe Experience Cloud.

Embora os FPIDs não sejam usados neste tutorial, é recomendável usar os FPIDs na implementação do SDK da Web. Leia mais sobre [IDs de dispositivo próprio no SDK da Web da plataforma](https://experienceleague.adobe.com/en/docs/experience-platform/edge/identity/first-party-device-ids)

>[!CAUTION]
>
> O FPID é uma maneira alternativa de gerar a ECID usando um cookie definido pelos servidores da Web. Não é usado para identificar usuários autenticados.

## ID autenticada

Como observado acima, todos os visitantes das suas propriedades digitais recebem uma ECID por Adobe ao usar o SDK da Web da plataforma. A ECID é a identidade padrão para rastrear comportamentos digitais não autenticados.

Você também pode enviar uma ID de usuário autenticada para que a Platform possa criar [Gráficos de identidade](https://experienceleague.adobe.com/pt-br/docs/platform-learn/tutorials/identities/understanding-identity-and-identity-graphs) e o Target possa definir sua [ID de terceiros](https://experienceleague.adobe.com/pt-br/docs/target/using/audiences/visitor-profiles/3rd-party-id). A definição da ID autenticada é feita usando o tipo de elemento de dados [!UICONTROL Mapa de Identidade].

Para criar o elemento de dados [!UICONTROL Mapa de Identidade]:

1. Vá para **[!UICONTROL Elementos de Dados]** e selecione **[!UICONTROL Adicionar Elemento de Dados]**

1. **[!UICONTROL Nomeie]** o Elemento de Dados `identityMap.loginID`

1. Como a **[!UICONTROL Extensão]**, selecione `Adobe Experience Platform Web SDK`

1. Como o **[!UICONTROL Tipo de Elemento de Dados]**, selecione `Identity map`

1. Isso solicita uma área de tela à direita na **[!UICONTROL interface da Coleção de Dados]** para que você configure a identidade:

   ![Interface de coleção de dados](assets/identity-identityMap-setup.png)

1. Como o **[!UICONTROL Namespace]**, selecione o namespace `lumaCrmId` que você criou anteriormente na lição [Configurar Identidades](configure-identities.md). Se não aparecer na lista suspensa, digite-o.

1. Depois que o **[!UICONTROL Namespace]** for selecionado, uma ID deverá ser definida. Selecione o elemento de dados `user.profile.attributes.username` criado anteriormente na lição [Criar elementos de dados](create-data-elements.md#create-data-elements-to-capture-the-data-layer), que captura uma ID quando os usuários estão conectados ao site Luma.

   <!--  >[!TIP]
    >
    >You can verify the **[!UICONTROL Luma CRM ID]** is collected in a data element on the web property by going to the [Luma Demo site](https://luma.enablementadobe.com/content/luma/us/en.html), logging in, [switching the tag environment](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) to your own, and typing `_satellite.getVar("user.profile.attributes.username")` in the web browser developer console.
    >
    >   ![Data Element  ID ](assets/identity-data-element-customer-id.png)
    -->

1. Como o **[!UICONTROL estado autenticado]**, selecione **[!UICONTROL Autenticado]**
1. Selecionar **[!UICONTROL Principal]**

1. Selecione **[!UICONTROL Salvar]**

   ![Interface de coleção de dados](assets/identity-id-namespace.png)

>[!TIP]
>
> A Adobe recomenda enviar identidades que representem uma pessoa, como `Luma CRM Id`, como a identidade [!UICONTROL principal].
>
> Se o mapa de identidade contiver o identificador de pessoa (por exemplo, `Luma CRM Id`), o identificador de pessoa se tornará a identidade [!UICONTROL principal]. Caso contrário, `ECID` se tornará a identidade [!UICONTROL primária].




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

Ao final dessas etapas, você deve ter os seguintes elementos de dados criados:

| Elementos de dados da extensão principal | Elementos de dados da extensão SDK da Web da plataforma |
-----------------------------|-------------------------------
| `cart.orderId` | `data.variable` |
| `cart.productInfo` | `identityMap.loginID` |
| `cart.productInfo.purchase` | `xdm.variable.content` |
| `page.pageInfo.hierarchie1` | |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `product.category` | |
| `product.productInfo.sku` | |
| `product.productInfo.title` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |

Com esses elementos de dados implementados, você estará pronto para começar a enviar dados para o Platform Edge Network criando uma regra nas tags.

[Próximo: ](create-tag-rule.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [postagem de Discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=pt)
