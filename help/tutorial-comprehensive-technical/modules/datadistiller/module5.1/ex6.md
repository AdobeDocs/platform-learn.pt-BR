---
title: Serviço de consulta - Explorar o conjunto de dados com o Power BI
description: Serviço de consulta - Explorar o conjunto de dados com o Power BI
kt: 5342
doc-type: tutorial
exl-id: c27abd0e-e563-4702-a243-1aec84ce6116
source-git-commit: b53ee64ae8438b8f48f842ed1f44ee7ef3e813fc
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# 5.1.6 Serviço de consulta e Power BI

Abra o Microsoft Power BI Desktop.

![início-power-bi.png](./images/start-power-bi.png)

Clique em **Obter Dados**.

![power-bi-get-data.png](./images/power-bi-get-data.png)

Pesquise por **postgres** (1), selecione **Postgres** (2) na lista e **Connect** (3).

![power-bi-connect-progress.png](./images/power-bi-connect-progress.png)

Vá para o Adobe Experience Platform, para **Consultas** e para **Credenciais**.

![query-service-credentials.png](./images/query-service-credentials.png)

Na página **Credenciais** do Adobe Experience Platform, copie o **Host** e cole-o no campo **Servidor**, copie o **Banco de Dados** e cole-o no campo **Banco de Dados** do Power BI e clique em OK (2).

>[!IMPORTANT]
>
>Certifique-se de incluir a porta **:80** no final do valor Server porque o Serviço de Consulta não usa atualmente a porta PostgreSQL padrão de 5432.

![power-bi-connect-server.png](./images/power-bi-connect-server.png)

Na próxima caixa de diálogo, preencha o Nome de usuário e a Senha com o Nome de usuário e a Senha encontrados nas **Credenciais** de Consultas no Adobe Experience Platform.

![query-service-credentials.png](./images/query-service-credentials.png)

Na caixa de diálogo Navegador, coloque seu **LDAP** no campo de pesquisa (1) para localizar seus conjuntos de dados CTAS e marque a caixa ao lado de cada (2). Em seguida, clique em Carregar (3).

![power-bi-load-churn-data.png](./images/power-bi-load-churn-data.png)

Verifique se a guia (1) **Relatório** está selecionada.

![power-bi-report-tab.png](./images/power-bi-report-tab.png)

Selecione o mapa (1) e, depois de adicioná-lo à tela de relatórios, aumente o mapa (2).

![power-bi-select-map.png](./images/power-bi-select-map.png)

Em seguida, precisamos definir as medidas e as dimensões. Para isso, arraste os campos da seção **campos** para os espaços reservados correspondentes (localizados em **visualizações**), conforme indicado abaixo:

![power-bi-drag-lat-lon.png](./images/power-bi-drag-lat-lon.png)

Como medida, usaremos uma contagem de **customerId**. Arraste o campo **crmid** da seção **fields** para o espaço reservado **Size**:

![power-bi-drag-crmid.png](./images/power-bi-drag-crmid.png)

Finalmente, para fazer uma análise de **callTopic**, vamos arrastar o campo **callTopic** para o espaço reservado de **filtros de nível de página** (talvez seja necessário rolar a tela na seção **visualizações**);

![power-bi-drag-calltopic.png](./images/power-bi-drag-calltopic.png)

Selecione/desmarque **callTopics** para investigar:

![power-bi-report-select-calltopic.png](./images/power-bi-report-select-calltopic.png)

Você terminou este exercício agora.

Próxima Etapa: [5.1.8 API de Serviço de Consulta](./ex8.md)

[Voltar ao módulo 5.1](./query-service.md)

[Voltar a todos os módulos](../../../overview.md)
