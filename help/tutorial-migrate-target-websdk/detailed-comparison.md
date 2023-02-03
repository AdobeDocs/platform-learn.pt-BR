---
title: Comparação da at.js 2.x com o SDK da Web | Migrar o Target da at.js 2.x para o SDK da Web
description: Saiba mais sobre as diferenças entre a at.js 2.x e o SDK da Web da plataforma, incluindo recursos, funções, configurações e fluxo de dados.
source-git-commit: 8209b13b745dbea418003b133a6834825947950e
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 8%

---

# Comparação da at.js com o SDK da Web da plataforma

A biblioteca independente da at.js do Adobe Target é significativamente diferente do SDK da Web da plataforma. As tabelas a seguir são uma referência para ajudar a avaliar as áreas de sua implementação nas quais você pode precisar se concentrar durante o processo de migração.

Depois de revisar as informações abaixo e avaliar sua implementação técnica atual da at.js, você deve ser capaz de entender o seguinte:

- Quais recursos do Target são compatíveis com o SDK da Web da plataforma
- Quais funções da at.js têm equivalentes de SDK da Web da plataforma
- Como as configurações do Target são aplicadas ao SDK da Web da plataforma
- Como o fluxo de dados da at.js e do SDK da Web da plataforma diferem

Se você nunca usou o Platform Web SDK, não se preocupe. Os itens abaixo são abordados com mais detalhes neste tutorial.

## Comparação de recursos

|  | Target at.js 2.x | SDK da Web da Platform |
|---|---|---|
| Atualizar perfil do Target | Suportado | Suportado |
| Acionar exibição para SPA | Suportado | Suportado |
| Recommendations do Target | Suportado | Suportado |
| Buscar ofertas baseadas em formulário | Suportado | Suportado |
| Rastrear eventos | Suportado | Suportado |
| A4T: Aplicativo de página única | Suportado | Suportado |
| A4T: Rastreamento de cliques | Suportado | Suportado |
| A4T: Registro no lado do cliente | Suportado | Suportado |
| A4T: Registro no lado do servidor | Suportado | Suportado |
| Aplicar ofertas | Suportado | Suportado |
| Renderizar novamente a exibição no SPA sem notificações | Suportado | Suportado |
| Aplicativos híbridos | Suportado | Suportado |
| URLs de controle de qualidade | Suportado | Suportado |
| IDs de terceiros da Mbox | Suportado | Suportado |
| Atributos do cliente | Suportado | Compatível |
| Ofertas remotas | Suportado | Suportado |
| Ofertas de redirecionamento | Suportado | Suportado. No entanto, não há suporte para o redirecionamento de uma página com o SDK da Web da plataforma para uma página com a at.js (e na direção oposta). |
| Decisão no dispositivo | Suportado | Não suportado no momento |
| Buscar mboxes previamente | Suportado | Ativado por padrão em todas as novas migrações iniciadas após 1 de outubro de 2022 |
| Eventos Personalizados | Suportado | Não suportado. Consulte a [roteiro público](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) para status atual. |
| Tokens de resposta | Suportado | Suportado. Consulte a [documentação de tokens de resposta dedicados](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) para exemplos de código e diferenças entre at.js e SDK da Web da plataforma |
| Provedores de dados | Suportado | Não suportado. O código personalizado pode ser usado para acionar um SDK da Web da plataforma `sendEvent` depois que os dados são recuperados de outro provedor. |


## Chamadas notáveis

