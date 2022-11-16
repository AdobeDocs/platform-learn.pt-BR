---
title: Recarregue os dados do cliente para fornecer experiências de eletrificação
description: Saiba como reduzir o impacto de dados de baixa qualidade, reduzir o tempo de implantação e multiplicar o ROI usando os mesmos dados para vários casos de uso.
role: Data Engineer, Data Architect, Developer
feature: Queries
kt: 10323
thumbnail: 342533.jpeg
exl-id: 30574cc5-66fa-4ab8-83ed-7af710294dbf
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 3%

---

# Recarregue os dados do cliente para fornecer experiências de eletrificação

Os dados omnicanais são um ingrediente essencial para potencializar perfis de clientes acionáveis usados por profissionais de marketing para orquestrar a ativação e medir as jornadas de clientes resultantes. No entanto, as organizações enfrentam desafios no gerenciamento da qualidade, escala e variedade desses dados. Eles exigem soluções simplificadas para reduzir o impacto de dados de baixa qualidade, reduzir o tempo de implantação e multiplicar o ROI usando os mesmos dados para vários casos de uso.

Este vídeo explora:

* Recursos de preparação de dados do Adobe Experience Platform que você pode aproveitar
* Aumento do ROI do Adobe Real-Time CDP, Adobe Journey Optimizer e Customer Journey Analytics

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## Exemplo de SQL

```sql
INSERT INTO summit_adv_data_prep_dataset
SELECT STRUCT(
customerId AS crmCustomerId, struct(sku AS sku, price AS sku_price, abandonTS AS abandonTS) AS abandonBrowse) AS _pfreportingonprod
FROM
(SELECT
B.personKey.sourceID AS customerId,
A.productListItems[0].SKU AS sku,
max(A.timestamp) AS abandonTS,
max(C._pfreportingonprod.price) AS price
FROM summit_adobe_analytics_dataset A,profile_attribute_14adf268_2a20_4dee_bee6_a6b0e34616a9 B,summit_product_dataset C
WHERE A._experience.analytics.customDimensions.eVars.eVar1 = B.personKey.sourceID
AND A.productListItems[0].sku = C._pfreportingonprod.sku
AND A.web.webpagedetails.URL NOT LIKE '%orderconfirmation%'
AND timestamp > current_date - interval '4 day'
GROUP BY customerId,sku
order by price desc)D;
```

Para obter mais informações, visite o [Documentação do Serviço de query](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=pt-BR).

>[!NOTE]
>
>Este vídeo é um trecho da sessão de Adobe Summit 2020 *[Recarregamento de dados omnichannel para experiências de eletrificação](https://business.adobe.com/summit/2022/sessions/recharging-omnichannel-data-for-electrifying-exper-s409.html)*.
