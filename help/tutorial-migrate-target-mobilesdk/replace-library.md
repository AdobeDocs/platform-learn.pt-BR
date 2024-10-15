---
title: Substituir a biblioteca - Migrar o Target da at.js 2.x para o SDK da Web
description: Saiba como migrar uma implementação do Adobe Target da at.js 2.x para o Adobe Experience Platform Web SDK. Os tópicos incluem visão geral da biblioteca, diferenças de implementação e outras chamadas importantes.
source-git-commit: 009548969b88d1bfa6eac23f65b1ca2144f27c34
workflow-type: tm+mt
source-wordcount: '1560'
ht-degree: 1%

---

# Substituir a biblioteca da at.js pelo SDK da Web da plataforma

Saiba como substituir sua implementação do Adobe Target na página para migrar da at.js para o SDK da Web da plataforma. Uma substituição básica consiste nas seguintes etapas:

* Revise suas configurações de administração do Target e anote a ID da organização de IMS
* Substituir a biblioteca at.js pelo SDK da Web da plataforma
* Atualizar o trecho pré-ocultação para implementações de biblioteca síncronas
* Configurar o SDK da Web da plataforma

>[!NOTE]
>
>Os exemplos fornecidos são para fins ilustrativos e a implementação real do Target pode variar. Se sua implementação do Target existente usar o gerenciador de tags da Coleção de dados do Adobe, você também pode consultar o [tutorial de implementação do Target do SDK da Web da plataforma](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html) para obter mais informações.


## Revisar configurações de administração do Target

A primeira etapa para migrar do Target para o SDK da Web da Platform é revisar suas configurações na seção **[!UICONTROL Administração]** da interface do Target.

### [!UICONTROL Implementação]

#### [!UICONTROL Detalhes da conta]

* **[!UICONTROL IMS Organization Id]** - Anote esse valor, pois ele é necessário para configurar o SDK da Web da Platform.
* **[!UICONTROL Decisão no dispositivo]** - este recurso não tem suporte do SDK da Web da plataforma. Essa configuração pode ser desativada após a migração e se você não usar mais a at.js em nenhum de seus sites ou se não tiver casos de uso do lado do servidor para a Decisão no dispositivo.

#### [!UICONTROL Métodos de implementação]

Todas as configurações editáveis na seção **[!UICONTROL Métodos de implementação]** se aplicam somente à at.js. Essas configurações são usadas para gerar uma biblioteca at.js personalizada para sua implementação. Revise essas configurações para verificar se você tem algum código personalizado ou está configurando cookies próprios e de terceiros para casos de uso entre domínios.

A configuração **[!UICONTROL Duração do Perfil]** só pode ser alterada pelo Atendimento ao cliente do Adobe. A duração do perfil do visitante do Target não é afetada pela sua abordagem de implementação. A at.js e o SDK da Web da Platform usam a mesma duração do perfil do visitante.

#### [!UICONTROL Privacidade]

* **[!UICONTROL Ofuscar endereços IP de visitantes]** - Essa configuração afeta os recursos de geolocalização. A at.js e o SDK da Web da Platform usam as mesmas configurações de ofuscação de IP de back-end para fins de geolocalização.

### [!UICONTROL Ambientes]

O SDK da Web da Platform usa uma configuração de sequência de dados que permite definir explicitamente uma [!UICONTROL ID de Ambiente] para sequências de dados separadas de desenvolvimento, preparo e produção. O principal caso de uso dessa configuração é para implementações de aplicativos móveis em que os URLs não existem para distinguir ambientes facilmente. A configuração é opcional, mas pode ser usada para garantir que todas as solicitações sejam associadas corretamente ao ambiente especificado. Isso é diferente de uma implementação da at.js na qual você deve atribuir ambientes do Target com base em domínios e regras de grupo de hosts.

>[!NOTE]
>
>Se uma ID de ambiente não for especificada na configuração da sequência de dados, o Target usará o mapeamento de domínio para ambiente conforme especificado na seção **Hosts**.

Para obter mais informações, consulte o guia [configuração da sequência de dados](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) e a documentação dos [Hosts](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=pt-BR) do Target.

## Implantar o SDK da Web da plataforma

A funcionalidade do Target é fornecida pela at.js e pelo SDK da Web da plataforma. Se ambas as bibliotecas forem usadas ao mesmo tempo, você poderá enfrentar problemas de renderização e rastreamento. Para migrar com sucesso para o SDK da Web da Platform, a primeira etapa é remover a at.js e substituí-la pelo SDK da Web da Platform (alloy.js).

Assuma uma implementação simples do Target com a at.js:

* Uma camada de dados próxima à parte superior da página fornece informações para o Target e outros aplicativos
* Uma ou mais bibliotecas auxiliares de terceiros cujos recursos podem ser usados em atividades do Target (por exemplo, jQuery)
* Um trecho pré-ocultação para atenuar a cintilação
* A biblioteca at.js do Target é carregada de forma assíncrona com configurações padrão para solicitar e renderizar atividades automaticamente:

+++at.js exemplo de implementação em uma página de HTML

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
  <!--prehiding snippet for Target with asynchronous deployment-->
  <script>
    ;(function(win, doc, style, timeout) {
      var STYLE_ID = 'at-body-style';

      function getParent() {
        return doc.getElementsByTagName('head')[0];
      }

      function addStyle(parent, id, def) {
        if (!parent) {
          return;
        }
        var style = doc.createElement('style');
        style.id = id;
        style.innerHTML = def;
        parent.appendChild(style);
      }

      function removeStyle(parent, id) {
        if (!parent) {
          return;
        }
        var style = doc.getElementById(id);
        if (!style) {
          return;
        }
        parent.removeChild(style);
      }
      addStyle(getParent(), STYLE_ID, style);
      setTimeout(function() {
        removeStyle(getParent(), STYLE_ID);
      }, timeout);
    }(window, document, "body {opacity: 0 !important}", 3000));
  </script>
  <!--Target at.js library loaded asynchonously-->
  <script src="/libraries/at.js" async></script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div>Homepage Hero Banner Content</div>
</body>
</html>
```

+++

Para atualizar o Target para usar o SDK da Web da plataforma, remova primeiro a at.js:

```HTML
<!--Target at.js library loaded asynchonously-->
<script src="/libraries/at.js" async></script>
```

E substitua pela biblioteca JavaScript ligada ou pelo código incorporado das tags e pela extensão SDK da Web da Adobe Experience Platform:

>[!BEGINTABS]

>[!TAB JavaScript]

```HTML
<!--Platform Web SDK base code-->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
<script src="https://cdn1.adoberesources.net/alloy/2.13.1/alloy.min.js" async></script>
```

>[!TAB Tags]

```HTML
<!--Tags Header Embed Code: REPLACE WITH THE INSTALL CODE FROM YOUR OWN ENVIRONMENT-->
<script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
```

Na propriedade da tag, adicione a extensão SDK da Web da Adobe Experience Platform:

<!--![Add the Adobe Experience Platform Web SDK extension](assets/library-tags-addExtension.png){zoomable="yes"}-->


>[!ENDTABS]

A versão independente pré-criada requer um &quot;código base&quot; adicionado diretamente à página que cria uma função global chamada liga. Use esta função para interagir com o SDK. Se você quiser nomear a função global como algo diferente, altere o nome `alloy`.

Consulte a documentação [Instalação do SDK da Web da Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html) para obter detalhes adicionais e opções de implantação.


## Atualizar a abordagem de pré-ocultação de conteúdo

A implementação do SDK da Web da Platform pode exigir um trecho pré-ocultado, dependendo se a biblioteca é carregada de forma assíncrona ou síncrona.

### Implementação assíncrona

Assim como na at.js, se a biblioteca do SDK da Web da Platform for carregada de forma assíncrona, a página poderá terminar a renderização antes que o Target tenha realizado uma troca de conteúdo. Esse comportamento pode levar ao que é conhecido como &quot;oscilação&quot;, onde o conteúdo padrão é exibido brevemente antes de ser substituído pelo conteúdo personalizado especificado pelo Target. Caso deseje evitar essa oscilação, o Adobe recomenda adicionar um trecho pré-ocultação especial imediatamente antes da referência de script do SDK da Web da plataforma assíncrona ou do código incorporado das tags.

Se sua implementação for assíncrona como os exemplos acima, substitua o trecho pré-ocultação da at.js pela versão abaixo compatível com o SDK da Web da plataforma:

```HTML
<!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
<script>
  !function(e,a,n,t){var i=e.head;if(i){
  if (a) return;
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("mboxEdit") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

O trecho pré-ocultação cria uma tag de estilo no cabeçalho da página com a definição CSS de sua escolha. Essa tag de estilo é removida quando uma resposta do Target é recebida ou o tempo limite é atingido.

O comportamento de pré-ocultação é controlado por duas configurações no final do trecho.

* `body { opacity: 0 !important }` especifica a definição de CSS a ser usada para a pré-ocultação até o Target ser carregado. Por padrão, a página inteira fica oculta. É possível atualizar essa definição para os seletores que você deseja pré-ocultar junto com a forma como deseja ocultá-los. É possível incluir várias definições, pois esse valor é simplesmente o que está inserido na tag de estilo pré-ocultação. Se você tiver um elemento de contêiner de fácil identificação que abranja o conteúdo abaixo de sua navegação, poderá usar essa configuração para limitar a pré-ocultação a esse elemento do contêiner.

* `3000` especifica o tempo limite em milissegundos para a pré-ocultação. Se uma resposta do Target não for recebida antes do tempo limite, a tag de estilo pré-ocultação será removida. Atingir esse tempo limite deve ser raro.

>[!IMPORTANT]
>
>Certifique-se de usar o trecho correto para o SDK da Web da Platform, pois ele usa uma ID de estilo diferente de `alloy-prehiding`. Se o trecho pré-ocultação para at.js for usado, talvez ele não funcione corretamente.

### Implementação síncrona

A Adobe recomenda implementar o SDK da Web da Platform de forma assíncrona para obter o melhor desempenho geral da página. No entanto, se a biblioteca alloy.js ou o código incorporado das tags for carregado de forma síncrona, o trecho pré-ocultação não será necessário. Em vez disso, o estilo pré-ocultação é especificado na configuração do SDK da Web da Platform.

O estilo pré-ocultação para implementações síncronas pode ser configurado usando a opção [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle). A configuração do SDK da Web da Platform é abordada na próxima seção.

Para saber mais sobre como o SDK da Web da Platform pode gerenciar a cintilação, consulte a seção do guia: [gerenciamento de cintilação para experiências personalizadas](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/manage-flicker.html)

## Configurar o SDK da Web da plataforma

O SDK da Web da Platform deve ser configurado em cada carregamento de página. O exemplo a seguir presume que todo o site está sendo atualizado para o SDK da Web da plataforma em uma única implantação:

>[!BEGINTABS]

>[!TAB JavaScript]

O comando `configure` deve ser sempre o primeiro comando do SDK chamado. O `edgeConfigId` é a [!UICONTROL ID da sequência de dados]

```JavaScript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

>[!TAB Tags]

Em implementações de tags, muitos campos são preenchidos automaticamente ou podem ser selecionados em menus suspensos. Observe que diferentes [!UICONTROL sandboxes] e [!UICONTROL datastreams] da Platform podem ser selecionadas para cada ambiente. O fluxo de dados será alterado com base no estado da biblioteca de tags no processo de publicação.

<!--![configuring the Web SDK tag extension](assets/tags-config.png){zoomable="yes"}-->
>[!ENDTABS]

Se você planeja migrar do at.js para o SDK da Web da Platform página por página, as seguintes opções de configuração são necessárias:


>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled":true,
  "idMigrationEnabled":true
});
```

>[!TAB Tags]

<!--![configuring the Web SDK tag extension migration options](assets/tags-config-migration.png){zoomable="yes"}-->

>[!ENDTABS]

As opções de configuração notáveis relacionadas ao Target são descritas abaixo:

| Opção | Descrição | Exemplo de valor |
| --- | --- | --- |
| `edgeConfigId` | A ID do fluxo de dados | `ebebf826-a01f-4458-8cec-ef61de241c93` |
| `orgId` | ID da organização da Adobe Experience Cloud | `ADB3LETTERSANDNUMBERS@AdobeOrg` |
| `targetMigrationEnabled` | Use essa opção para permitir que o SDK da Web leia e grave os cookies mbox e mboxEdgeCluster herdados usados pela at.js. Isso ajuda a manter o perfil do visitante ao mover de uma página que usa o SDK da Web para uma página que usa a biblioteca at.js e o oposto. | `true` |
| `idMigrationEnabled` | Se verdadeiro, o SDK lê e define cookies AMCV antigos. Essa opção ajuda na transição para o uso do SDK da Web da Platform, enquanto algumas partes do site ainda podem usar Visitor.js. | `true` |
| `thirdPartyCookiesEnabled` | Ativa a configuração de cookies de terceiros do Adobe. O SDK pode manter a ID de visitante em um contexto de terceiros para permitir que a mesma ID de visitante seja usada em todos os sites. Use essa opção se você tiver vários sites; no entanto, às vezes essa opção não é desejada por motivos de privacidade. | `true` |
| `prehidingStyle` | Usado para criar uma definição de estilo CSS que oculta as áreas de conteúdo da sua página da Web enquanto o conteúdo personalizado é carregado do servidor. Isso só é usado com implantações síncronas do SDK. | `body { opacity: 0 !important }` |

Para obter uma lista completa de opções, consulte o guia [configurando o SDK da Web da plataforma](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html).

## Exemplo de implementação

Depois que o SDK da Web da Platform estiver corretamente em vigor, a página de exemplo terá esta aparência.

>[!BEGINTABS]

>[!TAB JavaScript]

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
  <script src="https://cdn1.adoberesources.net/alloy/2.13.1/alloy.min.js" async></script>
  
  <!--Configure Platform Web SDK-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
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

Código da página:

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

<!--![Add the Adobe Experience Platform Web SDK extension](assets/library-tags-addExtension.png){zoomable="yes"}-->

E adicione as configurações desejadas:
<!--![configuring the Web SDK tag extension migration options](assets/tags-config-migration.png){zoomable="yes"}-->


>[!ENDTABS]



É importante observar que simplesmente incluir e configurar a biblioteca do SDK da Web da plataforma, como mostrado acima, não executa nenhuma chamada de rede para a rede da Adobe Edge.

Em seguida, saiba como [solicitar e aplicar atividades baseadas em formulário](render-activities.md) à página.

>[!NOTE]
>
>Estamos empenhados em ajudá-lo a ser bem-sucedido na migração para dispositivos móveis do Target da extensão do Target para a extensão do Otimize. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
