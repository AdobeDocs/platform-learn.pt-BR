---
title: Introdução | Migrar o Target da at.js 2.x para o SDK da Web
description: Saiba como migrar uma implementação do Adobe Target da at.js 2.x para o Adobe Experience Platform Web SDK. Os tópicos incluem carregamento da biblioteca do JavaScript, envio de parâmetros, atividades de renderização e outras chamadas importantes.
recommendations: catalog,noDisplay
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 6%

---

# Migrar o Target da at.js 2.x para o SDK da Web da plataforma

Este guia é para implementadores experientes da Adobe Target para saber como migrar uma implementação da at.js para o Adobe Experience Platform Web SDK.

O SDK da Web da Adobe Experience Platform é uma biblioteca JavaScript do lado do cliente que permite que os clientes da Adobe Experience Cloud interajam com serviços do Experience Cloud por meio da Rede de borda da Adobe Experience Platform. Essa nova biblioteca combina os recursos das bibliotecas de aplicativos Adobe separadas em um único pacote leve que pode aproveitar ao máximo os novos recursos do Adobe Experience Platform.

## Principais benefícios

Alguns dos benefícios do SDK da Web da plataforma em comparação à biblioteca independente da at.js incluem:

* Compartilhamento mais rápido de públicos-alvo da [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=pt-BR)
* Integração do Target com o Journey Optimizer para oferecer suporte [Entrega de offer decisioning](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* Capacidade de usar [ids próprias](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/generate-first-party-device-ids.html?lang=pt-BR) para gerar a ECID para identificação de visitante por mais tempo
* Consolidação de chamadas de rede em aplicativos Adobe
* Um espaço menor para melhorar as métricas de velocidade da página
* Uma integração mais estreita com o Adobe Analytics que não depende da compilação de informações de chamadas de rede separadas
* Flexibilidade de implementação adicional para desenvolvedores

Argumentavelmente, o maior benefício da migração para os clientes do Target é a integração com o Real-time Customer Data Platform. A Real-Time CDP oferece excelentes recursos de criação de público-alvo com base na gama completa de dados assimilados no Experience Platform e em seu recurso de Perfil do cliente em tempo real. Uma estrutura integrada de governança de dados automatiza o uso responsável desses dados. O Customer AI permite usar facilmente modelos de aprendizado de máquina para construir propensão e modelos de rotatividade, cujo resultado pode ser compartilhado de volta na Adobe Target. E, por fim, os clientes dos complementos opcionais do Healthcare e Privacy &amp; Security Shield podem usar o recurso de imposição de consentimento para aplicar facilmente as preferências de consentimento de clientes individuais. O SDK da Web da plataforma é um requisito para usar esses recursos da RTCDP em seu canal da Web.

## Objetivos de aprendizagem

Ao final deste tutorial, você poderá:

* Entender as diferenças de implementação do Target entre at.js e o SDK da Web da plataforma
* Configurar a configuração inicial para a funcionalidade do Target
* Atualizar a biblioteca at.js para o SDK da Web da plataforma
* Renderizar atividades do criador de experiências visuais e baseadas em formulário
* Envio de parâmetros para o Target
* Rastrear eventos de conversão
* Habilitar suporte entre domínios
* Atualizar públicos-alvo e scripts de perfil
* Validar a implementação
* Depurar a entrega da experiência do Target


## Pré-requisitos

Para concluir este tutorial, primeiro você deve:

* Ter uma compreensão técnica da implementação atual do Target at.js
* Certifique-se de que você [Função de editor ou editor](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) para sua instância do Target , para que você possa tentar exemplos por conta própria
* Saiba como configurar atividades no Adobe Target. Se você precisar de um atualizador, os seguintes tutoriais e guias serão úteis nesta lição:
   * [Usar o Visual Experience Composer](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html)
   * [Usar o Experience Composer baseado em formulário](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html)
   * [Criar atividades de direcionamento de experiência](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html)

Quando estiver pronto, o primeiro passo para uma migração bem-sucedida será [saiba mais sobre o processo de migração](migration-overview.md) e como a at.js e o SDK da Web da plataforma diferem.

>[!NOTE]
>
>Temos o compromisso de ajudar você a ser bem-sucedido com sua migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, informe-nos ao publicar em [este debate comunitário](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).