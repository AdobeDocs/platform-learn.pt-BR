---
title: Configurar uma sequência de dados para implementações do SDK móvel da Platform
description: Saiba como criar uma sequência de dados na Experience Platform.
feature: Mobile SDK,Datastreams
jira: KT-14625
exl-id: 7b83f834-d1fb-45d1-8bcf-bc621f94725c
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 6%

---

# Criar um fluxo de dados

Saiba como criar uma sequência de dados na Experience Platform.

Uma sequência de dados é uma configuração do lado do servidor no Platform Edge Network. A sequência de dados garante que os dados recebidos no Edge Network da plataforma sejam roteados adequadamente para aplicativos e serviços da Adobe Experience Cloud. Para obter mais informações, consulte a [documentação](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=pt-BR) ou este [vídeo](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=pt-BR).

![Arquitetura](assets/architecture.png)

## Pré-requisitos

Para criar uma sequência de dados, sua organização deve ser provisionada para esse recurso na interface da Coleção de dados (antigo [!UICONTROL Launch]) e você deve ter permissões de usuário para gerenciar e exibir sequências de dados.

## Objetivos de aprendizagem

Nesta lição, você vai:

* Saber quando usar um fluxo de dados.
* Criar um fluxo de dados.
* Configurar um fluxo de dados.

## Criar um fluxo de dados

As sequências de dados podem ser criadas na interface [!UICONTROL Coleção de Dados] usando a ferramenta de configuração [!UICONTROL Sequência de Dados]. Para criar um fluxo de dados:

1. Verifique se você está na sandbox de Experience Platform correta, pois os fluxos de dados são definidos em um nível de sandbox.
1. Selecione **[!UICONTROL Datastreams]** no painel esquerdo.
1. Selecione **[!UICONTROL Nova Sequência De Dados]**.

   ![início do datastreams](assets/datastream-new.png)

1. Forneça um **[!UICONTROL Nome]**, por exemplo `Luma Mobile App` e uma **[!UICONTROL Descrição]**, por exemplo `Datastream for Luma Mobile App`.

   >[!NOTE]
   >
   >Lembrete final: se você estiver assistindo a este tutorial com várias pessoas em uma única sandbox ou se estiver usando uma conta compartilhada, considere anexar ou anexar uma identificação como parte de suas convenções de nomenclatura. Por exemplo, em vez de `Luma Mobile App Event Dataset`, use `Luma Mobile App Event Dataset - Joe Smith`. Consulte também a observação em [Visão geral](overview.md).

1. Selecione o esquema criado na lição anterior na lista **Esquema de evento**.
1. Selecione **[!UICONTROL Salvar]**.

   ![novas sequências de dados](assets/datastream-name.png)


## Adicionar serviços

Ao percorrer as lições (opcionais) do [Analytics](analytics.md) e do [Experience Platform](platform.md) neste tutorial, você adiciona serviços à sua sequência de dados para que os dados enviados para o Edge Network da plataforma sejam encaminhados para esses aplicativos.

<!--

### Adobe Analytics

1. Select **[!UICONTROL Add Service]**.

1. Add **[!UICONTROL Adobe Analytics]** from the [!UICONTROL Service] list, 

1. Enter the name of the report site that you want to use in **[!UICONTROL Report Suite ID]**.

1. Enable the service by switching **[!UICONTROL Enabled]** on.

1. Select **[!UICONTROL Save]**.

   ![Add Adobe Analytics as datastream service](assets/datastream-service-aa.png)


### Adobe Experience Platform

You might also want to enable the Adobe Experience Platform service. 

>[!IMPORTANT]
>
>You can only enable the Adobe Experience Platform service when having created an event dataset. If you don't already have an event dataset created, follow the instructions [here](platform.md).

1. Click ![Add](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Add Service]** to add another service.

1. Select **[!UICONTROL Adobe Experience Platform]** from the [!UICONTROL Service] list.

1. Enable the service by switching **[!UICONTROL Enabled]** on.

1. Select the **[!UICONTROL Event Dataset]** that you created as part of the [Create a dataset](platform.md#create-a-dataset) instructions, for example **Luma Mobile App Event Dataset**

1. Select **[!UICONTROL Save]**.

   ![Add Adobe Experience Platform as a datastream service](assets/datastream-service-aep.png)
1. The final configuration should look something like this.
   
   ![datastream settings](assets/datastream-settings.png)

-->


>[!NOTE]
>
>Habilitar cada um dos serviços que sua organização usa garante que os dados coletados no aplicativo móvel possam ser usados em qualquer lugar. Para obter mais informações sobre as configurações da sequência de dados, consulte a documentação [aqui](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=pt-BR).

Ao implementar o SDK móvel da Platform em seu próprio aplicativo, você deve criar três fluxos de dados para mapear para seus três ambientes de tag (desenvolvimento, preparo e produção). Se você estiver usando o SDK móvel da Platform com aplicativos baseados na plataforma, como Adobe Real-time Customer Data Platform ou Adobe Journey Optimizer, certifique-se de criar esses fluxos de dados nas sandboxes apropriadas.

>[!SUCCESS]
>
>Agora você tem um fluxo de dados para usar no restante do tutorial.
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-os nesta [postagem de Discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=pt)

Próximo: **[Configurar uma propriedade de marca](configure-tags.md)**
