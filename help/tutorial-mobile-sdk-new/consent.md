---
title: Implementar consentimento
description: Saiba como implementar o consentimento em um aplicativo móvel.
feature: Mobile SDK,Consent
hide: true
source-git-commit: cd1efbfaa335c08cbcc22603fe349b4594cc1056
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 2%

---

# Implementar consentimento

Saiba como implementar o consentimento em um aplicativo móvel.

A extensão móvel do Adobe Experience Platform Consent permite a coleta de preferências de consentimento do aplicativo móvel ao usar o SDK móvel da Adobe Experience Platform e a extensão de rede de borda. Saiba mais sobre o [Extensão de consentimento](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/), na documentação.

## Pré-requisitos

* O aplicativo com SDKs instalados e configurados foi criado e executado com sucesso.

## Objetivos de aprendizagem

Nesta lição, você vai:

* Solicitar consentimento do usuário.
* Atualize a extensão com base na resposta do usuário.
* Saiba como obter o estado de consentimento atual.

## Solicitar consentimento

Se você seguiu o tutorial desde o início, talvez se lembre de que definiu o consentimento padrão na Extensão de consentimento como **[!UICONTROL Pendente - Enfileira eventos que ocorrem antes de o usuário fornecer preferências de consentimento.]**

Para começar a coletar dados, você deve obter o consentimento do usuário. Neste tutorial, você obtém consentimento do usuário simplesmente solicitando-o com um alerta. Em um aplicativo real, você pode consultar as práticas recomendadas de consentimento para sua região.

1. Você só deseja perguntar ao usuário uma vez. Portanto, você deseja combinar o consentimento do SDK móvel com as autorizações necessárias para rastreamento usando a interface do Apple [Estrutura de transparência de rastreamento de aplicativos](https://developer.apple.com/documentation/apptrackingtransparency). Neste aplicativo, você presume que, quando o usuário autoriza o rastreamento, o usuário também consente em coletar eventos.

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** no navegador do Projeto Xcode.

   Adicione esse código à `updateConsent` função.

   ```swift
   // Update consent
   let collectConsent = ["collect": ["val": value]]
   let currentConsents = ["consents": collectConsent]
   Consent.update(with: currentConsents)
   MobileCore.updateConfigurationWith(configDict: currentConsents)
   ```

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL ExibiçãoDeAviso]** no navegador Project do Xcode, que é a exibição mostrada após instalar ou reinstalar o aplicativo e iniciar o aplicativo pela primeira vez. Apple O usuário é solicitado a autorizar o rastreamento de acordo com as [Estrutura de transparência de rastreamento de aplicativos](https://developer.apple.com/documentation/apptrackingtransparency). Se o usuário autorizar, você também atualizará o consentimento.

   Adicione o seguinte código à `ATTrackingManager.requestTrackingAuthorization { status in` encerramento.

   ```swift
   // Add consent based on authorization
   if status == .authorized {
      // Set consent to yes
      MobileSDK.shared.updateConsent(value: "y")
   }
   else {
      // Set consent to yes
      MobileSDK.shared.updateConsent(value: "n")
   }
   ```

## Obter estado de consentimento atual

A extensão móvel de consentimento suprime/pendente automaticamente/permite rastreamento com base no valor de consentimento atual. Você também pode acessar o estado de consentimento atual sozinho:

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** no navegador Project do Xcode.

   Adicione o seguinte código à `getConsents` função:

   ```swift
   // Get consents
   Consent.getConsents { consents, error in
      guard error == nil, let consents = consents else { return }
      guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
      guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
      Logger.aepMobileSDK.info("Consent getConsents: \(jsonStr)")
   }
   ```

2. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL HomeView]** no navegador Project do Xcode.

   Adicione o seguinte código à `.task` modificador:

   ```swift
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

No exemplo acima, você está simplesmente registrando o status de consentimento no console no Xcode. Em um cenário real, você pode usá-lo para modificar quais menus ou opções são mostrados ao usuário.

## Validar com garantia

1. Revise o [Assurance](assurance.md) lição.
1. Instale o aplicativo.
1. Inicie o aplicativo usando o URL gerado pelo Assurance.
1. Se você adicionou o código acima corretamente, será solicitado a fornecer consentimento.

   Selecionar **[!UICONTROL Continuar...]** e selecione **[!UICONTROL Permitir]**.

   <img src="./assets/consent-update-1.png" width="300" /> 
   <img src="./assets/consent-update-2.png" width="300" />

1. Você deve ver um **[!UICONTROL Obter resposta de consentimento]** evento na interface do usuário do Assurance.
   ![validar consentimento](assets/consent-update.png)



>[!SUCCESS]
>
>Agora, você ativou o aplicativo para solicitar ao usuário que inicie primeiro após a instalação (ou reinstalação) que consente o uso do SDK do Adobe Experience Platform Mobile.<br/>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Próximo: **[Coletar dados do ciclo de vida](lifecycle-data.md)**