|  | Target at.js 2.x | SDK da Web da Platform |
|---|---|---|
| Mitigação de cintilação | O trecho pré-ocultação para implementações assíncronas usa uma ID de estilo de `at-body-style`. A at.js procura essa ID de elemento para remover o estilo assim que uma resposta é recebida. | O trecho pré-ocultação padrão usa uma ID de estilo de `alloy-prehiding`. O SDK da Web não é compatível com o trecho pré-ocultação da at.js, portanto, deve ser alterado como parte do processo de migração. |
| Renderizar automaticamente o conteúdo no carregamento da página | Controlada com uma configuração global do Target. Ativado quando `pageLoadEnabled` está definida como `true`. | Especificado no SDK da Web da plataforma `sendEvent` comando. Ativado ao definir a variável `renderDecisions` para `true`. |
| Renderização manual do conteúdo | O `applyOffer()` e `applyOffers()` as funções suportam a configuração somente HTML | O `applyPropositions` O comando oferece suporte à configuração, substituição ou anexação do HTML para maior flexibilidade |
| Rastreamento de eventos personalizados | Suportado com `trackEvent()` e `sendNotifications()` funções. Essas funções são específicas do Target e não afetam as métricas do Adobe Analytics. | Todos os dados do SDK da Web da plataforma `sendEvent` as chamadas são encaminhadas ao Target. Os dados complementares necessários especificamente para o Target devem ser incluídos no `sendEvent` com um eventType de `decisioning.propositionDisplay` ou `decisioning.propositionInteract` para garantir que as métricas do Adobe Analytics não sejam afetadas. |
| CNAME do Target | Suportado. Isso é separado do CNAME usado para o Analytics e do Serviço da Experience Cloud ID. | Não é mais relevante. Um único CNAME pode ser usado para todas as chamadas do SDK da Web da plataforma. |
| Depuração | O `mboxDisable`, `mboxDebug`e `mboxTrace` Parâmetros de URL podem ser usados para depuração com as ferramentas do desenvolvedor do navegador.<br><br>O Adobe Experience Platform Debugger também é uma ferramenta de depuração compatível. | O `mboxDisable`, `mboxDebug`e `mboxTrace` Parâmetros de URL não são suportados.<br><br>Você pode ativar a depuração do SDK da Web ao adicionar a variável `alloy_debug=true` para a sequência de consulta ou execução `alloy("setDebug", { "enabled": true });` no console do desenvolvedor.<br><br>A extensão de navegador do Adobe Experience Platform Debugger pode ser usada para iniciar um rastreamento de borda para depuração.<br><br>Consulte a [depurar o SDK da Web da plataforma](debugging.md) documentação para obter mais informações. |
| Analytics for Target (A4T) | Usa valores SDID para unir chamadas do Target e do Analytics | Nativamente compatível sem a necessidade de compilação |

>[!NOTE]
>
>Não há suporte para a migração do Target para o SDK da Web da plataforma, mantendo uma implementação AppMeasurement Adobe Analytics existente para uma determinada página.
>
> É possível migrar a implementação da at.js (e AppMeasurement.js) para o SDK da Web da plataforma, uma página de cada vez. Se seguir essa abordagem, é melhor definir a variável [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) e [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) opções para `true` com o `configure` comando.

## Funções da at.js e equivalentes do SDK da Web da plataforma

