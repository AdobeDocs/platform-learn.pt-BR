---
title: Interaja com públicos-alvo da sua Data Warehouse usando a Composição de público-alvo federado
description: A Federated Audience Composition é um recurso poderoso que permite que arquitetos e engenheiros de dados criem e enriqueçam públicos diretamente de data warehouses de terceiros.
breadcrumb-title: Visão geral
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2025-08-11T00:00:00Z
exl-id: 9d5a2e40-6cda-4164-87db-1bfffe3438e3
source-git-commit: dd5f594a54a9cab8ef78d36d2cf15a9b5f2b682a
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Interaja com públicos-alvo da sua Data Warehouse usando a Composição de público-alvo federado

A Federated Audience Composition (FAC) é um recurso avançado disponível para ambientes do Adobe Real-Time Customer Data Platform (Real-Time CDP) e do Adobe Journey Optimizer. Ele capacita arquitetos e engenheiros de dados a preparar e ativar públicos-alvo de alto valor diretamente de [data warehouses empresariais compatíveis](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"}, sem copiar ou mover dados do cliente para o Adobe Experience Platform (AEP). Essa abordagem de CDP combinável (uma solução personalizada para os clientes) está alinhada às tendências do setor, permitindo que as empresas aproveitem sua infraestrutura de dados para experiências digitais personalizadas, mantendo, ao mesmo tempo, a governança de dados.

## Contexto de negócios

A SecurFinancial é uma importante empresa de serviços financeiros. Ele aproveita sua grande variedade de dados de clientes em diferentes fontes para personalizar ofertas e campanhas para um grande número de segmentos. Eles planejam usar o recurso Composição de público federado do Adobe Real-Time CDP para preparar públicos-alvo de seu data warehouse e, ao mesmo tempo, ativá-los para destinos da Adobe Experience Platform, além do Adobe Journey Optimizer para fornecer uma solução personalizada para oferecer experiências ao cliente.

## Cenário de negócios

O SecurFinancial gostaria de lançar uma campanha por e-mail para redirecionar seus clientes pré-qualificados para um empréstimo com base em um bom crédito e que não têm um empréstimo ativo em seu portfólio do SecurFinancial. Embora estejam assimilando dados comportamentais online em tempo real, eles enfrentam desafios para identificar a pré-qualificação do cliente, pois estão impedidos de assimilar informações de crédito na AEP. Para qualificar clientes pré-qualificados sem mover dados restritos, eles usarão a Federated Audience Composition para enriquecer seu público comportamental do AEP.

## Guia

Este guia demonstra como oferecemos suporte ao cenário SecureFinancial Business. Especificamente, ele aborda como expomos públicos-alvo para sistemas que precisam desses públicos-alvo, incluindo uma conta de armazenamento S3, uma jornada no Journey Optimizer para direcionar uma campanha de email e redirecionamento no local para clientes que foram pré-aprovados para um empréstimo.

As etapas incluem:

1. Conectar o Adobe Experience Platform a um data warehouse corporativo.
2. Crie um público-alvo usando a Composição de público-alvo federado.
3. Mapeie um público federado para um destino externo do Amazon S3.
4. Crie uma jornada do cliente usando dados de público-alvo federado.
5. Enriqueça um público com dados federados.
6. Impulsione a personalização &quot;no momento&quot; no Edge.

## Pré-requisitos

Para executar atividades semelhantes em seu ambiente, verifique se você tem:

- Acesso a uma conta do Adobe Experience Platform provisionada com o Real-Time CDP ou o Journey Optimizer.
- Permissões de administrador do sistema ou a capacidade de ter permissões configuradas.
- Familiaridade com conceitos do Adobe Experience Platform, como esquemas, conjuntos de dados e públicos-alvo (recomendado: conclua a [Introdução à lista de reprodução do Adobe Experience Platform](https://experienceleague.adobe.com/en/playlists/experience-platform-introduction?lang=en){target="_blank"} no Experience League).
- Acesso a um [data warehouse de empresa](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"} com suporte.
- Conhecimento básico de SQL para consulta de data warehouses.
- **Ambientes de sandbox**: crie uma sandbox na instância de sua organização para testar com segurança sem afetar os dados de produção.
- **Conexão Data Warehouse**: este tutorial usa uma conexão Snowflake, mas você pode usar qualquer [data warehouse com suporte](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites).

Primeiro, vamos analisar a [Arquitetura e fluxo de alto nível para a composição de público-alvo federado](fac-architecture-and-flow.md).
