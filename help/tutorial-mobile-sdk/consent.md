---
title: Implementação do consentimento para implementações do Platform Mobile SDK
description: Saiba como implementar o consentimento em um aplicativo móvel.
feature: Mobile SDK,Consent
jira: KT-14629
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 1%

---

# Implementar consentimento

Saiba como implementar o consentimento em um aplicativo móvel.

A extensão móvel do Adobe Experience Platform Consent permite a coleta de preferências de consentimento do aplicativo móvel ao usar o Adobe Experience Platform Mobile SDK e a extensão Edge Network. Saiba mais sobre a [Extensão de consentimento](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) na documentação.

## Pré-requisitos

* O aplicativo com SDKs instalados e configurados foi criado e executado com sucesso.

## Objetivos de aprendizagem

Nesta lição, você vai:

* Solicitar consentimento do usuário.
* Atualize a extensão com base na resposta do usuário.
* Saiba como obter o estado de consentimento atual.

## Solicitar consentimento

Se você seguiu o tutorial desde o início, talvez se lembre de que definiu o consentimento padrão na Extensão de consentimento como **[!UICONTROL Pendente - Enfileirar eventos que ocorrem antes de o usuário fornecer preferências de consentimento.]**

Para começar a coletar dados, você deve obter o consentimento do usuário. Em um aplicativo real, você pode consultar as práticas recomendadas de consentimento para sua região. Neste tutorial, você obtém consentimento do usuário simplesmente solicitando-o com um alerta:

>[!BEGINTABS]

>[!TAB iOS]

1. Você só deseja pedir consentimento ao usuário uma vez. Você combina o consentimento do Mobile SDK com a autorização necessária para rastreamento usando a [Estrutura de transparência de rastreamento de aplicativos](https://developer.apple.com/documentation/apptrackingtransparency) da Apple. Neste aplicativo, você presume que, quando o usuário autoriza o rastreamento, ele consente em coletar eventos.

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** no navegador do Projeto Xcode.

   Adicione este código à função `updateConsent`.

   ```swift
   // Update consent
   let collectConsent = ["collect": ["val": value]]
   let currentConsents = ["consents": collectConsent]
   Consent.update(with: currentConsents)
   MobileCore.updateConfigurationWith(configDict: currentConsents)
   ```

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL DisclaimerView]** no navegador de projetos do Xcode. O Navegador do projeto do Xode é a exibição mostrada após instalar ou reinstalar o aplicativo e iniciá-lo pela primeira vez. O usuário é solicitado a autorizar o rastreamento de acordo com a [Estrutura de transparência de rastreamento de aplicativos](https://developer.apple.com/documentation/apptrackingtransparency) da Apple. Se o usuário autorizar, você também atualizará o consentimento.

   Adicione o seguinte código ao fechamento `ATTrackingManager.requestTrackingAuthorization { status in`.

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

>[!TAB Android]

1. Você só deseja pedir consentimento ao usuário uma vez. Neste aplicativo, você presume que, quando o usuário autoriza o rastreamento, ele consente em coletar eventos.

1. Navegue até **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]** no navegador do Android Studio.

   Adicione este código à função `updateConsent(value: String)`.

   ```kotlin
   // Update consent
   val collectConsent = mapOf("collect" to mapOf("val" to value))
   val currentConsents = mapOf("consents" to collectConsent)
   Consent.update(currentConsents)
   MobileCore.updateConfiguration(currentConsents)
   ```

1. Navegue até **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL views]** > **[!UICONTROL DisclaimerView.kt]** no navegador Android Studio.

   Adicione o seguinte código à função `DisclaimerView(navController: NavController)` abaixo de `// Set content to yes` e `// Set content to no`.

   ```kotlin
   // Add consent based on authorization
   if (status) {
      showPersonalizationWarning = false
   
      // Set consent to yes
      MobileSDK.shared.updateTrackingStatus(TrackingStatus.AUTHORIZED)
      MobileSDK.shared.updateConsent("y")
   } else {
      Toast.makeText(
            context,
            "You will not receive offers and location tracking will be disabled.",
            Toast.LENGTH_LONG
      ).show()
      showPersonalizationWarning = true
   
      // Set consent to no
      MobileSDK.shared.updateTrackingStatus(TrackingStatus.DENIED)
      MobileSDK.shared.updateConsent("n")
   }
   ```

>[!ENDTABS]

## Obter estado de consentimento atual

A extensão móvel de consentimento suprime/pendente automaticamente/permite rastreamento com base no valor de consentimento atual. Você também pode acessar o estado de consentimento atual sozinho:

>[!BEGINTABS]

>[!TAB iOS]

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** no navegador de projetos do Xcode.

   Adicione o seguinte código à função `getConsents`:

   ```swift
   // Get consents
   Consent.getConsents { consents, error in
      guard error == nil, let consents = consents else { return }
      guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
      guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
      Logger.aepMobileSDK.info("Consent getConsents: \(jsonStr)")
   }
   ```

2. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL HomeView]** no navegador de projetos do Xcode.

   Adicione o seguinte código ao modificador `.task`:

   ```swift
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

No exemplo acima, você está simplesmente registrando o status de consentimento no console no Xcode. Em um cenário real, você pode usá-lo para modificar quais menus ou opções são mostrados ao usuário.

>[!TAB Android]

1. Navegue até **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]** no navegador do Android Studio.

   Adicione o seguinte código à função `getConsents()`:

   ```kotlin
   // Get consents
   Consent.getConsents { callback ->
      if (callback != null) {
            val jsonStr = JSONObject(callback).toString(4)
            Log.i("MobileSDK", "Consent getConsents: $jsonStr")
      }
   }
   ```

1. Navegue até **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL views]** > **[!UICONTROL HomeView.kt]** no navegador do Android Studio.

   Adicionar o seguinte código a `LaunchedEffect(unit)`:

   ```kotlin
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

No exemplo acima, você está simplesmente registrando o status de consentimento no console no Android Studio. Em um cenário real, você pode usá-lo para modificar quais menus ou opções são mostrados ao usuário.

>[!ENDTABS]

## Validar com o Assurance

1. Exclua o aplicativo do seu dispositivo ou simulador para redefinir e inicializar o rastreamento e o consentimento corretamente.
1. Para conectar seu simulador ou dispositivo ao Assurance, reveja a seção [instruções de instalação](assurance.md#connecting-to-a-session).
1. Ao mover o aplicativo da tela **[!UICONTROL Página inicial]** para a tela **[!UICONTROL Produtos]** e de volta para a tela **[!UICONTROL Página inicial]**, você deverá ver um evento **[!UICONTROL Obter Resposta de Consentimento]** na interface do usuário do Assurance.
   ![validar consentimento](assets/consent-update.png){zoomable="yes"}


>[!SUCCESS]
>
>Agora, você ativou o aplicativo para solicitar ao usuário em seu início inicial após a instalação (ou reinstalação) o consentimento usando o Adobe Experience Platform Mobile SDK.
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-os nesta [postagem de discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Próximo: **[Coletar dados do ciclo de vida](lifecycle-data.md)**
