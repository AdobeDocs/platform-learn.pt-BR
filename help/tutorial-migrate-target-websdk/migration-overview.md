---
title: Visão geral da migração | Migrar o Target da at.js 2.x para o SDK da Web
description: Saiba mais sobre as principais diferenças entre o at.js e o SDK da Web da plataforma e como planejar seu esforço de migração.=
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 1%

---

# Visão geral da migração do at.js para o SDK da Web da plataforma

O nível de esforço para migrar da at.js para o SDK da Web da plataforma depende da complexidade de sua implementação atual e dos recursos de produto usados.

Não importa o quão simples ou complexa sua implementação seja, é importante entender totalmente seu estado atual antes de migrar. Este guia ajuda você a detalhar os componentes da implementação atual e desenvolver um plano gerenciável para migrar cada parte.

O processo de migração envolve as seguintes etapas principais:

1. Avaliar sua implementação atual e determinar uma abordagem de migração
1. Configure os componentes iniciais para se conectar à rede de borda da Adobe Experience Platform
1. Atualize a implementação fundamental para substituir at.js pelo SDK da Web da plataforma
1. Aprimore a implementação do SDK da Web da plataforma para seus casos de uso específicos. Isso pode envolver a transmissão de parâmetros adicionais, contabilização de alterações de visualização de aplicativo de página única (SPA), uso de tokens de resposta e muito mais.
1. Atualizar objetos na interface do Target, como scripts de perfil, atividades e definições de público-alvo
1. Valide a implementação final antes de fazer o switch no ambiente de produção

## Principais diferenças entre o at.js e o SDK da Web da plataforma

Antes de iniciar o processo de migração, é importante entender as diferenças entre o at.js e o SDK da Web da plataforma.

### Diferenças operacionais

O SDK da Web da plataforma combina a funcionalidade de vários aplicativos Adobe em uma única biblioteca. Essa abordagem unificada significa que você deve considerar as responsabilidades e os processos entre equipes para garantir uma implementação saudável.

|  | Target at.js 2.x | SDK da Web da Platform |
|---|---|---|
| Propriedade | A biblioteca at.js é independente de outras bibliotecas de aplicativos. As personalizações e a propriedade dessas bibliotecas diferentes podem se alinhar a equipes diferentes na organização. | A biblioteca do SDK da Web da plataforma e os dados transmitidos são unificados para todos os aplicativos do Adobe. A propriedade da implementação do SDK da Web da plataforma deve representar os participantes de todos os aplicativos downstream. |
| Manutenção | Equipes separadas podem trabalhar nos aprimoramentos de implementação para cada aplicativo do Adobe, como Target e Analytics. | Idealmente, uma única equipe deve ser responsável por aprimoramentos que afetam a implementação do SDK da Web da plataforma. |
| Processo | As alterações em uma implementação do Target podem seguir um processo que tem uma cadência diferente ou requisitos de controle de qualidade em comparação a outros aplicativos como o Analytics. | As alterações em uma implementação do SDK da Web da plataforma devem considerar todos os aplicativos downstream e o processo de QA e publicação deve ser ajustado adequadamente. |
| Colaboração | Os dados específicos do Target podem ser transmitidos diretamente nas chamadas do Target. Dependendo da implementação, pode haver chamadas adicionais do Target. Isso não tem impacto direto nos dados do Adobe Analytics e a coordenação com a equipe de análise não é tão crítica. | Os dados transmitidos nas chamadas do SDK da Web da plataforma podem ser encaminhados para o Target e o Analytics. A coordenação entre equipes é necessária para garantir que as alterações não tenham um impacto negativo em um aplicativo específico. |

### Diferenças técnicas

O SDK da Web da plataforma não é uma evolução da biblioteca at.js do Target. É uma abordagem nova e unificada para implementar todos os aplicativos Adobe para o canal da Web. Há várias diferenças técnicas a serem observadas.

|  | Target at.js 2.x | SDK da Web da Platform |
|---|---|---|
| Funcionalidade da biblioteca | Funcionalidade do Target fornecida pela at.js. Integrações com outros aplicativos fornecidos por Visitor.js e AppMeasurement.js | Funcionalidade para todos os aplicativos Adobe fornecidos por uma única biblioteca do SDK da Web da plataforma: alloy.js |
| Desempenho | A at.js é uma das várias bibliotecas que devem ser carregadas para a integração correta entre aplicativos. Isso resulta em menos do que o tempo de carregamento ideal. | O SDK da Web da plataforma é uma única biblioteca leve que remove a necessidade de várias bibliotecas específicas do aplicativo, resultando em melhor desempenho de carregamento de página. |
| Solicitações | Chamadas separadas para cada aplicativo do Adobe. As chamadas do Target são em grande parte independentes de outras chamadas de rede. | Uma única chamada para todos os aplicativos Adobe. As alterações nos dados transmitidos nessas chamadas podem afetar vários aplicativos downstream. |
| Pedido de carregamento | A integração adequada com outros aplicativos Adobe requer uma ordem de carregamento específica de bibliotecas e chamadas de rede. | A integração adequada não depende da combinação de dados de chamadas de rede específicas de aplicativos diferentes, portanto, a ordem de carregamento não é uma preocupação. |
| Rede Edge | Usa a Rede de borda da Adobe Experience Cloud (tt.omtrdc.net), opcionalmente com um CNAME específico para o Target. | Usa a Rede de borda da Adobe Experience Platform (edge.adobedc.net), opcionalmente com um único CNAME. |
| Terminologia básica | Nomeação da at.js: <br> - `mbox` <br> - `pageLoad` event (mbox global) <br> - `offer` | Equivalente ao SDK da Web da plataforma: <br> - `decisionScope` <br> - `__view__` decisionScope <br> - `proposition` |

### Vídeo de visão geral

O vídeo a seguir fornece uma visão geral do SDK da Web da Adobe Experience Platform e da Rede de borda da Adobe Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/34141/?quality=12&learn=on)

Agora que você entende as diferenças de alto nível entre o at.js e o SDK da Web da plataforma, é possível [planejar a migração](plan-migration.md).

>[!NOTE]
>
>Temos o compromisso de ajudar você a ser bem-sucedido com sua migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, informe-nos ao publicar em [este debate comunitário](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).