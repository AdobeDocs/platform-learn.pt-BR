---
title: Serviço de query - Uso do serviço de query
description: Serviço de query - Uso do serviço de query
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: dbf19991-cb09-43cf-887c-52996dfd2986
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---

# 4.2 Uso do serviço de query

## Objetivo

- Encontre e explore conjuntos de dados
- Saiba como abordar objetos e atributos dos Modelos de dados da experiência em suas consultas

## Contexto

Neste caso, você aprenderá a usar o PSQL para recuperar informações sobre os conjuntos de dados disponíveis, como gravar consultas para o Experience Data Model (XDM) e gravar suas primeiras consultas de relatório simples usando os conjuntos de dados do Serviço de query e do Haqqani Signal.

## 4.2.1 Consultas básicas

Neste caso, você aprenderá sobre os métodos para recuperar informações sobre os conjuntos de dados disponíveis e como recuperar corretamente os dados com uma consulta de um conjunto de dados XDM.

Todos os conjuntos de dados que exploramos pelo Adobe Experience Platform no início de 1 também estão disponíveis para acesso por meio de uma interface SQL como tabelas. Para listar essas tabelas, você pode usar a variável **mostrar tabelas;** comando.

Executar **mostrar tabelas;** em seu **Interface de linha de comando PSQL**. (não se esqueça de terminar o seu comando com um ponto e vírgula).

Copie o comando **mostrar tabelas;** e cole-o no prompt:

![command-prompt-show-tables.png](./images/command-prompt-show-tables.png)

Você verá o seguinte resultado:

```text
aepenablementfy21:all=> show tables;
                            name                            |        dataSetId         |                            dataSet                             | description | resolved 
------------------------------------------------------------+--------------------------+----------------------------------------------------------------+-------------+----------
 demo_system_event_dataset_for_call_center_global_v1_1      | 5fd1a9dea30603194baeea43 | Demo System - Event Dataset for Call Center (Global v1.1)      |             | false
 demo_system_event_dataset_for_mobile_app_global_v1_1       | 5fd1a9de250e4f194bec84cd | Demo System - Event Dataset for Mobile App (Global v1.1)       |             | false
 demo_system_event_dataset_for_voice_assistants_global_v1_1 | 5fd1a9de49ee76194b85f73c | Demo System - Event Dataset for Voice Assistants (Global v1.1) |             | false
 demo_system_event_dataset_for_website_global_v1_1          | 5fd1a9dee3224d194cdfe786 | Demo System - Event Dataset for Website (Global v1.1)          |             | false
 demo_system_profile_dataset_for_loyalty_global_v1_1        | 5fd1a9de250e4f194bec84cc | Demo System - Profile Dataset for Loyalty (Global v1.1)        |             | false
 demo_system_profile_dataset_for_ml_predictions_global_v1_1 | 5fd1a9de241f58194b0cb117 | Demo System - Profile Dataset for ML Predictions (Global v1.1) |             | false
 demo_system_profile_dataset_for_mobile_app_global_v1_1     | 5fd1a9deddf353194a2e00b7 | Demo System - Profile Dataset for Mobile App (Global v1.1)     |             | false
 demo_system_profile_dataset_for_website_global_v1_1        | 5fd1a9de42a61c194dd7b810 | Demo System - Profile Dataset for Website (Global v1.1)        |             | false
 journey_step_events                                        | 5fd1a7f30268c5194bbb7e5e | Journey Step Events                                            |             | false
```

Na dois pontos, pressione a barra de espaço para ver a próxima página do conjunto de resultados ou digite `q` para reverter para o prompt de comando.

Cada conjunto de dados na Platform tem sua tabela do Serviço de query correspondente. Você pode encontrar uma tabela do conjunto de dados por meio da interface do usuário dos conjuntos de dados:

![ui-dataset-tablename.png](./images/ui-dataset-tablename.png)

O `demo_system_event_dataset_for_website_global_v1_1` tabela é a tabela Serviço de query que corresponde à tabela `Demo System - Event Schema for Website (Global v1.1)` conjunto de dados.

Para consultar algumas informações sobre onde um produto foi visualizado, selecionaremos a variável **geografia** informações.

Copie a declaração abaixo e cole-a no prompt em **Interface de linha de comando PSQL** e pressione enter:

```sql
select placecontext.geo
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

No resultado da query, você observará que as colunas no Experience Data Model (XDM) podem ser tipos complexos e não apenas tipos escalares. Na query acima, gostaríamos de identificar localizações geográficas em que uma **commerce.productViews** ocorreu. Para identificar uma **commerce.productViews** precisamos navegar pelo modelo XDM usando o **.** (ponto) notação.

```text
aepenablementfy21:all=> select placecontext.geo
aepenablementfy21:all-> from   demo_system_event_dataset_for_website_global_v1_1
aepenablementfy21:all-> where  eventType = 'commerce.productViews'
aepenablementfy21:all-> and placecontext.geo.countryCode <> ''
aepenablementfy21:all-> limit 1;
                  geo                   
