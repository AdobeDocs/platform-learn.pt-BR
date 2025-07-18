---
title: Planejar a migração - Migre a implementação do Adobe Target no aplicativo móvel para a extensão do Offer Decisioning e do Target
description: Saiba mais sobre as principais diferenças entre a at.js e o Platform Web SDK e como planejar seu esforço de migração.
exl-id: 86849319-d2ad-4338-aa1a-d307d8807d4a
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# Planejar a migração

O nível de esforço para migrar da extensão do Target para a extensão do Offer Decisioning e do Target depende da complexidade da implementação atual e dos recursos do Target usados.

Independentemente da simplicidade ou complexidade de sua implementação, é importante entender totalmente seu estado atual antes de migrar. Este guia ajuda a detalhar os componentes da implementação atual e desenvolver um plano gerenciável para migrar cada parte.

O processo de migração envolve as seguintes etapas principais:

1. Avalie sua implementação atual e determine uma abordagem de migração
1. Configurar os componentes iniciais para se conectar ao Adobe Experience Platform Edge Network
1. Atualize a implementação básica para substituir a extensão do Target pela extensão do Offer Decisioning e do Target
1. Melhore a implementação Otimizar o SDK para seus casos de uso específicos. Isso pode envolver a transmissão de parâmetros adicionais, o uso de tokens de resposta e muito mais.
1. Atualizar objetos na interface do Target, como scripts de perfil, atividades e definições de público-alvo
1. Valide a implementação final antes de fazer a mudança no aplicativo de produção

>[!INFO]
>
>No ecossistema do Adobe Experience Platform Mobile SDK, as extensões são implementadas pelos SDKs importados para seus aplicativos que podem ter nomes diferentes:
>
> * **Target SDK** implementa a **extensão do Adobe Target**
> * **Otimizar SDK** implementa a **extensão do Offer Decisioning e do Target**


Em seguida, analise a [comparação detalhada da extensão do Target e da extensão do Offer Decisioning e do Target](detailed-comparison.md) para obter uma melhor compreensão das diferenças técnicas e identificar as áreas que exigem foco adicional.

>[!NOTE]
>
>Estamos empenhados em ajudá-lo a ser bem-sucedido na migração para dispositivos móveis do Target da extensão do Target para a extensão do Offer Decisioning e do Target. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484?profile.language=pt#M625).
