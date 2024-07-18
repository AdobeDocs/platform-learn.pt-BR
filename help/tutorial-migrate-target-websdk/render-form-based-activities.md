---
title: Migração do Target da at.js 2.x para o SDK da Web
description: Saiba como migrar uma implementação do Adobe Target da at.js 2.x para o Adobe Experience Platform Web SDK. Os tópicos incluem visão geral da biblioteca, diferenças de implementação e outras chamadas importantes.
exl-id: 43b9ae91-4524-4071-9eb4-12a0a8aec242
source-git-commit: 4690d41f92c83fe17eda588538d397ae1fa28af0
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 1%

---

# Renderizar atividades do Target que usam o compositor baseado em formulário

Algumas implementações do Target podem usar mboxes regionais (agora conhecidas como &quot;escopos&quot;) para fornecer conteúdo de atividades que usam o Experience Composer baseado em formulário. Se sua implementação do at.js Target usar mboxes, será necessário fazer o seguinte:

* Atualize todas as referências da implementação at.js que usam `getOffer()` ou `getOffers()` para os métodos equivalentes do SDK da Web da plataforma.
* Adicione o código para acionar um evento `propositionDisplay` de forma que uma impressão seja contada.

## Solicitar e aplicar conteúdo sob demanda

As atividades criadas usando o compositor baseado em formulário do Target e entregues a mboxes regionais não podem ser renderizadas automaticamente pelo SDK da Web da Platform. Semelhante à at.js, as ofertas entregues a locais específicos do Target precisam ser renderizadas sob demanda.


+++at.js Exemplo usando `getOffer()` e `applyOffer()`:

1. Executar `getOffer()` para solicitar uma oferta para uma localização
1. Executar `applyOffer()` para renderizar a oferta para um seletor especificado
1. Uma impressão de atividade é automaticamente incrementada no momento da solicitação `getOffer()`

```JavaScript
// Retrieve an offer for the homepage-hero location
adobe.target.getOffer({
  "mbox": "homepage_hero",

  // Render offer to the #hero-banner selector
  "success": function(offers) {
    adobe.target.applyOffer({
      "mbox": "homepage_hero",
      "selector": "#hero-banner",
      "offer": offers
    });
  },
  "error": {
    console.log(error);
  },
  "timeout": 3000
});
```

+++

+++SDK da Web da plataforma equivalente usando o comando `applyPropositions`:

1. Execute o comando `sendEvent` para solicitar ofertas (propostas) para um ou mais locais (escopos)
1. Execute o comando `applyPropositions` com o objeto de metadados que fornece instruções sobre como aplicar conteúdo à página para cada escopo
1. Execute o comando `sendEvent` com eventType de `decisioning.propositionDisplay` para rastrear uma impressão

```JavaScript
// Retrieve propositions for homepage_hero location (scope)
alloy("sendEvent", {
  "decisionScopes": ["homepage_hero"]
}).then(function(result) {
  var retrievedPropositions = result.propositions;
    
  // Render offer (proposition) to the #hero-banner selector by supplying extra metadata
  return alloy("applyPropositions", {
    "propositions": retrievedPropositions,
    "metadata": {
      // Specify each regional mbox or scope name along with a selector and actionType
      "homepage_hero": {
        "selector": "#hero-banner",
        "actionType": "setHtml"
      }
    }
  }).then(function(applyPropositionsResult) {
    var renderedPropositions = applyPropositionsResult.propositions;

    // Send the display notifications via sendEvent command
    alloy("sendEvent", {
      "xdm": {
        "eventType": "decisioning.propositionDisplay",
        "_experience": {
          "decisioning": {
            "propositions": renderedPropositions
          }
        }
      }
    });
  });
});
```

+++

O SDK da Web da Platform oferece maior controle para aplicar atividades baseadas em formulário à página usando o comando `applyPropositions` com um `actionType` especificado:

| `actionType` | Descrição | at.js `applyOffer()` | SDK da Web da plataforma `applyPropositions` |
| --- | --- | --- | --- |
| `setHtml` | Limpe o conteúdo do contêiner e adicione a oferta ao contêiner | Sim (sempre usado) | Sim |
| `replaceHtml` | Remover o contêiner e substituí-lo pela oferta | Não | Sim |
| `appendHtml` | Acrescenta a oferta após o seletor especificado | Não | Sim |

Consulte a [documentação dedicada](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html) sobre renderização de conteúdo usando o SDK da Web da plataforma para obter opções de renderização adicionais e exemplos.

## Exemplo de implementação

A página de exemplo abaixo se baseia na implementação descrita na seção anterior, apenas adiciona escopos adicionais ao comando `sendEvent`.

+++Exemplo de SDK da Web da Platform com vários escopos

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>

  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>

  <!--Prehiding snippet for Target with asynchronous deployment-->
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
  
  <!--Configure Platform Web SDK then send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    alloy("sendEvent", {
      // Request and render VEC-based activities
      "renderDecisions": true,
      // Request content for form-based activities using the "homepage_hero" scope
      "decisionScopes": ["homepage_hero"]
    }).then(function(result) {
      var retrievedPropositions = result.propositions;
        
      // Render offer (proposition) to the #hero-banner selector by supplying extra metadata
      return alloy("applyPropositions", {
        "propositions": retrievedPropositions,
        "metadata": {
          // Specify each regional mbox or scope name along with a selector and actionType
          "homepage_hero": {
            "selector": "#hero-banner",
            "actionType": "setHtml"
          }
        }
      }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
        alloy("sendEvent", {
          "xdm": {
            "eventType": "decisioning.propositionDisplay",
            "_experience": {
              "decisioning": {
                "propositions": renderedPropositions
              }
            }
          }
        });
      });
    });
  </script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div id="homepage-hero">Homepage Hero Banner Content</div>
</body>
</html>
```

Em seguida, saiba como [passar parâmetros do Target usando o SDK da Web da plataforma](send-parameters.md).

>[!NOTE]
>
>Estamos empenhados em ajudar você a ter sucesso com a migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
