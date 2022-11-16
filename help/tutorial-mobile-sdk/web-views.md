---
title: Gerenciar WebViews
description: Saiba como lidar com a coleta de dados com WebViews em um aplicativo móvel.
kt: 6987
exl-id: 9b3c96fa-a1b8-49d2-83fc-ece390b9231c
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 1%

---

# Gerenciar WebViews

Saiba como lidar com a coleta de dados com WebViews em um aplicativo móvel.

## Pré-requisitos

* Aplicativo criado e executado com êxito com SDKs instalados e configurados.

## Objetivos de aprendizagem

Nesta lição, você:

* Entenda por que você deve ter considerações especiais para WebViews.
* Entenda o código necessário para evitar problemas de rastreamento.

## Possíveis problemas de rastreamento

Se você enviar dados da parte nativa do aplicativo e um WebView, cada um gera sua própria Experience Cloud ID (ECID). Isso resulta em ocorrências desconectadas e dados inflados de visita/visitante. Mais informações sobre a ECID podem ser encontradas no [Visão geral da ECID](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en).

Para resolver essa situação indesejável, é importante passar o ECID do usuário da porção nativa para o WebView.

A extensão JavaScript do serviço de Experience Cloud ID no WebView extrai a ECID do URL em vez de enviar uma solicitação ao Adobe para obter uma nova ID. O serviço de ID usa essa ECID para rastrear o visitante.

## Implementação

No aplicativo de amostra Luma, localize a variável `TermsOfService.swift` (no `Intro-Login_SignUp` e localize o seguinte código:

```swift
// Show tou.html
let url = Bundle.main.url(forResource: "tou", withExtension: "html")
let myRequest = URLRequest(url: url!)
self.webView.load(myRequest)
```

Esta é uma maneira simples de carregar um WebView. Nesse caso, é um arquivo local, mas os mesmos conceitos se aplicam a páginas remotas.

Refatere o código de visualização da Web conforme mostrado abaixo:

```swift
let url = Bundle.main.url(forResource: "tou", withExtension: "html")
if var urlString = url?.absoluteString {
    // Adobe Experience Platform - Handle Web View
    AEPEdgeIdentity.Identity.getUrlVariables {(urlVariables, error) in
        if let error = error {
            self.simpleAlert("\(error.localizedDescription)")
            return;
        }

        if let urlVariables: String = urlVariables {
            urlString.append("?" + urlVariables)
        }

        DispatchQueue.main.async {
            self.webView.load(URLRequest(url: URL(string: urlString)!))
        }
        print("Successfully retrieved urlVariables for WebView, final URL: \(urlString)")
    }
} else {
    self.simpleAlert("Failed to create URL for webView")
}
```

Você pode saber mais sobre o `Identity.getUrlVariables` na API do [Guia de referência da API da extensão de rede de borda](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network/api-reference#geturlvariables).

## Validação

Depois de revisar o [instruções de configuração](assurance.md) e conectando seu simulador ou dispositivo ao Controle, carregue o WebView e procure o `Edge Identity Response URL Variables` do `com.adobe.griffon.mobile` fornecedor.

Para carregar o WebView, vá para a tela inicial do aplicativo Luma, selecione o ícone &quot;account&quot;, seguido pelo &quot;Termos de uso&quot; no rodapé.

Após carregar o WebView, selecione o evento e revise a `urlvariables` no campo `ACPExtensionEventData` , confirmando que os seguintes parâmetros estão presentes no URL: `adobe_mc`, `mcmid`e `mcorgid`.

![validação de visualização da web](assets/mobile-webview-validation.png)

Uma amostra `urvariables` pode ser visto abaixo:

```html
// Original (with escaped characters)
adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg

// Beautified
adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
```

>[!NOTE]
>
>A identificação de visitantes por meio desses parâmetros de URL é atualmente compatível com o SDK da Web da plataforma (versões 2.11.0 ou posterior) e `VisitorAPI.js`.


Próximo: **[Identidade](identity.md)**

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender sobre o Adobe Experience Platform Mobile SDK. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)