---
title: Mapear dados coletados com o SDK móvel da Platform para o Adobe Analytics
description: Saiba como coletar e mapear dados para o Adobe Analytics em um aplicativo móvel.
solution: Data Collection,Experience Platform,Analytics
jira: KT-14636
exl-id: 406dc687-643f-4f7b-a8e7-9aad1d0d481d
source-git-commit: 30dd0142f1f5220f30c45d58665b710a06c827a8
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 1%

---

# Coletar e mapear dados do Analytics

Saiba como mapear dados móveis para o Adobe Analytics.

Os dados de [evento](events.md) que você coletou e enviou para o Platform Edge Network em lições anteriores são encaminhados para os serviços configurados na sua sequência de dados, incluindo o Adobe Analytics. Mapeie os dados para as variáveis corretas em seu conjunto de relatórios.

![Arquitetura](assets/architecture-aa.png)

## Pré-requisitos

* Noções básicas sobre o rastreamento de ExperienceEvent.
* Dados XDM enviados com sucesso no aplicativo de amostra.
* Um conjunto de relatórios do Adobe Analytics que você pode usar nesta lição.

## Objetivos de aprendizagem

Nesta lição, você vai:

* Configure seu fluxo de dados com o serviço Adobe Analytics.
* Entenda o mapeamento automático de variáveis do Analytics.
* Configurar regras de processamento para mapear dados XDM para variáveis do Analytics.

## Adicionar serviço de sequência de dados do Adobe Analytics

Para enviar seus dados XDM do Edge Network para o Adobe Analytics, configure o serviço Adobe Analytics para a sequência de dados configurada como parte de [Criar uma sequência de dados](create-datastream.md).

1. Na interface da Coleção de dados, selecione **[!UICONTROL Sequências de dados]** e a sequência de dados.

1. Em seguida, selecione ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Adicionar Serviço]**.

1. Adicionar **[!UICONTROL Adobe Analytics]** da lista [!UICONTROL Serviço],

1. Digite o nome do conjunto de relatórios do Adobe Analytics que você deseja usar em **[!UICONTROL ID do Conjunto de Relatórios]**.

1. Habilite o serviço alternando **[!UICONTROL Habilitado]** em.

1. Selecione **[!UICONTROL Salvar]**.

   ![Adicionar o Adobe Analytics como serviço de sequência de dados](assets/datastream-service-aa.png)


## Mapeamento automático

Muitos dos campos XDM padrão são mapeados automaticamente para variáveis do Analytics. Veja a lista completa [aqui](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=en).

### Exemplo #1 - s.products

Um bom exemplo é a [variável de produtos](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en), que não pode ser preenchida com as regras de processamento. Com uma implementação XDM, você passa todos os dados necessários em `productListItems` e `s.products` são automaticamente preenchidos por meio do mapeamento do Analytics.

Este objeto:

```swift
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
```

resulta em:

```
s.products = ";5829;1;49.99,9841;3;30.00"
```

>[!NOTE]
>
>Se `productListItems[].SKU` e `productListItems[].name` contêm dados, o valor em `productListItems[].SKU` é usado. Consulte [Mapeamento de variável do Analytics no Adobe Experience Edge](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=en) para obter mais informações.


### Exemplo #2 - scAdd

Se você observar com atenção, todos os eventos têm dois campos: `value` (obrigatório) e `id` (opcional). O campo `value` é usado para incrementar a contagem de eventos. O campo `id` é usado para serialização.

Este objeto:

```swift
"commerce" : {
  "productListAdds" : {
    "value" : 1
  }
}
```

resulta em:

```
s.events = "scAdd"
```

Este objeto:

```swift
"commerce" : {
  "productListAdds" : {
    "value" : 1,
    "id": "321435"
  }
}
```

resulta em:

```
s.events = "scAdd:321435"
```

## Validar com garantia

Usando a [Garantia](assurance.md), você pode confirmar que está enviando um evento de experiência, os dados XDM estão corretos e o mapeamento do Analytics está acontecendo conforme esperado.

