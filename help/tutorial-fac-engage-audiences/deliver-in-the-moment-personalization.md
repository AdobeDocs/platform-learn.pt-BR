---
title: Fornecer personalização "no momento" usando o Edge Network
seo-title: Deliver "in-the moment" personalization using Edge Network | Engage with Audiences from your Data Warehouse using Federated Audience Composition
breadcrumb-title: Fornecer personalização "no momento" usando o Edge Network
description: Neste exercício, o público-alvo federado é avaliado no Edge para redirecionamento instantâneo "no momento".
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-drive-in-the-moment-personalization.jpg
exl-id: 20bfafb1-1d1b-48d8-84eb-97d4c9e03b76
source-git-commit: dd5f594a54a9cab8ef78d36d2cf15a9b5f2b682a
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# Fornecer personalização &quot;no momento&quot; usando o Edge Network

A Composição de público-alvo federado permite enriquecer públicos-alvo existentes no Adobe Experience Platform (AEP) usando dados de público-alvo compostos que foram federados a partir do data warehouse corporativo. Esses dados não serão mantidos no Adobe Experience Platform.

Neste exercício visual, usamos um público-alvo federado consultado com pontuação de crédito e atividade de empréstimo para enriquecer o público-alvo comportamental dos visitantes da página da Web de aplicativos de empréstimo.

Ao avaliar esse público-alvo no Edge, redirecionamos instantaneamente os visitantes da página do aplicativo de empréstimo pré-aprovado com ofertas personalizadas no site.

![edge-audience-enrich](assets/edge-audience-enrich.png)

## Etapas

1. **Salve e inicie** sua composição de público-alvo federado. Depois que a composição for executada, o público-alvo federado aparecerá no portal de público-alvo.
2. **Crie uma regra de público-alvo** usando atributos de perfil e eventos de experiência do Serviço de Perfil, incorporando seu público federado.

Vamos concluir com um [resumo dos aprendizados e das lições finais](conclusion.md)!
