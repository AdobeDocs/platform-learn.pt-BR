---
title: Enviar parâmetros - Migrar a implementação do Adobe Target no aplicativo móvel para o Adobe Journey Optimizer - Extensão de decisão
description: Saiba como enviar parâmetros de mbox, perfil e entidade para o Adobe Target usando o Experience Platform Web SDK.
exl-id: 927d83f9-c019-4a6b-abef-21054ce0991b
source-git-commit: b8baa6d48b9a99d2d32fad2221413b7c10937191
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 1%

---

# Enviar parâmetros para o Target usando a extensão do Decisioning

As implementações do Target diferem entre os aplicativos móveis devido à arquitetura do aplicativo, aos requisitos comerciais e aos recursos usados. A maioria das implementações do Target inclui transmitir vários parâmetros para informações contextuais, públicos-alvo e recomendações de conteúdo.

Com a extensão Target, todos os parâmetros Target foram passados usando a função `TargetParameters`.

Com a extensão de decisão:

* Parâmetros destinados a vários aplicativos do Adobe podem ser passados no objeto XDM
* Parâmetros destinados somente ao Target podem ser passados no objeto `data.__adobe.target`


>[!IMPORTANT]
>
> Com a extensão Decisão, os parâmetros enviados em uma solicitação se aplicam a todos os escopos na solicitação. Se você precisar definir parâmetros diferentes para escopos diferentes, faça solicitações adicionais.

## Parâmetros personalizados

Parâmetros de mbox personalizados são a maneira mais básica de enviar dados para o Target e podem ser passados nos objetos `xdm` ou `data.__adobe.target`.

## Parâmetros do perfil

Os parâmetros de perfil armazenam dados por um longo período no perfil de Destino do usuário e devem ser passados no objeto `data.__adobe.target`.

## Parâmetros de entidade

[Parâmetros de entidade](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html) são usados para transmitir dados comportamentais e informações de catálogo complementares para Recomendações de Destino. Semelhante aos parâmetros do perfil, a maioria dos parâmetros da entidade deve ser passada sob o objeto `data.__adobe.target`. A única exceção é que a matriz `xdm.productListItems` está presente, então o primeiro valor `SKU` é usado como `entity.id`.

Os parâmetros de entidade para um item específico devem ter o prefixo `entity.` para a captura adequada de dados. Os parâmetros `cartIds` e `excludedIds` reservados para algoritmos de recomendações não devem ter o prefixo e o valor de cada um deles deve conter uma lista separada por vírgulas de IDs de entidade.

## Parâmetros de compra

Os parâmetros de compra são passados em uma página de confirmação de pedido após um pedido bem-sucedido e são usados para metas de conversão e otimização do Target. Com uma implementação do Platform Mobile SDK usando a extensão Decisioning, esses parâmetros e são mapeados automaticamente a partir de dados XDM transmitidos como parte do grupo de campos `commerce`.

As informações de compra são passadas para o Target quando o grupo de campos `commerce` tem `purchases.value` definido como `1`. A ID do pedido e o total do pedido são mapeados automaticamente a partir do objeto `order`. Se a matriz `productListItems` estiver presente, os valores `SKU` serão usados para `productPurchasedId`.

Se você não estiver passando `commerce` campos no objeto `xdm`, é possível passar os detalhes do pedido para o público alvo usando os campos `data.__adobe.target.orderId`, `data.__adobe.target.orderTotal` e `data.__adobe.target.productPurchasedId`.

## ID do cliente (mbox3rdPartyId)

O Target permite a sincronização de perfis entre dispositivos e sistemas usando uma única ID do cliente. Essa ID do cliente deve ser passada no campo `identityMap` do objeto XDM e mapeada para o campo ID de terceiros do Target na sequência de dados.

## Tabela

