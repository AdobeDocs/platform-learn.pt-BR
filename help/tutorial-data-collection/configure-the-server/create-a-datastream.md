---
title: Criar um fluxo de dados
description: Criar um fluxo de dados
exl-id: 4a33a7f3-8bd8-4d28-9ae4-a0609444485f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---

# Criar um fluxo de dados

Os dados enviados de seu site com o SDK da Web da plataforma atingem um conjunto de servidores do Adobe chamados de [Rede de borda Adobe Experience Platform](https://business.adobe.com/products/experience-platform/experience-platform-edge-network.html). Essa rede pode enviar seus dados para o [Conjunto de dados Adobe Experience Platform criado anteriormente](create-a-schema.md) e outros produtos da Adobe Experience Cloud. Esses produtos Adobe também podem responder com dados para a sua página da Web. Por exemplo, a Edge Network pode retornar conteúdo de personalização da Adobe Target.

Para configurar quais produtos do Adobe Edge Network envia dados de e para, você deve criar um conjunto de dados. Quando a Edge Network recebe dados da sua página da Web, ela consulta o armazenamento de dados criado, lê a configuração e encaminha os dados para os produtos Adobe apropriados.

![Configuração do produto Datastream](../assets/datastream-diagram.png)

1. Para criar um armazenamento de dados, primeiro você deve navegar até a interface do usuário da Coleta de dados. No canto superior direito da Plataforma, clique em **[!UICONTROL Seletor de aplicativo]** e selecione **[!UICONTROL Coleta de dados]** no menu suspenso.
   ![Menu de coleta de dados](../assets/data-collection-menu.png)
1. Quando a interface da Coleta de dados for exibida, selecione **[!UICONTROL Datastreams]** na navegação à esquerda e, em seguida, na **[!UICONTROL Novo fluxo de dados]** no canto superior direito.
1. Forneça um nome para o armazenamento de dados, selecione [o esquema criado anteriormente](create-a-schema.md) como **[!UICONTROL Conjunto de dados do evento]** e selecione **[!UICONTROL Salvar]** (o mapeamento é abordado posteriormente).
   ![Nome e descrição do conjunto de dados](../assets/datastream-name-description.png)

## Adicionar serviço ao armazenamento de dados

A próxima tela permite que você adicione quais produtos e serviços do Adobe devem receber os dados enviados do seu site.

1. Selecione o **[!UICONTROL Adicionar Serviço]** comando. Para os fins deste tutorial, ative somente o Adobe Experience Platform, selecione [o conjunto de dados criado anteriormente](create-a-dataset.md) e selecione **[!UICONTROL Salvar]** no canto superior direito. Seu armazenamento de dados foi criado.
   ![Configuração do produto Datastream](../assets/datastream-product-configuration.png)

## Ambientes de fluxo de dados

As empresas geralmente têm um caminho de promoção para qualquer atualização de site. Alguém na empresa (um profissional de marketing ou engenheiro, dependendo das mudanças) normalmente testa suas alterações em um ambiente de desenvolvimento que somente essa pessoa está usando. Uma vez que se sintam confortáveis com as alterações, as alterações são promovidas para um ambiente de preparo onde recebem mais testes. Por fim, as alterações são publicadas no site de produção que os usuários veem. Os datastreams são compatíveis com esse padrão de promoção.

Se você estiver suportando aplicativos baseados em plataforma como Real-time CDP, Journey Optimizer ou Customer Journey Analytics, os conjuntos de dados adicionais deverão ser criados nas sandboxes separadas da Platform que correspondem a esses ambientes.

Se você não for um cliente da Platform, poderá criar vários conjuntos de dados em uma única sandbox e usar o recurso de cópia do conjunto de dados para duplicar as configurações.

O servidor agora está totalmente configurado para receber dados de sua página da Web.

[Próximo: ](../configure-the-client/whats-a-data-layer.md)

>[!NOTE]
>
>Obrigado por investir seu tempo para aprender sobre a coleta de dados. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
