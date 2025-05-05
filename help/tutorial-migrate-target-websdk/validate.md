---
title: Validar implementações do Target com o SDK da Web - Migrar o Target da at.js 2.x para o SDK da Web
description: Saiba como validar atividades e depurar uma implementação do Adobe Target usando o SDK da Web da Adobe Experience Platform.
exl-id: 09b4ebeb-fae9-470d-8ea9-f6e3c7d7da5e
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 0%

---

# Validar a implementação do SDK da Web da plataforma

Depois de migrar a implementação do Target da at.js para o SDK da Web da plataforma, é importante validar se tudo está funcionando corretamente antes de publicar qualquer alteração no site de produção. A Adobe recomenda o seguinte, abordado em detalhes nesta página:

* Realizar uma validação técnica para garantir que a implementação básica e as solicitações e respostas do SDK da Web da plataforma tenham aparência correta
* Garantir que as atividades do Target sejam entregues e renderizadas corretamente
* Verifique se os relatórios funcionam corretamente
* Rever públicos-alvo e scripts de perfil para garantir que sejam compatíveis com o SDK da Web da plataforma
* Verifique se as integrações com o Adobe ou aplicativos de terceiros funcionam corretamente

Cada implementação do Target é diferente, dependendo da arquitetura do site e dos recursos usados. Você pode usar as tabelas abaixo como ponto de partida e adicionar quaisquer itens exclusivos à sua implementação. A [Página Depuração](debugging.md) deste tutorial mostra as ferramentas que você pode usar para ajudar nesta validação.

## Validação técnica

| Item de validação | Notas |
|---|---|
| O trecho pré-ocultação da at.js não está mais presente na página | O SDK da Web da Platform não remove automaticamente o estilo com ID `at-body-style`. Deixar esse trecho antigo na página resultará em conteúdo oculto até que o tempo limite do trecho seja atingido. |
| A biblioteca at.js não está mais presente na página | Verifique se não há nenhum objeto &quot;adobe.target&quot; no console de ferramentas do desenvolvedor do seu navegador. A inclusão do SDK da Web da Platform e da at.js resulta em comportamento de renderização não intencional |
| Os parâmetros esperados estão no XDM e nos objetos de dados da solicitação `sendEvent` | |
| O catálogo do Recommendations é atualizado conforme esperado se estiver usando solicitações de página para preencher o catálogo | |
| Parâmetros de perfil passados com sucesso para o Target | Exibir rastreamentos do Edge no Debugger |
| Os parâmetros mapeados para o XDM no mapeador de sequência de dados são passados corretamente para o Target | Validar usando o recurso Edge Trace do Debugger e/ou Assurance |
| O conteúdo do público alvo retorna nas `sendEvent` respostas aplicáveis | Esperado quando a opção `renderDecisions` está definida como `true` ou os escopos são solicitados e o usuário se qualifica para uma atividade de Destino específica |
| Um evento `decisioning.propositionDisplay` é acionado após a renderização das atividades baseadas em VEC | As atividades renderizadas automaticamente e sob demanda devem ter chamadas de evento separadas |
| Um evento `decisioning.propositionDisplay` é acionado após a renderização das atividades baseadas em formulário | Aplicável somente para determinadas implementações. Requer código personalizado para executar esta chamada. |
| Um evento `decisioning.propositionDisplay` é acionado quando uma oferta é aplicada em uma alteração de exibição do SPA | Aplicável somente para implementações do SPA |
| Um evento `decisioning.propositionDisplay` NÃO é acionado quando um componente SPA é renderizado novamente para uma determinada exibição | Aplicável somente para implementações do SPA |
| Um evento `decisioning.propsitionInteract` é acionado após uma conversão de atividade | Espera-se que as conversões personalizadas e &quot;Clicou em um elemento&quot; migradas da at.js `trackEvent` ou `sendNotifications` tenham chamadas de evento separadas |
| Os tokens de resposta são retornados na resposta `sendEvent` e têm valores esperados | Os tokens de resposta devem funcionar normalmente com o SDK da Web |
| As ECIDs são consistentes em todas as páginas com o SDK da Web e a at.js | Aplicável a migrações página por página. Não se espera que as ofertas de redirecionamento funcionem nesses tipos de migrações |


## Entrega e renderização de atividade

