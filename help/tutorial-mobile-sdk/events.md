---
title: Rastrear dados do evento em aplicativos móveis com o Experience Platform Mobile SDK
description: Saiba como rastrear dados do evento em um aplicativo móvel.
jira: KT-14631
exl-id: 4779cf80-c143-437b-8819-1ebc11a26852
source-git-commit: a7768dcb056a57f4b170c393525e404f854be774
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 1%

---

# Rastrear dados do evento

Saiba como rastrear eventos em um aplicativo móvel.

A extensão do Edge Network fornece uma API para enviar eventos de experiência para a Platform Edge Network. Um evento de experiência é um objeto que contém dados em conformidade com a definição do esquema XDM ExperienceEvent. De maneira mais simples, esses eventos capturam o que as pessoas fazem no aplicativo móvel. Depois que a Platform Edge Network recebeu dados, esses dados podem ser encaminhados para aplicativos e serviços configurados no fluxo de dados, como Adobe Analytics e Experience Platform. Saiba mais sobre os [Eventos de experiência](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) na documentação do produto.

## Pré-requisitos

* Todas as dependências de pacote são configuradas no projeto Xcode.
* Extensões registradas em **[!UICONTROL AppDelegate]**.
* Configuração da extensão MobileCore para usar o `appId` de desenvolvimento.
* SDKs importados.
* O aplicativo foi criado e executado com sucesso com as alterações acima.

## Objetivos de aprendizagem

Nesta lição, você

* Entenda como estruturar dados XDM com base em um esquema.
* Enviar um evento XDM com base em um grupo de campos padrão.
* Enviar um evento XDM com base em um grupo de campos personalizado.
* Envie um evento de compra XDM.
* Valide com o Assurance.

## Construção de um evento de experiência

A extensão do Adobe Experience Platform Edge pode enviar eventos que seguem um esquema XDM definido anteriormente para o Adobe Experience Platform Edge Network.

O processo é assim...

1. Identifique a interação do aplicativo móvel que você está tentando rastrear.

1. Revise seu esquema e identifique o evento apropriado.

1. Revise seu esquema e identifique campos adicionais que devem ser usados para descrever o evento.

1. Construir e preencher o objeto de dados.

1. Criar e enviar evento.

1. Validar.


### Grupos de campos padrão

Para os grupos de campos padrão, o processo é semelhante a:

* No esquema, identifique os eventos que você está tentando coletar. Neste exemplo, você está rastreando eventos de experiência de comércio, por exemplo, um evento de exibição de produto (**[!UICONTROL productViews]**).

  ![esquema de exibição de produto](assets/datacollection-prodView-schema.png){zoomable="yes"}

* Para construir um objeto contendo os dados do evento de experiência em seu aplicativo, você usaria um código como:

>[!BEGINTABS]

>[!TAB iOS]

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

Neste código:

* `eventType`: descreve o evento que ocorreu, use um [valor conhecido](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) quando possível.

* `commerce.productViews.value`: o valor numérico ou booleano do evento. Se for um Booleano (ou &quot;Contador&quot; no Adobe Analytics), o valor sempre será definido como 1. Se for um evento numérico ou de moeda, o valor poderá ser > 1.

>[!TAB Android]

```kotlin
val xdmData = mapOf(
    "eventType" to "commerce.productViews",
    "commerce" to mapOf(
        "productViews" to mapOf(
        "value": 1
        )
    )
)
```

Neste código:

* `eventType`: descreve o evento que ocorreu, use um [valor conhecido](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) quando possível.

* `commerce.productViews.value`: o valor numérico ou booleano do evento. Se for um Booleano (ou &quot;Contador&quot; no Adobe Analytics), o valor sempre será definido como 1. Se for um evento numérico ou de moeda, o valor poderá ser > 1.

>[!ENDTABS]


