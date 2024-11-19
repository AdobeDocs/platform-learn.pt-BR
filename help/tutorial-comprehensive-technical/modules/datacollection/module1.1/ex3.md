---
title: Foundation - Configuração da coleção de dados do Adobe Experience Platform e da extensão SDK da Web - Introdução à coleção de dados do Adobe Experience Platform
description: Foundation - Configuração da coleção de dados do Adobe Experience Platform e da extensão SDK da Web - Introdução à coleção de dados do Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: 391c79d6-9c42-465e-bce8-60fa6474979c
source-git-commit: 3a19e88e820c63294eff38bb8f699a9f690afcb9
workflow-type: tm+mt
source-wordcount: '1269'
ht-degree: 10%

---

# 1.1.3 Introdução à coleta de dados do Adobe Experience Platform

## Contexto

Agora vamos dar uma olhada mais profunda nos componentes da Coleção de dados da Adobe Experience Platform para entender o que está instalado em seu site de demonstração. Você verá de perto a Extensão SDK da Web da Adobe Experience Platform, configurará um elemento de dados e uma regra e aprenderá a publicar uma biblioteca.

## Extensão SDK da Web da Adobe Experience Platform

Uma extensão é um conjunto de código empacotado que estende a interface da Coleção de dados da Adobe Experience Platform e a funcionalidade da biblioteca. A Coleção de dados da Adobe Experience Platform é a plataforma e as extensões são como aplicativos que são executados na plataforma. Todas as extensões usadas no tutorial são criadas e gerenciadas pelo Adobe, mas terceiros podem criar suas próprias extensões para limitar a quantidade de código personalizado que os usuários da Coleção de dados do Adobe Experience Platform precisam gerenciar.

