---
title: Migração do Target da at.js 2.x para o SDK da Web
description: Saiba como migrar uma implementação do Adobe Target da at.js 2.x para o Adobe Experience Platform Web SDK. Os tópicos incluem o carregamento da biblioteca do JavaScript, o envio de parâmetros, atividades de renderização e outras chamadas importantes.
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: c8920fde-ad6b-4f2d-a35f-ce865b35bba0
source-git-commit: eebe598e55228d038dfc2adb97df0f8ff03748ac
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 4%

---

# Migração do Target da at.js 2.x para o SDK da Web da plataforma

Este guia é para implementadores experientes do Adobe Target que aprendem a migrar uma implementação do at.js para o SDK da Web da Adobe Experience Platform.

O Adobe Experience Platform Web SDK é uma biblioteca JavaScript no lado do cliente que permite aos clientes da Adobe Experience Cloud interagir com os serviços do Experience Cloud por meio do Edge Network da Adobe Experience Platform. Esta nova biblioteca combina os recursos das bibliotecas de aplicativos Adobe separadas em um único pacote leve que pode aproveitar ao máximo os novos recursos do Adobe Experience Platform.

## Principais benefícios

Alguns dos benefícios do SDK da Web da Platform em comparação à biblioteca at.js independente incluem:

* Compartilhamento mais rápido de públicos do [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=pt-BR)
* Integração do Target ao Journey Optimizer para oferecer suporte à [entrega de Offer decisioning](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* Capacidade de usar [ids primárias](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/generate-first-party-device-ids.html?lang=pt-BR) para gerar a ECID para identificação de visitantes de maior duração
* Consolidação de chamadas de rede em aplicativos Adobe
* Uma área menor para melhorar as métricas de velocidade da página
* Uma integração mais estreita com o Adobe Analytics, que não depende da compilação de informações de chamadas de rede separadas
* Flexibilidade adicional na implementação para desenvolvedores

Indiscutivelmente, o maior benefício para os clientes do Target da migração é a integração com o Real-time Customer Data Platform. A Real-Time CDP oferece excelentes recursos de criação de público com base na gama completa de dados assimilados no Experience Platform e em seu recurso de Perfil do cliente em tempo real. Uma estrutura de governança de dados integrada automatiza o uso responsável desses dados. A IA do cliente permite usar facilmente modelos de aprendizado de máquina para criar modelos de propensão e churn cuja saída pode ser compartilhada de volta com a Adobe Target. E, por fim, os clientes dos complementos opcionais de Assistência médica, Privacidade e segurança podem usar o recurso de aplicação de consentimento para aplicar facilmente as preferências de consentimento de clientes individuais. O SDK da Web da Platform é um requisito para usar esses recursos da RTCDP no canal da Web.

## Objetivos de aprendizagem

Ao final deste tutorial, você poderá:

* Entender as diferenças de implementação do Target entre a at.js e o SDK da Web da plataforma
* Definir a configuração inicial da funcionalidade do Target
* Atualizar a biblioteca at.js para o SDK da Web da plataforma
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

Quando estiver pronto, a primeira etapa para uma migração bem-sucedida é [saber mais sobre o processo de migração](migration-overview.md) e a diferença entre a at.js e o SDK da Web da Platform.

>[!NOTE]
>
>Estamos empenhados em ajudar você a ter sucesso com a migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
