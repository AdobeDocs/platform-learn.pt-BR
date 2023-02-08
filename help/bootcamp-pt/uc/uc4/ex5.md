---
title: Bootcamp - Customer Journey Analytics - Visualização usando Customer Journey Analytics - Brasil
description: Bootcamp - Customer Journey Analytics - Visualização usando Customer Journey Analytics - Brasil
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 020e9fb8a1d02b93e4e95a4274806c7926c02757
workflow-type: tm+mt
source-wordcount: '1579'
ht-degree: 1%

---

# 4.5 Visualização usando Customer Journey Analytics

## Objetivos

- Entenda a interface do usuário do Analysis Workspace
- Conheça alguns Recursos que tornam o Analysis Workspace Diferente.
- Aprenda uma analisar no CJA usando no Analysis Workspace

## Contexto

exercício do exercício, você usará o Analysis Workspace no JA para analisar visualizações de produtos, funis de produtos, rotativo, etc.

Vamos usar o projeto que você criou em  [4.4 Preparação de dados no Analysis Workspace](./ex4.md), então acesse [https://analytics.adobe.com](https://analytics.adobe.com).

![demonstração](./images/prohome.png)

Abra seu projeto `yourLastName - Omnichannel Analysis`.

Com es projeto e Visualização de dados `yourLastName - Omnichannel Analysis` selecionado, você está pronto para começar um construir suas primeiras visual alizações.

![demonstração](./images/prodataView1.png)

## O Quantas visualizações de produtos temos diariamente?

Em Lugar, precisamos como dados certas para analisar os dados. Acessar o menu suspenso não calendário lado da tela. Clique em e selecione em intervalo de data aplicável.

>[!IMPORTANT]
>
>Selecione um intervalo de dados como **Nesta Semana** ou **Este mês**. Os dados disponíveis mais recentes foram absorvem vídeos em 19 de setembro de 2022.

![demonstração](./images/pro1.png)
Nenhum menu do lado esquerdo (cor da face), métricas calculadas **Exibições do produto**. Selecione-as e arraste e solte na tela, no canto superior tabela de forma livre.

![demonstração](./images/pro2.png)

dimensão **Dia** Será adicionada para sua tabela. Agora você pode ver sua pergunta respondida imediatamente.

![demonstração](./images/pro3.png)

Em, clique com o do métrica

![demonstração](./images/pro4.png)

Clique em **Visualizar** e selecione **Linha** Como visualização.

![demonstração](./images/pro5.png)

Você verá como suas visual alizações de produto por dia.

![demonstração](./images/pro6.png)

Você pode alterar o escopo de tempo para o dia clicando em **Configurações** visualização.

![demonstração](./images/pro7.png)

Clique no ponto ao lado de **Linha** e **Gerenciar a fonte de dados**.

![demonstração](./images/pro7a.png)

Em **Bloquear seleção** e selecione **Itens Selecionados** para bloquear esta visualização para que ela etera uma linha do tempo de visualização dos produtos.

![demonstração](./images/pro7b.png)

## 5 produtos vistos

Quais são os 5 produtos mais vistos?

Lembre-se de salvar o projeto de andamento em andamento.

| OS | Curto |
| ----------------- |-------------| 
| Windows | Controle + S |
| Mac | Command+S |

Vamos começar um dos 5 mais vistos. Nenhum menu do lado esquerdo, o Nome do Produto - Dimensão.

![demonstração](./images/pro8.png)

Agora arraste e solte **Nome do produto** para substituir a dimensão **Dia**:

Este será resultado.

![demonstração](./images/pro10a.png)

Em Nome dividir dos produtos. Pesquisas **brandName** e arraste para primeiro do produto.

![demonstração](./images/pro13.png)

Em, faça um detail usando Agente de usuário. Pesquisas **Agente do usuário** e arraste-o para baixo do nome da marca.

![demonstração](./images/pro15.png)

Em, exibida a abaixo:

![demonstração](./images/pro15a.png)

Por fim, você conhece mais alizações. Nenhum lado esquerdo, em visualizações, pesquisar `Donut`. Pegue `Donut`Arste e solte na tela visualização **Linha** 

![demonstração](./images/pro18.png)

Em seguida, na Tabela, selecione os primeiros 5 **Agente do usuário**  linhas do detalhamento em que fizemos **Google Pixel XL Smartphone preto de 32 GB** > **Signal do Haqqani**. Ao selecionar as 5 linhas, mantenha pressionada a tecla **CTRL** (no Windows) ou o botão **Comando** (no Mac).

Em, na Tabela, selecione como primeiras **Agente do usuário** faça fizemos detalhes **Google Pixel XL Smartphone preto de 32 GB** > **Signal do Haqqani**. Ao selecionar como 5 linhas, segure o **CTRL** (sem Windows) ou não **Comando** (sem Mac).

![demonstração](./images/pro20.png)

Você verá o gráfico de donut:

![demonstração](./images/pro21.png)

Você pode adaptar o design para ser legível, tornando o gráfico de **Linha** e o gráfico de **Rosca** um pouco menor para que sejam lado a lado

![demonstração](./images/pro22.png)

Clique no ponto ao lado de *Rosca** para **Gerenciar a fonte de dados**. Em **Bloquear seleção** para bloquear essa visualização para que ela evida uma linha do tempo de visualização alizações produto.

![demonstração](./images/pro22b.png)

Saiba mais sobre visualizações usando no Analysis Workspace em:

- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html?lang=pt-BR](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html?lang=pt-BR)
- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html)

