---
title: Comparação da extensão do Target com a extensão do Decisioning
description: Saiba mais sobre as diferenças entre a extensão do Target e a extensão do Decisioning, incluindo recursos, funções, configurações e fluxo de dados.
exl-id: 6c854049-4126-45cf-8b2b-683cf29549f3
source-git-commit: 8e4e23413c842f84159891287d09e8a6cfbbbc53
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 5%

---

# Comparação da extensão do Target com a extensão do Decisioning

A extensão do Adobe Journey Optimizer - Decisioning é diferente da extensão do Adobe Target para aplicativos móveis. As tabelas a seguir são uma referência para ajudar a avaliar as áreas da sua implementação nas quais talvez seja necessário se concentrar durante o processo de migração.

Depois de analisar as informações abaixo e avaliar a implementação da extensão técnica do Target atual, você deve ser capaz de entender o seguinte:

- Quais recursos do Target são compatíveis com o Adobe Journey Optimizer - Decisão
- Quais funções de extensão do Adobe Target têm equivalentes do Adobe Journey Optimizer - Decisão
- Como as configurações do Target são aplicadas com o Adobe Journey Optimizer - Decisão
- Como os dados fluem usando a extensão Adobe Journey Optimizer - Decisão


## Comparação de recursos

| Recurso | Extensão do Target | Extensão de decisão (Target via Edge) |
|---|---|---|
| Modo de busca prévia | Suportado | Suportado |
| Modo de execução | Suportado | Não suportado |
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
| Analytics for Target (A4T) | Somente no lado do cliente | Lado do cliente e lado do servidor |
| Visualizações móveis (modo de QA) | Suportado | Suporte limitado com o Assurance |

>[!IMPORTANT]
>
> \* Os parâmetros enviados em uma solicitação se aplicam a todos os escopos na solicitação. Se você precisar definir parâmetros diferentes para escopos diferentes, faça solicitações adicionais.



## Chamadas notáveis

>[!NOTE]
>
>Mantenha a configuração e as configurações das Tags de extensão do Target em vigor mesmo depois de migrar seu código de aplicativo para a extensão do Decisioning. Isso ajudará a garantir que o Target continue a funcionar para clientes que ainda não atualizaram o aplicativo para a nova versão.
>
>Se você usar a integração do Analytics for Target (A4T), certifique-se também de migrar sua implementação do Analytics com a extensão do Edge Bridge ao mesmo tempo em que migra sua implementação do Target para a extensão do Decisioning.

## Funções de extensão do Target e equivalentes da extensão do Decisioning

