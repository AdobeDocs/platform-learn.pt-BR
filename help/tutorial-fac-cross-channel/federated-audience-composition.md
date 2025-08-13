---
title: Enriqueça os públicos-alvo da Experience Platform com dados federados
seo-title: Enrich Experience Platform audiences with federated data | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Enriqueça os públicos-alvo da Experience Platform com dados federados
description: Neste exercício visual, um público-alvo do Experience Platform é enriquecido com dados federados.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-enrich-audience-with-federated-data.jpg
hide: true
source-git-commit: 0bbdc93969b4716407ecf51499d572cb50f5a0d3
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 7%

---


# Enriqueça os públicos-alvo da Experience Platform com dados federados

A Composição de público-alvo federado permite enriquecer públicos-alvo existentes no Adobe Experience Platform (AEP) usando dados de público-alvo compostos que foram federados a partir do data warehouse corporativo. Esses dados não serão mantidos nos perfis de clientes da Adobe Experience Platform.

## Leitura de um público-alvo do AEP em uma composição federada

Neste exercício visual, usamos o público-alvo **Visitante da página de aplicativos de empréstimo do SecurFinancial** armazenado no Serviço de Perfil da AEP para iniciar nossa composição federada. Ele usa os dados federados no Snowflake para determinar a pré-aprovação com base na pontuação de crédito e na atividade de empréstimo.

![exemplo de composição federada](assets/snowflake-preapproval.png)

### Etapas

1. **Mapeie o público-alvo do AEP** para o destino da Composição do Público Federado.
2. **Crie sua composição** com o público mapeado como um público de leitura.
3. **Reconcilie as identidades** no seu público-alvo de leitura para ingressar com dados federados.

![método-federado-1-1](assets/federated-method-1-1.png)

![método-federado-1-2](assets/federated-method-1-2.png)

Vamos ver outro exemplo de uso de dados federados para [oferecer suporte à personalização &quot;no momento&quot;](drive-in-the-moment-personalization.md)!
