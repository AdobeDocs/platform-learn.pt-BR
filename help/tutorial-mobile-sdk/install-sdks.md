---
title: Instalar SDKs do Adobe Experience Platform Mobile
description: Saiba como implementar o Adobe Experience Platform Mobile SDK em um aplicativo móvel.
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: bc53cb5926f708408a42aa98a1d364c5125cb36d
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 2%

---

# Instalar SDKs do Adobe Experience Platform Mobile

Saiba como implementar o Adobe Experience Platform Mobile SDK em um aplicativo móvel.

>[!INFO]
>
> Este tutorial será substituído por um novo tutorial usando um novo aplicativo móvel de amostra no final de novembro de 2023

## Pré-requisitos

* Biblioteca de tags criada com sucesso com as extensões descritas no [lição anterior](configure-tags.md).
* ID do arquivo do ambiente de desenvolvimento do [Instruções de instalação em dispositivos móveis](configure-tags.md#generate-sdk-install-instructions).
* Baixado, vazio [aplicativo de amostra](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}.
* Experiência com [XCode](Https://developer.apple.com/xcode/){target="_blank"}.
* Básico [linha de comando](https://en.wikipedia.org/wiki/Command-line_interface){target="_blank"} conhecimentos.

## Objetivos de aprendizagem

Nesta lição, você vai:

* Atualize seu arquivo CocoaPod.
* Importe os SDKs necessários.
* Registre as extensões.

>[!NOTE]
>
>Em uma implementação de aplicativo móvel, os termos &quot;extensões&quot; e &quot;SDKs&quot; são quase intercambiáveis.


## Atualizar PodFile

>[!NOTE]
>
> Se você não está familiarizado com CocoaPods, por favor, rever o oficial [guia de introdução](https://guides.cocoapods.org/using/getting-started.html).

A instalação é geralmente um simples comando sudo:

```console
sudo gem install cocoapods
```

Depois de instalar o CocoaPods, abra o Podfile.

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
> `AEPMessaging` só é necessário se você planejar implementar mensagens de push usando o Adobe Journey Optimizer. Leia o tutorial sobre [implementação de mensagens por push com o Adobe Journey Optimizer](journey-optimizer-push.md) para obter mais informações.

Depois de salvar as alterações no Podfile, navegue até a pasta que contém o projeto e execute o `pod install` para instalar as alterações.

![instalação do pod](assets/mobile-install-podfile-install.png)

>[!NOTE]
>
> Se você receber a mensagem &quot;Nenhum Podfile encontrado no diretório do projeto&quot;. erro, o terminal está na pasta errada. Navegue até a pasta com o Podfile que você atualizou e tente novamente.

Se quiser atualizar para a versão mais recente, execute o `pod update` comando.

>[!INFO]
>
>Se você não é capaz de usar CocoaPods em seus próprios aplicativos, você pode aprender sobre outros [implementações compatíveis](https://github.com/adobe/aepsdk-core-ios#binaries) no projeto GitHub.

## Criar CocoaPods

Para construir CocoaPods, abra `Luma.xcworkspace`e selecione **Produto**, seguido por **Limpar pasta de build**.

>[!NOTE]
>
> Talvez seja necessário definir **Criar somente arquitetura ativa** para **Não**. Para fazer isso, selecione o projeto Pods no navegador do projeto, selecione **Configurações de build** e defina o **Criar arquitetura ativa** para **Não**.

Agora você pode criar e executar o projeto.

![configurações de build](assets/mobile-install-build-settings.png)

>[!NOTE]
>
>O projeto Luma foi construído com o Xcode v12.5 em um chipset M1 e é executado no simulador iOS. Se você estiver usando uma configuração diferente, talvez precise alterar as configurações de criação para refletir sua arquitetura.
>
>Se a build não tiver sido bem-sucedida, tente reverter o **Criar arquitetura ativa** > **Depurar** redefinir para **Sim**.
>
>A configuração do simulador &quot;iPod touch (7ª geração)&quot; foi usada durante a criação deste tutorial.

## Importar extensões

Em cada um dos `.swift` adicione as seguintes importações. Comece adicionando a `AppDelegate.swift`.

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

No `AppDelegate.swift` adicione o seguinte código a `didFinishLaunchingWithOptions`. Substitua currentAppId pelo valor da ID do arquivo do ambiente de desenvolvimento que você recuperou das tags na [lição anterior](configure-tags.md).

```swift
let currentAppId = "b5cbd1a1220e/bae66382cce8/launch-88492c6dcb6e-development"

let extensions = [Edge.self, Assurance.self, Lifecycle.self, UserProfile.self, Consent.self, AEPEdgeIdentity.Identity.self, Messaging.self]

MobileCore.setLogLevel(.trace)

MobileCore.registerExtensions(extensions, {
    MobileCore.configureWith(appId: currentAppId)
})
```

`Messaging.self` só é necessário se você planejar implementar mensagens de push por meio do Adobe Journey Optimizer, conforme descrito [aqui](journey-optimizer-push.md).

O código acima faz o seguinte:

* Registra as extensões necessárias.
* Configura o MobileCore e outras extensões para usar a configuração de propriedade da tag.
* Ativa o log de depuração. Mais detalhes e opções podem ser encontrados na [Documentação do SDK móvel](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).

>[!IMPORTANT]
>Em um aplicativo de produção, você deve alternar a AppId com base no ambiente atual (dev/stag/prod).
>

Próximo: **[Configurar o Assurance](assurance.md)**

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)