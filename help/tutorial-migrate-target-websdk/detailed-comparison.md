---
title: Comparação da at.js 2.x com o SDK da Web - Migração do Target da at.js 2.x para o SDK da Web
description: Saiba mais sobre as diferenças entre a at.js 2.x e o SDK da Web da plataforma, incluindo recursos, funções, configurações e fluxo de dados.
exl-id: b6f0ac2b-0d8e-46ce-8e9f-7bbc61eb20ec
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '2007'
ht-degree: 3%

---

# Comparação da at.js com o SDK da Web da plataforma

A biblioteca at.js independente do Adobe Target é significativamente diferente do SDK da Web da plataforma. As tabelas a seguir são uma referência para ajudar a avaliar as áreas da sua implementação nas quais talvez seja necessário se concentrar durante o processo de migração.

Depois de revisar as informações abaixo e avaliar sua implementação técnica atual da at.js, você deve ser capaz de entender o seguinte:

- Quais recursos do Target são compatíveis com o SDK da Web da plataforma
- Quais funções da at.js têm equivalentes do SDK da Web da plataforma.
- Como as configurações do Target são aplicadas com o SDK da Web da plataforma
- Como o fluxo de dados da at.js e do SDK da Web da Platform difere

Se você não estiver familiarizado com o SDK da Web da Platform, não se preocupe. Os itens abaixo são abordados com mais detalhes neste tutorial.

## Comparação de recursos

| | at.js 2.x do Target | SDK da Web da Platform |
|---|---|---|
| Atualizar perfil de destino | Suportado | Suportado |
| Acionar exibição para SPA | Suportado | Suportado |
| Recommendations do Target | Suportado | Suportado |
| Buscar ofertas baseadas em formulário | Suportado | Suportado |
| Rastrear eventos | Suportado | Suportado |
| A4T: aplicativo de página única | Suportado | Suportado |
| A4T: rastreamento de cliques | Suportado | Suportado |
| A4T: registro no lado do cliente | Suportado | Suportado |
| A4T: registro do lado do servidor | Suportado | Suportado |
| Aplicar ofertas | Suportado | Suportado |
| Renderizar novamente a exibição no SPA sem notificações | Suportado | Suportado |
| Aplicativos híbridos | Suportado | Suportado |
| URLs de garantia da qualidade | Suportado | Suportado |
| IDs de terceiros da mbox | Suportado | Suportado |
| Atributos do cliente | Suportado | Suportado |
| Ofertas remotas | Suportado | Suportado |
| Ofertas de redirecionamento | Suportado | Compatível. No entanto, um redirecionamento de uma página com o SDK da Web da Platform para uma página com a at.js (e na direção oposta) não é compatível. |
| Decisão no dispositivo | Suportado | Não suportado no momento |
| Buscar previamente mboxes | Compatível com escopos personalizados e VEC para SPA | A busca prévia é o modo padrão do SDK da Web |
| Eventos personalizados | Suportado | Não suportado. Consulte o [roteiro público](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) para ver o status atual. |
| Tokens de resposta | Suportado | Compatível. Consulte a [documentação de tokens de resposta dedicados](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) para obter exemplos de código e as diferenças entre a at.js e o SDK da Web da Platform |
| Provedores de dados | Suportado | Não suportado. O código personalizado pode ser usado para acionar um comando `sendEvent` do SDK da Web da plataforma depois que os dados forem recuperados de outro provedor. |


## Chamadas notáveis