* No esquema, identifique quaisquer dados adicionais associados ao evento de visualização de produto de comércio. Neste exemplo, inclua **[!UICONTROL productListItems]**, que é um conjunto padrão de campos usados com qualquer evento relacionado ao comércio:

  ![esquema de itens de lista de produtos](assets/datacollection-prodListItems-schema.png){zoomable="yes"}
   * Observe que **[!UICONTROL productListItems]** é uma matriz para que vários produtos possam ser fornecidos.

* Para adicionar esses dados, expanda o objeto `xdmData` para incluir dados suplementares:

>[!BEGINTABS]

>[!TAB iOS]

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

>[!TAB Android]

```kotlin
val xdmData = mapOf(
    "eventType" to "commerce.productViews",
    "commerce" to mapOf(
        "productViews" to mapOf(
        "value": 1
        )
    ),
    "productListItems" to mapOf(
        "name": productName,
        "SKU": sku,
        "priceTotal", priceString,
        "quantity", 1
    )
)
```

>[!ENDTABS]

* Agora você pode usar esta estrutura de dados para criar um `ExperienceEvent`:

>[!BEGINTABS]

>[!TAB iOS]

```swift
let productViewEvent = ExperienceEvent(xdm: xdmData)
```

>[!TAB Android]

```kotlin
val productViewEvent = ExperienceEvent.Builder().setXdmSchema(xdmData).build()
```

>[!ENDTABS]

* E envie o evento e os dados para o Platform Edge Network usando a API `sendEvent`:

>[!BEGINTABS]

>[!TAB iOS]

```swift
Edge.sendEvent(experienceEvent: productViewEvent)
```

>[!TAB Android]

```kotlin
Edge.sendEvent(productViewEvent, null)
```

>[!ENDTABS]


A API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) é a do AEP Mobile SDK equivalente às chamadas de API [`MobileCore.trackAction`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction) e [`MobileCore.trackState`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackstate). Consulte [Migrar da extensão móvel do Analytics para o Adobe Experience Platform Edge Network](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/migrate-to-edge-network/) para obter mais informações.

Agora você implementará esse código em seu projeto.
Você tem diferentes ações relacionadas a produtos de comércio em seu aplicativo e deseja enviar eventos, com base nessas ações conforme executadas pelo usuário:

* exibir: ocorre quando um usuário exibe um produto específico,
* adicionar ao carrinho: quando um usuário toca <img src="assets/addtocart.png" width="20"/> em uma tela de detalhes do produto,
* salvar para mais tarde: quando um usuário tocar <img src="assets/saveforlater.png" width="15"/> / <img src="assets/heart.png" width="25"/> em uma tela de detalhes do produto,
* compra: quando um usuário toca <img src="assets/purchase.png" width="20"/> em uma tela de detalhes do produto.

Para implementar o envio de eventos de experiência relacionados ao comércio de maneira reutilizável, use uma função dedicada:

>[!BEGINTABS]

>[!TAB iOS]

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** no navegador do Projeto Xcode e adicione o seguinte à função `func sendCommerceExperienceEvent(commerceEventType: String, product: Product)`.

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
   * envia o evento de experiência usando a API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!UICONTROL ProductView]** no navegador do Projeto Xcode e adicione várias chamadas à função `sendCommerceExperienceEvent`:

   1. No modificador `.task`, dentro do fechamento `ATTrackingManager.trackingAuthorizationStatus`. Esse modificador `.task` é chamado quando a exibição de produto é inicializada e exibida, para que você queira enviar um evento de exibição de produto nesse momento específico.

      ```swift
      // Send productViews commerce experience event
      MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productViews", product: product)
      ```

   1. Para cada um dos botões (<img src="assets/saveforlater.png" width="15"/>, <img src="assets/addtocart.png" width="20"/> e <img src="assets/purchase.png" width="20"/>) na barra de ferramentas, adicione a chamada relevante dentro do fechamento `ATTrackingManager.trackingAuthorizationStatus == .authorized`:

      1. Para <img src="assets/saveforlater.png" width="15"/>

         ```swift
         // Send saveForLater commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "saveForLaters", product: product)
         ```

      1. Para <img src="assets/addtocart.png" width="20"/>

         ```swift
         // Send productListAdds commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productListAdds", product: product)
         ```

      1. Para <img src="assets/purchase.png" width="20"/>

         ```swift
         // Send purchase commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
         ```

