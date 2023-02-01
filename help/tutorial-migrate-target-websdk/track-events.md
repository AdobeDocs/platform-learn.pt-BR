---
title: Rastrear eventos | Migrar o Target da at.js 2.x para o SDK da Web
description: Saiba como rastrear eventos de conversão do Adobe Target usando o Experience Platform Web SDK.
source-git-commit: 43740912bc5a941aa21c5f38ed2c1aac74abffbc
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 1%

---


# Rastrear eventos de conversão do Target usando o SDK da Web da plataforma

Os eventos de conversão do Target podem ser rastreados com o SDK da Web da plataforma semelhante à at.js. Os eventos de conversão geralmente se enquadram nas seguintes categorias:

* Eventos rastreados automaticamente que não exigem configuração
* Eventos de conversão de compra que devem ser ajustados para uma implementação de SDK da Web da plataforma de práticas recomendadas
* Eventos de conversão que não são de compra que exigem atualizações de código

>[!WARNING]
>
> As implementações do SDK da Web da plataforma iniciadas após 1º de outubro de 2022 podem precisar usar o [solução alternativa de pré-busca](prefetch-workaround.md) para rastrear com sucesso alguns dos eventos descritos nesta página.

## Comparação de metas do rastreamento

A tabela a seguir compara como o at.js e o SDK da Web da plataforma rastreiam eventos de conversão

| Objetivo da atividade | Target at.js 2.x | SDK da Web da Platform |
|---|---|---|
| Conversão > Visualização de uma página | Rastreado automaticamente. Com base no valor de `context.address.url` na carga da solicitação da at.js. | Rastreado automaticamente. Com base no valor de `xdm.web.webPageDetails.URL` no `sendEvent` carga |
| Conversão > Visualização de uma mbox | Rastreado com a solicitação de um local de mbox de exibição ou uma notificação usando `trackEvent()` ou `sendNotifications()` com um `type` valor de `display`. | Rastreado com um SDK da Web da plataforma `sendEvent` com a `eventType` de `decisioning.propositionDisplay`. |
| Conversão > Clicou em um elemento | Rastreado automaticamente para atividades baseadas em VEC. Aparece como uma chamada de rede da at.js com um `notifications` no conteúdo da solicitação e em um `type` valor de `click`. | Rastreado automaticamente para atividades baseadas em VEC. Aparece como um SDK da Web da plataforma `sendEvent` com a `eventType` de `decisioning.propositionInteract`. |
| Envolvimento > Visualizações de página | Rastreado automaticamente | Rastreado automaticamente |
| Envolvimento > Tempo no site | Rastreado automaticamente | Rastreado automaticamente |

<!--
| Revenue > RPV, AOV, or Total Sales | Tracked based on the `orderTotal` parameter values for the specified mbox(es) | Tracked based on the `xdm.commerce.order.priceTotal` values. Its best to use the "any mbox" option in the goal setup. |
| Revenue > Orders | Tracked based on the unique `orderId` parameter values for the specified mbox(es) | Tracked based on the unique values for `xdm.commerce.order.purchaseID`. Its best to use the "any mbox" option in the goal setup. |
| Engagement > Custom Scoring | Tracked with the `mboxPageValue` parameter. Refer to the [dedicated documentation](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html) for more details. | Tracked with `data.__adobe.target.mboxPageValue` in the `sendEvent` payload |
-->

## Eventos rastreados automaticamente

As seguintes metas de conversão não exigem ajustes específicos na implementação:

* Conversão > Visualização de uma página
* Conversão > Clicou em um elemento
* Envolvimento > Visualizações de página
* Envolvimento > Tempo no site

>[!NOTE]
>
>O SDK da Web da plataforma permite maior controle sobre os valores transmitidos na carga da solicitação. Para garantir que os recursos do Target, como URLs de controle de qualidade e metas de conversão &quot;Visualizada uma página&quot; funcionem corretamente, verifique se a variável `xdm.web.webPageDetails.URL` contém o URL de página completo com o caractere correto maiúsculo.

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

## Eventos rastreados pelo cliente

As implementações do Target normalmente usam eventos de conversão personalizados para rastrear cliques em atividades baseadas em formulário, para significar uma conversão em um fluxo ou para transmitir parâmetros sem solicitar novo conteúdo.

A tabela abaixo descreve a abordagem da at.js e o equivalente do SDK da Web da plataforma para alguns casos de uso comuns de rastreamento de conversão.

| Caso de uso | Target at.js 2.x | SDK da Web da Platform |
|---|---|---|
| Rastrear um evento de conversão de cliques para um local de mbox (escopo) | Executar `trackEvent()` ou `sendNotifications()` com um `type` valor de `click` para um local de mbox específico | Executar um `sendEvent` com um tipo de evento de `decisioning.propositionInteract` |
| Rastrear um evento de conversão personalizado que também possa incluir dados adicionais, como parâmetros de perfil do Target | Executar `trackEvent()` ou `sendNotifications()` com um `type` valor de `display` para um local de mbox específico | Executar um `sendEvent` com um tipo de evento de `decisioning.propositionDisplay` |

>[!NOTE]
>
>Embora `decisioning.propositionDisplay` O é usado com mais frequência para incrementar impressões para escopos específicos, também deve ser usado como uma substituição direta para a at.js `trackEvent()` geralmente. O `trackEvent()` O padrão da função é um tipo de `display` se não especificado. Verifique sua implementação para garantir que você use o tipo de evento correto para qualquer conversão personalizada que tenha sido definida.

Consulte a documentação dedicada da at.js para obter mais informações sobre como usar o [`trackEvent()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-trackevent/) e [`sendNotifications()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21/) para rastrear eventos do Target.

Exemplo de at.js usando `trackEvent()` para rastrear um clique em um local da mbox:

```JavaScript
adobe.target.trackEvent({
  "type": "click",
  "mbox": "homepage_hero"
});
```

Com uma implementação do SDK da Web da plataforma, é possível rastrear eventos e ações do usuário ao chamar a função `sendEvent` , preenchendo o `_experience.decisioning.propositions` Grupo de campos XDM e definição do `eventType` para um de dois valores:

* `decisioning.propositionDisplay`: Sinaliza a renderização da atividade do Target.
* `decisioning.propositionInteract`: Sinaliza uma interação do usuário com a atividade, como um clique do mouse.

O `_experience.decisioning.propositions` O grupo de campos XDM é uma matriz de objetos. As propriedades de cada objeto são derivadas da variável `result.propositions` que é retornado no `sendEvent` comando: `{ id, scope, scopeDetails }`

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

Em seguida, saiba como [habilitar o compartilhamento de ID entre domínios](cross-domain.md) para perfis de visitante consistentes.

>[!NOTE]
>
>Temos o compromisso de ajudar você a ser bem-sucedido com sua migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, informe-nos ao publicar em [este debate comunitário](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).