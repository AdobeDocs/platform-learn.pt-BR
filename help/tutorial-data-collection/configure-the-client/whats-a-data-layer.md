---
title: O que é uma camada de dados?
description: O que é uma camada de dados?
exl-id: a53572c1-1295-4ed4-8a3d-aafff3235138
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# O que é uma camada de dados?

Ao implementar tecnologias de marketing em seu site, é provável que você tenha partes importantes de dados espalhadas por toda a interface do usuário. Por exemplo, o nome de um produto pode estar em um cabeçalho na página e o preço pode ser menor na página abaixo da imagem do produto. Se desejar enviar esses dados para o Adobe ou outro fornecedor, encontre os elementos de HTML que contêm os dados necessários, extraia os dados desses elementos e envie-os. Mas o que acontece quando a equipe de engenharia decide mover o nome do produto do cabeçalho para uma barra lateral? Sua implementação é interrompida. Sua implementação não pode mais encontrar o cabeçalho ou, pior, encontra o cabeçalho e envia dados irrelevantes para o servidor.

Um dos principais objetivos de uma camada de dados é resolver esse problema. Em seu modo mais simples, uma camada de dados é um objeto JavaScript ou uma matriz que contém dados sobre o produto na página. Ele inclui todos os dados relevantes que suas tecnologias de marketing exigem para atingir suas metas. Ao não depender dos elementos da interface do usuário para fornecer esses dados, nossa implementação se torna mais robusta. A camada de dados armazena os dados e deve ser considerada um contrato. Normalmente, esse contrato é celebrado entre a equipe de engenharia, que está inserindo dados na camada de dados, e a equipe de marketing, que está recuperando dados da camada de dados.

Se um engenheiro estiver prestes a alterar a estrutura da camada de dados, é muito mais provável que ele considere trabalhar com a equipe de marketing para que alterações apropriadas possam ser feitas na implementação de marketing. Esta comunicação e cooperação _must_ ser estabelecidas em sua organização para garantir uma implementação robusta.

## Contêiner vs. conteúdo

No setor, o termo &quot;camada de dados&quot; é lançado em torno de um pouco vagamente e pode, muitas vezes, levar a confusão e má comunicação. Considere uma caixa de mármores. Há duas partes: o recipiente (a caixa) e o conteúdo (os mármores). Da mesma forma, uma camada de dados geralmente é considerada como tendo duas partes: o contêiner (o objeto ou matriz JavaScript) e o conteúdo (os dados como `priceTotal`, `currencyCode`e `purchaseOrderNumber` ).

Como este tutorial se refere à Camada de dados do cliente do Adobe, ele se refere ao contêiner e não ao conteúdo. Quando se refere ao XDM, refere-se ao conteúdo e não ao container. Ao usar a Camada de dados do cliente do Adobe, não importa se o conteúdo é XDM ou seu próprio modelo de dados. A Camada de dados do cliente do Adobe não se importa. É só uma caixa. Mas, _é_ uma caixa com poderes especiais..

## Comunicação de alterações

Ao usar uma camada de dados, é possível alterar o conteúdo a qualquer momento. Esse é um bom recurso, porque os dados podem se tornar disponíveis em momentos diferentes. Por exemplo, você pode ter alguns dados sobre o usuário disponíveis imediatamente, mas pode precisar fazer uma solicitação assíncrona a terceiros para obter informações adicionais. Isto requer uma atenção especial. Se você precisar enviar esses dados assíncronos para a Adobe Experience Platform em algum momento, como suas tecnologias de marketing sabem quando determinados dados foram adicionados à camada de dados e estão prontos para serem enviados? Você precisa de uma camada de dados mais inteligente — uma camada de dados orientada por eventos.

Uma camada de dados orientada por eventos pode comunicar que seu conteúdo mudou para que as tecnologias de marketing possam reagir à mudança. Usado adequadamente, isso pode ajudar a evitar problemas de tempo que geralmente surgem com camadas de dados que não têm como se comunicar quando ocorrem alterações.

A Camada de dados do cliente do Adobe é uma camada de dados orientada por eventos.

[Próximo: ](how-to-use-the-adobe-client-data-layer.md)

>[!NOTE]
>
>Obrigado por investir seu tempo para aprender sobre a coleta de dados. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
