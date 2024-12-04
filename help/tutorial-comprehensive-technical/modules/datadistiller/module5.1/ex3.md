---
title: Serviço de consulta - Uso do Serviço de consulta
description: Serviço de consulta - Uso do Serviço de consulta
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
exl-id: 31c14a9b-cb62-48ab-815c-caa6e832794f
source-git-commit: d9d9a38c1e160950ae755e352a54667c8a7b30f7
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 0%

---

# 5.1.3 Uso do Serviço de consulta

## Objetivo

- Encontrar e explorar conjuntos de dados
- Saiba como abordar objetos e atributos do Experience Data Models em suas consultas

## Contexto

Com isso, você aprenderá a usar o PSQL para recuperar informações sobre os conjuntos de dados disponíveis, como gravar uma consulta para o Experience Data Model (XDM) e gravar suas primeiras consultas de relatórios simples usando o Serviço de consulta e os conjuntos de dados do Citi Signal.

## Consultas básicas

Nesta seção, você aprenderá sobre os métodos para recuperar informações sobre os conjuntos de dados disponíveis e como recuperar dados corretamente com uma consulta de um conjunto de dados XDM.

Todos os conjuntos de dados que exploramos por meio do Adobe Experience Platform no início do 1 também estão disponíveis para acesso por meio de uma interface SQL como tabelas. Para listar essas tabelas, você pode usar o comando **show tables;**.

Execute `show tables;` em sua **interface de linha de comando do PSQL**. (não se esqueça de terminar o comando com um ponto e vírgula).

Copie o comando `show tables;` e cole-o no prompt:

![command-prompt-show-tables.png](./images/commandpromptshowtables.png)

Você verá o seguinte resultado:

```text
tech-insiders:all=> show tables;
                               name                               |                                                  dataSetId                                                   |                                       dataSet                                        | description |        labels        
------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+-------------+----------------------
 ajo_bcc_feedback_event_dataset                                   | 672a07cb7728e82aefa1ec56                                                                                     | AJO BCC Feedback Event Dataset                                                       |             | 
 ajo_classification_dataset                                       | 672a07cab55b0d2aef6f9626                                                                                     | AJO Classification Dataset                                                           |             | 
 ajo_consent_service_dataset                                      | 672a07c80fd5fd2aee4155ca                                                                                     | AJO Consent Service Dataset                                                          |             | 'PROFILE'
 ajo_email_tracking_experience_event_dataset                      | 672a07c926d57d2aef020230                                                                                     | AJO Email Tracking Experience Event Dataset                  :
                               name                               |                                                  dataSetId                                                   |                                       dataSet                                        | description |        labels        
------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+-------------+----------------------
 ajo_bcc_feedback_event_dataset                                   | 672a07cb7728e82aefa1ec56                                                                                     | AJO BCC Feedback Event Dataset                                                       |             | 
 ajo_classification_dataset                                       | 672a07cab55b0d2aef6f9626                                                                                     | AJO Classification Dataset                                                           |             | 
 ajo_consent_service_dataset                                      | 672a07c80fd5fd2aee4155ca                                                                                     | AJO Consent Service Dataset                                                          |             | 'PROFILE'
 ajo_email_tracking_experience_event_dataset                      | 672a07c926d57d2aef020230                                                                                     | AJO Email Tracking Experience Event Dataset   
```

No sinal de dois pontos, pressione a barra de espaço para ver a próxima página do conjunto de resultados, ou digite `q` para reverter para o prompt de comando.

Cada conjunto de dados na AEP tem sua tabela de Serviço de consulta correspondente. Você pode encontrar a tabela de um conjunto de dados por meio da interface do usuário de conjuntos de dados:

![ui-dataset-tablename.png](./images/uidatasettablename.png)

A tabela `demo_system_event_dataset_for_website_global_v1_1` é a tabela do Serviço de Consulta que corresponde ao conjunto de dados `Demo System - Event Schema for Website (Global v1.1)`.

