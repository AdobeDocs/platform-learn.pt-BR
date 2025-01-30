---
title: Visão geral da migração - Migrar do Adobe Target para o Adobe Journey Optimizer - Extensão móvel da decisão
description: Saiba mais sobre as principais diferenças entre a at.js e o Platform Web SDK e como planejar seu esforço de migração.
exl-id: 86849319-d2ad-4338-aa1a-d307d8807d4a
source-git-commit: 6e442413c178e76183f88454d97d3896f8efa8bc
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 1%

---

# Visão geral da migração do Target at.js para o Platform Web SDK

O nível de esforço para migrar da extensão do Target para a extensão do Decisioning depende da complexidade da implementação atual e dos recursos de produto usados.

Independentemente da simplicidade ou complexidade de sua implementação, é importante entender totalmente seu estado atual antes de migrar. Este guia ajuda a detalhar os componentes da implementação atual e desenvolver um plano gerenciável para migrar cada parte.

O processo de migração envolve as seguintes etapas principais:

1. Avalie sua implementação atual e determine uma abordagem de migração
1. Configure os componentes iniciais para conectar ao Edge Network Adobe Experience Platform
1. Atualize sua implementação para substituir o Target SDK pelo XYZ
1. Melhore a implementação do Platform Mobile SDK para seus casos de uso específicos. Isso pode envolver a transferência de parâmetros adicionais, XYZ.
1. Atualizar objetos na interface do Target, como scripts de perfil, atividades e definições de público??
1. Valide a implementação final antes de publicar seu aplicativo atualizado

## Principais diferenças entre a at.js e a Platform Web SDK

Antes de iniciar o processo de migração, é importante entender as diferenças entre a at.js e o Platform Web SDK.

### Diferenças operacionais

O Platform Web SDK combina a funcionalidade de vários aplicativos Adobe em uma única biblioteca. Essa abordagem unificada significa que você deve considerar as responsabilidades e os processos entre equipes para garantir uma implementação saudável.

| | at.js 2.x do Target | SDK da Web da Platform |
|---|---|---|
| Propriedade | A extensão do Target é independente dos outros SDKs de aplicativos (NÃO ACREDITE QUE ISSO SEJA VERDADEIRO PARA DISPOSITIVOS MÓVEIS). As personalizações e a propriedade dessas bibliotecas diferentes podem se alinhar a equipes diferentes na organização. | A biblioteca Web SDK da Platform e os dados transmitidos são unificados para todos os aplicativos Adobe. A propriedade da implementação do Platform Web SDK deve representar as partes interessadas de todos os aplicativos downstream. |
| Manutenção | Equipes separadas podem trabalhar nos aprimoramentos de implementação para cada aplicativo do Adobe, como Target e Analytics. | Idealmente, uma única equipe deve ser responsável pelas melhorias que afetam a implementação do Platform Web SDK. |
| Processo | As alterações em uma implementação do Target podem seguir um processo que tem uma cadência ou requisitos de controle de qualidade diferentes em comparação a outros aplicativos, como o Analytics. | As alterações na implementação de um Platform Web SDK devem considerar todos os aplicativos downstream e o processo de controle de qualidade e publicação deve ser ajustado de acordo. |
| Colaboração | Os dados específicos do Target podem ser transmitidos diretamente nas chamadas do Target. Dependendo da implementação, pode haver chamadas adicionais do Target. Isso não tem impacto direto nos dados do Adobe Analytics e a coordenação com a equipe de análise não é tão crítica. | Os dados transmitidos em chamadas do Platform Web SDK podem ser encaminhados para o Target e para o Analytics. É necessária coordenação entre as equipes para garantir que as alterações não afetem negativamente um aplicativo específico. |

### Diferenças técnicas

O Platform Web SDK não é uma evolução da biblioteca at.js do Target. É uma abordagem nova e unificada para implementar todos os aplicativos Adobe para o canal da Web. Há várias diferenças técnicas que devem ser consideradas.

| | at.js 2.x do Target | SDK da Web da Platform |
|---|---|---|
| Funcionalidade de biblioteca | A funcionalidade do Target fornecida pela at.js. Integrações com outros aplicativos fornecidos pelo Visitor.js e AppMeasurement.js | Funcionalidade para todos os aplicativos Adobe fornecidos por uma única biblioteca SDK da Web da plataforma: alloy.js |
| Desempenho | A at.js é uma das várias bibliotecas que devem ser carregadas para a integração adequada entre os aplicativos. Isso resulta em tempo de carregamento inferior ao ideal. | O Platform Web SDK é uma única biblioteca leve que elimina a necessidade de várias bibliotecas específicas do aplicativo, resultando em um melhor desempenho do carregamento da página. |
| Solicitações | Chamadas separadas para cada aplicativo Adobe. As chamadas do Target são em grande parte independentes das outras chamadas de rede. | Uma única chamada para todos os aplicativos Adobe. As alterações nos dados transmitidos nessas chamadas podem afetar vários aplicativos downstream. |
| Pedido de carregamento | A integração adequada com outros aplicativos Adobe requer uma ordem de carregamento específica de bibliotecas e chamadas de rede. | A integração adequada não depende da compilação de dados de chamadas de rede diferentes específicas do aplicativo, portanto, a ordem de carregamento não é uma preocupação. |
| Edge Network | Usa o Edge Network Adobe Experience Cloud (tt.omtrdc.net), opcionalmente com um CNAME específico do Target. | Usa o Edge Network Adobe Experience Platform (edge.adobedc.net), opcionalmente com um único CNAME. |
| Terminologia básica | Nomeação do at.js: <br> - `mbox` <br> - `pageLoad` evento (mbox global) <br> - `offer` | Equivalente ao Platform Web SDK: <br> - `decisionScope` <br> - `__view__` decisionScope <br> - `proposition` |

### Visão geral do vídeo

O vídeo a seguir fornece uma visão geral do Adobe Experience Platform Web SDK e do Adobe Experience Platform Edge Network.


Agora que você entende as diferenças de alto nível entre a at.js e o Platform Web SDK, você pode [planejar a migração](plan-migration.md).

>[!NOTE]
>
>Estamos empenhados em ajudá-lo a ser bem-sucedido na migração para dispositivos móveis do Target da extensão do Target para a extensão do Decisioning. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
