---
title: Rastrear dados do evento
description: Saiba como rastrear dados do evento em um aplicativo móvel.
hide: true
exl-id: b926480b-b431-4db8-835c-fa1db6436a93
source-git-commit: 4434bee35591d7cf79b7dddc03faba83d00b31f5
workflow-type: tm+mt
source-wordcount: '1390'
ht-degree: 1%

---

# Rastrear dados do evento

Saiba como rastrear eventos em um aplicativo móvel.

A extensão Edge Network fornece uma API para enviar eventos de experiência para a Platform Edge Network. Um Evento de experiência é um objeto que contém dados em conformidade com a definição do esquema XDM ExperienceEvent. De maneira mais simples, eles capturam o que as pessoas fazem no seu aplicativo móvel. Depois que os dados forem recebidos pela Platform Edge Network, poderão ser encaminhados para aplicativos e serviços configurados no fluxo de dados, como Adobe Analytics e Experience Platform. Saiba mais sobre o [Eventos de experiência](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) na documentação do produto.

## Pré-requisitos

* Todas as dependências de pacote estão em vigor no projeto Xcode.
* Extensões registradas no **[!UICONTROL AppDelegate]**.
* Extensão MobileCore configurada para usar seu desenvolvimento `appId`.
* SDKs importados.
* O aplicativo foi criado e executado com sucesso com as alterações acima.

## Objetivos de aprendizagem

Nesta lição, você

* Entenda como estruturar dados XDM com base em um esquema.
* Enviar um evento XDM com base em um grupo de campos padrão.
* Enviar um evento XDM com base em um grupo de campos personalizado.
* Envie um evento de compra XDM.
* Validar com garantia.

## Construção de um evento de experiência

A extensão de borda do Adobe Experience Platform pode enviar eventos que seguem um esquema XDM definido anteriormente para a Rede de borda da Adobe Experience Platform.

O processo é assim...

1. Identifique a interação do aplicativo móvel que você está tentando rastrear.

1. Revise seu esquema e identifique o evento apropriado.

1. Revise seu esquema e identifique campos adicionais que devem ser usados para descrever o evento.

1. Construir e preencher o objeto de dados.

1. Criar e enviar evento.

1. Validar.


### Grupos de campos padrão

Para os grupos de campos padrão, o processo é semelhante a:

* No esquema, identifique os eventos que você está tentando coletar. Neste exemplo, você está rastreando eventos de experiência de comércio, por exemplo, uma exibição de produto (**[!UICONTROL productViews]**).

  ![esquema de exibição de produto](assets/datacollection-prodView-schema.png)

* Para construir um objeto contendo os dados do evento de experiência em seu aplicativo, você usaria o código como:

  ```swift
  var xdmData: [String: Any] = [
      "eventType": "commerce.productViews",
      "commerce": [
          "productViews": [
            "value": 1
          ]
      ]
  ]
  ```

   * `eventType`: descreve o evento que ocorreu, use um [valor conhecido](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) quando possível.
   * `commerce.productViews.value`: o valor numérico ou booleano do evento. Se for um Booleano (ou &quot;Contador&quot; no Adobe Analytics), o valor sempre será definido como 1. Se for um evento numérico ou de moeda, o valor poderá ser > 1.

* No esquema, identifique quaisquer dados adicionais associados ao evento de visualização de produto de comércio. Neste exemplo, inclua **[!UICONTROL productListItems]** que é um conjunto padrão de campos usados com qualquer evento relacionado ao comércio:

  ![esquema de itens da lista de produtos](assets/datacollection-prodListItems-schema.png)
   * Observe que **[!UICONTROL productListItems]** O é um array para que vários produtos possam ser fornecidos.

* Para adicionar esses dados, expanda suas `xdmData` objeto para incluir dados suplementares:

  ```swift
  var xdmData: [String: Any] = [
      "eventType": "commerce.productViews",
          "commerce": [
          "productViews": [
              "value": 1
          ]
      ],
      "productListItems": [
          [
              "name":  productName,
              "SKU": sku,
              "priceTotal": priceString,
              "quantity": 1
          ]
      ]
  ]
  ```

* Agora você pode usar essa estrutura de dados para criar um `ExperienceEvent`:

  ```swift
  let productViewEvent = ExperienceEvent(xdm: xdmData)
  ```

* E envie o evento e os dados para a Rede de borda da Platform usando o `sendEvent` API:

  ```swift
  Edge.sendEvent(experienceEvent: productViewEvent)
  ```

A variável [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) A API é o SDK do AEP Mobile equivalente ao [`MobileCore.trackAction`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction) e [`MobileCore.trackState`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackstate) Chamadas de API. Consulte [Migração da extensão para dispositivos móveis do Analytics para a Rede de borda da Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/migrate-to-edge-network/) para obter mais informações.

Agora, você implementará realmente esse código em seu projeto Xcode.
Você tem diferentes ações relacionadas a produtos de comércio em seu aplicativo e deseja enviar eventos, com base nessas ações conforme executadas pelo usuário:

