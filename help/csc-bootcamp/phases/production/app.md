---
title: Bootcamp do CSC - Criar conteúdo de aplicativo móvel
description: Bootcamp do CSC - Criar conteúdo de aplicativo móvel
doc-type: multipage-overview
exl-id: db4e91da-2077-4133-aca9-e3413990f4be
source-git-commit: 143da6340b932563a3309bb46c1c7091e0ab2ee2
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 0%

---

# Criar conteúdo de aplicativo móvel

## O que é a entrega de conteúdo headless?

Com um sistema de gerenciamento de conteúdo headless, o back-end e o front-end agora são dissociados. A parte headless representa o back-end de conteúdo, já que um CMS headless é um sistema exclusivamente back-end de gerenciamento de conteúdo, projetado e criado explicitamente como um repositório de conteúdo que torna o conteúdo acessível por meio de uma API, para exibição em qualquer dispositivo.

O front-end, que é desenvolvido e mantido de maneira independente, busca conteúdo do back-end headless usando uma API de entrega de conteúdo, normalmente no formato JSON. Por exemplo, pode ser como um aplicativo web ou, no nosso caso, como um aplicativo móvel.

Um CMS headless de back-end geralmente requer que o conteúdo seja estruturado, com base em um modelo ou esquema. Isso facilita os aplicativos clientes que solicitam o conteúdo correto para renderizar uma experiência. Alguns CMS, como o AEM, podem expor conteúdo estruturado e não estruturado no formato JSON.

Uma característica importante dessa topologia é que o conteúdo veiculado pelo CMS headless no formato JSON é um conteúdo puro, sem informações de design ou layout. Em uma implementação de CMS headless, toda a formatação e layout são mantidos pelo aplicativo de front-end dissociado.

Um benefício importante de uma topologia de CMS headless é a capacidade de reutilizar conteúdo em vários canais, que podem usar diferentes implementações de front-end do lado do cliente. Isso pode tornar o processo de desenvolvimento de front-end mais eficiente. Mas também significa que o processo de desenvolvimento da experiência de front-end pode se tornar muito centrado em código e TI, com essa última tornando-se responsável pela experiência.

## Como a entrega de conteúdo headless funciona no AEM?

O AEM as a Cloud Service é uma ferramenta flexível para o modelo de implementação headless, oferecendo três recursos avançados:

![Entrega de conteúdo headless](./images/prod-app-headless.png)

1. Modelos de conteúdo
   - Os modelos de conteúdo são uma representação estruturada do conteúdo.
   - Os modelos de conteúdo são definidos pelos arquitetos de informações no editor de modelos de fragmento de conteúdo do AEM.
   - Os modelos de conteúdo servem como base para os fragmentos de conteúdo.
1. Fragmentos de conteúdo
   - Os fragmentos de conteúdo são criados com base em um Modelo de conteúdo.
   - Criado por autores de conteúdo usando o editor de fragmento de conteúdo AEM.
   - Os fragmentos de conteúdo são armazenados no AEM Assets e gerenciados na interface do administrador do Assets.
1. API de conteúdo para entrega
   - A API do GraphQL do AEM é compatível com a entrega de fragmentos de conteúdo.
   - A API REST do AEM Assets é compatível com operações CRUD de fragmentos de conteúdo.
   - A entrega direta de conteúdo também é possível com a [exportação em JSON do Componente principal do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=en).

## Exercício

Para essa campanha de bootcamp, vamos nos concentrar na parte do &quot;conteúdo&quot; - afinal, é a cadeia de fornecimento de conteúdo que estamos buscando. Já prevemos um modelo de conteúdo, bem como as APIs de entrega necessárias, para que você possa se concentrar no que é importante.

Primeiro, vamos explorar nosso modelo de conteúdo: é o &quot;contrato&quot; que temos com o CMS headless, para que saibamos qual conteúdo pode vir pela nossa frente e em que formato.

