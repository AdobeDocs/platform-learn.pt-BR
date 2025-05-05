---
title: Executar consultas
seo-title: Run queries | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Executar consultas
description: Nesta lição, você aprenderá a configurar, gravar e executar consultas para validar os dados assimilados.
role: Data Architect, Data Engineer
feature: Queries
jira: KT-4348
thumbnail: 4348-run-queries.jpg
exl-id: a37531cb-96ad-4547-86af-84f7ed65f019
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Executar consultas

<!-- 15 min-->
Nesta lição, você aprenderá a configurar, gravar e executar consultas para validar os dados assimilados.

O Serviço de consulta da Adobe Experience Platform ajuda você a entender seus dados, permitindo que use o SQL padrão para consultar dados na Platform. Usando o Serviço de consulta, você pode ingressar em qualquer conjunto de dados no Data Lake e capturar os resultados da consulta como um novo conjunto de dados para usar em relatórios, aprendizado de máquina ou para assimilação no Perfil do cliente em tempo real.

Os **Arquitetos de Dados** e **Engenheiros de Dados** precisarão usar o serviço de consulta fora deste tutorial.

Antes de começar os exercícios, assista a este vídeo curto para saber mais sobre o Serviço de consulta:
>[!VIDEO](https://video.tv.adobe.com/v/33187?learn=on&enablevpops&captions=por_br)

## Permissões necessárias

Na lição [Configurar Permissões](configure-permissions.md), você configura todos os controles de acesso necessários para concluir esta lição.

<!-- Settings > **[!UICONTROL Services]** > **[!UICONTROL Query Service]**
* Permission items Data Management > **[!UICONTROL View Datasets]** and  **[!UICONTROL Manage Datasets]**
* Permission item Sandboxes > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## Consultas simples

Vamos começar com algumas consultas simples:

1. Na interface do usuário da Platform, acesse **Consultas** na navegação à esquerda
1. Selecione o botão **Criar Consulta** na parte superior direita para abrir uma caixa de texto para executar consultas
1. Insira a seguinte consulta no editor e pressione Shift+Enter ou Shift+Return para executar a consulta.

   ```
   SHOW TABLES
   ```

1. Isso mostra a lista de tabelas disponíveis

   ![Consulta SHOW TABLE](assets/queries-showTables.png)


1. Agora, tente esta consulta, substituindo `_techmarketingdemos` pelo seu próprio namespace de locatário, que, se você se lembrar, está visível em seus esquemas.

   ```
   SELECT person.name.lastName,loyalty.tier
   FROM luma_loyalty_dataset
   WHERE loyalty.tier ='gold'
   ```

   ![SELECIONAR dados do conjunto de dados de fidelidade](assets/queries-loyaltySelect.png)

1. Se houver algum erro, mensagens detalhadas serão exibidas na guia **[!UICONTROL Console]**, conforme mostrado abaixo
   ![Erro na consulta](assets/queries-error.png)

1. Com sua consulta bem-sucedida, **[!UICONTROL Nomeie]** ela `Luma Gold Level Customers`
1. Selecione o botão **[!UICONTROL Salvar]**
   ![Salvando a consulta](assets/queries-loyaltySelect-save.png)


<!--SELECT COUNT(DISTINCT (_techmarketingdemos.systemIdentifier.loyaltyId)) FROM luma_loyalty_dataset 


SELECT _techmarketingdemos.systemIdentifier.loyaltyId, COUNT(_techmarketingdemos.systemIdentifier.loyaltyId)
FROM luma_loyalty_dataset 
GROUP BY _techmarketingdemos.systemIdentifier.loyaltyId
HAVING COUNT(_techmarketingdemos.systemIdentifier.loyaltyId) > 1;-->

## Exercícios adicionais

Exercícios adicionais do Serviço de query serão adicionados ao tutorial em uma data posterior.
<!--
## Join Datasets

In this exercise, we will join two datasets `Luma Loyalty Dataset` and `Luma Offline Purchase` to get list of gold customers who have spend over $500 dollars in one purchase.

1. Create a new query
1. Copy and paste following query in query editor and execute, again replacing `_techmarketingdemos` with your own tenant namespace
    
    ```
    SELECT DISTINCT lopd.commerce.order.purchaseID as PurchaseId ,
        lld.person.name.firstName as LastName ,
        lld.person.name.lastName as LastName ,
        lopd.personalEmail.address as email,
        lopd.commerce.order.priceTotal as Total

    FROM luma_loyalty_dataset lld
    JOIN luma_offline_purchase_event_dataset lopd
    ON lopd._techmarketingdemos.systemIdentifier.loyaltyId = lld._techmarketingdemos.systemIdentifier.loyaltyId

    WHERE lld._techmarketingdemos.loyalty.level ='gold' AND lopd.commerce.order.priceTotal >500;
    ```

1. You should get list of Gold Customers who have spend over $500 in single purchase.

## Output datasets

1. Select on Output Dataset button
1. Provide name and description to the dataset
1. Save.
1. Go to **Datasets** under **Data Management** to find new dataset created.

-->
<!--Add content for Adobe Defined Functions-->

## Recursos adicionais

* [Documentação do Serviço de consulta](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=pt-BR)
* [Referência da API do Serviço de Consulta](https://www.adobe.io/experience-platform-apis/references/query-service/)

E agora, para a lição final prática, [criando segmentos](build-segments.md)!