Vá para [Coleção de dados do Adobe Experience Platform](https://experience.adobe.com/launch/) e selecione **Marcas**.

Esta é a página Propriedades da coleção de dados do Adobe Experience Platform que você viu antes.

![Página de propriedades](./images/launch1.png)

Em **Introdução**, o Sistema de Demonstração criou duas propriedades do Cliente para você: uma para o site e outra para o aplicativo móvel. Localize-os procurando por `--aepUserLdap--` na caixa **[!UICONTROL Pesquisar]**.
Clique para abrir a propriedade **Web**.

![Caixa de pesquisa](./images/property6.png)



Em seguida, você verá a página Visão geral da propriedade. Clique em **[!UICONTROL Extensões]** no painel esquerdo, depois clique em **Adobe Experience Platform Web SDK** e em **[!UICONTROL Configurar]**.

![Página de visão geral da propriedade](./images/property7.png)

Bem-vindo ao SDK da Web da Adobe Experience Platform. Aqui você pode configurar a extensão com a sequência de dados criada em [Introdução](./../../../modules/gettingstarted/gettingstarted/ex2.md), bem como algumas configurações mais avançadas.

O domínio de borda padrão é sempre **edge.adobedc.net**. Se você implementou uma configuração CNAME em seu ambiente Adobe Experience Cloud ou Adobe Experience Platform, será necessário atualizar o **[!UICONTROL Domínio do Edge]**.

Se o domínio de borda da sua instância for diferente do padrão, atualize o domínio de borda aqui. Se não tiver certeza, use o domínio padrão. Um domínio de borda possibilita configurar um servidor de rastreamento próprio, que usa uma configuração CNAME no back-end para garantir que os dados sejam coletados no Adobe.

![Página inicial das extensões](./images/property9edgedomain.png)

Em **[!UICONTROL Sequências de dados]**, você já selecionou a sequência de dados na seção **Introdução**. Você selecionou esta sequência de dados: `--aepUserLdap-- - Demo System Datastream`, na lista da caixa **[!UICONTROL Sequência de Dados]**, para cada um dos ambientes.

Clique em **[!UICONTROL Salvar]** para voltar para o modo de exibição Extensões.

![Página inicial das extensões](./images/property9edge.png)

## Elementos de dados

Os elementos de dados são os blocos fundamentais do seu dicionário de dados (ou mapa de dados). Use elementos de dados para coletar, organizar e entregar dados em toda a tecnologia de marketing e anúncios.

Um único elemento de dados é uma variável cujo valor pode ser mapeado para consultar strings, URLs, valores de cookie, variáveis JavaScript e assim por diante. Você pode fazer referência a esse valor pelo nome da variável em toda a Coleção de dados da Adobe Experience Platform. Esta coleção de elementos de dados se torna o dicionário de dados definidos que você pode usar para criar suas regras (eventos, condições e ações). Esse dicionário de dados é compartilhado em toda a Coleção de dados da Adobe Experience Platform para uso com qualquer extensão adicionada à propriedade.

Agora você editará um elemento de dados já existente em um formato compatível com o SDK da Web.

Clique em Elementos de dados no painel à esquerda para ser levado para a página Elementos de dados.

![Página Inicial De Elementos De Dados](./images/dataelement1.png)

>[!NOTE]
>
>Você está editando apenas um elemento de dados neste exercício, mas pode ver o botão **[!UICONTROL Adicionar elemento de dados]** nesta página, que seria usado para adicionar uma nova variável ao dicionário de dados. Isso poderia ser usado em toda a Coleção de dados da Adobe Experience Platform. Fique à vontade para examinar alguns dos outros elementos de dados já existentes, principalmente usando o armazenamento local como a fonte de dados.

Na barra de pesquisa, digite **XDM - Exibição do produto** e clique no Elemento de Dados que ele retorna.

![Pesquisar ruleArticlePages](./images/dataelement2.png)

Esta tela mostra o Objeto XDM que você editará. O Experience Data Model (XDM) é um conceito que será explorado muito mais detalhadamente neste tutorial técnico, mas, por enquanto, é suficiente entendê-lo como o formato exigido pelo SDK da Web do Adobe Experience Platform. Você adicionará um pouco mais de informações aos dados coletados nas páginas de Artigo do site de demonstração.

Clique no botão de mais ao lado de **web**, na parte inferior da árvore.

Clique no botão de mais ao lado de **webPageDetails**.

Clique em **siteSection**. Agora você vê que **siteSection** ainda não está vinculado a nenhum elemento de dados. Vamos mudar isso.

![Navegar até a seção do site](./images/dataelement3.png)

Role para cima e insira o texto `%Product Category%`. Clique em **[!UICONTROL Salvar]**.

![Salvar](./images/dataelement4.png)

Neste ponto, a extensão SDK da Web da Adobe Experience Platform está instalada e você atualizou um elemento de dados para coletar dados em uma estrutura XDM. Em seguida, vamos verificar as regras que enviarão dados na hora correta.

## Regras

A coleta de dados do Adobe Experience Platform é um sistema baseado em regras. Busca a interação do usuário e dados associados. Quando os critérios definidos nas regras são cumpridos, a regra aciona a extensão, o script ou o código do lado do cliente identificado.

Crie regras para integrar os dados e a funcionalidade de tecnologia de marketing e de anúncios que unifique produtos diferentes em uma única solução.

Vamos detalhar a regra que envia dados nas páginas do artigo.

Clique em **[!UICONTROL Regras]** no painel esquerdo.

**[!UICONTROL Pesquisar]** por `Product View`.

Clique na regra retornada.

![Mídia - Pesquisa de regra das Páginas de Artigo](./images/rule1.png)

Vamos analisar os elementos individuais que compõem essa regra.

Para todas as regras: Se um **[!UICONTROL Evento]** especificado ocorrer, as **[!UICONTROL Condições]** serão avaliadas e, em seguida, as **[!UICONTROL Ações]** especificadas ocorrerão, se necessário.

![Mídia - Regra de Páginas de Artigo](./images/rule2.png)

Clique em Evento **Core - Evento personalizado**. Esta é a visualização que é carregada.

Clique na lista suspensa **Tipo de evento**.

Isso lista algumas das interações padrão que você pode usar para sinalizar a coleta de dados do Adobe Experience Platform para executar as ações, se as condições forem verdadeiras.

![Eventos](./images/rule3.png)

Clique em **[!UICONTROL Cancelar]** para voltar para a Regra.

Clique no **Enviar Evento de Experiência &quot;Exibição do Produto&quot;** da Ação.

![Enviar ação de evento](./images/rule5a.png)

Aqui você pode ver os dados que estão sendo enviados para a borda pelo SDK da Web da Adobe Experience Platform. Mais especificamente, isso é usando a **liga** **[!UICONTROL instância]** do SDK da Web. O evento **[!UICONTROL Tipo]** está definido como **Exibições do produto (carrinho) do Commerce** e os Dados XDM que você está enviando são o elemento de dados **XDM - Exibição de produto** alterado anteriormente.

![Enviar ação de evento](./images/rule5.png)

Agora que você visualizou a Regra, é possível publicar todas as alterações na Coleção de dados da Adobe Experience Platform.

## Publish em uma biblioteca

Por fim, para validar a regra e o elemento de dados que você acabou de atualizar, é necessário publicar uma biblioteca contendo os itens editados em nossa propriedade. Você precisa seguir algumas etapas rápidas na seção **[!UICONTROL Publicação]** da Coleção de dados da Adobe Experience Platform.

Clique em **[!UICONTROL Fluxo de publicação]** na navegação à esquerda

Clique na biblioteca existente, chamada **Principal**.

![Acesso à biblioteca](./images/publish1.png)

Clique no botão **Adicionar todos os recursos alterados**. Em seguida,
Clique no botão **Salvar e criar para desenvolvimento**.

![Acesso à biblioteca](./images/publish1a.png)

A biblioteca pode levar alguns minutos para ser criada e, quando estiver concluída, exibirá um ponto verde à esquerda do nome da biblioteca.

![Biblioteca de conteúdo](./images/publish2.png)

Como você pode ver na tela Fluxo de publicação, há muito mais processo de publicação na Coleção de dados da Adobe Experience Platform que está além do escopo deste tutorial. Vamos usar uma única biblioteca em nosso ambiente de desenvolvimento.

Próxima Etapa: [1.1.4 Coleta de Dados da Web no Lado do Cliente](./ex4.md)

[Voltar ao módulo 1.1](./data-ingestion-launch-web-sdk.md)

[Voltar a todos os módulos](./../../../overview.md)
