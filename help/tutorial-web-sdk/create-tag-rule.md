---
title: Criar uma regra de tag
description: Saiba como enviar um evento para a Platform Edge Network com seu objeto XDM usando uma regra de tag. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Tags
exl-id: e06bad06-3ee3-475f-9b10-f0825a48a312
source-git-commit: 9f75ef042342e1ff9db6039e722159ad96ce5e5b
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 3%

---

# Criar uma regra de tag


>[!CAUTION]
>
>Esperamos publicar alterações importantes neste tutorial na sexta-feira, 15 de março de 2024. Depois desse ponto, muitos exercícios serão alterados e talvez seja necessário reiniciar o tutorial desde o início para concluir todas as lições.

Saiba como enviar um evento para a Platform Edge Network com seu objeto XDM usando uma regra de tag. Uma regra de tag é uma combinação de eventos, condições e ações que instrui a propriedade de tag a fazer algo.

>[!NOTE]
>
> Para fins de demonstração, os exercícios desta lição baseiam-se no exemplo usado durante a [Criar elementos de dados](create-data-elements.md) etapa; enviar uma ação de evento XDM para capturar conteúdo e identidades dos usuários na [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html).


## Objetivos de aprendizagem

No final desta lição, você poderá:

* Usar uma convenção de nomenclatura para gerenciar regras nas tags
* Criar uma regra de tag para enviar um evento XDM
* Publicar uma regra de tag em uma biblioteca de desenvolvimento


## Pré-requisitos

Você está familiarizado com as tags de Coleção de dados e a [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html)e você deve ter concluído as seguintes lições anteriores no tutorial:

* [Configurar permissões](configure-permissions.md)
* [Configurar um esquema XDM](configure-schemas.md)
* [Configurar um namespace de identidade](configure-identities.md)
* [Configurar uma sequência de dados](configure-datastream.md)
* [Extensão SDK da Web instalada na propriedade da tag](install-web-sdk.md)
* [Criar elementos de dados](create-data-elements.md)

## Convenções de nomenclatura

Para gerenciar melhor as regras nas tags, é recomendável seguir uma convenção de nomenclatura padrão. Este tutorial usa uma convenção de nomenclatura de três partes:

* [localização] - [evento] - [ferramenta]

onde;

1. local é a página ou páginas no site em que a regra é acionada
1. evento é o acionador que aciona o sinal do
1. ferramenta é o aplicativo ou aplicativos específicos usados na etapa de ação dessa regra


## Criar regra de tag

Nas tags, as regras são usadas para executar ações (acionar chamadas) em várias condições. Você usará essa primeira regra para enviar o objeto XDM para a Rede de borda usando o SDK da Web [!UICONTROL Enviar evento] ação. Posteriormente neste tutorial, você enviará diferentes versões do objeto XDM com base no tipo de página na qual o visitante está. Por esse motivo, você usará as condições da regra para excluir esses outros tipos de páginas.

Para criar uma regra de tag:

1. Abra a propriedade da tag que você está usando neste tutorial
1. Ir para **[!UICONTROL Regras]** na navegação à esquerda
1. Selecione o **[!UICONTROL Criar nova regra]** botão
   ![Criar uma regra](assets/rules-create.png)
1. Atribua um nome à regra `all pages - library load - AA & AT`

   >[!NOTE]
   >
   > Essa regra é usada de uma maneira específica pelo Adobe Analytics e pelo Target em uma lição futura, por isso `AA & AT` é usado no final do nome.

1. No **[!UICONTROL Eventos]** , selecione **[!UICONTROL Adicionar]**
   ![Nomear a regra e adicionar um evento](assets/rule-name.png)
1. Use o **[!UICONTROL Extensão principal]** e selecione `Library Loaded (Page Top)` como o **[!UICONTROL Tipo de evento]**.

   Essa configuração significa que a regra é acionada sempre que a biblioteca de tags é carregada em uma página.
1. Selecionar **[!UICONTROL Manter alterações]** para retornar à tela principal da regra
   ![Adicionar o evento Biblioteca carregada](assets/rule-event-pagetop.png)
