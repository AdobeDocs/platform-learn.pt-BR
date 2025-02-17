---
title: Assimilar e analisar dados do Google Analytics no Adobe Experience Platform com o Conector de Source do BigQuery - Carregue dados do BigQuery para o Adobe Experience Platform
description: Assimilar e analisar dados do Google Analytics no Adobe Experience Platform com o Conector de Source do BigQuery - Carregue dados do BigQuery para o Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: f58af1cf-6f2e-420c-9eed-29382806a9f4
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 2%

---

# 1.2.4 Carregar dados do BigQuery no Adobe Experience Platform

## Objetivos

- Mapear dados do BigQuery para um esquema XDM
- Carregar dados do BigQuery no Adobe Experience Platform
- Familiarize-se com a interface do usuário do BigQuery Source Connector

## Antes de começar

Após o exercício anterior, essa página deve ser aberta no Adobe Experience Platform:

![demonstração](./images/datasets.png)

**Se estiver aberto, continue com o próximo exercício.**

**Se não estiver aberto, vá para [Adobe Experience Platform](https://experience.adobe.com/platform/home).**

No menu esquerdo, vá para Origens. Você verá a página inicial de **Fontes**. No menu **Fontes**, vá para o conector de origem do **Google BigQuery** e clique em **Configurar**.

![demonstração](./images/sourceshome.png)

Em seguida, você verá a tela de seleção da conta do Google BigQuery. Selecione sua conta e clique em **Avançar**.

![demonstração](./images/0c.png)

Você verá a tela **Selecionar dados**.

![demonstração](./images/datasets.png)

## 1.2.4.1 Seleção de tabela do BigQuery

Na tela **Selecionar dados**, selecione seu conjunto de dados do BigQuery. Agora você pode ver uma pré-visualização de dados de amostra do Google Analytics no BigQuery.

Clique em **Next**.

![demonstração](./images/datasets1.png)

## 1.2.4.2 Mapeamento XDM

Agora você verá isto:

![demonstração](./images/xdm4a.png)

Agora é necessário criar um novo conjunto de dados ou selecionar um conjunto de dados existente para carregar os dados do Google Analytics. Para este exercício, um conjunto de dados e um esquema já foram criados. Não é necessário criar um novo esquema ou conjunto de dados.

Selecione **Conjunto de dados existente**. Abra o menu suspenso para selecionar um conjunto de dados. Procure o conjunto de dados chamado `Demo System - Event Dataset for BigQuery (Global v1.1)` e selecione-o. Clique em **Next**.

![demonstração](./images/xdm6.png)

Role para baixo. Agora é necessário mapear cada **Campo Source** do Google Analytics/BigQuery para um **Campo Target** XDM, campo por campo. Você poderá ver vários erros, que serão abordados pelo exercício de mapeamento abaixo.

![demonstração](./images/xdm8.png)

Use a tabela de mapeamento abaixo para este exercício.

| Campo de origem | Campo de público alvo |
| ----------------- |-------------| 
| `_id` | `_id` |
| `_id` | canal._id |
| `timeStamp` | carimbo de data e hora |
| `GA_ID` | ``--aepTenantId--``.identification.core.gaid |
| `customerID` | ``--aepTenantId--``. identification.core.crmId |
| `Page` | web.webPageDetails.name |
| `Device` | device.type |
| `Browser` | environment.browserDetails.vendor |
| `MarketingChannel` | marketing.trackingCode |
| `TrafficSource` | channel.typeAtSource |
| `TrafficMedium` | channel.mediaType |
| `TransactionID` | commerce.order.payments.transactionID |
| `Ecommerce_Action_Type` | eventType |
| `Pageviews` | web.webPageDetails.pageViews.value |


Para alguns campos, é necessário remover o mapeamento original e criar um novo, para um **Campo Calculado**.

| Campo calculado | Campo de público alvo |
| ----------------- |-------------| 
| `iif(Unique_Purchases == null, 0, Unique_Purchases)` | commerce.purchases.value |
| `iif(Product_Detail_Views == null, 0, Product_Detail_Views)` | commerce.productViews.value |
| `iif(Adds_To_Cart == null, 0, Adds_To_Cart)` | commerce.productListAdds.value |
| `iif(Product_Removes_From_Cart == null, 0, Product_Removes_From_Cart), 1, 0)` | commerce.productListRemovals.value |
| `iif(Product_Checkouts == null, 0, Product_Checkouts)` | commerce.checkouts.value |

Para criar um **Campo Calculado**, clique em **+ Novo tipo de campo** e em **Campo calculado**.

![demonstração](./images/xdm8a.png)

Cole a regra acima e clique em **Salvar** para cada um dos campos na tabela acima.

![demonstração](./images/xdm8b.png)

Agora você tem um **Mapeamento** como este.

Os campos de origem **GA_ID** e **customerID** estão mapeados para um Identificador neste Esquema XDM. Isso permitirá enriquecer os dados do Google Analytics (dados de comportamento da Web/aplicativo) com outros conjuntos de dados, como dados de fidelidade ou da central de atendimento.

Clique em **Next**.

![demonstração](./images/xdm34.png)

## 1.2.4.3 Conexão e agendamento da assimilação de dados

Você verá a guia **Agendamento**:

Na guia **Agendamento**, você pode definir uma frequência para o processo de assimilação de dados para este **Mapeamento** e dados.

Como você está usando dados de demonstração no Google BigQuery que não serão atualizados, não há necessidade real de definir um cronograma neste exercício. Você precisa selecionar algo e, para evitar muitos processos de assimilação de dados inúteis, é necessário definir a frequência da seguinte maneira:

- Frequência: **Semana**
- Intervalo: **200**
- Hora de início: **a qualquer momento na próxima hora**

**Importante**: certifique-se de ativar a opção **Preenchimento retroativo**.

Por último, mas não menos importante, você deve definir um campo **delta**.

O campo **delta** é usado para agendar a conexão e carregar somente novas linhas que chegam ao seu conjunto de dados do BigQuery. Um campo delta geralmente é sempre uma coluna de carimbo de data e hora. Portanto, para assimilações de dados agendadas futuras, somente as linhas com um novo carimbo de data e hora mais recente serão assimiladas.

Selecione **timeStamp** como o campo delta.
Clique em **Next**.

![demonstração](./images/ex437.png)

## 1.2.4.4 Analisar e iniciar conexão

Agora você verá uma visão geral detalhada da sua conexão. Verifique se tudo está correto antes de continuar, pois algumas configurações não podem mais ser alteradas posteriormente, como por exemplo, o mapeamento XDM.

Clique em **Concluir**.

![demonstração](./images/xdm46.png)

Depois que a conexão for criada, você verá o seguinte:

![demonstração](./images/xdm48.png)

Agora você está pronto para continuar com o próximo exercício, no qual usará o Customer Journey Analytics para criar visualizações avançadas com base nos dados do Google Analytics.

## Próximas etapas

Ir para [1.2.5 Analisar Dados do Google Analytics usando o Customer Journey Analytics](./ex5.md){target="_blank"}

Retorne para [Assimilar e analisar dados do Google Analytics no Adobe Experience Platform com o Conector de Source do BigQuery](./customer-journey-analytics-bigquery-gcp.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