1. Revise a seção [instruções de configuração](assurance.md#connecting-to-a-session) para conectar seu simulador ou dispositivo ao Assurance.

1. Enviar um evento **[!UICONTROL productListAdds]** (adicionar um produto à cesta).

1. Veja a ocorrência do ExperienceEvent.

   ![ocorrência de xdm do analytics](assets/analytics-assurance-experiencevent.png)

1. Revise a parte XDM do JSON.

   ```json
   "xdm" : {
     "productListItems" : [ {
       "SKU" : "LLWS05.1-XS",
       "name" : "Desiree Fitness Tee",
       "priceTotal" : 24
     } ],
   "timestamp" : "2023-08-04T12:53:37.662Z",
   "eventType" : "commerce.productListAdds",
   "commerce" : {
     "productListAdds" : {
       "value" : 1
     }
   }
   // ...
   ```

1. Revise o evento **[!UICONTROL analytics.mapping]**.

   ![ocorrência de xdm do analytics](assets/analytics-assurance-mapping.png)

Observe o seguinte no mapeamento do Analytics:

* **[!UICONTROL eventos]** são preenchidos com `scAdd` com base em `commerce.productListAdds`.
* **[!UICONTROL pl]** (variável products) são preenchidos com um valor concatenado com base em `productListItems`.
* Há outras informações interessantes nesse evento, incluindo todos os dados de contexto.


## Mapeamento com dados de contexto

Os dados XDM encaminhados para o Analytics são convertidos em [dados de contexto](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/proc-rules.html?lang=en), incluindo campos padrão e personalizados.

A chave de dados de contexto é construída seguindo esta sintaxe:

```
a.x.[xdm path]
```

Por exemplo:

```
// Standard Field
a.x.commerce.saveforlaters.value

// Custom Field
a.x._techmarketingdemos.appinformation.appstatedetails.screenname
```

>[!NOTE]
>
>Campos personalizados são colocados sob o identificador Experience Cloud Org.
>
>`_techmarketingdemos` é substituído pelo valor exclusivo de sua organização.



Para mapear esses dados de contexto XDM para seus dados do Analytics em seu conjunto de relatórios, você pode:

### Usar um grupo de campos

* Adicione o grupo de campos **[!UICONTROL Extensão completa do Adobe Analytics ExperienceEvent]** ao esquema.

  ![Grupo de campos Analytics ExperienceEvent FullExtension](assets/schema-analytics-extension.png)

* Crie cargas XDM no aplicativo, de acordo com o grupo de campos Extensão Completa do Adobe Analytics ExperienceEvent, de modo semelhante ao que você fez na lição [Rastrear Dados do Evento](events.md), ou
* Crie regras na propriedade Tags que usam ações de regra para anexar ou modificar dados ao grupo de campos Extensão completa do Adobe Analytics ExperienceEvent. Consulte para obter mais detalhes [Anexar dados a eventos do SDK](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/) ou [Modificar dados em eventos do SDK](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/).


### eVars de merchandising

Se você estiver usando [eVars de merchandising](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/conversion-variables/merchandising-evars.html?lang=en) na configuração do Analytics, por exemplo, para capturar a cor dos produtos, como `&&products = ...;evar1=red;event10=50,...;evar1=blue;event10=60`, é necessário estender a carga XDM definida em [Rastrear dados do evento](events.md) para capturar essas informações de merchandising.

* No JSON:

  ```json
  {
    "productListItems": [
        {
            "SKU": "LLWS05.1-XS",
            "name": "Desiree Fitness Tee",
            "priceTotal": 24,
            "_experience": {
                "analytics": {
                    "events1to100": {
                        "event10": {
                            "value": 50
                        }
                    },
                    "customDimensions": {
                        "eVars": {
                            "eVar1": "red",
                        }
                    }
                }
            }
        }
    ],
    "eventType": "commerce.productListAdds",
    "commerce": {
        "productListAdds": {
            "value": 1
        }
    }
  }
  ```

* No código:

  ```swift
  var xdmData: [String: Any] = [
    "productListItems": [
      [
        "name":  productName,
        "SKU": sku,
        "priceTotal": priceString,
        "_experience" : [
          "analytics": [
            "events1to100": [
              "event10": [
                "value:": value
              ]
            ],
            "customDimensions": [
              "eVars": [
                "eVar1": color
              ]
            ]
          ]
        ]
      ]
    ],
    "eventType": "commerce.productViews",
    "commerce": [
      "productViews": [
        "value": 1
      ]
    ]
  ]
  ```


### Usar regras de processamento

Veja como uma regra de processamento usando esses dados pode ser exibida:

* Você **[!UICONTROL Substitui o valor de]** (1) **[!UICONTROL Nome da Tela do Aplicativo (eVar 2)]** (2) pelo valor de **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (3) se **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (4) **[!UICONTROL estiver definido]** (5).

* Você **[!UICONTROL Definir evento]** (6) **[!UICONTROL Adicionar à Lista de Desejos (Evento 3)]** (7) a **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (8) se **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (9) **[!UICONTROL estiver definido]** (10).

![regras de processamento do analytics](assets/analytics-processing-rules.png)

>[!IMPORTANT]
>
>
>Algumas das variáveis mapeadas automaticamente podem não estar disponíveis para uso nas regras de processamento.
>
>
>Na primeira vez que você mapeia para uma regra de processamento, a interface não mostra as variáveis de dados de contexto do objeto XDM. Para corrigir isso, selecione qualquer valor, Salve e volte para editar. Todas as variáveis XDM agora devem aparecer.


Informações adicionais sobre regras de processamento e dados de contexto podem ser encontradas [aqui](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules.html?lang=en).

>[!TIP]
>
>Ao contrário de implementações anteriores do aplicativo móvel, não há distinção entre exibições de página/tela e outros eventos. Em vez disso, você pode incrementar a métrica **[!UICONTROL Exibição de página]** definindo a dimensão **[!UICONTROL Nome de página]** em uma regra de processamento. Como você está coletando o campo personalizado `screenName` no tutorial, é altamente recomendável mapear o nome da tela como **[!UICONTROL Nome da Página]** em uma regra de processamento.


>[!SUCCESS]
>
>Você configurou o aplicativo para mapear os objetos XDM da Experience Edge para variáveis do Adobe Analytics, habilitando o serviço Adobe Analytics no fluxo de dados e usando regras de processamento, quando aplicável.<br/> Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-os nesta [postagem de Discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com:443/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Próximo: **[Enviar dados para o Experience Platform](platform.md)**
