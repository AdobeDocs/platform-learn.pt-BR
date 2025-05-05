---
title: Rastrear eventos - Migrar o Target da at.js 2.x para o SDK da Web
description: Saiba como rastrear eventos de conversão do Adobe Target usando o SDK da Web do Experience Platform.
exl-id: 5da772bc-de05-4ea9-afbd-3ef58bc7f025
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 1%

---

# Rastrear eventos de conversão do Target usando o SDK da Web da plataforma

Os eventos de conversão do Target podem ser rastreados com o SDK da Web da plataforma semelhante à at.js. Os eventos de conversão normalmente se enquadram nas seguintes categorias:

* Eventos rastreados automaticamente que não exigem nenhuma configuração
* Eventos de conversão de compra que devem ser ajustados para uma implementação do SDK da Web da plataforma de práticas recomendadas
* Eventos de conversão que não são de compra e que exigem atualizações de código

## Comparação do rastreamento de metas

A tabela a seguir compara como a at.js e o SDK da Web da Platform rastreiam eventos de conversão

| Objetivo da atividade | at.js 2.x do Target | SDK da Web da Platform |
|---|---|---|
| Conversão > Visualizou uma página | Rastreado automaticamente. Com base no valor de `context.address.url` na carga da solicitação de at.js. | Rastreado automaticamente. Baseado no valor de `xdm.web.webPageDetails.URL` na carga `sendEvent` |
| Conversão > Visualizou uma mbox | Rastreado com a solicitação de um local de mbox de exibição ou uma notificação usando `trackEvent()` ou `sendNotifications()` com um valor `type` de `display`. | Rastreado com uma chamada `sendEvent` do SDK da Web da plataforma com o `eventType` de `decisioning.propositionDisplay`. |
| Conversão > Clicou em um elemento | Rastreado automaticamente para atividades baseadas em VEC. Aparece como uma chamada de rede at.js com um objeto `notifications` na carga da solicitação in e um valor `type` de `click`. | Rastreado automaticamente para atividades baseadas em VEC. Aparece como uma chamada `sendEvent` do SDK da Web da Platform com o `eventType` de `decisioning.propositionInteract`. |
| Engajamento > Exibições de página | Rastreado automaticamente | Rastreado automaticamente |
| Engajamento > Tempo no site | Rastreado automaticamente | Rastreado automaticamente |

<!--
| Revenue > RPV, AOV, or Total Sales | Tracked based on the `orderTotal` parameter values for the specified mbox(es) | Tracked based on the `xdm.commerce.order.priceTotal` values. Its best to use the "any mbox" option in the goal setup. |
| Revenue > Orders | Tracked based on the unique `orderId` parameter values for the specified mbox(es) | Tracked based on the unique values for `xdm.commerce.order.purchaseID`. Its best to use the "any mbox" option in the goal setup. |
| Engagement > Custom Scoring | Tracked with the `mboxPageValue` parameter. Refer to the [dedicated documentation](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html?lang=pt-BR) for more details. | Tracked with `data.__adobe.target.mboxPageValue` in the `sendEvent` payload |
-->

## Eventos rastreados automaticamente

As seguintes metas de conversão não exigem ajustes específicos na sua implementação:

* Conversão > Visualizou uma página
* Conversão > Clicou em um elemento
* Engajamento > Exibições de página
* Engajamento > Tempo no site

>[!NOTE]
>
>O SDK da Web da Platform permite maior controle sobre os valores transmitidos na carga da solicitação. Para garantir que recursos do Target, como URLs de controle de qualidade e metas de conversão &quot;Visualizou uma página&quot;, funcionem corretamente, verifique se o valor `xdm.web.webPageDetails.URL` contém a URL da página inteira com a capitalização de caracteres adequada.

<!--
## Purchase conversion events

The following conversion goals are based on the order details information passed in the Platform Web SDK `sendEvent` payload:

