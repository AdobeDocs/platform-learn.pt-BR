---
title: Conexão com o Data Warehouse
seo-title: Configure a Data Warehouse connection | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Conexão com o Data Warehouse
description: Nesta lição, configuramos uma conexão entre o Adobe Experience Platform e o Data Warehouse corporativo para ativar a Federated Audience Composition.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-configure-a-data-warehouse-connection.jpg
hide: true
source-git-commit: fcfadca95c12d0123cfb221e44909f7e0fa8abab
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# Conexão com o Data Warehouse

Nesta lição, configuramos uma conexão entre o Adobe Experience Platform e o Data Warehouse corporativo para ativar a Federated Audience Composition. Isso permite consultar dados diretamente de depósitos compatíveis sem replicação. Além disso, criamos Esquemas e Modelos de dados com base nas tabelas do Data Warehouse.

Neste laboratório, nos conectamos a uma conta do Snowflake. A Federated Audience Composition oferece suporte a uma lista crescente de conexões de warehouse em nuvem. Consulte a [lista atualizada de integrações](https://experienceleague.adobe.com/pt-br/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"}.


## Etapas

1. Navegue até a seção **DADOS FEDERADOS** no painel esquerdo.
2. No link **Federated Databases**, clique no botão **Add federated database**.
3. Adicione um nome e selecione **Snowflake**.
4. Preencha os detalhes, clique no botão **Testar conexão** e no botão **Implantar funções**.

   ![snowflake-connection-setup](assets/snowflake-connection-setup.png)

   ![snowflake-connection-setup-step2](assets/snowflake-connection-setup-step2.png)

   ![snowflake-connection-setup-step3](assets/snowflake-connection-setup-step3.png)

## Criar um esquema

Para criar esquemas na Composição de público federado, siga estas etapas:

1. Na seção **DADOS FEDERADOS**, clique em **Modelos**.
2. Navegue pela guia **Esquema** e clique no botão **Criar Esquema**.
3. Selecione o banco de dados de origem na lista e clique na guia **Adicionar tabelas**.
4. Selecione as seguintes tabelas:
   - FSI_CRM
   - FSI_CRM_CONSENT_PREFERENCE

   ![criar-esquema](assets/create-schema.png)

   ![tabela-seleção](assets/select-table.png)

Depois de selecionar as tabelas, analise as colunas de cada tabela e selecione a chave primária. Para este exercício, selecionamos **EMAIL** como chave primária em ambas as tabelas.

![criar-esquema](assets/create-schema.png)

![criar-etapa-esquema2](assets/create-schema-step2.png)

## Visualizar dados em um esquema

Para visualizar os dados na tabela representada pelo esquema, navegue até a guia **Dados**.

Clique no link **Calcular** para visualizar o número total de registros.

![visualizar-dados-no-esquema](assets/preview-data-in-schema.png)

## Criar um modelo de dados

Os modelos de dados permitem criar um vínculo entre tabelas. O link pode ser criado entre tabelas no mesmo banco de dados, como tabelas no Snowflake, ou entre tabelas em bancos de dados diferentes, como um link entre uma tabela no Snowflake e uma tabela no Amazon Redshift.

Para criar um modelo de dados na Composição do Audience Federated, siga estas etapas:

1. Na seção **DADOS FEDERADOS**, clique em **Modelos** e em **Modelo de Dados**.
2. Clique no botão **Criar modelo de dados**.
3. Forneça um nome para o modelo de dados.
4. Clique em **Adicionar esquemas** e selecione os esquemas **FSI_CRM** e **FSI_CRM_CONSENT_PREFERENCE**.
5. Crie um link entre essas tabelas clicando em **Criar links**.

Ao criar um link, escolha a cardinalidade aplicável:

- **1-N**: uma ocorrência da tabela de origem pode ter várias ocorrências correspondentes da tabela de destino, mas uma ocorrência da tabela de destino pode ter no máximo uma ocorrência correspondente da tabela de origem.
- **N-1**: uma ocorrência da tabela de destino pode ter várias ocorrências correspondentes da tabela de origem, mas uma ocorrência da tabela de origem pode ter no máximo uma ocorrência correspondente da tabela de destino.
- **1-1**: uma ocorrência da tabela de origem pode ter no máximo uma ocorrência correspondente da tabela de destino.

Veja abaixo uma prévia do link criado para os exercícios em laboratório. O link permite uma associação entre o CRM e as tabelas de consentimento, usando a chave primária de **EMAIL** para executar uma associação.

![visualizar-modelo-de-dados](assets/preview-data-model.png)

Agora, estamos prontos para [criar e público-alvo](audience-creation-exercise.md).
