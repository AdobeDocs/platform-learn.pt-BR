---
title: Renderizar atividades do VEC - Migrar o Target da at.js 2.x para o SDK da Web
description: Saiba como recuperar e aplicar atividades do Visual Experience Composer com uma implementação de SDK da Web do Adobe Target.
exl-id: bbbbfada-e236-44de-a7bf-5c63ff840db4
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# Renderizar atividades do Adobe Target Visual Experience Composer (VEC)

As atividades do Target são configuradas usando o Visual Experience Composer (VEC) ou o compositor baseado em formulário. O SDK da Web da Platform pode recuperar e aplicar atividades baseadas em VEC na página, da mesma forma que a at.js. Nessa parte da migração, você deverá:

* Instalar a extensão de navegador Auxiliar de edição visual
* Execute uma chamada `sendEvent` com o SDK da Web da plataforma para solicitar atividades.
* Atualize todas as referências da implementação at.js que usam `getOffers()` para executar uma solicitação `pageLoad` do Target.

## Extensão de navegador Auxiliar de edição visual

A extensão de navegador da para Google Chrome, Auxiliar de edição visual do Adobe Experience Cloud, permite carregar sites de maneira confiável no Visual Experience Composer (VEC) do Adobe Target para criar e controlar a qualidade das experiências da web com mais rapidez.

A extensão de navegador Auxiliar de edição visual funciona com sites da Web que usam at.js ou SDK da Web da plataforma.

### Obter e instalar o Auxiliar de edição visual

