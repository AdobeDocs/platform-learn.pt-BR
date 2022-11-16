---
title: Assimilar e analisar dados do Google Analytics no Adobe Experience Platform com o BigQuery Source Connector - Crie sua primeira query no BigQuery
description: Assimilar e analisar dados do Google Analytics no Adobe Experience Platform com o BigQuery Source Connector - Crie sua primeira query no BigQuery
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 73154afc-c3e3-420c-9471-5bb106dbfd02
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 1%

---

# 12.2 Criar sua primeira query no BigQuery

## Objetivos

- Explore a interface do usuário do BigQuery
- Criar uma consulta SQL no BigQuery
- Salve os resultados da consulta SQL em um conjunto de dados no BigQuery

## Contexto

Quando os dados do Google Analytics estão no BigQuery, dimensões, métricas e outras variáveis são aninhadas. Além disso, os dados do Google Analytics são carregados diariamente em diferentes tabelas. Isso significa que tentar conectar tabelas Google Analytics no BigQuery ao Adobe Experience Platform diretamente é muito difícil e não é uma boa ideia.

A solução para esse problema é transformar os dados do Google Analytics em um formato legível para facilitar a assimilação no Adobe Experience Platform.

## 12.2.1 Crie um conjunto de dados para salvar novas Tabelas BigQuery

