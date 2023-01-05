---
title: Renderizar atividades do VEC | Migrar o Target da at.js 2.x para o SDK da Web
description: Saiba como recuperar e aplicar atividades do visual experience composer com uma implementação do SDK da Web do Adobe Target.
feature: Visual Experience Composer (VEC),Implement Client-side,APIs/SDKs,at.js,AEP Web SDK, Web SDK,Implementation
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 8%

---

# Renderizar atividades do Adobe Target Visual Experience Composer (VEC)

As atividades do Target são configuradas usando o Visual Experience Composer (VEC) ou o compositor baseado em formulário. O SDK da Web da plataforma pode recuperar e aplicar atividades baseadas em VEC na página, exatamente como a at.js. Para essa parte da migração, você:

* Instale a extensão de navegador do Visual Editing Helper, se necessário
* Executar um `sendEvent` chame com o SDK da Web da plataforma para solicitar atividades.
* Atualizar quaisquer referências da implementação da at.js que usam `getOffers()` para executar um Target `pageLoad` solicitação.

## Extensão do navegador do Visual Editing Helper

A extensão do navegador Adobe Experience Cloud Visual Editing Helper para Google Chrome permite carregar sites de maneira confiável no Adobe Target Visual Experience Composer (VEC) para criar e controlar a qualidade das experiências da Web com rapidez.

A extensão do navegador do assistente do Visual Editing funciona com sites que usam at.js ou SDK da Web da plataforma.

>[!IMPORTANT]
>
>A nova extensão do Visual Editing Helper substitui a anterior [Extensão de navegador do Target VEC Helper](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html). Se a extensão VEC Helper mais antiga estiver instalada, ela deverá ser removida ou desativada antes de usar a extensão Visual Editing Helper.

### Obter e instalar o Visual Editing Helper

