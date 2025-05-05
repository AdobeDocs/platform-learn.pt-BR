---
title: Serviço de consulta - API do serviço de consulta
description: Serviço de consulta - API do serviço de consulta
kt: 5342
doc-type: tutorial
exl-id: d356f7e2-523b-41a2-9cc6-1ea2a028c3a7
source-git-commit: c49b41e1b033573dbebc9ced3a3f4071bf94d04e
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 2%

---

# 5.1.8 API do serviço de consulta

## Objetivo

- Use a API do Serviço de consulta para gerenciar modelos e agendamentos de consulta

## Contexto

Neste exercício, você executará chamadas de API para gerenciar modelos de consulta e agendamentos de consulta usando uma coleção do Postman. Você definirá modelos de consulta, executará consultas regulares e consultas CTAS. Uma consulta **CTAS** (criar tabela como consulta seleção) armazena seu conjunto de resultados em um conjunto de dados explícito. Embora as consultas regulares sejam armazenadas em um conjunto de dados implícito (ou gerado pelo sistema), normalmente é exportado em formato de arquivo parquet.

## Documentação

- [Ajuda do Adobe Experience Platform Query Service](https://experienceleague.adobe.com/docs/experience-platform/query/api/getting-started.html?lang=pt-BR)
- [API de Serviço de Consulta](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml)

## API do serviço de consulta

A API do Serviço de consulta permite gerenciar consultas não interativas no data lake da Adobe Experience Platform.

Não interativo significa que uma solicitação para executar uma consulta não resultará em uma resposta imediata. A consulta será processada e seu conjunto de resultados será armazenado em um conjunto de dados implícito ou explícito (CTAS: create table as select).

## Exemplo de consulta

Como exemplo de consulta, você usará a primeira consulta listada em [4.3 - Consultas, consultas, consultas... e análise de churn](./ex3.md):

Quantas visualizações de produto temos diariamente?

**SQL**

```sql
select date_format( timestamp , 'yyyy-MM-dd') AS Day,
       count(*) AS productViews
from   demo_system_event_dataset_for_website_global_v1_1
where  --aepTenantId--.demoEnvironment.brandName IN ('Citi Signal')
and eventType = 'commerce.productViews'
group by Day
limit 10;
```

## Consultas

>[!IMPORTANT]
>
>Se você for um funcionário da Adobe, siga as instruções aqui para usar o [PostBuster](./../../../postbuster.md).

Abra o Postman no computador. Como parte do Módulo 2.1, você criou um ambiente do Postman e importou uma coleção do Postman. Siga as instruções no [Exercício 2.1.3](./../../../modules/rtcdp-b2c/module2.1/ex3.md) caso ainda não tenha feito isso.

Como parte da coleção do Postman que você importou, você verá uma pasta **3. Serviço de Consulta**. Se você não vir esta pasta, baixe novamente a [coleção do Postman](./../../../assets/postman/postman_profile.zip) e importe novamente essa coleção no Postman, conforme instruído no [Exercício 2.1.3](./../../../modules/rtcdp-b2c/module2.1/ex3.md).

![QS](./images/pm3.png)

>[!NOTE]
>
>Neste momento, somente a pasta **1. Consultas** contêm solicitações. Outras solicitações serão adicionadas em um estágio de camada.

Abra essa pasta e conheça as chamadas da API do Serviço de consulta para executar, monitorar e baixar o conjunto de resultados da consulta.

Uma chamada POST para [/query/queries] com a seguinte carga disparará a execução de nossa query;

### Criar consulta

Clique na solicitação denominada **1.1 QS - Criar consulta** e vá para **Cabeçalhos**. Você verá isto:

![Segmentação](./images/s1_call.png)

Vamos focalizar neste campo de cabeçalho:

| Chave | Valor |
| ----------- | ----------- |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>É necessário especificar o nome da sandbox da Adobe Experience Platform que você está usando. O campo de cabeçalho **x-sandbox-name** deve ser `--aepSandboxName--`.

Vá para a seção **Corpo** desta solicitação. No **Corpo** desta solicitação, você verá o seguinte:

![Segmentação](./images/s1_bodydtl.png)

```sql
{
    "name" : "ldap - QS API demo - Citi Signal - Product Views Per Day",
	"description": "ldap - QS API demo - Citi Signal - Product Views Per Day",
	"dbName": "--aepSandboxName--:all",
	"sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where --aepTenantId--.demoEnvironment.brandName IN ('Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10"
}
```

Atenção: atualize a variável **name** na solicitação abaixo substituindo **ldap** pelo seu **específico—aepUserLdap—**.

Depois de adicionar o **ldap** específico, o Corpo deve ser semelhante a:

```json
{
    "name" : "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
	"description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
	"dbName": "tech-insiders:all",
	"sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10"
}
```

>[!NOTE]
>
>A chave **dbName** no corpo JSON acima se refere à sandbox usada na instância do Adobe Experience Platform. Se você estiver usando a sandbox PROD, o dbName deverá ser **prod:all**, se você usar outra sandbox, como por exemplo **tech-insiders**, o dbName deverá ser igual a **tech-insiders:all**.

Em seguida, clique no botão azul **Enviar** para criar o segmento e exibir os resultados.

![Segmentação](./images/s1_bodydtl_results.png)

Quando a solicitação POST for bem-sucedida, retornará a seguinte resposta:

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "module7:all",
        "sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
        "name": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
        "description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day"
    },
    "clientId": "5a143b5ae4aa4631a1f3b09cd051333f",
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "8f0d7f25-f7aa-493b-9792-290f884a7e5b",
    "elapsedTime": 0,
    "updated": "2021-01-20T13:23:13.951Z",
    "client": "API",
    "userId": "A3392DB95FFF08EE0A495E87@techacct.adobe.com",
    "created": "2021-01-20T13:23:13.951Z",
    "_links": {
        "self": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

O **estado** atual da consulta é **ENVIADO**. Uma vez executado, seu estado será **SUCCESS**.

Você também pode pesquisar consultas enviadas por meio da interface do Adobe Experience Platform, abrir o [Adobe Experience Platform](https://experience.adobe.com/#/@experienceplatform/platform/home), navegar até as **Consultas**, acessar o **Log** e selecionar sua consulta:

![Segmentação](./images/s1_bodydtl_results_qs.png)

### Obter consultas

Clique na solicitação chamada **1.2 QS - Obter consultas** e vá para **Cabeçalhos**. Você verá isto:

![Segmentação](./images/s2_call.png)

Vamos focalizar neste campo de cabeçalho:

| Chave | Valor |
| ----------- | ----------- |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>É necessário especificar o nome da sandbox da Adobe Experience Platform que você está usando. O campo de cabeçalho **x-sandbox-name** deve ser `--aepSandboxName--`.

Ir para **Params**. Você verá isto:

![Segmentação](./images/s2_call_p.png)

O parâmetro **orderby** permite especificar uma ordem de classificação com base na propriedade **created**. Observe o sinal **&#39;-&#39;** antes de criado, o que significa que a ordem na qual a lista de consultas é retornada usará sua data de criação na ordem **decrescente**. Sua consulta deve estar no topo da lista.

Em seguida, clique no botão azul **Enviar** para criar o segmento e exibir os resultados.

![Segmentação](./images/s2_bodydtl_results.png)

Quando bem-sucedida, a solicitação retornará uma resposta semelhante à abaixo. O **estado** da resposta pode ser **ENVIADO**, **EM_ANDAMENTO** ou **SUCESSO**. Pode levar vários minutos para que a consulta tenha um estado **SUCCESS**. Você pode repetir o envio desta solicitação várias vezes até ver o estado **SUCCESS**.

```json
{
    "queries": [
        {
            "isInsertInto": false,
            "sessionType": "HTTP_SESSION",
            "request": {
                "dbName": "tech-insiders:all",
                "sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
                "name": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
                "description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day"
            },
            "computeMetrics": null,
            "clientId": "b7d8a1fc396242889bb31dc83644e91d",
            "state": "IN_PROGRESS",
            "rowCount": 0,
            "isService": false,
            "errors": [],
            "isCTAS": false,
            "version": 1,
            "id": "a535234e-dc0c-42ea-bcad-eb09c5997d76",
            "elapsedTime": 8088,
            "updated": "2024-12-04T14:17:10.627Z",
            "client": "API",
            "effectiveSQL": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
            "userId": "8CD31E54673C49EE0A495E05@techacct.adobe.com",
            "isParentLevel": true,
            "created": "2024-12-04T14:14:22.637Z",
                "version": 1,
    "_links": {
        "next": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries?orderby=-created&start=2024-11-22T00:32:04.505Z"
        },
        "prev": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries?orderby=-created&start=2024-12-04T14:14:22.637Z&isPrevLink=true"
        }
    }
}
```

Quando o estado for **SUCCESS**, continue com a próxima solicitação.

### Obter Status da Consulta

Clique na solicitação chamada **1.3 QS - Obter Status da Consulta** e vá para **Cabeçalhos**. Você verá isto:

![Segmentação](./images/s3_call.png)

Vamos focalizar neste campo de cabeçalho:

| Chave | Valor |
| ----------- | ----------- |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>É necessário especificar o nome da sandbox da Adobe Experience Platform que você está usando. O campo de cabeçalho **x-sandbox-name** deve ser `--aepSandboxName--`.

Em seguida, clique no botão azul **Enviar** para criar o segmento e exibir os resultados.

![Segmentação](./images/s3_bodydtl_results.png)

Quando bem-sucedida, a solicitação retornará uma resposta semelhante à abaixo.

```json
{
    "isInsertInto": false,
    "sessionType": "HTTP_SESSION",
    "request": {
        "dbName": "tech-insiders:all",
        "sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
        "name": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
        "description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day"
    },
    "computeMetrics": {
        "executorVMSeconds": 138,
        "clusterCpuSeconds": 3312,
        "clusterVMHours": 0.07666666805744171,
        "driverVMSeconds": 138,
        "clusterVMSeconds": 276
    },
    "clientId": "b7d8a1fc396242889bb31dc83644e91d",
    "state": "SUCCESS",
    "rowCount": 1,
    "isService": false,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "a535234e-dc0c-42ea-bcad-eb09c5997d76",
    "elapsedTime": 199219,
    "updated": "2024-12-04T14:17:41.856Z",
    "client": "API",
    "effectiveSQL": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
    "userId": "8CD31E54673C49EE0A495E05@techacct.adobe.com",
    "isParentLevel": true,
    "created": "2024-12-04T14:14:22.637Z",
    "_links": {
        "self": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/a535234e-dc0c-42ea-bcad-eb09c5997d76",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/a535234e-dc0c-42ea-bcad-eb09c5997d76",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "referenced_datasets": [
            {
                "id": "672a10b1074ceb2af0aa7034",
                "href": "https://platform-va7.adobe.io/data/foundation/catalog/dataSets/672a10b1074ceb2af0aa7034"
            }
        ]
    }
}
```

Quando uma consulta atingir o estado de **SUCCESS**, a resposta também indicará o número de linhas recuperadas pela consulta por meio da propriedade **rowCount**. No nosso exemplo, 10 linhas são retornadas pela query. Vamos ver na próxima seção como podemos recuperar as 10 linhas.

### Recuperar resultado da consulta

A resposta **SUCCESS** acima inclui uma propriedade **referenced_datasets**, que aponta para o conjunto de dados implícito que armazena o resultado da consulta. Para obter acesso ao resultado, usamos sua propriedade **href** ou **id**.

Clique na solicitação chamada **1.4 QS - Obter Resultado da Consulta** e vá para **Cabeçalhos**. Você verá isto:

![Segmentação](./images/s4_call.png)

Vamos focalizar neste campo de cabeçalho:

| Chave | Valor |
| ----------- | ----------- |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>É necessário especificar o nome da sandbox da Adobe Experience Platform que você está usando. O campo de cabeçalho **x-sandbox-name** deve ser `--aepSandboxName--`.

Em seguida, clique no botão azul **Enviar** para criar o segmento e exibir os resultados.

![Segmentação](./images/s4_bodydtl_results.png)

A resposta dessa solicitação apontará para os arquivos do conjunto de dados:

```json
{
    "672a10b1074ceb2af0aa7034": {
        "name": "Demo System - Event Dataset for Website (Global v1.1)",
        "description": "Demo System - Event Dataset for Website (Global v1.1)",
        "enableErrorDiagnostics": false,
        "tags": {
            "adobe/siphon/partition/definition": [
                "day(timestamp, _ACP_DATE)",
                "identity(_ACP_BATCHID)"
            ],
            "adobe/siphon/meta": [
                "acpBufferedFlag::false"
            ],
            "aep/siphon/partitions": [
                "_ACP_DATE",
                "_ACP_BATCHID"
            ],
            "acp_granular_plugin_validation_flags": [
                "identity:enabled",
                "profile:disabled"
            ],
            "adobe/pqs/table": [
                "demo_system_event_dataset_for_website_global_v1_1"
            ],
            "acp_granular_validation_flags": [
                "requiredFieldCheck:enabled"
            ],
            "aep/siphon/cleanup/trash/timestamp": [
                "1733302532212"
            ],
            "acp_validationContext": [
                "enabled"
            ],
            "adobe/siphon/table/format": [
                "delta"
            ],
            "unifiedProfile": [
                "enabled:true",
                "enabledAt:2024-11-05 12:33:59"
            ],
            "aep/siphon/cleanup/meta/timestamp": [
                "1733302532287"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ]
        },
        "state": "ACTIVE",
        "imsOrg": "907075E95BF479EC0A495C73@AdobeOrg",
        "sandboxId": "79e3c8b2-0609-4564-a3c8-b20609a5648c",
        "extensions": {
            "adobe_lakeHouse": {
                "metrics": {
                    "storageSize": 810709,
                    "rowCount": 1141,
                    "asOf": 1732494676514
                }
            },
            "adobe_unifiedProfile": {}
        },
        "version": "1.0.21",
        "created": 1730810034023,
        "updated": 1733302532348,
        "createdClient": "d75039d36ca543c78612f7aac18e6c2b",
        "createdUser": "53FB1E5E66CDC87D0A495FC0@techacct.adobe.com",
        "updatedUser": "acp_foundation_dataTracker@AdobeID",
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "viewId": "672a10b2074ceb2af0aa7035",
        "fileDescription": {
            "format": "parquet"
        },
        "files": "@/dataSetFiles?dataSetId=672a10b1074ceb2af0aa7034",
        "schemaRef": {
            "id": "https://ns.adobe.com/experienceplatform/schemas/d9b88a044ad96154637965a97ed63c7b20bdf2ab3b4f642e",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
}
```

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao módulo 5.1](./query-service.md)

[Voltar a todos os módulos](../../../overview.md)
