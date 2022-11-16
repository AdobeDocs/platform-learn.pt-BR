---
title: Foundation - Configuração da coleta de dados do Adobe Experience Platform e da extensão do SDK da Web - Introdução à coleta de dados do Adobe Experience Platform
description: Foundation - Configuração da coleta de dados do Adobe Experience Platform e da extensão do SDK da Web - Introdução à coleta de dados do Adobe Experience Platform
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 16d97ec0-9ad9-41c6-b1a1-a0e688aa95df
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 9%

---

# 1.3 - Introdução à coleta de dados do Adobe Experience Platform

## Contexto

Agora vamos analisar os blocos de construção da Coleta de dados do Adobe Experience Platform para entender o que está instalado em seu site de demonstração. Você terá uma análise mais detalhada da Extensão do SDK da Web da Adobe Experience Platform, irá configurar um elemento de dados e uma regra e aprenderá a publicar uma biblioteca.

## 1.3.1 - Extensão Adobe Experience Platform Web SDK

Uma extensão é um conjunto de código empacotado que estende a interface da Coleta de dados do Adobe Experience Platform e a funcionalidade da biblioteca. A coleta de dados do Adobe Experience Platform é a plataforma e as extensões são como aplicativos que são executados na plataforma. Todas as extensões usadas no tutorial são criadas e gerenciadas pelo Adobe, mas terceiros podem criar suas próprias extensões para limitar a quantidade de código personalizado que os usuários da Coleta de dados da Adobe Experience Platform precisam gerenciar.

