---
title: Bootcamp - Customer Journey Analytics - Data preparation in Analysis Workspace - Brazil
description: Bootcamp - Customer Journey Analytics - Data preparation in Analysis Workspace - Brazil
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Workspace Basics, Calculated Metrics
exl-id: d56128af-dd1e-47ea-922f-85418e9da687
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 0%

---

# 4.4 Preparação de dados em Customer Journey Analytics

## Objetivos

- Entenda a UO do Analysis Workspace no CJA
- Entenda os problemas de mudança de dados no Analysis Workspace
- Aprenda a corrigir de dados

## 4.4.1 Interface do Analysis Workspace no CJA

O Analysis Workspace remove todas as limitações típicas de um único relatório do Analytics. Ele fornece uma tela robusta e flexível para criar projetos de analytics personalizados. Arraste e solte qualquer número de tabelas de dados, visualizações e componentes (dimensões, métricas, segmentos e granularidades de tempo) para um projeto. Criação instantânea de avarias e segmentos, criação de cortes para análise, criação de alertas, comparação de segmentos, análise de fluxo e de falhas e relatórios de curadoria e agendamento para compartilhar com qualquer pessoa em seu negócio.

O Customer Journey Analytics solução alternativa dos dados da plataforma. É muitíssimo recomendado para acompanhar este vídeo de visão geral de quatro minutos:

>[!VIDEO](https://video.tv.adobe.com/v/35109?quality=12&learn=on)

Se você nunca usou o Analysis Workspace antes, recomamos este vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/26266?quality=12&learn=on)

### Criar Seu Projeto

Agora é hora de criar primeiro projeto do CJA. Vá para a aba de projetos dentro do CJA. Clique em **Criar novo**.

![](./images/prmenu.png)

Em seguida, você verá a tela abaixo. **Projeto em branco** então clique em **Criar**.

![demonstração](./images/prmenu1.png)

Você verá um projeto e esperança.

![demonstração](./images/premptyprojects.png)

Primeiro,-se de escolha a Visualização de dados em vez de direito superior da tela. Exemplo, uma Visualização de dados a ser selecionado é `vangeluwe - Omnichannel Data View`.

![demonstração](./images/prdv.png)

Em seguida, você vai salvar seu projeto e dar um nome a ele. Você pode usar o comando para salvar:

| Sistema operacional | Atalho |
| ----------------- |-------------| 
| Windows | Ctrl+S |
| Mac | Command+S |

Você verá este pop-up:

![demonstração](./images/prsave.png)

Usar este modelo de nomenclatura:

| Nome | Descrição |
| ----------------- |-------------| 
| `yourLastName - Omnichannel Analysis` | `yourLastName - Omnichannel Analysis` |

Em seguida, clique em **Salvar**.

![demonstração](./images/prsave2.png)

## 4.4.2 Métricas calculadas

consultado em 28 de novembro de 2012 &quot;µ todos os componentes na Visualização de dados, ainda há dois anos atrás para que os usuários dos testes para analisar seus dados&quot; . Além disso, qualquer processo de análise, você pode criar as calculadas para aprofundar a pesquisa de informações.

Como exemplo, crioulo Taxa de transformação que definem a navegação/Compras na Visualização de dados.

## Taxa de ➡

Vamos começar a abrir o construtor de métricas calculadas. Clique em **+** para criar sua primeira Métrica calculada no Analysis Workspace.

![demonstração](./images/pradd.png)

O **Construtor De Métrica Calculada** irá:

![demonstração](./images/prbuilder.png)

**Compras** na lista de métricas no menu do lado esquerdo. Em **Métricas** clique em **Mostrar tudo**

![demonstração](./images/calcbuildercr1.png)

Agora destinada e sola a **Compras** na resolução da.

![demonstração](./images/calcbuildercr2.png)

, taxa de conversão **Conversões / Sessões**. Então, vamos fazer o mesmo que analisar a tela de definição de. a ➡ **Sessões** e garantie solte-a no de definição, no evento **Compras**.

![demonstração](./images/calcbuildercr3.png)

Observe que o operador de classificação é selecionado político.

![demonstração](./images/calcbuildercr4.png)

A taxa de evolução é dada em mudança. Então, vamos mudar o formato para analisar e escolher 2 casas decimais.

![demonstração](./images/calcbuildercr5.png)

Finally, Change the name and description of the calculated metric:

| Título | Descrição |
| ----------------- |-------------| 
| Conversion Rate | Conversion Rate |

Por fim, altere o nome e a descrição da:

![demonstração](./images/calcbuildercr6.png)

Não se livrar de **Salvar** a Métrica ➡.

![demonstração](./images/pr9.png)

## 4.4.3 Dimensões calculadas: Filtros (segmentação) e intervalos de datas

### Filtros: Dimensões calculadas

Os riscos não devem ser apenas para métricas. Antes de iniciar qualquer análise, também é criar algumas **Dimension calculados**. Isso limita, ➡, **sem Adobe Analytics.** Nenhum Customer Journey Analytics, esses segmentos são classificados de **Filtros**.

![demonstração](./images/prfilters.png)

A criação de eventos relacionados os usuários de a inicialização o analytics com algumas organizações calculadas valiosas. Isso irá automatizar é a responsabilidade, além de ajudar na parte de. Abaixo está compartilhado:

1. Mídia Própria, Mídia Paga,
2. Visitas novas x recorentes
3. Clientes com responsabilidade

filtros filtros podem ser analisados ou durante a parte de análise (o que você fará no próximo exercício).

### Intervalos de dados: Dimensões de tempo calculadas

A organização de tempo são outro tipo de organizações calculadas. Alguns já existentes, mas você pode mudar as tendências de tempo compartilhado na fase falsa de dados.

Estas considerações de tempo compartilhado ajudarão analistas e usuários de negócios a notar questões importantes e usá-las para filtrar e o tempo de serviço. Perguntas e respostas quando as autoridades responsáveis:

- Quando foi uma Black Friday do ano passado? Entre os dias 21 e 29?
- Quando veiculamos aquela campanha de TV em dezembro?
- De quando a situação é conhecida como as visitas de verão de 2018? Quero comparar com 2019. A propósito, você sabe os dias exatos em 2019?

![demonstração](./images/timedimensions.png)

Agora você pode o buscado de dados usando o Analysis Workspace do CJA.

Próxima etapa: [4.5 Visualização usando Customer Journey Analytics](./ex5.md)

[Retorno para Fluxo de monitoramento 4](./uc4.md)

[Retorno para Todos os compartilhados](./../../overview.md)