Muitas funções de extensão do Target têm uma abordagem equivalente usando a extensão do Decisioning descrita na tabela abaixo. Para obter mais detalhes sobre as [funções](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consulte o Guia do Desenvolvedor do Adobe Target.

| Extensão do Target | Extensão de decisão | Notas |
| --- | --- | --- | 
| `prefetchContent` | `updatePropositions` |  |
| `retrieveLocationContent` | `getPropositions` | Ao usar a API `getPropositions`, não é feita nenhuma chamada remota para buscar escopos não armazenados em cache no SDK. |
| `displayedLocations` | Oferta -> `displayed()` | Além disso, o método de oferta `generateDisplayInteractionXdm` pode ser usado para gerar o XDM para exibição de item. Posteriormente, a API sendEvent do SDK de rede da Edge pode ser usada para anexar dados XDM adicionais e de formato livre, e enviar um Evento de experiência ao remoto. |
| `clickedLocation` | Oferta -> `tapped()` | Além disso, o método de oferta `generateTapInteractionXdm` pode ser usado para gerar o XDM para toque de item. Posteriormente, a API sendEvent do SDK de rede da Edge pode ser usada para anexar dados XDM adicionais e de formato livre, e enviar um Evento de experiência ao remoto. |
| `clearPrefetchCache` | `clearCachedPropositions` |  |
| `resetExperience` | n/d | Use a API `removeIdentity` da identidade para a extensão Edge Network para o SDK parar de enviar o identificador de visitante para a rede Edge. Para obter mais detalhes, consulte [a documentação da API removeIdentity](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity). <br><br>Observação: a API `resetIdentities` do Mobile Core apaga todas as identidades armazenadas no SDK, incluindo a Experience Cloud ID (ECID), e ela deve ser usada com moderação! |
| `getSessionId` | n/d | O identificador de resposta `state:store` carrega informações relacionadas à sessão. A extensão de rede do Edge ajuda a gerenciá-la anexando itens de armazenamento de estado não expirados a solicitações subsequentes. |
| `setSessionId` | n/d | O identificador de resposta `state:store` carrega informações relacionadas à sessão. A extensão de rede do Edge ajuda a gerenciá-la anexando itens de armazenamento de estado não expirados a solicitações subsequentes. |
| `getThirdPartyId` | n/d | Use a API updateIdentities da extensão Identity for Edge Network para fornecer o valor da ID de terceiros. Em seguida, configure o namespace da ID de terceiros no fluxo de dados. Para obter mais detalhes, consulte [a documentação móvel da ID de terceiros do Target](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `setThirdPartyId` | n/d | Use a API updateIdentities da extensão Identity for Edge Network para fornecer o valor da ID de terceiros. Em seguida, configure o namespace da ID de terceiros no fluxo de dados. Para obter mais detalhes, consulte [a documentação móvel da ID de terceiros do Target](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `getTntId` | n/d | O identificador de resposta `locationHint:result` carrega as informações de dica de localização do Target. Presume-se que a borda do Target esteja co-localizada com a Experience Edge. <br> <br>A extensão de rede do Edge usa a dica de local do EdgeNetwork para determinar o cluster de rede da Edge para o qual enviar solicitações. Para compartilhar a dica de local de rede do Edge entre SDKs (aplicativos híbridos), use as APIs do `getLocationHint` e do `setLocationHint` da extensão Edge Network. Para obter mais detalhes, consulte [a `getLocationHint` documentação da API](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |
| `setTntId` | n/d | O identificador de resposta `locationHint:result` carrega as informações de dica de localização do Target. Presume-se que a borda do Target esteja co-localizada com a Experience Edge. <br> <br>A extensão de rede do Edge usa a dica de local do EdgeNetwork para determinar o cluster de rede da Edge para o qual enviar solicitações. Para compartilhar a dica de local de rede do Edge entre SDKs (aplicativos híbridos), use as APIs do `getLocationHint` e do `setLocationHint` da extensão Edge Network. Para obter mais detalhes, consulte [a `getLocationHint` documentação da API](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |

## Configurações de extensão do Target e equivalentes da extensão do Decisioning

A extensão do Target tem [configurações configuráveis](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui) que são [configuradas na sequência de dados](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#adobe-experience-platform-data-collection-setup) com a extensão de Decisão.

| Extensão do Target | Extensão de decisão | Notas |
| --- | --- | --- | 
| Código do cliente | n/d | Definido automaticamente pela borda usando os detalhes da Organização IMS |
| ID do ambiente | ID do ambiente de destino | Configurado na sequência de dados |
| Propriedade do Workspace de destino | Token de propriedade | Configurado na sequência de dados |
| Tempo limite | Não configurável | O tempo limite da extensão do Decisioning é de 10 segundos |
| Domínio do servidor | domínio Edge Network | Definido na extensão Adobe Experience Platform Edge Network |

>[!IMPORTANT]
>
> Mantenha as configurações de extensão do Target em vigor mesmo após ter migrado seu código de aplicativo para a extensão do Decisioning. Isso ajudará a garantir que o Target continue a funcionar para usuários que ainda não atualizaram seus aplicativos.

## Diagrama do sistema de extensão de decisão

O diagrama a seguir deve ajudar você a entender o fluxo de dados usando a extensão Adobe Journey Optimizer - Decisioning.

![Decisão do Adobe Target Edge com o SDK móvel do lado do cliente](assets/diagram.png)


>[!NOTE]
>
>Estamos empenhados em ajudá-lo a ser bem-sucedido na migração para dispositivos móveis do Target da extensão do Target para a extensão do Decisioning. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
