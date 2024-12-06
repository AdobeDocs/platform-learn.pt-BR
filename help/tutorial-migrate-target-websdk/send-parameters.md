---
title: Enviar parâmetros - Migrar o Target da at.js 2.x para o SDK da Web
description: Saiba como enviar parâmetros de mbox, perfil e entidade para o Adobe Target usando o SDK da Web do Experience Platform.
exl-id: 7916497b-0078-4651-91b1-f53c86dd2100
source-git-commit: f30d6434be69e87406326955b3821d07bd2e66c1
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 0%

---

# Enviar parâmetros para o Target usando o SDK da Web da plataforma

As implementações do Target diferem entre os sites devido à arquitetura do site, aos requisitos comerciais e aos recursos usados. A maioria das implementações do Target inclui transmitir vários parâmetros para informações contextuais, públicos-alvo e recomendações de conteúdo.

Vamos usar uma página simples de detalhes do produto e uma página de confirmação de pedido para demonstrar as diferenças entre as bibliotecas ao transmitir parâmetros para o Target.

Considere os dois exemplos de páginas a seguir que usam at.js:

+++at.js em uma página de Detalhes do produto:

```HTML
<!doctype html>
<html>
<head>
  <title>Product Details - Men's Shirt</title>
  <!--Target parameters -->
  <script>
    targetPageParams = function() {
      return {
        // Property token
        "at_property": "5a0fd9bb-67de-4b5a-0fd7-9cc09f50a58d",
        // Mbox parameters
        "pageName": "product detail",
        // Profile parameters
        "profile.gender": "male",
        "user.categoryId": "clothing",
        // Entity parameters for Target Recomendations
        "entity.id": "SKU-00001-LARGE",
        "entity.categoryId": "clothing,shirts",
        "entity.customEntity": "some value",
        "cartIds": "SKU-00002,SKU-00003",
        "excludedIds": "SKU-00001-SMALL",
        // Customer ID for cross-device profile synching and Customer Attributes
        "mbox3rdPartyId": "TT8675309",
      };
    };
  </script>
  <!--Target at.js library loaded asynchonously-->
  <script src="/libraries/at.js" async></script>
</head>
<body>
  <h1 id="title">Men's Large Shirt</h1>
  <p>SKU: SKU-00001-LARGE</p>
</body>
</html>
```

+++


+++at.js em uma página de Confirmação de pedido:

```HTML
<!doctype html>
<html>
<head>
  <title>Order Confirmation</title>-->
  <!--Target parameters -->
  <script>
    targetPageParams = function() {
      return {
        // Property token
        "at_property": "5a0fd9bb-67de-4b5a-0fd7-9cc09f50a58d",
        // Order confirmation parameters
        "orderId": "ABC123",
        "productPurchasedId": "SKU-00002,SKU-00003",
        "orderTotal": 1337.89,
        // Customer ID for cross-device profile synching and Customer Attributes
        "mbox3rdPartyId": "TT8675309",
      };
    };
  </script>
  <!--Target at.js library loaded asynchonously-->
  <script src="/libraries/at.js" async></script>
</head>
<body>
  <h1 id="title">Order Confirmation</h1>
  <p>Thank you for your order</p>
</body>
</html>
```

+++


## Resumo de mapeamento de parâmetros

Os parâmetros do Target para essas páginas são enviados de forma diferente usando o SDK da Web da plataforma. Há várias maneiras de enviar parâmetros para o Target usando a at.js:

- Definir com a função `targetPageParams()` para o evento de carregamento de página (usado nos exemplos desta página)
- Definir com a função `targetPageParamsAll()` para todas as solicitações do Target na página
- Enviar parâmetros diretamente com a função `getOffer()` para um único local
- Enviar parâmetros diretamente com a função `getOffers()` para um ou mais locais


O SDK da Web da Platform fornece uma única maneira consistente de enviar dados sem a necessidade de funções adicionais. Todos os parâmetros devem ser passados na carga com o comando `sendEvent` e se enquadram em duas categorias:

- Mapeado automaticamente do objeto `xdm`
- Passado manualmente usando o objeto `data.__adobe.target`

A tabela abaixo descreve como os parâmetros de exemplo seriam remapeados usando o SDK da Web da plataforma:

| Exemplo de parâmetro at.js | Opção do SDK da Web da Platform | Notas |
| --- | --- | --- |
| `at_property` | N/D | Os tokens de propriedade estão configurados na [sequência de dados](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) e não podem ser definidos na chamada `sendEvent`. |
| `pageName` | `xdm.web.webPageDetails.name` | Todos os parâmetros de mbox do Target devem ser passados como parte do objeto `xdm` e estar em conformidade com um esquema usando a classe XDM ExperienceEvent. Os parâmetros da mbox não podem ser passados como parte do objeto `data`. |
| `profile.gender` | `data.__adobe.target.profile.gender` | Todos os parâmetros de perfil do Target devem ser passados como parte do objeto `data` e prefixados com `profile.` para serem mapeados adequadamente. |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | Parâmetro reservado usado para o recurso Afinidade de Categoria do Destino que deve ser passado como parte do objeto `data`. |
| `entity.id` | `data.__adobe.target.entity.id` <br>OU<br> `xdm.productListItems[0].SKU` | As IDs de entidade são usadas para contadores comportamentais do Recommendations de destino. Essas IDs de entidade podem ser passadas como parte do objeto `data` ou mapeadas automaticamente a partir do primeiro item na matriz `xdm.productListItems` se sua implementação usar esse grupo de campos. |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | As IDs de categoria de entidade podem ser passadas como parte do objeto `data`. |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | Parâmetros de entidade personalizados são usados para atualizar o catálogo de produtos do Recommendations. Esses parâmetros personalizados devem ser passados como parte do objeto `data`. |
| `cartIds` | `data.__adobe.target.cartIds` | Usado para os algoritmos de recomendações baseadas no carrinho do Target. |
| `excludedIds` | `data.__adobe.target.excludedIds` | Usado para impedir que IDs de entidade específicas retornem em um design de recomendações. |
| `mbox3rdPartyId` | Definir no objeto `xdm.identityMap` | Usado para sincronizar perfis do Target entre dispositivos e atributos do cliente. O namespace a ser usado para a ID do cliente deve ser especificado na [Configuração de destino da sequência de dados](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid.html). |
| `orderId` | `xdm.commerce.order.purchaseID` | Usado para identificar um pedido exclusivo para o rastreamento de conversão do Target. |
| `orderTotal` | `xdm.commerce.order.priceTotal` | Usado para rastrear totais de ordem para metas de conversão e otimização de Target. |
| `productPurchasedId` | `data.__adobe.target.productPurchasedId` <br>OU<br> `xdm.productListItems[0-n].SKU` | Usado para rastreamento de conversão do Target e algoritmos de recomendações. Consulte a seção [parâmetros de entidade](#entity-parameters) abaixo para obter detalhes. |
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | Usado para a meta de atividade [pontuação personalizada](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html). |

{style="table-layout:auto"}

## Parâmetros personalizados

Parâmetros de mbox personalizados devem ser passados como dados XDM com o comando `sendEvent`. É importante garantir que o esquema XDM inclua todos os campos necessários para a implementação do Target.

Exemplo de at.js usando `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "pageName": "product detail"
  };
};
```

Exemplos de JavaScript do SDK da Web da plataforma usando o comando `sendEvent`:

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetails": {
        // Other attributes included according to xdm schema
        "name": "product detail"
      }
    }
  }
});
```

>[!TAB Tags]

Nas marcas, primeiro use um elemento de dados [!UICONTROL objeto XDM] para mapear para o campo XDM:

![Mapeamento para um campo XDM em um elemento de dados do Objeto XDM](assets/params-tags-pageName.png){zoomable="yes"}

E inclua seu [!UICONTROL objeto XDM] na sua [!UICONTROL ação de envio] (vários [!UICONTROL objetos XDM] podem ser [mesclados](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)):

![Incluindo um elemento de dados de objeto XDM em um evento Send](assets/params-tags-sendEvent.png){zoomable="yes"}

>[!ENDTABS]


>[!NOTE]
>
>Como os parâmetros personalizados da mbox fazem parte do objeto `xdm`, você precisa atualizar quaisquer públicos-alvo, atividades ou scripts de perfil que referenciem esses parâmetros da mbox usando seus novos nomes. Consulte a página [Atualizar públicos-alvo e scripts de perfil do Target para compatibilidade com o SDK da Web da plataforma](update-audiences.md) deste tutorial para obter mais informações.


## Parâmetros do perfil

Os parâmetros do perfil de destino devem ser passados sob o objeto `data.__adobe.target` na carga do comando `sendEvent` do SDK da Web da plataforma.

Semelhante ao at.js, todos os parâmetros de perfil também devem ter o prefixo `profile.` para que o valor seja armazenado corretamente como um atributo de perfil de Destino persistente. O parâmetro reservado `user.categoryId` para o recurso de Afinidade de Categoria do Target tem o prefixo `user.`.

Exemplo de at.js usando `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "profile.gender": "male",
    "user.categoryId": "clothing"
  };
};
```

Exemplos de SDK da Web da plataforma usando o comando `sendEvent`:

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "data": {
    "__adobe": {
      "target": {
        "profile.gender": "male",
        "user.categoryId": "clothing"
      }
    }
  }
});
```