## Funil de interação do produto, da visualização de compra

Existem muitas formas de resolver esta questão. Uma tartaruga é do tipo da Interação de usino-lo em uma tabela de livre. Outra forma é usar uma **Visualização de fallout**. Vamos usar o último pois queremos e analisar ao tempo.

Feche o painel real clicando aqui:

![demonstração](./images/pro23.png)

Agora adicione um novo painel em branco **+ Adicionar painel em branco**.

![demonstração](./images/pro24.png)

Clique na visualização de **Fallout**.

![demonstração](./images/pro25.png)

Selecione o intervalo de dados do exercício anterior.

![demonstração](./images/prodatef.png)

Em, você

![demonstração](./images/prodatefa.png)

Encontrar um dimensão **Tipo de evento** nos no lado esquerdo:

![demonstração](./images/pro26.png)

Clique na seta para abrir dimensão:

![demonstração](./images/pro27.png)

Você verá os pos de eventos disponíveis.

![demonstração](./images/pro28.png)

Selecione no item **commerce.productViews** e arraste e solte-o no campo **Adicionar ponto de contato** da **Visualização de fallout**.

![demonstração](./images/pro29.png)

Faça o o com **commerce.productListAdds** e **commerce.purches** e solte-os no campo **Adicionar ponto de contato** da  **Visualização de fallout**. O seu visualização agora, o romance semelhante ao seguinte:

![demonstração](./images/props1.png)

Você faz muitas coisas. exemplos: comparar ao longo do tempo, comparar passo por dispositivo ou comparar fidelidade. Não entanto, se quiseeeeanalisar interessantes o porquê clientes não comparação am como  o item, podemos a carrinho do CA: clicar com o.

Clique com o ponto de contato do mouse sem toque **commerce.productListAdds**. Em **Detalhar o fallout neste ponto de contato**.

![demonstração](./images/pro32.png)

Uma nova tabela de obra é criada para analisar o que se fizeram.

![demonstração](./images/pro33.png)

Alteração o **Tipo de evento** por **Nome da página**, uma nova tabela de moeda, para ver em páginas eles estão indo, em vez da confirmação de compra.

![demonstração](./images/pro34.png)

## O que é fazem não há lugar a acessar de uma bandeira Cancelar?

Novamente, há muitas formas de realizar análise. Vamos usar a análise fluxo para parte da descoberta.

Feche o painel real clicando aqui:

![demonstração](./images/pro0.png)

Agora adicione um novo painel em branco **+ Adicionar painel em branco**.

![demonstração](./images/pro0a.png)

Clique na visualização **Fluxo**.

![demonstração](./images/pro35.png)

Em, exibido:

![demonstração](./images/pro351.png)

Selecione o intervalo de dados do exercício anterior.

