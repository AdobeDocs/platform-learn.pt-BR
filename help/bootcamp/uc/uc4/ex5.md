---
title: Bootcamp - Customer Journey Analytics - Visualização usando Customer Journey Analytics
description: Bootcamp - Customer Journey Analytics - Visualização usando Customer Journey Analytics
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 051b5b91-56c4-414e-a4c4-74aa67219551
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1500'
ht-degree: 1%

---

# 4.5 Visualização usando Customer Journey Analytics

## Objetivos

- Entender a interface do usuário do Analysis Workspace
- Saiba mais sobre alguns recursos que tornam o Analysis Workspace tão diferente.
- Saiba como analisar no CJA usando o Analysis Workspace

## Contexto

Neste exercício, você usará o Analysis Workspace no CJA para analisar exibições de produtos, funis de produtos, churn etc.

Vamos usar o projeto criado em [4.4 Preparação de dados no Analysis Workspace](./ex4.md), vá para [https://analytics.adobe.com](https://analytics.adobe.com).

![demonstração](./images/prohome.png)

Abra o projeto `yourLastName - Omnichannel Analysis`.

Com seu projeto aberto e a Exibição de dados `yourLastName - Omnichannel Analysis` selecionado, você está pronto para começar a criar suas primeiras visualizações.

![demonstração](./images/prodataView1.png)

## Quantas visualizações de produtos temos diariamente

Primeiro, precisamos selecionar as datas certas para analisar os dados. Vá para a lista suspensa do calendário no lado direito da tela de desenho. Clique nele e selecione o intervalo de datas aplicável.

>[!IMPORTANT]
>
>Selecione um intervalo de datas como **Nesta Semana** ou **Este mês**. Os dados disponíveis mais recentes foram assimilados em 19 de setembro de 2022.

![demonstração](./images/pro1.png)

No menu à esquerda (área de componentes), localize a Métrica calculada **Exibições do produto**. Selecione-o e arraste-o e solte-o na tela, na parte superior direita da tabela de forma livre.

![demonstração](./images/pro2.png)

Dimensionar automaticamente a dimensão **Dia** serão adicionadas para criar a primeira tabela. Agora vocês podem ver sua pergunta respondida em tempo real.

![demonstração](./images/pro3.png)

Em seguida, clique com o botão direito do mouse no resumo da métrica.

![demonstração](./images/pro4.png)

Clique em **Visualizar** e depois selecione **Linha** como visualização.

![demonstração](./images/pro5.png)

Você verá suas visualizações de produtos por dia.

![demonstração](./images/pro6.png)

Você pode alterar o escopo de tempo para dia clicando em **Configurações** na visualização.

![demonstração](./images/pro7.png)

Clique no ponto ao lado de **Linha** para **Gerenciar a fonte de dados**.

![demonstração](./images/pro7a.png)

Em seguida, clique em **Bloquear seleção** e selecione **Itens Selecionados** para bloquear essa visualização de modo que ela sempre exiba uma linha do tempo de Exibições do produto.

![demonstração](./images/pro7b.png)

## Os 5 principais produtos visualizados

Quais são os 5 principais produtos visualizados?

Lembre-se de salvar o projeto de vez em quando.

| OS | Curto |
| ----------------- |-------------| 
| Windows | Controle + S |
| Mac | Command+S |

Vamos começar a encontrar os 5 principais produtos visualizados. No menu lateral esquerdo, localize a variável **Nome do produto** - Dimension.

![demonstração](./images/pro8.png)

Arrastar e soltar **Nome do produto** para substituir o **Dia** dimensão:

Esse será o resultado

![demonstração](./images/pro10a.png)

Em seguida, tente detalhar um dos produtos por Nome da Marca. Procurar por **brandName** e arraste-o para baixo do nome do produto.

![demonstração](./images/pro13.png)

Em seguida, faça um detalhamento usando o Agente do usuário. Procurar por **Agente do usuário** e arraste-a sob o nome da marca.

![demonstração](./images/pro15.png)

Você verá isso:

![demonstração](./images/pro15a.png)

Por fim, é possível adicionar mais visualizações. No lado esquerdo, em visualizações, procure por `Donut`. Tome `Donut`, arraste-o e solte-o na tela sob a **Linha** visualização.

![demonstração](./images/pro18.png)

Em seguida, na Tabela, selecione os primeiros 5 **Agente do usuário**  linhas do detalhamento em que fizemos **Google Pixel XL Smartphone preto de 32 GB** > **Signal do Haqqani**. Ao selecionar as 5 linhas, mantenha pressionada a tecla **CTRL** (no Windows) ou o botão **Comando** (no Mac).

![demonstração](./images/pro20.png)

Você verá o gráfico de rosca alterado:

![demonstração](./images/pro21.png)

Você pode até adaptar o design para que seja mais legível, tornando **Linha** e o **Rosca** gráfico um pouco menor para que se ajustem um ao outro:

![demonstração](./images/pro22.png)

Clique no ponto ao lado de **Rosca** para **Gerenciar a fonte de dados**.
Em seguida, clique em **Bloquear seleção** para bloquear essa visualização de modo que ela sempre exiba uma linha do tempo de Exibições do produto.

![demonstração](./images/pro22b.png)

Saiba mais sobre visualizações usando o Analysis Workspace aqui:

- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html?lang=pt-BR](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html?lang=pt-BR)
- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html)