| Item de validação | Notas |
|---|---|
| As atividades baseadas em VEC são renderizadas corretamente no carregamento da página | É melhor validar modificações de código personalizadas e modificações básicas, como reorganizar elementos ou substituir texto |
| As atividades com base em VEC são renderizadas corretamente nas alterações de exibição do SPA | Aplicável somente para implementações do SPA |
| As atividades baseadas em formulário são renderizadas corretamente | Aplicável somente para determinadas implementações. A renderização de atividades baseadas em formulário requer um código personalizado semelhante ao at.js. |
| As atividades que usam redirecionamentos funcionam corretamente | Os redirecionamentos são suportados se a página de origem e de destino usarem o SDK da Web da plataforma. Um redirecionamento do Target de uma página da at.js para uma página do SDK da Web da plataforma do ou o oposto não é suportado. |
| Atividades que usam ofertas remotas funcionam corretamente | Não comum, verifique seu inventário de ofertas do Target para Ofertas remotas |
| A cintilação é atenuada adequadamente | A manipulação de cintilação é opcional, mas certifique-se de que todas as táticas de mitigação existentes estejam funcionando como esperado para obter o melhor desempenho da página e experiência do usuário |
| Os links de controle de qualidade funcionam conforme esperado | Se não estiver funcionando, confirme se web.webPageDetails.URL corresponde exatamente ao URL no navegador |
| Todos os tipos de ofertas usados com frequência são renderizados conforme esperado |  |

## Relatórios

| Item de validação | Notas |
|---|---|
| Os visitantes são atribuídos a atividades baseadas em VEC | É melhor validar se o relatório funciona conforme esperado para modificações de carregamento de página e modificações de exibição de SPA |
| Os visitantes são atribuídos a atividades baseadas em formulário | Dependendo da abordagem de renderização usada, sua implementação pode exigir um código personalizado para executar um evento `decisioning.propositionDisplay` |
| As metas de conversão padrão são capturadas corretamente | Aplica-se ao Target ou Analytics como a fonte de geração de relatórios |
| As conversões e os detalhes do pedido são capturados corretamente | Verifique o relatório de Auditoria |
| As conversões de rastreamento de cliques são capturadas corretamente |  |
| As metas de conversão personalizadas são capturadas corretamente | Por exemplo, metas de conversão migradas da at.js `trackEvent` ou `sendNotifications` que são normalmente usadas com a meta &quot;visualizou uma mbox&quot; |

## Públicos-alvo e scripts de perfil

| Item de validação | Notas |
|---|---|
| Os públicos usados em atividades ativas são compatíveis com o SDK da Web da Platform | Os públicos que usam o componente &quot;Personalizado&quot; (parâmetro de mbox) devem ser atualizados para incluir atributos XDM |
| Todos os scripts de perfil são compatíveis com o SDK da Web da Platform | Todos os scripts de perfil que usam parâmetros mbox devem ser atualizados para incluir atributos XDM |
| Retorno de atividades para públicos do Target | É melhor executar a validação completa em públicos-alvo modificados para se tornarem compatíveis com o SDK da Web da Platform |
| Os scripts de perfil são avaliados conforme esperado | Exibir rastreamentos do Edge no Debugger |

## Integrações com aplicativos Adobe

| Item de validação | Notas |
|---|---|
| Retorno de atividades para públicos-alvo do Experience Cloud | Por exemplo, um segmento publicado do Adobe Analytics |
| Retorno de atividades para públicos-alvo do Experience Platform | Somente se aplica se você tiver uma licença para um aplicativo baseado em Experience Platform como RTCDP |
| Retorno de atividades para públicos-alvo do Audience Manager | Por exemplo, um segmento baseado na visita a uma página específica |
| Os dados da atividade do Target são exibidos no Analysis Workspace | Aplicável a atividades que usam o Adobe Analytics como fonte de relatórios |

## Integrações com aplicativos de terceiros

| Item de validação | Notas |
|---|---|
| Os dados do token de resposta são passados corretamente a aplicativos de terceiros | As abordagens de integração podem variar, mas um método comum é usar tokens de resposta do Target para transmitir informações de atividade e experiência para outras ferramentas de análise, como o Google Analytics |
| As informações de terceiros são transmitidas como XDM ou dados de perfil | Todas as informações relevantes de terceiros devem ser passadas em `sendEvent` chamadas para o Target |

Depois de executar as etapas de validação acima, você pode ter certeza de que a implementação do SDK da Web da Platform está pronta para entrar em produção.

Em seguida, saiba como [solucionar problemas de uma implementação do Target usando o SDK da Web da plataforma](debugging.md).

>[!NOTE]
>
>Estamos empenhados em ajudar você a ter sucesso com a migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=pt#M463).