Ir para [Coleta de dados do Adobe Experience Platform](https://experience.adobe.com/launch/) e selecione **Tags**.

Esta é a página Propriedades da coleta de dados do Adobe Experience Platform que você viu anteriormente.

![Página Propriedades](./images/launch1.png)

No módulo 0, o Demo System criou duas propriedades do cliente para você: um para o site e um para o aplicativo móvel. Localizá-los pesquisando por `--demoProfileLdap--` no **[!UICONTROL Pesquisar]** caixa.

![Caixa de pesquisa](./images/property6.png)

Abra o **Web** propriedade.

Você verá a página Visão geral da propriedade . Clique em **[!UICONTROL Extensões]** no painel esquerdo. Clique no botão **[!UICONTROL Configurar]** na extensão Adobe Experience Platform Web SDK.

![Página Visão geral da propriedade](./images/property7.png)

Bem-vindo ao SDK da Web da Adobe Experience Platform! Aqui você pode configurar a extensão com o Datastream criado em [Exercício 0.2](./../module0/ex2.md) além de algumas configurações mais avançadas. Você só vai definir duas configurações para este exercício.

O Domínio de borda padrão é sempre **edge.adobedc.net**. Se você implementou uma configuração CNAME no ambiente Adobe Experience Cloud ou Adobe Experience Platform, será necessário atualizar o **[!UICONTROL Domínio de borda]**. Sua instância do Adobe Experience Platform está usando este Domínio de Borda: `--webSdkEdgeDomain--`.

Se o Domínio de borda da instância for diferente do padrão, atualize o Domínio de borda. Um Domínio de borda possibilita configurar um servidor de rastreamento próprio, que usa uma configuração CNAME no back-end para garantir que os dados sejam coletados no Adobe.

![Página inicial das extensões](./images/property9edgedomain.png)

Agora, verifique se a variável **[!UICONTROL Escolher na lista]** o botão de opção está selecionado em **[!UICONTROL Datastreams]** e selecione o conjunto de dados chamado: `--demoProfileLdap-- - Demo System Datastream`, na lista na **[!UICONTROL Datastream]** caixa.

![Página inicial das extensões](./images/property9edge.png)

Clique em **[!UICONTROL Salvar]** para voltar para a visualização Extensões.

![Página inicial do SDK da Web do Adobe Experience Platform](./images/save.png)

## 1.3.2 Elementos de dados

Os elementos de dados são os blocos fundamentais do seu dicionário de dados (ou mapa de dados). Use elementos de dados para coletar, organizar e entregar dados em toda a tecnologia de marketing e anúncios.

Um único elemento de dados é uma variável cujo valor pode ser mapeado para consultar strings, URLs, valores de cookie, variáveis JavaScript e assim por diante. Você pode fazer referência a esse valor pelo nome da variável em toda a Coleta de dados do Adobe Experience Platform. Esta coleção de elementos de dados se torna o dicionário de dados definidos que você pode usar para criar suas regras (eventos, condições e ações). Esse dicionário de dados é compartilhado em toda a Coleta de dados da Adobe Experience Platform para uso com qualquer extensão adicionada à propriedade.

Agora você editará um elemento de dados já existente em um formato compatível com o SDK da Web.

Clique em Elementos de dados no painel à esquerda para acessar a página Elementos de dados .

![Página inicial dos elementos de dados](./images/dataelement1.png)

>[!NOTE]
>
>Você só está editando um elemento de dados neste exercício, mas pode ver a variável **[!UICONTROL Adicionar elemento de dados]** nessa página, que seria usada para adicionar uma nova variável ao dicionário de dados. Isso pode ser usado em toda a Coleta de dados do Adobe Experience Platform. Você pode ver alguns dos outros elementos de dados já existentes, principalmente usando o armazenamento local como fonte de dados.

Na barra de pesquisa, digite **XDM - Exibição do produto** e clique no Elemento de dados retornado.

![Pesquisar por ruleArticlePages](./images/dataelement2.png)

Esta tela mostra o objeto XDM que você editará. O Experience Data Model (XDM) é um conceito que será explorado muito mais neste Tutorial técnico, mas por enquanto é suficiente entendê-lo como o formato exigido pelo Adobe Experience Platform Web SDK. Você adicionará um pouco mais de informações aos dados coletados nas páginas do artigo do site de demonstração.

Clique no botão de mais ao lado de **web** na parte inferior da árvore.

Clique no botão de mais ao lado de **webPageDetails**.

Clique em **siteSection**. Agora você vê isso **siteSection** ainda não está vinculado a nenhum elemento de dados. Vamos mudar isso.

![Navegar até a seção do site](./images/dataelement3.png)

Role para cima e insira o texto `%Product Category%`. Clique em **[!UICONTROL Salvar]**.

![Salvar](./images/dataelement4.png)

Neste ponto, a extensão Adobe Experience Platform Web SDK está instalada e você atualizou um elemento de dados para coletar dados em relação a uma estrutura XDM. Em seguida, vamos verificar as regras que enviarão dados no horário correto.

## 1.3.3 Regras

A Coleta de dados do Adobe Experience Platform é um sistema baseado em regras. Busca a interação do usuário e dados associados. Quando os critérios definidos nas regras são cumpridos, a regra aciona a extensão, o script ou o código do lado do cliente identificado.

Crie regras para integrar os dados e a funcionalidade de tecnologia de marketing e de anúncios que unifique produtos diferentes em uma única solução.

Vamos analisar a regra que envia dados nas páginas do artigo.

Clique em **[!UICONTROL Regras]** no painel esquerdo.

**[!UICONTROL Pesquisar]** para `Product View`.

Clique na regra que é retornada.

![Mídia - Pesquisa da regra de Páginas do artigo](./images/rule1.png)

Vamos analisar os elementos individuais que compõem esta regra. Para todas as regras Se uma **[!UICONTROL Evento]** ocorre, **[!UICONTROL Condições]** são avaliadas e, em seguida, especificadas **[!UICONTROL Ações]** se necessário.

![Mídia - Regra de páginas do artigo](./images/rule2.png)

Clique no evento **Evento personalizado - Exibição do produto**. Essa é a exibição carregada.

Clique no botão **Tipo de evento** menu suspenso.

Isso lista algumas das interações padrão que podem ser usadas para sinalizar a Coleta de dados do Adobe Experience Platform para executar as ações, caso as condições sejam verdadeiras.

![Eventos](./images/rule3.png)

Clique em **[!UICONTROL Cancelar]** para voltar à Regra.

Clique na Ação **Enviar evento de &quot;Exibição de produto&quot; para o AEP**.

Aqui você pode ver os dados que estão sendo enviados para a Adobe Edge pelo SDK da Web da Adobe Experience Platform. Mais especificamente, isso está usando a variável **liga** **[!UICONTROL Instância]** do SDK da Web. Configurando outro **[!UICONTROL Instância]** permitiria a utilização de diferentes Datastreams, entre outras coisas. Você especificou o evento **[!UICONTROL Tipo]** como um **commerce.productViews** e os dados XDM que você está enviando são **XDM - Exibição do produto** elemento de dados alterado anteriormente.

![Enviar ação de evento](./images/rule5.png)

Agora que você visualizou a Regra, é possível publicar todas as alterações na Coleta de dados do Adobe Experience Platform.

## 1.3.4 Publicar em uma biblioteca

Finalmente, para validar a regra e o elemento de dados que você acabou de atualizar, é necessário publicar uma biblioteca contendo os itens editados em nossa propriedade. Há algumas etapas rápidas que você precisa tomar no **[!UICONTROL Publicação]** da Coleta de dados do Adobe Experience Platform.

Clique em **[!UICONTROL Fluxo de publicação]** na navegação à esquerda

Clique na biblioteca existente, chamada de **Principal**.

![Acesso à biblioteca](./images/publish1.png)

Clique no botão **Adicionar todos os recursos alterados** botão.

![Acesso à biblioteca](./images/publish1a.png)

Role para baixo para ver que a maioria dos recursos permanecerá como **Revisão 1 (mais recente)**, mas os dois que mudamos - **Elemento de dados: ruleArticlePages** e **Extensão: Adobe Experience Platform Web SDK** será marcado com apenas **Mais recentes**.

Clique no botão **Salvar e criar para desenvolvimento** botão.

![Biblioteca de conteúdo](./images/publish2.png)

A biblioteca pode levar alguns minutos para ser criada e, quando estiver concluída, exibirá um ponto verde à esquerda do nome da biblioteca.

Como você pode ver na tela Fluxo de publicação, há muito mais no processo de publicação na Coleta de dados do Adobe Experience Platform que está além do escopo deste tutorial. Vamos usar apenas uma biblioteca em nosso ambiente de desenvolvimento.

Próxima etapa: [1.4 Coleta de dados da Web do lado do cliente](./ex4.md)

[Voltar ao Módulo 1](./data-ingestion-launch-web-sdk.md)

[Voltar para todos os módulos](./../../overview.md)