## Funil de interação do produto, da visualização à compra

Há muitas maneiras de resolver essa questão. Uma delas é usar o Tipo de interação do produto e usá-lo em uma tabela de forma livre. Outra maneira é usar um **Visualização de fallout**. Vamos usar o último como queremos visualizar e analisar ao mesmo tempo.

Feche o painel atual clicando aqui:

![demonstração](./images/pro23.png)

Em seguida, adicione um novo painel em branco clicando em **+ Adicionar painel em branco**.

![demonstração](./images/pro24.png)

Clique na visualização **Fallout**.

![demonstração](./images/pro25.png)

Selecione o mesmo intervalo de datas do exercício anterior.

![demonstração](./images/prodatef.png)

Você verá isso.

![demonstração](./images/prodatefa.png)

Encontre a dimensão **Tipo de evento** sob os componentes do lado esquerdo:

![demonstração](./images/pro26.png)

Clique na seta para abrir a dimensão:

![demonstração](./images/pro27.png)

Você verá todos os tipos de evento disponíveis.

![demonstração](./images/pro28.png)

Selecionar o item **commerce.productViews** e arraste e solte-o no **Adicionar ponto de contato** dentro do **Visualização de fallout**.

![demonstração](./images/pro29.png)

Faça o mesmo com **commerce.productListAdds** e **commerce.purches** e solte-os no **Adicionar ponto de contato** dentro do **Visualização de fallout**. A visualização terá esta aparência:

![demonstração](./images/props1.png)

Você pode fazer muitas coisas aqui. Alguns exemplos: comparar ao longo do tempo, comparar cada etapa por dispositivo ou comparar por fidelidade. No entanto, se queremos analisar coisas interessantes como por que os clientes não compram depois de adicionar um item ao carrinho, podemos usar a melhor ferramenta no CJA: clique com o botão direito do mouse.

Clique com o botão direito no ponto de contato **commerce.productListAdds**. Em seguida, clique em **Detalhar o fallout neste ponto de contato**.

![demonstração](./images/pro32.png)

Será criada uma nova tabela de forma livre para analisar o que as pessoas fizeram se não compraram.

![demonstração](./images/pro33.png)

Altere o **Tipo de evento** por **Nome da página**, na nova tabela de forma livre, para ver quais páginas estão indo, em vez da Página de confirmação de compra.

![demonstração](./images/pro34.png)

## O que as pessoas fazem no site antes de acessar a página Cancelar Serviço?

Novamente, há muitas maneiras de executar essa análise. Vamos usar a análise de fluxo para iniciar a parte de descoberta.

Feche o painel atual clicando aqui:

![demonstração](./images/pro0.png)

Em seguida, adicione um novo painel em branco clicando em **+ Adicionar painel em branco**.

![demonstração](./images/pro0a.png)

Clique na visualização **Fluxo**.

![demonstração](./images/pro35.png)

Você verá isso:

![demonstração](./images/pro351.png)

Selecione o mesmo intervalo de datas do exercício anterior.

![demonstração](./images/pro0b.png)

Encontre a dimensão **Nome da página** sob os componentes do lado esquerdo:

![demonstração](./images/pro36.png)

Clique na seta para abrir a dimensão:

![demonstração](./images/pro37.png)

