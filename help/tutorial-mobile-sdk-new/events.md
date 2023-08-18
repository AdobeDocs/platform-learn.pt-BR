---
title: Eventos
description: Saiba como coletar dados do evento em um aplicativo móvel.
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 0%

---

# Eventos

Saiba como rastrear eventos em um aplicativo móvel.

A extensão Edge Network fornece uma API para enviar eventos de experiência para a Platform Edge Network. Um Evento de experiência é um objeto que contém dados em conformidade com a definição do esquema XDM ExperienceEvent. De maneira mais simples, eles capturam o que as pessoas fazem no seu aplicativo móvel. Depois que os dados forem recebidos pela Platform Edge Network, poderão ser encaminhados para aplicativos e serviços configurados no fluxo de dados, como Adobe Analytics e Experience Platform. Saiba mais sobre o [Eventos de experiência](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) na documentação do produto.

## Pré-requisitos

* Todas as dependências de pacote em vigor no projeto Xcode.
* Extensões registradas no AppDelegate.
* MobileCore configurado para usar appId de desenvolvimento.
* SDKs importados.
* O aplicativo foi criado e executado com sucesso com as alterações acima.

## Objetivos de aprendizagem

Nesta lição, você vai:

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

  ```swift {highlight="2-8"}
  var xdmData: [String: Any] = [
      "eventType": "commerce.productViews",
      "commerce": [
          "productViews": [
            "id": sku,
            "value": 1
          ]
      ]
  ]
  ```

   * `eventType`: descreve o evento que ocorreu, use um [valor conhecido](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) quando possível.
   * `commerce.productViews.id`: um valor de string que representa o SKU do produto
   * `commerce.productViews.value`: forneça o valor numérico do evento. Se for um Booleano (ou &quot;Contador&quot; no Adobe Analytics), o valor sempre será definido como 1. Se for um evento numérico ou de moeda, o valor poderá ser > 1.

* No esquema, identifique quaisquer dados adicionais associados ao evento de visualização de produto de comércio. Neste exemplo, inclua `productListItems` que é um conjunto padrão de campos usados com qualquer evento relacionado ao comércio:

  ![esquema de itens da lista de produtos](assets/datacollection-prodListItems-schema.png)
   * Observe que `productListItems` O é um array para que vários produtos possam ser fornecidos.

* Para adicionar esses dados, expanda suas `xdmData` objeto para incluir dados suplementares:

