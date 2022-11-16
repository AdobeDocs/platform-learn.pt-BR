---
title: Serviço de query - API do serviço de query
description: Serviço de query - API do serviço de query
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 6f437bd3-b134-4509-8e32-ad6f7b70608e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 3%

---

# 4.7 API do serviço de consulta

## Objetivo

- Usar a API do Serviço de Consulta para gerenciar modelos de consulta e agendamentos de consulta

## Contexto

Neste exercício, você executará chamadas de API para gerenciar modelos de consulta e agendamentos de consulta usando uma coleção do Postman. Você definirá templates de query, executará queries regulares e queries CTAS. A **CTAS** query (criar tabela como consulta selecionada) armazena seu conjunto de dados explícito. Embora as consultas regulares sejam armazenadas em um conjunto de dados implícito (ou gerado pelo sistema), isso geralmente é exportado no formato de arquivo de parâmetros.

## Documentação

- [Ajuda do Serviço de consulta da Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/query/api/getting-started.html)
- [API do serviço de consulta](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml)

## 4.7.1 API do Serviço de query

A API do Serviço de query permite gerenciar consultas não interativas no lago de dados do Adobe Experience Platform.

Não interativo significa que uma solicitação para executar um query não resultará em uma resposta imediata. O query será processado e seu conjunto de resultados será armazenado em um CTAS implícito ou explícito: criar tabela como selecione) conjunto de dados.

## 4.7.2 Exemplo de consulta

Como exemplo de consulta, você usará a primeira consulta listada em [4.3 - Consultas, consultas, consultas... e análise de churn](./ex3.md):

Quantas visualizações de produtos temos diariamente?

**SQL**

```sql
select date_format( timestamp , 'yyyy-MM-dd') AS Day,
       count(*) AS productViews
from   demo_system_event_dataset_for_website_global_v1_1
where  --aepTenantId--.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal')
and eventType = 'commerce.productViews'
group by Day
limit 10;
```

## 4.7.3 Consultas

Abra o Postman no seu computador. Como parte do Módulo 3, você criou um ambiente Postman e importou uma coleção do Postman. Siga as instruções em [Exercício 3.3.3](./../module3/ex3.md) caso ainda não tenha feito isso.

Como parte da coleção do Postman importada, você verá uma pasta **3. Serviço de query**. Se você não vir esta pasta, baixe novamente o [Coleção Postman](../../assets/postman/postman_profile.zip) e reimporte essa coleção no Postman, conforme instruído em [Exercício 3.3.3](./../module3/ex3.md).

![QS](./images/pm3.png)

>[!NOTE]
>
>Nesse momento, somente a pasta **1. Queries** contém solicitações. Outras solicitações serão adicionadas em um estágio de camada.

Abra essa pasta e conheça as chamadas da API do Serviço de query para executar, monitorar e baixar o conjunto de resultados da consulta.

Uma chamada de POST para [/query/queries] com a carga a seguir acionará a execução do nosso query;

### 4.7.3.1 Criar consulta

Clique na solicitação nomeada **1.1 QS - Criar consulta** e ir para **Cabeçalhos**. Você verá isso:

![Segmentação](./images/s1_call.png)

Vamos focar neste campo de cabeçalho:

| Chave | Valor |
| ----------- | ----------- |
| x-sandbox-name | `--module7sandbox--` |

>[!NOTE]
>
>Você precisa especificar o nome da sandbox do Adobe Experience Platform que está usando. O campo de cabeçalho **x-sandbox-name** deve ser `--module7sandbox--`.

Vá para a **Corpo** seção desta solicitação. No **Corpo** dessa solicitação, você verá o seguinte:

![Segmentação](./images/s1_bodydtl.png)

```sql
{
    "name" : "ldap - QS API demo - Citi Signal - Product Views Per Day",
	"description": "ldap - QS API demo - Citi Signal - Product Views Per Day",
	"dbName": "module7:all",
	"sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10"
}
```

Atenção: atualize a variável **name** na solicitação abaixo, substituindo **ldap** com seu **ldap**.

Depois de adicionar o **ldap** O corpo deve ser semelhante a este:

```json
{
    "name" : "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
	"description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
	"dbName": "module7:all",
	"sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10"
}
```