Você encontrará todas as páginas visualizadas. Encontre o nome da página: **Cancelar Serviço**.
Arrastar e soltar **Cancelar Serviço** no campo Fluxo Visualization no meio:

![demonstração](./images/pro38.png)

Você verá isso:

![demonstração](./images/pro40.png)

Agora vamos analisar se os clientes que visitaram o **Cancelar Serviço** A página no site também chamou o callcenter e qual foi o resultado.

Sob as dimensões, volte e localize **Tipo de interação da chamada**.
Arrastar e soltar **Tipo de interação da chamada** para substituir a primeira interação à direita no **Visualização de fluxo**.

![demonstração](./images/pro43.png)

Agora você está vendo o tíquete de suporte dos clientes que chamaram a central de atendimento depois de visitar o **Cancelar Serviço** página.

![demonstração](./images/pro44.png)

Em seguida, nas dimensões, pesquise por **Feed de chamada**.  Arraste e solte-o para substituir a primeira interação à direita no **Visualização de fluxo**.

![demonstração](./images/pro46.png)

Você verá isso:

![demonstração](./images/flow.png)

Como você pode ver, executamos uma análise omnicanal usando a Visualização de fluxo. Graças a isso, descobrimos que alguns clientes que pensavam em cancelar seu serviço tinham um sentimento positivo depois de ligar para o centro de atendimento. Será que talvez tenhamos mudado de ideias com uma promoção?


## Como os clientes com um contato Callcenter positivo estão se saindo em relação aos KPIs principais?

Vamos primeiro segmentar os dados para obter somente usuários com **positivo** chamadas . No CJA, os segmentos são chamados de Filtros. Vá para filtros dentro da área do componente (no lado esquerdo) e clique em **+**.

![demonstração](./images/pro58.png)

No Construtor de filtros, dê um nome ao filtro

| Nome | Descrição |
| ----------------- |-------------| 
| Feed de chamada - Positivo | Feed de chamada - Positivo |

![demonstração](./images/pro47.png)

Nos componentes (dentro do Construtor de filtros), encontre **Feed de chamada** e arraste e solte-o em Definição do Construtor de filtros.

![demonstração](./images/pro48.png)

Em seguida, selecione **positivo** como valor para o filtro.

![demonstração](./images/pro49.png)

Alterar o escopo a ser **Pessoa** nível.

![demonstração](./images/pro50.png)

Para concluir, basta clicar em **Salvar**.

![demonstração](./images/pro51.png)

Então você estará de volta. Se ainda não tiver sido feito, feche o painel anterior.

![demonstração](./images/pro0c.png)

Em seguida, adicione um novo painel em branco clicando em **+ Adicionar painel em branco**.

![demonstração](./images/pro24c.png)

Selecione o mesmo intervalo de datas do exercício anterior.

![demonstração](./images/pro24d.png)

Clique em **Tabela de forma livre**.

![demonstração](./images/pro52.png)

Agora, arraste e solte o filtro que acabou de criar.

![demonstração](./images/pro53.png)

Tempo para adicionar algumas métricas. Comece com **Exibições do produto**. Arraste e solte na tabela de forma livre. Também é possível excluir o **Eventos** métrica.

![demonstração](./images/pro54.png)

Faça o mesmo com **Pessoas**,  **Adicionar ao carrinho** e **Compras**. Você vai acabar com uma mesa como esta.

![demonstração](./images/pro55.png)

Graças à primeira análise de fluxo, veio-me à mente uma nova questão. Então decidimos criar esta tabela e verificar alguns KPIs em relação a um segmento para responder essa pergunta. Como você pode ver, o tempo de insight é muito mais rápido do que usar SQL ou outras soluções de BI.

## Recapitulação do Customer Journey Analytics e Analysis Workspace

Como você aprendeu neste laboratório, a Analysis Workspace une os dados de todos os canais para analisar toda a jornada do cliente. Além disso, lembre-se de que é possível trazer dados para o mesmo espaço de trabalho que não é compilado para a jornada.
Pode ser realmente útil trazer dados desconectados para sua análise para contextualizar a jornada. Alguns exemplos incluem informações como dados NPS, pesquisas, eventos Facebook Ads ou interações offline (não identificadas).

Próxima etapa: [4.6 De insights à ação](./ex6.md)

[Voltar para Fluxo de Usuário 4](./uc4.md)

[Voltar para todos os módulos](./../../overview.md)
