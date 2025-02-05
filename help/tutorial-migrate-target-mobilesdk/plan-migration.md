---
title: Planejar a migração - Migrar do Adobe Target para o Adobe Journey Optimizer - Extensão móvel da decisão
description: Saiba mais sobre as principais diferenças entre a at.js e o Platform Web SDK e como planejar seu esforço de migração.
exl-id: 86849319-d2ad-4338-aa1a-d307d8807d4a
source-git-commit: f3fd5f45412900dcb871bc0b346ce89108fa8913
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---

# Planejar a migração

O nível de esforço para migrar da extensão do Target para a extensão do Decisioning depende da complexidade da implementação atual e dos recursos de produto usados.

Independentemente da simplicidade ou complexidade de sua implementação, é importante entender totalmente seu estado atual antes de migrar. Este guia ajuda a detalhar os componentes da implementação atual e desenvolver um plano gerenciável para migrar cada parte.

O processo de migração envolve as seguintes etapas principais:

1. Avalie sua implementação atual e determine uma abordagem de migração
1. Configure os componentes iniciais para conectar ao Edge Network Adobe Experience Platform
1. Atualize a implementação básica para substituir a extensão do Target e a extensão do Decisioning
1. Melhore a implementação Otimizar o SDK para seus casos de uso específicos. Isso pode envolver a transmissão de parâmetros adicionais, o uso de tokens de resposta e muito mais.
1. Atualizar objetos na interface do Target, como scripts de perfil, atividades e definições de público-alvo
1. Valide a implementação final antes de fazer o switch no ambiente de produção

## Principais diferenças entre a extensão do Target e a extensão do Decisioning

Antes de iniciar o processo de migração, é importante entender as diferenças entre a extensão do Target e a extensão do Decisioning.

### Diferenças operacionais

| | at.js 2.x do Target | SDK da Web da Platform |
|---|---|---|
| Processo | As alterações em uma implementação do Target podem seguir um processo que tem uma cadência ou requisitos de controle de qualidade diferentes em comparação a outros aplicativos, como o Analytics. | As alterações na implementação de uma extensão do Decisioning devem considerar todos os aplicativos downstream e o processo de controle de qualidade e publicação deve ser ajustado de acordo. |
| Colaboração | Os dados específicos do Target podem ser transmitidos diretamente nas chamadas do Target. Se a fonte de relatórios do Target for o Adobe Analytics, os dados específicos do Target também poderão ser passados para o Adobe Analytics quando os métodos de rastreamento apropriados na extensão do Target forem chamados para exibição de conteúdo e interação do Target. | Os dados transmitidos nas chamadas de extensão do Decisioning podem ser encaminhados para o Target e para o Analytics se a fonte de relatórios do Target for o Adobe Analytics, o Adobe Analytics estiver habilitado no fluxo de dados e os métodos de rastreamento apropriados na extensão do Decisioning forem chamados quando o conteúdo do Target for exibido e tiver interação com o. |

### Diferenças técnicas

| | Extensão do Target | Extensão de decisão |
|---|---|---|
| Dependências | Depende apenas do Mobile Core SDK | Depende do Mobile Core e do Edge Network SDK |
| Funcionalidade de biblioteca | Oferece suporte à busca de conteúdo somente do Adobe Target | Suporte para busca de conteúdo do Adobe Target e do Offer decisioning |
| Solicitações | As chamadas do Target são em grande parte independentes de outras chamadas de rede | As chamadas de rede do Target são enfileiradas junto com chamadas de rede para outras soluções da Edge, como mensagens no Edge SDK, e executadas em série. |
| Edge Network | Usa o valor do servidor Target ou o Edge Network Adobe Experience Cloud com o código de cliente (clientcode.tt.omtrdc.net), ambos especificados na [Configuração do Target](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui) na interface da Coleção de Dados | Usa o domínio de rede Edge especificado na [configuração de Edge Network](https://developer.adobe.com/client-sdks/edge/edge-network/#configure-the-edge-network-extension-in-data-collection-ui) do Adobe Experience Platform na interface da Coleção de dados. |
| Terminologia básica | mbox, TargetParameters | DecisionScope, Map (Android)/dicionário (iOS) para parâmetros de destino |
| Conteúdo padrão | Permite transmitir conteúdo padrão do lado do cliente no TargetRequest, que é retornado se a chamada de rede falhar ou resultar em erro. | Não permite transmitir conteúdo padrão do lado do cliente. Não retorna conteúdo se uma chamada de rede falhar ou resultar em erro. |
| Parâmetros do Target | Permite transmitir TargetParameters globais por solicitação e diferentes TargetParameters por mbox | Permite transmitir TargetParameters globais apenas por solicitação |

Em seguida, analise a [comparação detalhada entre a extensão do Target e a extensão do Decisioning](detailed-comparison.md) para obter uma melhor compreensão das diferenças técnicas e identificar áreas que exigem foco adicional.

>[!NOTE]
>
>Estamos empenhados em ajudá-lo a ser bem-sucedido na migração para dispositivos móveis do Target da extensão do Target para a extensão do Decisioning. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
