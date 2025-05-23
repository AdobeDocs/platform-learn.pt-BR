---
title: Migrar seu aplicativo móvel do Adobe Target para o Adobe Journey Optimizer - Extensão de decisão
description: Saiba como migrar sua implementação de aplicativo móvel do Adobe Target para o Adobe Journey Optimizer - Extensão de decisão
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: 32363b95-b6ad-44af-a3b0-e1fbbbf5a8f1
source-git-commit: e0359d1bade01f79d0f7aff6a6e69f3e4d0c3b62
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 1%

---

# Migrar seu aplicativo móvel do Adobe Target para o Adobe Journey Optimizer - Extensão de decisão

Este guia é para implementadores experientes do Adobe Target que aprendem a migrar implementações existentes do Adobe Experience Platform Mobile SDK da extensão do Adobe Target para a extensão do Adobe Journey Optimizer - Decisioning.

O Adobe Experience Platform Mobile SDK capacita o engajamento completo em seus aplicativos móveis. A extensão do Target se baseia no Mobile SDK para ajudar você a personalizar as experiências do aplicativo com o Adobe Target. A extensão Decisioning é uma abordagem mais recente para implementar o Adobe Target em aplicativos móveis que usa os recursos do Adobe Experience Platform Edge Network que ajudam a integrar o Target a aplicativos baseados em plataforma, como Real-Time CDP e Journey Optimizer.

![Diagrama mostrando o SDK móvel se conectando ao Target por meio da Edge Network com a extensão de Decisão](assets/datacollection.png)

## Principais benefícios

Alguns dos benefícios da extensão do Adobe Journey Optimizer Decisioning em comparação à extensão do Target incluem:

* Compartilhamento mais rápido de públicos do [Real-Time Customer Data Platform](https://experienceleague.adobe.com/pt-br/docs/platform-learn/tutorials/destinations/target/next-hit-personalization)
* Integração do Target ao Journey Optimizer para oferecer suporte à [entrega de Offer Decisioning](https://experienceleague.adobe.com/pt-br/docs/target/using/integrate/ajo/offer-decision)
* Uma integração mais estreita com o Adobe Analytics, que não depende da compilação de informações de chamadas de rede separadas
* Flexibilidade adicional na implementação para desenvolvedores

Indiscutivelmente, o maior benefício para os clientes do Target da migração é a integração com o Real-Time Customer Data Platform. A Real-Time CDP oferece excelentes recursos de criação de público com base na ampla variedade de dados assimilados na Experience Platform e em seu recurso de Perfil do cliente em tempo real. Uma estrutura integrada de governança de dados automatiza o uso responsável desses dados. A IA do cliente permite usar facilmente modelos de aprendizado de máquina para criar modelos de propensão e churn cuja saída pode ser compartilhada de volta com a Adobe Target. E, por fim, os clientes dos complementos opcionais de Assistência médica, Privacidade e segurança podem usar o recurso de aplicação de consentimento para aplicar as preferências de consentimento de clientes individuais. O Platform Mobile SDK e a extensão Decisioning são um requisito para usar esses recursos do Real-Time CDP no canal móvel.

## Etapas de migração

O nível de esforço para migrar da extensão do Target para a extensão do Decisioning depende da complexidade da implementação atual e dos recursos do Target usados.

Independentemente da simplicidade ou complexidade de sua implementação, é importante entender totalmente seu estado atual antes de migrar. Este guia ajuda a detalhar os componentes da implementação atual e desenvolver um plano gerenciável para migrar cada parte.

O processo de migração envolve as seguintes etapas principais:

1. Avalie sua implementação atual, incluindo:
   1. Todas as APIs do Target SDK usadas
   1. Modificações nas configurações globais do Target
   1. Integração com o Adobe Analytics
   1. Uso de parâmetros de mbox, perfil e entidade
   1. Uso de scripts de perfil e públicos-alvo
   1. Código personalizado exclusivo para sua implementação
1. Configurar os componentes iniciais para se conectar ao Adobe Experience Platform Edge Network
1. Atualizar a implementação básica para substituir a extensão do Target pela extensão do Decisioning
1. Melhore a implementação Otimizar o SDK para seus casos de uso específicos. Isso pode envolver a transmissão de parâmetros adicionais, o uso de tokens de resposta e muito mais.
1. Atualizar objetos na interface do Target, como scripts de perfil, atividades e definições de público-alvo
1. Valide a implementação final antes de fazer a mudança no aplicativo de produção


>[!INFO]
>
>No ecossistema do Adobe Experience Platform Mobile SDK, as extensões são implementadas pelos SDKs importados para seus aplicativos que podem ter nomes diferentes:
>
> * **Target SDK** implementa a **extensão do Adobe Target**
> * **Otimizar o SDK** implementa a **Adobe Journey Optimizer - Extensão de decisão**

Em seguida, analise a [comparação detalhada entre a extensão do Target e a extensão do Decisioning](comparison.md) para obter uma melhor compreensão das diferenças técnicas e identificar áreas que exigem foco adicional.

>[!NOTE]
>
>Estamos empenhados em ajudá-lo a ser bem-sucedido na migração para dispositivos móveis do Target da extensão do Target para a extensão do Decisioning. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484?profile.language=pt#M625).
