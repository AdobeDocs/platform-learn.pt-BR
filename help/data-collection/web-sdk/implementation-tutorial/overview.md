---
title: Visão geral
description: Visão geral
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 8ffa258b-6ff7-4413-aead-21b106668c65
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---

# Visão geral

A coleta de dados sobre eventos que ocorrem no navegador de um usuário é um princípio fundamental de uma estratégia de marketing. O Adobe forneceu várias ferramentas para ajudar você a gerenciar esses dados. Embora você possa se familiarizar com cada uma dessas ferramentas individualmente, este tutorial tenta fornecer uma visão mais ampla do que cada uma dessas ferramentas faz e de como elas trabalham em conjunto para atingir um objetivo comum.

Neste tutorial, discutiremos uma estratégia para (1) estruturar e persistir seus dados no Adobe Experience Platform, (2) gerenciar seus dados no navegador e comunicar que determinados eventos ocorreram e (3) reagir a esses eventos enviando dados relevantes para o Adobe Experience Platform.

Embora este tutorial use a Camada de dados do cliente Adobe, o SDK da Web da Adobe Experience Platform e o recurso de tags para uma implementação mais prescritiva e contínua, você também pode misturar e combinar essas ferramentas com ferramentas de terceiros ou internas para obter o máximo de flexibilidade.

## Exemplo de cenário

Para este tutorial, pressupomos que você está implementando a coleta de dados para uma página de produto simples em um site de comércio eletrônico. A página do produto é carregada no navegador. Aqui, você rastreará se o usuário visualizou o produto. O usuário decide comprar o produto e, em seguida, clica em um botão para adicionar o produto ao carrinho. Aqui, você rastreará se o usuário abriu um novo carrinho e adicionou o produto ao carrinho enviando eventos de experiência ao Adobe Experience Platform. Por fim, o usuário clica em uma variável _Baixar o aplicativo_ vincule porque eles estão interessados no seu aplicativo móvel. Você rastreará se o usuário clicou no link.
