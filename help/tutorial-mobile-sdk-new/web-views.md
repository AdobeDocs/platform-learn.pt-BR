---
title: Manipular WebViews
description: Saiba como lidar com a coleta de dados com WebViews em um aplicativo móvel.
jira: KT-6987
hide: true
source-git-commit: e119e2bdce524c834cdaf43ed9eb9d26948b0ac6
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---


# Manipular WebViews

Saiba como lidar com a coleta de dados com WebViews em um aplicativo móvel.

## Pré-requisitos

* O aplicativo com SDKs instalados e configurados foi criado e executado com sucesso.

## Objetivos de aprendizagem

Nesta lição, você vai:

* Entenda por que você deve considerar especialmente os WebViews no aplicativo.
* Entenda o código necessário para evitar problemas de rastreamento.

## Possíveis problemas de rastreamento

Se você enviar dados da parte nativa do aplicativo e um WebView, cada um gera sua própria ID de Experience Cloud (ECID), o que resulta em ocorrências desconectadas e dados inflados de visita/visitante. Mais informações sobre a ECID podem ser encontradas na [Visão geral da ECID](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en).

Para resolver essa situação indesejável, é importante transmitir a ECID do usuário da parte nativa do aplicativo para um WebView que você possa desejar usar no aplicativo.

A extensão JavaScript do serviço de ID do Experience Cloud no WebView extrai a ECID do URL em vez de enviar uma solicitação ao Adobe para obter uma nova ID. O serviço de ID usa essa ECID para rastrear o visitante.

## Implementação

Navegue até **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Visualizações]** > **[!UICONTROL Informações]** > **[!UICONTROL TermsOfServiceSheet]** e localize o `func loadUrl()` na caixa `final class SwiftUIWebViewModel: ObservableObject` classe. Adicione a seguinte chamada para lidar com a exibição da Web:

```swift
// Adobe Experience Platform - Handle Web View
AEPEdgeIdentity.Identity.getUrlVariables {(urlVariables, error) in
    if let error = error {
        print("Error with Webview", error)
        return;
    }
    
    if let urlVariables: String = urlVariables {
        urlString.append("?" + urlVariables)
        guard let url = URL(string: urlString) else {
            return
        }
        DispatchQueue.main.async {
            self.webView.load(URLRequest(url: url))
        }
    }
    Logger.aepMobileSDK.info("Successfully retrieved urlVariables for WebView, final URL: \(urlString)")
}
```

A variável `AEPEdgeIdentity.Identity.getUrlVariables` A API configura as variáveis para que o URL contenha todas as informações relevantes, como ECID e muito mais. No exemplo, você está usando um arquivo local, mas os mesmos conceitos se aplicam a páginas remotas.

Você pode saber mais sobre o `Identity.getUrlVariables` API no [Guia de referência de API de extensão de identidade para rede de borda](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables).

## Validação

Para executar o código:

1. Vá para a **[!UICONTROL Configurações]** no aplicativo
1. Toque no **[!UICONTROL Exibir...]** botão para mostrar a **[!UICONTROL Termos de uso]**.

   <img src="./assets/tou1.png" width="300" /> <img src="./assets/tou2.png" width="300" />

1. Na interface do usuário do Assurance, procure pela variável **[!UICONTROL Variáveis de URL de resposta da Identidade de borda]** evento do **[!UICONTROL com.adobe.griffon.mobile]** fornecedor.
1. Selecione o evento e revise a **[!UICONTROL urlvariable]** no campo **[!UICONTROL ACPExtensionEventData]** , confirmando se os seguintes parâmetros estão presentes no URL: `adobe_mc`, `mcmid`, e `mcorgid`.

   ![validação de webview](assets/webview-validation.png)

   Uma amostra `urvariables` O campo pode ser visto abaixo:

   * Original (com caracteres de escape)

     ```html
     adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg
     ```

   * Embelado

     ```html
     adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
     ```

>[!NOTE]
>
>A compilação de visitantes por meio desses parâmetros de URL é compatível com o SDK da Web da plataforma (versões 2.11.0 ou posterior) e ao usar `VisitorAPI.js`.


>[!SUCCESS]
>
>Agora você configurou o aplicativo para mostrar conteúdo com base em um URL em uma visualização da Web usando a mesma ECID que a ECID já emitida pelo SDK do Adobe Experience Platform Mobile.<br/>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Próximo: **[Identidade](identity.md)**
