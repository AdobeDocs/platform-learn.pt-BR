---
title: Recarregue os dados do cliente para fornecer experiências eletrizantes
description: Saiba como reduzir o impacto de dados de baixa qualidade, reduzir o tempo de implantação e multiplicar o ROI usando os mesmos dados para uma variedade de casos de uso.
feature: Queries
role: Data Engineer, Data Architect, Developer
jira: KT-10323
thumbnail: 342533.jpeg
exl-id: 30574cc5-66fa-4ab8-83ed-7af710294dbf
source-git-commit: adbe8f4476340abddebbf9231e3dde44ba328063
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 3%

---

# Recarregue os dados do cliente para fornecer experiências eletrizantes

Os dados omnichannel são um ingrediente essencial para potencializar perfis acionáveis do cliente usados por profissionais de marketing para orquestrar a ativação e medir as jornadas resultantes do cliente. No entanto, as organizações enfrentam desafios para gerenciar a qualidade, a escala e a variedade desses dados. Elas exigem soluções simplificadas para reduzir o impacto de dados de baixa qualidade, o tempo de implantação e o ROI, usando os mesmos dados para uma grande variedade de casos de uso.

Este vídeo aborda:

* Recursos de preparação de dados do Adobe Experience Platform que você pode aproveitar
* Aumento do ROI da Adobe Real-Time CDP, Adobe Journey Optimizer e Customer Journey Analytics

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

Para obter mais informações, visite o [Documentação do Serviço de consulta](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=pt-BR).

>[!NOTE]
>
>Este vídeo é um trecho da sessão do Adobe Summit 2020 *[Recarregando dados omnicanal para experiências de eletrificação](https://business.adobe.com/summit/2022/sessions/recharging-omnichannel-data-for-electrifying-exper-s409.html)*.