1. No **[!UICONTROL Condições]** , selecione a **[!UICONTROL Adicionar]** botão
   ![Adicionar condições](assets/rules-add-conditions.png)
1. Selecionar **[!UICONTROL Tipo de lógica]** `Exception`, **[!UICONTROL Extensão]** `Core`, e **[!UICONTROL Tipo de condição]** `Path Without Query String`
1. Insira o caminho do URL `/content/luma/us/en/user/cart.html` no **[!UICONTROL caminho igual a]** e **[!UICONTROL name]** it `Core - cart page`
1. Selecionar **[!UICONTROL Manter alterações]**
   ![Adicionar condições](assets/rule-condition-exception.png)
1. Adicione mais três exceções para os seguintes caminhos de URL

   * **`Core - checkout page`** for `/content/luma/us/en/user/checkout.html`
   * **`Core - thank you page`** for `/content/luma/us/en/user/checkout/order/thank-you.html`
   * **`Core - product page`** para `/products/` com o switch Regex ligado

   ![Adicionar condições](assets/rule-condition-exception-all.png)

1. No **[!UICONTROL Ações]** , selecione **[!UICONTROL Adicionar]**
1. Selecionar **[!UICONTROL Adobe Experience Platform Web SDK]** como o **[!UICONTROL Extensão]**
1. Selecionar **[!UICONTROL Enviar evento]** como o **[!UICONTROL Tipo de ação]**
1. Selecionar **[!UICONTROL web.webpagedetails.pageViews]** como o **[!UICONTROL Tipo]**.

   >[!WARNING]
   >
   > Essa lista suspensa preenche o **`xdm.eventType`** no objeto XDM. Embora também seja possível digitar rótulos de forma livre neste campo, é altamente recomendável **não** pois terá efeitos adversos com a Platform.

1. Como a variável **[!UICONTROL Dados XDM]**, selecione o `xdm.content` elemento de dados criado na lição anterior
1. Selecionar **[!UICONTROL Manter alterações]** para retornar à tela principal da regra

   ![Adicionar a ação Enviar evento](assets/rule-set-action-xdm.png)
1. Selecionar **[!UICONTROL Salvar]** para salvar a regra

   ![Salvar a regra](assets/rule-save.png)

## Publicar a regra em uma biblioteca

Em seguida, publique a regra no seu ambiente de desenvolvimento para que possamos verificar se ela funciona.

Para criar uma biblioteca:

1. Ir para **[!UICONTROL Fluxo de publicação]** na navegação à esquerda
1. Selecionar **[!UICONTROL Adicionar biblioteca]**

   ![Selecione Adicionar biblioteca](assets/rule-publish-library.png)
1. Para o **[!UICONTROL Nome]**, insira `Luma Web SDK Tutorial`
1. Para o **[!UICONTROL Ambiente]**, selecione `Development`
1. Selecionar  **[!UICONTROL Adicionar todos os recursos alterados]**

   >[!NOTE]
   >
   >    Além da extensão do SDK da Web da Adobe Experience Platform e da `all pages - library load - AA & AT` regra, você verá os componentes de tag criados nas lições anteriores. A extensão principal contém o JavaScript básico exigido por todas as propriedades de tag da Web.

1. Selecionar **[!UICONTROL Salvar e criar para desenvolvimento]**

   ![Criar a biblioteca](assets/rule-publish-add-all-changes.png)

A biblioteca pode levar alguns minutos para ser criada e, quando estiver concluída, exibirá um ponto verde à esquerda do nome da biblioteca:

![Compilação concluída](assets/rule-publish-success.png)

Como você pode ver no [!UICONTROL Fluxo de publicação] há muito mais no processo de publicação, que está além do escopo deste tutorial. Este tutorial usa apenas uma única biblioteca no ambiente de desenvolvimento do.

Agora você está pronto para validar os dados na solicitação usando o Adobe Experience Platform Debugger.

[Próxima ](validate-with-debugger.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
