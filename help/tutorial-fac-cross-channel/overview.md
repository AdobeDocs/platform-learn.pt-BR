---
title: Desbloqueie insights entre canais com a Composição de público federado
description: A Federated Audience Composition é um recurso poderoso que permite que arquitetos e engenheiros de dados criem e enriqueçam públicos diretamente de data warehouses de terceiros.
breadcrumb-title: Visão geral
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2025-08-11T00:00:00Z
exl-id: 9d5a2e40-6cda-4164-87db-1bfffe3438e3
source-git-commit: a3c8d8b03472d01f491bf787ed647a696d3a5524
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Visão geral

A Federated Audience Composition é um recurso avançado disponível para ambientes do Adobe Real-Time Customer Data Platform (Real-Time CDP) e Adobe Journey Optimizer. Ele permite que arquitetos e engenheiros de dados criem e enriqueçam públicos diretamente de data warehouses de terceiros [compatíveis](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"} sem replicar dados para a Adobe Experience Platform. Este tutorial fornece orientação prática para usuários técnicos para conectar data warehouses empresariais, criar e enriquecer públicos-alvo e ativá-los para experiências de marketing personalizadas.

## Guia visual

Este guia visual mostra as etapas de cada uma das atividades realizadas para dar suporte a vários aspectos do cenário de negócios. O objetivo é fornecer atividades que você pode aproveitar em seu ambiente, incluindo:

- Conectar o Adobe Experience Platform a um data warehouse corporativo.
- Crie e gerencie públicos-alvo usando a Composição de público-alvo federado.
- Mapeie públicos federados para destinos externos, como o Amazon S3.
- Enriqueça os públicos existentes com dados federados.
- Crie públicos-alvo para impulsionar personalização &quot;no momento&quot;.
- Crie jornadas do cliente usando dados de público-alvo federado.

Este guia foi projetado para arquitetos de dados e engenheiros de dados que trabalham com Real-Time CDP ou Journey Optimizer. Ele presume estar familiarizado com o Adobe Experience Platform e os conceitos básicos do data warehouse.

## Contexto de negócios

A SecurFinancial é uma importante empresa de serviços financeiros. Ele aproveita sua grande variedade de dados de clientes em diferentes fontes para personalizar ofertas e campanhas para um grande número de segmentos. Eles planejam usar o recurso Real-Time CDP Federated Audience Composition da Adobe, que permite que as empresas usem seu data warehouse existente enquanto usam os aplicativos da Adobe Experience Platform para fornecer experiências personalizadas aos clientes. Os principais benefícios incluem:

- **Acesso aos dados do warehouse**: crie públicos-alvo de alto valor a partir de conjuntos de dados em data warehouses com suporte sem replicação de dados.
- **Movimentação de dados minimizada**: consulta dados diretamente no warehouse, reduzindo a duplicação e mantendo a governança de dados.
- **Fluxos de trabalho de experiência unificada**: prepare e ative públicos-alvo no Adobe Experience Platform para casos de uso entre canais.
- **Personalização aprimorada**: enriqueça perfis e públicos-alvo com atributos de warehouse para potencializar experiências acionadas em tempo real.

## Cenário de negócios

O SecurFinancial gostaria de lançar uma campanha por e-mail para redirecionar seus clientes pré-qualificados para um empréstimo com base em um bom crédito e que não têm um empréstimo ativo em seu portfólio do SecurFinancial. Embora estejam assimilando dados comportamentais online em tempo real, eles enfrentam desafios para identificar a pré-qualificação do cliente, pois estão impedidos de assimilar informações de crédito na AEP. Para qualificar clientes pré-qualificados sem mover dados restritos, eles usarão a Federated Audience Composition para enriquecer seu público comportamental do AEP.

## Pré-requisitos

Para executar atividades semelhantes em seu ambiente, verifique se você tem:

- Acesso a uma conta do Adobe Experience Platform provisionada com o Real-Time CDP ou o Journey Optimizer.
- Permissões de administrador do sistema ou a capacidade de ter permissões configuradas.
- Familiaridade com conceitos do Adobe Experience Platform, como esquemas, conjuntos de dados e públicos-alvo (recomendado: conclua a [Introdução à lista de reprodução do Adobe Experience Platform](https://experienceleague.adobe.com/en/playlists/experience-platform-introduction?lang=en){target="_blank"} no Experience League).
- Acesso a um data warehouse corporativo compatível (por exemplo, Amazon Redshift, Azure Synapse Analytics, Snowflake ou Google BigQuery).
- Conhecimento básico de SQL para consulta de data warehouses.
- **Ambientes de sandbox**: crie uma sandbox na instância do Real-Time CDP de sua organização para testar com segurança sem afetar os dados de produção.
- **Conexão do Data Warehouse**: este tutorial usa uma conexão do Snowflake, mas você pode usar qualquer [warehouse de nuvem com suporte](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites).

Vamos começar com a [Data Warehouse Connection](data-warehouse-connection.md).