Muitas funções da at.js têm uma abordagem equivalente usando o SDK da Web da plataforma descrito na tabela abaixo. Para obter mais detalhes sobre o [Funções da at.js](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consulte o Guia do desenvolvedor do Adobe Target.

| Função da at.js 2.x | Equivalente ao SDK da Web da plataforma |
| --- | --- | 
| `getOffer()` e `getOffers()` | Para solicitar e [renderizar automaticamente](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#automatically-rendering-content) Experiências baseadas em VEC do Target, use o `sendEvent` e defina o `renderDecisions` para verdadeiro.<br><br>Para solicitar experiências baseadas em formulário ou para [renderizar manualmente](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) conteúdo, especifique uma matriz de `decisionScopes` (mboxes) com o `sendEvent` comando. |
| `applyOffer()` e `applyOffers()` | Use o [`applyPropositions`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#applypropositions) para aplicar o conteúdo. Você pode optar por definir, substituir ou anexar o HTML a um seletor específico. |
| `triggerView()` | O SDK da Web da plataforma aciona automaticamente um [exibir alteração](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-trigger-a-view-change-in-a-single-page-application) para efeitos do SPA VEC, se `web.webPageDetails.viewName` é definida na variável `xdm` da `sendEvent` comando. |
| `trackEvent()` e `sendNotifications()` | Use o `sendEvent` com um [específico `eventType`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-track-events) definido:<br><br>`decisioning.propositionDisplay` sinaliza a renderização de uma atividade<br><br>`decisioning.propositionInteract` sinaliza uma interação do usuário com uma atividade , como um clique do mouse. |
| `targetGlobalSettings()` | Nenhum equivalente direto. Consulte a [Comparação de configurações do Target](detailed-comparison.md) para obter mais detalhes. |
| `targetPageParams()` e `targetPageParamsAll()` | Todos os dados transmitidos no `xdm` da `sendEvent` é mapeado para os parâmetros da mbox do Target. Como os parâmetros da mbox são nomeados usando a notação de pontos serializada, a migração para o SDK da Web da plataforma pode exigir a atualização de públicos e atividades existentes para usar os novos nomes de parâmetros da mbox. <br><br>Dados passados como parte de `data.__adobe.target` do `sendEvent` está mapeado para [Perfil do Target e parâmetros específicos do Recommendations](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html#single-profile-update). |
| Eventos personalizados da at.js | Não suportado. Consulte a [roteiro público](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) para status atual. [Tokens de resposta](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html) são expostas como parte da `propositions` na resposta do `sendEvent` chame. |

## Configurações da at.js e equivalentes do SDK da Web da plataforma

A biblioteca at.js pode ser configurada e baixada com várias configurações na interface do usuário do Target. Essas configurações também podem ser atualizadas com a variável [`targetGlobalSettings()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/targetglobalsettings/) . A tabela abaixo compara essas configurações com as disponíveis com o SDK da Web da plataforma.

| Configuração da at.js | Equivalente ao SDK da Web da plataforma |
| --- | --- |
| `bodyHiddenStyle` | Defina as [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle) com o `configure` comando |
| `bodyHidingEnabled` | Se uma `prehidingStyle` é definido com a variável `configure` , esse recurso é ativado. Se um estilo não estiver definido, o SDK da Web da plataforma não tentará ocultar nenhum conteúdo. |
| `clientCode` | Automaticamente configurado |
| `cookieDomain` | Não aplicável |
| `crossDomain` | Defina as `thirdPartyCookiesEnabled` para `true` com o `configure` para ativar cookies próprios e de terceiros em casos de uso entre domínios |
| `cspScriptNonce` e `cspStyleNonce` | Consulte a documentação para [configuração de uma CSP](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-a-csp.html) |
| `dataProviders` | Não suportado |
| `decisioningMethod` | Todos os SDK da Web da plataforma `sendEvent` Os comandos usam decisões do lado do servidor. Decisões híbridas e no dispositivo não são compatíveis. |
| `defaultContentHiddenStyle` e `defaultContentVisibleStyle` | Aplicável somente com a at.js 1.x. Semelhante à at.js 2.x, qualquer atenuação de cintilação para experiências baseadas em formulário pode ser realizada usando o código personalizado. |
| `deviceIdLifetime` | Não suportado. If `targetMigrationEnabled` está definida como `true` com o `configure` , o `mbox` é definido com a duração do dispositivo definida como 2 anos. Este valor não é configurável. |
| `enabled` | A funcionalidade Target está ativada ou desativada com a configuração de fluxo de dados |
| `globalMboxAutoCreate` | Defina as `renderDecisions` para `true` com o `sendEvent` para buscar e renderizar automaticamente experiências baseadas em VEC.<br><br>Solicitar um `decisionScope` para `__view__` se preferir renderizar manualmente as experiências baseadas em VEC. |
| `imsOrgId` | Defina as `orgId` com o `configure` comando |
| `optinEnabled` e `optoutEnabled` | Consulte o SDK da Web da plataforma [opções de privacidade](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html). O `defaultConsent` se aplica a todas as soluções do Adobe compatíveis com o SDK da Web da plataforma. |
| `overrideMboxEdgeServer` e `overrideMboxEdgeServerTimeout` | Não aplicável. Todas as solicitações do SDK da Web da plataforma usam a rede Adobe Experience Platform Edge. |
| `pageLoadEnabled` | Defina as `renderDecisions` para `true` com o `sendEvent` comando |
| `secureOnly` | Não suportado. O SDK da Web da plataforma define todos os cookies com a variável `secure` e `sameSite="none"` atributos. |
| `selectorsPollingTimeout` | Não suportado. O SDK da Web da plataforma usa um valor de 5 segundos. O código personalizado pode ser usado para renderizar manualmente o conteúdo, se necessário. |
| `serverDomain` | Use o `edgeDomain` com o `configure` comando |
| `telemetryEnabled` | Não aplicável |
| `timeout` | Não suportado. É recomendável garantir que qualquer código de mitigação de cintilação inclua um tempo limite apropriado. |
| `viewsEnabled` | Não suportado. O conteúdo das exibições do Target é sempre buscado na primeira `sendEvent()` chamar se `renderDecisions` está definida como `true` ou `__view__` o decisionScope está incluído na solicitação. |
| `visitorApiTimeout` | Não aplicável |


## Comparação de diagrama de sistema

Os diagramas a seguir devem ajudar você a entender as diferenças do fluxo de dados entre uma implementação do Target usando at.js e uma implementação usando o SDK da Web da plataforma.

### Diagrama de sistema da at.js 2.x

![Comportamento do at.js 2.0 no carregamento da página](assets/target-at-js-2x-diagram.png)

| Chame | Detalhes |
| --- | --- |
| 1 | A chamada retorna Experience Cloud ID (ECID). Se o usuário estiver autenticado, outra chamada sincroniza a ID do cliente. |
| 2 | A biblioteca at.js é carregada de forma síncrona e oculta o corpo do documento (a at.js também pode ser carregada de forma assíncrona com uma opção que oculta previamente o trecho implementado na página). |
| 3 | A solicitação de Carregamento de página é feita incluindo todos os parâmetros configurados, ECID, SDID e ID do cliente. |
| 4 | Os scripts de perfil executam e fazem o feed na Loja de perfis. A Loja solicita públicos qualificados da Biblioteca de público-alvo (por exemplo, públicos-alvo compartilhados do Analytics, Audience Manager e assim por diante). Os atributos do cliente são enviados para a Loja de perfis em um processo em lote. |
| 5 | Com base no URL, nos parâmetros de solicitação e nos dados do perfil, o Target decide quais atividades e experiências retornarão ao visitante para a página atual e para as exibições futuras. |
| 6 | O conteúdo direcionado foi enviado de volta à página, incluindo, opcionalmente, valores de perfil para personalização adicional.<br><br>O conteúdo direcionado na página atual é revelado o mais rápido possível sem cintilação do conteúdo padrão.<br><br>O conteúdo direcionado para futuras exibições de um aplicativo de página única é armazenado em cache no navegador, portanto, pode ser aplicado instantaneamente, sem uma chamada de servidor extra, quando as exibições forem acionadas. (Consulte o diagrama a seguir para o comportamento triggerView() ). |
| 7 | Dados do Analytics enviados da página para os Servidores de coleta de dados. |
| 8 | Os dados do Target são correspondidos aos dados do Analytics pela SDID, e processados no armazenamento de relatório do Analytics. Em seguida, os dados do Analytics podem ser visualizados no Analytics e no Target pelos relatórios do A4T. |

Consulte o guia do desenvolvedor para obter mais informações sobre como [implementar o Target usando at.js para aplicativos de página única](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application/).

### Diagrama de sistema do Web SDK do Platform

![Diagrama da decisão de borda do Adobe Target com o SDK da Web da plataforma](assets/target-platform-web-sdk.png)

| Chame | Detalhes |
| --- | --- |
| 1 | O dispositivo carrega o SDK da Web da plataforma. O SDK da Web da plataforma envia uma solicitação para a rede de borda com dados XDM, a ID do ambiente do Datastreams, parâmetros transmitidos e a ID do cliente (opcional). A página (ou contêineres) é pré-oculta. |
| 2 | A rede de borda envia a solicitação aos serviços de borda para enriquecê-la com a ID do visitante, o consentimento e outras informações de contexto do visitante, como localização geográfica e nomes amigáveis ao dispositivo. |
| 3 | A rede de borda envia a solicitação de personalização enriquecida para a borda do Target com a ID do visitante e os parâmetros transmitidos. |
| 4 | Os scripts de perfil executam e, em seguida, fazem o feed no armazenamento de perfil do Target. O armazenamento de perfil busca segmentos da Biblioteca de público-alvo (por exemplo, segmentos compartilhados do Adobe Analytics, Adobe Audience Manager, Adobe Experience Platform). |
| 5 | Com base nos parâmetros de solicitação de URL e dados de perfil, o Target determina quais atividades e experiências serão exibidas para o visitante na exibição de página atual e para futuras exibições pré-buscadas. O Target envia isso de volta para a rede de borda. |
| 6 | a. A rede de borda envia a resposta de personalização de volta para a página, incluindo, opcionalmente, valores de perfil para personalização adicional. O conteúdo personalizado na página atual é revelado o mais rápido possível sem cintilação do conteúdo padrão.<br><br>b. O conteúdo personalizado para exibições que são mostradas como resultado das ações do usuário em um Aplicativo de página única (SPA) é armazenado em cache para renderização instantânea sem chamadas de servidor adicionais.<br><br>c. A rede de borda envia a ID do visitante e outros valores nos cookies (por exemplo, consentimento, ID da sessão, identidade, verificação de cookie, personalização e assim por diante). |
| 7 | A rede de borda encaminha detalhes do Analytics for Target (A4T) (metadados de atividade, experiência e conversão) para a borda do Analytics. |

Consulte o guia do desenvolvedor para obter mais informações sobre como [implementar o Target usando o SDK da Web da plataforma para aplicativos de página única](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html).

Depois de ter uma boa compreensão técnica da implementação atual do Target e dos recursos que usa, a próxima etapa é executar a variável [configuração inicial](initial-setup.md).

>[!NOTE]
>
>Temos o compromisso de ajudar você a ser bem-sucedido com sua migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, informe-nos ao publicar em [este debate comunitário](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
