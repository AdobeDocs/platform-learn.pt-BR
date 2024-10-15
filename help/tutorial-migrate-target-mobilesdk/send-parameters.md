---
title: Enviar parâmetros - Migrar o Target da at.js 2.x para o SDK da Web
description: Saiba como enviar parâmetros de mbox, perfil e entidade para o Adobe Target usando o SDK da Web do Experience Platform.
source-git-commit: 009548969b88d1bfa6eac23f65b1ca2144f27c34
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 0%

---

# Enviar parâmetros para o Target usando o SDK da Web da plataforma

As implementações do Target diferem entre os sites devido à arquitetura do site, aos requisitos comerciais e aos recursos usados. A maioria das implementações do Target inclui transmitir vários parâmetros para informações contextuais, públicos-alvo e recomendações de conteúdo.

Vamos usar uma página simples de detalhes do produto e uma página de confirmação de pedido para demonstrar as diferenças entre as extensões ao transmitir parâmetros para o Target.


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

Os parâmetros de mbox personalizados devem ser passados como XDM ou usando o objeto de dados com o comando `sendEvent`. É importante garantir que o esquema XDM inclua todos os campos necessários para a implementação do Target.


## Parâmetros do perfil

Os parâmetros do perfil de destino devem ser passados...

## Parâmetros de entidade

Parâmetros de entidade são usados para transmitir dados comportamentais e informações de catálogo complementares para o Target Recommendations. Todos os [parâmetros de entidade](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html) suportados pela at.js também são suportados pelo SDK da Web da plataforma. Semelhante aos parâmetros de perfil, todos os parâmetros de entidade devem ser passados sob o objeto `data.__adobe.target` na carga do comando `sendEvent` do SDK da Web da plataforma.

Os parâmetros de entidade para um item específico devem ter o prefixo `entity.` para a captura adequada de dados. Os parâmetros `cartIds` e `excludedIds` reservados para algoritmos de recomendações não devem ter o prefixo e o valor de cada um deles deve conter uma lista separada por vírgulas de IDs de entidade.



## Parâmetros de compra

Os parâmetros de compra são passados em uma página de confirmação de pedido após um pedido bem-sucedido e são usados para metas de conversão e otimização do Target. Com uma implementação do SDK móvel da Platform usando a extensão Otimize, esses parâmetros e são mapeados automaticamente a partir de dados XDM transmitidos como parte do grupo de campos `commerce`.


As informações de compra são passadas para o Target quando o grupo de campos `commerce` tem `purchases.value` definido como `1`. A ID do pedido e o total do pedido são mapeados automaticamente a partir do objeto `order`. Se a matriz `productListItems` estiver presente, os valores `SKU` serão usados para `productPurchasedId`.


## ID do cliente (mbox3rdPartyId)

O Target permite a sincronização de perfis entre dispositivos e sistemas usando uma única ID de cliente.



Em seguida, saiba como [rastrear eventos de conversão do Target](track-events.md) com o SDK da Web da plataforma.

>[!NOTE]
>
>Estamos empenhados em ajudá-lo a ser bem-sucedido na migração para dispositivos móveis do Target da extensão do Target para a extensão do Otimize. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