>[!TAB Tags]

Nas marcas, primeiro crie um elemento de dados para definir o objeto `data.__adobe.target`:

![Definindo seu objeto de dados em um elemento de dados](assets/params-tags-dataObject.png){zoomable="yes"}

E inclua seu objeto de dados em sua [!UICONTROL ação de envio] (vários [!UICONTROL objetos] podem ser [mesclados](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)):

![Incluindo um objeto de dados em um evento Send](assets/params-tags-sendEvent-withData.png){zoomable="yes"}

>[!ENDTABS]

## Parâmetros de entidade

Parâmetros de entidade são usados para transmitir dados comportamentais e informações de catálogo complementares para o Target Recommendations. Todos os [parâmetros de entidade](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html) suportados pela at.js também são suportados pelo SDK da Web da plataforma. Semelhante aos parâmetros de perfil, todos os parâmetros de entidade devem ser passados sob o objeto `data.__adobe.target` na carga do comando `sendEvent` do SDK da Web da plataforma.

Os parâmetros de entidade para um item específico devem ter o prefixo `entity.` para a captura adequada de dados. Os parâmetros `cartIds` e `excludedIds` reservados para algoritmos de recomendações não devem ter o prefixo e o valor de cada um deles deve conter uma lista separada por vírgulas de IDs de entidade.

Exemplo de at.js usando `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "entity.id": "SKU-00001-LARGE",
    "entity.categoryId": "clothing,shirts",
    "entity.customEntity": "some value",
    "cartIds": "SKU-00002,SKU-00003",
    "excludedIds": "SKU-00001-SMALL"
  };
};
```

Exemplos de SDK da Web da plataforma usando o comando `sendEvent`:

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "data": {
    "__adobe": {
      "target": {
        "entity.id": "SKU-00001-LARGE",
        "entity.categoryId": "clothing,shirts",
        "entity.customEntity": "some value",
        "cartIds": "SKU-00002,SKU-00003",
        "excludedIds": "SKU-00001-SMALL"
      }
    }
  }
});
```

>[!TAB Tags]

Nas marcas, primeiro crie um elemento de dados para definir o objeto `data.__adobe.target`:

![Definindo seu objeto de dados em um elemento de dados](assets/params-tags-dataObject-entities.png){zoomable="yes"}

E inclua seu objeto de dados em sua [!UICONTROL ação de envio] (vários [!UICONTROL objetos] podem ser [mesclados](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)):

![Incluindo um objeto de dados em um evento Send](assets/params-tags-sendEvent-withData.png){zoomable="yes"}

>[!ENDTABS]

>[!NOTE]
>
>Se o grupo de campos `commerce` for usado e a matriz `productListItems` for incluída na carga XDM, o primeiro valor `SKU` nessa matriz será mapeado para `entity.id` para fins de incremento de uma exibição de produto.


## Parâmetros de compra

Os parâmetros de compra são passados em uma página de confirmação de pedido após um pedido bem-sucedido e são usados para metas de conversão e otimização do Target. Com uma implementação do SDK da Web da Platform, esses parâmetros e são mapeados automaticamente a partir de dados XDM transmitidos como parte do grupo de campos `commerce`.

Exemplo de at.js usando `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "orderId": "ABC123",
    "productPurchasedId": "SKU-00002,SKU-00003"
    "orderTotal": 1337.89
  };
};
```

As informações de compra são passadas para o Target quando o grupo de campos `commerce` tem `purchases.value` definido como `1`. A ID do pedido e o total do pedido são mapeados automaticamente a partir do objeto `order`. Se a matriz `productListItems` estiver presente, os valores `SKU` serão usados para `productPurchasedId`.

Exemplo de SDK da Web da plataforma usando `sendEvent`:

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "ABC123",
        "priceTotal": 1337.89
      },
      "purchases": {
        "value": 1
      }
    },
    "productListItems": [{
      "SKU": "SKU-00002"
    }, {
      "SKU": "SKU-00003"
    }],
      "_experience": {
          "decisioning": {
              "propositions": [{
                  "scope": "<your_mbox>"
              }],
              "propositionEventType": {
                  "display": 1
              }
          }
      }
  }
});
```

