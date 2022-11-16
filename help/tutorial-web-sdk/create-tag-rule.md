---
title: Criar uma regra de tag
description: Saiba como enviar um evento para a Rede de borda da plataforma com seu objeto XDM usando uma regra de tag. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Tags
exl-id: e06bad06-3ee3-475f-9b10-f0825a48a312
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 5%

---

# Criar uma regra de tag

Saiba como enviar um evento para a Rede de borda da plataforma com seu objeto XDM usando uma regra de tag. Uma regra de tag é uma combinação de eventos, condições e ações que instrui a propriedade de tag a fazer algo.

>[!NOTE]
>
> Para fins de demonstração, os exercícios desta lição baseiam-se no exemplo usado durante a [Criar elementos de dados](create-data-elements.md) degrau; envio de uma ação de evento XDM para capturar conteúdo e identidades de usuários no [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html).


## Objetivos de aprendizagem

No final desta lição, você poderá:

* Usar uma convenção de nomenclatura para gerenciar regras nas tags
* Criar uma regra de tag para enviar um evento XDM
* Publicar uma regra de tag em uma biblioteca de desenvolvimento


## Pré-requisitos

Você está familiarizado com as tags de Coleta de dados e a variável [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html)e você deve ter concluído as seguintes lições anteriores no tutorial:

* [Configurar permissões](configure-permissions.md)
* [Configurar um esquema XDM](configure-schemas.md)
* [Configurar um namespace de identidade](configure-identities.md)
* [Configurar um conjunto de dados](configure-datastream.md)
* [Extensão do SDK da Web instalada na propriedade da tag](install-web-sdk.md)
* [Criar elementos de dados](create-data-elements.md)

## Convenções de nomenclatura

Para gerenciar melhor as regras em tags, é recomendável seguir uma convenção de nomenclatura padrão. Este tutorial usa uma convenção de nomenclatura de três partes:

* [localização] - [evento] - [ferramenta]

em que;

1. local é a página ou páginas no site em que a regra é acionada
1. evento é o acionador que aciona o beacon
1. ferramenta é o aplicativo específico ou os aplicativos usados na etapa de ação para essa regra


## Criar regra de tag

Para criar uma regra de tag:

1. Abra a propriedade de tag usada neste tutorial
1. Ir para **[!UICONTROL Regras]** na navegação à esquerda
1. Selecione o **[!UICONTROL Criar nova regra]** botão
   ![Criar uma regra](assets/rules-create.png)
1. Atribua um nome à regra `all pages - library load - AA & AT`

   >[!NOTE]
   >
   > Essa regra é usada de uma maneira específica pelo Adobe Analytics e Target em uma lição futura, por isso `AA & AT` é usada no final do nome.

1. No **[!UICONTROL Eventos]** seção , selecione **[!UICONTROL Adicionar]**

   ![Nomear a regra e adicionar um evento](assets/rule-name.png)
1. Use o **[!UICONTROL Extensão principal]** e selecione `Library Loaded (Page Top)` como **[!UICONTROL Tipo de evento]**.

   Essa configuração significa que a regra é acionada sempre que a biblioteca de tags é carregada em uma página.
1. Selecionar **[!UICONTROL Manter alterações]** para retornar à tela de regra principal
   ![Adicionar o evento Biblioteca carregada](assets/rule-event-pagetop.png)
1. No **[!UICONTROL Condições]** selecione a **[!UICONTROL Adicionar]** botão
   ![Adicionar condições](assets/rules-add-conditions.png)
1. Selecionar **[!UICONTROL Tipo lógico]** `Exception`, **[!UICONTROL Extensão]** `Core`e **[!UICONTROL Tipo de condição]** `Path Without Query String`
1. Insira o caminho do URL `/content/luma/us/en/user/cart.html` no **[!UICONTROL caminho igual]** e **[!UICONTROL name]** it `Core - cart page`
1. Selecione **[!UICONTROL Manter alterações]**

   ![Adicionar condições](assets/rule-condition-exception.png)
1. Adicione mais três exceções para os seguintes caminhos de URL

   * **`Core - checkout page`** for `/content/luma/us/en/user/checkout.html`
   * **`Core - thank you page`** para `/content/luma/us/en/user/checkout/order/thank-you.html`
   * **`Core - product page`** para `/products/` com o interruptor Regex ligado

   ![Adicionar condições](assets/rule-condition-exception-all.png)

1. No **[!UICONTROL Ações]** seção , selecione **[!UICONTROL Adicionar]**
1. Selecionar **[!UICONTROL Adobe Experience Platform Web SDK]** como **[!UICONTROL Extensão]**
1. Selecionar **[!UICONTROL Enviar evento]** como **[!UICONTROL Tipo de ação]**
1. Selecionar **[!UICONTROL web.webpagedetails.pageViews]** como **[!UICONTROL Tipo]**.

   >[!WARNING]
   >
   > Essa lista suspensa preenche a variável **`xdm.eventType`** no objeto XDM. Embora você também possa digitar rótulos de forma livre neste campo, é altamente recomendável **não** já que terá efeitos adversos com a Platform.

1. Como **[!UICONTROL Dados XDM]**, selecione o `xdm.content` elemento de dados criado na lição anterior
1. Selecionar **[!UICONTROL Manter alterações]** para retornar à tela de regra principal

   ![Adicionar a ação Enviar evento](assets/rule-set-action-xdm.png)
1. Selecionar **[!UICONTROL Salvar]** para salvar a regra

   ![Salvar a regra](assets/rule-save.png)

## Publicar a regra em uma biblioteca

Em seguida, publique a regra no seu ambiente de desenvolvimento para que possamos verificar se funciona.

Para criar uma biblioteca:

1. Ir para **[!UICONTROL Fluxo de publicação]** na navegação à esquerda
1. Selecionar **[!UICONTROL Adicionar biblioteca]**

   ![Selecione Adicionar biblioteca](assets/rule-publish-library.png)
1. Para o **[!UICONTROL Nome]**, insira `Luma Web SDK Tutorial`
1. Para o **[!UICONTROL Ambiente]**, selecione `Development`
1. Selecionar  **[!UICONTROL Adicionar todos os recursos alterados]**

   >[!NOTE]
   >
   >    Além da extensão do SDK da Web da Adobe Experience Platform e do `all pages - library load - AA & AT` , você verá os componentes da tag criados nas lições anteriores. A extensão principal contém o JavaScript básico necessário para todas as propriedades da tag da Web.

1. Selecionar **[!UICONTROL Salvar e criar para desenvolvimento]**

   ![Criar e criar a biblioteca](assets/rule-publish-add-all-changes.png)

A biblioteca pode levar alguns minutos para ser criada e, quando estiver concluída, exibe um ponto verde à esquerda do nome da biblioteca:

![Build concluída](assets/rule-publish-success.png)

Como você pode ver no [!UICONTROL Fluxo de publicação] , há muito mais no processo de publicação, o que está além do escopo deste tutorial. Este tutorial só usa uma única biblioteca no ambiente de desenvolvimento do .

Agora você está pronto para validar os dados na solicitação usando o Adobe Experience Platform Debugger.

[Próximo ](validate-with-debugger.md)

>[!NOTE]
>
>Obrigado por investir seu tempo para aprender sobre o SDK da Web da Adobe Experience Platform. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
