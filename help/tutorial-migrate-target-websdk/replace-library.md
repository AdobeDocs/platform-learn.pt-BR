---
title: Substituir a biblioteca | Migrar o Target da at.js 2.x para o SDK da Web
description: Saiba como migrar uma implementação do Adobe Target da at.js 2.x para o Adobe Experience Platform Web SDK. Os tópicos incluem visão geral da biblioteca, diferenças de implementação e outras chamadas importantes.
source-git-commit: ac5cee1888b39e5ba0134c850c378737e142f1d4
workflow-type: tm+mt
source-wordcount: '1654'
ht-degree: 1%

---

# Substitua a biblioteca at.js pelo SDK da Web da plataforma

Saiba como substituir sua implementação na página do Adobe Target para migrar da at.js para o SDK da Web da plataforma. Uma substituição básica consiste nas seguintes etapas:

* Revise as configurações de administração do Target e anote a IMS Organization ID
* Substitua a biblioteca at.js pelo SDK da Web da plataforma
* Atualizar o trecho pré-ocultação para implementações de biblioteca síncrona
* Configurar o SDK da Web da plataforma

>[!NOTE]
>
>Os exemplos fornecidos são para fins ilustrativos e sua implementação real do Target pode variar. Se sua implementação existente do Target usar o gerenciador de tags da Coleta de dados do Adobe, você também poderá consultar [Tutorial de implementação do Platform Web SDK do Target](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html) para obter mais informações.


## Revisar as configurações de administração do Target

A primeira etapa para migrar o Target para o SDK da Web da plataforma é revisar suas configurações no **[!UICONTROL Administração]** seção.

### [!UICONTROL Implementação]

#### [!UICONTROL Detalhes da conta]

* **[!UICONTROL ID da organização IMS]** - Anote esse valor, pois é necessário configurar o SDK da Web da plataforma.
* **[!UICONTROL Decisão no dispositivo]** - Esse recurso não é compatível com o SDK da Web da plataforma. Essa configuração pode ser desativada após a migração e se não usar mais a at.js em nenhum de seus sites da Web ou se tiver nenhum caso de uso do lado do servidor para o On-Device Decisioning.

#### [!UICONTROL Métodos de implementação]

Todas as configurações editáveis no **[!UICONTROL Métodos de implementação]** aplicar somente a at.js. Essas configurações são usadas para gerar uma biblioteca at.js personalizada para sua implementação. Revise essas configurações para verificar se você tem algum código personalizado ou está configurando cookies próprios e de terceiros para casos de uso entre domínios.

O **[!UICONTROL Duração do perfil]** só pode ser alterada pelo Adobe Customer Care. A duração do perfil do visitante do Target não é afetada pela sua abordagem de implementação. A at.js e o SDK da Web da plataforma usam a mesma duração do perfil do visitante.

#### [!UICONTROL Privacidade]

* **[!UICONTROL Ofuscar endereços IP do visitante]** - Essa configuração afeta os recursos de geolocalização. A at.js e o SDK da Web da plataforma usam as mesmas configurações de ofuscação de IP de backend para fins de geolocalização.

### [!UICONTROL Ambientes]

O SDK da Web da plataforma usa uma configuração de conjunto de dados que permite definir explicitamente um [!UICONTROL ID do ambiente] para desenvolvimento, armazenamento temporário e produção separados. O principal caso de uso dessa configuração é para implementações de aplicativos móveis em que URLs não existem para distinguir ambientes facilmente. A configuração é opcional, mas pode ser usada para garantir que todas as solicitações estejam associadas corretamente ao ambiente especificado. Isso é diferente de uma implementação da at.js, na qual você deve atribuir ambientes Target com base em domínios e regras de grupo de hosts.

>[!NOTE]
>
>Se uma ID de ambiente não for especificada na configuração do conjunto de dados, o Target usará o mapeamento de domínio para ambiente conforme especificado na variável **Hosts** seção.

Para obter mais informações, consulte [configuração do datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) guia e Target [Hosts](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) documentação.

## Implantar o SDK da Web da plataforma

A funcionalidade do Target é fornecida pela at.js e pelo SDK da Web da plataforma. Se ambas as bibliotecas forem usadas ao mesmo tempo, você poderá enfrentar problemas de renderização e rastreamento. Para migrar com êxito para o SDK da Web da plataforma, a primeira etapa é remover a at.js e substituí-la pelo SDK da Web da plataforma (alloy.js).

