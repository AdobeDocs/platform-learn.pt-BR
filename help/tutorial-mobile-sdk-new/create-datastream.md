---
title: Configurar uma sequência de dados
description: Saiba como criar um fluxo de dados no Experience Platform.
feature: Mobile SDK,Datastreams
hide: true
exl-id: d8b9df3d-49ee-4578-92c6-0f920a86fe7e
source-git-commit: 4a12f8261cf1fb071bc70b6a04c34f6c16bcce64
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 10%

---

# Criar um fluxo de dados

Saiba como criar um fluxo de dados no Experience Platform.

Uma sequência de dados é uma configuração do lado do servidor na Platform Edge Network. A sequência de dados garante que os dados recebidos na Platform Edge Network sejam roteados adequadamente para aplicativos e serviços da Adobe Experience Cloud. Para obter mais informações, consulte [documentação](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=pt-BR) ou esta [vídeo](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=pt-BR).

![Arquitetura](assets/architecture.png)

## Pré-requisitos

Para criar um fluxo de dados, sua organização deve ser provisionada para esse recurso na interface da Coleção de dados (antiga [!UICONTROL Launch]) e você deve ter permissões de usuário para gerenciar e visualizar fluxos de dados.

## Objetivos de aprendizagem

Nesta lição, você vai:

* Saber quando usar um fluxo de dados.
* Criar um fluxo de dados.
* Configurar uma sequência de dados.

## Criar um fluxo de dados

As sequências de dados podem ser criadas no [!UICONTROL Coleta de dados] usando a [!UICONTROL Sequência de dados] ferramenta de configuração. Para criar um fluxo de dados:

1. Verifique se você está na sandbox de Experience Platform correta, pois os fluxos de dados são definidos em um nível de sandbox.
1. Selecionar **[!UICONTROL Datastreams]** no painel esquerdo.
1. Selecione **[!UICONTROL Novo fluxo de dados]**.

   ![início: datastreams](assets/datastream-new.png)

1. Forneça um **[!UICONTROL Nome]**, por exemplo `Luma Mobile App` e uma **[!UICONTROL Descrição]**, por exemplo `Datastream for Luma Mobile App`.

   >[!NOTE]
   >
   >Lembrete final: se você estiver assistindo a este tutorial com várias pessoas em uma única sandbox ou se estiver usando uma conta compartilhada, considere anexar ou anexar uma identificação como parte de suas convenções de nomenclatura. Por exemplo, em vez de `Luma Mobile App Event Dataset`, use `Luma Mobile App Event Dataset - Joe Smith`. Consulte também a nota em [Visão geral](overview.md).

1. Selecione o schema criado na lição anterior do **Esquema de evento** lista.
1. Selecione **[!UICONTROL Salvar]**.

   ![novos fluxos de dados](assets/datastream-name.png)


## Adicionar serviços

Ao acessar o (opcional) [Analytics](analytics.md) e [Experience Platform](platform.md) lições neste tutorial, você adiciona serviços ao seu fluxo de dados para que os dados enviados para a Platform Edge Network sejam encaminhados para esses aplicativos.

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
>Habilitar cada um dos serviços que sua organização usa garante que os dados coletados no aplicativo móvel possam ser usados em qualquer lugar. Para obter mais informações sobre configurações de sequência de dados, consulte a documentação [aqui](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=pt-BR).

Ao implementar o SDK móvel da Platform em seu próprio aplicativo, você deve criar três fluxos de dados para mapear para seus três ambientes de tag (desenvolvimento, preparo e produção). Se você estiver usando o SDK móvel da Platform com aplicativos baseados na plataforma, como Adobe Real-time Customer Data Platform ou Adobe Journey Optimizer, certifique-se de criar esses fluxos de dados nas sandboxes apropriadas.

>[!SUCCESS]
>
>Agora você tem um fluxo de dados para usar no restante do tutorial.
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Próximo: **[Configurar uma propriedade de tag](configure-tags.md)**