| | at.js 2.x do Target | SDK da Web da Platform |
|---|---|---|
| Mitigação de cintilação | O trecho pré-ocultação para implementações assíncronas usa uma ID de estilo de `at-body-style`. A at.js procura essa ID de elemento para remover o estilo depois que uma resposta é recebida. | O trecho pré-ocultação padrão usa uma ID de estilo de `alloy-prehiding`. O SDK da Web não é compatível com o trecho pré-ocultação da at.js, portanto, ele deve ser alterado como parte do processo de migração. |
| Renderizar conteúdo automaticamente no carregamento da página | Controlado com uma configuração global do Target. Habilitado quando `pageLoadEnabled` está definido como `true`. | Especificado no comando `sendEvent` do SDK da Web da plataforma. Habilitado ao configurar a opção `renderDecisions` como `true`. |
| Renderização manual do conteúdo | As funções `applyOffer()` e `applyOffers()` suportam somente a configuração de HTML | O comando `applyPropositions` oferece suporte à configuração, substituição ou acréscimo de HTML para obter mais flexibilidade |
| Rastreamento de eventos personalizados | Com suporte nas funções `trackEvent()` e `sendNotifications()`. Essas funções são específicas do Target e não afetam as métricas do Adobe Analytics. | Todos os dados das chamadas `sendEvent` do SDK da Web da plataforma são encaminhados para o Target. Os dados complementares necessários especificamente para o Target devem ser incluídos com o comando `sendEvent` com um eventType de `decisioning.propositionDisplay` ou `decisioning.propositionInteract` para garantir que as métricas do Adobe Analytics não sejam afetadas. |
| CNAME de destino | Compatível. Isso é separado do CNAME usado para o Analytics e o Serviço de ID de Experience Cloud. | Não é mais relevante. Um único CNAME pode ser usado para todas as chamadas do SDK da Web da plataforma. |
| Depuração | Os parâmetros de URL do `mboxDisable`, `mboxDebug` e `mboxTrace` podem ser usados para depuração com as ferramentas de desenvolvedor do seu navegador.<br><br>O Adobe Experience Platform Debugger também é uma ferramenta de depuração compatível. | Os parâmetros de URL `mboxDisable`, `mboxDebug` e `mboxTrace` não têm suporte.<br><br>Você pode ativar a depuração do SDK da Web adicionando o `alloy_debug=true` à sua cadeia de caracteres de consulta ou executando `alloy("setDebug", { "enabled": true });` no console do desenvolvedor.<br><br>A extensão do navegador Adobe Experience Platform Debugger pode ser usada para iniciar um rastreamento de borda para depuração.<br><br>Consulte a [documentação de depuração do SDK da Web da Platform](debugging.md) para obter mais informações. |
| Analytics for Target (A4T) | Usa valores SDID para unir chamadas do Target e do Analytics | Suporte nativo sem a necessidade de compilação |

>[!NOTE]
>
>Não há suporte para a migração do Target para o SDK da Web da Platform enquanto uma determinada página é mantida em uma implementação existente do AppMeasurement Adobe Analytics.
>
> É possível migrar sua implementação at.js (e AppMeasurement.js) para o SDK da Web da plataforma uma página por vez. Se você seguir esta abordagem, é melhor definir as opções [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) e [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) como `true` com o comando `configure`.

## Funções da at.js e equivalentes do SDK da Web da Platform

