---
title: Serviço de consulta - Introdução
description: Serviço de consulta - Introdução
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# 5.1.1 Introdução

## 5.1.1.1 Familiarização com a interface do usuário do Adobe Experience Platform

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--module7sandbox--``. Você pode fazer isso clicando no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. Depois de selecionar a [!UICONTROL sandbox] apropriada, você verá a alteração da tela e agora estará na [!UICONTROL sandbox] dedicada.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/sb1.png)


## 5.1.1.2 Explorar dados na plataforma

Trazer dados de diferentes canais é uma tarefa difícil para qualquer marca. E neste exercício, os clientes do Citi Signal estão se envolvendo com o Citi Signal em seu site, em seu aplicativo móvel, os dados de compra são coletados pelo sistema de ponto de venda do Citi Signal, e eles têm dados de CRM e Fidelidade. O Citi Signal está usando o Adobe Analytics e o Adobe Launch para capturar dados em seu site, no aplicativo móvel e no sistema POS. Portanto, esses dados já estão fluindo para o Adobe Experience Platform. Vamos começar explorando todos os dados para o Citi Signal que já existe no Adobe Experience Platform.

No menu esquerdo, vá para **Conjuntos de dados**.

![emea-website-interaction-dataset.png](./images/emea-website-interaction-dataset.png)

O Citi Signal está transmitindo dados para a Adobe Experience Platform e esses dados estão disponíveis no conjunto de dados `Demo System - Event Dataset for Website (Global v1.1)`. Pesquisar por `Demo System - Event Dataset for Website`.

![emea-callcenter-interaction-dataset.png](./images/emea-website-interaction-dataset1.png)

Os dados de Interação do Callcenter do Citi Signal são capturados no conjunto de dados `Demo System - Event Dataset for Call Center (Global v1.1)`. Pesquisar dados de `Demo System - Event Dataset for Call Center` na caixa de pesquisa. Clique no nome do conjunto de dados para abri-lo.

![emea-callcenter-interaction-dataset.png](./images/emea-callcenter-interaction-dataset.png)

Depois de clicar no conjunto de dados, você terá uma visão geral da atividade do conjunto de dados, como lotes assimilados e com falha.

![preview-interaction-dataset.png](./images/preview-interaction-dataset.png)

Clique em **Visualizar Conjunto de Dados** para ver uma amostra dos dados armazenados no conjunto de dados `Demo System - Event Dataset for Call Center (Global v1.1)`. O painel esquerdo mostra a estrutura do esquema para esse conjunto de dados.

![explorar-interação-dataset.png](./images/explore-interaction-dataset.png)

Clique no botão **Fechar** para fechar a janela **Visualizar Conjunto de Dados**.

## 5.1.1.3 Introdução ao Serviço de consulta

O Serviço de consulta do Adobe Experience Platform é acessado clicando em **Consultas** no menu esquerdo.

![select-queries.png](./images/select-queries.png)

Ao acessar o **Log**, você verá a página Lista de Consultas, que fornece uma lista de todas as consultas executadas nesta organização, com as mais recentes no topo.

![lista-consulta.png](./images/query-list.png)

Clique em qualquer consulta SQL na lista e observe os detalhes fornecidos no painel direito.

![click-sql-query.png](./images/click-sql-query.png)

Você pode rolar a janela para ver a consulta inteira ou clicar no ícone destacado abaixo para copiar a consulta inteira para o bloco de notas. Não é necessário copiar a consulta neste momento.

![click-copy-query.png](./images/click-copy-query.png)

Não é possível ver apenas as consultas que foram executadas, essa interface do usuário permite criar novos conjuntos de dados a partir de consultas. Esses conjuntos de dados podem ser vinculados ao Perfil do cliente em tempo real da Adobe Experience Platform ou podem ser usados como entrada para o Adobe Experience Platform Data Science Workspace.

## 5.1.1.4 Conectar o cliente PSQL ao serviço de consulta

O Serviço de consulta oferece suporte a clientes com um driver para PostgreSQL. Nesta etapa, usaremos o PSQL, uma interface de linha de comando, e o Power BI Tableau. Vamos nos conectar ao PSQL.

Clique em **Credenciais**.

![queries-select-configuration.png](./images/queries-select-configuration.png)

Você verá a tela abaixo. A tela Configuração fornece informações do servidor e credenciais para autenticação no Serviço de consulta. Por enquanto, nos concentraremos no lado direito da tela que contém um comando connect para PSQL. Clique no botão Copiar para copiar o comando para a área de transferência.

![copy-psql-connection.png](./images/copy-psql-connection.png)

Para Windows: abra a linha de comando pressionando a tecla Windows e digitando cmd e clicando no resultado do Prompt de comando.

![open-command-prompt.png](./images/open-command-prompt.png)

Para o macOS: abra o terminal.app por meio da pesquisa em destaque:

![open-terminal-osx.png](./images/open-terminal-osx.png)

Cole o comando connect que você copiou da interface do usuário do Serviço de consulta e pressione Enter na janela de prompt de comando:

Windows:

![comando-prompt-connected.png](./images/command-prompt-connected.png)

MacOS:

![comando-prompt-cole-osx.png](./images/command-prompt-paste-osx.png)

Agora você está conectado ao Serviço de consulta usando PSQL.

Nos próximos exercícios, haverá bastante interação com essa janela. Nos referiremos a ele como sua **interface de linha de comando PSQL**.

Agora você está pronto para começar a enviar consultas.

Próxima Etapa: [5.1.2 Usando o Serviço de Consulta](./ex2.md)

[Voltar ao módulo 5.1](./query-service.md)

[Voltar a todos os módulos](../../../overview.md)
