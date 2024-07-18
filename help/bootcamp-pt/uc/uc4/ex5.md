---
title: Bootcamp - Customer Journey Analytics - Visualização usando Customer Journey Analytics - Brasil
description: Bootcamp - Customer Journey Analytics - Visualização usando Customer Journey Analytics - Brasil
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Visualizations
exl-id: eb5eac54-22d8-428b-acac-16570f75085e
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 0%

---

# 4.5 Visualização usando o Customer Journey Analytics

## Objetivos

- Entenda um interface fazer Analysis Workspace
- Conheça alguns recursos que versãoram o Analysis Workspace tão diferente.
- Aprenda a analisar no CJA usando o Analysis Workspace

## Contexto

Neste exercício, você usará o Analysis Workspace no CJA para analisar visualizações de produtos, funis de produtos, rotatividade etc.

Vamos usar o projeto que você criou em [4.4 Preparação de dados no Analysis Workspace](./ex4.md), então acesse [https://analytics.adobe.com](https://analytics.adobe.com).

![demonstração](./images/prohome.png)

Abra seu projeto `yourLastName - Omnichannel Analysis`.

Com seu projeto projeto e visualização de dados `yourLastName - Omnichannel Analysis` selecionados, está pronto para começar a página principal de visualizações você.

![demonstração](./images/prodataView1.png)

## Vidas de produtos a cada dia?

Em primeiro lugar, temos a experiência como dados atualizados para os dados. Acessar o menu indicado do calendário no lado direito da tela. Clique nos itens e em todo o intervalo de datas.

>[!IMPORTANT]
>
>um intervalo de dados como **Esta semana** ou **Este mês**. Os dados relacionados mais recentes foram absorvidos em 19 de setembro de 2022.

![demonstração](./images/pro1.png)
Não há menu do lado esquerdo (área de componentes), encontrar as métricas calculadas **Visualizações do produto**. consultado em 15 de julho de 2012 &quot;µ-as e solte na tela, no canto superior direito da tabela de forma livre&quot; .

![demonstração](./images/pro2.png)

Automatizar a dimensão **Dia** será adicionada para criar sua tabela principal. Agora você pode ver sua pergunta respondida.

![demonstração](./images/pro3.png)

Em seguida, clique com o botão direito do mouse no resumo da rotação.

![demonstração](./images/pro4.png)

Clique em **Visualizar** e **Linha** como.

![demonstração](./images/pro5.png)

Você verá as suas visualizações de produto por dia.

![demonstração](./images/pro6.png)

Você pode mudar o escopo de tempo o dia alterado em **Configurações** na.

![demonstração](./images/pro7.png)

Clique em ponto ao lado de **Line** e **Manage the Data Source**.

![demonstração](./images/pro7a.png)

Em seguida, clique em **Bloquear Seleção** e **Itens Selecionados** para bloquear esta documentação para produtos que sempre exiba uma linha do tempo de Visualizações de.

![demonstração](./images/pro7b.png)

## 5 produtos mais marcados

Quais são os 5 produtos mais pesados?

créditos-se de gravura o projeto de tempos em tempos.

| Sistema operacional | Atalho |
| ----------------- |-------------| 
| Windows | Ctrl+S |
| Mac | Command+S |

Vamos começar a encontrar os 5 produtos mais. Não há menu do lado esquerdo, encontre o Nome do produto - Dimensão.

![demonstração](./images/pro8.png)

Agora ➡ e solte **Nome do produto** para forçar a modificar **Dia**:

Este será o resultado.

![demonstração](./images/pro10a.png)

Em seguida, dividir os produtos por Nome da marca. Perguntas frequentes **brandName** e reivindicações para baixo do primeiro nome do produto.

![demonstração](./images/pro13.png)

Em seguida, um detalhamento utilizando o comando de usuário. Consultar **Agente de Usuário** e solicitado-o para baixo do nome da marca.

![demonstração](./images/pro15.png)

Em sequência, será exibido a tela abaixo:

![demonstração](./images/pro15a.png)

Por fim, você pode adicionar mais visualizações. Nenhum lado esquerdo, em visualizações, pesquise `Donut`. Pegue`Donut`, arraste e solte na tela sob uma linha de visualização **** 

![demo](./images/pro18.png)

Em seguida, na Tabela, selecione as primeiras 5 **linhas de Agente do Usuário** do detalhamento que fizemos em **Smartphone Google Pixel XL 32GB Preto** > **Citi Signal**. Ao selecionar as 5 linhas, mantenha pressionado o botão **CTRL** (no Windows) ou o botão **Command** (no Mac).

Em seguida, na Tabela, as 5 linhas de **Usuário** do detalhamento que ➡ em **Smartphone Google Pixel XL 32GB Preto** > **Sinal de Citi**. Ao selecionar como 5 linhas, o botão **CTRL** (sem Windows) ou o botão **Comando** (sem Mac).

![demo](./images/pro20.png)

Você verá o gráfico de rosca alterado:

![demo](./images/pro21.png)

Você pode até adaptar o design para ser mais legível, tornando o gráfico de **Linha** e o gráfico de **Rosca** um pouco menor para que sejam exibidos lado a lado:

![demo](./images/pro22.png)

Clique no ponto ao lado de *Rosca** para **Gerenciar o Source de Dados**. Em seguida, clique em **Bloquear seleção** para bloquear essa para que ela sempre exiba uma linha do tempo de Visualizações de produto.

![demonstração](./images/pro22b.png)

Saiba mais sobre visualizações usando o Analysis Workspace em:

- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html)
- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html)