Muitas funções da at.js têm uma abordagem equivalente usando o SDK da Web da plataforma descrito na tabela abaixo. Para obter mais detalhes sobre as [funções da at.js](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consulte o Guia do Desenvolvedor do Adobe Target.

| Função da at.js 2.x | Equivalente ao SDK da Web da plataforma |
| --- | --- | 
| `getOffer()` e `getOffers()` | Para solicitar e [renderizar automaticamente](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#automatically-rendering-content) experiências baseadas em VEC do Target, use o comando `sendEvent` e defina a opção `renderDecisions` como verdadeira.<br><br>Para solicitar experiências baseadas em formulário ou [renderizar manualmente](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) o conteúdo, especifique uma matriz de `decisionScopes` (mboxes) com o comando `sendEvent`. |
| `applyOffer()` e `applyOffers()` | Use o comando [`applyPropositions`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#applypropositions) para aplicar conteúdo. Você pode optar por definir, substituir ou anexar HTML a um seletor específico. |
| `triggerView()` | O SDK da Web da Platform acionará automaticamente uma [alteração de exibição](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-trigger-a-view-change-in-a-single-page-application) para fins de VEC para SPA se a propriedade `web.webPageDetails.viewName` estiver definida na opção `xdm` do comando `sendEvent`. |
| `trackEvent()` e `sendNotifications()` | Use o comando `sendEvent` com um conjunto [específico `eventType`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-track-events):<br><br>`decisioning.propositionDisplay` sinaliza a renderização de uma atividade<br><br>`decisioning.propositionInteract` sinaliza a interação do usuário com uma atividade, como um clique do mouse. |
| `targetGlobalSettings()` | Sem equivalente direto. Consulte a [Comparação de configurações do Target](detailed-comparison.md) para obter mais detalhes. |
| `targetPageParams()` e `targetPageParamsAll()` | Todos os dados passados na opção `xdm` do comando `sendEvent` são mapeados para parâmetros mbox de Destino. Como os parâmetros da mbox são nomeados usando a notação de pontos serializada, a migração para o SDK da Web da Platform pode exigir a atualização de públicos-alvo e atividades existentes para usar os novos nomes de parâmetro da mbox. <br><br>Os dados passados como parte de `data.__adobe.target` do comando `sendEvent` estão mapeados para [perfil de destino e parâmetros específicos do Recommendations](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html#single-profile-update). |
| Eventos personalizados da at.js | Não suportado. Consulte o [roteiro público](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) para ver o status atual. [Tokens de resposta](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html) são expostos como parte de `propositions` na resposta da chamada `sendEvent`. |

## Configurações da at.js e equivalentes do SDK da Web da Platform

A biblioteca at.js pode ser configurada e baixada com várias configurações na interface do usuário do Target. Essas configurações também podem ser atualizadas com a função [`targetGlobalSettings()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/targetglobalsettings/). A tabela abaixo compara essas configurações com as disponíveis com o SDK da Web da plataforma.

| Configuração do at.js | Equivalente ao SDK da Web da plataforma |
| --- | --- |
| `bodyHiddenStyle` | Defina o [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle) com o comando `configure` |
| `bodyHidingEnabled` | Se um `prehidingStyle` for definido com o comando `configure`, esse recurso será habilitado. Se um estilo não estiver definido, o SDK da Web da Platform não tentará ocultar nenhum conteúdo. |
| `clientCode` | Configurado automaticamente |
| `cookieDomain` | Não aplicável |
| `crossDomain` | Defina a opção `thirdPartyCookiesEnabled` como `true` com o comando `configure` para habilitar cookies próprios e de terceiros para casos de uso entre domínios |
| `cspScriptNonce` e `cspStyleNonce` | Consulte a documentação para [configurar uma CSP](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-a-csp.html) |
| `dataProviders` | Não suportado |
| `decisioningMethod` | Todos os comandos `sendEvent` do SDK da Web da Platform usam a decisão do lado do servidor. A decisão híbrida e no dispositivo não é compatível. |
| `defaultContentHiddenStyle` e `defaultContentVisibleStyle` | Aplicável somente com a at.js 1.x. Semelhante à at.js 2.x, qualquer mitigação de cintilação para experiências baseadas em formulário pode ser realizada usando o código personalizado. |
| `deviceIdLifetime` | Não suportado. Se `targetMigrationEnabled` estiver definido como `true` com o comando `configure`, o cookie `mbox` será definido com a duração do dispositivo definida como 2 anos. Este valor não é configurável. |
| `enabled` | A funcionalidade do Target está ativada ou desativada com a configuração do fluxo de dados |
| `globalMboxAutoCreate` | Defina a opção `renderDecisions` como `true` com o comando `sendEvent` para buscar e renderizar automaticamente experiências baseadas em VEC.<br><br>Solicite um `decisionScope` para `__view__` se preferir renderizar manualmente as experiências baseadas em VEC. |
| `imsOrgId` | Definir o `orgId` com o comando `configure` |
| `optinEnabled` e `optoutEnabled` | Consulte as [opções de privacidade](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html) do SDK da Web da Platform. A opção `defaultConsent` se aplica a todas as soluções de Adobe compatíveis com o SDK da Web da plataforma. |
| `overrideMboxEdgeServer` e `overrideMboxEdgeServerTimeout` | Não aplicável. Todas as solicitações de SDK da Web da Platform usam a rede Edge da Adobe Experience Platform. |
| `pageLoadEnabled` | Defina a opção `renderDecisions` como `true` com o comando `sendEvent` |
| `secureOnly` | Não suportado. O SDK da Web da Platform define todos os cookies com os atributos `secure` e `sameSite="none"`. |
| `selectorsPollingTimeout` | Não suportado. O SDK da Web da Platform usa um valor de 5 segundos. O código personalizado pode ser usado para renderizar conteúdo manualmente, se necessário. |
| `serverDomain` | Usar a configuração `edgeDomain` com o comando `configure` |
| `telemetryEnabled` | Não aplicável |
| `timeout` | Não suportado. Recomenda-se garantir que qualquer código de mitigação de cintilação inclua um tempo limite apropriado. |
| `viewsEnabled` | Não suportado. O conteúdo das exibições do Target sempre será obtido na primeira chamada `sendEvent()` se `renderDecisions` estiver definido como `true` ou se o `__view__` decisionScope estiver incluído na solicitação. |
| `visitorApiTimeout` | Não aplicável |


## Comparação do diagrama do sistema

Os diagramas a seguir devem ajudar você a entender as diferenças de fluxo de dados entre uma implementação do Target usando at.js e uma implementação usando o SDK da Web da plataforma.

### diagrama de sistema da at.js 2.x

Comportamento do ![at.js 2.0 no carregamento da página](assets/target-at-js-2x-diagram.png){zoomable="yes"}

| Chame | Detalhes |
| --- | --- |
| 1 | A chamada retorna a ID de Experience Cloud (ECID). Se o usuário for autenticado, outra chamada sincroniza a ID do cliente. |
| 2 | A biblioteca at.js é carregada de forma síncrona e oculta o corpo do documento (a at.js também pode ser carregada de forma assíncrona com uma opção que oculta previamente o trecho implementado na página). |
| 3 | A solicitação de Carregamento de página é feita, incluindo todos os parâmetros configurados, ECID, SDID e ID do cliente. |
| 4 | Os scripts de perfil executam e fazem o feed na Loja do perfil. A Loja solicita públicos qualificados da Biblioteca de público-alvo (por exemplo, públicos-alvo compartilhados do Analytics, Audience Manager e assim por diante). Os atributos do cliente são enviados à Loja de perfis em um processo em lote. |
| 5 | Com base no URL, parâmetros de solicitação e dados de perfil, o Target decide quais Atividades e Experiências retornarão ao visitante para a página atual e para as exibições futuras. |
| 6 | O conteúdo direcionado é enviado de volta para a página, opcionalmente incluindo valores de perfil para personalização adicional.<br><br>O conteúdo direcionado na página atual é revelado o mais rápido possível sem cintilação do conteúdo padrão.<br><br>O conteúdo direcionado para exibições futuras de um aplicativo de página única é armazenado em cache no navegador para que possa ser aplicado instantaneamente, sem uma chamada de servidor extra, quando as exibições forem acionadas. |
| 7 | Dados do Analytics enviados da página para os Servidores de coleta de dados. |
| 8 | Os dados do Target são correspondidos aos dados do Analytics pela SDID, e processados no armazenamento de relatórios do Analytics. Em seguida, os dados do Analytics podem ser exibidos no Analytics e no Target pelos relatórios do A4T. |

Consulte o guia do desenvolvedor para obter mais informações sobre como [implementar o Target usando a at.js para aplicativos de página única](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application/).

### Diagrama de sistema do SDK da Web da Platform

![Diagrama da decisão de borda do Adobe Target com o SDK da Web da plataforma](assets/target-platform-web-sdk.png)

| Chame | Detalhes |
| --- | --- |
| 1 | O dispositivo carrega o SDK da Web da Platform. O SDK da Web da Platform envia uma solicitação para a rede de borda com dados XDM, a ID de ambiente dos fluxos de dados, os parâmetros transmitidos e a ID do cliente (opcional). A página (ou contêineres) é pré-oculta. |
| 2 | A rede de borda envia a solicitação aos serviços de borda para enriquecê-la com a ID do visitante, o consentimento e outras informações de contexto do visitante, como geolocalização e nomes amigáveis ao dispositivo. |
| 3 | A rede de borda envia a solicitação de personalização enriquecida para a borda do Target com a ID do visitante e os parâmetros transmitidos. |
| 4 | Os scripts de perfil executam e, em seguida, fazem o feed no armazenamento do perfil do Target. O armazenamento de perfil busca segmentos da Biblioteca de público-alvo (por exemplo, segmentos compartilhados da Adobe Analytics, Adobe Audience Manager, Adobe Experience Platform). |
| 5 | Com base nos parâmetros de solicitação de URL e dados de perfil, o Target determina quais atividades e experiências serão exibidas para o visitante na exibição de página atual e para exibições futuras de busca prévia. O Target envia isso de volta para a rede de borda. |
| 6 | a. A rede de borda envia a resposta de personalização de volta para a página, incluindo, opcionalmente, valores de perfil para personalização adicional. O conteúdo personalizado na página atual é revelado o mais rápido possível sem cintilação do conteúdo padrão.<br><br>b. O conteúdo personalizado para exibições que são mostradas como resultado das ações do usuário em um Aplicativo de página única (SPA) é armazenado em cache para renderização instantânea sem chamadas de servidor adicionais.<br><br>c A rede de borda envia a ID do visitante e outros valores em cookies (por exemplo, consentimento, ID de sessão, identidade, verificação de cookie, personalização e assim por diante). |
| 7 | A rede de borda encaminha os detalhes do Analytics for Target (A4T) (metadados de atividade, experiência e conversão) para a borda do Analytics. |

Consulte o guia do desenvolvedor para obter mais informações sobre como [implementar o Target usando o SDK da Web da plataforma para aplicativos de página única](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html).

Depois de ter uma boa compreensão técnica da sua implementação do Target atual e dos recursos que você usa, a próxima etapa é executar a [configuração inicial](initial-setup.md).

>[!NOTE]
>
>Estamos empenhados em ajudar você a ter sucesso com a migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