| Exemplo de parâmetro at.js | Opção do Platform Web SDK | Notas |
| --- | --- | --- |
| `at_property` | N/D | Os tokens de propriedade estão configurados na [sequência de dados](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) e não podem ser definidos na chamada `sendEvent`. |
| `pageName` | `xdm.web.webPageDetails.name` ou <br> `data.__adobe.target.pageName` | Os parâmetros da mbox de destino podem ser passados como parte do objeto `xdm` ou parte do objeto `data.__adobe.target`. |
| `profile.gender` | `data.__adobe.target.profile.gender` | Todos os parâmetros de perfil do Target devem ser passados como parte do objeto `data` e prefixados com `profile.` para serem mapeados adequadamente. |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | Parâmetro reservado usado para o recurso Afinidade de Categoria do Destino que deve ser passado como parte do objeto `data`. |
| `entity.id` | `data.__adobe.target.entity.id` <br>OU<br> `xdm.productListItems[0].SKU` | As IDs de entidade são usadas para contadores comportamentais do Target Recommendations. Essas IDs de entidade podem ser passadas como parte do objeto `data` ou mapeadas automaticamente a partir do primeiro item na matriz `xdm.productListItems` se sua implementação usar esse grupo de campos. |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | As IDs de categoria de entidade podem ser passadas como parte do objeto `data`. |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | Parâmetros de entidade personalizados são usados para atualizar o catálogo de produtos do Recommendations. Esses parâmetros personalizados devem ser passados como parte do objeto `data`. |
| `cartIds` | `data.__adobe.target.cartIds` | Usado para os algoritmos de recomendações baseadas no carrinho do Target. |
| `excludedIds` | `data.__adobe.target.excludedIds` | Usado para impedir que IDs de entidade específicas retornem em um design de recomendações. |
| `mbox3rdPartyId` | Definir no objeto `xdm.identityMap` | Usado para sincronizar perfis do Target entre dispositivos e atributos do cliente. O namespace a ser usado para a ID do cliente deve ser especificado na [Configuração de destino da sequência de dados](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid.html). |
| `orderId` | `xdm.commerce.order.purchaseID`<br> (quando `commerce.purchases.value` está definido como `1`)<br> ou<br> `data.__adobe.target.orderId` | Usado para identificar um pedido exclusivo para o rastreamento de conversão do Target. |
| `orderTotal` | `xdm.commerce.order.priceTotal`<br> (quando `commerce.purchases.value` está definido como `1`)<br> ou<br> `data.__adobe.target.orderTotal` | Usado para rastrear totais de ordem para metas de conversão e otimização de Target. |
| `productPurchasedId` | `xdm.productListItems[0-n].SKU`<br> (quando `commerce.purchases.value` está definido como `1`) <br>OU<br> `data.__adobe.target.productPurchasedId` | Usado para rastreamento de conversão do Target e algoritmos de recomendações. |
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | Usado para a meta de atividade [pontuação personalizada](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html). |

{style="table-layout:auto"}


## Exemplos de transmissão de parâmetros

Vamos usar um exemplo simples para demonstrar as diferenças entre as extensões ao transmitir parâmetros para o Target.

### Android

>[!BEGINTABS]

>[!TAB Otimizar SDK]

```Java
final Map<String, Object> data = new HashMap<>();
final Map<String, String> targetParameters = new HashMap<>();
 
// Mbox parameters
targetParameters.put("status", "platinum");
 
// Profile parameters - prefix with profile.
targetParameters.put("profile.gender", "male");
 
// Product parameters
targetParameters.put("productId", "pId1");
targetParameters.put("categoryId", "cId1");
 
// Order parameters
targetParameters.put("orderId", "id1");
targetParameters.put("orderTotal", "1.0");
targetParameters.put("purchasedProductIds", "ppId1");
 
data.put("__adobe", new HashMap<String, Object>() {
  {
    put("target", targetParameters);
  }
});
 
// Target location (or mbox)
final DecisionScope decisionScope = DecisionScope("myTargetLocation")
 
final List<DecisionScope> decisionScopes = new ArrayList<>();
decisionScopes.add(decisionScope);
 
Optimize.updatePropositions(decisionScopes, null, data);
```

>[!TAB SDK de Destino]

```Java
Map<String, String> mboxParameters = new HashMap<String, String>();
mboxParameters1.put("status", "platinum");
 
Map<String, String> profileParameters = new HashMap<String, String>();
profileParameters1.put("gender", "male");
 
List<String> purchasedProductIds = new ArrayList<String>();
purchasedProductIds.add("ppId1");
TargetOrder targetOrder = new TargetOrder("id1", 1.0, purchasedProductIds);
 
TargetProduct targetProduct = new TargetProduct("pId1", "cId1");
 
TargetParameters targetParameters = new TargetParameters.Builder()
                                    .parameters(mboxParameters)
                                    .profileParameters(profileParameters)
                                    .product(targetProduct)
                                    .order(targetOrder)
                                    .build();
```

>[!ENDTABS]

### iOS

>[!BEGINTABS]

>[!TAB Otimizar SDK]

```Swift
var data: [String: Any] = [:]
var targetParameters: [String: String] = [:]
 
// Mbox parameters
targetParameters["status"] = "platinum"
 
// Profile parameters - prefix with profile.
targetParameters["profile.gender"] = "make"
 
// Product parameters
targetParameters["productId"] = "pId1"
targetParameters["categoryId"] = "cId1"
 
// Add order parameters
targetParameters["orderId"] = "id1"
targetParameters["orderTotal"] = "1.0"
targetParameters["purchasedProductIds"] = "ppId1"
 
data["__adobe"] = [
  "target": targetParameters
]
 
// Target location (or mbox)
let decisionScope = DecisionScope(name: "myTargetLocation")
Optimize.updatePropositions(for: [decisionScope] withXdm: nil andData: data)
```

>[!TAB SDK de Destino]

```Swift
let mboxParameters = [
                        "status": "platinum"
                     ]
 
let profileParameters = [
                            "gender": "male"
                        ]
 
let order = TargetOrder(id: "id1", total: 1.0, purchasedProductIds: ["ppId1"])
 
let product = TargetProduct(productId: "pId1", categoryId: "cId1")
 
let targetParameters = TargetParameters(parameters: mboxParameters, profileParameters: profileParameters, order: order, product: product))
```


>[!ENDTABS]






Em seguida, saiba como [rastrear eventos de conversão do Target](track-events.md) com o Platform Web SDK.

>[!NOTE]
>
>Estamos empenhados em ajudá-lo a ser bem-sucedido na migração para dispositivos móveis do Target da extensão do Target para a extensão do Decisioning. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
