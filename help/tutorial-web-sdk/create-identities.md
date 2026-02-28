---
title: Criar identidades para o Platform Web SDK
description: Saiba como criar identidades no XDM e usar o elemento de dados do Mapa de identidade para capturar IDs de usuários. Esta lição é parte do tutorial Implementar a Adobe Experience Cloud com o SDK da web.
feature: Web SDK, Tags, Identities
jira: KT-15402
exl-id: 7ca32dc8-dd86-48e0-8931-692bcbb2f446
source-git-commit: 1feddab414a8a7e49f04b8886c275d06516d0114
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 3%

---

# Criar identidades

Saiba como capturar identidades com o SDK da web da Adobe Experience Platform. Capture dados de identidade não autenticados e autenticados no [site de demonstração do Luma](https://newluma.enablementadobe.com). Saiba como usar os elementos de dados criados anteriormente para coletar dados autenticados com um tipo de elemento de dados do Platform Web SDK chamado Mapa de identidade.

Esta lição se concentra no elemento de dados do Mapa de identidade disponível com a extensão de tags da Adobe Experience Platform Web SDK. Você mapeia elementos de dados contendo uma ID de usuário autenticada e um status de autenticação para o XDM.



## Objetivos de aprendizagem

No final desta lição, você poderá:

* Entenda a relação entre a Experience Cloud ID (ECID) e a ID de dispositivo próprio (FPID)
* Entender a diferença entre IDs não autenticadas e autenticadas
* Criar um elemento de dados do mapa de identidade

## Pré-requisitos

Você entende o que é uma camada de dados, se familiarizou com a camada de dados do [site de demonstração do Luma](https://newluma.enablementadobe.com){target="_blank"} e sabe como fazer referência a elementos de dados em tags. Você deve ter concluído as lições anteriores no tutorial:

* [Configurar um esquema XDM](configure-schemas.md)
* [Configurar um namespace de identidade](configure-identities.md)
* [Configurar uma sequência de dados](configure-datastream.md)
* [Extensão do Web SDK instalada na propriedade da tag](install-web-sdk.md)
* [Criar elementos de dados](create-data-elements.md)


## Experience Cloud ID

A [Experience Cloud ID (ECID)](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/features/ecid) é um namespace de identidade compartilhada usado em aplicativos Adobe Experience Platform e Adobe Experience Cloud. A ECID fornece a base para a identidade do cliente e é a identidade padrão para propriedades digitais. A ECID é o identificador ideal para rastrear comportamentos de usuários não autenticados, pois está sempre presente.

<!-- FYI I commented this out because it was breaking the build - Jack
>[!TIP]
>
> When you use the Experience Platform Web SDK to set up Adobe applications on your digital properties, the ECID is generated at the Adobe Edge server level. As such, ECID is not viewable on the client-side network request payload. You can view the ECID by seeing the Preview tab of the network request, or by using the [Adobe Experience Platform Debugger Edge Trace](set-up-analytics.md#experience-cloud-id-validation).
>![View ECID](assets/validate-dev-console-ecid.png)
-->

Leia mais sobre como [ECIDs são rastreados usando o Platform Web SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/edge/identity/overview).

As ECIDs são definidas usando uma combinação de cookies primários e do Platform Edge Network. Por padrão, os cookies de identidade primários são definidos no lado do cliente pelo Web SDK. Para levar em conta as restrições do navegador na duração do cookie, você pode optar por definir seus próprios cookies de identidade primários no lado do servidor. Esses cookies de identidade são chamados de IDs de dispositivo primário (FPIDs).

>[!IMPORTANT]
>
>A [extensão do Experience Cloud ID Service](https://exchange.adobe.com/apps/ec/100160/adobe-experience-cloud-id-launch-extension) não é necessária ao implementar o Adobe Experience Platform Web SDK, pois a funcionalidade do Serviço de ID é incorporada ao Platform Web SDK.

## ID de dispositivo próprio (FPID)

FPIDs são cookies próprios _você definiu usando seus próprios servidores da Web_, que o Adobe usa para criar a ECID, em vez de usar o cookie próprio definido pela Web SDK. Embora o suporte ao navegador possa variar, os cookies primários tendem a ser mais duráveis quando definidos por um servidor que aproveita um registro DNS A (para IPv4) ou registro AAAA (para IPv6), em vez de quando definidos por um código DNS CNAME ou JavaScript.

Depois que um cookie FPID é definido, seu valor pode ser buscado e enviado para o Adobe à medida que os dados do evento são coletados. Os FPIDs coletados são usados como seeds para gerar ECIDs no Platform Edge Network, que continuam a ser os identificadores padrão nos aplicativos Adobe Experience Cloud.

Embora os FPIDs não sejam usados neste tutorial, é recomendável usar os FPIDs na implementação de seu próprio Web SDK. Leia mais sobre [IDs de dispositivo próprio no Platform Web SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/edge/identity/first-party-device-ids)

>[!CAUTION]
>
> O FPID é uma maneira alternativa de gerar a ECID usando um cookie definido pelos servidores da Web. Não é usado para identificar usuários autenticados.

## ID autenticada

Como observado acima, todos os visitantes das suas propriedades digitais recebem uma ECID da Adobe ao usar o Platform Web SDK. A ECID é a identidade padrão para rastrear comportamentos digitais não autenticados.

Você também pode enviar uma ID de usuário autenticada para que a Platform possa criar [Gráficos de identidade](https://experienceleague.adobe.com/pt-br/docs/platform-learn/tutorials/identities/understanding-identity-and-identity-graphs) e o Target possa definir sua [ID de terceiros](https://experienceleague.adobe.com/pt-br/docs/target/using/audiences/visitor-profiles/3rd-party-id). A definição da ID autenticada é feita usando o tipo de elemento de dados [!UICONTROL Mapa de Identidade].

Para criar o elemento de dados [!UICONTROL Mapa de Identidade]:

1. Vá para **[!UICONTROL Elementos de Dados]** e selecione **[!UICONTROL Adicionar Elemento de Dados]**

1. **[!UICONTROL Nomeie]** o Elemento de Dados `Identity Map`

1. Como a **[!UICONTROL Extensão]**, selecione `Adobe Experience Platform Web SDK`

1. Como o **[!UICONTROL Tipo de Elemento de Dados]**, selecione `Identity map`

1. Como o **[!UICONTROL Namespace]**, selecione o namespace `lumaCrmId` criado na lição [Configurar Identidades](configure-identities.md). Se não aparecer na lista suspensa, digite-o.

1. Como a **[!UICONTROL ID]**, selecione o elemento de dados `User Id` criado na lição [Criar elementos de dados](create-data-elements.md#create-data-elements-to-capture-the-data-layer).

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

| Elementos de dados da extensão principal | Elementos de dados da extensão do Platform Web SDK |
-----------------------------|-------------------------------
| `Ecommerce Cart Products` | `Data Variable` |
| `Ecommerce Checkout Products` | `Identity Map` |
| `Ecommerce Checkout Products` | `XDM Variable` |
| `Ecommerce Product Category` | |
| `Ecommerce Product Id` | |
| `Ecommerce Product Name` | |
| `Ecommerce Purchase Id` | |
| `Page Name` | |
| `User Id` | |
| `User Logged In` | |

Com esses elementos de dados implementados, você estará pronto para começar a enviar dados para o Platform Edge Network criando uma regra nas tags.

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [postagem de discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/adobe-experience-platform-18/tutorial-discussion-implement-adobe-experience-cloud-with-web-sdk-tutorial-248848?profile.language=pt)
