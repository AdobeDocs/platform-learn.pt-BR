---
title: Manipular WebViews
description: Saiba como lidar com a coleta de dados com WebViews em um aplicativo móvel.
jira: KT-6987
exl-id: 9b3c96fa-a1b8-49d2-83fc-ece390b9231c
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 1%

---

# Manipular WebViews

Saiba como lidar com a coleta de dados com WebViews em um aplicativo móvel.

## Pré-requisitos

* O aplicativo com SDKs instalados e configurados foi criado e executado com sucesso.

## Objetivos de aprendizagem

Nesta lição, você vai:

* Entenda por que você deve considerar especialmente as WebViews.
* Entenda o código necessário para evitar problemas de rastreamento.

## Possíveis problemas de rastreamento

Se você enviar dados da parte nativa do aplicativo e um WebView, cada um gera sua própria ID de Experience Cloud (ECID). Isso resulta em ocorrências desconectadas e dados de visita/visitante aumentados. Mais informações sobre a ECID podem ser encontradas na [Visão geral da ECID](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en).

Para resolver essa situação indesejável, é importante transmitir a ECID do usuário da parte nativa para o WebView.

A extensão JavaScript do serviço de ID do Experience Cloud no WebView extrai a ECID do URL em vez de enviar uma solicitação ao Adobe para obter uma nova ID. O serviço de ID usa essa ECID para rastrear o visitante.

## Implementação

No aplicativo de amostra Luma, localize o `TermsOfService.swift` (no campo `Intro-Login_SignUp` e localize o seguinte código:

```swift
// Show tou.html
let url = Bundle.main.url(forResource: "tou", withExtension: "html")
let myRequest = URLRequest(url: url!)
self.webView.load(myRequest)
```

Essa é uma maneira simples de carregar um WebView. Nesse caso, é um arquivo local, mas os mesmos conceitos se aplicam a páginas remotas.

Refatore o código de visualização da web conforme mostrado abaixo:

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

Você pode saber mais sobre o `Identity.getUrlVariables` API no [Guia de referência de API de extensão de identidade para rede de borda](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables).

## Validação

Depois de revisar o [instruções de configuração](assurance.md) e conectando seu simulador ou dispositivo ao Assurance, carregue o WebView e procure o `Edge Identity Response URL Variables` evento do `com.adobe.griffon.mobile` fornecedor.

Para carregar o WebView, vá para a tela inicial do aplicativo Luma, selecione o ícone &quot;conta&quot;, seguido pelos &quot;Termos de uso&quot; no rodapé.

Depois de carregar o WebView, selecione o evento e revise o `urlvariables` no campo `ACPExtensionEventData` , confirmando se os seguintes parâmetros estão presentes no URL: `adobe_mc`, `mcmid`, e `mcorgid`.

![validação de webview](assets/mobile-webview-validation.png)

Uma amostra `urvariables` O campo pode ser visto abaixo:

```html
// Original (with escaped characters)
adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg

// Beautified
adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
```

>[!NOTE]
>
>No momento, a compilação de visitantes por meio desses parâmetros de URL é compatível com o SDK da Web da plataforma (versões 2.11.0 ou posteriores) e `VisitorAPI.js`.


Próximo: **[Identidade](identity.md)**

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar feedback geral ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)