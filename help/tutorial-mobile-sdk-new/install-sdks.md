---
title: Instalar SDKs do Adobe Experience Platform Mobile
description: Saiba como implementar o Adobe Experience Platform Mobile SDK em um aplicativo móvel.
hide: true
exl-id: 86348d8b-f428-465d-a79e-ce73d140da79
source-git-commit: c74053b99729269fa42d18372f84fd7c6c2c2e0c
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 1%

---

# Instalar SDKs do Adobe Experience Platform Mobile

Saiba como implementar o Adobe Experience Platform Mobile SDK em um aplicativo móvel.

## Pré-requisitos

* Biblioteca de tags criada com sucesso com as extensões descritas em [lição anterior](configure-tags.md).
* ID do arquivo do ambiente de desenvolvimento do [Instruções de instalação em dispositivos móveis](configure-tags.md#generate-sdk-install-instructions).
* Baixou o vazio [aplicativo de amostra](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}.
* Experiência com [Xcode](Https://developer.apple.com/xcode/){target="_blank"}.

## Objetivos de aprendizagem

Nesta lição, você vai:

* Adicione os SDKs necessários ao seu projeto usando o Gerenciador de pacotes do Swift.
* Registre as extensões.

>[!NOTE]
>
>Em uma implementação de aplicativo móvel, os termos &quot;extensões&quot; e &quot;SDKs&quot; são quase intercambiáveis.

## Gerenciador de pacotes Swift

Em vez de usar CocoaPods e um arquivo Pod (conforme descrito em [Gerar instruções de instalação do SDK](./configure-tags.md#generate-sdk-install-instructions)), você adiciona pacotes individuais usando o gerenciador de pacotes Swift nativo do Xcode. O projeto Xcode já tem todas as dependências de pacotes adicionadas para você. O Xcode **[!UICONTROL Dependências de pacote]** A tela deve ter a seguinte aparência:

![Dependências do pacote Xcode](assets/xcode-package-dependencies.png){zoom=&quot;yes&quot;}


No Xcode, você pode usar **[!UICONTROL Arquivo]** > **[!UICONTROL Adicionar pacotes...]** para adicionar pacotes. A tabela abaixo fornece links para os URLs que você usaria para adicionar pacotes. Os links também direcionam você para mais informações sobre cada pacote específico.

| Pacote | Descrição |
|---|---|
| [AEP Core](https://github.com/adobe/aepsdk-core-ios) | A variável `AEPCore`, `AEPServices`, e `AEPIdentity` As extensões representam a base do SDK do Adobe Experience Platform - todos os aplicativos que usam o SDK devem incluí-las. Esses módulos contêm um conjunto comum de funcionalidades e serviços exigidos por todas as extensões do SDK.<br/><ul><li>`AEPCore` contém a implementação do Hub de eventos. O Hub de eventos é o mecanismo usado para fornecer eventos entre o aplicativo e o SDK. O Hub de eventos também é usado para compartilhar dados entre extensões.</li><li>`AEPServices` O fornece várias implementações reutilizáveis necessárias para suporte à plataforma, incluindo rede, acesso ao disco e gerenciamento de banco de dados.</li><li>`AEPIdentity` implementa a integração com os serviços de identidade da Adobe Experience Platform.</li><li>`AEPSignal` representa a extensão de sinal dos SDKs da Adobe Experience Platform que permite aos profissionais de marketing enviar um &quot;sinal&quot; para seus aplicativos a fim de enviar dados para destinos externos ou abrir URLs.</li><li>`AEPLifecycle` representa a extensão Lifecycle dos SDKs da Adobe Experience Platform que ajuda a coletar métricas de ciclo de vida do aplicativo, como informações de instalação ou atualização do aplicativo, informações de inicialização e sessão do aplicativo, informações do dispositivo e quaisquer dados de contexto adicionais fornecidos pelo desenvolvedor do aplicativo.</li></ul> |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios) | A extensão móvel da Rede de borda da Adobe Experience Platform (`AEPEdge`) permite enviar dados para a Rede da Adobe Edge a partir de um aplicativo para dispositivos móveis. Essa extensão permite implementar os recursos do Adobe Experience Cloud de forma mais robusta, atender a várias soluções de Adobe por meio de uma chamada de rede e, simultaneamente, encaminhar essas informações para a Adobe Experience Platform.<br/>A extensão móvel da Rede de borda é uma extensão para o SDK do Adobe Experience Platform e requer o `AEPCore` e `AEPServices` extensões para manipulação de eventos, bem como a `AEPEdgeIdentity` extensão para recuperar as identidades, como ECID. |
| [Identidade da borda da AEP](https://github.com/adobe/aepsdk-edgeidentity-ios) | A extensão móvel da AEP Edge Identity (`AEPEdgeIdentity`) permite a manipulação de dados de identidade do usuário de um aplicativo móvel ao usar o SDK do Adobe Experience Platform e a extensão Edge Network. |
| [Consentimento de borda da AEP](https://github.com/adobe/aepsdk-edgeconsent-ios) | A extensão móvel da Coleção de consentimento da AEP (`AEPConsent`) ativa a coleção de preferências de consentimento do aplicativo móvel ao usar o SDK do Adobe Experience Platform e a extensão Edge Network. |
| [Perfil de usuário da AEP](https://github.com/adobe/aepsdk-userprofile-ios) | A extensão móvel do perfil de usuário do Adobe Experience Platform (`AEPUserProfile`) é uma extensão para gerenciar perfis de usuário para o SDK do Adobe Experience Platform. |
| [AEP Places](https://github.com/adobe/aepsdk-places-ios) | A extensão do AEP Places (`AEPPlaces`) permite rastrear eventos de geolocalização, conforme definido na interface do Adobe Places e nas regras de tag da coleção de dados do Adobe. |
| [Mensagens AEP](https://github.com/adobe/aepsdk-messaging-ios) | A extensão Mensagens da AEP (`AEPMessaging`) permite enviar tokens de notificação por push e feedback de click-through de notificação por push para a Adobe Experience Platform. |
| [Otimização da AEP](https://github.com/adobe/aepsdk-optimize-ios) | A extensão Otimizar AEP (`AEPOptimize`) fornece APIs para permitir workflows de personalização em tempo real nos SDKs do Adobe Experience Platform Mobile usando o Adobe Target ou o Adobe Journey Optimizer Offer Decisioning. Exige `AEPCore` e `AEPEdge` extensões para enviar eventos de consulta de personalização para a rede Experience Edge. |
| [AEP Assurance](https://github.com/adobe/aepsdk-assurance-ios) | O Assurance (também conhecido como projeto Griffon) é uma extensão nova e inovadora (`AEPAssurance`) para ajudá-lo a inspecionar, testar, simular e validar a maneira como você coleta dados ou fornece experiências em seu aplicativo móvel. Essa extensão habilita seu aplicativo para Assurance. |


## Importar extensões

No Xcode, navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]** e verifique se as importações a seguir fazem parte desse arquivo de origem.

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

Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **AppDelegate** no navegador do Projeto Xcode.

1. Substitua o `@AppStorage` value `YOUR_ENVIRONMENT_ID_GOES_HERE` para `environmentFileId` ao valor da ID do arquivo do ambiente de desenvolvimento que você recuperou das tags na [Gerar instruções de instalação do SDK](configure-tags.md#generate-sdk-install-instructions).

   ```swift
   @AppStorage("environmentFileId") private var environmentFileId = "YOUR_ENVIRONMENT_ID_GOES_HERE"
   ```

1. Adicione o seguinte código à `application(_, didFinishLaunchingWithOptions)` função.

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
1. Ativa o log de depuração. Mais detalhes e opções podem ser encontrados na [Documentação do SDK do Adobe Experience Platform Mobile](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).
1. Inicia o monitoramento do ciclo de vida. Consulte [Ciclo de vida](lifecycle-data.md) etapa no tutorial para obter mais detalhes.
1. Define o consentimento padrão como desconhecido. Consulte [Consentimento](consent.md) etapa no tutorial para obter mais detalhes.

>[!IMPORTANT]
>
>Atualize o `MobileCore.configureWith(appId: self.environmentFileId)` com o `appId` com base no `environmentFileId` no ambiente de tags que você está criando para (desenvolvimento, armazenamento temporário ou produção).
>

>[!SUCCESS]
>
>Agora você instalou os pacotes necessários e atualizou seu projeto para registrar corretamente as extensões do SDK do Adobe Experience Platform Mobile necessárias que usará para o restante do tutorial.
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Próximo: **[Configurar o Assurance](assurance.md)**