* exibir: ocorre quando um usuário exibe um produto específico,
* adicionar ao carrinho: quando um usuário toca <img src="assets/addtocart.png" width="20" /> em uma tela de detalhes do produto,
* salvar para mais tarde: quando um usuário tocar <img src="assets/saveforlater.png" width="15" /> em uma tela de detalhes do produto,
* compra: quando um usuário toca <img src="assets/purchase.png" width="20" /> em uma tela de detalhes do produto.

Para implementar o envio de eventos de experiência relacionados ao comércio de maneira reutilizável, use uma função dedicada:

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** no navegador do Projeto Xcode, e adicione o seguinte à `func sendCommerceExperienceEvent(commerceEventType: String, product: Product)` função.

   ```swift
   // Set up a data dictionary, create an experience event and send the event.
   let xdmData: [String: Any] = [
       "eventType": "commerce." + commerceEventType,
       "commerce": [
           commerceEventType: [
               "value": 1
           ]
       ],
       "productListItems": [
           [
               "name": product.name,
               "priceTotal": product.price,
               "SKU": product.sku
           ]
       ]
   ]
   
   let commerceExperienceEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: commerceExperienceEvent)
   ```

   Essa função considera o tipo de evento de experiência de comércio e o produto como parâmetros e

   * define a carga XDM como um dicionário, usando os parâmetros da função,
   * configura um evento de experiência usando o dicionário,
   * envia o evento de experiência usando o [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API.

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!UICONTROL ProductView]** no navegador do Projeto Xcode e adicione várias chamadas à `sendCommerceExperienceEvent` função:

   1. No `.task` modificador, dentro do `ATTrackingManager.trackingAuthorizationStatus` encerramento. Este `.task` o modificador é chamado quando a exibição de produto é inicializada e exibida, para que você queira enviar um evento de exibição de produto naquele momento específico.

      ```swift
      // Send productViews commerce experience event
      MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productViews", product: product)
      ```

   1. Para cada um dos botões (<img src="assets/saveforlater.png" width="15" />, <img src="assets/addtocart.png" width="20" /> e <img src="assets/purchase.png" width="20" />) na barra de ferramentas, adicione a chamada relevante na variável `ATTrackingManager.trackingAuthorizationStatus == .authorized` encerramento:

      1. Para  <img src="assets/saveforlater.png" width="15" />

         ```swift
         // Send saveForLater commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "saveForLaters", product: product)
         ```

      1. Para  <img src="assets/addtocart.png" width="20" />

         ```swift
         // Send productListAdds commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productListAdds", product: product)
         ```

      1. Para  <img src="assets/purchase.png" width="20" />

         ```swift
         // Send purchase commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
         ```

>[!TIP]
>
>Caso esteja desenvolvendo para Android™, use o Map (`java.util.Map`) como a interface fundamental para criar sua carga XDM.


### Grupos de campos personalizados

Imagine que você queira rastrear visualizações de tela e interações no próprio aplicativo. Lembre-se de que você definiu um grupo de campos personalizado para esse tipo de evento.

* No esquema, identifique os eventos que você está tentando coletar.
  ![esquema de interação do aplicativo](assets/datacollection-appInteraction-schema.png)

* Comece a construir seu objeto.

  >[!NOTE]
  >
  * Os grupos de campos padrão sempre começam na raiz do objeto.
  >
  * Os grupos de campos personalizados sempre começam em um objeto exclusivo da sua organização Experience Cloud, `_techmarketingdemos` neste exemplo.

  Para o evento de interação do aplicativo, você construiria um objeto como:

  ```swift
  let xdmData: [String: Any] = [
    "eventType": "application.interaction",
    "_techmarketingdemos": [
      "appInformation": [
          "appInteraction": [
              "name": "login",
              "appAction": [
                  "value": 1
                  ]
              ]
          ]
      ]
  ]
  ```

  Para o evento de rastreamento de tela, você construiria um objeto como:

  ```swift
  var xdmData: [String: Any] = [
    "eventType": "application.scene",
    "_techmarketingdemos": [
        "appInformation": [
            "appStateDetails": [
                "screenType": "App",
                    "screenName": "luma: content: ios: us: en: login",
                    "screenView": [
                        "value": 1
                    ]
                ]
            ] 
        ]
  ]
  ```


* Agora você pode usar essa estrutura de dados para criar um `ExperienceEvent`.

  ```swift
  let event = ExperienceEvent(xdm: xdmData)
  ```

* Envie o evento e os dados para a Rede de borda da Platform.

  ```swift
  Edge.sendEvent(experienceEvent: event)
  ```


Novamente, vamos implementar esse código no seu projeto Xcode.

