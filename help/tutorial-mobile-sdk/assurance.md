---
title: Configurar Controle
description: Saiba como implementar a extensão Assurance em um aplicativo móvel.
exl-id: e15774b2-2f52-400f-9313-bb4338a88918
source-git-commit: 7df759ec0ea248ee91ae673e3468ffa3f6cc5be5
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 2%

---

# Assurance

Saiba como configurar o Adobe Experience Platform Assurance em um aplicativo móvel.

O Assurance, formalmente conhecido como Project Griffon, foi projetado para ajudar você a inspecionar, provar, simular e validar como você coleta dados ou veicula experiências em seu aplicativo móvel.

O Assurance ajuda a inspecionar eventos brutos do SDK gerados pelo SDK do Adobe Experience Platform Mobile. Todos os eventos coletados pelo SDK estão disponíveis para inspeção. Os eventos do SDK são carregados em uma exibição de lista, classificados por tempo. Cada evento tem uma exibição detalhada que fornece mais detalhes. Também são fornecidas exibições adicionais para navegar pela configuração do SDK, elementos de dados, estados compartilhados e versões de extensão do SDK. Saiba mais sobre o [Controle](https://aep-sdks.gitbook.io/docs/foundation-extensions/adobe-experience-platform-assurance) na documentação do produto.


## Pré-requisitos

* Criação e execução bem-sucedidas do aplicativo de amostra com SDKs instalados e configurados.

## Objetivos de aprendizagem

Nesta lição, você:

* Confirme se sua organização tem acesso (e solicite-o caso não tenha).
* Configure seu URL básico.
* Adicione o código específico do iOS necessário.
* Conecte-se a uma sessão.

## Confirmar acesso

Confirme se sua organização tem acesso ao Controle completando as seguintes etapas:

1. Visita [https://experience.adobe.com/#/assurance](https://experience.adobe.com/griffon){target="_blank"}
1. Faça logon usando suas credenciais do Adobe ID para o Experience Cloud.
1. Se você for trazido para o **[!UICONTROL Sessões]** , depois você tem acesso. Se você for trazido para a página de acesso beta, selecione **[!UICONTROL Registrar]**.

## Implementação

Além do [Instalação do SDK](install-sdks.md) Se você tiver concluído a lição anterior, a iOS também exigirá a seguinte adição. Adicione o seguinte código ao arquivo `AppDelegate.swift`:

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey: Any] = [:]) -> Bool {
    Assurance.startSession(url: url)
    return true
}
```

O exemplo de Luma fornecido para este tutorial usa o iOS 12.0. Se você estiver seguindo junto com seu próprio aplicativo baseado em cena usando o iOS 13 e posterior, use o `UISceneDelegate's scene(_:openURLContexts:)` método como segue:

```swift
func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>) {
    // Called when the app in background is opened with a deep link.
    if let deepLinkURL = URLContexts.first?.url {
        Assurance.startSession(url: deepLinkURL)
    }
}
```

Mais informações podem ser encontradas [here](https://aep-sdks.gitbook.io/docs/foundation-extensions/adobe-experience-platform-assurance#implement-aep-assurance-session-start-apis-ios-only){target="_blank"}.

## Configurar um URL base

1. Abra o XCode e selecione o nome do projeto.
1. Navegue até o **Informações** guia .
1. Role para baixo até **Tipos de URL** e selecione o **+** para adicionar um novo.
1. Definir **Identificador** e **Esquemas de URL** para &quot;lumadeeplink&quot;.
1. Crie e execute o aplicativo.

![url de garantia](assets/mobile-assurance-url-type.png)

Para saber mais sobre Esquemas de URL no iOS, consulte [Documentação do Apple](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target="_blank"}.

O Assurance funciona abrindo um URL, seja via navegador ou código QR, esse URL começa com o URL base que abre o aplicativo e contém parâmetros adicionais. Esses parâmetros exclusivos são usados para conectar a sessão.

## Conexão com uma sessão

1. Navegue até o [Interface de usuário de garantia](https://experience.adobe.com/griffon){target="_blank"}.
1. Selecionar **[!UICONTROL Criar sessão]**.
1. Fornecer **[!UICONTROL Nome da sessão]** como `Luma App QA` e **[!UICONTROL URL básica]** `lumadeeplink://default`
1. Selecione **[!UICONTROL Próximo]**.
   ![sessão de criação de seguro](assets/mobile-assurance-create-session.png)
1. **[!UICONTROL Verificar código QR]** se você estiver usando um dispositivo físico. Se você estiver usando o simulador, então **[!UICONTROL Copiar link]** e abra-o com Safari no simulador.
   ![código de controle de qualidade](assets/mobile-assurance-qr-code.png)
1. Quando o aplicativo é carregado, você é apresentado com uma modal solicitando que você insira o PIN da etapa anterior.
   ![pino de entrada de seguro](assets/mobile-assurance-enter-pin.png)
1. Se a conexão tiver sido bem-sucedida, você verá eventos na interface do usuário da Web Assurance e um ícone de Garantia flutuante no aplicativo.
   * Ícone de controle flutuante.
      ![modal de garantia](assets/mobile-assurance-modal.png)
   * Experience Cloud events que vêm na interface do usuário da Web.
      ![eventos de controle](assets/mobile-assurance-events.png)

Se você encontrar algum desafio, revise a [técnico](https://aep-sdks.gitbook.io/docs/foundation-extensions/adobe-experience-platform-assurance){target="_blank"} and [general documentation](https://aep-sdks.gitbook.io/docs/beta/project-griffon){target="_blank"}.

Próximo: **[Consentimento](consent.md)**

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender sobre o Adobe Experience Platform Mobile SDK. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
