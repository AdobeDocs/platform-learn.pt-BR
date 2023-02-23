---
title: Validar as implementações do Target com o SDK da Web | Migrar o Target da at.js 2.x para o SDK da Web
description: Saiba como validar atividades e depurar uma implementação do Adobe Target usando o Adobe Experience Platform Web SDK.
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 0%

---

# Validar a implementação do SDK da Web da plataforma

Depois de migrar a implementação do Target da at.js para o SDK da Web da plataforma, é importante validar se tudo está funcionando corretamente antes de publicar qualquer alteração no site de produção. O Adobe recomenda o seguinte, que é abordado detalhadamente nesta página:

* Execute uma validação técnica para garantir que as solicitações e respostas básicas do SDK da Web da plataforma e da implementação tenham a aparência correta
* Assegure-se de que as atividades do Target sejam entregues e renderizadas corretamente
* Verifique se o relatório funciona corretamente
* Revise públicos-alvo e scripts de perfil para garantir a compatibilidade com o SDK da Web da plataforma
* Verifique se as integrações com o Adobe ou aplicativos de terceiros funcionam corretamente

Cada implementação do Target é diferente, dependendo da arquitetura do site e dos recursos usados. Você pode usar as tabelas abaixo como ponto de partida e adicionar qualquer item exclusivo à sua implementação. O [Página de depuração](debugging.md) deste tutorial mostra as ferramentas que você pode usar para ajudar nesta validação.

## Validação técnica

| Item de validação | Notas |
|---|---|
| O trecho pré-ocultação da at.js não está mais presente na página | O SDK da Web da plataforma não remove automaticamente o estilo com a ID `at-body-style`. Deixar esse trecho antigo na página resulta em conteúdo oculto até atingir o tempo limite do trecho. |
| A biblioteca at.js não está mais presente na página | Verifique se não há nenhum objeto &quot;adobe.target&quot; no console de ferramentas do desenvolvedor do navegador. A inclusão do SDK da Web da plataforma e da at.js resulta em comportamento de renderização não intencional |
| Os parâmetros esperados estão no XDM e os objetos de dados do `sendEvent` solicitação |  |
| O catálogo do Recommendations é atualizado como esperado se estiver usando solicitações de página para preencher o catálogo |  |
| Parâmetros de perfil foram enviados com êxito para o Target | Exibir rastreamentos de borda no Debugger |
| Os parâmetros mapeados para XDM no mapeador de conjunto de dados são passados corretamente para o Target | Validar usando o recurso Edge Trace do Debugger e/ou Assurance |
| O conteúdo do Target retorna no `sendEvent` response | Esperado quando `renderDecisions` está definida como `true` Os escopos ou são solicitados e o usuário se qualifica para uma atividade específica do Target |
| A `decisioning.propositionDisplay` O evento é acionado após a renderização de atividades baseadas em VEC | As atividades renderizadas automaticamente e sob demanda devem ter chamadas de evento separadas |
| A `decisioning.propositionDisplay` evento é acionado após a renderização de atividades baseadas em formulário | Aplicável somente a determinadas implementações. Requer código personalizado para executar esta chamada. |
| A `decisioning.propositionDisplay` evento é acionado quando uma oferta é aplicada em uma alteração de exibição de SPA | Aplicável somente para implementações de SPA |
| A `decisioning.propositionDisplay` O evento NÃO é acionado quando um componente SPA é renderizado novamente para uma determinada exibição | Aplicável somente para implementações de SPA |
| A `decisioning.propsitionInteract` evento é acionado após uma conversão de atividade | O &quot;Clicou em um elemento&quot; e as conversões personalizadas migraram da at.js `trackEvent` ou `sendNotifications` devem ter chamadas de evento separadas |
| Os tokens de resposta são retornados no `sendEvent` e ter valores esperados | Os tokens de resposta devem funcionar normalmente com o SDK da Web |
| As ECIDs são consistentes em páginas com o SDK da Web e a at.js | Aplica-se a migrações página por página. Não é esperado que as ofertas de redirecionamento funcionem nesses tipos de migração |


## Delivery e renderização de atividade

