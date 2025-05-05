---
title: Visão geral da migração - Migrar o Target da at.js 2.x para o Web SDK
description: Saiba mais sobre as principais diferenças entre a at.js e o Platform Web SDK e como planejar seu esforço de migração.
exl-id: a8ed78e4-c8c2-4505-b4b5-e5d508f5ed87
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 1%

---

# Visão geral da migração do Target at.js para o Platform Web SDK

O nível de esforço para migrar da at.js para o Platform Web SDK depende da complexidade da implementação atual e dos recursos de produto usados.

Independentemente da simplicidade ou complexidade de sua implementação, é importante entender totalmente seu estado atual antes de migrar. Este guia ajuda a detalhar os componentes da implementação atual e desenvolver um plano gerenciável para migrar cada parte.

O processo de migração envolve as seguintes etapas principais:

1. Avalie sua implementação atual e determine uma abordagem de migração
1. Configurar os componentes iniciais para se conectar ao Adobe Experience Platform Edge Network
1. Atualize a implementação básica para substituir a at.js pelo Platform Web SDK
1. Melhore a implementação do Platform Web SDK para seus casos de uso específicos. Isso pode envolver a transmissão de parâmetros adicionais, a contabilização de alterações de exibição de aplicativo de página única (SPA), o uso de tokens de resposta e muito mais.
1. Atualizar objetos na interface do Target, como scripts de perfil, atividades e definições de público-alvo
1. Valide a implementação final antes de fazer o switch no ambiente de produção

## Principais diferenças entre a at.js e a Platform Web SDK

Antes de iniciar o processo de migração, é importante entender as diferenças entre a at.js e o Platform Web SDK.

### Diferenças operacionais

O Platform Web SDK combina a funcionalidade de vários aplicativos da Adobe em uma única biblioteca. Essa abordagem unificada significa que você deve considerar as responsabilidades e os processos entre equipes para garantir uma implementação saudável.

| | at.js 2.x do Target | SDK da Web da Platform |
|---|---|---|
| Propriedade | A biblioteca da at.js é independente de outras bibliotecas de aplicativos. As personalizações e a propriedade dessas bibliotecas diferentes podem se alinhar a equipes diferentes na organização. | A biblioteca Web SDK da Platform e os dados transmitidos são unificados para todos os aplicativos da Adobe. A propriedade da implementação do Platform Web SDK deve representar as partes interessadas de todos os aplicativos downstream. |
| Manutenção | Equipes separadas podem trabalhar nos aprimoramentos de implementação para cada aplicativo do Adobe, como Target e Analytics. | Idealmente, uma única equipe deve ser responsável pelas melhorias que afetam a implementação do Platform Web SDK. |
| Processo | As alterações em uma implementação do Target podem seguir um processo que tem uma cadência ou requisitos de controle de qualidade diferentes em comparação a outros aplicativos, como o Analytics. | As alterações na implementação de um Platform Web SDK devem considerar todos os aplicativos downstream e o processo de controle de qualidade e publicação deve ser ajustado de acordo. |
| Colaboração | Os dados específicos do Target podem ser transmitidos diretamente nas chamadas do Target. Dependendo da implementação, pode haver chamadas adicionais do Target. Isso não tem impacto direto nos dados do Adobe Analytics e a coordenação com a equipe de análise não é tão crítica. | Os dados transmitidos em chamadas do Platform Web SDK podem ser encaminhados para o Target e para o Analytics. É necessária coordenação entre as equipes para garantir que as alterações não afetem negativamente um aplicativo específico. |

### Diferenças técnicas

O Platform Web SDK não é uma evolução da biblioteca at.js do Target. É uma abordagem nova e unificada para implementar todos os aplicativos Adobe para o canal da Web. Há várias diferenças técnicas que devem ser consideradas.

| | at.js 2.x do Target | SDK da Web da Platform |
|---|---|---|
| Funcionalidade de biblioteca | A funcionalidade do Target fornecida pela at.js. Integrações com outros aplicativos fornecidos pelo Visitor.js e AppMeasurement.js | Funcionalidade para todos os aplicativos da Adobe fornecida por uma única biblioteca SDK da Platform Web: alloy.js |
| Desempenho | A at.js é uma das várias bibliotecas que devem ser carregadas para a integração adequada entre os aplicativos. Isso resulta em tempo de carregamento inferior ao ideal. | O Platform Web SDK é uma única biblioteca leve que elimina a necessidade de várias bibliotecas específicas do aplicativo, resultando em um melhor desempenho do carregamento da página. |
| Solicitações | Chamadas separadas para cada aplicativo do Adobe. As chamadas do Target são em grande parte independentes das outras chamadas de rede. | Uma única chamada para todos os aplicativos da Adobe. As alterações nos dados transmitidos nessas chamadas podem afetar vários aplicativos downstream. |
| Pedido de carregamento | A integração adequada com outros aplicativos da Adobe requer uma ordem de carregamento específica de bibliotecas e chamadas de rede. | A integração adequada não depende da compilação de dados de chamadas de rede diferentes específicas do aplicativo, portanto, a ordem de carregamento não é uma preocupação. |
| Edge Network | Usa o Edge Network do Adobe Experience Cloud (tt.omtrdc.net), opcionalmente com um CNAME específico do Target. | Usa o Adobe Experience Platform Edge Network (edge.adobedc.net), opcionalmente com um único CNAME. |
| Terminologia básica | Nomeação do at.js: <br> - `mbox` <br> - `pageLoad` evento (mbox global) <br> - `offer` | Equivalente ao Platform Web SDK: <br> - `decisionScope` <br> - `__view__` decisionScope <br> - `proposition` |

### Visão geral do vídeo

O vídeo a seguir fornece uma visão geral do Adobe Experience Platform Web SDK e do Adobe Experience Platform Edge Network.

>[!VIDEO](https://video.tv.adobe.com/v/37265/?learn=on&enablevpops&captions=por_br)

Agora que você entende as diferenças de alto nível entre a at.js e o Platform Web SDK, você pode [planejar a migração](plan-migration.md).

>[!NOTE]
>
>Estamos empenhados em ajudá-lo a ter sucesso com a migração do Target da at.js para o Web SDK. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=pt#M463).