>[!NOTE]
>
>A chave **dbName** no corpo JSON acima refere-se à sandbox usada na instância do Adobe Experience Platform. Se você estiver usando a sandbox PROD, o dbName deve ser **prod:all**, se você usar outra sandbox como, por exemplo, **módulo7**, dbName deve ser igual a **módulo7:all**.

Em seguida, clique em azul **Enviar** para criar o segmento e exibir os resultados disso.

![Segmentação](./images/s1_bodydtl_results.png)

Quando bem-sucedida, a solicitação de POST retornará a seguinte resposta:

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

O atual **state** do query é **ENVIADO**, uma vez executado, seu estado se tornará **SUCESSO**.

Também é possível pesquisar consultas enviadas por meio da interface do usuário do Adobe Experience Platform, abrir [Adobe Experience Platform](https://experience.adobe.com/#/@experienceplatform/platform/home), navegue até **Queries** para **Log** e selecione seu query:

![Segmentação](./images/s1_bodydtl_results_qs.png)

### 4.7.3.2 Obter Consultas

Clique na solicitação nomeada **1.2 QS - Obter consultas** e ir para **Cabeçalhos**. Você verá isso:

![Segmentação](./images/s2_call.png)

Vamos focar neste campo de cabeçalho:

| Chave | Valor |
| ----------- | ----------- |
| x-sandbox-name | `--module7sandbox--` |

>[!NOTE]
>
>Você precisa especificar o nome da sandbox do Adobe Experience Platform que está usando. O campo de cabeçalho **x-sandbox-name** deve ser `--module7sandbox--`.

Ir para **Params**. Você verá isso:

![Segmentação](./images/s2_call_p.png)

O **orderby** permite especificar uma ordem de classificação com base no **criado** propriedade. Observe que **&#39;-&#39;** fazer logon na frente da criação, o que significa que a ordem em que a lista de queries é retornada usará a data de criação em **decrescente** ordem. Seu query deve estar no topo da lista.

Em seguida, clique em azul **Enviar** para criar o segmento e exibir os resultados disso.

![Segmentação](./images/s2_bodydtl_results.png)

Quando bem-sucedida, a solicitação retornará uma resposta semelhante à abaixo. O **state** da resposta pode ser **ENVIADO**, **IN_PROGRESS** ou **SUCESSO**. Pode levar vários minutos até que o query tenha uma **SUCESSO** estado. É possível repetir o envio dessa solicitação várias vezes, até que você veja a variável **SUCESSO** estado.

```json
{
    "queries": [
        {
            "isInsertInto": false,
            "request": {
                "dbName": "module7:all",
                "sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
                "name": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
                "description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day"
            },
            "clientId": "5a143b5ae4aa4631a1f3b09cd051333f",
            "state": "SUCCESS",
            "rowCount": 1,
            "errors": [],
            "isCTAS": false,
            "version": 1,
            "id": "8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "elapsedTime": 217481,
            "updated": "2021-01-20T13:26:51.432Z",
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
                "referenced_datasets": [
                    {
                        "id": "60080ace62c49a19490c5870",
                        "href": "https://platform-va7.adobe.io/data/foundation/catalog/dataSets/60080ace62c49a19490c5870"
                    }
                ]
            }
        }
     ]
    },
    "version": 1
}
```

Quando o estado for **SUCESSO**, continue com a próxima solicitação.

### 4.7.3.3 Obter Status de Consulta

Clique na solicitação nomeada **1.3 QS - Obter status de consulta** e ir para **Cabeçalhos**. Você verá isso:

![Segmentação](./images/s3_call.png)

Vamos focar neste campo de cabeçalho:

| Chave | Valor |
| ----------- | ----------- |
| x-sandbox-name | `--module7sandbox--` |

>[!NOTE]
>
>Você precisa especificar o nome da sandbox do Adobe Experience Platform que está usando. O campo de cabeçalho **x-sandbox-name** deve ser `--module7sandbox--`.

Em seguida, clique em azul **Enviar** para criar o segmento e exibir os resultados disso.

![Segmentação](./images/s3_bodydtl_results.png)

Quando bem-sucedida, a solicitação retornará uma resposta semelhante à abaixo.

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
    "state": "SUCCESS",
    "rowCount": 1,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "8f0d7f25-f7aa-493b-9792-290f884a7e5b",
    "elapsedTime": 217481,
    "updated": "2021-01-20T13:26:51.432Z",
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
        "referenced_datasets": [
            {
                "id": "60080ace62c49a19490c5870",
                "href": "https://platform-va7.adobe.io/data/foundation/catalog/dataSets/60080ace62c49a19490c5870"
            }
        ]
    }
}
```

Quando um query atinge o estado de **SUCESSO**, a resposta também indicará o número de linhas recuperadas pelo query por meio do **rowCount** propriedade. No nosso exemplo, 10 linhas são retornadas pelo query. Veja na próxima seção como podemos recuperar as 10 linhas.

### 4.7.3.4 Recuperar Resultado da Consulta

O **SUCESSO** a resposta acima inclui uma **referenced_datasets** , que aponta para o conjunto de dados implícito que armazena o resultado do query. Para obter acesso ao resultado, usamos **href** ou **id** propriedade.

Clique na solicitação nomeada **1.4 QS - Obter resultado da consulta** e ir para **Cabeçalhos**. Você verá isso:

![Segmentação](./images/s4_call.png)

Vamos focar neste campo de cabeçalho:

| Chave | Valor |
| ----------- | ----------- |
| x-sandbox-name | `--module7sandbox--` |

>[!NOTE]
>
>Você precisa especificar o nome da sandbox do Adobe Experience Platform que está usando. O campo de cabeçalho **x-sandbox-name** deve ser `--module7sandbox--`.

Em seguida, clique em azul **Enviar** para criar o segmento e exibir os resultados disso.

![Segmentação](./images/s4_bodydtl_results.png)

A resposta dessa solicitação apontará para os arquivos do conjunto de dados:

```json
{
    "60080ace62c49a19490c5870": {
        "name": "Demo System - Event Dataset for Website (Global v1.1)",
        "description": "Demo System - Event Dataset for Website (Global v1.1)",
        "enableErrorDiagnostics": false,
        "tags": {
            "adobe/siphon/partition/definition": [
                "day(timestamp, _ACP_DATE)",
                "identity(_ACP_BATCHID)"
            ],
            "aep/siphon/partitions": [
                "_ACP_DATE",
                "_ACP_BATCHID"
            ],
            "acp_granular_plugin_validation_flags": [
                "identity:enabled",
                "profile:enabled"
            ],
            "adobe/siphon/buffered-promotion-recency": [
                "live"
            ],
            "adobe/siphon/use-buffered-promotion": [
                "true"
            ],
            "adobe/pqs/table": [
                "demo_system_event_dataset_for_website_global_v1_1"
            ],
            "aep/siphon/expire-snapshot-timestamp": [
                "1611141272703"
            ],
            "acp_granular_validation_flags": [
                "requiredFieldCheck:enabled"
            ],
            "acp_validationContext": [
                "enabled"
            ],
            "adobe/siphon/table/format": [
                "iceberg"
            ],
            "unifiedProfile": [
                "enabled:true",
                "enabledAt:2021-01-20 10:49:51"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ]
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "imsOrg": "907075E95BF479EC0A495C73@AdobeOrg",
        "sandboxId": "62cd9f38-8529-4b05-8d9f-388529db0540",
        "lastBatchId": "01EWFQZ15XRNNB1FPKPW5ETRVP",
        "lastBatchStatus": "success",
        "lastSuccessfulBatch": "01EWFQZ15XRNNB1FPKPW5ETRVP",
        "version": "1.0.6",
        "created": 1611139790698,
        "updated": 1611149266031,
        "createdClient": "750e24ee855b4ac18ccc4f4817f96ee1",
        "createdUser": "3A260B485E909A170A495E76@techacct.adobe.com",
        "updatedUser": "acp_foundation_dataTracker@AdobeID",
        "viewId": "60080ace62c49a19490c5871",
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
        "files": "@/dataSets/60080ace62c49a19490c5870/views/60080ace62c49a19490c5871/files",
        "schemaMetadata": {
            "delta": [],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/experienceplatform/schemas/d9b88a044ad96154637965a97ed63c7b20bdf2ab3b4f642e",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
}
```

>[!NOTE]
>
>Mais exercícios serão adicionados em breve para ajudá-lo a interagir com a API do Serviço de query.

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao Módulo 4](./query-service.md)

[Voltar para todos os módulos](../../overview.md)
