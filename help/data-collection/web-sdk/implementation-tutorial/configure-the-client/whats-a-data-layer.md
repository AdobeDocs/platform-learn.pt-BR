---
title: O que é uma camada de dados?
description: O que é uma camada de dados?
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 747f2e60-646e-4324-993c-88568415ea59
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# O que é uma camada de dados?

Ao implementar tecnologias de marketing em seu site, é provável que você tenha dados importantes espalhados por toda a interface do usuário. Por exemplo, o nome de um produto pode estar em um cabeçalho na página e o preço pode ser menor na página abaixo da imagem do produto. Se você quiser enviar esses dados para o Adobe ou algum outro fornecedor, certamente poderá encontrar os elementos de HTML que contêm os dados procurando tags ou atributos de HTML específicos, extrair os dados desses elementos e enviá-los. Mas o que acontece quando sua equipe de engenharia decide mover o nome do produto do cabeçalho para uma barra lateral? Sua implementação falha. Sua implementação não pode mais encontrar o cabeçalho ou, pior, ele encontra o cabeçalho e envia dados irrelevantes para o servidor.

Um dos principais objetivos de uma camada de dados é resolver esse problema. Na mais simples, uma camada de dados é um objeto JavaScript (ou, como veremos mais tarde, uma matriz) que contém dados sobre o produto na página ou quaisquer outros dados relevantes nos quais suas tecnologias de marketing dependam para atingir suas metas. Ao não depender dos elementos da interface do usuário para fornecer esses dados, nossa implementação se torna mais robusta. A camada de dados contém os dados e deve ser considerada um contrato. Normalmente, esse contrato é entre a equipe de engenharia, que está inserindo dados na camada de dados, e a equipe de marketing, que está recuperando dados da camada de dados.

Se um engenheiro estiver prestes a alterar a estrutura da camada de dados, ele considerará muito mais a possibilidade de trabalhar com a equipe de marketing para que as alterações apropriadas possam ser feitas na implementação de marketing. A presente comunicação e cooperação _deve_ seja estabelecida em sua organização para garantir uma implementação robusta.

## Contêiner vs. conteúdo

No setor, o termo &quot;camada de dados&quot; é usado de forma um pouco vaga e geralmente pode levar a confusão e má comunicação. Considere uma caixa de bolinhas. Há duas partes: o container (a caixa) e o conteúdo (as bolinhas de vidro). Da mesma forma, uma camada de dados geralmente é considerada como tendo duas partes: o contêiner (o objeto ou matriz do JavaScript) e o conteúdo (os dados como `priceTotal`, `currencyCode`, e `purchaseOrderNumber` ).

Como este tutorial se refere à Camada de dados do cliente Adobe, ele se refere ao contêiner e não ao conteúdo. Quando se refere ao XDM, se refere ao conteúdo e não ao contêiner. No caso da Camada de dados de clientes Adobe, não importa se o conteúdo é XDM ou seu próprio modelo de dados. A Camada de dados de clientes Adobe não se importa. É só uma caixa. Mas, ele _é_ uma caixa com poderes especiais...

## Comunicando alterações

Ao usar uma camada de dados, você pode alterar o conteúdo a qualquer momento. Esse é um recurso bom, pois os dados podem se tornar disponíveis em momentos diferentes. Por exemplo, você pode ter alguns dados sobre o usuário disponíveis imediatamente, mas pode precisar fazer uma solicitação assíncrona a terceiros para obter informações adicionais. Isso requer uma consideração especial. Se você precisar enviar esses dados assíncronos para o Adobe Experience Platform em algum momento, como suas tecnologias de marketing sabem quando determinados dados foram adicionados à camada de dados e estão prontos para serem enviados? Você precisa de uma camada de dados mais inteligente: uma camada de dados orientada por eventos.

Uma camada de dados orientada por eventos é capaz de comunicar que seu conteúdo mudou para que as tecnologias de marketing possam reagir à mudança. Usado corretamente, isso pode ajudar a evitar problemas de tempo que geralmente surgem com camadas de dados que não têm meios de se comunicar quando ocorrem alterações.

A Camada de dados de clientes Adobe é uma camada de dados orientada por eventos.