```swift {highlight="9-16"}
var xdmData: [String: Any] = [
    "eventType": "commerce.productViews",
        "commerce": [
        "productViews": [
            "id": sku,
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

* Em seguida, use a estrutura de dados para criar uma `ExperienceEvent`:

  ```swift
  let productViewEvent = ExperienceEvent(xdm: xdmData)
  ```

* E envie o evento e os dados para a Rede de borda da Platform usando a API sendEvent:

  ```swift
  Edge.sendEvent(experienceEvent: productViewEvent)
  ```

Então agora, vamos implementar esse código no seu projeto Xcode.
Você tem ações relacionadas a produtos de comércio diferentes (exibir, adicionar ao carrinho, salvar para mais tarde, comprar) em seu aplicativo e deseja enviar eventos com base nessas ações, conforme executadas pelo usuário.

1. Para estruturar o envio de eventos de experiência, vá para `MobileSDK`e adicione o seguinte à `sendCommerceExperienceEvent` função. Essa função considera o evento de experiência de comércio e o produto como parâmetros:

   ```swift {highlight="2-22"}
   func sendCommerceExperienceEvent(commerceEventType: String, product: Product) {
     let xdmData: [String: Any] = [
         "eventType": "commerce." + commerceEventType,
         "commerce": [
             commerceEventType: [
                 "id": product.sku,
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
   
     Logger.viewCycle.info("About to send commerce experience event of type  \(commerceEventType)..."
     let commerceExperienceEvent = ExperienceEvent(xdm: xdmData)
     Edge.sendEvent(experienceEvent: commerceExperienceEvent)
   }
   ```

1. Entrada `ProductView` adicionar várias chamadas à variável `sendCommerceExperienceEvent` função:

   1. No `.task` modificador na variável `ATTrackingManager.trackingAuthorizationStatus` encerramento. A variável `.task` o modificador é chamado quando a exibição de produto é inicializada e exibida, para que você queira enviar um evento de exibição de produto naquele momento específico.

      ```swift {highlight="4-5"}
      .task {
          if ATTrackingManager.trackingAuthorizationStatus == .authorized {
               // Send commerce experience event
              MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productView", product: product)
          }
      }
      ```

   1. Para cada um dos botões (Saved for later, Add to cart e Purchase) na barra de ferramentas, disponível em Product View, adicione a chamada relevante.

      * Em Salvar para mais tarde / Adicionar à lista de desejos:

        ```swift {highlight="5-6"}
        Button {
            Task {
                if ATTrackingManager.trackingAuthorizationStatus == .authorized {
                // Send saveForLater commerce experience event
                    MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "saveForLaters", product: product)
                }
            }
            showSaveForLaterDialog.toggle()
        } label: {
            Label("", systemImage: "heart")
        }
        .alert(isPresented: $showSaveForLaterDialog, content: {
            Alert(title: Text( "Saved for later"), message: Text("The selected item is saved to your wishlist…"))
        })
        ```

      * Para Adicionar ao carrinho:

        ```swift {highlight="5-6"}
        Button {
            Task {
                if ATTrackingManager.trackingAuthorizationStatus == .authorized {
                    // Send productListAdds commerce experience event
                    MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productListAdds", product: product)
                }
            }
            showAddToCartDialog.toggle()
        } label: {
                Label("", systemImage: "cart.badge.plus")
        }
        alert(isPresented: $showAddToCartDialog, content: {
            Alert(title: Text( "Added to basket"), message: Text("The selected item is added to your basket…"))
        })
        ```

      * Para Compra:

        ```swift {highlight="5-6"}
        Button {
            Task {
                if ATTrackingManager.trackingAuthorizationStatus == .authorized {
                    // Send purchase commerce experience event
                    MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
                }
            }
            showPurchaseDialog.toggle()
        } label: {
            Label("", systemImage: "creditcard")
        }
        .alert(isPresented: $showPurchaseDialog, content: {
            Alert(title: Text( "Purchases"), message: Text("The selected item is purchased…"))
        })
        ```

### Grupos de campos personalizados

Imagine que você queira rastrear visualizações de tela e interações no próprio aplicativo. Lembre-se de que você definiu um grupo de campos personalizado para esse tipo de evento.

* No esquema, identifique os eventos que você está tentando coletar.
  ![esquema de interação do aplicativo](assets/datacollection-appInteraction-schema.png)

* Comece a construir seu objeto.

  >[!NOTE]
  >
  >  Os grupos de campos padrão sempre começam na raiz do objeto.
  >
  >  Os grupos de campos personalizados sempre começam em um objeto exclusivo da sua organização Experience Cloud, `_techmarketingdemos` neste exemplo.

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


* Em seguida, a estrutura de dados para criar um `ExperienceEvent`.

  ```swift
  let event = ExperienceEvent(xdm: xdmData)
  ```

* Envie o evento e os dados para a Rede de borda da Platform.

  ```swift
  Edge.sendEvent(experienceEvent: event)
  ```


Novamente, vamos implementar esse código no seu projeto Xcode.

1. Para maior comodidade, você define duas funções no `MobileSDK`.

   Um para interações do aplicativo. Adicione o código destacado à `sendAppInteractionEvent(actionName)` função em **[!UICONTROL MobileSDK]**:

   ```swift {highlight="2-16"}
   func sendAppInteractionEvent(actionName: String) {
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
   }
   ```

   E uma para monitoramento de tela. Adicione o código realçado a `sendTrackScreenEvent(stateName)` função em **[!UICONTROL MobileSDK]**:

   ```swift {highlight="2-17"}
   func sendTrackScreenEvent(stateName: String) {
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
   }
   ```

1. Navegue até **[!UICONTROL LoginSheet]**.

   * Adicione o seguinte código destacado ao fechamento do botão Logon:

     ```swift {highlight="3"}
     Button("Login") {                               
        // Send app interaction event
        MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
        dismiss()
     }
     .disabled(currentEmailId.isValidEmail == false)
     .buttonStyle(.bordered)
     ```

   * Adicione o código destacado a seguir a `onAppear` modificador:

     ```swift {highlight="13"}
     .onAppear {
        Task {
            if currentEmailId == "testUser@gmail.com" || currentEmailId.isValidEmail == false {
                // still allow to log in
                disableLogin = false
            }
            else {
                disableLogin = true
            }
        }
        // Send track screen event
        MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: login")
     }
     ```

### Validação

1. Revise o [instruções de configuração](assurance.md) e conecte seu simulador ou dispositivo ao Assurance.
1. Execute o aplicativo para fazer logon e interagir com um produto.

   1. Mova o ícone do Assurance para a esquerda.
   1. Selecionar **[!UICONTROL Início]** na barra de guias.
   1. Selecione o **[!UICONTROL Logon]** botão para abrir a folha Logon.
   1. Selecione o **[!UICONTROL A|]** botão para inserir um email e uma id do cliente aleatórios.
   1. Selecionar **[!UICONTROL Logon]**.
   1. Selecionar **[!UICONTROL Produtos]** na barra de guias.
   1. Selecione um produto.
   1. Selecionar **[!UICONTROL Salvar para mais tarde]**.
   1. Selecionar **[!UICONTROL Adicionar ao carrinho]**.
   1. Selecionar **[!UICONTROL Comprar]**.

      <img src="./assets/mobile-app-events-1.png" width="200"> <img src="./assets/mobile-app-events-2.png" width="200"> <img src="./assets/mobile-app-events-3.png" width="200">


1. Procure o **[!UICONTROL hitReceived]** eventos do **[!UICONTROL com.adobe.edge.konductor]** fornecedor.
1. Selecione o evento e revise os dados XDM na **[!UICONTROL messages]** objeto.
   ![validação da coleção de dados](assets/datacollection-validation.png)


### Implementar no aplicativo Luma

Agora você deve ter todas as ferramentas para começar a adicionar a coleção de dados ao aplicativo Luma. Você pode adicionar mais inteligência à forma como o usuário interage com seus produtos e adicionar mais interação no aplicativo e chamadas de rastreamento de tela ao aplicativo:

* Implemente a ordem, o check-out, a cesta vazia e outras funcionalidades no aplicativo e adicione o evento de experiência comercial relevante a essa funcionalidade.
* Repita a chamada para `sendAppInteractionEvent` com o parâmetro apropriado para rastrear outras interações do usuário no aplicativo.
* Repita a chamada para `sendTrackScreenEvent` com o parâmetro apropriado para rastrear cada tela visualizada pelo usuário no aplicativo.

>[!TIP]
>
>Revise o [aplicativo totalmente implementado](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) para obter mais exemplos.


## Enviar eventos para o Analytics e a Platform

Agora que você coletou os eventos e os enviou para a Platform Edge Network, eles serão enviados para os aplicativos e serviços configurados em seu [sequência de dados](create-datastream.md). Em lições posteriores, mapeie esses dados para [Adobe Analytics](analytics.md) e [Adobe Experience Platform](platform.md).

>[!SUCCESS]
>
>Agora você configurou o aplicativo para rastrear eventos de comércio, interação com o aplicativo e rastreamento de tela para a Rede de borda da Adobe Experience Platform e todos os serviços definidos no fluxo de dados.<br/>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Próximo: **[WebViews](web-views.md)**
