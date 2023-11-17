---
title: Instalar e configurar a extensão de tag do SDK da Web da Adobe Experience Platform
description: Saiba como instalar e configurar a extensão de tag do SDK da Web da Platform na interface da Coleção de dados. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Web SDK
exl-id: f30a44bb-99d7-476e-873a-b7802a0fe6aa
source-git-commit: 4a12f8261cf1fb071bc70b6a04c34f6c16bcce64
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 15%

---

# Instalar a extensão de tag do SDK da Web da Adobe Experience Platform

Saiba como instalar e configurar a extensão de tag do SDK da Web da Platform na interface da Coleção de dados. Essa extensão de tag é a _somente extensão de tag_ necessário para enviar dados para _todos os aplicativos Adobe Experience Cloud_, incluindo [Analytics](setup-analytics.md), [Target](setup-target.md), [Audience Manager](setup-audience-manager.md), Real-time Customer Data Platform e Journey Optimizer!

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Criar uma propriedade de tag na interface da Coleção de dados
* Instalar a extensão de tag do SDK da Web da Platform
* Mapear o fluxo de dados criado anteriormente para a extensão

## Pré-requisitos

Você deve ter concluído as lições anteriores neste tutorial:

* [Configurar permissões](configure-permissions.md)
* [Configurar um esquema XDM](configure-schemas.md)
* [Configurar um namespace de identidade](configure-identities.md)
* [Configurar uma sequência de dados](configure-datastream.md)

## Instalar extensão SDK da Web do Experience Platform

### Adicionar uma propriedade do

Primeiro, você deve ter uma propriedade de tag. Uma propriedade é um container para todos os JavaScript, regras e outros recursos necessários para coletar detalhes de uma página da Web e enviá-los para vários locais.

Crie uma nova propriedade de tag para o tutorial:

1. Abra o [Interface da coleção de dados](https://launch.adobe.com/){target="_blank"}
1. Selecionar **[!UICONTROL Tags]** na navegação à esquerda
1. Selecione o botão **[!UICONTROL Nova propriedade]**
   ![Adicionar uma nova propriedade](assets/websdk-property-addNewProperty.png)
1. Como a variável **[!UICONTROL Nome]**, insira `Web SDK Course` (adicione seu nome ao final se várias pessoas da sua empresa estiverem fazendo este tutorial)
1. Como a variável **[!UICONTROL Domínios]**, insira `enablementadobe.com` (explicado posteriormente)
1. Selecione **[!UICONTROL Salvar]**
   ![Detalhes da propriedade](assets/websdk-property-propertyDetails.png)

## Adicionar a extensão SDK da Web

Com seu esquema XDM, sequência de dados e propriedade de tag criados, você está pronto para instalar a extensão SDK da Web da plataforma:

1. Abra a nova propriedade de tag
1. Ir para **[!UICONTROL Extensões]** > **[!UICONTROL Catálogo]**
1. Pesquisar por `Adobe Experience Platform Web SDK`
1. Selecionar **[!UICONTROL Instalar]**

   ![Instalar extensão SDK da Web](assets/extension-platform-web-sdk.jpg)


## Vincular o SDK da Web da Platform à sequência de dados

Deixe a maioria das configurações padrão e atualize-as posteriormente, conforme necessário. A única coisa que você deve fazer agora é vincular a extensão ao seu fluxo de dados:

1. Em **[!UICONTROL Datastreams]**, selecione o **[!UICONTROL Escolher da lista]** método de entrada
1. Selecione o fluxo de dados criado anteriormente, `Luma Web SDK`
1. Selecione **[!UICONTROL Salvar]**
   >[!NOTE]
   >
   > Se não conseguir encontrar o fluxo de dados, acesse o [Configurar um fluxo de dados](configure-datastream.md) lição e siga as etapas para criar uma

   ![Seleção de sequência de dados](assets/extension-luma-web-sdk-datastream-extension.png)

Agora que você instalou o SDK da Web da Platform e o associou à sequência de dados, você está pronto para começar a mapear elementos de dados para um objeto XDM com o esquema criado.

>[!NOTE]
>
>Durante este tutorial, você configura apenas um fluxo de dados e o associa a todos os ambientes de tag (desenvolvimento, preparo e produção). Ao implementar o SDK da Web da Platform em seu próprio site, você deve configurar um fluxo de dados separado para cada ambiente e mapeá-los para os ambientes de tag usando o **[!UICONTROL Método de entrada]** > **[!UICONTROL Inserir valores]**
>
>![Seleção de sequência de dados](assets/extension-luma-web-sdk-datastream-extension-enterValues.png)

>[!NOTE]
>
>Embora você não tenha configurado um CNAME no [!UICONTROL Domínio de borda] nesta lição, a Adobe recomenda usar um CNAME ao implementar o SDK da Web da Platform em seu próprio site. Embora uma implementação CNAME não forneça benefícios em termos de duração do cookie, ela pode oferecer outros benefícios. Esses benefícios incluem bloqueadores de anúncios e navegadores menos comuns que impedem o envio de dados para domínios que eles classificam como rastreadores. Nesses casos, o uso de um CNAME pode impedir que a coleção de dados seja interrompida para usuários que utilizam essas ferramentas.

Para obter mais informações sobre cada seção da extensão, consulte [Configurar a extensão SDK da Web do Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/web-sdk-extension-configuration.html?lang=pt-BR)



[Próximo: ](create-data-elements.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
