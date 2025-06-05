---
title: Coletar dados de identidade em um aplicativo móvel com o Mobile SDK
description: Saiba como coletar dados de identidade em um aplicativo móvel.
feature: Mobile SDK,Identities
jira: KT-14633
exl-id: cbcd1708-29e6-4d74-be7a-f75c917ba2fa
source-git-commit: d73f9b3eafb327783d6bfacaf4d57cf8881479f7
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 1%

---

# Coletar dados de identidade

Saiba como coletar dados de identidade em um aplicativo móvel.

O Serviço de identidade da Adobe Experience Platform ajuda você a obter uma melhor visualização dos clientes e de seus comportamentos, unindo identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e de impacto em tempo real. Campos de identidade e namespaces são a cola que une diferentes fontes de dados para criar o perfil do cliente em tempo real de 360 graus.

Saiba mais sobre a [Extensão da identidade](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) e o [serviço de identidade](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=pt-BR) na documentação.

## Pré-requisitos

* O aplicativo com SDKs instalados e configurados foi criado e executado com sucesso.

## Objetivos de aprendizagem

Nesta lição, você vai:

* Configurar um namespace de identidade personalizado.
* Atualizar identidades.
* Valide o gráfico de identidade.
* Obtenha a ECID e outras identidades.


## Configurar um namespace de identidade personalizado

Os namespaces de identidade são componentes do [Serviço de Identidade](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=pt-BR) que servem como indicadores do contexto ao qual uma identidade está relacionada. Por exemplo, eles distinguem um valor de `name@email.com` como um endereço de email ou `443522` como uma ID de CRM numérica.

>[!NOTE]
>
>O Mobile SDK gera uma identidade exclusiva em seu próprio namespace, chamada Experience Cloud ID (ECID) quando o aplicativo é instalado. Essa ECID é armazenada na memória persistente no dispositivo móvel e é enviada com cada ocorrência. A ECID é removida quando o usuário desinstala o aplicativo ou define o status de privacidade global do Mobile SDK como recusa. No aplicativo Luma de amostra, você deve remover e reinstalar o aplicativo para criar um novo perfil com sua própria ECID exclusiva.


Para criar um novo namespace de identidade:

1. Na interface da Coleção de dados, selecione **[!UICONTROL Identidades]** na navegação do painel esquerdo.
1. Selecione **[!UICONTROL Criar namespace de identidade]**.
1. Forneça um **[!UICONTROL Nome de exibição]** de `Luma CRM ID` e um **[!UICONTROL Símbolo de identidade]** valor de `lumaCRMId`.
1. Selecione **[!UICONTROL ID entre dispositivos]**.
1. Selecione **[!UICONTROL Criar]**.

   ![criar namespace de identidade](assets/identity-create.png)




## Atualizar identidades

Você deseja atualizar a identidade padrão (email) e a identidade personalizada (ID do CRM da Luma) quando o usuário fizer logon no aplicativo.

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** no navegador do Projeto Xcode e localize a implementação da função `func updateIdentities(emailAddress: String, crmId: String)`. Adicione o código a seguir à função.

   ```swift
   // Set up identity map, add identities to map and update identities
   let identityMap: IdentityMap = IdentityMap()
   
   let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
   let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
   identityMap.add(item:emailIdentity, withNamespace: "Email")
   identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
   
   Identity.updateIdentities(with: identityMap)
   ```

   Este código:

   1. Cria um objeto `IdentityMap` vazio.

      ```swift
      let identityMap: IdentityMap = IdentityMap()
      ```

   1. Configura objetos `IdentityItem` para email e ID do CRM.

      ```swift
      let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
      let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
      ```

   1. Adiciona estes objetos `IdentityItem` ao objeto `IdentityMap`.

      ```swift
      identityMap.add(item:emailIdentity, withNamespace: "Email")
      identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
      ```

   1. Envia o objeto `IdentityItem` como parte da chamada de API `Identity.updateIdentities` para a Edge Network.

      ```swift
      Identity.updateIdentities(with: identityMap) 
      ```

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL LoginSheet]** no navegador do Projeto Xcode e localize o código a ser executado ao selecionar o botão **[!UICONTROL Logon]**. Adicione o seguinte código:

   ```swift
   // Update identities
   MobileSDK.shared.updateIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                             
   ```


