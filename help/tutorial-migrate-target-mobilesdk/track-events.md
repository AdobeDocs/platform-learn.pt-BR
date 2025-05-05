---
title: Rastrear eventos de conversão - Migre a implementação do Adobe Target no aplicativo móvel para o Adobe Journey Optimizer - Extensão de decisão
description: Saiba como rastrear eventos de conversão do Adobe Target usando a extensão móvel do Adobe Journey Optimizer - Decisioning
exl-id: 7b53aab1-0922-4d9f-8bf0-f5cf98ac04c4
source-git-commit: d2da62ed2d36f73af1c8053be5af27feea32cb14
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# Rastrear eventos de conversão do Target usando a extensão móvel do Decisioning

O objetivo da maioria das atividades do Target é impulsionar ações valiosas do usuário em seu aplicativo, como compras, registro, cliques e muito mais. As implementações do Target geralmente usam eventos de conversão personalizados para rastrear essas ações, geralmente contendo detalhes adicionais sobre a conversão. Os eventos de conversão do Target podem ser rastreados com a opção Otimizar SDK, semelhante ao SDK do Target. APIs específicas precisam ser chamadas para rastrear eventos de conversão, conforme mostrado na tabela abaixo:

| Objetivo da atividade | Extensão do Target | Extensão do Decisioning |
|---|---|---|
| Rastrear um evento de conversão de exibição para um local da mbox (escopo) | Chamar a API [displayedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} quando o local da mbox for visualizado | Chame a API [exibido](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} quando a Oferta para o local da mbox for visualizada. Isso envia um evento com o tipo de evento decisioning.propositionDisplay para a rede da Experience Edge. **Isso é essencial para incrementar os visitantes em suas atividades do Target e deve ser feito ao entregar ofertas do Target regulares e padrão.** |
| Rastrear um evento de conversão de cliques para um local da mbox (escopo) | Chame a API [clickedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} em quando o local da mbox for clicado | Chame a API [tapped](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} quando a Oferta para o local da mbox for clicada. Isso envia um evento com tipo de evento decisioning.propositionInteract para a rede da Experience Edge. |
| Rastrear um evento de conversão personalizado que também pode incluir dados adicionais, como parâmetros do perfil do Target e detalhes do pedido | Transmita os dados adicionais no campo TargetParameters fornecidos pelas APIs [displayedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} e [clickedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} | Use as APIs dos métodos públicos [generateDisplayInteractionXdm](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-edge-extension-api){target=_blank} e [generateTapInteractionXdm](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-edge-extension-api){target=_blank} disponíveis na Oferta para o local da mbox a fim de gerar os dados formatados XDM para exibição e clique, respectivamente. Em seguida, chame a API [sendEvent](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#sendevent){target=_blank} do Edge SDK para enviar esses dados de rastreamento XDM juntamente com quaisquer dados adicionais XDM e de forma livre para a rede da Experience Edge. |


Em seguida, saiba como [atualizar públicos-alvo e scripts de perfil](update-audiences.md) para garantir a compatibilidade com a extensão do Decisioning.

>[!NOTE]
>
>Estamos empenhados em ajudá-lo a ser bem-sucedido na migração para dispositivos móveis do Target da extensão do Target para a extensão do Decisioning. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=pt#M463).
