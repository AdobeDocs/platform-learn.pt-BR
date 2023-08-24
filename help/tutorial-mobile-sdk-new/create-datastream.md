---
title: Configurar uma sequência de dados
description: Saiba como criar um fluxo de dados no Experience Platform.
feature: Mobile SDK,Datastreams
hide: true
source-git-commit: 7de7c7e13ea6d02f1193620e0cc35299e07d59e5
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 9%

---


# Criar um fluxo de dados

Saiba como criar um fluxo de dados no Experience Platform.

Uma sequência de dados é uma configuração do lado do servidor na Platform Edge Network. A sequência de dados garante que os dados recebidos na Platform Edge Network sejam roteados adequadamente para aplicativos e serviços da Adobe Experience Cloud. Para obter mais informações, consulte [documentação](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=pt-BR) ou esta [vídeo](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=pt-BR).

## Pré-requisitos

Para criar um fluxo de dados, sua organização deve ser provisionada para esse recurso na interface da Coleção de dados (antiga [!UICONTROL Launch]) e você deve ter permissões de usuário para [!UICONTROL Experience Platform] > [!UICONTROL Coleta de dados] > **[!UICONTROL Gerenciar fluxos de dados]** e **[!UICONTROL Exibir fluxos de dados]**.

## Objetivos de aprendizagem

Nesta lição, você vai:

* Saber quando usar um fluxo de dados.
* Criar um fluxo de dados.
* Configurar uma sequência de dados.

## Criar um fluxo de dados

As sequências de dados podem ser criadas no [!UICONTROL Coleta de dados] usando a [!UICONTROL Sequência de dados] ferramenta de configuração. Para criar um fluxo de dados:

1. Verifique se você está na sandbox de Experience Platform correta, pois as sequências de dados são definidas em um nível de sandbox.
1. Selecionar **[!UICONTROL Datastreams]** no painel esquerdo.
1. Selecione **[!UICONTROL Novo fluxo de dados]**.

   ![início: datastreams](assets/datastream-new.png)

1. Forneça um **[!UICONTROL Nome]**, por exemplo `Luma Mobile App` e uma **[!UICONTROL Descrição]**, por exemplo `Datastream for Luma Mobile App`.
1. Selecione o schema criado na lição anterior do **Esquema de evento** uma lista.
1. Selecione **[!UICONTROL Salvar]**.

   ![novos fluxos de dados](assets/datastream-name.png)


## Adicionar serviços

Em seguida, você conecta os serviços do Experience Cloud ao fluxo de dados. Quando o SDK móvel da Platform envia dados para a rede de borda, a sequência de dados envia os dados para estes serviços:

1. Selecione **[!UICONTROL Adicionar serviço]**.

1. Adicionar **[!UICONTROL Adobe Analytics]** do [!UICONTROL Serviço] lista,

1. Informe o nome do site de relatório que deseja usar no **[!UICONTROL ID do conjunto de relatórios]**.

1. Habilitar o serviço alternando **[!UICONTROL Ativado]** em.

1. Selecione **[!UICONTROL Salvar]**.

   ![Adicionar o Adobe Analytics como serviço de sequência de dados](assets/datastream-service-aa.png)

Talvez você também queira ativar o serviço Adobe Experience Platform.

>[!IMPORTANT]
>
>Você só pode ativar o serviço Adobe Experience Platform ao criar um conjunto de dados de evento. Se você ainda não tiver um conjunto de dados de evento criado, siga as instruções [aqui](platform.md).

1. Clique em ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Adicionar serviço]** para adicionar outro serviço.

1. Selecione **[!UICONTROL Adobe Experience Platform]** na lista [!UICONTROL Serviço].

1. Habilitar o serviço alternando **[!UICONTROL Ativado]** em.

1. Selecione o **[!UICONTROL Conjunto de dados do evento]** que você criou como parte da [Criar um conjunto de dados](platform.md#create-a-dataset) instrução, por exemplo **Conjunto de dados de evento do aplicativo móvel Luma**

1. Selecione **[!UICONTROL Salvar]**.

   ![Adicionar o Adobe Experience Platform como um serviço de sequência de dados](assets/datastream-service-aep.png)
1. A configuração final deve ser semelhante a esta.

   ![configurações de sequência de dados](assets/datastream-settings.png)


>[!NOTE]
>
>Habilitar cada um dos serviços que sua organização usa garante que os dados coletados no aplicativo móvel possam ser usados em qualquer lugar. Para obter mais informações sobre configurações de sequência de dados, consulte a documentação [aqui](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html#adobe-experience-platform-settings).

Ao implementar o SDK do Platform Mobile em seu próprio aplicativo, você deve criar três fluxos de dados para mapear para seus três ambientes de tag (desenvolvimento, preparo e produção). Se você estiver usando o SDK móvel da Platform com aplicativos baseados na plataforma, como Adobe Real-time Customer Data Platform ou Adobe Journey Optimizer, certifique-se de criar esses fluxos de dados nas sandboxes adequadas da Platform.

>[!SUCCESS]
>
>Agora você tem um fluxo de dados para usar no restante do tutorial.<br/>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Próximo: **[Configurar tags](configure-tags.md)**