>[!TAB Tags]

Nas tags, primeiro use um elemento de dados [!UICONTROL objeto XDM] para mapear para os campos XDM necessários (consulte o exemplo do JavaScript) e o escopo personalizado opcional:

![Mapeamento para um campo XDM em um elemento de dados do Objeto XDM](assets/params-tags-purchase.png){zoomable="yes"}

E inclua seu [!UICONTROL objeto XDM] na sua [!UICONTROL ação de envio] (vários [!UICONTROL objetos XDM] podem ser [mesclados](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)):

![Incluindo um elemento de dados de objeto XDM em um evento Send](assets/params-tags-sendEvent-purchase.png){zoomable="yes"}

>[!ENDTABS]

>[!IMPORTANT]
>
> `_experience.decisioning.propositionEventType` deve ser definido com `display: 1` para que a chamada seja usada para incrementar uma métrica do Target.

>[!NOTE]
>
> Se você quiser usar um nome de local/mbox personalizado em sua definição de métrica do Target, por exemplo `orderConfirmPage`, preencha a matriz `_experience.decisioning.propositions` com um escopo personalizado, como no exemplo acima.

>[!NOTE]
>
>O valor `productPurchasedId` também pode ser passado como uma lista separada por vírgulas de IDs de entidade sob o objeto `data`.


## ID do cliente (mbox3rdPartyId)

O Target permite a sincronização de perfis entre dispositivos e sistemas usando uma única ID de cliente. Com a at.js, isso pode ser definido como `mbox3rdPartyId` na solicitação do Target ou como a primeira ID do cliente enviada para o Serviço de identidade Experience Cloud. Ao contrário da at.js, uma implementação do SDK da Web da Platform permite especificar qual ID de cliente usar como o `mbox3rdPartyId`, se houver várias. Por exemplo, se sua empresa tiver uma ID de cliente global e IDs de cliente separadas para diferentes linhas de negócios, você poderá configurar qual ID do Target deve usar.

Há algumas etapas para configurar a sincronização de ID para casos de uso de dispositivos cruzados do Target e Atributos do cliente:

1. Crie um **[!UICONTROL namespace de identidade]** para a ID do cliente na tela **[!UICONTROL Identidades]** da Coleção de Dados ou da Plataforma
1. Verifique se o **[!UICONTROL alias]** nos Atributos do cliente corresponde ao **[!UICONTROL símbolo de identidade]** do seu namespace
1. Especifique o **[!UICONTROL símbolo de identidade]** como o **[!UICONTROL Namespace de ID de Terceiros de Destino]** na configuração de Destino da sequência de dados
1. Executar um comando `sendEvent` usando o grupo de campos `identityMap`

Exemplo de at.js usando `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "mbox3rdPartyId": "TT8675309"
  };
};
```