>[!TAB Android]

1. Navegue até **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]** no navegador do Android Studio e adicione o seguinte à função `func sendCommerceExperienceEvent(commerceEventType: String, product: Product)`.

   ```kotlin
   // Set up a data map, create an experience event and send the event.
   val xdmData = mapOf(
       "eventType" to "commerce.$commerceEventType",
       "commerce" to mapOf(commerceEventType to mapOf("value" to 1)),
       "productListItems" to listOf(
           mapOf(
               "name" to product.name,
               "priceTotal" to product.price,
               "SKU" to product.sku
           )
       )
   )
   val commerceExperienceEvent = ExperienceEvent.Builder().setXdmSchema(xdmData).build()
   Edge.sendEvent(commerceExperienceEvent, null)
   ```

   Essa função considera o tipo de evento de experiência de comércio e o produto como parâmetros e

   * define a carga XDM como um mapa, usando os parâmetros da função,
   * configura um evento de experiência usando o mapa,
   * envia o evento de experiência usando a API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).

1. Navegue até **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL views]** > **[!UICONTROL ProductView.kt]** no navegador do Android Studio e adicione várias chamadas à função `sendCommerceExperienceEvent`:

   1. Na função de composição `LaunchedEffect(Unit)`, você deseja enviar um evento de exibição de produto no momento específico em que um produto é visualizado.

      ```kotlin
      // Send productViews commerce experience event
      MobileSDK.shared.sendCommerceExperienceEvent("productViews", product)
      ```

   1. Para cada um dos botões (<img src="assets/heart.png" width="25"/>, <img src="assets/addtocart.png" width="20"/> e <img src="assets/purchase.png" width="20"/>) na barra de ferramentas, adicione a chamada relevante dentro de `scope.launch` de `if (MobileSDK.shared.trackingEnabled == TrackingStatus.AUTHORIZED)  statement`:

      1. Para <img src="assets/heart.png" width="25"/>

         ```kotlin
         // Send saveForLater commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent("saveForLaters", product)
         ```

      1. Para <img src="assets/addtocart.png" width="20"/>

         ```kotlin
         // Send productListAdds commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent("productListAdds", product)
         ```

      1. Para <img src="assets/purchase.png" width="20"/>

         ```kotlin
         // Send purchase commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent("purchases", product)
         ```

>[!ENDTABS]

>[!TIP]
>
>Caso esteja desenvolvendo para Android™, use o Mapa (`java.util.Map`) como a interface fundamental para criar sua carga XDM.


### Grupos de campos personalizados

Imagine que você queira rastrear visualizações de tela e interações no próprio aplicativo. Lembre-se de que você definiu um grupo de campos personalizado para esse tipo de evento.

* No esquema, identifique os eventos que você está tentando coletar.
  ![esquema de interação do aplicativo](assets/datacollection-appInteraction-schema.png){zoomable="yes"}

* Comece a construir seu objeto.

  >[!NOTE]
  >
  >* Os grupos de campos padrão sempre começam na raiz do objeto.
  >
  >* Os grupos de campos personalizados sempre começam em um objeto exclusivo da sua organização da Experience Cloud, `_techmarketingdemos` neste exemplo.

* Para o evento de interação do aplicativo, você construiria um objeto como:

>[!BEGINTABS]

>[!TAB iOS]

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

>[!TAB Android]

```kotlin
val xdmData = mapOf(
    "eventType" to "application.interaction",
    "_techmarketingdemos" to mapOf(
        "appInformation" to mapOf(
            "appInteraction" to mapOf(
                "name" to "login",
                "appAction" to mapOf("value" to 1)
            )
        )
    )
)
```

>[!ENDTABS]

* Para o evento de rastreamento de tela, você construiria um objeto como:

>[!BEGINTABS]

>[!TAB iOS]

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