* Revenue > Revenue per Visit (RPV)
* Revenue > Average Order Value (AOV)
* Revenue > Total Sales
* Revenue > Orders

Target at.js implementations typically use an order confirmation mbox with the `trackEvent()` or `sendNotifications()` functions to pass the order ID, order total, and a list of product IDs purchased. These methods are specific to Target.

The Platform Web SDK is a shared library for all Adobe applications and you may have other applications such as Adobe Analytics to consider. Because of this shared nature, its best send a single order confirmation call using the appropriate commerce XDM field group.

For more information and an example, refer to the tutorial section about [sending purchase parameters to Target](send-parameters.md#purchase-parameters). 
-->

## Eventos rastreados de forma personalizada

As implementações do Target geralmente usam eventos de conversão personalizados para rastrear cliques para atividades baseadas em formulário, para indicar uma conversão em um fluxo ou para transmitir parâmetros sem solicitar novo conteúdo.

A tabela abaixo descreve a abordagem da at.js e o equivalente do SDK da Web da Platform para alguns casos de uso comuns de rastreamento de conversão.

| Caso de uso | at.js 2.x do Target | SDK da Web da Platform |
|---|---|---|
| Rastrear um evento de conversão de cliques para um local da mbox (escopo) | Executar `trackEvent()` ou `sendNotifications()` com um valor `type` de `click` para um local de mbox específico | Executar um comando `sendEvent` com um tipo de evento de `decisioning.propositionInteract` |
| Rastrear um evento de conversão personalizado que também pode incluir dados adicionais, como parâmetros do perfil do Target | Executar `trackEvent()` ou `sendNotifications()` com um valor `type` de `display` para um local de mbox específico | Executar um comando `sendEvent` com um tipo de evento de `decisioning.propositionDisplay` |

>[!NOTE]
>
>Embora o `decisioning.propositionDisplay` seja usado com mais frequência para incrementar impressões para escopos específicos, ele também deve ser usado como um substituto direto do at.js `trackEvent()` normalmente. O padrão da função `trackEvent()` é um tipo de `display`, caso não seja especificado. Verifique sua implementação para garantir que você use o tipo de evento correto para quaisquer conversões personalizadas que possa ter definido.

Consulte a documentação dedicada da at.js para obter mais informações sobre como usar o [`trackEvent()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-trackevent/) e o [`sendNotifications()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21/) para rastrear eventos do Target.

Exemplo de at.js usando `trackEvent()` para rastrear um clique em um local da mbox:

```JavaScript
adobe.target.trackEvent({
  "type": "click",
  "mbox": "homepage_hero"
});
```

Com uma implementação do SDK da Web da Platform, é possível rastrear eventos e ações do usuário chamando o comando `sendEvent`, preenchendo o grupo de campos XDM `_experience.decisioning.propositions` e definindo `eventType` como um destes dois valores:

* `decisioning.propositionDisplay`: Sinaliza a renderização da atividade do Target.
* `decisioning.propositionInteract`: Sinaliza uma interação do usuário com a atividade, como um clique do mouse.

O grupo de campos XDM `_experience.decisioning.propositions` é uma matriz de objetos. As propriedades de cada objeto são derivadas do `result.propositions` que é retornado no comando `sendEvent`: `{ id, scope, scopeDetails }`

```JavaScript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];

        if (item.schema === "https://ns.adobe.com/personalization/measurement") {
          // add metric to the DOM element
          const button = document.getElementById("form-based-click-metric");

          button.addEventListener("click", event => {
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
            // send the click track event
            alloy("sendEvent", {
              "xdm": {
                "eventType": "decisioning.propositionInteract",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          });
        }
      }
    }
  }
});
```

Em seguida, saiba como [habilitar o compartilhamento de ID entre domínios](cross-domain.md) para obter perfis de visitante consistentes.

>[!NOTE]
>
>Estamos empenhados em ajudar você a ter sucesso com a migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=pt#M463).