Vá para o [Console BigQuery](https://console.cloud.google.com/bigquery).

![demonstração](./images/ex3/1.png)

Em **Explorer**, você verá a ID do projeto. Clique na ID do projeto (não clique no link **bigquery-public-data** conjunto de dados).

![demonstração](./images/ex3/2.png)

Você pode ver que ainda não há um conjunto de dados, por isso vamos criar um agora.
Clique em **CRIAR CONJUNTO DE DADOS**.

![demonstração](./images/ex3/4.png)

No lado direito da tela, você verá o **Criar conjunto de dados** menu.

![demonstração](./images/ex3/5.png)

Para o **ID do conjunto de dados**, use a convenção de nomenclatura abaixo. Para os outros campos, mantenha as configurações padrão.

| Nomenclatura | Exemplo |
| ----------------- | ------------- | 
| `--demoProfileLdap--_BigQueryDataSets` | vangeluw_BigQueryDataSets |

![demonstração](./images/ex3/6.png)

Em seguida, clique em **Criar conjunto de dados**.

![demonstração](./images/ex3/7.png)

Em seguida, você estará de volta ao BigQuery Console com seu conjunto de dados criado.

![demonstração](./images/ex3/8.png)

## 12.2.2 Criar seu primeiro SQL BigQuery

Em seguida, você criará seu primeiro query no BigQuery. O objetivo desse query é pegar os dados de amostra do Google Analytics e transformá-los para que possam ser assimilados no Adobe Experience Platform. Vá para o **EDITOR** guia .

![demonstração](./images/ex3/9.png)

Copie a consulta SQL a seguir e cole-a nesse Editor de consultas. Leia o query e entenda a sintaxe Google Analytics BigQuery.


```sql
SELECT
  CONCAT(fullVisitorId, CAST(hitTime AS String), '-', hitNumber) AS _id,
  TIMESTAMP(DATETIME(Year_Current, Month_Current, Day_Current, Hour, Minutes, Seconds)) AS timeStamp,
  fullVisitorId as GA_ID,
  -- Fake CUSTOMER ID
  CONCAT('3E-D4-',fullVisitorId, '-1W-93F' ) as customerID,
  Page,
  Landing_Page,
  Exit_Page,
  Device,
  Browser,
  MarketingChannel,
  TrafficSource,
  TrafficMedium,
  -- Enhanced Ecommerce
  TransactionID,
  CASE
      WHEN EcommerceActionType = '2' THEN 'Product_Detail_Views'
      WHEN EcommerceActionType = '3' THEN 'Adds_To_Cart'
      WHEN EcommerceActionType = '4' THEN 'Product_Removes_From_Cart'
      WHEN EcommerceActionType = '5' THEN 'Product_Checkouts'
      WHEN EcommerceActionType = '6' THEN 'Product_Refunds'
    ELSE
    NULL
  END
     AS Ecommerce_Action_Type,
  -- Entrances (metric)
  SUM(CASE
      WHEN isEntrance = TRUE THEN 1
    ELSE
    0
  END
    ) AS Entries,
    
--Pageviews (metric)
    COUNT(*) AS Pageviews,
    
 -- Exits 
    SUM(
    IF
      (isExit IS NOT NULL,
        1,
        0)) AS Exits,
        
 --Bounces
   SUM(CASE
      WHEN isExit = TRUE AND isEntrance = TRUE THEN 1
    ELSE
    0
  END
    ) AS Bounces,
        
  -- Unique Purchases (metric)
  COUNT(DISTINCT TransactionID) AS Unique_Purchases,
  -- Product Detail Views (metric)
  COUNT(CASE
      WHEN EcommerceActionType = '2' THEN fullVisitorId
    ELSE
    NULL
  END
    ) AS Product_Detail_Views,
  -- Product Adds To Cart (metric)
  COUNT(CASE
      WHEN EcommerceActionType = '3' THEN fullVisitorId
    ELSE
    NULL
  END
    ) AS Adds_To_Cart,
  -- Product Removes From Cart (metric)
  COUNT(CASE
      WHEN EcommerceActionType = '4' THEN fullVisitorId
    ELSE
    NULL
  END
    ) AS Product_Removes_From_Cart,
  -- Product Checkouts (metric)
  COUNT(CASE
      WHEN EcommerceActionType = '5' THEN fullVisitorId
    ELSE
    NULL
  END
    ) AS Product_Checkouts,
  -- Product Refunds (metric)
  COUNT(CASE
      WHEN EcommerceActionType = '7' THEN fullVisitorId
    ELSE
    NULL
  END
    ) AS Product_Refunds
  FROM (
  SELECT
    -- Landing Page (dimension)
    CASE
      WHEN hits.isEntrance = TRUE THEN hits.page.pageTitle
    ELSE NULL
  END
    AS Landing_page,
    
        -- Exit Page (dimension)
    CASE
      WHEN hits.isExit = TRUE THEN hits.page.pageTitle
    ELSE
    NULL
  END
    AS Exit_page,
    
    hits.page.pageTitle AS Page,
    hits.isEntrance,
    hits.isExit,
    hits.hitNumber as hitNumber,
    hits.time as hitTime,
    date as Fecha,
    fullVisitorId,
    visitStartTime,
    device.deviceCategory AS Device,
    device.browser AS Browser,
    channelGrouping AS MarketingChannel,
    trafficSource.source AS TrafficSource,
    trafficSource.medium AS TrafficMedium,
    hits.transaction.transactionId AS TransactionID,
    CAST(EXTRACT(YEAR FROM CURRENT_DATE()) AS INT64) AS Year_Current,
    CAST(EXTRACT(MONTH FROM CURRENT_DATE()) AS INT64) AS Month_Current,
     CAST(EXTRACT(DAY FROM CURRENT_DATE()) AS INT64) AS Day_Current,
    CAST(EXTRACT(DAY FROM DATE_SUB(CURRENT_DATE(),INTERVAL 1 DAY)) AS INT64) AS Day_Current_Before,
    CAST(FORMAT_DATE('%Y', PARSE_DATE("%Y%m%d", date)) AS INT64) AS Year,
  CAST(FORMAT_DATE('%m', PARSE_DATE("%Y%m%d",date)) AS INT64) AS Month,
  CAST(FORMAT_DATE('%d', PARSE_DATE("%Y%m%d",date)) AS INT64) AS Day,
    CAST(EXTRACT (hour FROM TIMESTAMP_SECONDS(hits.time)) AS INT64) AS Hour,
  CAST(EXTRACT (minute FROM TIMESTAMP_SECONDS(hits.time)) AS INT64) AS Minutes,
  CAST(EXTRACT (second FROM TIMESTAMP_SECONDS(hits.time)) AS INT64) AS SecondS,
    hits.eCommerceAction.action_type AS EcommerceActionType
  
  FROM
    `bigquery-public-data.google_analytics_sample.ga_sessions_*`,
     UNNEST(hits) AS hits
  WHERE
    _table_suffix BETWEEN '20170101'
    AND '20170331'
    AND totals.visits = 1
    AND hits.type = 'PAGE'
    )
    
GROUP BY
  1,
  2,
  3,
  4,
  5,
  6,
  7,
  8,
  9,
  10,
  11,
  12,
  13,
  14
    
  ORDER BY 2 DESC
```

Quando estiver pronto, clique em **Executar** para executar o query:

![demonstração](./images/ex3/10.png)

A execução do query pode levar alguns minutos.

Quando o query terminar de ser executado, você verá a saída abaixo no **Resultados da consulta**.

![demonstração](./images/ex3/12.png)

## 12.2.3 Salve os resultados da consulta BigQuery SQL

A próxima etapa é salvar a saída do seu query clicando no botão **SALVAR RESULTADOS** botão.

![demonstração](./images/ex3/13.png)

Como o local da saída, selecione **Tabela BigQuery**.

![demonstração](./images/ex3/14.png)

Você verá um novo pop-up, onde **Nome do projeto** e **Nome do conjunto de dados** são preenchidas previamente. O nome do conjunto de dados deve ser o conjunto de dados criado no início deste exercício, com esta convenção de nomenclatura:

| Nomenclatura | Exemplo |
| ----------------- | ------------- | 
| `--demoProfileLdap--_BigQueryDataSets` | `vangeluw_BigQueryDataSets` |

Agora é necessário inserir um nome de Tabela. Use esta convenção de nomenclatura:

| Nomenclatura | Exemplo |
| ----------------- |------------- | 
| `--demoProfileLdap--_GAdataTableBigQuery` | `vangeluw_GAdataTableBigQuery` |

![demonstração](./images/ex3/16.png)

Clique em **SALVAR**.

Pode levar algum tempo até que os dados estejam prontos na tabela criada. Após alguns minutos, atualize o navegador. Em seguida, você deve ver em seu conjunto de dados a variável `--demoProfileLdap--_GAdataTableBigquery` tabela abaixo **Explorer** dentro do seu projeto BigQuery.

![demonstração](./images/ex3/19.png)

Agora, você pode continuar com o próximo exercício, onde você conectará esta tabela ao Adobe Experience Platform.

Próxima etapa: [12.3 Conectar GCP e BigQuery ao Adobe Experience Platform](./ex3.md)

[Voltar ao Módulo 12](./customer-journey-analytics-bigquery-gcp.md)

[Voltar para todos os módulos](./../../overview.md)
