---
title: Serviço de query - Power BI/Tableau
description: Serviço de query - Power BI/Tableau
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 11525d05-1c19-4d41-8f47-4feb3e8aed66
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# 4.4 Gerar um conjunto de dados a partir de um query

## Objetivo

Saiba como gerar conjuntos de dados a partir dos resultados do query Conecte o Microsoft Power BI Desktop/Tableau diretamente ao Serviço de query Criando um relatório no Microsoft Power BI Desktop/Tableau Desktop

## Contexto da lição

Uma interface de linha de comando para consultar dados é excitante, mas não apresenta bem. Nesta lição, nós o guiaremos por meio de um fluxo de trabalho recomendado para saber como você pode usar o Microsoft Power BI Desktop/Tableau diretamente no Serviço de query para criar relatórios visuais para seus participantes.

## 4.4.1 Criar um conjunto de dados a partir de uma consulta SQL

A complexidade da consulta afetará o tempo que o Serviço de query leva para retornar resultados. E ao consultar diretamente a partir da linha de comando ou de outras soluções como o Microsoft Power BI/Tableau, o Serviço de Consulta é configurado com um tempo limite de 5 minutos (600 segundos). Em alguns casos, essas soluções serão configuradas com tempos limite mais curtos. Para executar consultas maiores e carregar frontalmente o tempo necessário para retornar resultados, oferecemos um recurso para gerar um conjunto de dados a partir dos resultados da consulta. Esse recurso utiliza o recurso SQL padrão conhecido como Criar tabela como seleção (CTAS). Ela está disponível na interface do usuário da plataforma na Lista de query e também está disponível para ser executada diretamente a partir da linha de comando com PSQL.

No anterior, você substituiu **digite seu nome** com seu próprio ldap antes de executá-lo no PSQL.

```sql
select /* enter your name */
       e.--aepTenantId--.identification.core.ecid as ecid,
       e.placeContext.geo.city as city,
       e.placeContext.geo._schema.latitude latitude,
       e.placeContext.geo._schema.longitude longitude,
       e.placeContext.geo.countryCode as countrycode,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callFeeling as callFeeling,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callTopic as callTopic,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callContractCancelled as contractCancelled,
       l.--aepTenantId--.loyaltyDetails.level as loyaltystatus,
       l.--aepTenantId--.loyaltyDetails.points as loyaltypoints,
       l.--aepTenantId--.identification.core.loyaltyId as crmid
from   demo_system_event_dataset_for_website_global_v1_1 e
      ,demo_system_event_dataset_for_call_center_global_v1_1 c
      ,demo_system_profile_dataset_for_loyalty_global_v1_1 l
where  e.--aepTenantId--.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal')
and    e.web.webPageDetails.name in ('Cancel Service', 'Call Start')
and    e.--aepTenantId--.identification.core.ecid = c.--aepTenantId--.identification.core.ecid
and    l.--aepTenantId--.identification.core.ecid = e.--aepTenantId--.identification.core.ecid;
```

Navegue até a interface do usuário do Adobe Experience Platform - [https://experience.adobe.com/platform](https://experience.adobe.com/platform)

Você pesquisará sua instrução executada na interface do usuário do Adobe Experience Platform Query inserindo seu ldap no campo de pesquisa:

Selecionar **Queries**, vá para **Log** e insira o ldap no campo de pesquisa.

![search-query-for-ctas.png](./images/search-query-for-ctas.png)

Selecione seu query e clique em **Conjunto de dados de saída**.

![search-query-for-ctas.png](./images/search-query-for-ctasa.png)

Enter `--demoProfileLdap-- Callcenter Interaction Analysis` como nome e descrição para o conjunto de dados e pressione a tecla **Executar Consulta** botão

![create-ctas-dataset.png](./images/create-ctas-dataset.png)

Como resultado, você verá uma nova consulta com um status **Enviado**.

![ctas-query-submit.png](./images/ctas-query-submitted.png)

Após a conclusão, você verá uma nova entrada para **Conjunto de dados criado** (talvez seja necessário atualizar a página).

![ctas-dataset-created.png](./images/ctas-dataset-created.png)

Assim que seu conjunto de dados for criado (o que pode levar de 5 a 10 minutos), você poderá continuar o exercício.

Próxima etapa - Opção A: [4.5 Serviço e Power BI de query](./ex5.md)

Próxima etapa - Opção B: [4.6 Serviço de consulta e Tableau](./ex6.md)

[Voltar ao Módulo 4](./query-service.md)

[Voltar para todos os módulos](../../overview.md)