- Vá para o autor do AEM em [https://author-p105462-e991028.adobeaemcloud.com/](https://author-p105462-e991028.adobeaemcloud.com/) e faça logon com as credenciais fornecidas.

- No menu Iniciar do AEM, selecione Ferramentas > Geral > Modelos de fragmento de conteúdo

![menu de modelos de fragmento de conteúdo](./images/prod-app-cfm.png)

- Na próxima tela, você terá uma visão geral de todos os sites que estão usando conteúdo headless. Isso permite que você mantenha a governança sobre vários sites headless, sem ter medo de que eles interfiram um com o outro. No nosso caso, estamos trabalhando com o site da Adobe, então, selecione esse modelo.

![sites headless diferentes](./images/prod-app-cfm-folder.png)

- Nesta pasta, podemos ver algum conteúdo técnico headless que estamos usando no site da Adobe. Interessado em saber mais? Fique à vontade para entrar em contato. Por enquanto, vamos nos concentrar na tarefa antes das mãos: o aplicativo móvel. Passe o mouse sobre o cartão Página inicial do aplicativo móvel e clique no ícone de lápis para abrir o modelo de conteúdo.

![modelo de conteúdo da página inicial do aplicativo móvel](./images/prod-app-created-cfm.png)

- No Editor de modelos de fragmentos de conteúdo, é possível ver os detalhes de um determinado modelo de conteúdo. Em nosso caso, podemos ver a página inicial do nosso aplicativo móvel existe do logotipo da Adobe, um cabeçalho, algum texto livre opcional e um produto em destaque opcional. Todos esses itens são fáceis de configurar e atualizar, de modo que, se o modelo de conteúdo precisar de elementos extras, isso possa ser feito sem interferência do desenvolvedor no CMS.

![modelo de conteúdo de detalhes](./images/prod-app-cfm-details.png)

>[!WARNING]
>
> **Observe que alterar o modelo de conteúdo tem implicações ainda maiores**, pois o aplicativo móvel depende do recebimento de determinadas informações para poder exibir os elementos corretos. Tenha muito cuidado ao atualizar ou remover campos, a adição de campos não deve ter impacto.

Agora que temos uma ideia do que o conteúdo deve existir, podemos criar o fragmento de conteúdo.

- Clique no logotipo do AEM no canto superior esquerdo para abrir a navegação e navegue até Navegação \> Fragmentos de conteúdo.

![opção de menu de fragmentos de conteúdo](./images/prod-cf-ui.png)

- Na interface a seguir, você obtém uma visão geral de todo o conteúdo existente no AEM. Os filtros à esquerda podem ser usados para restringir se você estiver pesquisando por um fragmento de conteúdo específico. Para criar um novo fragmento de conteúdo, vamos clicar no botão &quot;Criar&quot; na parte superior direita.

![botão criar fragmento de conteúdo](./images/prod-app-create-cf.png)

- No modal aberto, você verá que alguns campos ainda não são editáveis. É lógico: com base em onde criamos nosso fragmento, modelos diferentes estarão disponíveis.
  ![criar fragmento de conteúdo](./images/prod-app-create-cf-details.png)
   - Primeiro, selecione onde criaremos nosso fragmento clicando no ícone de pasta ao lado do campo &quot;Local&quot;. Expanda a árvore de conteúdo clicando nas pastas &quot;adobike&quot; \> &quot;en&quot; \> &quot;mobile-app&quot; e, em seguida, confirme a seleção clicando no botão &quot;Escolher&quot;.
     ![selecione o local correto](./images/prod-app-folder.png)
   - Você observará que o campo &quot;Modelo de fragmento de conteúdo&quot; agora é editável. Clique na seta ao lado do campo para abrir a lista suspensa e selecionar o modelo de conteúdo que visualizamos anteriormente: &quot;Página inicial do aplicativo móvel&quot;.
   - Em seguida, dê ao fragmento de conteúdo um título significativo (dica: inclua o número da equipe para encontrar o conteúdo facilmente). Observe que o campo &quot;Nome&quot; é preenchido automaticamente para facilitar a vida: é o nome que o sistema usa para identificar o fragmento e não deve ser tocado.
   - Por fim, clique no botão &quot;Criar e abrir&quot;, que, como o nome indica, criará o fragmento de conteúdo e o abrirá para que você possa editá-lo imediatamente.

- Aqui, sua equipe pode decidir qual conteúdo você deseja mostrar no aplicativo móvel. ![detalhes do fragmento de conteúdo](./images/prod-cf-details.png)
   - Certifique-se de selecionar o nº da equipe para que você possa verificar o conteúdo posteriormente no aplicativo móvel.
   - Para selecionar ativos de imagem, clique no ícone de pasta para procurar a imagem correta no AEM Assets.
   - Para o produto em destaque, clique no ícone de pesquisa do produto para selecionar facilmente nosso produto Commerce &quot;Adobe 1&quot;, de modo que os detalhes relacionados ao comércio sejam carregados no aplicativo.
   - Certifique-se de clicar no botão &quot;Salvar&quot; quando terminar de salvar todo o conteúdo criado e publicar suas alterações.
     ![publicar alterações](./images/prod-app-publish.png)

Agora que prevemos o aplicativo móvel com algum conteúdo, estamos prontos para entregar nossa campanha.


Próxima Etapa: [Fase 3 - Entrega: verificar aplicativo móvel](../delivery/app.md)

[Retorne à Fase 2 - Produção: crie um anúncio de mídia social](./social.md)

[Voltar a todos os módulos](../../overview.md)
