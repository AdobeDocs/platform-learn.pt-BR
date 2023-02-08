---
title: Bootcamp - Customer Journey Analytics - Preparação de dados no Analysis Workspace - Brasil
description: Bootcamp - Customer Journey Analytics - Preparação de dados no Analysis Workspace - Brasil
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 1%

---

# 4.4 Preparação de dados em Customer Journey Analytics

## Objetivos

- Entenda a UO do Analysis Workspace no CJA
- Entendos conceitos de preparação de dados no Analysis Workspace
- Aprenda a fazer cálculos

## 4.4.1 Interface do usuário do Analysis Workspace no CJA

O A Analysis Workspace remove como limitações icas de um único do Analytics. Ele fornece uma robusta e flexível para projetos de analytics personalizado. Arste e solte visualização de dados, alizações e (métricas, segmentos e granularidades de tempo) para um projeto. Criação instantânea de avarias e segmentos, criação de cortes para análise, criação de alertas, comparação de segmentos, análise de fluxo e de costadoria de curadoria para compartil har e agendamento em questão.

O Customer Journey Analytics traz Solução dos dados da plataforma. É altamente recommendations aceitável assistir um este vídeo visão geral de quatro:

>[!VIDEO](https://video.tv.adobe.com/v/35109?quality=12&learn=on)

Veja você o Analysis Workspace antes, recommendations este vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/26266?quality=12&learn=on)

### Crie Seu Projeto

Agora é de manhã, projeto do CJA. Vá para a aba do projetos. Clique em **Criar novo**.

![demonstração](./images/prmenu.png)

Em, você vê a tela. Selecione **Projeto em branco** então clique em **Criar**.

![demonstração](./images/prmenu1.png)

Você verá um projeto.

![demonstração](./images/premptyprojects.png)

Primeiro, certifique-se de selecionar uma Visualização de dados em canto superior da tela. exemplo, Visualização de dados selecionada ser `vangeluwe - Omnichannel Data View`.

![demonstração](./images/prdv.png)

Em, você salvar seu projeto. Você pode usar o seguinte para salvar:

| OS | Curto |
| ----------------- |-------------| 
| Windows | Controle + S |
| Mac | Command+S |

Você verá este pop-up:

![demonstração](./images/prsave.png)

Utilizar a abreviatura de nomenclatura:

| Nome | Descrição |
| ----------------- |-------------| 
| `yourLastName - Omnichannel Analysis` | `yourLastName - Omnichannel Analysis` |

Em **Salvar**.

![demonstração](./images/prsave2.png)

## 4.4.2 calculadas das metricas

Tensões os na Visualização de você, adaptar os prontos para o que usuários para os alguns . Além disso, durante processador de análise, você  calculadas para aprofundar um de insights.

Como exemplo, criuma Taxa de conversão usando um métrica/evento Compras que definimos imos na Visualização de dados.

## Taxa de conversão

Vamos começar a construtor de métricas. Clique em **+** Para sua primeira Métrica calculada

![demonstração](./images/pradd.png)

O **Criador de métricas calculadas** aparecer irá:

![demonstração](./images/prbuilder.png)

Encontro **Compras** na lista de métricas nenhum menu do lado esquerdo. Em **Métricas** panelinha **Mostrar tudo**

![demonstração](./images/calcbuildercr1.png)

Agora arraste e solte a métrica **Compras** na métrica.

![demonstração](./images/calcbuildercr2.png)

Normalmente, taxa de conversão significa **Conversões / Sessões**. Por conseguinte, &quot;&quot;Baixo&quot; cálculo na tela de métrica de calculada. Encontrar um métrica **Sessões** e arraste e-a no criador de solidão evento **Compras**.

![demonstração](./images/calcbuildercr3.png)

Observe que o operador de divisão é selecionado automaticamente.

![demonstração](./images/calcbuildercr4.png)

Um taxa de conversão é comumente representada em porcentagem. Então, vamos mudar o para, centagem e selecionar casas decimais.

![demonstração](./images/calcbuildercr5.png)

Finalmente, altere o nome e a descrição da métrica calculada:

| Title | Descrição |
| ----------------- |-------------| 
| Taxa de conversão | Taxa de conversão |

Por fim, altere o nome e a descrição da métrica calculada:

![demonstração](./images/calcbuildercr6.png)

Não se esqueça **Salvar** uma calculada Métrica.

![demonstração](./images/pr9.png)

## 4.4.3 Dimensões calculadas: Filtros (segmentação) e intervalos de dados

### Filtros: Dimensões calculadas

Os cálculos não devem ser para métricas. Antes de , é. **Dimension calculadas**. Isso significa, essencialmente **segmentos** sem Adobe Analytics. Sem Customer Journey Analytics, bagunça segmentos são chamados de **Filtros**.

![demonstração](./images/prfilters.png)

Um filtros de criação dará os usuários de negócios o calendário analytics com algumas validosas. Isso vai  o direito autoral tarefas. Abaixo estão alguns exemplos:

1. Mídia Propria, Mídia Paga,
2. Visitas novas x recorrentes
3. Clientes com carrinho abandonado

Esses podem são criados antes durante a parte de análise (o que fará no próximo).

### Intervalos de dados: Dimensões de tempo calculadas

Como de tempo do outro é de calculadas. suas, mas você também  próprias Dimensões de tempo alizadas na fase de preparação de dados.

Dimensionamento de tempo calculado ajudarão analistas e de negócios a lembrar data importantes e usá-las para filtrar e alterar o de relatório. Perguntas e dúvidas típ icas fazemos quando:

- Quando foi a Black Friday do ano? Entre os dias 21 e 29?
- Quando veiculamos aquela campanha de TV em dezembro?
- De quando fizemos como vendas de verao de 2018? Quero comparar com 2019. Um propósito, você sabe os exatos em 2019?

![demonstração](./images/timedimensions.png)

Agora você concluiu o de preparação de dados usando o Analysis Workspace do CJA.

Proxima. [4.5 Visualização usando Customer Journey Analytics](./ex5.md)

[Retornar para Fluxo 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)
