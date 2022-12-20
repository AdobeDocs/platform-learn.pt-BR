---
title: Configurar um conjunto de dados
description: Saiba como criar um armazenamento de dados no Experience Platform.
exl-id: 7b83f834-d1fb-45d1-8bcf-bc621f94725c
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 6%

---

# Criar um fluxo de dados

Saiba como criar um armazenamento de dados no Experience Platform.

Um armazenamento de dados é uma configuração do lado do servidor na Rede de borda da plataforma.  O armazenamento de dados garante que os dados recebidos na Rede de borda da plataforma sejam roteados para aplicativos e serviços da Adobe Experience Cloud adequadamente. Para obter mais informações, consulte o [documentação](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=pt-BR) ou [vídeo](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=pt-BR).

## Pré-requisitos

Para criar um armazenamento de dados, sua organização deve ser provisionada para esse recurso na interface da Coleta de dados (anteriormente [!UICONTROL Launch]) e você deve ter permissões de usuário para [!UICONTROL Experience Platform] > [!UICONTROL Coleta de dados] > **[!UICONTROL Gerenciar datastreams]** e **[!UICONTROL Visualizar fluxos de dados]**.

## Objetivos de aprendizagem

Nesta lição, você:

* Saiba quando usar um armazenamento de dados.
* Criar um fluxo de dados.
* Configure um armazenamento de dados.

## Criar um fluxo de dados

Os datastreams podem ser criados no [!UICONTROL Coleta de dados] usando a [!UICONTROL Datastream] ferramenta de configuração. Para criar um armazenamento de dados:

1. Verifique se você está na sandbox de plataforma correta.
1. Selecionar **[!UICONTROL Novo fluxo de dados]**.

   ![página inicial do datastreams](assets/mobile-datastream-new.png)

1. Forneça um nome, por exemplo `Luma App`.
1. Selecione o schema que você criou na lição anterior.
1. Selecione **[!UICONTROL Salvar]**.

   ![novos datastreams](assets/mobile-datastream-name.png)


## Adicionar serviços

Em seguida, é possível conectar os serviços do Experience Cloud ao armazenamento de dados. Quando o SDK do Platform Mobile envia dados para a Edge Network, o armazenamento de dados enviará os dados para esses serviços:

1. Adicionar **[!UICONTROL Adobe Analytics]** e fornecer um conjunto de relatórios.

1. Habilitar **[!UICONTROL Adobe Audience Manager]** (opcional).

1. Habilitar **[!UICONTROL Adobe Experience Platform]** e **[!UICONTROL conjunto de dados]** (opcional).
   * Se ainda não tiver um conjunto de dados criado, siga as instruções [here](platform.md).

1. A configuração final deve ser parecida com isso.
   ![configurações do datastream](assets/mobile-datastream-settings.png)


>[!NOTE]
>
>Habilitar cada um dos serviços que sua organização usa garante que os dados coletados no aplicativo móvel possam ser usados em todos os lugares. Encontre mais informações sobre as configurações do armazenamento de dados. Consulte a documentação [here](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html#adobe-experience-platform-settings).

Ao implementar o SDK do Platform Mobile em seu próprio site, você deve criar três conjuntos de dados para mapear para seus três ambientes de tags (desenvolvimento, estágio e produção). Se você estiver usando o SDK do Platform Mobile com aplicativos baseados em plataforma, como o Adobe Real-time Customer Data Platform ou o Adobe Journey Optimizer, certifique-se de criar esses conjuntos de dados nas sandboxes apropriadas da Platform.

Próximo: **[Configurar tags](configure-tags.md)**

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender sobre o Adobe Experience Platform Mobile SDK. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
