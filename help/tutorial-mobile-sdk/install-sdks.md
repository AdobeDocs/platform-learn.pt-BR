---
title: Instalar SDKs do Adobe Experience Platform Mobile
description: Saiba como implementar o Adobe Experience Platform Mobile SDK em um aplicativo móvel.
jira: KT-14627
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---

# Instalar SDKs do Adobe Experience Platform Mobile

Saiba como implementar o Adobe Experience Platform Mobile SDK em um aplicativo móvel.

## Pré-requisitos

* Biblioteca de marcas criada com êxito com as extensões descritas na [lição anterior](configure-tags.md).
* ID do Arquivo de Ambiente de Desenvolvimento das [Instruções de Instalação Móvel](configure-tags.md#generate-sdk-install-instructions).
* Baixe o [aplicativo de amostra](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"} vazio.
* Experiência com [Xcode](Https://developer.apple.com/xcode/){target="_blank"}.

## Objetivos de aprendizagem

Nesta lição, você vai:

* Adicione os SDKs necessários ao seu projeto usando o Gerenciador de pacotes do Swift.
* Registre as extensões.

>[!NOTE]
>
>Em uma implementação de aplicativo móvel, os termos &quot;extensões&quot; e &quot;SDKs&quot; são quase intercambiáveis.

## Gerenciador de pacotes Swift

Em vez de usar CocoaPods e um arquivo Pod (como descrito em [Gerar instruções de instalação do SDK](./configure-tags.md#generate-sdk-install-instructions)), adicione pacotes individuais usando o gerenciador de pacotes Swift nativo do Xcode. O projeto Xcode já tem todas as dependências de pacotes adicionadas para você. A tela **[!UICONTROL Dependências de Pacote]** do Xcode deve ser semelhante a:

![Dependências Do Pacote Xcode](assets/xcode-package-dependencies.png){zoomable="yes"}


No Xcode, você pode usar **[!UICONTROL Arquivo]** > **[!UICONTROL Adicionar pacotes...]** para adicionar pacotes. A tabela abaixo fornece links para os URLs que você usaria para adicionar pacotes. Os links também direcionam você para mais informações sobre cada pacote específico.

| Pacote | Descrição |
|---|---|
| [Núcleo da AEP](https://github.com/adobe/aepsdk-core-ios) | As extensões `AEPCore`, `AEPServices` e `AEPIdentity` representam a base do SDK do Adobe Experience Platform. Todos os aplicativos que usam o SDK devem incluí-los. Esses módulos contêm um conjunto comum de funcionalidades e serviços exigidos por todas as extensões do SDK.<br/><ul><li>`AEPCore` contém a implementação do Hub de Eventos. O Hub de eventos é o mecanismo usado para fornecer eventos entre o aplicativo e o SDK. O Hub de eventos também é usado para compartilhar dados entre extensões.</li><li>O `AEPServices` fornece várias implementações reutilizáveis necessárias para suporte à plataforma, incluindo rede, acesso a disco e gerenciamento de banco de dados.</li><li>`AEPIdentity` implementa a integração com os serviços de identidade da Adobe Experience Platform.</li><li>`AEPSignal` representa a extensão de Sinal dos SDKs da Adobe Experience Platform que permite aos profissionais de marketing enviar um &quot;sinal&quot; para seus aplicativos enviar dados para destinos externos ou abrir URLs.</li><li>`AEPLifecycle` representa a extensão de ciclo de vida dos SDKs da Adobe Experience Platform que ajuda a coletar métricas de ciclo de vida do aplicativo, como informações de instalação ou atualização do aplicativo, informações de inicialização e sessão do aplicativo, informações do dispositivo e quaisquer dados de contexto adicionais fornecidos pelo desenvolvedor do aplicativo.</li></ul> |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios) | A extensão para dispositivos móveis Adobe Experience Platform Edge Network (`AEPEdge`) permite enviar dados para a Rede Adobe Edge a partir de um aplicativo para dispositivos móveis. Essa extensão permite implementar os recursos do Adobe Experience Cloud de forma mais robusta, atender a várias soluções de Adobe por meio de uma chamada de rede e, simultaneamente, encaminhar essas informações para a Adobe Experience Platform.<br/>A extensão móvel do Edge Network é uma extensão para o SDK do Adobe Experience Platform e requer as extensões `AEPCore` e `AEPServices` para manipulação de eventos, bem como a extensão `AEPEdgeIdentity` para recuperação de identidades, como ECID. |
| [Identidade do AEP Edge](https://github.com/adobe/aepsdk-edgeidentity-ios) | A extensão para dispositivos móveis da AEP Edge Identity (`AEPEdgeIdentity`) permite o tratamento de dados de identidade do usuário de um aplicativo para dispositivos móveis ao usar o SDK do Adobe Experience Platform e a extensão Edge Network. |
| [Consentimento da AEP para Edge](https://github.com/adobe/aepsdk-edgeconsent-ios) | A extensão para dispositivos móveis da Coleção de consentimento da AEP (`AEPConsent`) habilita a coleção de preferências de consentimento do aplicativo para dispositivos móveis ao usar o SDK da Adobe Experience Platform e a extensão Edge Network. |
| [Perfil de usuário da AEP](https://github.com/adobe/aepsdk-userprofile-ios) | A extensão Móvel do Perfil de Usuário do Adobe Experience Platform (`AEPUserProfile`) é uma extensão para gerenciar perfis de usuário para o SDK do Adobe Experience Platform. |
| [AEP Places](https://github.com/adobe/aepsdk-places-ios) | A extensão do AEP Places (`AEPPlaces`) permite rastrear eventos de geolocalização conforme definido na interface do Adobe Places e nas regras de tag da coleção de dados do Adobe. |
| [Mensagens da AEP](https://github.com/adobe/aepsdk-messaging-ios) | A extensão de Mensagens da AEP (`AEPMessaging`) permite enviar tokens de notificação por push e feedback de click-through de notificação por push para a Adobe Experience Platform. |
| [Otimização da AEP](https://github.com/adobe/aepsdk-optimize-ios) | A extensão de Otimização da AEP (`AEPOptimize`) fornece APIs para permitir fluxos de trabalho de personalização em tempo real nos SDKs do Adobe Experience Platform Mobile usando o Adobe Target ou o Adobe Journey Optimizer Offer Decisioning. Ela requer as extensões `AEPCore` e `AEPEdge` para enviar eventos de consulta de personalização para a rede da Experience Edge. |
| [Garantia da AEP](https://github.com/adobe/aepsdk-assurance-ios) | O Assurance (também conhecido como projeto Griffon) é uma extensão nova e inovadora (`AEPAssurance`) para ajudá-lo a inspecionar, testar, simular e validar a maneira como você coleta dados ou veicula experiências em seu aplicativo móvel. Essa extensão habilita seu aplicativo para Assurance. |


## Importar extensões

No Xcode, navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]** e verifique se as seguintes importações fazem parte deste arquivo de origem.

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

1. Substitua o `@AppStorage` valor `YOUR_ENVIRONMENT_ID_GOES_HERE` de `environmentFileId` pelo valor da ID do Arquivo do Ambiente de Desenvolvimento que você recuperou das marcas em [Gerar instruções de instalação do SDK](configure-tags.md#generate-sdk-install-instructions).

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
1. Ativa o log de depuração. Mais detalhes e opções podem ser encontrados na [documentação do SDK do Adobe Experience Platform Mobile](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).
1. Inicia o monitoramento do ciclo de vida. Consulte a etapa [Ciclo de vida](lifecycle-data.md) do tutorial para obter mais detalhes.
1. Define o consentimento padrão como desconhecido. Consulte a etapa [Consentimento](consent.md) do tutorial para obter mais detalhes.

>[!IMPORTANT]
>
>Atualize `MobileCore.configureWith(appId: self.environmentFileId)` com o `appId` baseado no `environmentFileId` do ambiente de marcas para o qual você está criando (desenvolvimento, preparo ou produção).
>

>[!SUCCESS]
>
>Agora você instalou os pacotes necessários e atualizou seu projeto para registrar corretamente as extensões do SDK do Adobe Experience Platform Mobile necessárias que usará para o restante do tutorial.
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-os nesta [postagem de Discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Próximo: **[Configurar o Assurance](assurance.md)**
