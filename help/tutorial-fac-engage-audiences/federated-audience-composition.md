---
title: Enriquecer públicos-alvo com dados de warehouse
seo-title: Enrich Audiences with Warehouse Data | Engage with Audiences from your Data Warehouse using Federated Audience Composition
breadcrumb-title: Enriquecer públicos-alvo com dados de warehouse
description: Neste exercício, um público-alvo da Experience Platform é enriquecido com dados de warehouse.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-enrich-audience-with-federated-data.jpg
exl-id: 3f6aa121-0dbd-4ad9-b136-d1455eed03ca
source-git-commit: dd5f594a54a9cab8ef78d36d2cf15a9b5f2b682a
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 7%

---

# Enriquecer públicos-alvo com dados de warehouse

A Composição de público-alvo federado permite enriquecer públicos-alvo existentes no Adobe Experience Platform (AEP) usando dados de público-alvo compostos que foram federados a partir do data warehouse corporativo. Esses dados não serão mantidos nos perfis de clientes da Adobe Experience Platform.

## Leitura de um público-alvo em uma composição federada

Neste exercício, usamos o público-alvo **Visitante da página de aplicativos de empréstimo do SecurFinancial** armazenado no Serviço de perfil da Experience Platform para iniciar nossa composição federada. Ele usa os dados federados no Snowflake para determinar a pré-aprovação com base na pontuação de crédito e na atividade de empréstimo.

![exemplo de composição federada](assets/snowflake-preapproval.png)

### Etapas

1. **Mapeie o público-alvo do AEP** para o destino da Composição do Público Federado.
2. **Crie sua composição** com o público mapeado como um público de leitura.
3. **Reconcilie as identidades** no seu público-alvo de leitura para ingressar com dados federados.

![método-federado-1-1](assets/federated-method-1-1.png)

![método-federado-1-2](assets/federated-method-1-2.png)

Vamos ver outro exemplo de uso de dados federados para [oferecer suporte à personalização &quot;no momento&quot;](deliver-in-the-moment-personalization.md)!
