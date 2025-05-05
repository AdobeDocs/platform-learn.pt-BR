---
title: Instalar e configurar a extensão de tag do Adobe Experience Platform Web SDK
description: Saiba como instalar e configurar a extensão de tag do Platform Web SDK na interface da Coleção de dados. Esta lição é parte do tutorial Implementar a Adobe Experience Cloud com o SDK da web.
feature: Web SDK, Tags
jira: KT-15404
exl-id: f30a44bb-99d7-476e-873a-b7802a0fe6aa
source-git-commit: e0359d1bade01f79d0f7aff6a6e69f3e4d0c3b62
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 11%

---

# Instalar a extensão de tag do Adobe Experience Platform Web SDK

Saiba como instalar e configurar a extensão de tag do Adobe Experience Platform Web SDK. A maneira mais fácil de implementar o Web SDK é usando o gerenciador de tags da Adobe, as tags (antes conhecidas como Launch). A extensão de tag do Platform Web SDK é a _única extensão de tag_ necessária para enviar dados para _todos os aplicativos da Adobe Experience Cloud_, incluindo [Analytics](setup-analytics.md), [Target](setup-target.md), [Audience Manager](setup-audience-manager.md), Real-Time Customer Data Platform e [Journey Optimizer](setup-web-channel.md)!

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Criar uma propriedade de tag na interface da Coleção de dados
* Instalar a extensão de tag do Platform Web SDK
* Mapear o fluxo de dados criado anteriormente para a extensão

## Pré-requisitos

Você deve ter concluído as lições anteriores neste tutorial:

* [Configurar uma sequência de dados](configure-datastream.md)

### Adicionar uma propriedade de tag

Primeiro, você deve ter uma propriedade de tag. Uma propriedade é um container para todas as JavaScript, regras e outros recursos necessários para coletar detalhes de uma página da Web e enviá-los para vários locais.

Crie uma nova propriedade de tag para o tutorial:

1. Abra a [interface da Coleção de Dados](https://experience.adobe.com/data-collection/){target="_blank"}
1. Selecione **[!UICONTROL Tags]** na navegação à esquerda
1. Selecione o botão **[!UICONTROL Nova propriedade]**
   ![Adicionar uma nova propriedade](assets/websdk-property-addNewProperty.png)
1. Como o **[!UICONTROL Nome]**, digite `Web SDK Course` (adicione seu nome ao final, se várias pessoas da sua empresa estiverem fazendo este tutorial)
1. Como os **[!UICONTROL Domínios]**, digite `enablementadobe.com` (explicado mais tarde)
1. Selecione **[!UICONTROL Salvar]**
   ![Detalhes da propriedade](assets/websdk-property-propertyDetails.png)

## Adicionar a extensão Web SDK

Com seu esquema XDM, sequência de dados e propriedade de tag criados, você está pronto para instalar a extensão Platform Web SDK:

1. Abra a nova propriedade de tag
1. Ir para **[!UICONTROL Extensões]** > **[!UICONTROL Catálogo]**
1. Pesquisar por `Adobe Experience Platform Web SDK`
1. Selecione **[!UICONTROL Instalar]**

   ![Instalar Extensão Web SDK](assets/extension-platform-web-sdk.png)


## Vincular a extensão ao fluxo de dados

Deixe a maioria das configurações padrão e atualize-as posteriormente, conforme necessário. A única coisa que você deve fazer agora é vincular a extensão ao seu fluxo de dados:

1. Em **[!UICONTROL Datastreams]**, selecione o método de entrada **[!UICONTROL Escolher da lista]**
1. Selecione a sandbox em que você criou o esquema, o namespace de identidade e o fluxo de dados
1. Selecione a sequência de dados criada anteriormente, `Luma Web SDK`
1. Selecione **[!UICONTROL Salvar]**

   >[!NOTE]
   >
   > Se não conseguir encontrar a sequência de dados, vá para a lição [Configurar uma sequência de dados](configure-datastream.md) e siga as etapas para criar uma

   ![Seleção de sequência de dados](assets/extension-luma-web-sdk-datastream-extension.png)

Para obter mais informações sobre cada seção da extensão, consulte [Configurar a extensão do Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/tags/extensions/client/web-sdk/web-sdk-extension-configuration).

>[!NOTE]
>
>Embora você não tenha configurado um CNAME na configuração [!UICONTROL domínio do Edge] nesta lição, a Adobe recomenda usar um CNAME ao implementar o Platform Web SDK em seu próprio site. Embora uma implementação CNAME não forneça benefícios em termos de duração do cookie, ela pode oferecer outros benefícios. Esses benefícios incluem bloqueadores de anúncios e navegadores menos comuns que impedem o envio de dados para domínios que eles classificam como rastreadores. Nesses casos, o uso de um CNAME pode impedir que a coleção de dados seja interrompida para usuários que utilizam essas ferramentas.

>[!NOTE]
>
>Durante este tutorial, você configura apenas um fluxo de dados e o associa a todos os ambientes de tag (desenvolvimento, preparo e produção). Ao implementar o Platform Web SDK em seu próprio site, você deve configurar um fluxo de dados separado para cada ambiente e mapeá-los de acordo na configuração da extensão.

Agora que você instalou o Platform Web SDK e o associou à sequência de dados, você está pronto para começar a coletar dados.

[Próximo: ](create-data-elements.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [postagem de discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=pt)
