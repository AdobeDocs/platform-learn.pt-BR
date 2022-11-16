---
title: Criar regras para rastrear eventos de exibição de página e comércio
description: Criar regras para rastrear eventos de exibição de página e comércio
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 2dd02462-ddb5-4f67-8b0f-4a5bf5f7d655
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---

# Criar regras para rastrear eventos de exibição de página e comércio

Para rastrear se o usuário visualizou a página do produto, crie uma regra dentro das tags do Adobe Experience Platform. Faça isso clicando em [!UICONTROL Regras] no menu à esquerda, em seguida, clique em [!UICONTROL Adicionar regra].

Para o nome da regra, insira _Página visualizada_.

## Adicionar um evento

Clique no botão [!UICONTROL Adicionar] botão abaixo [!UICONTROL Eventos]. Agora você mostra estar na exibição de evento. Para o [!UICONTROL Extensão] , selecione [!UICONTROL Camada de dados do cliente Adobe]. Para o [!UICONTROL Tipo de evento] , selecione [!UICONTROL Dados enviados].

Porque você deseja que essa regra seja acionada somente quando a variável `pageViewed` for enviado para a camada de dados, selecione [!UICONTROL Evento específico] under [!UICONTROL Ouça] e tipo _pageViewed_ na [!UICONTROL Evento / Chave para se registrar] campo de texto.

![Evento de exibição de página](../../../assets/implementation-strategy/page-viewed-event.png)

Clique em [!UICONTROL  Manter alterações].

## Adicionar uma ação

Agora que você está de volta à exibição de regra, clique no botão [!UICONTROL Adicionar] botão abaixo [!UICONTROL Ações]. Agora você deve estar na exibição de ação. Para o [!UICONTROL Extensão] , selecione [!UICONTROL Adobe Experience Platform Web SDK]. Para o [!UICONTROL Tipo de ação] , selecione [!UICONTROL Enviar evento]. Essa ação permite enviar um evento de experiência para a Rede de borda da Adobe Experience Platform.

No lado direito da tela, encontre a variável [!UICONTROL Tipo] e selecione `web.webpagedetails.pageViews`. Este é um dos tipos canônicos de evento de experiência que o Adobe Experience Platform fornece prontos para uso. Representa uma exibição de página.

Para o [!UICONTROL Dados XDM] , insira `%event.fullState%`. Isso indica que o estado calculado (também conhecido como estado completo) da camada de dados, que é capturada no momento em que a regra foi acionada, deve ser enviado como parte do evento de experiência.

![Ação exibida na página](../../../assets/implementation-strategy/page-viewed-action.png)

Se os dados enviados para a camada de dados do site não estiverem em conformidade com o esquema XDM ou se você quiser enviar apenas uma parte do estado calculado da camada de dados, use a [!UICONTROL Objeto XDM] tipo de elemento de dados (fornecido pela extensão Adobe Experience Platform Web SDK) para criar um objeto apropriado que corresponda ao esquema.

Clique no botão [!UICONTROL Manter alterações.]

## Salve a regra

Sua regra deve estar concluída.

![Regra exibida na página](../../../assets/implementation-strategy/page-viewed-rule.png)

Salve a regra clicando em [!UICONTROL Salvar].

## Repetir o processo

Repita o processo descrito acima para criar regras para quando um produto é visualizado, um carrinho de compras é aberto e um produto é adicionado ao carrinho. As únicas diferenças entre as regras serão o nome da regra, o valor inserido na variável [!UICONTROL Evento / Chave para se registrar] no campo [!UICONTROL Dados enviados] e o [!UICONTROL Tipo] no campo [!UICONTROL Enviar evento] ação. Estes são os valores para cada regra:

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

Em seguida, manteremos cliques de rastreamento no [!UICONTROL Baixar o aplicativo] link .
