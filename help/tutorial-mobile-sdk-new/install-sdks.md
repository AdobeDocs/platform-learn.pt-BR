---
title: Instalar SDKs do Adobe Experience Platform Mobile
description: Saiba como implementar o Adobe Experience Platform Mobile SDK em um aplicativo móvel.
hide: true
source-git-commit: e364d70375f687b9c50691efd04a1db757fee364
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 1%

---

# Instalar SDKs do Adobe Experience Platform Mobile

Saiba como implementar o Adobe Experience Platform Mobile SDK em um aplicativo móvel.

## Pré-requisitos

* Biblioteca de tags criada com sucesso com as extensões descritas no [lição anterior](configure-tags.md).
* ID do arquivo do ambiente de desenvolvimento do [Instruções de instalação em dispositivos móveis](configure-tags.md#generate-sdk-install-instructions).
* Baixado, vazio [aplicativo de amostra](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}.
* Experiência com [XCode](Https://developer.apple.com/xcode/){target="_blank"}.

## Objetivos de aprendizagem

Nesta lição, você vai:

* Adicione os SDKs necessários ao seu projeto usando o Gerenciador de pacotes do Swift.
* Registre as extensões.

>[!NOTE]
>
>Em uma implementação de aplicativo móvel, os termos &quot;extensões&quot; e &quot;SDKs&quot; são quase intercambiáveis.

## Gerenciador de pacotes Swift

Em vez de usar CocoaPods e usar um arquivo Pod (conforme descrito nas Instruções de instalação em dispositivos móveis, consulte [Gerar instruções de instalação do SDK](./configure-tags.md#generate-sdk-install-instructions)), você adiciona pacotes individuais usando o gerenciador de pacotes Swift nativo do Xcode.

No Xcode, use **[!UICONTROL Arquivo]** > **[!UICONTROL Adicionar pacotes...]** e instale todos os pacotes listados na tabela abaixo. Selecione o link do pacote na tabela para obter o URL completo do pacote específico.

| Pacote | Descrição |
|---|---|
| [AEP Core](https://github.com/adobe/aepsdk-core-ios.git) | A variável `AEPCore`, `AEPServices`, e `AEPIdentity` As extensões representam a base do SDK do Adobe Experience Platform - todos os aplicativos que usam o SDK devem incluí-las. Esses módulos contêm um conjunto comum de funcionalidades e serviços exigidos por todas as extensões do SDK.<br/>`AEPCore` contém a implementação do Hub de eventos. O Hub de eventos é o mecanismo usado para fornecer eventos entre o aplicativo e o SDK. O Hub de eventos também é usado para compartilhar dados entre extensões.<br/>`AEPServices` O fornece várias implementações reutilizáveis necessárias para suporte à plataforma, incluindo rede, acesso ao disco e gerenciamento de banco de dados.<br/>`AEPIdentity` implementa a integração com os serviços de identidade da Adobe Experience Platform.<br/>`AEPSignal` representa a extensão Signal do SDK da Adobe Experience Platform que permite que os profissionais de marketing enviem um &quot;sinal&quot; para seus aplicativos a fim de enviar dados para destinos externos ou abrir URLs.<br/>`AEPLifecycle` representa a extensão Lifecycle do SDK do Adobe Experience Platform que ajuda a coletar medições de ciclo de vida do aplicativo, como informações de instalação ou atualização do aplicativo, informações de inicialização e sessão do aplicativo, informações do dispositivo e quaisquer dados de contexto adicionais fornecidos pelo desenvolvedor do aplicativo. |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios.git) | A extensão móvel da Rede de borda da Adobe Experience Platform permite enviar dados para a Rede da Adobe Edge a partir de um aplicativo móvel. Essa extensão permite implementar os recursos do Adobe Experience Cloud de forma mais robusta, atender a várias soluções de Adobe por meio de uma chamada de rede e, simultaneamente, encaminhar essas informações para a Adobe Experience Platform.<br/>A extensão móvel da Rede de borda é uma extensão para o SDK do Adobe Experience Platform e requer o `AEPCore` e `AEPServices` extensões para manipulação de eventos, bem como a `AEPEdgeIdentity` extensão para recuperar as identidades, como ECID. |
| [Identidade da borda da AEP](https://github.com/adobe/aepsdk-edgeidentity-ios.git) | A extensão móvel AEP Edge Identity permite o tratamento de dados de identidade do usuário de um aplicativo móvel ao usar o SDK do Adobe Experience Platform e a extensão Edge Network. |
| [Consentimento de borda da AEP](https://github.com/adobe/aepsdk-edgeconsent-ios.git) | A extensão móvel AEP Consent Collection permite a coleta de preferências de consentimento do aplicativo móvel ao usar o SDK do Adobe Experience Platform e a extensão Edge Network. |
| [Perfil de usuário da AEP](https://github.com/adobe/aepsdk-userprofile-ios.git) | A extensão móvel do perfil de usuário do Adobe Experience Platform é uma extensão para gerenciar perfis de usuário para o SDK do Adobe Experience Platform. |
| [AEP Places](https://github.com/adobe/aepsdk-places-ios) | A extensão do Adobe Experience Platform Places é uma extensão do SDK Swift para Adobe Experience Platform. A extensão AEPPaces permite rastrear eventos de geolocalização conforme definido na interface do usuário do Adobe Places e nas regras do Adobe Launch. |
| [Mensagens AEP](https://github.com/adobe/aepsdk-messaging-ios.git) | A extensão Mensagens da AEP é uma extensão para o SDK Swift da Adobe Experience Platform. A extensão Mensagens da AEP permite enviar tokens de notificação por push e feedback de click-through de notificação por push para a Adobe Experience Platform. |
| [Otimização da AEP](https://github.com/adobe/aepsdk-optimize-ios) | A extensão Otimizar AEP fornece APIs para permitir fluxos de trabalho de personalização em tempo real nos SDKs móveis da Adobe Experience Platform usando o Adobe Target ou o Adobe Journey Optimizer Offer Decisioning. Exige `AEPCore` e `AEPEdge` extensões para enviar eventos de consulta de personalização para a rede Experience Edge. |
| [AEP Assurance](https://github.com/adobe/aepsdk-assurance-ios.git) | O Assurance (também conhecido como projeto Griffon) é um produto novo e inovador para ajudá-lo a inspecionar, testar, simular e validar a maneira como você coleta dados ou veicula experiências em seu aplicativo móvel. |


Após instalar todos os pacotes, seu Xcode **[!UICONTROL Dependências de pacote]** A tela deve ter a seguinte aparência:

![Dependências do pacote Xcode](assets/xcode-package-dependencies.png)


## Importar extensões

No Xcode, navegue até **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL AppDelegate]** e adicione as seguintes importações.

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

Faça o mesmo para **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** > **[!UICONTROL MobileSDK]**.

## Atualizar AppDelegate

Navegue até **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **AppDelegate** no navegador de projetos do Xcode.

1. Defina o `@AppStorage` valor para `environmentFileId` ao valor da ID do arquivo do ambiente de desenvolvimento que você recuperou das tags na etapa 6 da [Gerar instruções de instalação do SDK](configure-tags.md#generate-sdk-install-instructions).

   ```swift
   @AppStorage("environmentFileId") private var environmentFileId = "b5cbd1a1220e/1857ef6cacb5/launch-2594f26b23cd-development"
   ```

1. Adicione o seguinte código à `application(_, didFinishLaunchingWithOptions)` função.

   ```swift
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
   
       // update version and build
       Logger.configuration.info("Luma - Updating version and build number...")
       SettingsBundleHelper.setVersionAndBuildNumber()
   })
   ```

O código acima faz o seguinte:

1. Registra as extensões necessárias.
1. Configura o MobileCore e outras extensões para usar a configuração de propriedade da tag.
1. Ativa o log de depuração. Mais detalhes e opções podem ser encontrados na [Documentação do SDK do Adobe Experience Platform Mobile](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).

>[!IMPORTANT]
>
>Atualize o `MobileCore.configureWith(appId: self.environmentFileId)` com o `appId` com base no `environmentFileId` no ambiente de tags que você está criando para (desenvolvimento, armazenamento temporário ou produção).
>

>[!SUCCESS]
>
>Agora você instalou os pacotes necessários e atualizou seu projeto para registrar corretamente as extensões do SDK do Adobe Experience Platform Mobile necessárias que usará para o restante do tutorial.<br/>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Próximo: **[Configurar o Assurance](assurance.md)**
