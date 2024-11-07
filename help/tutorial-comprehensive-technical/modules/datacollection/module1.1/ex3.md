---
title: Foundation - Configuração da coleção de dados do Adobe Experience Platform e da extensão SDK da Web - Introdução à coleção de dados do Adobe Experience Platform
description: Foundation - Configuração da coleção de dados do Adobe Experience Platform e da extensão SDK da Web - Introdução à coleção de dados do Adobe Experience Platform
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 9%

---

# 1.1.3 - Introdução à coleta de dados do Adobe Experience Platform

## Contexto

Agora vamos dar uma olhada mais profunda nos componentes da Coleção de dados da Adobe Experience Platform para entender o que está instalado em seu site de demonstração. Você verá de perto a Extensão SDK da Web da Adobe Experience Platform, configurará um elemento de dados e uma regra e aprenderá a publicar uma biblioteca.

## 1.1.3.1 - Extensão SDK da Web do Adobe Experience Platform

Uma extensão é um conjunto de código empacotado que estende a interface da Coleção de dados da Adobe Experience Platform e a funcionalidade da biblioteca. A Coleção de dados da Adobe Experience Platform é a plataforma e as extensões são como aplicativos que são executados na plataforma. Todas as extensões usadas no tutorial são criadas e gerenciadas pelo Adobe, mas terceiros podem criar suas próprias extensões para limitar a quantidade de código personalizado que os usuários da Coleção de dados do Adobe Experience Platform precisam gerenciar.

