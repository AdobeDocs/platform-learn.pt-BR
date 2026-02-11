---
title: IA do cliente - Painel de pontuação e segmentação (previsão e ação)
description: IA do cliente - Painel de pontuação e segmentação (previsão e ação)
kt: 5342
doc-type: tutorial
exl-id: a6df3ff1-f907-4185-8189-f0b39c67c943
source-git-commit: 2d5ca888eb24c1f65b4ecd48030ec8d1659b7f84
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---

# 2.2.3 IA do cliente: painel de pontuação e segmentação (previsão e ação)

Depois que a instância da IA do cliente concluir uma execução de modelo, ela permitirá visualizar a pontuação de propensão avaliada para prever um cliente que realizará uma compra nos próximos 30 dias.

![IA](./images/caiinstancesummary1.png)

>[!NOTE]
>
>Somente uma instância da IA do cliente com status de **Sucesso** permitirá que você visualize os insights do serviço.

## Previsão de propensão

Agora vamos analisar a propensão prevista gerada pelo modelo de instância da IA do cliente. Clique no nome da instância para exibir o painel.

![IA](./images/caimodels1.png)

O painel IA do cliente mostra o resumo sobre pontuação, distribuição de população e os fatores influentes para o modelo avaliar.

![Descrição da IA](./images/caidescription.png)

Passe o mouse sobre os fatores influentes para ver o detalhamento da distribuição de dados.

![Fatores de influência](./images/caiinfluencefactors.png)

## Ações comerciais

### Segmentação de clientes

O painel IA do cliente permite definir segmentos com um único clique. Clique no botão **Criar segmento** nos cartões de propensão.

![Criar um segmento](./images/caiinfluencefactors1.png)

Você verá que uma definição de segmento é criada automaticamente.

![Regra de segmento](./images/caicreatesegment.png)

Nomeie seu segmento, seguindo esta convenção de nomenclatura: `--aepUserLdap-- - Customer AI High Propensity`. Clique em **Publicar**.

![Regra de segmento](./images/caicreatesegment1.png)

Agora você pode usar esse segmento para direcionamento usando, por exemplo, a Real-time CDP, o Journey Optimizer e o Adobe Target.

## Cleanup

Para garantir que nenhum dado de demonstração desnecessário seja mantido em seu ambiente, exclua o conjunto de dados `--aepUserLdap-- - Demo System - Customer Experience Event Dataset` depois de concluir este exercício com êxito. Se você não excluir os dados de demonstração, haverá um impacto de custo para sua instância do AEP.

![Perfil](./images/cleanup.png)

## Próximas etapas

Volte para os [Serviços inteligentes](./intelligent-services.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