>[!TAB Android]

```kotlin
val xdmData = mapOf(
    "eventType" to "application.scene",
    tenant.value to mapOf(
        "appInformation" to mapOf(
            "appStateDetails" to mapOf(
                "screenType" to "App",
                "screenName" to stateName,
                "screenView" to mapOf("value" to 1)
            )
        )
    )
)
```

>[!ENDTABS]



* Agora você pode usar esta estrutura de dados para criar um `ExperienceEvent`.

>[!BEGINTABS]

>[!TAB iOS]

```swift
let event = ExperienceEvent(xdm: xdmData)
```

>[!TAB Android]

```kotlin
val event = ExperienceEvent(xdmData)
```

>[!ENDTABS]


* Envie o evento e os dados para a Platform Edge Network.

>[!BEGINTABS]

>[!TAB iOS]

```swift
Edge.sendEvent(experienceEvent: event)
```

>[!TAB Android]

```kotlin
Edge.sendEvent(event, null)
```

>[!ENDTABS]

Novamente, implemente esse código em seu projeto.

>[!BEGINTABS]

>[!TAB iOS]

1. Para maior comodidade, você define duas funções no **[!UICONTROL MobileSDK]**. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** no navegador do Projeto Xcode.

   * Um para interações do aplicativo. Adicionar este código à função `func sendAppInteractionEvent(actionName: String)`:

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
      * envia o evento de experiência usando a API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).


   * E uma para monitoramento de tela. Adicionar este código à função `func sendTrackScreenEvent(stateName: String) `:

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
      * envia o evento de experiência usando a API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL LoginSheet]**.

   1. Adicione o seguinte código destacado ao fechamento do botão Logon:

      ```swift
      // Send app interaction event
      MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
      ```

   1. Adicionar o seguinte código realçado ao modificador `onAppear`:

      ```swift
      // Send track screen event
      MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: login")
      ```

>[!TAB Android]

1. Para maior comodidade, você define duas funções no **[!UICONTROL MobileSDK]**. Navegue até **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL templates]** > **[!UICONTROL MobileSDK]** no seu navegador Android Studio.

   * Um para interações do aplicativo. Adicionar este código à função `fun sendAppInteractionEvent(actionName: String)`:

     ```kotlin
     // Set up a data map, create an experience event and send the event.
     val xdmData = mapOf(
         "eventType" to "application.interaction",
         tenant.value to mapOf(
             "appInformation" to mapOf(
                 "appInteraction" to mapOf(
                     "name" to actionName,
                     "appAction" to mapOf("value" to 1)
                 )
             )
         )
     )
     val appInteractionEvent = ExperienceEvent.Builder().setXdmSchema(xdmData).build()
     Edge.sendEvent(appInteractionEvent, null)
     ```

     Essa função usa o nome da ação como um parâmetro e

      * define a carga XDM como um mapa, usando o parâmetro da função,
      * configura um evento de experiência usando o mapa,
      * envia o evento de experiência usando a API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).


   * E uma para monitoramento de tela. Adicionar este código à função `fun sendTrackScreenEvent(stateName: String)`:

     ```kotlin
     // Set up a data map, create an experience event and send the event.
     val xdmData = mapOf(
         "eventType" to "application.scene",
         tenant.value to mapOf(
             "appInformation" to mapOf(
                 "appStateDetails" to mapOf(
                     "screenType" to "App",
                     "screenName" to stateName,
                     "screenView" to mapOf("value" to 1)
                 )
             )
         )
     )
     val trackScreenEvent = ExperienceEvent.Builder().setXdmSchema(xdmData).build()
     Edge.sendEvent(trackScreenEvent, null)
     ```

     Esta função usa o nome do estado como um parâmetro e

      * define a carga XDM como um mapa, usando o parâmetro da função,
      * configura um evento de experiência usando o mapa,
      * envia o evento de experiência usando a API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).