Vá para [Coleção de dados do Adobe Experience Platform](https://experience.adobe.com/launch/) e selecione **Marcas**.

Esta é a página Propriedades da coleção de dados do Adobe Experience Platform que você viu antes.

![Página de propriedades](./images/launch1.png)

No módulo 0, o Sistema de demonstração criou duas propriedades do cliente para você: uma para o site e outra para o aplicativo móvel. Localize-os procurando por `--aepUserLdap--` na caixa **[!UICONTROL Pesquisar]**.

![Caixa de pesquisa](./images/property6.png)

Abra a propriedade **Web**.

Em seguida, você verá a página Visão geral da propriedade. Clique em **[!UICONTROL Extensões]** no painel esquerdo. Clique no botão **[!UICONTROL Configurar]** na Extensão SDK da Web da Adobe Experience Platform.

![Página de visão geral da propriedade](./images/property7.png)

Bem-vindo ao SDK da Web da Adobe Experience Platform. Aqui você pode configurar a extensão com a sequência de dados criada no [Exercício 0.2](./../../../modules/gettingstarted/gettingstarted/ex2.md), bem como algumas configurações mais avançadas. Você só definirá duas configurações para este exercício.

O Domínio padrão do Edge é sempre **edge.adobedc.net**. Se você implementou uma configuração CNAME em seu ambiente Adobe Experience Cloud ou Adobe Experience Platform, será necessário atualizar o **[!UICONTROL Domínio do Edge]**. Sua instância do Adobe Experience Platform está usando este Domínio Edge: `--webSdkEdgeDomain--`.

Se o Domínio Edge da sua instância for diferente do padrão, atualize o Domínio Edge. Um Domínio do Edge possibilita configurar um servidor de rastreamento próprio, que usa uma configuração CNAME no back-end para garantir que os dados sejam coletados no Adobe.

![Página inicial das extensões](./images/property9edgedomain.png)

Agora, verifique se o botão de opção **[!UICONTROL Escolher da lista]** está selecionado no cabeçalho **[!UICONTROL Sequências de Dados]** e selecione a sequência de dados chamada: `--aepUserLdap-- - Demo System Datastream`, na lista da caixa **[!UICONTROL Sequência de Dados]**.

![Página inicial das extensões](./images/property9edge.png)

Clique em **[!UICONTROL Salvar]** para voltar para o modo de exibição Extensões.

![Página inicial do SDK da Web do Adobe Experience Platform](./images/save.png)

## 1.1.3.2 Elementos de dados

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

## 1.1.3.3 Regras

A coleta de dados do Adobe Experience Platform é um sistema baseado em regras. Busca a interação do usuário e dados associados. Quando os critérios definidos nas regras são cumpridos, a regra aciona a extensão, o script ou o código do lado do cliente identificado.

Crie regras para integrar os dados e a funcionalidade de tecnologia de marketing e de anúncios que unifique produtos diferentes em uma única solução.

Vamos detalhar a regra que envia dados nas páginas do artigo.

Clique em **[!UICONTROL Regras]** no painel esquerdo.

**[!UICONTROL Pesquisar]** por `Product View`.

Clique na regra retornada.

![Mídia - Pesquisa de regra das Páginas de Artigo](./images/rule1.png)

Vamos analisar os elementos individuais que compõem essa regra. Para todas as regras: Se um **[!UICONTROL Evento]** especificado ocorrer, as **[!UICONTROL Condições]** serão avaliadas e, em seguida, as **[!UICONTROL Ações]** especificadas ocorrerão, se necessário.

![Mídia - Regra de Páginas de Artigo](./images/rule2.png)

Clique no **Evento personalizado - Exibição do produto**. Esta é a visualização que é carregada.

Clique na lista suspensa **Tipo de evento**.

Isso lista algumas das interações padrão que você pode usar para sinalizar a coleta de dados do Adobe Experience Platform para executar as ações, se as condições forem verdadeiras.

![Eventos](./images/rule3.png)

Clique em **[!UICONTROL Cancelar]** para voltar para a Regra.

Clique no Evento Ação **Enviar &quot;Exibição do Produto&quot; para a AEP**.

Aqui você pode ver os dados que estão sendo enviados para a Adobe Edge pelo SDK da Web da Adobe Experience Platform. Mais especificamente, isso é usando a **liga** **[!UICONTROL instância]** do SDK da Web. Configurar outra **[!UICONTROL Instância]** permitiria que diferentes Datastreams fossem usados, entre outras coisas. Você especificou o evento **[!UICONTROL Tipo]** como um **commerce.productViews** e os Dados XDM que está enviando são o elemento de dados **XDM - Exibição de Produto** que você alterou anteriormente.

![Enviar ação de evento](./images/rule5.png)

Agora que você visualizou a Regra, é possível publicar todas as alterações na Coleção de dados da Adobe Experience Platform.

## 1.1.3.4 Publish em uma biblioteca

Por fim, para validar a regra e o elemento de dados que você acabou de atualizar, é necessário publicar uma biblioteca contendo os itens editados em nossa propriedade. Você precisa seguir algumas etapas rápidas na seção **[!UICONTROL Publicação]** da Coleção de dados da Adobe Experience Platform.

Clique em **[!UICONTROL Fluxo de publicação]** na navegação à esquerda

Clique na biblioteca existente, chamada **Principal**.

![Acesso à biblioteca](./images/publish1.png)

Clique no botão **Adicionar todos os recursos alterados**.

![Acesso à biblioteca](./images/publish1a.png)

Role para baixo para ver que a maioria dos recursos permanecerá como **Revisão 1 (Mais Recente)**, mas os dois que alteramos - **Elemento de Dados: ruleArticlePages** e **Extensão: Adobe Experience Platform Web SDK** serão marcados apenas com **Mais Recente**.

Clique no botão **Salvar e criar para desenvolvimento**.

![Biblioteca de conteúdo](./images/publish2.png)

A biblioteca pode levar alguns minutos para ser criada e, quando estiver concluída, exibirá um ponto verde à esquerda do nome da biblioteca.

Como você pode ver na tela Fluxo de publicação, há muito mais processo de publicação na Coleção de dados da Adobe Experience Platform que está além do escopo deste tutorial. Vamos usar uma única biblioteca em nosso ambiente de desenvolvimento.

Próxima Etapa: [1.1.4 Coleta de Dados da Web no Lado do Cliente](./ex4.md)

[Voltar ao módulo 1.1](./data-ingestion-launch-web-sdk.md)

[Voltar a todos os módulos](./../../../overview.md)
