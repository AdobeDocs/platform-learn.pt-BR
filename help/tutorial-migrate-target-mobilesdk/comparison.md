---
title: Comparação entre a extensão do Target e a extensão do Offer Decisioning
description: Saiba mais sobre as diferenças entre a extensão do Target para a extensão do Offer Decisioning e do Target, incluindo recursos, funções, configurações e fluxo de dados.
exl-id: 6c854049-4126-45cf-8b2b-683cf29549f3
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 3%

---

# Comparação entre a extensão do Target e a extensão do Offer Decisioning

A extensão do Offer Decisioning e do Target é diferente da extensão do Adobe Target para aplicativos móveis. As tabelas a seguir são uma referência para ajudar a avaliar as áreas da sua implementação nas quais talvez seja necessário se concentrar durante o processo de migração.

Depois de analisar as informações abaixo e avaliar a implementação da extensão técnica do Target atual, você deve ser capaz de entender o seguinte:

- Quais recursos do Target são compatíveis com o Offer Decisioning e o Target
- Quais funções de extensão do Adobe Target têm equivalentes do Offer Decisioning e do Target
- Como as configurações do Target são aplicadas com o Offer Decisioning e o Target
- Como os dados fluem usando a extensão do Offer Decisioning e do Target

## Diferenças operacionais

| | Extensão do Target | Extensão do Offer Decisioning e do Target |
|---|---|---|
| Processo | As alterações em uma implementação do Target podem seguir um processo que tem uma cadência ou requisitos de controle de qualidade diferentes em comparação a outros aplicativos, como o Analytics. | As alterações em uma implementação de extensão do Offer Decisioning e do Target devem considerar todos os aplicativos downstream e o processo de controle de qualidade e publicação deve ser ajustado de acordo. |
| Colaboração | Os dados específicos do Target podem ser transmitidos diretamente nas chamadas do Target. Se a origem de relatório do Target for o Adobe Analytics (A4T), os dados específicos do Target também poderão ser passados para o Adobe Analytics quando os métodos de rastreamento apropriados na extensão do Target forem chamados para exibição de conteúdo e interação do Target. | Os dados transmitidos nas chamadas de extensão do Offer Decisioning e do Target podem ser encaminhados para o Target e para o Analytics se a origem de relatório do Target for o Adobe Analytics (A4T), o Adobe Analytics estiver habilitado no fluxo de dados e os métodos de rastreamento apropriados na extensão do Offer Decisioning e do Target forem chamados quando o conteúdo do Target for exibido e tiver interação com o. |

## Diferenças básicas

| | Extensão do Target | Extensão do Offer Decisioning e do Target |
|---|---|---|
| Dependências | Depende apenas do Mobile Core SDK | Depende do Mobile Core e do Edge Network SDK |
| Funcionalidade de biblioteca | Oferece suporte à busca de conteúdo somente do Adobe Target | Suporte para busca de conteúdo do Adobe Target e do Offer Decisioning |
| Solicitações | As chamadas do Target são em grande parte independentes de outras chamadas de rede | As chamadas de rede do Target são enfileiradas junto com chamadas de rede para outras soluções da Edge, como mensagens no Edge SDK, e executadas em série. |
| Edge Network | Usa o valor do servidor do Target ou o Edge Network do Adobe Experience Cloud com o código de cliente (clientcode.tt.omtrdc.net), ambos especificados na [Configuração do Target](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui) na interface da Coleção de Dados | Usa o domínio de rede Edge especificado na [configuração do Edge Network](https://developer.adobe.com/client-sdks/edge/edge-network/#configure-the-edge-network-extension-in-data-collection-ui) da Adobe Experience Platform na interface da Coleção de dados. |
| Terminologia básica | mbox, TargetParameters | DecisionScope, Map (Android)/dicionário (iOS) para parâmetros do Target |
| Conteúdo padrão | Permite transmitir conteúdo padrão do lado do cliente no TargetRequest, que é retornado se a chamada de rede falhar ou resultar em erro. | Não permite transmitir conteúdo padrão do lado do cliente. Não retorna conteúdo se uma chamada de rede falhar ou resultar em erro. |
| Parâmetros do Target | Permite transmitir TargetParameters globais por solicitação e diferentes TargetParameters por mbox | Permite transmitir TargetParameters globais apenas por solicitação |



## Comparação de recursos

| Recurso | Extensão do Target | Extensão do Offer Decisioning e do Target (Target via Edge) |
|---|---|---|
| Modo de busca prévia | Suportado | Suportado |
| Modo de execução | Suportado | Incompatível |
| Parâmetros personalizados | Suportado | Compatível* |
| Parâmetros do perfil | Suportado | Compatível* |
| Parâmetros de entidade | Suportado | Compatível* |
| Públicos-alvo | Suportado | Suportado |
| Públicos da Real-Time CDP | Não suportado | Suportado |
| Atributos do Real-Time CDP | Não suportado | Suportado |
| Medições de ciclo de vida | Suportado | Compatível com as regras de Coleção de dados |
| thirdPartyId (mbox3rdPartyId) | Suportado | Compatível com o Mapa de identidade e o Namespace de ID de terceiros no fluxo de dados |
| Notificações (exibir, clicar) | Suportado | Suportado |
| Tokens de resposta | Suportado | Suportado |
| Visualizações móveis (modo de QA) | Suportado | Suporte limitado com o Assurance |

>[!IMPORTANT]
>
> \* Os parâmetros enviados em uma solicitação se aplicam a todos os escopos na solicitação. Se você precisar definir parâmetros diferentes para escopos diferentes, faça solicitações adicionais.



## Chamadas notáveis

>[!NOTE]
>
>Mantenha a configuração e as configurações das Tags de extensão do Target em vigor mesmo após migrar o código do aplicativo para a extensão do Offer Decisioning e do Target. Isso ajudará a garantir que o Target continue a funcionar para clientes que ainda não atualizaram o aplicativo para a nova versão.
>
>Se você usar a integração do Analytics for Target (A4T), migre também sua implementação do Analytics com a extensão do Edge Bridge ao mesmo tempo em que migra sua implementação do Target para a extensão do Offer Decisioning e do Target.





>[!IMPORTANT]
>
> Mantenha as configurações da extensão do Target em vigor mesmo depois de migrar o código do aplicativo para a extensão do Offer Decisioning e do Target. Isso ajudará a garantir que o Target continue a funcionar para usuários que ainda não atualizaram seus aplicativos.

## Diagrama do sistema de extensões do Offer Decisioning e do Target

O diagrama a seguir deve ajudar você a entender o fluxo de dados usando a extensão do Offer Decisioning e do Target.

![Decisão do Adobe Target Edge com o Mobile SDK do lado do cliente](assets/diagram.png)


>[!NOTE]
>
>Estamos empenhados em ajudá-lo a ser bem-sucedido na migração para dispositivos móveis do Target da extensão do Target para a extensão do Offer Decisioning e do Target. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484?profile.language=pt#M625).
