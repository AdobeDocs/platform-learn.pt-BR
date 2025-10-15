---
title: Recarregue os dados do cliente para fornecer experiências eletrizantes
description: Saiba como reduzir o impacto de dados de baixa qualidade, reduzir o tempo de implantação e multiplicar o ROI usando os mesmos dados para uma variedade de casos de uso.
feature: Queries
role: Data Engineer, Data Architect, Developer
level: Beginner
jira: KT-10323
thumbnail: 342533.jpeg
exl-id: 30574cc5-66fa-4ab8-83ed-7af710294dbf
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Recarregue os dados do cliente para fornecer experiências eletrizantes

Os dados omnichannel são um ingrediente essencial para potencializar perfis acionáveis do cliente usados por profissionais de marketing para orquestrar a ativação e medir as jornadas resultantes do cliente. No entanto, as organizações enfrentam desafios para gerenciar a qualidade, a escala e a variedade desses dados. Elas exigem soluções simplificadas para reduzir o impacto de dados de baixa qualidade, o tempo de implantação e o ROI, usando os mesmos dados para uma grande variedade de casos de uso.
Para obter mais informações, visite a [documentação do Serviço de consulta](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=pt-BR).

Este vídeo aborda:

* Recursos de preparação de dados do Adobe Experience Platform que você pode aproveitar
* Aumento do ROI da Adobe Real-Time CDP, Adobe Journey Optimizer e Customer Journey Analytics

>[!VIDEO](https://video.tv.adobe.com/v/3454945?learn=on&enablevpops&captions=por_br)

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

>[!NOTE]
>
>Este vídeo é um trecho da sessão *[Recarregando Dados Omnichannel para Experiências de Eletrificação](https://business.adobe.com/br/summit/2022/sessions/recharging-omnichannel-data-for-electrifying-exper-s409.html)* do Adobe Summit 2020.