![demonstração](./images/pro0b.png)

Encontrar um dimensão **Nome da página** nos no lado esquerdo:

![demonstração](./images/pro36.png)

Clique na seta para abrir dimensão:

![demonstração](./images/pro37.png)

Você encontr ará como vistas páginas. Encontro no início: **Cancelar Serviço**.
Arraste e solte **Cancelar Serviço** uma Visualização de fluxo no campo meio:

![demonstração](./images/pro38.png)

Em, exibido:

![demonstração](./images/pro40.png)

Vamos agora analisar os clientes que visitaram a C **Cancelar Serviço** nenhum site também ligaram para o call center e qual foi o resultado.

Nas, torne e, de interação. Arraste e solte **Tipo de interação da chamada** para substituir primeira interação em direita **Visualização de fluxo**.

![demonstração](./images/pro43.png)

Agora você visualiza o tíquete dos clientes que ligaram para a central atendimento depois de visitar **Cancelar Serviço**.

![demonstração](./images/pro44.png)

Em, aquisição **Feed de chamada**. Arraste e solte para substituir a primeira interação à direita na visualização de fluxo.

![demonstração](./images/pro46.png)

Em, exibido:

![demonstração](./images/flow.png)

Como pode ver, executamos uma análise omnichannel usando um visualização de fluxo. Graças a isso, descobrimos que alguns que se estavam em cancelar o tiveram. Uma positiva de para o call center. Talvez mudado de ideia?

## Qual é o desempenho dos clientes com um relação Call center Positivo principais KPIs

Primeiros passos os dados para usuários com chamadas **positivo**. Não há CJA, os Segmentos são chamados de Filtros. Acesse para filtros na mané (no lado esquerdo e panelhe em) **+**.

![demonstração](./images/pro58.png)

Dentro do Construtor de filtro, dê um nome ao filtro

| Nome | Descrição |
| ----------------- |-------------| 
| Feed de chamada - Positivo | Feed de chamada - Positivo |

![demonstração](./images/pro47.png)

N. o S. (Construtor de filtro), **Feed de chamada** e arraste e solte na Definição do construtor de filtro.

![demonstração](./images/pro48.png)

Ágora selecione **positivo** como valor para o filtro.

![demonstração](./images/pro49.png)

Altere o espo para o nível **Pessoa**.

![demonstração](./images/pro50.png)

Para finatualizata, basta clicar em **Salvar**.

![demonstração](./images/pro51.png)

Então, você vai retornar para esta tela. Se Cabinda não tornou, feche painel anterior.

![demonstração](./images/pro0c.png)

Agora adicione um novo painel em branco **+ Adicionar painel em branco**.

![demonstração](./images/pro24c.png)

Selecione o intervalo de dados do exercício anterior.

![demonstração](./images/pro24d.png)

Clique em **Tabela de forma livre**.

![demonstração](./images/pro52.png)

Agora arraste e filtro que você acabou de solte.

![demonstração](./images/pro53.png)

Hora de métricas. Comece com **Exibições do produto**. Arraste e solte na tabela de forma livre. Você também pode excluir a métrica **Eventos**.

![demonstração](./images/pro54.png)

Faça o o com **Pessoas**, **Adicionar ao carrinho** e **Compras**. Você vai acabar com uma tabela como um seguinte.

![demonstração](./images/pro55.png)

Graças à primeira análise de fluxo, uma nova pergunta surgiu. Então decidimos tomar tabela e verificar KPIs em um segmento para responder a essa pergunta. Como você pode ver, tempo de insight é muito o rápido do usar SQL ou usar soluções de BI.

## Recapitulação do Analysis Workspace e do Customer Journey Analytics

Como você aninhou laboratório, no Analysis Workspace reúne os dados dos os para analisar jornada do cliente. Além disso, lembre-se de que você trazer para o espaço de trabalho que não está à jornada. Pode ser muito útil trazer desconectados para sua análise contextua Apostjornada. Alguns exemplos coisas como os dados NPS, pesquisas, eventos de anúncios do Facebook ou interações offline (não identificadas).

Proxima. [4.6 De insights a ação](./ex6.md)

[Retornar para Fluxo 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)
