---
title: Visão geral
description: Visão geral
exl-id: 527d8f73-33d0-45a6-b7a4-5e46cdb7c138
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 2%

---

# Usar a coleta de dados do Adobe Experience Platform

A coleta de dados sobre eventos que ocorrem no navegador de um usuário é um princípio fundamental de uma estratégia de marketing. O Adobe forneceu várias ferramentas para ajudar você a gerenciar esses dados. Embora você possa se familiarizar com cada uma dessas ferramentas individualmente, este tutorial tenta fornecer uma visão mais ampla do que cada uma delas faz e como elas trabalham em conjunto para atingir um objetivo comum.

Neste tutorial, discutimos uma estratégia para:

1. Estruturar e persistir seus dados no Adobe Experience Platform,
1. Gerenciar seus dados no navegador e comunicar que determinados eventos ocorreram, e
1. Reagir a tais eventos enviando dados relevantes para a Adobe Experience Platform.

Embora este tutorial use a Camada de dados do cliente do Adobe, o SDK da Web da Adobe Experience Platform e o [!DNL Tags] para uma implementação mais prescritiva e contínua, você também pode combinar essas ferramentas com ferramentas de terceiros ou internas para obter a flexibilidade máxima.

## Exemplo de cenário

Durante este tutorial, você implementa a coleta de dados para uma página de produto simples em um site de comércio eletrônico:

1. A página do produto é carregada no navegador. Aqui você rastreia que o usuário visualizou o produto.
1. O usuário decide comprar o produto, então clique em um botão para adicionar o produto ao carrinho. Aqui, você rastreia se o usuário abriu um novo carrinho e adicionou o produto ao carrinho enviando eventos de experiência para o Adobe Experience Platform.
1. Por fim, o usuário clica em um _Baixar o aplicativo_ link porque eles estão interessados no seu aplicativo móvel. Você rastreia que o usuário clicou no link.

Vamos começar!

[Próximo: ](structuring-your-data.md)

>[!NOTE]
>
>Obrigado por investir seu tempo para aprender sobre a coleta de dados. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
