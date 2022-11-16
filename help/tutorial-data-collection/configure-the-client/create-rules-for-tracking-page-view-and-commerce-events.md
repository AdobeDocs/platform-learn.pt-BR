---
title: Criar regras para rastrear eventos de exibição de página e comércio
description: Criar regras para rastrear eventos de exibição de página e comércio
exl-id: 00bf3374-9319-47ce-a75a-2b94f793c938
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 4%

---

# Criar regras para rastrear eventos de exibição de página e comércio

Para rastrear se o usuário visualizou a página do produto, crie uma regra no Adobe Experience Platform [!DNL Tags].

1. Clique em **[!UICONTROL Regras]** na navegação do lado esquerdo, em seguida, clique em **[!UICONTROL Criar nova regra]**.

1. Para o nome da regra, insira **_Página visualizada_**.

## Adicionar um evento

1. Clique no botão **[!UICONTROL Adicionar]** botão abaixo [!UICONTROL Eventos]. Agora você mostra estar na exibição de evento. Para o [!UICONTROL Extensão] , selecione **[!UICONTROL Camada de dados do cliente Adobe]**. Para o [!UICONTROL Tipo de evento] , selecione **[!UICONTROL Dados enviados]**.
1. Porque você deseja que essa regra seja acionada somente quando a variável `pageViewed` for enviado para a camada de dados, selecione **[!UICONTROL Evento específico]** under [!UICONTROL Ouça] e tipo **_pageViewed_** na [!UICONTROL Evento / Chave para se registrar] campo de texto.
1. Clique em **[!UICONTROL Manter alterações]**.
   ![Evento de exibição de página](../assets/page-viewed-event.png)

## Adicionar uma ação

Agora que você está de volta à exibição de regra:

1. Clique no botão **[!UICONTROL Adicionar]** em [!UICONTROL Ações]. Agora você deve estar na exibição de ação. Para o [!UICONTROL Extensão] , selecione **[!UICONTROL Adobe Experience Platform Web SDK]**. Para o [!UICONTROL Tipo de ação] , selecione **[!UICONTROL Enviar evento]**. Essa ação permite enviar um evento de experiência para a Rede de borda da Adobe Experience Platform.
1. No meio da tela, encontre a variável [!UICONTROL Tipo] e selecione **`web.webpagedetails.pageViews`**. Este é um dos tipos canônicos de evento de experiência que o Adobe Experience Platform fornece prontos para uso. Representa uma exibição de página.
1. Para o [!UICONTROL Dados XDM] , insira **`%event.fullState%`**. Isso indica que o estado calculado (também conhecido como estado completo) da camada de dados, que é capturada no momento em que a regra foi acionada. Isso deve ser enviado como parte do evento de experiência.
1. Clique no botão **[!UICONTROL Manter alterações.]**
   ![Ação exibida na página](../assets/page-viewed-action.png)

Se os dados enviados para a camada de dados do site não estiverem em conformidade com o esquema XDM ou se você quiser enviar apenas uma parte do estado calculado da camada de dados, use a [!UICONTROL Objeto XDM] tipo de elemento de dados (fornecido pela extensão Adobe Experience Platform Web SDK) para criar um objeto apropriado que corresponda ao esquema.

## Salve a regra

1. Salve a regra clicando em **[!UICONTROL Salvar]**.
   ![Regra exibida na página](../assets/page-viewed-rule.png)

## Repetir o processo

Repita o processo descrito acima para criar regras para quando um produto é visualizado, um carrinho de compras é aberto e um produto é adicionado ao carrinho. As únicas diferenças entre as regras são o nome da regra, o valor inserido na variável [!UICONTROL Evento / Chave para se registrar] no campo [!UICONTROL Dados enviados] e o [!UICONTROL Tipo] no campo [!UICONTROL Enviar evento] ação. Estes são os valores para cada regra:

Regra visualizada pelo produto:

* **Nome da regra**: _Produto visualizado_
* **Evento / Chave para se registrar** within [!UICONTROL Dados enviados] evento: `productViewed`
* **Tipo** within [!UICONTROL Enviar evento] ação: `commerce.productViews`

Regra de abertura do carrinho:

* **Nome da regra**: _Carrinho aberto_
* **Evento / Chave para se registrar** within [!UICONTROL Dados enviados] evento: `cartOpened`
* **Tipo** within [!UICONTROL Enviar evento] ação: `commerce.productListOpens`

Produto adicionado à regra do carrinho:

* **Nome da regra**: _Produto Adicionado Ao Carrinho_
* **Evento / Chave para se registrar** within [!UICONTROL Dados enviados] evento: `productAddedToCart`
* **Tipo** within [!UICONTROL Enviar evento] ação: `commerce.productListAdds`

Em seguida, manipulamos cliques de rastreamento no [!UICONTROL Baixar o aplicativo] link .

[Próximo: ](create-a-data-element-and-rule-for-tracking-app-downloads.md)

>[!NOTE]
>
>Obrigado por investir seu tempo para aprender sobre a coleta de dados. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
