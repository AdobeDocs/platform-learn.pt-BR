---
title: Identidade
description: Saiba como coletar dados de identidade em um aplicativo móvel.
feature: Mobile SDK,Identities
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 6%

---

# Identidade

Saiba como coletar dados de identidade em um aplicativo móvel.

O Serviço de identidade da Adobe Experience Platform ajuda você a obter uma melhor visualização dos clientes e de seus comportamentos, unindo identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e de impacto em tempo real. Campos de identidade e namespaces são a cola que une diferentes fontes de dados para criar o perfil do cliente em tempo real de 360 graus.

Saiba mais sobre o [Extensão de identidade](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) e a variável [serviço de identidade](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=pt-BR) na documentação.

## Pré-requisitos

* O aplicativo com SDKs instalados e configurados foi criado e executado com sucesso.

## Objetivos de aprendizagem

Nesta lição, você vai:

* Configurar um namespace de identidade personalizado.
* Atualizar identidades.
* Valide o gráfico de identidade.
* Obtenha a ECID e outras identidades.


## Configurar um namespace de identidade personalizado

Os namespaces de identidade são componentes de [Serviço de identidade](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=pt-BR) que servem como indicadores do contexto ao qual uma identidade está relacionada. Por exemplo, eles distinguem um valor de `name@email.com` como um endereço de email ou `443522` como uma ID do CRM numérica.

1. Na interface da Coleção de dados, selecione **[!UICONTROL Identidades]** no painel de navegação esquerdo.
1. Selecione **[!UICONTROL Criar namespace de identidade]**.
1. Forneça um **[!UICONTROL Nome de exibição]** de `Luma CRM ID` e uma **[!UICONTROL Símbolo de identidade]** valor de `lumaCRMId`.
1. Selecionar **[!UICONTROL ID entre dispositivos]**.
1. Selecione **[!UICONTROL Criar]**.

   ![criar namespace de identidade](assets/identity-create.png)




## Atualizar identidades

Você deseja atualizar a identidade padrão (email) e a identidade personalizada (ID do CRM da Luma) quando o usuário fizer logon no aplicativo.

1. Navegue até **[!UICONTROL LoginSheet]** (em **[!UICONTROL Visualizações]** > **[!UICONTROL Geral]**) no projeto de aplicativo Xcode Luma e encontre a chamada para `updateIdentities`:

   ```swift {highlight="3,4"}
   Button("Login") {
       // call updaeIdentities
       MobileSDK.shared.updateIdentities(emailAddress: currentEmailId, crmId: currentCRMId)
   
       // Send app interaction event
       MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
       dismiss()
   }
   .disabled(currentEmailId.isValidEmail == false)
   .buttonStyle(.bordered)
   ```

1. Navegue até a `updateIdentities` implementação de função no **[!UICONTROL MobileSDK]** (em **[!UICONTROL Utils]**) no projeto de aplicativo Xcode Luma. Adicione o código destacado a seguir à função.

   ```swift {highlight="2-12"}
   func updateIdentities(emailAddress: String, crmId: String) {
       let identityMap: IdentityMap = IdentityMap()
       // Add identity items
       let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
       let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
       identityMap.add(item:emailIdentity, withNamespace: "Email")
       identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
   
       // Update identities
       Identity.updateIdentities(with: identityMap)
   }
   ```

   Este código:

   1. Cria um vazio `IdentityMap` objeto.

      ```swift
      let identityMap: IdentityMap = IdentityMap()
      ```

   1. Configura `IdentityItem` objetos para email e ID de CRM.

      ```swift
      let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
      let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
      ```

   1. Adiciona estes `IdentityItem` objetos para o `IdentityMap` objeto.

      ```swift
      identityMap.add(item:emailIdentity, withNamespace: "Email")
      identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
      ```

   1. Envia o `IdentityItem` como parte da `Identity.updateIdentities` chamada de API para a Rede de borda.

      ```swift
      Identity.updateIdentities(with: identityMap) 
      ```


>[!NOTE]
>
>É possível enviar várias identidades em um único `updateIdentities` chame. Você também pode modificar identidades enviadas anteriormente.


## Remover uma identidade

Você pode usar `removeIdentity` para remover a identidade do IdentityMap armazenado do lado do cliente. A extensão Identity interrompe o envio do identificador para a Rede de borda. O uso dessa API não remove o identificador do gráfico de perfil do usuário do lado do servidor ou do gráfico de identidade.

1. Navegue até **[!UICONTROL LoginSheet]** (em **[!UICONTROL Visualizações]** > **[!UICONTROL Geral]**) no projeto de aplicativo Xcode Luma e encontre a chamada para `removeIdentities`:

   ```swift {highlight="3"}
   Button("Logout", role: .destructive) {
       // call removeIdentities
       MobileSDK.shared.removeIdentities(emailAddress: currentEmailId, crmId: currentCRMId)
       dismiss()                   
   }
   .buttonStyle(.bordered)
   ```

1. Adicione o seguinte código à `removeIdentities` função em `MobileSDK`:

   ```swift {highlight="2-8"}
   func removeIdentities(emailAddress: String, crmId: String) {
       Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
       Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCRMId")
       // reset email and CRM Id to their defaults
       currentEmailId = "testUser@gmail.com"
       currentCRMId = "112ca06ed53d3db37e4cea49cc45b71e"
   }
   ```


## Validar com garantia

1. Revise o [instruções de configuração](assurance.md) e conecte seu simulador ou dispositivo ao Assurance.
1. No aplicativo Luma
   1. Selecione o **[!UICONTROL Início]** guia.
   1. Selecione o **[!UICONTROL Logon]** ícone na parte superior direita.
   1. Forneça um endereço de email e uma ID de CRM ou
   1. Selecione A| para gerar um relatório aleatoriamente **[!UICONTROL E-mail]** e **[!UICONTROL ID do CRM]**.
   1. Selecionar **[!UICONTROL Logon]**.

      <img src="./assets/identity1.png" width="300"> <img src="./assets/identity2.png" width="300">


1. Procure na interface do usuário da Web do Assurance o **[!UICONTROL Identidades de atualização de identidade da borda]**evento do **[!UICONTROL com.adobe.griffon.mobile]** fornecedor.
1. Selecione o evento e revise os dados na variável **[!UICONTROL ACPExtensionEventData]** objeto. Você deve ver as identidades atualizadas.
   ![validar atualização de identidades](assets/identity-validate-assurance.png)

## Validar com gráfico de identidade

Depois de concluir as etapas no [lição do Experience Platform](platform.md), você pode confirmar a captura de identidade no visualizador de gráficos de identidade de Plataformas:

1. Selecionar **[!UICONTROL Identidades]** na interface da Coleção de dados.
1. Selecionar **[!UICONTROL Gráfico de identidade]** na barra superior.
1. Enter `Luma CRM ID` como o **[!UICONTROL Namespace de identidade]** e sua ID do CRM (por exemplo, `24e620e255734d8489820e74f357b5c8`) como a **[!UICONTROL Valor de identidade]**.
1. Você vê a **[!UICONTROL Identidades]** listado.

   ![validar gráfico de identidade](assets/identity-validate-graph.png)


>[!SUCCESS]
>
>Agora você configurou o aplicativo para atualizar identidades na Rede de borda e (quando configurado) com o Adobe Experience Platform.<br/>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Próximo: **[Perfil](profile.md)**
