---
title: Instalar e configurar a extensão de tag do Adobe Experience Platform Web SDK
description: Saiba como instalar e configurar a extensão de tag do SDK da Web da plataforma na interface da Coleta de dados. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Web SDK
exl-id: f30a44bb-99d7-476e-873a-b7802a0fe6aa
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 13%

---

# Instalar a extensão de tag do Adobe Experience Platform Web SDK

Saiba como instalar e configurar a extensão de tag do SDK da Web da plataforma na interface da Coleta de dados. Essa extensão de tag é o _somente extensão de tag_ necessário para enviar dados para o _todos os aplicativos Adobe Experience Cloud_, incluindo [Analytics](setup-analytics.md), [Target](setup-target.md), [Audience Manager](setup-audience-manager.md), Real-time Customer Data Platform e Journey Optimizer!

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Criar uma propriedade de tag na interface da Coleta de dados
* Instalar a extensão de tag do SDK da Web da plataforma
* Mapear o armazenamento de dados criado anteriormente para a extensão

## Pré-requisitos

Você deve ter concluído as lições anteriores neste tutorial:

* [Configurar permissões](configure-permissions.md)
* [Configurar um esquema XDM](configure-schemas.md)
* [Configurar um namespace de identidade](configure-identities.md)
* [Configurar um conjunto de dados](configure-datastream.md)

## Instalar a extensão SDK do Experience Platform Web

### Adicionar uma propriedade

Primeiro, você deve ter uma propriedade de tag. Uma propriedade é um contêiner de todos os recursos JavaScript, regras e outros recursos necessários para coletar detalhes de uma página da Web e enviá-los para vários locais.

Crie uma nova propriedade de tag para o tutorial:

1. Abra o [Interface da Coleta de dados](https://launch.adobe.com/){target=&quot;_blank&quot;}
1. Selecionar **[!UICONTROL Tags]** na navegação à esquerda
1. Selecione o botão **[!UICONTROL Nova propriedade]**
   ![Adicionar uma nova propriedade](assets/websdk-property-addNewProperty.png)
1. Como **[!UICONTROL Nome]**, insira `Web SDK Course` (adicione seu nome ao final, se várias pessoas de sua empresa estiverem recebendo este tutorial)
1. Como **[!UICONTROL Domínios]**, insira `enablementadobe.com` (explicado mais tarde)
1. Selecione **[!UICONTROL Salvar]**
   ![Detalhes da propriedade](assets/websdk-property-propertyDetails.png)

## Adicionar a extensão Web SDK

Com o esquema XDM, o conjunto de dados e a propriedade da tag criados agora, você está pronto para instalar a extensão SDK da Web da plataforma:

1. Abra sua nova propriedade de tag
1. Ir para **[!UICONTROL Extensões]** > **[!UICONTROL Catálogo]**
1. Procurar por `Adobe Experience Platform Web SDK`
1. Selecionar **[!UICONTROL Instalar]**

   ![Instalar a extensão do SDK da Web](assets/extension-platform-web-sdk.jpg)


## Vincular o SDK da Web da plataforma ao armazenamento de dados

Deixe a maioria das configurações padrão e atualize-as posteriormente, conforme necessário. A única coisa que você deve fazer agora é vincular a extensão ao armazenamento de dados:

1. Em **[!UICONTROL Datastreams]**, selecione o **[!UICONTROL Escolher na lista]** método de entrada
1. Selecione o conjunto de dados criado anteriormente, `Luma Web SDK`
1. Selecione **[!UICONTROL Salvar]**
   >[!NOTE]
   >
   > Se não conseguir encontrar o armazenamento de dados, acesse [Configurar um conjunto de dados](configure-datastream.md) lição e siga as etapas para criar uma

   ![Seleção de fluxo de dados](assets/extension-luma-web-sdk-datastream-extension.png)

Agora que você instalou o SDK da Web da plataforma e o associou ao armazenamento de dados, está pronto para iniciar o mapeamento de elementos de dados para um objeto XDM com o esquema criado.

>[!NOTE]
>
>Durante esse tutorial, você configura apenas um conjunto de dados e o associa a todos os ambientes de tags (desenvolvimento, estágio e produção). Ao implementar o SDK da Web da Plataforma em seu próprio site, você deve configurar um conjunto de dados separado para cada ambiente e mapeá-los para seus ambientes de tags usando o **[!UICONTROL Método de entrada]** > **[!UICONTROL Inserir valores]**
>
>![Seleção de fluxo de dados](assets/extension-luma-web-sdk-datastream-extension-enterValues.png)

>[!NOTE]
>
>Embora você não tenha configurado um CNAME no [!UICONTROL Domínio de borda] nesta lição, o Adobe recomenda usar um CNAME ao implementar o SDK da Web da plataforma em seu próprio site. Embora uma implementação CNAME não forneça benefícios em termos de duração do cookie, ela pode oferecer outros benefícios. Esses benefícios incluem bloqueadores de anúncios e navegadores menos comuns que impedem o envio de dados para domínios que eles classificam como rastreadores. Nesses casos, o uso de um CNAME pode impedir que a coleção de dados seja interrompida para usuários que utilizam essas ferramentas.

Para obter mais informações sobre cada seção da extensão, consulte [Configurar a extensão Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/web-sdk-extension-configuration.html)



[Próximo: ](create-data-elements.md)

>[!NOTE]
>
>Obrigado por investir seu tempo para aprender sobre o SDK da Web da Adobe Experience Platform. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
