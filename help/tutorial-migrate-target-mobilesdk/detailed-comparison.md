---
title: Comparação da extensão do Target com a extensão do Decisioning
description: Saiba mais sobre as diferenças entre a extensão do Target e a extensão do Decisioning, incluindo recursos, funções, configurações e fluxo de dados.
source-git-commit: 78d04d625aa55ce5eb76615c220b49aefd958431
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 4%

---

# Comparação da extensão do Target com a extensão do Decisioning

A extensão do Adobe Journey Optimizer - Decisioning é diferente da extensão do Adobe Target para aplicativos móveis. As tabelas a seguir são uma referência para ajudar a avaliar as áreas da sua implementação nas quais talvez seja necessário se concentrar durante o processo de migração.

Depois de analisar as informações abaixo e avaliar a implementação da extensão técnica do Target atual, você deve ser capaz de entender o seguinte:

- Quais recursos do Target são compatíveis com o Adobe Journey Optimizer - Decisão
- Quais funções de extensão do Adobe Target têm equivalentes do Adobe Journey Optimizer - Decisão
- Como as configurações do Target são aplicadas com o Adobe Journey Optimizer - Decisão
- Como o fluxo de dados da extensão do Adobe Target e da extensão do Adobe Journey Optimizer - Decisão difere

Se você não estiver familiarizado com o SDK da Web da Platform, não se preocupe. Os itens abaixo são abordados com mais detalhes neste tutorial.

## Comparação de recursos

| Recurso | Extensão do Target | Extensão de decisão (Target via Edge) |
|---|---|---|
| Modo de busca prévia | Suportado | Suportado |
| Modo de execução | Suportado | Não suportado |
| Parâmetros personalizados | Suportado | Não há suporte para parâmetros por mbox |
| Audiências de entrada | Suportado | Suportado |
| Segmentação de público usando métricas móveis de ciclo de vida | Suportado | Compatível com as regras de Coleção de dados |
| thirdPartyId (mbox3rdPartyId) | Compatível com o Mapa de identidade e a configuração de namespace na sequência de dados |
| Notificações (exibir, clicar) | Suportado | Suportado |
| Tokens de resposta | Suportado | Suportado |
| Ofertas dinâmicas | Suportado | Suportado |
| Analytics for Target (A4T) | Somente no lado do cliente | Lado do cliente e lado do servidor |
| Visualizações móveis (modo de QA) | Suportado | Suporte limitado |



## Chamadas notáveis

>[!NOTE]
>
>Não há suporte para a migração do Target para o SDK da Web da Platform enquanto uma determinada página é mantida em uma implementação existente do AppMeasurement Adobe Analytics.
>
> É possível migrar sua implementação at.js (e AppMeasurement.js) para o SDK da Web da plataforma uma página por vez. Se você seguir esta abordagem, é melhor definir as opções [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) e [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) como `true` com o comando `configure`.

## Funções de extensão do Target e equivalentes da extensão do Decisioning

Muitas funções de extensão do Target têm uma abordagem equivalente usando a extensão do Decisioning descrita na tabela abaixo. Para obter mais detalhes sobre as [funções](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consulte o Guia do Desenvolvedor do Adobe Target.

| Extensão do Target | Extensão de decisão |
| --- | --- | 
| |  |

## Configurações de extensão do Target e equivalentes da extensão do Decisioning

A extensão do Target pode ser configurada e baixada com várias configurações no ...

| Extensão do Target | Extensão de decisão |
| --- | --- | 
| |  |


## Comparação do diagrama do sistema

Os diagramas a seguir devem ajudar você a entender as diferenças de fluxo de dados entre uma implementação do Target usando a extensão Adobe Journey Optimizer - Decisioning e uma implementação usando a extensão Adobe Target.

### Diagrama do sistema de extensão do Target



### Diagrama do sistema de extensão de decisão




>[!NOTE]
>
>Estamos empenhados em ajudá-lo a ser bem-sucedido na migração para dispositivos móveis do Target da extensão do Target para a extensão do Decisioning. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