1. Navegue até a [extensão de navegador Auxiliar de edição visual do Adobe Experience Cloud na Chrome Web Store](https://chrome.google.com/webstore/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca).
1. Clique em Adicionar ao **Chrome** > **Adicionar Extensão**.
1. Abra o VEC no Target.
1. Para usar a extensão, clique no ícone da extensão de navegador Auxiliar de edição visual ![ícone da extensão de edição visual](assets/VEC-Helper.png){zoomable="yes"} na barra de ferramentas do navegador Chrome no VEC ou no Modo de controle de qualidade.

O Auxiliar de edição visual é ativado automaticamente quando um site é aberto no VEC do Target para permitir a criação. A extensão não tem configurações condicionais. A extensão lida com todas as configurações automaticamente, incluindo as configurações de cookies SameSite.

Consulte a documentação dedicada para obter mais informações sobre a [extensão do Auxiliar de edição visual](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension.html?lang=pt-BR) e a [solução de problemas do Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/troubleshoot-composer.html?lang=pt-BR).

>[!IMPORTANT]
>
>A nova [extensão Auxiliar de Edição Visual](https://chrome.google.com/webstore/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca) substitui a [extensão de navegador Auxiliar do VEC do Target](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html?lang=pt-BR) anterior. Se a extensão auxiliar do VEC mais antiga estiver instalada, ela deverá ser removida ou desativada antes de usar a extensão auxiliar de edição visual.

## Solicitar e aplicar conteúdo automaticamente

Depois que o SDK da Web da Platform for configurado na página, você poderá solicitar conteúdo do Target. Ao contrário da at.js, que pode ser configurada para solicitar conteúdo automaticamente quando a biblioteca é carregada, o SDK da Web da Platform exige que você execute explicitamente um comando.

Se sua implementação do at.js tiver a configuração `pageLoadEnabled` definida como `true`, que habilita a renderização automática de atividades baseadas em VEC, você executará o seguinte comando `sendEvent` com o SDK da Web da plataforma:

>[!BEGINTABS]

>[!TAB JavaScript]

```Javascript
alloy("sendEvent", {
  "renderDecisions": true
});
```

>[!TAB Tags]

Nas marcas, use o tipo de ação [!UICONTROL Enviar evento] com a opção [!UICONTROL Renderizar decisões de personalização visual] selecionada:

![Enviar um evento com decisões de personalização visual de renderização selecionadas nas marcas](assets/vec-sendEvent-renderTrue.png){zoomable="yes"}

>[!ENDTABS]

<!--
When the Platform Web SDK renders an activity to the page with `renderDecisions` set to `true`, an additional notification call fires automatically to increment an impression and attribute the visitor to the activity. This call uses an event type with the value `decisioning.propositionDisplay`.

![Platform Web SDK call incrementing a Target impression](assets/target-impression-call.png){zoomable="yes"}
-->

## Solicitar e aplicar conteúdo sob demanda

Algumas implementações do Target exigem algum processamento personalizado de ofertas de VEC antes de aplicá-las à página. Ou solicitam vários locais em uma única chamada. Em uma implementação at.js, isso pode ser feito configurando `pageLoadEnabled` como `false` e usando a função `getOffers()` para executar uma solicitação `pageLoad`.

+++ Exemplo de at.js usando `getOffers()` e `applyOffers()` para renderizar manualmente atividades baseadas em VEC

```JavaScript
adobe.target.getOffers({
  request: {
    execute: {
      pageLoad: {}
    }
  }
}).
then(response => adobe.target.applyOffers({ response: response }));
```

+++

O SDK da Web da Platform não tem um evento `pageLoad` específico. Todas as solicitações de conteúdo do Target são controladas com a opção `decisionScopes` com o comando `sendEvent`. O escopo `__view__` atende à finalidade da solicitação `pageLoad`.

+++ Uma abordagem `sendEvent` equivalente do SDK da Web da plataforma:

1. Executar um comando `sendEvent` que inclua o escopo de decisão `__view__`
1. Aplicar o conteúdo retornado à página com o comando `applyPropositions`
1. Execute um comando `sendEvent` com o tipo de evento `decisioning.propositionDisplay` e detalhes de apresentação para incrementar uma impressão

```Javascript
alloy("sendEvent", {
  // Request the special "__view__" scope for target-global-mbox / pageLoad
  decisionScopes: ["__view__"]
}).then(function(result) {
  // Check if content (propositions) were returned
  if (result.propositions) {
    var retrievedPropositions = result.propositions;
    // Apply propositions to the page
    return alloy("applyPropositions", {
      propositions: retrievedPropositions
    }).then(function(applyPropositionsResult) {
      var renderedPropositions = applyPropositionsResult.propositions;
      // Send a display notification with the sendEvent command
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
  }
});
```

+++

>[!NOTE]
>
>É possível [renderizar manualmente as modificações](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=pt-BR#manually-rendering-content) feitas no Visual Experience Composer. A renderização manual de modificações baseadas em VEC não é comum. Verifique se a implementação da at.js usa a função `getOffers()` para executar manualmente uma solicitação do Target `pageLoad` sem usar `applyOffers()` para aplicar o conteúdo à página.

O SDK da Web da Platform oferece aos desenvolvedores muita flexibilidade na solicitação e renderização de conteúdo. Consulte a [documentação dedicada sobre renderização de conteúdo personalizado](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=pt-BR) para obter opções e detalhes adicionais.

## Exemplo de implementação

A implementação do SDK da Web da plataforma fundamental está concluída.

>[!BEGINTABS]

>[!TAB JavaScript]

Exemplo de JavaScript com renderização automática de conteúdo do Target:

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
  
  <!--Configure Platform Web SDK then send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    
    // Send an event to the Adobe edge network and render Target content automatically 
    alloy("sendEvent", {
      "renderDecisions": true
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


>[!TAB Tags]

Exemplo de página de tags com renderização automática de conteúdo do Target:


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

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

    <!--Tags Header Embed Code: REPLACE WITH THE INSTALL CODE FROM YOUR OWN ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
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

Nas tags, adicione a extensão SDK da Web da Adobe Experience Platform:

![Adicionar a extensão SDK da Web da Adobe Experience Platform](assets/library-tags-addExtension.png){zoomable="yes"}

Adicione as configurações desejadas:
![configurando as opções de migração da extensão de tag do SDK da Web](assets/tags-config-migration.png){zoomable="yes"}

Crie uma regra com uma ação [!UICONTROL Enviar evento] e [!UICONTROL Renderizar decisões de personalização visual] selecionadas:
![Enviar um evento com Personalizações de Renderização selecionadas nas marcas](assets/vec-sendEvent-renderTrue.png){zoomable="yes"}

>[!ENDTABS]

Em seguida, saiba como solicitar e [renderizar atividades do Target com base em formulário](render-form-based-activities.md).

>[!NOTE]
>
>Estamos empenhados em ajudar você a ter sucesso com a migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=pt#M463).
