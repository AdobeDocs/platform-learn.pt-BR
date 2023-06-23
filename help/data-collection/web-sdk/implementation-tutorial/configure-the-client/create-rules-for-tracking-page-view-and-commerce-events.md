---
title: Criar regras para rastrear eventos de exibição de página e de comércio
description: Criar regras para rastrear eventos de exibição de página e de comércio
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 2dd02462-ddb5-4f67-8b0f-4a5bf5f7d655
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---

# Criar regras para rastrear eventos de exibição de página e de comércio

Para rastrear se o usuário visualizou a página do produto, crie uma regra nas tags da Adobe Experience Platform. Faça isso clicando em [!UICONTROL Regras] no menu à esquerda, clique em [!UICONTROL Adicionar regra].

Para o nome da regra, informe _Página visualizada_.

## Adicionar um evento

Clique em [!UICONTROL Adicionar] botão em [!UICONTROL Eventos]. Agora, você deve estar na exibição de evento. Para o [!UICONTROL Extensão] selecione [!UICONTROL Camada de dados de clientes Adobe]. Para o [!UICONTROL Tipo de evento] selecione [!UICONTROL Dados enviados].

Porque você deseja que essa regra seja acionada somente quando a variável `pageViewed` for enviado para a camada de dados, selecione [!UICONTROL Evento Específico] em [!UICONTROL Ouvir] e tipo _pageViewed_ no [!UICONTROL Evento / Chave para se inscrever] campo de texto.

![Evento exibido na página](../../../assets/implementation-strategy/page-viewed-event.png)

Clique em [!UICONTROL  Manter alterações].

## Adicionar uma ação

Agora que você voltou à exibição de regra, clique no link [!UICONTROL Adicionar] botão em [!UICONTROL Ações]. Agora você deve estar na exibição de ação. Para o [!UICONTROL Extensão] selecione [!UICONTROL Adobe Experience Platform Web SDK]. Para o [!UICONTROL Tipo de ação] selecione [!UICONTROL Enviar evento]. Essa ação permite enviar um evento de experiência para a Adobe Experience Platform Edge Network.

No lado direito da tela, localize a variável [!UICONTROL Tipo] e selecione `web.webpagedetails.pageViews`. Esse é um dos tipos de evento de experiência canônico que a Adobe Experience Platform fornece prontos para uso. Ele representa uma exibição de página.

Para o [!UICONTROL Dados XDM] insira `%event.fullState%`. Isso indica que o estado calculado (também conhecido como estado completo) da camada de dados, que é capturado no momento em que a regra foi acionada, deve ser enviado como parte do evento de experiência.

![Ação exibida na página](../../../assets/implementation-strategy/page-viewed-action.png)

Se os dados enviados para a camada de dados do seu site não estiverem em conformidade com o esquema XDM ou se você quiser enviar apenas uma parte do estado calculado da camada de dados, use o [!UICONTROL Objeto XDM] tipo de elemento de dados (fornecido pela extensão SDK da Web da Adobe Experience Platform) para criar um objeto apropriado que corresponda ao esquema.

Clique no botão [!UICONTROL Manter alterações.]

## Salve a regra

Sua regra agora deve estar concluída.

![Regra de exibição de página](../../../assets/implementation-strategy/page-viewed-rule.png)

Salve a regra clicando em [!UICONTROL Salvar].

## Repetir o processo

Repita o processo descrito acima para criar regras para quando um produto for visualizado, um carrinho de compras for aberto e um produto for adicionado ao carrinho. As únicas diferenças entre as regras serão o nome da regra, o valor inserido no [!UICONTROL Evento / Chave para se inscrever] no campo [!UICONTROL Dados enviados] e o [!UICONTROL Tipo] no campo [!UICONTROL Enviar evento] ação. Estes são os valores de cada regra:

Regra exibida pelo produto:

* **Nome da regra**: _Produto visualizado_
* **Evento / Chave para se inscrever** no prazo de [!UICONTROL Dados enviados] evento: `productViewed`
* **Tipo** no prazo de [!UICONTROL Enviar evento] ação: `commerce.productViews`

Regra de abertura do carrinho:

* **Nome da regra**: _Carrinho aberto_
* **Evento / Chave para se inscrever** no prazo de [!UICONTROL Dados enviados] evento: `cartOpened`
* **Tipo** no prazo de [!UICONTROL Enviar evento] ação: `commerce.productListOpens`

Produto adicionado à regra do carrinho:

* **Nome da regra**: _Produto adicionado ao carrinho_
* **Evento / Chave para se inscrever** no prazo de [!UICONTROL Dados enviados] evento: `productAddedToCart`
* **Tipo** no prazo de [!UICONTROL Enviar evento] ação: `commerce.productListAdds`

Em seguida, lidaremos com o rastreamento de cliques no [!UICONTROL Baixar o aplicativo] link.