1. Navegue até **[!UICONTROL Android]** ![ChevronDown ](/help/assets/icons/ChevronDown.svg)**[!DNL app]**>**[!DNL kotlin+java]**>**[!DNL com.adobe.luma.tutorial.android]**>**[!UICONTROL  visualizações ]**>**[!UICONTROL  LoginSheet.kt ]**

   1. Adicione o seguinte código realçado ao evento **[!UICONTROL Button]** **[!UICONTROL onClick]**:

      ```kotlin
      // Send app interaction event
      MobileSDK.shared.sendAppInteractionEvent("login")
      ```

   1. Adicione o seguinte código realçado à função combinável `LaunchedEffect(Unit)`:

      ```kotlin
      // Send track screen event
      MobileSDK.shared.sendTrackScreenEvent("luma: content: android: us: en: login")
      ```

>[!ENDTABS]



## Validação

1. Revise a seção [instruções de instalação](assurance.md#connecting-to-a-session) para conectar seu simulador ou dispositivo ao Assurance.

   1. Mova o ícone do Assurance para a esquerda.
   1. Selecione **[!UICONTROL Página inicial]** na barra de guias e verifique se você vê um **[!UICONTROL ECID]**, **[!UICONTROL Email]** e **[!UICONTROL CRM ID]** na tela inicial.
   1. Selecione **[!DNL Products]** na barra de guias.
   1. Selecione um produto.
   1. Selecionar <img src="assets/saveforlater.png" width="15"/> (iOS) ou <img src="assets/heart.png" width="25"/> (Android).
   1. Selecionar <img src="assets/addtocart.png" width="20"/>.
   1. Selecionar <img src="assets/purchase.png" width="15"/>.

>[!BEGINTABS]

>[!TAB iOS]

<img src="./assets/mobile-app-events-3.png" width="300">

>[!TAB Android]

<img src="./assets/mobile-app-events-3-android.png" width="278">

>[!ENDTABS]

1. Na interface do Assurance, procure os eventos **[!UICONTROL hitReceived]** do fornecedor **[!UICONTROL com.adobe.edge.konductor]**.
1. Selecione o evento e revise os dados XDM no objeto **[!UICONTROL messages]**. Como alternativa, você pode usar o ![Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) **[!UICONTROL Copiar Evento Bruto]** e usar um editor de texto ou código de sua preferência para colar e inspecionar o evento.

   ![validação da coleção de dados](assets/datacollection-validation.png){zoomable="yes"}


## Próximas etapas

Agora você deve ter todas as ferramentas para começar a adicionar a coleção de dados ao seu aplicativo. Você pode adicionar mais inteligência à forma como o usuário interage com seus produtos no aplicativo e adicionar mais interação com o aplicativo e chamadas de rastreamento de tela para o aplicativo:

* Implemente a ordem, o check-out, a cesta vazia e outras funcionalidades no aplicativo e adicione eventos de experiência de comércio relevantes a essa funcionalidade.
* Repita a chamada para `sendAppInteractionEvent` com o parâmetro apropriado para rastrear outras interações do aplicativo pelo usuário.
* Repita a chamada para `sendTrackScreenEvent` com o parâmetro apropriado para rastrear telas visualizadas pelo usuário no aplicativo.

>[!TIP]
>
>Consulte o [aplicativo concluído](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) para obter mais exemplos.


## Enviar eventos para o Analytics e a Platform

Agora que você coletou os eventos e os enviou para a Platform Edge Network, eles serão enviados para os aplicativos e serviços configurados em sua [sequência de dados](create-datastream.md). Em lições posteriores, você mapeia estes dados para o [Adobe Analytics](analytics.md), o [Adobe Experience Platform](platform.md) e outras soluções da Adobe Experience Cloud (como o [Adobe Target](target.md) e o Adobe Journey Optimizer).

>[!SUCCESS]
>
>Agora você configurou o aplicativo para rastrear eventos de comércio, interação com o aplicativo e rastreamento de tela na Adobe Experience Platform Edge Network. E a todos os serviços definidos no fluxo de dados.
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-os nesta [postagem de discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Próximo: **[Manipular WebViews](web-views.md)**