1. Para maior comodidade, você define duas funções no **[!UICONTROL MobileSDK]**. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** no navegador do Projeto Xcode.

   1. Um para interações do aplicativo. Adicione esse código à `func sendAppInteractionEvent(actionName: String)` função:

      ```swift
      // Set up a data dictionary, create an experience event and send the event.
      let xdmData: [String: Any] = [
          "eventType": "application.interaction",
          tenant : [
              "appInformation": [
                  "appInteraction": [
                      "name": actionName,
                      "appAction": [
                          "value": 1
                      ]
                  ]
              ]
          ]
      ]
      let appInteractionEvent = ExperienceEvent(xdm: xdmData)
      Edge.sendEvent(experienceEvent: appInteractionEvent)
      ```

      Essa função usa o nome da ação como um parâmetro e

      * define a carga XDM como um dicionário, usando o parâmetro da função,
      * configura um evento de experiência usando o dicionário,
      * envia o evento de experiência usando o [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API.


   1. E uma para monitoramento de tela. Adicione esse código à `func sendTrackScreenEvent(stateName: String) ` função:

      ```swift
      // Set up a data dictionary, create an experience event and send the event.
      let xdmData: [String: Any] = [
          "eventType": "application.scene",
          tenant : [
              "appInformation": [
                  "appStateDetails": [
                      "screenType": "App",
                      "screenName": stateName,
                      "screenView": [
                          "value": 1
                      ]
                  ]
              ]
          ]
      ]
      let trackScreenEvent = ExperienceEvent(xdm: xdmData)
      Edge.sendEvent(experienceEvent: trackScreenEvent)
      ```

      Esta função usa o nome do estado como um parâmetro e

      * define a carga XDM como um dicionário, usando o parâmetro da função,
      * configura um evento de experiência usando o dicionário,
      * envia o evento de experiência usando o [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API.

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL LoginSheet]**.

   1. Adicione o seguinte código destacado ao fechamento do botão Logon:

      ```swift
      // Send app interaction event
      MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
      ```

   1. Adicione o código destacado a seguir a `onAppear` modificador:

      ```swift
      // Send track screen event
      MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: login")
      ```

## Validação

1. Revise o [instruções de configuração](assurance.md#connecting-to-a-session) seção para conectar seu simulador ou dispositivo com o Assurance.

   1. Mova o ícone do Assurance para a esquerda.
   1. Selecionar **[!UICONTROL Início]** na barra de guias e verifique se há uma **[!UICONTROL ECID]**, **[!UICONTROL E-mail]**, e **[!UICONTROL ID do CRM]** na tela inicial.
   1. Selecionar **[!DNL Products]** na barra de guias.
   1. Selecione um produto.
   1. Selecionar <img src="assets/saveforlater.png" width="15" />.
   1. Selecionar <img src="assets/addtocart.png" width="20" />.
   1. Selecionar <img src="assets/purchase.png" width="15" />.

      <img src="./assets/mobile-app-events-3.png" width="300">


1. Na interface do usuário do Assurance, procure pela variável **[!UICONTROL hitReceived]** eventos do **[!UICONTROL com.adobe.edge.konductor]** fornecedor.
1. Selecione o evento e revise os dados XDM na **[!UICONTROL messages]** objeto. Como alternativa, você pode usar ![Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) **[!UICONTROL Copiar evento bruto]** e use um editor de texto ou código de sua preferência para colar e inspecionar o evento.

   ![validação da coleção de dados](assets/datacollection-validation.png)


## Próximas etapas

Agora você deve ter todas as ferramentas para começar a adicionar a coleção de dados ao seu aplicativo. Você pode adicionar mais inteligência à forma como o usuário interage com seus produtos no aplicativo e adicionar mais interação com o aplicativo e chamadas de rastreamento de tela para o aplicativo:

* Implemente a ordem, o check-out, a cesta vazia e outras funcionalidades no aplicativo e adicione eventos de experiência de comércio relevantes a essa funcionalidade.
* Repita a chamada para `sendAppInteractionEvent` com o parâmetro apropriado para rastrear outras interações do aplicativo pelo usuário.
* Repita a chamada para `sendTrackScreenEvent` com o parâmetro apropriado para rastrear telas visualizadas pelo usuário no aplicativo.

>[!TIP]
>
Revise o [aplicativo concluído](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) para obter mais exemplos.


## Enviar eventos para o Analytics e a Platform

Agora que você coletou os eventos e os enviou para a Platform Edge Network, eles serão enviados para os aplicativos e serviços configurados em seu [sequência de dados](create-datastream.md). Em lições posteriores, mapeie esses dados para [Adobe Analytics](analytics.md), [Adobe Experience Platform](platform.md)e outras soluções da Adobe Experience Cloud, como [Adobe Target](target.md) e Adobe Journey Optimizer.

>[!SUCCESS]
>
Agora você configurou o aplicativo para rastrear eventos de comércio, interação com o aplicativo e rastreamento de tela para a Rede de borda da Adobe Experience Platform e todos os serviços definidos no fluxo de dados.
>
Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Próximo: **[Manipular WebViews](web-views.md)**
