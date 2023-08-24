---
title: Mapeamento do Analytics
description: Saiba como coletar dados para o Adobe Analytics em um aplicativo móvel.
solution: Data Collection,Experience Platform,Analytics
hide: true
source-git-commit: e119e2bdce524c834cdaf43ed9eb9d26948b0ac6
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 2%

---

# Mapeamento do Analytics

Saiba como mapear dados móveis para o Adobe Analytics.

A variável [evento](events.md) Os dados coletados e enviados para a Platform Edge Network em lições anteriores são encaminhados para os serviços configurados na sua sequência de dados, incluindo o Adobe Analytics. Mapeie os dados para as variáveis corretas em seu conjunto de relatórios.

## Pré-requisitos

* Noções básicas sobre o rastreamento de ExperienceEvent.
* Dados XDM enviados com sucesso no aplicativo de amostra.
* Sequência de dados configurada para o Adobe Analytics

## Objetivos de aprendizagem

Nesta lição, você vai:

* Entenda o mapeamento automático de variáveis do Analytics.
* Configurar regras de processamento para mapear dados XDM para variáveis do Analytics.

## Mapeamento automático

Muitos dos campos XDM padrão são mapeados automaticamente para variáveis do Analytics. Veja a lista completa [aqui](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=en).

### Exemplo #1 - s.products

Um bom exemplo é o [variável products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) que não podem ser preenchidos com regras de processamento. Com uma implementação XDM, você passa todos os dados necessários em productListItems e s.products são preenchidos automaticamente por meio do mapeamento do Analytics.

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
>Atualmente `productListItems[N].SKU` é ignorado pelo mapeamento automático.

### Exemplo #2 - scAdd

Se você observar de perto, todos os eventos têm dois campos `value` (obrigatório) e `id` (opcional). A variável `value` é usado para incrementar a contagem de eventos. A variável `id` é usado para serialização.

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

## Validar com garantia

Usar o [Ferramenta de controle de qualidade Assurance](assurance.md) Você pode confirmar que está enviando um ExperienceEvent, que os dados XDM estão corretos e que o mapeamento do Analytics está acontecendo conforme esperado. Por exemplo:

1. Envie um evento productListAdds.

1. Veja a ocorrência do ExperienceEvent.

   ![ocorrência xdm do analytics](assets/analytics-assurance-experiencevent.png)

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
       "id" : "LLWS05.1-XS",
       "value" : 1
     }
   }
   // ...
   ```

1. Revise o **[!UICONTROL analytics.mapping]** evento.

   ![ocorrência xdm do analytics](assets/analytics-assurance-mapping.png)

Observe o seguinte no mapeamento do Analytics:

* **[!UICONTROL events]** são preenchidos com `scAdd` baseado em `commerce.productListAdds`.
* **[!UICONTROL pl]** (variável products) são preenchidos com um valor concatenado com base em `productListItems`.
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
>Campos personalizados são colocados sob o identificador Experience Cloud Org.
>
>`_techmarketingdemos` é substituída pelo valor único de sua organização.


Veja como uma regra de processamento usando esses dados pode ser exibida:

* Você **[!UICONTROL Substituir valor de]** (1) **[!UICONTROL Nome da tela do aplicativo (eVar 2)]** (2) com o valor de **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (3) se **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (4) **[!UICONTROL está definido]** (5).

* Você **[!UICONTROL Definir evento]** (6) **[!UICONTROL Adicionar à lista de desejos (Evento 3)]** (7) a **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (8) se **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (9) **[!UICONTROL está definido]** (10).

![regras de processamento do analytics](assets/analytics-processing-rules.png)

>[!IMPORTANT]
>
>
>Algumas das variáveis mapeadas automaticamente podem não estar disponíveis para uso nas regras de processamento.
>
>
>Na primeira vez que você mapeia para uma regra de processamento, a interface do usuário não mostra as variáveis de dados de contexto do objeto XDM. Para corrigir isso, selecione qualquer valor, Salve e volte para editar. Todas as variáveis XDM agora devem aparecer.


Informações adicionais sobre regras de processamento e dados de contexto podem ser encontradas [aqui](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules.html?lang=en).

>[!TIP]
>
>Ao contrário de implementações anteriores do aplicativo móvel, não há distinção entre exibições de página/tela e outros eventos. Em vez disso, você pode incrementar a variável **[!UICONTROL Exibição da página]** ao definir a variável **[!UICONTROL Nome da página]** em uma regra de processamento. Como você está coletando o personalizado `screenName` no tutorial, é altamente recomendável mapear o nome da tela para **[!UICONTROL Nome da página]** em uma regra de processamento.

>[!SUCCESS]
>
>Você configurou o aplicativo para mapear os objetos XDM da Experience Edge para variáveis do Adobe Analytics, habilitando o serviço da Adobe Analytics no fluxo de dados e usando regras de processamento, quando aplicável.<br/> Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Próximo: **[Experience Platform](platform.md)**