Considere uma implementação simples do Target com a at.js:

* Uma camada de dados próxima à parte superior da página fornece informações para o Target e outros aplicativos
* Uma ou mais bibliotecas auxiliares de terceiros cujos recursos podem ser usados em atividades do Target (por exemplo, jQuery)
* Um trecho pré-ocultado para atenuar a cintilação
* A biblioteca at.js do Target é carregada de forma assíncrona com as configurações padrão para solicitar e renderizar atividades automaticamente:

Implementação de exemplo de +++at.js em uma página HTML

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

Para atualizar o Target para usar o SDK da Web da plataforma, primeiro remova a at.js:

```HTML
<!--Target at.js library loaded asynchonously-->
<script src="/libraries/at.js" async></script>
```

E substitua por uma biblioteca JavsScript liga ou seu código incorporado de tags e a extensão Adobe Experience Platform Web SDK:

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

Na propriedade da tag , adicione a extensão SDK da Web da Adobe Experience Platform:

![Adicionar a extensão Adobe Experience Platform Web SDK](assets/library-tags-addExtension.png){zoomable=&quot;yes&quot;}


>[!ENDTABS]

A versão independente pré-criada requer um &quot;código base&quot; adicionado diretamente à página, o que cria uma função global chamada liga. Use essa função para interagir com o SDK. Se quiser nomear a função global como outra coisa, altere a variável `alloy` nome.

Consulte a [Instalação do SDK da Web da plataforma](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=pt-BR) documentação para obter detalhes adicionais e opções de implantação.


## Atualizar a abordagem de pré-ocultação de conteúdo

A implementação do SDK da Web da plataforma pode exigir uma pré-ocultação do trecho, dependendo se a biblioteca é carregada de forma assíncrona ou síncrona.

### Implementação assíncrona

Assim como com a at.js, se a biblioteca do SDK da Web da plataforma carregar de forma assíncrona, a página poderá terminar a renderização antes que o Target tenha realizado uma troca de conteúdo. Esse comportamento pode levar ao que é conhecido como &quot;oscilação&quot;, onde o conteúdo padrão é exibido brevemente antes de ser substituído pelo conteúdo personalizado especificado pelo Target. Se quiser evitar essa oscilação, o Adobe recomenda adicionar um trecho pré-ocultação especial imediatamente antes da referência do script assíncrono do SDK da Web da Plataforma ou do código incorporado das tags.

Se sua implementação for assíncrona como os exemplos acima, substitua o trecho pré-ocultação da at.js pela versão abaixo compatível com o SDK da Web da plataforma:

```HTML
<!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
<script>
  !function(e,a,n,t){var i=e.head;if(i){
  if (a) return;
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
</script>
```

O trecho pré-ocultação cria uma tag de estilo no cabeçalho da página com a definição de CSS de sua escolha. Essa tag de estilo é removida quando uma resposta do Target é recebida ou o tempo limite é atingido.

O comportamento de pré-ocultação é controlado por duas configurações no final do trecho.

* `body { opacity: 0 !important }` especifica a definição de CSS a ser usada para a pré-ocultação até o Target ser carregado. Por padrão, a página inteira está oculta. Você pode atualizar essa definição para os seletores que deseja visualizar junto com como deseja ocultá-los. É possível incluir várias definições, pois esse valor é simplesmente o que é inserido na tag de estilo de pré-ocultação. Se você tiver um elemento de contêiner de fácil identificação que abranja o conteúdo sob sua navegação, poderá usar essa configuração para limitar a pré-ocultação a esse elemento do contêiner.

* `3000` especifica o tempo limite em milissegundos para a pré-ocultação. Se uma resposta do Target não for recebida antes do tempo limite, a tag de estilo de pré-ocultação será removida. Atingir este tempo limite deve ser raro.

>[!IMPORTANT]
>
>Certifique-se de usar o trecho correto para o SDK da Web da plataforma, pois ele usa uma ID de estilo diferente de `alloy-prehiding`. Se o trecho pré-ocultação para at.js for usado, talvez não funcione corretamente.

### Implementação síncrona

O Adobe recomenda implementar o SDK da Web da plataforma de forma assíncrona para obter o melhor desempenho geral da página. No entanto, se a biblioteca ou código incorporado de tags do alloy.js for carregado de forma síncrona, o trecho pré-ocultação não será necessário. Em vez disso, o estilo de pré-ocultação é especificado na configuração do SDK da Web da plataforma.

