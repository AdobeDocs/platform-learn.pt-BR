---
title: Composição de público-alvo federado Arquitetura e fluxo de alto nível
seo-title: Federated Audience Composition High-level Architecture & Flow | Engage with Audiences from your Data Warehouse using Federated Audience Composition
breadcrumb-title: Composição de público-alvo federado Arquitetura e fluxo de alto nível
description: Visão geral da arquitetura de alto nível e do fluxo da Composição do Audience Federated.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-high-level-architecture.jpg
exl-id: 4cb0b730-4206-476b-93d9-776dfbd464ff
source-git-commit: ae3799bbc8ff34a47470ea3300e0a0eb9f158c82
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# Composição de público-alvo federado Arquitetura e fluxo de alto nível

Antes de analisarmos as etapas de suporte ao cenário de negócios do SecurFinancial, analisaremos a arquitetura de alto nível e o fluxo dessa abordagem de CDP combinável.

O módulo Federated Audience Composition no Adobe Experience Platform expande o acesso aos conjuntos de dados do data warehouse sem copiar os dados subjacentes, minimizando a movimentação e a duplicação de dados.

Isso também fornece às organizações a arquitetura combinável necessária, que já concluíram o trabalho de gerenciamento de dados necessário em seu warehouse e desejam usar um padrão de cópia zero, em que o Adobe Experience Platform se torna o mecanismo de envolvimento.

Ele permite que as empresas processem rapidamente as informações armazenadas em um ou mais data warehouses. Isso elimina a necessidade de assimilar dados na Adobe Experience. Além disso, fornece acesso a novos conjuntos de dados que residem em data warehouses corporativos, mas que até agora estavam inacessíveis para workflows de experiência do cliente. Os exemplos podem incluir transações históricas ou dados pessoais que serão úteis em um nível de público-alvo agregado para o engajamento do cliente.

![arquitetura de rosto](assets/fac-architecture.png)

Agora, vamos criar uma [Conexão com o Data Warehouse](data-warehouse-connection.md).
