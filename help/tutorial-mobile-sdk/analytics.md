---
title: Mapeamento do Analytics
description: Saiba como coletar dados do Adobe Analytics em um aplicativo móvel.
exl-id: 406dc687-643f-4f7b-a8e7-9aad1d0d481d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 2%

---

# Mapeamento do Analytics

Saiba como mapear dados móveis para o Adobe Analytics.

O [evento](events.md) os dados coletados e enviados para a Rede de borda da plataforma em lições anteriores são encaminhados para os serviços configurados no conjunto de dados, incluindo o Adobe Analytics. Basta mapear os dados para as variáveis corretas em seu conjunto de relatórios.

## Pré-requisitos

* Noções básicas sobre o rastreamento de ExperienceEvent.
* Enviar dados XDM com êxito no aplicativo de amostra.
* Armazenamento de dados configurado para o Adobe Analytics

## Objetivos de aprendizagem

Nesta lição, você:

* Entenda o mapeamento automático das variáveis do Analytics.
* Configure regras de processamento para mapear dados XDM para variáveis do Analytics.

## Mapeamento automático

Muitos dos campos XDM padrão são mapeados automaticamente para variáveis do Analytics. Veja a lista completa [aqui](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=en).

### Exemplo #1 - s.products

Um bom exemplo é o [variável products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) que não podem ser preenchidas usando as regras de processamento. Com uma implementação XDM, você transmite todos os dados necessários em productListItems e s.products são automaticamente preenchidos por meio do mapeamento do Analytics.

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

Resultaria no seguinte:

```
s.products = ";Yoga Mat;1;49.99,;Water Bottle,3,30.00"
```

>[!NOTE]
>
>Atualmente `productListItems[N].SKU` é ignorada pelo mapeamento automático.

### Exemplo #2 - scAdd

Se você observar atentamente, todos os eventos terão dois campos `value` (obrigatório) e `id` (opcional). O `value` é usado para incrementar a contagem de eventos. O `id` é usado para serialização.

Este objeto:

```swift
"commerce" : {
  "productListAdds" : {
    "value" : 1
  }
}
```

Resultaria no seguinte:

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

Resultaria no seguinte:

```
s.events = "scAdd:321435"
```

## Validar com Controle de Controle

Usar o [Ferramenta de controle de qualidade](assurance.md) é possível confirmar que você está enviando um ExperienceEvent, os dados XDM estão corretos e o mapeamento do Analytics está acontecendo como esperado. Por exemplo:

1. Envie um evento productListAdds .

   ```swift
   var xdmData: [String: Any] = [
     "eventType": "commerce.productListAdds",
     "commerce": [
       "productListAdds": [
         "value": 1
       ]
     ],
     "productListItems": [
       [
         "name": "neve studio dance jacket - (blue)",
         "SKU": "test-sku",
         "priceTotal": 69
       ]
     ]
   ]
   let addToCartEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: addToCartEvent)
   ```

1. Exibir a ocorrência do ExperienceEvent.

   ![ocorrência de xdm do analytics](assets/mobile-analytics-assurance-xdm.png)

1. Revise a parte XDM do JSON.

   ```json
     "xdm" : {
       "productListItems" : [ {
         "priceTotal" : 69,
         "SKU" : "test-sku",
         "name" : "neve studio dance jacket - (blue)"
       } ],
       "timestamp" : "2021-10-22T22:03:37Z",
       "commerce" : {
         "productListAdds" : {
           "value" : 1
         }
       },
       "eventType" : "commerce.productListAdds",
       //...
     }
   ```

1. Revise o `analytics.mapping` evento.

   ![ocorrência de xdm do analytics](assets/mobile-analytics-assurance-mapping.png)

Observe o seguinte no mapeamento do Analytics:

* &#39;events&#39; foi preenchido com &#39;scAdd&#39; com base em `commerce.productListAdds`.
* &#39;pl&#39; (variável de produtos) foi preenchido com um valor concatenado com base em `productListItems`.
* Há outras informações interessantes nesse evento, incluindo todos os dados de contexto.


## Mapeamento com dados de contexto

Os dados XDM encaminhados para o Analytics são convertidos em [dados de contexto](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/proc-rules.html?lang=en) incluindo campos padrão e personalizados.

A chave de dados de contexto é construída seguindo esta sintaxe:

```
a.x.[xdm path]
```

Por exemplo:

```
//Standard Field
a.x.commerce.saveforlaters.value

//Custom Field
a.x._techmarketingdemos.appinformationa.appstatedetails.screenname
```

>[!NOTE]
>
>Campos personalizados são colocados sob seu identificador Experience Cloud Org.
>
>&quot;_techmarketingdemos&quot; é substituído pelo valor exclusivo de sua organização.

Esta é a aparência de uma regra de processamento usando esses dados:

![regras de processamento do analytics](assets/mobile-analytics-processing-rules.png)

>[!IMPORTANT]
>
>
>Algumas das variáveis mapeadas automaticamente podem não estar disponíveis para uso nas regras de processamento.
>
>
>Na primeira vez que você mapeia para uma regra de processamento, a interface do usuário não mostra as variáveis de dados de contexto do objeto XDM. Para corrigir o que seleciona qualquer valor, clique em Salvar e volte para editar. Todas as variáveis XDM agora devem aparecer.


Informações adicionais sobre regras de processamento e dados de contexto podem ser encontradas [here](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules.html?lang=en).

>[!TIP]
>
>Ao contrário das implementações anteriores de aplicativos móveis, não há distinção entre páginas/exibições de tela e outros eventos. Em vez disso, você pode incrementar o **[!UICONTROL Exibição da página]** definindo a variável **[!UICONTROL Nome da página]** em uma regra de processamento. Como você está coletando o `screenName` no tutorial, é altamente recomendável mapear para **[!UICONTROL Nome da página]** em uma regra de processamento.


Próximo: **[Experience Platform](platform.md)**

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender sobre o Adobe Experience Platform Mobile SDK. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)