Exemplos de SDK da Web da plataforma usando o comando `sendEvent`:

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "identityMap": {
      "GLOBAL_CUSTOMER_ID": [{
        "id": "TT8675309",
        "authenticatedState": "authenticated",
        "primary": true
      }]
    }
  }
});
```

>[!TAB Tags]

O valor [!UICONTROL ID], [!UICONTROL Estado autenticado] e [!UICONTROL Namespace] foram capturados em um elemento de dados [!UICONTROL Mapa de identidade]:
![Elemento de dados do Mapa de identidade capturando a ID do cliente](assets/params-tags-customerIdDataElement.png){zoomable="yes"}

O elemento de dados [!UICONTROL Mapa de identidade] é usado para definir o campo [!UICONTROL Mapa de identidade] no elemento de dados [!UICONTROL objeto XDM]:
![Elemento de dados do Mapa de Identidade usado no elemento de dados do objeto XDM](assets/params-tags-customerIdInXDMObject.png){zoomable="yes"}

O [!UICONTROL objeto XDM] é então incluído na ação [!UICONTROL Enviar evento] de uma regra:

![Incluindo um elemento de dados de objeto XDM em um evento Send](assets/params-tags-sendEvent-xdm.png){zoomable="yes"}

No serviço Adobe Target da sua sequência de dados, certifique-se de definir o [!UICONTROL Namespace de ID de terceiros de destino] para o mesmo namespace usado no elemento de dados [!UICONTROL Mapa de identidade]:
![Definir o Namespace da ID de Terceiros de Destino na sequência de dados](assets/params-tags-customerIdNamespaceInDatastream.png){zoomable="yes"}

>[!ENDTABS]

>[!NOTE]
>
> A Adobe recomenda enviar namespaces que representam uma pessoa, como identidades autenticadas, como a identidade principal.



## Exemplo de SDK da Web da Platform

Agora que você entende como os diferentes parâmetros do Target são mapeados usando o SDK da Web da Platform, nossas duas páginas de exemplo podem ser migradas da at.js para o SDK da Web da Platform, como mostrado abaixo. As páginas de exemplo incluem o seguinte:

- Trecho pré-ocultação do Target para uma implementação de biblioteca assíncrona
- O código base do SDK da Web da plataforma
- A biblioteca de JavaScript do SDK da Web da Platform
- Um comando `configure` para inicializar a biblioteca
- Um comando `sendEvent` para enviar dados e solicitar que o conteúdo do Target seja renderizado

+++SDK da Web em uma página de Detalhes do produto:

```HTML
<!doctype html>
<html>
<head>
  <title>Product Details - Men's Shirt</title>

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

  <!--Platform Web SDK base code-->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
  <script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>

  <!--Configure Platform Web SDK and send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    alloy("sendEvent", {
      "renderDecisions": true,
      "xdm": {
        "identityMap": {
          "GLOBAL_CUSTOMER_ID": [{
            "id": "TT8675309",
            "authenticatedState": "authenticated",
            "primary": true
          }]
        },
        "web": {
          "webPageDetails": {
            // Other attributes included according to XDM schema
            "pageName": "product detail"
          }
        }
      },
      "data": {
        "__adobe": {
          "target": {
            "profile.gender": "male",
            "user.categoryId": "clothing",
            "entity.id": "SKU-00001-LARGE",
            "entity.categoryId": "clothing,shirts",
            "entity.customEntity": "some value",
            "cartIds": "SKU-00002,SKU-00003",
            "excludedIds": "SKU-00001-SMALL"
          }
        }
      }
    });
  </script>
</head>
<body>
  <h1 id="title">Men's Large Shirt</h1>
  <p>SKU: SKU-00001-LARGE</p>
</body>
</html>
```

+++

+++SDK da Web em uma página de Confirmação de pedido:

```HTML
<!doctype html>
<html>
<head>
  <title>Order Confirmation</title>


  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->

  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

  <!--Platform Web SDK base code-->

  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
    (window,["alloy"]);
  </script>
  <!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
  <script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>

  <!--Configure Platform Web SDK and send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    alloy("sendEvent", {
      "xdm": {
        "identityMap": {
          "GLOBAL_CUSTOMER_ID": [{
            "id": "TT8675309",
            "authenticatedState": "authenticated",
            "primary": true
          }]
        },
        "commerce": {
          "order": {
            "purchaseID": "ABC123",
            "priceTotal": 1337.89
          },
          "purchases": {
            "value": 1
          }
        },
        "productListItems": [{
          "SKU": "SKU-00002"
        }, {
          "SKU": "SKU-00003"
        }],
        "_experience": {
            "decisioning": {
                "propositions": [{
                    "scope": "<your_mbox>"
                }],
                "propositionEventType": {
                    "display": 1
                }
            }
        }
      }
    });
  </script>
</head>
<body>
  <h1 id="title">Order Confirmation</h1>
  <p>Thank you for your order</p>
</body>
</html>
```

+++

Em seguida, saiba como [rastrear eventos de conversão do Target](track-events.md) com o SDK da Web da plataforma.

>[!NOTE]
>
>Estamos empenhados em ajudar você a ter sucesso com a migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