----------------------------------------
 ("(57.4694803,-3.1269422)",Tullich,GB)
(1 row)
```

Observe que o resultado é um objeto simples, em vez de um único valor? O **placecontext.geo** O objeto contém quatro atributos: esquema, país e cidade. E quando um objeto é declarado como uma coluna, ele retornará o objeto inteiro como uma string. O esquema XDM pode ser mais complexo do que o que você conhece, mas é muito eficiente e foi arquitetado para suportar muitas soluções, canais e casos de uso.

Para selecionar as propriedades individuais de um objeto, use a variável **.** (ponto) notação.

Copie a declaração abaixo e cole-a no prompt em **Interface de linha de comando PSQL**:

```sql
select placecontext.geo._schema.longitude
      ,placecontext.geo._schema.latitude
      ,placecontext.geo.city
      ,placecontext.geo.countryCode
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

O resultado da consulta acima deve ser semelhante a este.
O resultado agora é um conjunto de valores simples:

```text
aepenablementfy21:all=> select placecontext.geo._schema.longitude
aepenablementfy21:all->       ,placecontext.geo._schema.latitude
aepenablementfy21:all->       ,placecontext.geo.city
aepenablementfy21:all->       ,placecontext.geo.countryCode
aepenablementfy21:all-> from   demo_system_event_dataset_for_website_global_v1_1
aepenablementfy21:all-> where  eventType = 'commerce.productViews'
aepenablementfy21:all-> and placecontext.geo.countryCode <> ''
aepenablementfy21:all-> limit 1;
 longitude  |  latitude  |  city   | countrycode 
------------+------------+---------+-------------
 -3.1269422 | 57.4694803 | Tullich | GB
(1 row)
```

Não se preocupe, há uma maneira fácil de obter o caminho para uma propriedade específica. Na parte a seguir, você aprenderá como.

Você precisará editar uma consulta, então primeiro vamos abrir um editor.

No Windows

Clique no botão **pesquisa** ícone na barra de ferramentas do Windows, digite **bloco de notas** no **pesquisa** clique no campo **bloco de notas** resultado:

![windows-start-notepad.png](./images/windows-start-notepad.png)

No Mac

Instalar [Colchetes](https://github.com/adobe/brackets/releases/download/release-1.14/Brackets.Release.1.14.dmg) ou use outro Editor de texto preferido se ele não estiver instalado e siga as instruções. Após a instalação, procure por **Colchetes** por meio da pesquisa Mac spotlight e abra-a.

Copie a seguinte instrução para o bloco de notas ou colchetes:

```sql
select your_attribute_path_here
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

Volte para a interface do usuário do Adobe Experience Platform (deve estar aberta no navegador) ou navegue para [https://platform.adobe.com](https://platform.adobe.com).

Selecionar **Esquemas**, insira `Demo System - Event Schema for Website (Global v1.1)` no **pesquisa** e selecione `Demo System - Event Schema for Website (Global v1.1) Schema` na lista.

![browse-schema.png](./images/browse-schema.png)

Explore o modelo XDM para **Sistema de demonstração - Esquema de evento para site (Global v1.1)**, clicando em um objeto. Expanda a árvore para **placecontext**, **geografia** e **schema**. Quando você seleciona o atributo real **longitude**, você verá o caminho completo na caixa vermelha realçada. Para copiar o caminho do atributo, clique no ícone copiar caminho.

![explore-schema-for-path.png](./images/explore-schema-for-path.png)

Alterne para o bloco de notas/colchetes e remova **your_attribute_path_here** da primeira linha. Posicione o cursor após **select** na primeira linha e cole (CTRL-V).

Copie a declaração modificada de bloco de notas/colchetes e cole-a no prompt do **Interface de linha de comando PSQL** e pressione enter.

O resultado deve ser semelhante a:

```text
aepenablementfy21:all=> select placeContext.geo._schema.longitude
aepenablementfy21:all-> from   demo_system_event_dataset_for_website_global_v1_1
aepenablementfy21:all-> where  eventType = 'commerce.productViews'
aepenablementfy21:all-> and placecontext.geo.countryCode <> ''
aepenablementfy21:all-> limit 1;
 longitude  
------------
 -3.1269422
```

Próxima etapa: [4.3 Consultas, consultas, consultas... e análise de churn](./ex3.md)

[Voltar ao Módulo 4](./query-service.md)

[Voltar para todos os módulos](../../overview.md)
