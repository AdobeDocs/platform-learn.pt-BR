---
title: Configurar um fluxo de dados para o SDK da Web da plataforma
description: Saiba como habilitar um fluxo de dados e configurar soluções de Experience Cloud. Esta lição é parte do tutorial Implementar a Adobe Experience Cloud com o SDK da web.
feature: Web SDK,Datastreams
jira: KT-15399
exl-id: 20f770d1-eb0f-41a9-b451-4069a0a91fc4
source-git-commit: a8431137e0551d1135763138da3ca262cb4bc4ee
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 8%

---

# Configurar uma sequência de dados

Saiba como configurar uma sequência de dados para o SDK da web da Adobe Experience Platform.

[Datastreams](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview) informa ao Adobe Experience Platform Edge Network para onde enviar os dados coletados pelo SDK da Web da plataforma. Na configuração dos datastreams, você habilita os aplicativos Experience Cloud, a conta Experience Platform e o encaminhamento de eventos.

![SDK da Web, sequências de dados e diagrama de Edge Network](assets/dc-websdk-datastreams.png)

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Criar um fluxo de dados
* Introdução a substituições de sequência de dados

## Pré-requisitos

Antes de configurar o fluxo de dados, você já deve ter concluído as seguintes lições:

* [Configurar um esquema](configure-schemas.md)
* [Configurar um namespace de identidade](configure-identities.md)

## Criar um fluxo de dados

Agora, você pode criar um fluxo de dados para informar ao Platform Edge Network para onde enviar os dados coletados pelo SDK da Web.

**Para criar uma sequência de dados:**

1. Abrir a [interface de Coleção de Dados](https://launch.adobe.com/){target="_blank"}
1. Verifique se você está na sandbox correta

   >[!NOTE]
   >
   >Se você for o cliente de um aplicativo baseado em plataforma, como o Real-Time CDP ou o Journey Optimizer, recomendamos usar uma sandbox de desenvolvimento para este tutorial. Caso contrário, use a sandbox **[!UICONTROL Prod]**.

1. Vá para **[!UICONTROL Datastreams]** na navegação à esquerda
1. Selecionar **[!UICONTROL Nova Sequência De Dados]**
1. Digite `Luma Web SDK: Development Environment` como **[!UICONTROL Nome]**. Esse nome é referenciado posteriormente ao configurar a extensão do SDK da Web na propriedade da tag.
1. Selecione **[!UICONTROL Salvar]**

   ![Criar a sequência de dados](assets/datastream-create-new-datastream.png)

   >[!NOTE]
   >
   >Você não precisa selecionar um esquema. Uma seleção de esquema só será necessária se você estiver usando o recurso [Preparação de Dados para a Coleção de Dados](/help/data-collection/edge/data-prep.md).

Na próxima tela, você poderá adicionar serviços, como aplicativos Adobe, ao fluxo de dados. No entanto, você não adicionará serviços nesse momento. Você fará isso posteriormente nas lições [Configurar Experience Platform](setup-experience-platform.md), [Configurar o Analytics](setup-analytics.md), [Configurar Audience Manager](setup-audience-manager.md), [Configurar Target](setup-target.md) ou [Encaminhamento de Eventos](setup-event-forwarding.md).

>[!NOTE]
>
>Ao implementar o SDK da Web da Platform em seu próprio site, você deve criar três fluxos de dados para mapear para seus três ambientes de tag (desenvolvimento, preparo e produção). Se estiver usando o SDK da Web da Platform com aplicativos baseados na plataforma, como Adobe Real-time Customer Data Platform ou Adobe Journey Optimizer, certifique-se de criar esses fluxos de dados nas sandboxes da Platform apropriadas.

## Substituir um fluxo de dados

[Substituições de sequência de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overrides) permitem definir configurações adicionais para a sequência de dados e substituir a configuração padrão em determinadas condições.

A substituição da configuração da sequência de dados é um processo de duas etapas:

1. Primeiro, você define substituições de fluxo de dados na configuração do serviço de fluxo de dados. Por exemplo, você pode definir conjuntos de relatórios alternativos do Analytics, espaços de trabalho do Target ou conjuntos de dados da Platform para usar como substituições.
1. Em seguida, você envia as substituições para o Edge Network com uma ação de evento de envio do SDK da Web ou por uma configuração na extensão de tag do SDK da Web.

Na lição [Configurar Adobe Analytics](setup-analytics.md), você substitui o conjunto de relatórios de uma página usando a Ação de evento Enviar SDK da Web da plataforma.

Agora você está pronto para instalar a extensão SDK da Web da Platform na sua propriedade de tag!

[Próximo: ](install-web-sdk.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [postagem de Discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
