---
title: Lidar com WebViews com o SDK móvel da plataforma
description: Saiba como lidar com a coleta de dados com WebViews em um aplicativo móvel.
jira: KT-14632
exl-id: 9b3c96fa-a1b8-49d2-83fc-ece390b9231c
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

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

Se você enviar dados da parte nativa do aplicativo e de um WebView dentro do aplicativo, cada um gera sua própria ID de Experience Cloud (ECID), o que resulta em ocorrências desconectadas e dados inflacionados de visitas/visitantes. Mais informações sobre a ECID podem ser encontradas na [visão geral da ECID](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en).

Para resolver essa situação indesejável, é importante transmitir a ECID do usuário da parte nativa do aplicativo para um WebView que você possa desejar usar no aplicativo.

A extensão de identidade da AEP Edge usada no WebView coleta a ECID atual e a adiciona ao URL em vez de enviar uma solicitação ao Adobe para obter uma nova ID. A implementação usa essa ECID para solicitar o URL.

## Implementação

Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Info]** > **[!DNL TermsOfServiceSheet]** e localize a função `func loadUrl()` na classe `final class SwiftUIWebViewModel: ObservableObject`. Adicione a seguinte chamada para lidar com a exibição da Web:

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

A API [`AEPEdgeIdentity.Identity.getUrlVariables`](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) configura as variáveis para que a URL contenha todas as informações relevantes, como ECID e muito mais. No exemplo, você está usando um arquivo local, mas os mesmos conceitos se aplicam a páginas remotas.

Você pode saber mais sobre a API `Identity.getUrlVariables` no [Guia de referência de API de Identidade para extensão do Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables).

## Validar

Para executar o código:

1. Revise a seção [instruções de configuração](assurance.md#connecting-to-a-session) para conectar seu simulador ou dispositivo ao Assurance.
1. Vá para as **[!UICONTROL Configurações]** do aplicativo
1. Toque no botão **[!DNL View...]** para mostrar **[!DNL Terms of Use]**.

   <img src="./assets/tou1.png" width="300" /> <img src="./assets/tou2.png" width="300" />

1. Na interface do usuário do Assurance, procure o evento **[!UICONTROL Variáveis de URL de resposta de identidade da Edge]** do fornecedor **[!UICONTROL com.adobe.griffon.mobile]**.
1. Selecione o evento e revise o campo **[!UICONTROL urlvariable]** no objeto **[!UICONTROL ACPExtensionEventData]**, confirmando se os seguintes parâmetros estão presentes na URL: `adobe_mc`, `mcmid` e `mcorgid`.

   ![validação de webview](assets/webview-validation.png)

   Um exemplo de campo `urvariables` pode ser visto abaixo:

   * Original (com caracteres de escape)

     ```html
     adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg
     ```

   * Embelado

     ```html
     adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
     ```

Infelizmente, a depuração da sessão da Web é limitada. Por exemplo, você não pode usar o Adobe Experience Platform Debugger no navegador para continuar a depurar a sessão do webview.

>[!NOTE]
>
>A compilação de visitantes por meio desses parâmetros de URL é suportada no SDK da Web da plataforma (versões 2.11.0 ou posterior) e ao usar `VisitorAPI.js`.


>[!SUCCESS]
>
>Agora você configurou o aplicativo para mostrar conteúdo com base em um URL em uma visualização da Web usando a mesma ECID que a ECID já emitida pelo SDK do Adobe Experience Platform Mobile.
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-os nesta [postagem de Discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Próximo: **[Identidade](identity.md)**
