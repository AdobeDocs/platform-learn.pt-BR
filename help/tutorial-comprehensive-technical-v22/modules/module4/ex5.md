---
title: Serviço de query - Explore o conjunto de dados com o Power BI
description: Serviço de query - Explore o conjunto de dados com o Power BI
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 0f9e6719-056b-4858-8c86-04b3beaa950e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# 4.5 Serviço e Power BI de query

Abra o Microsoft Power BI Desktop.

![start-power-bi.png](./images/start-power-bi.png)

Clique em **Obter dados**.

![power-bi-get-data.png](./images/power-bi-get-data.png)

Procurar por **pôsteres** (1), selecione **Postgres** (2) da lista e **Connect** (3)

![power-bi-connect-progress.png](./images/power-bi-connect-progress.png)

Vá para Adobe Experience Platform, para **Queries** e **Credenciais**.

![query-service-credentials.png](./images/query-service-credentials.png)

No **Credenciais** no Adobe Experience Platform, copie a **Host** e cole-o no **Servidor** e copie o **Banco de dados** e cole-o no **Banco de dados** no Power BI, clique em OK (2).

>[!IMPORTANT]
>
>Certifique-se de incluir a porta **80** no final do valor do Servidor porque o Serviço de Consulta não usa atualmente a porta PostgreSQL padrão de 5432.

![power-bi-connect-server.png](./images/power-bi-connect-server.png)

Na próxima caixa de diálogo, preencha o Nome de usuário e a Senha com seu Nome de usuário e Senha encontrados no **Credenciais** de Consultas no Adobe Experience Platform.

![query-service-credentials.png](./images/query-service-credentials.png)

Na caixa de diálogo Navegador, coloque **LDAP** no campo de pesquisa (1) para localizar seus conjuntos de dados do CTAS e marcar a caixa ao lado de cada (2). Em seguida, clique em Carregar (3).

![power-bi-load-churn-data.png](./images/power-bi-load-churn-data.png)

Certifique-se de que o **Relatório** (1) está selecionada.

![power-bi-report-tab.png](./images/power-bi-report-tab.png)

Selecione o mapa (1) e, depois que ele for adicionado à tela de relatórios, amplie o mapa (2).

![power-bi-select-map.png](./images/power-bi-select-map.png)

Em seguida, precisamos definir as medidas e as dimensões. Para isso, arraste os campos do **campos** seção sobre os espaços reservados correspondentes (localizados em **visualizações**) conforme indicado abaixo:

![power-bi-arrastar-lat-lon.png](./images/power-bi-drag-lat-lon.png)

Como medida, usaremos uma contagem de **customerId**. Arraste o **crmid** do campo **campos** na seção **Tamanho** espaço reservado:

![power-bi-arrastar-crmid.png](./images/power-bi-drag-crmid.png)

Finalmente, para fazer algumas **callTopic** , vamos arrastar a **callTopic** no campo para **Filtros de nível de página** espaço reservado (talvez seja necessário rolar no **visualizações** seção);

![power-bi-arrastar-calltopic.png](./images/power-bi-drag-calltopic.png)

Selecionar/desmarcar **callTopics** para investigar:

![power-bi-report-select-calltopic.png](./images/power-bi-report-select-calltopic.png)

Você já terminou este exercício.

Próxima etapa: [4.7 API do serviço de consulta](./ex7.md)

[Voltar ao Módulo 4](./query-service.md)

[Voltar para todos os módulos](../../overview.md)
