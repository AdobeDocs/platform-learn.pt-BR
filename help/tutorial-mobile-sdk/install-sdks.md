---
title: Instalar SDKs do Adobe Experience Platform Mobile
description: Saiba como implementar o SDK do Adobe Experience Platform Mobile em um aplicativo para dispositivos móveis.
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 1%

---

# Instalar SDKs do Adobe Experience Platform Mobile

Saiba como implementar o SDK do Adobe Experience Platform Mobile em um aplicativo para dispositivos móveis.

## Pré-requisitos

* Biblioteca de tags criada com êxito com as extensões descritas no [lição anterior](configure-tags.md).
* ID do arquivo do ambiente de desenvolvimento do [Instruções de instalação em dispositivos móveis](configure-tags.md#generate-sdk-install-instructions).
* Baixado, vazio [aplicativo de exemplo](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target=&quot;_blank&quot;}.
* Experiência com [XCode](Https://developer.apple.com/xcode/){target=&quot;_blank&quot;}.
* Básico [linha de comando](https://en.wikipedia.org/wiki/Command-line_interface)Conhecimento de {target=&quot;_blank&quot;}.

## Objetivos de aprendizagem

Nesta lição, você:

* Atualize seu arquivo CocoaPod.
* Importe os SDKs necessários.
* Registre as extensões.

>[!NOTE]
>
>Em uma implementação de aplicativo móvel, os termos &quot;extensões&quot; e &quot;SDKs&quot; são quase permutáveis.


## Atualizar PodFile

>[!NOTE]
>
> Se você não está familiarizado com o CocoaPods, reveja o código [guia de introdução](https://guides.cocoapods.org/using/getting-started.html).

Instalar geralmente é um comando sudo simples:

```console
sudo gem install cocoapods
```

Depois que tiver o CocoaPods instalado, abra o Podfile.

![podfile inicial](assets/mobile-install-initial-podfile.png)

Atualize o arquivo para incluir os seguintes pods:

```swift
pod 'AEPCore', '~> 3'
pod 'AEPEdge', '~> 1'
pod 'AEPUserProfile', '~> 3'
pod 'AEPAssurance', '~> 3'
pod 'AEPServices', '~> 3'
pod 'AEPEdgeConsent', '~> 1'
pod 'AEPLifecycle', '~>3'
pod 'AEPMessaging', '~>1'
pod 'AEPEdgeIdentity', '~>1'
pod 'AEPSignal', '~>3'
```

>[!NOTE]
>
> `AEPMessaging` só é necessário se você planeja implementar mensagens de push usando o Adobe Journey Optimizer. Leia o tutorial em [implementação de mensagens por push com o Adobe Journey Optimizer](journey-optimizer-push.md) para obter mais informações.

Depois de salvar as alterações em seu Podfile, navegue até a pasta com seu projeto e execute o `pod install` para instalar as alterações.

![pod install](assets/mobile-install-podfile-install.png)

>[!NOTE]
>
> Se você receber o arquivo &quot;Nenhum Podfile encontrado no diretório do projeto&quot;. seu terminal está na pasta incorreta. Navegue até a pasta com o Podfile que você atualizou e tente novamente.

Se quiser atualizar para a versão mais recente, execute o `pod update` comando.

>[!INFO]
>
>Se você não conseguir usar o CocoaPods em seus próprios aplicativos, você pode aprender sobre outros [implementações compatíveis](https://github.com/adobe/aepsdk-core-ios#binaries) no projeto GitHub.

## Criar CocoaPods

Para construir CocoaPods, abra `Luma.xcworkspace`e selecione **Produto**, seguida de **Limpar Pasta De Compilação**.

>[!NOTE]
>
> Talvez seja necessário definir **Criar somente arquitetura ativa** para **Não**. Para fazer isso, selecione o projeto Pods no navegador do projeto, selecione **Configurações de build** e defina o **Criar arquitetura ativa** para **Não**.

Agora é possível criar e executar o projeto.

![configurações de build](assets/mobile-install-build-settings.png)

>[!NOTE]
>
>O projeto Luma foi criado com o Xcode v12.5 em um chipset M1 e é executado no simulador iOS. Se estiver usando uma configuração diferente, talvez seja necessário alterar as configurações da build para refletir a arquitetura.
>
>Se a build não tiver sido bem-sucedida, tente reverter a variável **Criar arquitetura ativa** > **Depurar** retornar para **Sim**.
>
>A configuração do simulador &quot;iPod touch (7ª geração)&quot; foi usada durante a criação deste tutorial.

## Importar extensões

Em cada uma das `.swift` , adicione as seguintes importações. Comece adicionando a `AppDelegate.swift`.

```swift
import AEPUserProfile
import AEPAssurance
import AEPEdge
import AEPCore
import AEPEdgeIdentity
import AEPEdgeConsent
import AEPLifecycle
import AEPMessaging //Optional, used for AJO push messaging
import AEPSignal
import AEPServices
```

## Atualizar AppDelegate

No `AppDelegate.swift` , adicione o seguinte código a `didFinishLaunchingWithOptions`. Substitua currentAppId pelo valor de ID de arquivo do ambiente de desenvolvimento que você recuperou das tags no [lição anterior](configure-tags.md).

```swift
let currentAppId = "b5cbd1a1220e/bae66382cce8/launch-88492c6dcb6e-development"

let extensions = [Edge.self, Assurance.self, Lifecycle.self, UserProfile.self, Consent.self, AEPEdgeIdentity.Identity.self, Messaging.self]

MobileCore.setLogLevel(.trace)

MobileCore.registerExtensions(extensions, {
    MobileCore.configureWith(appId: currentAppId)
})
```

`Messaging.self` só é necessário se você planeja implementar mensagens por push via Adobe Journey Optimizer, conforme descrito [here](journey-optimizer-push.md).

O código acima faz o seguinte:

* Registra as extensões necessárias.
* Configura o MobileCore e outras extensões para usar a configuração da propriedade da tag.
* Ativa o log de depuração. Mais detalhes e opções podem ser encontrados na [Documentação do SDK móvel](https://aep-sdks.gitbook.io/docs/getting-started/enable-debug-logging).

>[!IMPORTANT]
>Em um aplicativo de produção, você deve alternar o AppId com base no ambiente atual (dev/stag/prod).

Próximo: **[Configurar Controle](assurance.md)**

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender sobre o Adobe Experience Platform Mobile SDK. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)