| Item de validação | Notas |
|---|---|
| As atividades baseadas em VEC são renderizadas adequadamente no carregamento da página | É melhor validar as modificações de código personalizado e as modificações básicas, como reorganizar elementos ou substituir texto |
| As atividades baseadas em VEC são renderizadas adequadamente nas alterações SPA exibição | Aplicável somente para implementações de SPA |
| As atividades baseadas em formulário são renderizadas adequadamente | Aplicável somente a determinadas implementações. A renderização de atividades baseadas em formulário requer código personalizado semelhante ao at.js. |
| As atividades que usam redirecionamentos funcionam corretamente | Os redirecionamentos serão suportados se as páginas de origem e de destino usarem o SDK da Web da plataforma. Um redirecionamento do Target de uma página da at.js para uma página da Web da plataforma ou da maneira oposta não é suportado. |
| As atividades que usam ofertas remotas funcionam corretamente | Não é comum, verifique o inventário de ofertas do Target para Ofertas remotas |
| A cintilação é devidamente mitigada | O manuseio de cintilação é opcional, mas garanta que todas as táticas de mitigação que você tenha em vigor estejam funcionando como esperado para obter o desempenho ideal da página e a experiência do usuário |
| Os links de controle de qualidade funcionam conforme esperado | Se não estiver funcionando, confirme se o web.webPageDetails.URL corresponde exatamente ao URL no navegador |
| Todos os tipos de ofertas comumente usados são renderizados como esperado |  |

## Relatórios

| Item de validação | Notas |
|---|---|
| Os visitantes são atribuídos a atividades baseadas em VEC | É melhor validar os trabalhos de relatório conforme esperado para modificações de carregamento de página e modificações de visualização de SPA |
| Os visitantes são atribuídos a atividades baseadas em formulário | Dependendo da abordagem de renderização usada, sua implementação pode exigir que o código personalizado execute uma `decisioning.propositionDisplay` evento |
| As metas de conversão padrão são capturadas corretamente | Aplica-se ao Target ou Analytics como a fonte de relatórios |
| As conversões e os detalhes do pedido são capturados corretamente | Verificar o relatório de Auditoria |
| As conversões de rastreamento de cliques são capturadas corretamente |  |
| As metas de conversão personalizadas são capturadas corretamente | Por exemplo, metas de conversão migradas da at.js `trackEvent` ou `sendNotifications` que são comumente usados com a meta de &quot;visualizar uma mbox&quot; |

## Públicos-alvo e scripts de perfil

| Item de validação | Notas |
|---|---|
| Os públicos-alvo usados em atividades ativas são compatíveis com o SDK da Web da plataforma | Os públicos-alvo que usam o componente &quot;Personalizado&quot; (parâmetro da mbox) devem ser atualizados para incluir atributos XDM |
| Todos os scripts de perfil são compatíveis com o SDK da Web da plataforma | Qualquer script de perfil que use parâmetros mbox deve ser atualizado para incluir atributos XDM |
| Retorno de atividades para públicos-alvo do Target | É melhor executar a validação completa em públicos-alvo modificados para tornar compatível com o SDK da Web da plataforma |
| Os scripts de perfil são avaliados como esperado | Exibir rastreamentos de borda no Debugger |

## Integrações com aplicativos Adobe

| Item de validação | Notas |
|---|---|
| Retorno de atividades para públicos-alvo do Experience Cloud | Por exemplo, um segmento publicado no Adobe Analytics |
| Retorno de atividades para públicos-alvo do Experience Platform | Aplica-se somente se você tiver uma licença para um aplicativo baseado em Experience Platform, como RTCDP |
| Retorno de atividades para públicos-alvo do Audience Manager | Por exemplo, um segmento baseado em visitar uma página específica |
| Os dados da atividade do Target são exibidos no Analysis Workspace | Aplica-se a atividades que usam o Adobe Analytics como fonte de relatórios |

## Integrações com aplicativos de terceiros

| Item de validação | Notas |
|---|---|
| Os dados do token de resposta são passados corretamente para aplicativos de terceiros | As abordagens de integração podem variar, mas um método comum é usar os tokens de resposta do Target para transmitir informações de atividade e experiência para outras ferramentas de análise, como o Google Analytics |
| As informações de terceiros são passadas como dados XDM ou de perfil | Todas as informações pertinentes de terceiros devem ser transmitidas `sendEvent` chamadas para o Target |

Depois de executar as etapas de validação acima, você pode ter certeza de que a implementação do SDK da Web da plataforma está pronta para migrar para a produção.

Em seguida, saiba como [solucionar problemas de uma implementação do Target usando o SDK da Web da plataforma](debugging.md).

>[!NOTE]
>
>Temos o compromisso de ajudar você a ser bem-sucedido com sua migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, informe-nos ao publicar em [este debate comunitário](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).