---
title: Serviço de consulta - Explorar o conjunto de dados com o Power BI
description: Serviço de consulta - Explorar o conjunto de dados com o Power BI
kt: 5342
doc-type: tutorial
exl-id: c27abd0e-e563-4702-a243-1aec84ce6116
source-git-commit: f843c50af04d744a7d769f320b5b55a5e6d25ffd
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# 5.1.6 Serviço de consulta e Power BI

Abra o Microsoft Power BI Desktop.

![início-power-bi.png](./images/startpowerbi.png)

Clique em **Obter Dados**.

![power-bi-get-data.png](./images/powerbigetdata.png)

Pesquise por **postgres** (1), selecione **Postgres** (2) na lista e **Connect** (3).

![power-bi-connect-progress.png](./images/powerbiconnectprogress.png)

Vá para o Adobe Experience Platform, para **Consultas** e para **Credenciais**.

![query-service-credentials.png](./images/queryservicecredentials.png)

Na página **Credenciais** do Adobe Experience Platform, copie o **Host** e cole-o no campo **Servidor**, copie o **Banco de Dados** e cole-o no campo **Banco de Dados** do Power BI e clique em OK (2).

>[!IMPORTANT]
>
>Certifique-se de incluir a porta **:80** no final do valor Server porque o Serviço de Consulta não usa atualmente a porta PostgreSQL padrão de 5432.

![power-bi-connect-server.png](./images/powerbiconnectserver.png)

Na próxima caixa de diálogo, preencha o Nome de usuário e a Senha com o Nome de usuário e a Senha encontrados nas **Credenciais** de Consultas no Adobe Experience Platform.

![query-service-credentials.png](./images/queryservicecredentials.png)

Na caixa de diálogo Navegador, coloque seu **LDAP** no campo de pesquisa (1) para localizar seus conjuntos de dados CTAS e marque a caixa ao lado de cada (2). Em seguida, clique em Carregar (3).

![power-bi-load-churn-data.png](./images/powerbiloadchurndata.png)

Verifique se a guia (1) **Relatório** está selecionada.

![power-bi-report-tab.png](./images/powerbireporttab.png)

Selecione o mapa (1) e, depois de adicioná-lo à tela de relatórios, aumente o mapa (2).

![power-bi-select-map.png](./images/powerbiselectmap.png)

Em seguida, precisamos definir as medidas e as dimensões. Para isso, arraste os campos da seção **campos** para os espaços reservados correspondentes (localizados em **visualizações**), conforme indicado abaixo:

![power-bi-drag-lat-lon.png](./images/powerbidraglatlon.png)

Como medida, usaremos uma contagem de **customerId**. Arraste o campo **crmid** da seção **fields** para o espaço reservado **Size**:

![power-bi-drag-crmid.png](./images/powerbidragcrmid.png)

Finalmente, para fazer uma análise de **callTopic**, vamos arrastar o campo **callTopic** para o espaço reservado de **filtros de nível de página** (talvez seja necessário rolar a tela na seção **visualizações**);

![power-bi-drag-calltopic.png](./images/powerbidragcalltopic.png)

Selecione/desmarque **callTopics** para investigar:

![power-bi-report-select-calltopic.png](./images/powerbireportselectcalltopic.png)

Você terminou este exercício agora.

Próxima Etapa: [5.1.8 API de Serviço de Consulta](./ex8.md)

[Voltar ao módulo 5.1](./query-service.md)

[Voltar a todos os módulos](../../../overview.md)