>[!NOTE]
>
>Você pode enviar várias identidades em uma única chamada `updateIdentities`. Você também pode modificar identidades enviadas anteriormente.


## Remover uma identidade

Você pode usar a API [`Identity.removeIdentity`](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#removeidentity) para remover a identidade do mapa de identidade armazenado do lado do cliente. A extensão Identity interrompe o envio do identificador para a Edge Network. O uso dessa API não remove o identificador do gráfico de identidade do lado do servidor. Consulte [Exibir gráficos de identidade](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/view-identity-graphs.html?lang=en) para obter mais informações sobre gráficos de identidade.

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** no navegador do Projeto Xcode e adicione o seguinte código à função `func removeIdentities(emailAddress: String, crmId: String)`:

   ```swift
   // Remove identities and reset email and CRM Id to their defaults
   Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
   Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCRMId")
   currentEmailId = "testUser@gmail.com"
   currentCRMId = "b642b4217b34b1e8d3bd915fc65c4452"
   ```

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL LoginSheet]** no navegador do Projeto Xcode e localize o código a ser executado ao selecionar o botão **[!UICONTROL Logout]**. Adicione o seguinte código:

   ```swift
   // Remove identities
   MobileSDK.shared.removeIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                  
   ```


## Validar com o Assurance

1. Revise a seção [instruções de instalação](assurance.md#connecting-to-a-session) para conectar seu simulador ou dispositivo ao Assurance.
1. No aplicativo Luma
   1. Selecione a guia **[!UICONTROL Início]** e mova o ícone do Assurance para a esquerda.
   1. Selecione o Ícone <img src="assets/login.png" width="15" /> na parte superior direita.

      <img src="./assets/identity1.png" width="300">

   1. Forneça um endereço de email e uma ID de CRM ou
   1. Selecionar <img src="assets/insert.png" width="15" /> para gerar aleatoriamente um **[!UICONTROL Email]** e uma **[!UICONTROL ID do CRM]**.
   1. Selecione **[!UICONTROL Logon]**.

      <img src="./assets/identity2.png" width="300">


1. Procure na interface da Web do Assurance o evento **[!UICONTROL Identidades de Atualização de Identidade do Edge]** do fornecedor **[!UICONTROL com.adobe.griffon.mobile]**.
1. Selecione o evento e examine os dados no objeto **[!UICONTROL ACPExtensionEventData]**. Você deve ver as identidades atualizadas.
   ![validar atualização de identidades](assets/identity-validate-assurance.png)

## Validar com gráfico de identidade

Depois de concluir as etapas da [lição do Experience Platform](platform.md), você poderá confirmar a captura de identidade no visualizador de gráficos de identidade de Plataformas:

1. Selecione **[!UICONTROL Identidades]** na interface da Coleção de Dados.
1. Selecione **[!UICONTROL Gráfico de identidade]** na barra superior.
1. Insira `Luma CRM ID` como o **[!UICONTROL Namespace de identidade]** e sua ID do CRM (por exemplo `24e620e255734d8489820e74f357b5c8`) como o **[!UICONTROL Valor de identidade]**.
1. Você vê as **[!UICONTROL Identidades]** listadas.

   ![validar gráfico de identidade](assets/identity-validate-graph.png)

>[!INFO]
>
>Não há código no aplicativo para redefinir a ECID, o que significa que você só pode redefinir a ECID (e efetivamente criar um novo perfil com uma nova ECID) por meio de uma desinstalação e uma reinstalação do aplicativo. Para implementar a redefinição de identificadores, consulte as chamadas de API [`Identity.resetIdentities`](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#resetidentities) e [`MobileCore.resetIdentities`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#resetidentities). Entretanto, ao usar um identificador de notificação por push (consulte [Envio de notificações por push](journey-optimizer-push.md)), esse identificador se tornará outro identificador de perfil &quot;fixo&quot; no dispositivo.


>[!SUCCESS]
>
>Agora você configurou o aplicativo para atualizar identidades na Edge Network e (quando configurado) com o Adobe Experience Platform.
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-os nesta [postagem de discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Próximo: **[Coletar dados de perfil](profile.md)**