Para consultar algumas informações sobre onde um produto foi exibido, selecionaremos as informações **geo**.

Copie a consulta abaixo e cole-a no prompt em sua **interface de linha de comando do PSQL** e pressione Enter:

```sql
select placecontext.geo
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

No resultado da query, você observará que as colunas no Experience Data Model (XDM) podem ser tipos complexos e não apenas tipos escalares. Na consulta acima, gostaríamos de identificar localizações geográficas em que um **commerce.productViews** ocorreu. Para identificar um **commerce.productViews**, precisamos navegar pelo modelo XDM usando o **.Notação** (ponto).

```text
tech-insiders:all=> select placecontext.geo
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
                 geo                  
--------------------------------------
 ("(51.59119,-1.407848)",Charlton,GB)
(1 row)
```

Observe que o resultado é um objeto plano em vez de um valor único? O objeto **placecontext.geo** contém quatro atributos: esquema, país e cidade. E quando um objeto é declarado como uma coluna, ele retornará o objeto inteiro como uma string. O esquema XDM pode ser mais complexo do que o que você conhece, mas é muito eficiente e foi projetado para oferecer suporte a muitas soluções, canais e casos de uso.

Para selecionar as propriedades individuais de um objeto, use o **.Notação** (ponto).

Copie a instrução abaixo e cole-a no prompt em sua **interface de linha de comando do PSQL**:

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

O resultado da consulta acima deve ter esta aparência.
O resultado agora é um conjunto de valores simples:

```text
tech-insiders:all=> select placecontext.geo._schema.longitude
      ,placecontext.geo._schema.latitude
      ,placecontext.geo.city
      ,placecontext.geo.countryCode
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
 longitude | latitude |   city   | countrycode 
-----------+----------+----------+-------------
 -1.407848 | 51.59119 | Charlton | GB
(1 row)
```

Não se preocupe, há uma maneira fácil de obter o caminho em direção a uma propriedade específica. Na parte a seguir, você aprenderá como.

Você precisará editar uma consulta, portanto, primeiro vamos abrir um editor.

No Windows: use o **Bloco de Notas**

No Mac: instale qualquer aplicativo Editor de texto de sua escolha e abra-o.

Copie a seguinte instrução no editor de texto:

```sql
select your_attribute_path_here
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

Volte para a interface do usuário do Adobe Experience Platform (deve ser aberta no navegador) ou navegue até [Adobe Experience Platform](https://experience.adobe.com/platform).

Selecione **Esquemas**, digite `Demo System - Event Schema for Website` no campo **pesquisa** e clique para abrir o esquema `Demo System - Event Schema for Website (Global v1.1) Schema`.

![browse-schema.png](./images/browseschema.png)

Explore o modelo XDM do **Sistema de demonstração - Esquema de evento do site (Global v1.1)** clicando em um objeto. Expanda a árvore para **placecontext**, **geo** e **schema**. Ao selecionar o atributo real **longitude**, você verá o caminho completo na caixa vermelha destacada. Para copiar o caminho do atributo, clique no ícone de caminho de cópia.

![explorar-esquema-para-caminho.png](./images/exploreschemaforpath.png)

Alterne para o bloco de notas/colchetes e remova **seu_caminho_de_atributo_aqui** da primeira linha. Posicione o cursor depois de **selecionar** na primeira linha e cole (CTRL-V).

![explorar-esquema-para-caminho.png](./images/exploreschemaforpath1.png)

Copie a instrução modificada e cole-a no prompt em sua **interface de linha de comando do PSQL** e pressione Enter.

O resultado deve ficar assim:

```text
tech-insiders:all=> select placeContext.geo._schema.longitude
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
 longitude 
-----------
 -1.407848
(1 row)
```

Próxima Etapa: [5.1.4 Consultas, consultas, consultas... e análise de churn](./ex4.md)

[Voltar ao módulo 5.1](./query-service.md)

[Voltar a todos os módulos](../../../overview.md)
