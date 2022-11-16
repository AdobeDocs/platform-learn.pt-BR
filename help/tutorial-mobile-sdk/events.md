---
title: Eventos
description: Saiba como coletar dados do evento em um aplicativo móvel.
exl-id: 4779cf80-c143-437b-8819-1ebc11a26852
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 1%

---

# Eventos

Saiba como rastrear eventos em um aplicativo móvel.

A extensão Edge Network fornece uma API para enviar Eventos de experiência para a Platform Edge Network. Um Evento de experiência é um objeto que contém dados que estão em conformidade com a definição do esquema XDM ExperienceEvent. Mais simplesmente, eles capturam o que as pessoas fazem no aplicativo móvel. Depois que os dados são recebidos pela Rede de borda da plataforma, eles podem ser encaminhados para aplicativos e serviços configurados em seu armazenamento de dados, como Adobe Analytics e Experience Platform. Saiba mais sobre o [Eventos de experiência](https://aep-sdks.gitbook.io/docs/getting-started/initialize-the-sdk) na documentação do produto.

## Pré-requisitos

* PodFile atualizado com os SDKs necessários.
* Extensões registradas no AppDelegate.
* Configurado o MobileCore para usar o AppId de desenvolvimento.
* SDKs importados.
* Aplicativo criado e executado com êxito com as alterações acima.

## Objetivos de aprendizagem

Nesta lição, você:

* Entenda como estruturar dados XDM com base em um esquema.
* Envie um evento XDM com base em um grupo de campos padrão.
* Envie um evento XDM com base em um grupo de campos personalizado.
* Envie um evento de compra XDM.
* Validar com Controle de Controle.

## Criar um evento de experiência

A extensão Adobe Experience Platform Edge pode enviar eventos que seguem um esquema XDM definido anteriormente para a Rede de borda da Adobe Experience Platform.

O processo é assim...

1. Identifique a interação do aplicativo móvel que você está tentando rastrear.

1. Revise o esquema e identifique o evento apropriado.

1. Revise seu esquema e identifique quaisquer campos adicionais que devem ser usados para descrever o evento.

1. Construa e preencha o objeto de dados.

1. Criar e enviar evento.

1. Validar.

Vejamos alguns exemplos.

### Exemplo #1 - grupos de campos padrão

Analise o exemplo a seguir sem tentar implementá-lo no aplicativo de amostra:

1. No esquema , identifique o evento que você está tentando coletar; neste exemplo, estamos rastreando uma visualização de produto.
   ![esquema de exibição de produto](assets/mobile-datacollection-prodView-schema.png)

1. Comece a construir seu objeto:

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

   * eventType: Descreve o evento que ocorreu, use um [valor conhecido](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) sempre que possível.
   * commerce.productViews.value: Forneça o valor numérico do evento. Se for um booleano (ou &quot;Contador&quot; no Adobe Analytics), o valor sempre será 1. Se for um evento numérico ou de moeda, o valor pode ser > 1.

1. No esquema , identifique quaisquer dados adicionais associados ao evento. Neste exemplo, inclua `productListItems` que é um conjunto padrão de campos usados com eventos relacionados ao comércio:
   ![esquema de itens da lista de produtos](assets/mobile-datacollection-prodListItems-schema.png)
   * Observe que `productListItems` é um array para que vários produtos possam ser fornecidos.

1. Expanda o objeto xdmData para incluir dados suplementares:

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

1. Use a estrutura de dados para criar uma `ExperienceEvent`:

   ```swift
   let productViewEvent = ExperienceEvent(xdm: xdmData)
   ```

1. Envie o evento e os dados para a Rede de borda da plataforma:

   ```swift
   Edge.sendEvent(experienceEvent: productViewEvent)
   ```

### Exemplo 2 - grupos de campos personalizados

Analise o exemplo a seguir sem tentar implementá-lo no aplicativo de amostra:

1. No esquema , identifique o evento que está tentando coletar. Neste exemplo, rastreie uma &quot;Interação do aplicativo&quot; que consiste em um evento e nome da Ação do aplicativo.
   ![schema de interação do aplicativo](assets/mobile-datacollection-appInteraction-schema.png)

1. Comece a construir o objeto.

   >[!NOTE]
   >
   >  Os grupos de campos padrão sempre começam na raiz do objeto.
   >
   >  Os grupos de campos personalizados sempre começam em um objeto exclusivo de sua organização de Experience Cloud, &quot;_techmarketingdemonstrações&quot; neste exemplo.

   ```swift
   var xdmData: [String: Any] = [
   "_techmarketingdemos": [
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
   ```

   Ou, em alternativa..

   ```swift
   var xdmData: [String: Any] = [:]
   xdmData["_techmarketingdemos"] = [
       "appInformation": [
           "appInteraction": [
               "name": actionName,
               "appAction": [
                   "value": 1
               ]
           ]
       ]
   ]
   ```

1. Use a estrutura de dados para criar uma `ExperienceEvent`.

   ```swift
   let appInteractionEvent = ExperienceEvent(xdm: xdmData)
   ```

1. Envie o evento e os dados para a Rede de borda da plataforma.

   ```swift
   Edge.sendEvent(experienceEvent: appInteractionEvent)
   ```

### Adicionar rastreamento de visualização de tela ao aplicativo Luma

Espera-se que os exemplos acima tenham explicado o processo de pensamento ao construir um objeto de dados XDM. Em seguida, adicionaremos o rastreamento de visualização de tela no aplicativo Luma.

1. Navegue até `Home.swift`.
1. Adicione o código a seguir a `viewDidAppear(...)`.

   ```swift
           let stateName = "luma: content: ios: us: en: home"
           var xdmData: [String: Any] = [:]
           //Page View
           xdmData["_techmarketingdemos"] = [
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
           let experienceEvent = ExperienceEvent(xdm: xdmData)
           Edge.sendEvent(experienceEvent: experienceEvent)
   ```

1. Repita o procedimento para cada tela no aplicativo, atualizando `stateName` como vai.



### Validação

1. Revise o [instruções de configuração](assurance.md) e conecte seu simulador ou dispositivo ao Controle.
1. Execute a ação e procure a variável `hitReceived` do `com.adobe.edge.konductor` fornecedor.
1. Selecione o evento e revise os dados XDM na `messages` objeto.
   ![validação da coleção de dados](assets/mobile-datacollection-validation.png)

### Exemplo #3 - compra

Neste exemplo, suponha que o usuário tenha feito a seguinte compra com êxito:

* Produto nº 1 - Yoga Mat.
   * US$ 49,99 x1
   * SKU: 5829
* Produto nº 2 - Garrafa d&#39;água.
   * US$ 10,00 x3
   * SKU: 9841
* Total do pedido: 79,99 $
* Id De Pedido Exclusivo: 298234720
* Tipo de pagamento: Cartão de crédito Visa
* Id Da Transação De Pagamento Exclusivo: 847361

#### Esquema

Estes são os campos de esquema relacionados a serem usados:

* eventType: &quot;commerce.purch&quot;
* commerce.purchases
* commerce.order
* productsListItems
* _techmarketingdemos.appStateDetails (personalizado)

>[!TIP]
>
>Os grupos de campos personalizados são sempre colocados em seu identificador de organização de Experience Cloud.
>
>&quot;_techmarketingdemos&quot; é substituído pelo valor exclusivo de sua organização.

![schema de compra](assets/mobile-datacollection-purchase-schema.png)


#### Código

Veja como construir e enviar o objeto XDM no aplicativo.

```swift
let stateName = "luma: content: ios: us: en: orderconfirmation"
let currencyCode = "USD"
let orderTotal = "79.99"
let paymentType = "Visa Credit Card"
let orderId = "298234720"
let paymentTransactionId = "847361"
var xdmData: [String: Any] = [
  "eventType": "commerce.purchases",
  "commerce": [
    "purchases": [
      "value": 1
    ],
    "order": [
      "currencyCode": currencyCode,
      "priceTotal": orderTotal,
      "purchaseID": orderId,
      "purchaseOrderNumber": orderId,
      "payments": [ //Assuming only 1 payment type is used
        [
          "currencyCode": currencyCode,
          "paymentAmount": orderTotal,
          "paymentType": paymentType,
          "transactionID": paymentTransactionId
        ]
      ]
    ]
  ],
  "productListItems": [
      [
          "name":  "Yoga Mat",
          "SKU": "5829",
          "priceTotal": "49.99",
          "quantity": 1
      ],
      [
        "name":  "Water Bottle",
        "SKU": "9841",
        "priceTotal": "30.00",
        "quantity": 3
      ]
  ]
]

//Custom field group
xdmData["_techmarketingdemos"] = [
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
let experienceEvent = ExperienceEvent(xdm: xdmData)
Edge.sendEvent(experienceEvent: experienceEvent)
```

>[!NOTE]
>
>Para maior clareza, todos os valores são codificados. Numa situação real, os valores seriam preenchidos dinamicamente.


### Implementar no aplicativo Luma

Você deve ter todas as ferramentas para começar a adicionar a coleta de dados ao aplicativo de amostra Luma. Abaixo está uma lista de requisitos hipotéticos de rastreamento que podem ser seguidos.

* Rastreie cada visualização de tela.
   * Campos de esquema: screenType, screenName, screenView
* Rastreie ações não comerciais.
   * Campos de esquema: appInteraction.name, appAction
* Ações de comércio:
   * Página do produto: productViews
   * Adicionar ao carrinho: productListAdds
   * Remover do carrinho: productListRemoments
   * Iniciar Check-out: check-outs
   * Exibir carrinho: productListViews
   * Adicionar à lista de desejos: saveForLaters
   * Compra: compras, pedido

>[!TIP]
>
>Revise o [aplicativo totalmente implementado](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) para obter mais exemplos.

### Validação

1. Revise o [instruções de configuração](assurance.md) e conecte seu simulador ou dispositivo ao Controle.

1. Execute a ação e procure a variável `hitReceived` do `com.adobe.edge.konductor` fornecedor.

1. Selecione o evento e revise os dados XDM na `messages` objeto.
   ![validação da coleção de dados](assets/mobile-datacollection-validation.png)

## Enviar eventos para o Analytics e a Platform

Depois de coletar os eventos e enviá-los para a Rede de borda da plataforma, eles serão enviados para os aplicativos e serviços configurados no [datastream](create-datastream.md). Em lições posteriores, você mapeará esses dados para [Adobe Analytics](analytics.md) e [Adobe Experience Platform](platform.md).

Próximo: **[WebViews](web-views.md)**

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender sobre o Adobe Experience Platform Mobile SDK. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)