## Funil de interação do produto, da à compra compra

muitas formas de resolver questão. Uma delas é usar o Tipo de Interação de Produto e usá-lo em uma tabela de formato livre. Outra forma é usar uma **Visualização de fallout**. Vamos usar o último, temos que analisar e analisar ao mesmo tempo.

Fechhe o monitoramento histórico compartilhado:

![demonstração](./images/pro23.png)

Agora ➡ um novo painel em branco **+ Adicionar painel em branco**.

![demonstração](./images/pro24.png)

Clique na corrigir de **Fallout**.

![demonstração](./images/pro25.png)

o mesmo de datas do exercício anterior.

![demonstração](./images/prodatef.png)

Em seguida, você verá:

![demonstração](./images/prodatefa.png)

modificar um **Tipo de evento** nos componentes no lado:

![demonstração](./images/pro26.png)

Clique na seta para a abertura:

![demonstração](./images/pro27.png)

Você verá todos os Estados de eventos.

![demonstração](./images/pro28.png)

o item **commerce.productViews** e corrigir-o no campo **Adicionar Touchpoint** dentro da **Visualização de Fallout**.

![demonstração](./images/pro29.png)

Faça o mesmo com **commerce.productListAdds** e **commerce.purchases** e solte-os no campo **Add Touchpoint** dentro da **Visualização de Fallout**. Sua melhoria deve ser observada a seguir:

![demonstração](./images/props1.png)

Você pode fazer as coisas aqui. Alguns episódios: comparar ao longo do tempo, comparar cada passo por tocar ou acompanhar por. Não há nenhum equilíbrio, se quisermos analisar o curso do curso, como os clientes não compram de lidar com um item ao carrinho, podemos usar um botão de ferramentas do CJA: com o botão direito.

Clique com o botão direito do mouse no ponto de contato **commerce.productListAdds**. Em seguida, clique em **Fallout de detalhamento neste ponto de contato**.

![demonstração](./images/pro32.png)

&quot;Uma nova tabela de formato livre será analisada para analisar o que as pessoas fizeram se não compraram&quot; .

![demonstração](./images/pro33.png)

Altere o **Tipo de Evento** por **Nome da Página**, na nova tabela de formato livre, para ver em páginas eles estão indo, em vez da Página de contato de compra.

![demonstração](./images/pro34.png)

## O que as pessoas não fazem no site antes de acessar um cancelamento atendido?

Novamente, há muitas formas de realizar essa análise. Vamos usar a análise de fluxo para iniciar parte da circulação.

Fechhe o monitoramento histórico compartilhado:

![demonstração](./images/pro0.png)

Agora ➡ um novo painel em branco **+ Adicionar painel em branco**.

![demonstração](./images/pro0a.png)

Clique na ➡ **Fluxo**.

![demonstração](./images/pro35.png)

Em seguida, será exibido:

![demonstração](./images/pro351.png)

o mesmo de datas do exercício anterior.

![demo](./images/pro0b.png)

Encontre um dimensão **Página Nome** nos componentes no lado esquerdo:

![demo](./images/pro36.png)

Clique na seta para a abertura:

![demonstração](./images/pro37.png)

Você pode mudar todas as páginas vistas. Selecionar o nome da página: **Cancelar Serviço**.
Arraste e solte **Cancelar Serviço** na Visualização de fluxo no campo do meio:

![demo](./images/pro38.png)

Em seguida, será exibido:

![demo](./images/pro40.png)

Vamos analisar os clientes que visitaram a página C **Cancelar Serviço** nenhum site também pode analisar o central de atendimento e qual foi o resultado.

Nas organizada, reporter e encontre Tipo de interação de música. Arraste e solte **Tipo de interação de chamada** para modificar uma interação à direita **Visualização de fluxo**.

![demonstração](./images/pro43.png)

Agora você visualiza o ticket de suporte dos clientes que ligaram para a central de atendimento de visitar a página **Cancelar Serviço**.

![demonstração](./images/pro44.png)

Em seguida, nas organizacionais, adquirir **Sensação de Chamada**. Arraste e solte para substituir a primeira interação à direita na mudança de fluxo.

![demonstração](./images/pro46.png)

Em seguida, será exibido:

![demonstração](./images/flow.png)

Como pode ver, executamos uma análise omnichannel usando a navegação de fluxo. Graças a, mos que alguns clientes que estão presentes em lidar com o mandato tem uma avaliação positiva de ligar para o call center. Quem mudou de ideia com uma promoção?

## Qual é o cliente dos clientes com um contato de call Positivo em partes dos principais KPIs

Primado, vamos segmentar os dados para usuários usuários com chamadas {0 positivo **.** Não há CJA, os Segmentos são movidos de filtros. Acesse para filtros na área de componentes (no lado esquerdo) e clique em **+**.

![demonstração](./images/pro58.png)

Dentro do Construtor de Filtragem, dê um nome ao filtro

| Nome | Descrição |
| ----------------- |-------------| 
| Sensação de chamada - Positiva | Sensação de chamada - Positiva |

![demonstração](./images/pro47.png)

Nos componentes (dentro do Construtor de Filtro), encontre **Sensação de Chamada** e garantia e solte na Definição de filtro.

![demonstração](./images/pro48.png)

Agora **positivo** como valor para o filtro.

![demonstração](./images/pro49.png)

Alteração no escopo para o nível **Pessoa**.

![demonstração](./images/pro50.png)

Para finalizar, ➡ em **Salvar**.

![demonstração](./images/pro51.png)

Então, você muda para esta tela. Se ainda não estiver reunido, feche o painel anterior.

![demonstração](./images/pro0c.png)

Agora ➡ um novo painel em branco **+ Adicionar painel em branco**.

![demonstração](./images/pro24c.png)

o mesmo de datas do exercício anterior.

![demonstração](./images/pro24d.png)

Clique em **Tabela de forma livre**.

![demonstração](./images/pro52.png)

Agora e solte o filtro que você acabou de criar.

![demonstração](./images/pro53.png)

Hora de controlar algumas métricas. Comece com **Exibições do produto**. Arraste e solte na tabela de forma livre. Você também pode modificar a **s.**

![demonstração](./images/pro54.png)

Faça o mesmo com **Pessoas**, **Adicionar ao carrinho** e **Compras**. Você vai acabar com uma tabela como a seguir.

![demonstração](./images/pro55.png)

Graças à primeira análise de fluxo, uma nova descoberta. Então decimos todas as tarefas verificadas e verificadas KPIs em um segmento para responder a pergunta. Como você pode ver, o tempo de insight é muito mais rápido do que usar SQL ou usar outras soluções de BI.

## Recapitulação do Analysis Workspace e do Customer Journey Analytics

O Analysis Workspace remover todas as condições típicas de um serviço do Analytics. Ele fornece uma tela robusta e flexível para criar projetos de análise personalizados. Arraste e solte qualquer número de tabelas de dados, visualizações e componentes (dimensões, métricas, segmentos e granularidades de tempo) para um projeto. Você pode criar de forma instantânea filtros e analises, gráficos de coorte, alertas, segmentos, análises de fluxo e relatórios de curadoria e agendamento para compartilhar com qualquer pessoa em seu negócio.

Próxima etapa: [4.6 De insights ação](./ex6.md)

[Retorno para Fluxo de monitoramento 4](./uc4.md)

[Retorno para Todos os compartilhados](./../../overview.md)
