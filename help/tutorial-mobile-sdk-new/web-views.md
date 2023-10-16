---
title: Manipular WebViews
description: Saiba como lidar com a coleta de dados com WebViews em um aplicativo móvel.
jira: KT-6987
hide: true
exl-id: 0c8818f7-39d3-496e-a835-2d85d50e50d6
source-git-commit: 5d34e510ef72190762c29b71359b362ef4be7b22
workflow-type: tm+mt
source-wordcount: '490'
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

Se você enviar dados da parte nativa do aplicativo e de um WebView dentro do aplicativo, cada um gera sua própria ID de Experience Cloud (ECID), o que resulta em ocorrências desconectadas e dados inflacionados de visitas/visitantes. Mais informações sobre a ECID podem ser encontradas na [Visão geral da ECID](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en).

Para resolver essa situação indesejável, é importante transmitir a ECID do usuário da parte nativa do aplicativo para um WebView que você possa desejar usar no aplicativo.

A extensão de identidade de borda da AEP usada no WebView coleta a ECID atual e a adiciona ao URL em vez de enviar uma solicitação ao Adobe para uma nova ID. A implementação usa essa ECID para solicitar o URL.

## Implementação

Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Info]** > **[!DNL TermsOfServiceSheet]** e localize o `func loadUrl()` na caixa `final class SwiftUIWebViewModel: ObservableObject` classe. Adicione a seguinte chamada para lidar com a exibição da Web:

```swift
// Handle web view
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

A variável [`AEPEdgeIdentity.Identity.getUrlVariables`](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) A API configura as variáveis para que o URL contenha todas as informações relevantes, como ECID e muito mais. No exemplo, você está usando um arquivo local, mas os mesmos conceitos se aplicam a páginas remotas.

Você pode saber mais sobre o `Identity.getUrlVariables` API no [Guia de referência de API de extensão de identidade para rede de borda](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables).

## Validar 

Para executar o código:

1. Revise o [instruções de configuração](assurance.md#connecting-to-a-session) seção para conectar seu simulador ou dispositivo ao Assurance.
1. Vá para a **[!UICONTROL Configurações]** no aplicativo
1. Toque no **[!DNL View...]** botão para mostrar a **[!DNL Terms of Use]**.

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

Infelizmente, a depuração da sessão da Web é limitada; você não pode usar o Adobe Experience Platform Debugger no seu navegador, por exemplo, para continuar a depurar a sessão do webview.

>[!NOTE]
>
>A compilação de visitantes por meio desses parâmetros de URL é compatível com o SDK da Web da plataforma (versões 2.11.0 ou posterior) e ao usar `VisitorAPI.js`.


>[!SUCCESS]
>
>Agora você configurou o aplicativo para mostrar conteúdo com base em um URL em uma visualização da Web usando a mesma ECID que a ECID já emitida pelo SDK do Adobe Experience Platform Mobile.<br/>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Próximo: **[Identidade](identity.md)**
