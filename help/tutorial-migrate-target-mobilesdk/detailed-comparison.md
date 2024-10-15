---
title: Comparação da extensão do Target com a extensão Otimize
description: Saiba mais sobre as diferenças entre a at.js 2.x e o SDK da Web da plataforma, incluindo recursos, funções, configurações e fluxo de dados.
source-git-commit: 009548969b88d1bfa6eac23f65b1ca2144f27c34
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 4%

---

# Comparação da extensão do Target com a extensão Otimize

A biblioteca at.js independente do Adobe Target é significativamente diferente do SDK da Web da plataforma. As tabelas a seguir são uma referência para ajudar a avaliar as áreas da sua implementação nas quais talvez seja necessário se concentrar durante o processo de migração.

Depois de revisar as informações abaixo e avaliar sua implementação técnica atual da at.js, você deve ser capaz de entender o seguinte:

- Quais recursos do Target são compatíveis com o SDK da Web da plataforma
- Quais funções da at.js têm equivalentes do SDK da Web da plataforma.
- Como as configurações do Target são aplicadas com o SDK da Web da plataforma
- Como o fluxo de dados da at.js e do SDK da Web da Platform difere

Se você não estiver familiarizado com o SDK da Web da Platform, não se preocupe. Os itens abaixo são abordados com mais detalhes neste tutorial.

## Comparação de recursos

| | Extensão do Target | Extensão Otimize (Target via Edge) | Experiências baseadas em código do AJO (SDK de mensagens) |
|---|---|---|---|
| Modo de busca prévia | Suportado | Suportado | Suportado |
| Modo de execução | Suportado | Não suportado | Não suportado |
| Parâmetros personalizados | Suportado | Não há suporte para parâmetros por mbox | Não suportado |
| Audiências de entrada | Suportado | Suportado | Compatível por meio do público-alvo do Campaign e da configuração de validação de experimento |
| Segmentação de público usando métricas móveis de ciclo de vida | Suportado | Compatível com as regras de Coleção de dados | No momento, o direcionamento de experiência não é compatível |
| thirdPartyId (mbox3rdPartyId) | Compatível com o Mapa de identidade e a configuração de namespace na sequência de dados | Não suportado |
| Notificações (exibir, clicar) | Suportado | Suportado | Suportado |
| Tokens de resposta | Suportado | Suportado | Nenhum equivalente para retornar metadados específicos do Campaign fora do conteúdo |
| Ofertas dinâmicas | Suportado | Suportado | A renderização de token relacionado ao perfil e ao item de decisão no conteúdo é compatível |
| Analytics for Target (A4T) | Somente no lado do cliente | Lado do cliente e lado do servidor | Não suportado |
| Visualizações móveis (modo de QA) | Suportado | Suporte limitado | Em progresso |



## Chamadas notáveis

>[!NOTE]
>
>Não há suporte para a migração do Target para o SDK da Web da Platform enquanto uma determinada página é mantida em uma implementação existente do AppMeasurement Adobe Analytics.
>
> É possível migrar sua implementação at.js (e AppMeasurement.js) para o SDK da Web da plataforma uma página por vez. Se você seguir esta abordagem, é melhor definir as opções [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) e [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) como `true` com o comando `configure`.

## Funções de extensão do Target e equivalentes da extensão do Otimize

Muitas funções de extensão do Target têm uma abordagem equivalente usando a extensão Otimize descrita na tabela abaixo. Para obter mais detalhes sobre as [funções](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consulte o Guia do Desenvolvedor do Adobe Target.

| Extensão do Target | Otimizar extensão |
| --- | --- | 
| |  |

## Configurações de extensão do Target e equivalentes da extensão Otimizar

A extensão do Target pode ser configurada e baixada com várias configurações no ...

| Extensão do Target | Otimizar extensão |
| --- | --- | 
| |  |


## Comparação do diagrama do sistema

Os diagramas a seguir devem ajudar você a entender as diferenças de fluxo de dados entre uma implementação do Target usando at.js e uma implementação usando o SDK da Web da plataforma.

### Diagrama do sistema de extensão do Target



### Otimizar o diagrama de sistema da extensão




>[!NOTE]
>
>Estamos empenhados em ajudá-lo a ser bem-sucedido na migração para dispositivos móveis do Target da extensão do Target para a extensão do Otimize. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