1. Navegue até o [Extensão de navegador Adobe Experience Cloud Visual Editing Helper na Chrome Web Store](https://chrome.google.com/webstore/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca).
1. Clique em Adicionar a **Cromo** > **Adicionar extensão**.
1. Abra o VEC no Target.
1. Para usar a extensão, clique no ícone de extensão do navegador do Visual Editing Helper ![Ícone da extensão de edição visual](assets/VEC-Helper.png) na barra de ferramentas do navegador Chrome, no VEC ou no Modo de QA.

O Auxiliar de edição visual é ativado automaticamente quando um site é aberto no VEC do Target para permitir a criação. A extensão não tem configurações condicionais. A extensão lida com todas as configurações automaticamente, incluindo as configurações de cookies SameSite.

Consulte a documentação dedicada para obter mais informações sobre o [Extensão do Visual Editing Helper](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension.html) e [solução de problemas do Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/troubleshoot-composer.html).

## Solicitar e aplicar conteúdo automaticamente

Depois que o SDK da Web da plataforma é configurado na página, você pode solicitar conteúdo do Target. Ao contrário da at.js, que pode ser configurada para solicitar conteúdo automaticamente quando a biblioteca for carregada, o SDK da Web da plataforma exige que você execute um comando explicitamente.

Se sua implementação da at.js tiver o `pageLoadEnabled` definir como `true` que permite a renderização automática de atividades baseadas em VEC, você executaria o seguinte `sendEvent` com o SDK da Web da plataforma:

```Javascript
alloy("sendEvent", {
  "renderDecisions": true
});
```

>[!TIP]
>
> Ao usar o recurso de tags (antigo Launch) para implementar o SDK da Web, os comandos &#39;sendEvent&#39; para atividades do VEC podem ser implementados em uma regra usando o [!UICONTROL Enviar evento] tipo de ação com a [!UICONTROL Renderizar decisões de personalização visual] opção selecionada.

Quando o SDK da Web da plataforma renderiza uma atividade para a página com `renderDecisions` defina como `true`, uma chamada de notificação adicional é acionada automaticamente para incrementar uma impressão e atribuir o visitante à atividade. Essa chamada usa um tipo de evento com o valor `decisioning.propositionDisplay`.

![Chamada de SDK da Web da plataforma que aumenta uma impressão do Target](assets/target-impression-call.png)

## Solicitar e aplicar conteúdo sob demanda

Algumas implementações da at.js do Target podem ter `pageLoadEnabled` defina como `false` em vez disso, use o `getOffers()` para executar uma `pageLoad` solicitação. Esse tipo de configuração é usado se sua implementação requer processamento adicional da variável `getOffers()` antes de aplicar conteúdo à página ou para solicitar conteúdo para vários locais em uma única chamada.

O código a seguir usa `getOffers()` e `applyOffers()` para aplicar atividades baseadas em VEC sob demanda em vez de automaticamente ao carregar a biblioteca.

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

O SDK da Web da plataforma não tem um `pageLoad` evento. Todas as solicitações de conteúdo do Target são controladas com a variável `decisionScopes` com a opção `sendEvent` comando. O `__view__` o âmbito de aplicação `pageLoad` solicitação. Um SDK da Web da plataforma equivalente `sendEvent` A abordagem seria:

1. Executar um `sendEvent` que inclui o comando `__view__` escopo de decisão
1. Aplique o conteúdo retornado à página com a variável `applyPropositions` comando
1. Executar um `sendEvent` com o `decisioning.propositionDisplay` tipo de evento e detalhes da apresentação para incrementar uma impressão

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

>[!NOTE]
>
>É possível [renderizar manualmente modificações](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) criado no Visual Experience Composer. A renderização manual de modificações com base em VEC não é comum. Verifique se a implementação da at.js usa a variável `getOffers()` para executar manualmente um Target `pageLoad` solicitação sem usar `applyOffers()` para aplicar o conteúdo à página.

O SDK da Web da plataforma oferece aos desenvolvedores uma grande flexibilidade na solicitação e renderização de conteúdo. Consulte a [documentação dedicada sobre a renderização de conteúdo personalizado](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html) para obter mais opções e detalhes.

## Exemplo de implementação

A implementação do SDK da Web da plataforma fundamental está concluída. Nossa página de exemplo básica com a renderização automática de conteúdo do Target ativada deve ser semelhante a:

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

>[!TIP]
>
> Ao usar o recurso de tags (antigo Launch) para implementar o SDK da Web, o código de inserção de tags substitui as seções &quot;Código base do SDK da Web da plataforma&quot;, &quot;SDK da Web da plataforma carregado de forma assíncrona&quot; e &quot;Configurar SDK da Web da plataforma&quot; acima. O comando &#39;sendEvent&#39; é feito em uma regra usando o [!UICONTROL Enviar evento] tipo de ação com a [!UICONTROL Renderizar decisões de personalização visual] opção selecionada.

## Criação de atividades com a extensão do navegador do assistente do Visual Editing

A extensão do navegador Adobe Experience Cloud Visual Editing Helper para Google Chrome permite carregar sites de maneira confiável no Adobe Target Visual Experience Composer (VEC) para criar e controlar a qualidade das experiências da Web com rapidez.

A extensão do navegador do assistente do Visual Editing funciona com sites que usam at.js ou SDK da Web da plataforma.

>[!IMPORTANT]
>
>A nova extensão do Visual Editing Helper substitui a anterior [Extensão de navegador do Target VEC Helper](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html). Se a extensão VEC Helper mais antiga estiver instalada, ela deverá ser removida ou desativada antes de usar a extensão Visual Editing Helper.

### Obter e instalar o Visual Editing Helper

1. Navegue até o [Extensão de navegador Adobe Experience Cloud Visual Editing Helper na Chrome Web Store](https://chrome.google.com/webstore/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca).
1. Clique em Adicionar a **Cromo** > **Adicionar extensão**.
1. Abra o VEC no Target.
1. Para usar a extensão, clique no ícone da extensão de navegador Auxiliar de edição visual (ícone da extensão de edição visual) na barra de ferramentas do Chrome no VEC ou no modo de controle de qualidade.

O Visual Editing Helper é ativado automaticamente quando um site é aberto no VEC do Target para oferecer suporte à criação. A extensão não tem configurações condicionais. A extensão lida com todas as configurações automaticamente, incluindo as configurações de cookies SameSite.

Consulte a documentação dedicada para obter mais informações sobre o [Extensão do Visual Editing Helper](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension.html) e [solução de problemas do Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/troubleshoot-composer.html).

Em seguida, saiba como solicitar e [renderizar atividades do Target baseadas em formulário](render-form-based-activities.md).

>[!NOTE]
>
>Temos o compromisso de ajudar você a ser bem-sucedido com sua migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, informe-nos ao publicar em [este debate comunitário](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
