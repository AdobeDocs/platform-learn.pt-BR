---
title: Instalar SDKs da Adobe Experience Platform para dispositivos móveis
description: Saiba como implementar o SDK da Adobe Experience Platform para dispositivos móveis em um aplicativo móvel.
jira: KT-14627
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '1768'
ht-degree: 3%

---

# Instalar SDKs da Adobe Experience Platform para dispositivos móveis {#tutorial_install_mobile_sdks}

>[!CONTEXTUALHELP]
>
>id="platform_mobile_sdk_tutorial_install"
>title="Instalar SDKs da Adobe Experience Platform para dispositivos móveis"
>abstract="Saiba como implementar o SDK da Adobe Experience Platform para dispositivos móveis em um aplicativo móvel."

Saiba como implementar o SDK da Adobe Experience Platform para dispositivos móveis em um aplicativo móvel.

## Pré-requisitos

* Biblioteca de marcas criada com êxito com as extensões descritas na [lição anterior](configure-tags.md).
* ID do Arquivo de Ambiente de Desenvolvimento das [Instruções de Instalação Móvel](configure-tags.md#generate-sdk-install-instructions).
* Baixe o [aplicativo de exemplo para o iOS](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) ou o [aplicativo de exemplo para o Android](https://github.com/adobe/Luma-Android).
* Experiência com [Xcode](Https://developer.apple.com/xcode/) (iOS) ou [Android Studio](https://developer.android.com/studio/intro?utm_source=android-studio) (Android)

## Objetivos de aprendizagem

Nesta lição, você vai:

* Adicione os SDKs necessários ao projeto.
* Registre as extensões.

>[!NOTE]
>
>Em uma implementação de aplicativo móvel, os termos *extensões* e *SDKs* são quase intercambiáveis.

>[!BEGINTABS]

>[!TAB iOS]

## Gerenciador de pacotes Swift

Em vez de usar CocoaPods e um arquivo Pod (como descrito em [Gerar instruções de instalação do SDK](./configure-tags.md#generate-sdk-install-instructions)), adicione pacotes individuais usando o gerenciador de pacotes Swift nativo do Xcode. O projeto Xcode já tem todas as dependências de pacotes adicionadas para você. A tela **[!UICONTROL Dependências de Pacote]** do Xcode deve ser semelhante a:

![Dependências Do Pacote Xcode](assets/xcode-package-dependencies.png){zoomable="yes"}


No Xcode, você pode usar **[!UICONTROL Arquivo]** > **[!UICONTROL Adicionar pacotes...]** para adicionar pacotes. A tabela abaixo fornece links para os URLs que você usaria para adicionar pacotes. Os links também direcionam você para mais informações sobre cada pacote específico.

| Pacote | Descrição |
|---|---|
| [AEP Core](https://github.com/adobe/aepsdk-core-ios) | As extensões `AEPCore`, `AEPServices` e `AEPIdentity` representam a base do Adobe Experience Platform SDK - todos os aplicativos que usam o SDK devem incluí-las. Esses módulos contêm um conjunto comum de funcionalidades e serviços que todas as extensões do SDK exigem.<br/><ul><li>`AEPCore` contém a implementação do Hub de Eventos. O Hub de eventos é o mecanismo usado para fornecer eventos entre o aplicativo e a SDK. O Hub de eventos também é usado para compartilhar dados entre extensões.</li><li>O `AEPServices` fornece várias implementações reutilizáveis necessárias para suporte à plataforma, incluindo rede, acesso a disco e gerenciamento de banco de dados.</li><li>`AEPIdentity` implementa a integração com os serviços de identidade da Adobe Experience Platform.</li><li>`AEPSignal` representa a extensão de Sinal dos SDKs da Adobe Experience Platform que permite aos profissionais de marketing enviar um &quot;sinal&quot; para seus aplicativos enviar dados para destinos externos ou abrir URLs.</li><li>`AEPLifecycle` representa a extensão de ciclo de vida dos SDKs da Adobe Experience Platform que ajuda a coletar métricas de ciclo de vida do aplicativo, como informações de instalação ou atualização do aplicativo, informações de inicialização e sessão do aplicativo, informações do dispositivo e quaisquer dados de contexto adicionais fornecidos pelo desenvolvedor do aplicativo.</li></ul> |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios) | A extensão móvel do Adobe Experience Platform Edge Network (`AEPEdge`) permite enviar dados para a Rede de borda da Adobe a partir de um aplicativo móvel. Essa extensão permite implementar os recursos do Adobe Experience Cloud de forma mais robusta, atender a várias soluções da Adobe por meio de uma chamada de rede e, simultaneamente, encaminhar essas informações para a Adobe Experience Platform.<br/>A extensão do Edge Network para dispositivos móveis é uma extensão do Adobe Experience Platform SDK. A extensão requer as extensões `AEPCore` e `AEPServices` para manipulação de eventos, bem como a extensão `AEPEdgeIdentity` para recuperação de identidades, como ECID. |
| [Identidade do AEP Edge](https://github.com/adobe/aepsdk-edgeidentity-ios) | A extensão móvel (`AEPEdgeIdentity`) do Adobe Experience Platform Edge Identity permite o tratamento de dados de identidade do usuário de um aplicativo móvel ao usar o Adobe Experience Platform SDK e a extensão do Edge Network. |
| [Consentimento do AEP Edge](https://github.com/adobe/aepsdk-edgeconsent-ios) | A extensão móvel da Coleção de consentimento da Adobe Experience Platform (`AEPConsent`) habilita a coleção de preferências de consentimento do aplicativo móvel ao usar o Adobe Experience Platform SDK e a extensão Edge Network. |
| [Perfil de Usuário do AEP](https://github.com/adobe/aepsdk-userprofile-ios) | A extensão Móvel do Perfil de Usuário do Adobe Experience Platform (`AEPUserProfile`) é uma extensão para gerenciar perfis de usuário do Adobe Experience Platform SDK. |
| [AEP Places](https://github.com/adobe/aepsdk-places-ios) | A extensão do Adobe Experience Platform Places (`AEPPlaces`) permite rastrear eventos de geolocalização conforme definido na interface do Adobe Places e nas regras da tag da coleção de dados da Adobe. |
| [Mensagens do AEP](https://github.com/adobe/aepsdk-messaging-ios) | A extensão do Adobe Experience Platform Messaging (`AEPMessaging`) permite enviar tokens de notificação por push e feedback de click-through de notificação por push para a Adobe Experience Platform. |
| [Otimização do AEP](https://github.com/adobe/aepsdk-optimize-ios) | A extensão Adobe Experience Platform Otimize (`AEPOptimize`) fornece APIs para permitir fluxos de trabalho de personalização em tempo real nos SDKs do Adobe Experience Platform Mobile usando o Adobe Target ou o Adobe Journey Optimizer Offer Decisioning. Ele requer as extensões `AEPCore` e `AEPEdge` para enviar eventos de consulta de personalização para a Experience Edge Network. |
| [AEP Assurance](https://github.com/adobe/aepsdk-assurance-ios) | O Adobe Experience Platform Assurance é um produto da Adobe Experience Cloud que ajuda a inspecionar, testar, simular e validar a maneira como você coleta dados ou oferece experiências em seu aplicativo móvel. |


## Importar extensões

Abra o projeto no Xcode na pasta **[!UICONTROL Start]** do aplicativo de amostra.

No Xcode, navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]** e verifique se as importações a seguir fazem parte deste arquivo de origem.

```swift
// import AEP MobileSDK libraries
import AEPCore
import AEPServices
import AEPIdentity
import AEPSignal
import AEPLifecycle
import AEPEdge
import AEPEdgeIdentity
import AEPEdgeConsent
import AEPUserProfile
import AEPPlaces
import AEPMessaging
import AEPOptimize
import AEPAssurance
```

Faça o mesmo para **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]**.

## Atualizar AppDelegate

Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **AppDelegate** no navegador de projetos Xcode.

1. Substitua o `@AppStorage` valor `YOUR_ENVIRONMENT_ID_GOES_HERE` de `environmentFileId` pelo valor da ID de Arquivo de Ambiente que você recuperou das marcas em [Gerar instruções de instalação do SDK](configure-tags.md#generate-sdk-install-instructions).

   ```swift
   @AppStorage("environmentFileId") private var environmentFileId = "YOUR_ENVIRONMENT_ID_GOES_HERE"
   ```

1. Adicione o seguinte código à função `application(_, didFinishLaunchingWithOptions)`.

   ```swift
   // Define extensions
   let extensions = [
       AEPIdentity.Identity.self,
       Lifecycle.self,
       Signal.self,
       Edge.self,
       AEPEdgeIdentity.Identity.self,
       Consent.self,
       UserProfile.self,
       Places.self,
       Messaging.self,
       Optimize.self,
       Assurance.self
   ]
   
   // Register extensions
   MobileCore.registerExtensions(extensions, {
       // Use the environment file id assigned to this application via Adobe Experience Platform Data Collection
       Logger.aepMobileSDK.info("Luma - using mobile config: \(self.environmentFileId)")
       MobileCore.configureWith(appId: self.environmentFileId)
   
       // set this to false or comment it when deploying to TestFlight (default is false),
       // set this to true when testing on your device.
       MobileCore.updateConfigurationWith(configDict: ["messaging.useSandbox": true])
       if appState != .background {
           // only start lifecycle if the application is not in the background
           MobileCore.lifecycleStart(additionalContextData: nil)
       }
   
       // assume unknown, adapt to your needs.
       MobileCore.setPrivacyStatus(.unknown)
   })
   ```

O código acima faz o seguinte:

1. Registra as extensões necessárias.
1. Configura o MobileCore e outras extensões para usar a configuração de propriedade da tag.
1. Ativa o log de depuração. Mais detalhes e opções podem ser encontrados na [documentação do Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).
1. Inicia o monitoramento do ciclo de vida. Consulte a etapa [Ciclo de vida](lifecycle-data.md) do tutorial para obter mais detalhes.
1. Define o consentimento padrão como desconhecido. Consulte a etapa [Consentimento](consent.md) do tutorial para obter mais detalhes.

Atualize `MobileCore.configureWith(appId: self.environmentFileId)` com o `appId` baseado no `environmentFileId` do ambiente de marcas para o qual você está criando (desenvolvimento, preparo ou produção).

>[!TAB Android]

## Gradle

Use as dependências da [Gerar instruções de instalação do SDK](./configure-tags.md#generate-sdk-install-instructions) para adicionar pacotes individuais usando a integração do Gradle com o Android Studio. O projeto do Android Studio já tem todas as dependências de pacotes adicionadas para você.

1. Selecione ![FolderOutline](/help/assets/icons/FolderOutline.svg) como a ferramenta.
1. Selecione a exibição **[!UICONTROL Android]**.
1. Selecione **[!UICONTROL Gradle scripts]** > **[!UICONTROL build.gradle.kts (Módulo :app)]** no painel esquerdo. Em seguida, no painel direito, role até ver `dependencies`.

   ![Dependências do Android Gradle](assets/androidstudio-package-dependencies.png){zoomable="yes"}

No Android Studio, você pode usar **[!UICONTROL Arquivo]** > **[!UICONTROL Estrutura de Projeto...]** para adicionar dependências de módulo. Selecione **[!UICONTROL Dependências]** e use **[!UICONTROL Módulos]** ![Adicionar](/help/assets/icons/Add.svg) para adicionar módulos. A tabela abaixo fornece links para os URLs que você usaria para adicionar módulos de dependência. Os links também direcionam você para mais informações sobre cada módulo específico.

| Pacote<br/>com.adobe.<br/>marketing.mobile: | Descrição |
|---|---|
| [núcleo](https://github.com/adobe/aepsdk-core-android) | As extensões `MobileCore` e `Identity` representam a base do Adobe Experience Platform SDK. Todos os aplicativos que usam a SDK devem incluí-los. Esses módulos contêm um conjunto comum de funcionalidades e serviços que todas as extensões do SDK exigem.<ul><li>`MobileCore` contém a implementação do Hub de Eventos. O Hub de eventos é o mecanismo usado para fornecer eventos entre o aplicativo e a SDK. O Hub de Eventos também é usado para compartilhar dados entre extensões e fornece várias implementações reutilizáveis necessárias para suporte à plataforma, incluindo rede, acesso ao disco e gerenciamento de banco de dados.</li><li>`Identity` implementa a integração com os serviços de identidade da Adobe Experience Platform.</li><li>`Signal` representa a extensão de Sinal do Adobe Experience Platform SDK que permite aos profissionais de marketing enviar um &quot;sinal&quot; para seus aplicativos enviar dados para destinos externos ou abrir URLs.</li><li>`Lifecycle` representa a extensão de ciclo de vida do Adobe Experience Platform SDK que ajuda a coletar métricas de ciclo de vida do aplicativo, como informações de instalação ou atualização do aplicativo, informações de inicialização e sessão do aplicativo, informações do dispositivo e quaisquer dados de contexto adicionais fornecidos pelo desenvolvedor do aplicativo.</li></ul> |
| [borda](https://github.com/adobe/aepsdk-edge-android) | A extensão móvel do Adobe Experience Platform Edge Network (`AEPEdge`) permite enviar dados para a Rede de borda da Adobe a partir de um aplicativo móvel. Essa extensão permite implementar os recursos do Adobe Experience Cloud de forma mais robusta, atender a várias soluções da Adobe por meio de uma chamada de rede e, simultaneamente, encaminhar essas informações para a Adobe Experience Platform.<br/>A extensão do Edge Network para dispositivos móveis é uma extensão do Adobe Experience Platform SDK. A extensão requer as extensões `Mobile Core` e `Services` para manipulação de eventos. E a extensão `Identity for Edge Network` para recuperar as identidades, como ECID. |
| [edgeidentity](https://github.com/adobe/aepsdk-edgeidentity-android) | A extensão móvel Adobe Experience Platform Edge Identity permite a manipulação de dados de identidade do usuário de um aplicativo móvel ao usar o Adobe Experience Platform SDK e a extensão do Edge Network. |
| [edgeconsent](https://github.com/adobe/aepsdk-edgeconsent-android) | A extensão móvel da Coleção de consentimento da Adobe Experience Platform permite a coleta de preferências de consentimento do aplicativo móvel ao usar o Adobe Experience Platform SDK e a extensão do Edge Network. |
| [perfil de usuário](https://github.com/adobe/aepsdk-userprofile-android) | A extensão do Adobe Experience Platform User Profile Mobile é uma extensão para gerenciar perfis de usuário do Adobe Experience Platform SDK. |
| [aepplaces](https://github.com/adobe/aepsdk-places-android) | O Adobe Places Service é um serviço de localização geográfica que permite o uso de aplicativos móveis com detecção de localização. E entender o contexto de localização usando interfaces avançadas e fáceis de usar do SDK acompanhadas por um banco de dados flexível de pontos de interesse (POIs). Para obter mais informações, consulte a Documentação do Places Service.<br/>Este serviço é a extensão para dispositivos móveis do Places para o Android 2.x Adobe Experience Platform SDK e requer a extensão principal para manipulação de eventos. |
| [mensagens](https://github.com/adobe/aepsdk-messaging-android) | A extensão Mensagens da Adobe Experience Platform habilita notificações por push, mensagens no aplicativo e experiências baseadas em código para seus aplicativos móveis. Essa extensão também ajuda a coletar tokens de push do usuário e gerencia a medição de interação com os serviços da Adobe Experience Platform. |
| [otimizar](https://github.com/adobe/aepsdk-optimize-android) | A extensão Otimize do Adobe Experience Platform fornece APIs para permitir fluxos de trabalho de personalização em tempo real nos SDKs da Adobe Experience Platform usando o Adobe Target ou o Adobe Journey Optimizer Offer Decisioning. Depende do Mobile Core e exige a extensão do Edge para enviar eventos de consulta de personalização para o Experience Edge Network. |
| [garantia](https://github.com/adobe/aepsdk-assurance-android) | O Assurance (também conhecido como projeto Griffon) é uma extensão móvel para o Adobe Experience Platform que permite a integração com o Adobe Experience Platform Assurance. A extensão ajuda a inspecionar, testar, simular e validar a maneira como você coleta dados ou fornece experiências em seu aplicativo móvel. Esta extensão requer MobileCore. |

## Importar extensões

No Android Studio, navegue até **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL LumaApplication]** e verifique se as importações a seguir fazem parte do arquivo de origem.

```kotlin
import com.adobe.marketing.mobile.Assurance
import com.adobe.marketing.mobile.Edge
import com.adobe.marketing.mobile.Lifecycle
import com.adobe.marketing.mobile.LoggingMode
import com.adobe.marketing.mobile.Messaging
import com.adobe.marketing.mobile.MobileCore
import com.adobe.marketing.mobile.MobilePrivacyStatus
import com.adobe.marketing.mobile.Places
import com.adobe.marketing.mobile.Signal
import com.adobe.marketing.mobile.UserProfile
import com.adobe.marketing.mobile.edge.consent.Consent
import com.adobe.marketing.mobile.edge.identity.Identity
import com.adobe.marketing.mobile.optimize.Optimize
```

Faça o mesmo para **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]**.


## Atualizar LumaApplication

No modo de exibição **[!UICONTROL Android]**, navegue até **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL LumaApplication]** no Android Studio.

1. Substitua `"YOUR_ENVIRONMENT_FILE_ID"` em `private var environmentFileId = "YOUR_ENVIRONMENT_ID_GOES_HERE"` pelo valor da ID de Arquivo de Ambiente que você recuperou das marcas em [Gerar instruções de instalação do SDK](configure-tags.md#generate-sdk-install-instructions).

   ```kotlin
   private var environmentFileId = "YOUR_ENVIRONMENT_ID_GOES_HERE"
   ```

1. Adicione o seguinte código à função `override fun onCreate()` em `class LumaApplication : Application()`.

   ```kotlin
   // Define extensions
   val extensions = listOf(
      Identity.EXTENSION,
      Lifecycle.EXTENSION,
      Signal.EXTENSION,
      Edge.EXTENSION,
      Consent.EXTENSION,
      UserProfile.EXTENSION,
      Places.EXTENSION,
      Messaging.EXTENSION,
      Optimize.EXTENSION,
      Assurance.EXTENSION
   )
   
   // Register extensions
   MobileCore.registerExtensions(extensions) {
   // Use the environment file id assigned to this application via Adobe Experience Platform Data Collection
     Log.i("Luma", "Using mobile config: $environmentFileId")
     MobileCore.configureWithAppID(environmentFileId)
   
     // set this to true when testing on your device, default is false.
     //MobileCore.updateConfiguration(mapOf("messaging.useSandbox" to true))
   
     // assume unknown, adapt to your needs.
     MobileCore.setPrivacyStatus(MobilePrivacyStatus.UNKNOWN)
   }
   ```

   O código acima faz o seguinte:

   1. Registra as extensões necessárias.
   1. Configura o MobileCore e outras extensões para usar a configuração de propriedade da tag.
   1. Ativa o log de depuração. Mais detalhes e opções podem ser encontrados na [documentação do Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).
   1. Inicia o monitoramento do ciclo de vida. Consulte a etapa [Ciclo de vida](lifecycle-data.md) do tutorial para obter mais detalhes.
   1. Define o consentimento padrão como desconhecido. Consulte a etapa [Consentimento](consent.md) do tutorial para obter mais detalhes.

Atualize `MobileCore.configureWith(environmentFileId)` com o `environmentFileId` baseado na ID do Arquivo de Ambiente do ambiente de marcas que você está criando para (desenvolvimento, preparo ou produção).


>[!ENDTABS]

>[!SUCCESS]
>
>Agora você instalou os pacotes necessários e atualizou seu projeto para registrar as extensões do Adobe Experience Platform Mobile SDK necessárias que você usará para o restante do tutorial.
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-os nesta [postagem de discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Próximo: **[Configurar Assurance](assurance.md)**