O estilo de pré-ocultação para implementações síncronas pode ser configurado usando o [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle) opção. A configuração do SDK da Web da plataforma é abordada na próxima seção.

Para saber mais sobre como o SDK da Web da plataforma pode gerenciar a cintilação, consulte a seção do guia :  [gerenciamento de cintilação para experiências personalizadas](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/manage-flicker.html)

## Configurar o SDK da Web da plataforma

O SDK da Web da plataforma deve ser configurado em cada carregamento de página. O exemplo a seguir parte do princípio que todo o site está sendo atualizado para o SDK da Web da plataforma em uma única implantação:

>[!BEGINTABS]

>[!TAB JavaScript]

O `configure` deve ser sempre o primeiro comando do SDK chamado. O `edgeConfigId` é [!UICONTROL ID do fluxo de dados]

```JavaScript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

>[!TAB Tags]

Em implementações de tags, muitos campos são preenchidos automaticamente ou podem ser selecionados em menus suspensos. Observe que diferentes plataformas [!UICONTROL sandboxes] e [!UICONTROL datastreams] pode ser selecionado para cada ambiente. O armazenamento de dados será alterado com base no estado da biblioteca de tags no processo de publicação.

![configuração da extensão de tag do SDK da Web](assets/tags-config.png){zoomable=&quot;yes&quot;}
>[!ENDTABS]

Se você planeja migrar da at.js para o SDK da Web da plataforma página por página, as seguintes opções de configuração são necessárias:


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

![configuração das opções de migração da extensão de tag do SDK da Web](assets/tags-config-migration.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]

As opções de configuração importantes relacionadas ao Target são descritas abaixo:

| Opção | Descrição | Valor de exemplo |
| --- | --- | --- |
| `edgeConfigId` | A ID do datastream | `ebebf826-a01f-4458-8cec-ef61de241c93` |
| `orgId` | ID da organização da Adobe Experience Cloud | `ADB3LETTERSANDNUMBERS@AdobeOrg` |
| `targetMigrationEnabled` | Use esta opção para permitir que o SDK da Web leia e grave os cookies herdados de mbox e mboxEdgeCluster usados pela at.js. Isso ajuda a manter o perfil do visitante ao mover de uma página que usa o SDK da Web para uma página que usa a biblioteca at.js e do modo oposto. | `true` |
| `idMigrationEnabled` | Se verdadeiro, o SDK lê e define cookies AMCV antigos. Essa opção ajuda na transição para o uso do SDK da Web da plataforma, enquanto algumas partes do site ainda podem usar o Visitor.js. | `true` |
| `thirdPartyCookiesEnabled` | Ativa a configuração de cookies de terceiros do Adobe. O SDK pode manter a ID de visitante em um contexto de terceiros para permitir que a mesma ID de visitante seja usada em sites. Use essa opção se você tiver vários sites; no entanto, às vezes, essa opção não é desejada por motivos de privacidade. | `true` |
| `prehidingStyle` | Usado para criar uma definição de estilo CSS que oculta as áreas de conteúdo da página da Web, enquanto o conteúdo personalizado é carregado do servidor. Isso é usado somente com implantações síncronas do SDK. | `body { opacity: 0 !important }` |

Para obter uma lista completa de opções, consulte [configuração do SDK da Web da plataforma](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=pt-BR) guia.

## Exemplo de implementação

Quando o SDK da Web da plataforma estiver corretamente no lugar, a página de exemplo terá esta aparência.

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

Em tags, adicione a extensão SDK da Web da Adobe Experience Platform:

![Adicionar a extensão Adobe Experience Platform Web SDK](assets/library-tags-addExtension.png){zoomable=&quot;yes&quot;}

E adicione as configurações desejadas:
![configuração das opções de migração da extensão de tag do SDK da Web](assets/tags-config-migration.png){zoomable=&quot;yes&quot;}


>[!ENDTABS]



É importante observar que a simples inclusão e configuração da biblioteca do SDK da Web da plataforma, conforme mostrado acima, não executa chamadas de rede para a Rede da Adobe Edge.

Em seguida, saiba como [solicitar e aplicar atividades baseadas em VEC](render-vec-activities.md) à página.

>[!NOTE]
>
>Temos o compromisso de ajudar você a ser bem-sucedido com sua migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, informe-nos ao publicar em [este debate comunitário](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).