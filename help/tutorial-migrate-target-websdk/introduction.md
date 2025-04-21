---
title: Migração do Target da at.js 2.x para o Web SDK
description: Saiba como migrar uma implementação do Adobe Target da at.js 2.x para o Adobe Experience Platform Web SDK. Os tópicos incluem o carregamento da biblioteca do JavaScript, o envio de parâmetros, atividades de renderização e outras chamadas importantes.
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: c8920fde-ad6b-4f2d-a35f-ce865b35bba0
source-git-commit: e0359d1bade01f79d0f7aff6a6e69f3e4d0c3b62
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 5%

---

# Migração do Target da at.js 2.x para a Platform Web SDK

Este guia é para implementadores experientes do Adobe Target que aprendem a migrar uma implementação do at.js para o Adobe Experience Platform Web SDK.

O Adobe Experience Platform Web SDK é uma biblioteca JavaScript do lado do cliente que permite aos clientes da Adobe Experience Cloud interagir com os serviços da Experience Cloud por meio do Adobe Experience Platform Edge Network. Esta nova biblioteca combina os recursos das bibliotecas de aplicativos Adobe separadas em um único pacote leve que pode aproveitar ao máximo os novos recursos do Adobe Experience Platform.


>[!NOTE]
>
>Tutoriais de migração semelhantes estão disponíveis para:
>
> * [Adobe Analytics](../tutorial-migrate-analytics-websdk/migration-to-websdk-overview.md)
> * [Adobe Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk)

>[!CAUTION]
>
> Como o Platform Web SDK é compatível com várias aplicações Adobe, todas as bibliotecas Adobe em uma determinada página devem ser migradas ao mesmo tempo. Por exemplo, uma implementação mista do Web SDK para Target e AppMeasurement para Analytics em uma única página _não é suportada_. No entanto, há suporte para uma implementação mista em páginas diferentes, por exemplo, Web SDK na página A e at.js com AppMeasurement na página B.



## Principais benefícios

Alguns dos benefícios do Platform Web SDK em comparação à biblioteca at.js independente incluem:

* Compartilhamento mais rápido de públicos do [Real-Time Customer Data Platform](https://experienceleague.adobe.com/en/docs/platform-learn/tutorials/destinations/target/next-hit-personalization)
* Integração do Target ao Journey Optimizer para oferecer suporte à [entrega de Offer Decisioning](https://experienceleague.adobe.com/en/docs/target/using/integrate/ajo/offer-decision)
* Capacidade de usar [ids primárias](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/edge-network/generate-first-party-device-ids) para gerar a ECID para identificação de visitantes de maior duração
* Uma área menor para melhorar as métricas de velocidade da página
* Flexibilidade adicional na implementação para desenvolvedores

Indiscutivelmente, o maior benefício para os clientes do Target da migração é a integração com o Real-Time Customer Data Platform. A Real-Time CDP oferece excelentes recursos de criação de público com base na ampla variedade de dados assimilados na Experience Platform e em seu recurso de Perfil do cliente em tempo real. Uma estrutura de governança de dados integrada automatiza o uso responsável desses dados. A IA do cliente permite usar facilmente modelos de aprendizado de máquina para criar modelos de propensão e churn cuja saída pode ser compartilhada de volta com a Adobe Target. E, por fim, os clientes dos complementos opcionais de Assistência médica, Privacidade e segurança podem usar o recurso de aplicação de consentimento para aplicar facilmente as preferências de consentimento de clientes individuais. O Platform Web SDK é um requisito para usar esses recursos do Real-Time CDP no canal da Web.

## Objetivos de aprendizagem

Ao final deste tutorial, você poderá:

* Entender as diferenças de implementação do Target entre a at.js e o Platform Web SDK
* Definir a configuração inicial da funcionalidade do Target
* Atualizar a biblioteca at.js para o Platform Web SDK
* Renderizar atividades baseadas em formulário e no visual experience composer
* Envio de parâmetros para o Target
* Rastrear eventos de conversão
* Habilitar suporte entre domínios
* Atualizar públicos e scripts de perfil
* Validar a implementação
* Depurar entrega de experiência do Target


## Pré-requisitos

Para concluir este tutorial, primeiro você deve:

* Ter uma compreensão técnica de sua implementação atual da at.js do Target
* Verifique se você tem uma [função de Editor ou Editor](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) para sua instância do Target, para que possa tentar exemplos por conta própria
* Saber como configurar atividades no Adobe Target. Se você precisar de uma atualização, os seguintes tutoriais e guias serão úteis para esta lição:
   * [Usar o Visual Experience Composer](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html)
   * [Usar o Experience Composer baseado em formulário](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html)
   * [Criar atividades de direcionamento de experiência](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html)

Quando estiver pronto, a primeira etapa para uma migração bem-sucedida é [saber mais sobre o processo de migração](migration-overview.md) e a diferença entre a at.js e o Platform Web SDK.

>[!NOTE]
>
>Estamos empenhados em ajudá-lo a ter sucesso com a migração do Target da at.js para o Web SDK. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
