---
title: Configurar uma sequência de dados
description: Saiba como criar um fluxo de dados no Experience Platform.
feature: Mobile SDK,Datastreams
exl-id: 7b83f834-d1fb-45d1-8bcf-bc621f94725c
source-git-commit: 94ca4a238c241518219fb2e8d73f775836f86d86
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 8%

---

# Criar um fluxo de dados

Saiba como criar um fluxo de dados no Experience Platform.

>[!INFO]
>
> Este tutorial será substituído por um novo tutorial usando um novo aplicativo móvel de amostra no final de novembro de 2023

Uma sequência de dados é uma configuração do lado do servidor na Platform Edge Network.  A sequência de dados garante que os dados recebidos na Platform Edge Network sejam roteados adequadamente para aplicativos e serviços da Adobe Experience Cloud. Para obter mais informações, consulte [documentação](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=pt-BR) ou esta [vídeo](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=pt-BR).

## Pré-requisitos

Para criar um fluxo de dados, sua organização deve ser provisionada para esse recurso na interface da Coleção de dados (antiga [!UICONTROL Launch]) e você deve ter permissões de usuário para [!UICONTROL Experience Platform] > [!UICONTROL Coleta de dados] > **[!UICONTROL Gerenciar fluxos de dados]** e **[!UICONTROL Exibir fluxos de dados]**.

## Objetivos de aprendizagem

Nesta lição, você vai:

* Saber quando usar um fluxo de dados.
* Criar um fluxo de dados.
* Configurar uma sequência de dados.

## Criar um fluxo de dados

As sequências de dados podem ser criadas no [!UICONTROL Coleta de dados] usando a [!UICONTROL Sequência de dados] ferramenta de configuração. Para criar um fluxo de dados:

1. Verifique se você está na sandbox correta da Platform.
1. Selecione **[!UICONTROL Novo fluxo de dados]**.

   ![início: datastreams](assets/mobile-datastream-new.png)

1. Forneça um nome, por exemplo `Luma App`.
1. Selecione o schema criado na lição anterior.
1. Selecione **[!UICONTROL Salvar]**.

   ![novos fluxos de dados](assets/mobile-datastream-name.png)


## Adicionar serviços

Em seguida, você pode conectar os serviços do Experience Cloud ao fluxo de dados. Quando o SDK móvel da Platform envia dados para a rede de borda, a sequência de dados enviará os dados para estes serviços:

1. Adicionar **[!UICONTROL Adobe Analytics]** e fornecer um conjunto de relatórios.

1. Ativar **[!UICONTROL Adobe Audience Manager]** (opcional).

1. Ativar **[!UICONTROL Adobe Experience Platform]** e fornecer uma **[!UICONTROL conjunto de dados]** (opcional).
   * Se você ainda não tiver um conjunto de dados criado, siga as instruções [aqui](platform.md).

1. A configuração final deve ser semelhante a esta.
   ![configurações de sequência de dados](assets/mobile-datastream-settings.png)


>[!NOTE]
>
>Habilitar cada um dos serviços que sua organização usa garante que os dados coletados no aplicativo móvel possam ser usados em qualquer lugar. Encontre mais informações sobre configurações de sequência de dados, revise a documentação [aqui](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html#adobe-experience-platform-settings).

Ao implementar o SDK do Platform Mobile em seu próprio site, você deve criar três fluxos de dados para mapear para seus três ambientes de tag (desenvolvimento, preparo e produção). Se você estiver usando o SDK móvel da Platform com aplicativos baseados na plataforma, como Adobe Real-time Customer Data Platform ou Adobe Journey Optimizer, certifique-se de criar esses fluxos de dados nas sandboxes adequadas da Platform.

Próximo: **[Configurar tags](configure-tags.md)**

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar feedback geral ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
