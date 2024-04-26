---
title: Configurar um fluxo de dados para o SDK da Web da plataforma
description: Saiba como habilitar um fluxo de dados e configurar soluções de Experience Cloud. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Web SDK,Datastreams
jira: KT-15399
exl-id: 20f770d1-eb0f-41a9-b451-4069a0a91fc4
source-git-commit: 8602110d2b2ddc561e45f201e3bcce5e6a6f8261
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 4%

---

# Configurar uma sequência de dados

Saiba como configurar uma sequência de dados para o Adobe Experience Platform Web SDK.

[Datastreams](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview) informe ao Adobe Experience Platform Edge Network para onde enviar os dados coletados pelo SDK da Web da plataforma. Na configuração dos datastreams, você habilita os aplicativos Experience Cloud, a conta Experience Platform e o encaminhamento de eventos.

![SDK da Web, fluxos de dados e diagrama de Edge Network](assets/dc-websdk-datastreams.png)

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

**Para criar um fluxo de dados:**

1. Abra o [Interface da coleção de dados](https://launch.adobe.com/){target="_blank"}
1. Verifique se você está na sandbox correta

   >[!NOTE]
   >
   >Se você for o cliente de um aplicativo baseado em plataforma, como o Real-Time CDP ou o Journey Optimizer, recomendamos usar uma sandbox de desenvolvimento para este tutorial. Caso não esteja, use o **[!UICONTROL Prod]** sandbox.

1. Ir para **[!UICONTROL Datastreams]** na navegação à esquerda
1. Selecionar **[!UICONTROL Nova sequência de dados]**
1. Enter `Luma Web SDK: Development Environment` como o **[!UICONTROL Nome]**. Esse nome é referenciado posteriormente ao configurar a extensão do SDK da Web na propriedade da tag.
1. Selecionar **[!UICONTROL Salvar]**

   ![Criar a sequência de dados](assets/datastream-create-new-datastream.png)

   >[!NOTE]
   >
   >Você só precisará selecionar um esquema se estiver usando a variável [Preparação de dados para coleção de dados](/help/data-collection/edge/data-prep.md) recurso.

Na próxima tela, você poderá adicionar serviços, como aplicativos Adobe, ao fluxo de dados. No entanto, você não adicionará serviços neste ponto do tutorial. Você fará isso mais tarde nas lições [Configurar Experience Platform](setup-experience-platform.md), [Configurar o Analytics](setup-analytics.md), [Configurar Audience Manager](setup-audience-manager.md), [Configurar o Target](setup-target.md)ou [Encaminhamento de evento](setup-event-forwarding.md).

>[!NOTE]
>
>Ao implementar o SDK da Web da Platform em seu próprio site, você deve criar três fluxos de dados para mapear para seus três ambientes de tag (desenvolvimento, preparo e produção). Se estiver usando o SDK da Web da Platform com aplicativos baseados na plataforma, como Adobe Real-time Customer Data Platform ou Adobe Journey Optimizer, certifique-se de criar esses fluxos de dados nas sandboxes da Platform apropriadas.

## Substituir um fluxo de dados

[Substituições de fluxo de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overrides) O permite definir configurações adicionais para o fluxo de dados e, em seguida, substituir a configuração padrão em determinadas condições.

A substituição da configuração da sequência de dados é um processo de duas etapas:

1. Primeiro, você define substituições de fluxo de dados na configuração do serviço de fluxo de dados. Por exemplo, você pode definir conjuntos de relatórios alternativos do Analytics, espaços de trabalho do Target ou conjuntos de dados da Platform para usar como substituições.
1. Em seguida, você envia as substituições para o Edge Network com uma ação de evento de envio do SDK da Web ou por uma configuração na extensão de tag do SDK da Web.

No [Configurar o Adobe Analytics](setup-analytics.md) lição, você substitui o conjunto de relatórios de uma página usando a ação enviar evento do SDK da Web da plataforma.

Agora você está pronto para instalar a extensão SDK da Web da Platform na sua propriedade de tag!

[Próximo: ](install-web-sdk.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar feedback geral ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
