---
title: Configuração da sua base de dados relacional
description: Configuração da sua base de dados relacional
kt: 5342
doc-type: tutorial
exl-id: 532e5f2c-971f-488f-bef4-3a8141408cc8
source-git-commit: bf3bebfa3bd79829da5352e950aed3f4ef5bf6d1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 6%

---

# 3.8.1 Configuração da sua base de dados relacional

Faça login no Adobe Journey Optimizer em [https://experience.adobe.com](https://experience.adobe.com). Clique em **Journey Optimizer**.

![OC do AJO](./images/aechome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`.

![OC do AJO](./images/ajohome.png)

## 3.8.1.1 Configuração de esquema baseada em relação

Um esquema com base relacional é a definição formal do modelo de dados com base em modelo.

Especifica:

- O conjunto de tabelas
- As colunas em cada tabela
- As restrições
- As relações entre tabelas

Organizar esquemas ou tabelas em um modelo de dados baseado em modelo é estruturar seus dados em várias tabelas. Certifique-se de que cada tabela armazene um tipo de entidade/esquema.

Ao assimilar dados no para uso com as Campanhas orquestradas da Adobe Journey Optimizer, as seguintes fontes estão disponíveis:

- Amazon S3
- Google Cloud Storage
- SFTP
- Snowflake
- Google BigQuery
- Data Landing Zone
- Azure Databricks
- Upload de arquivo local

A primeira etapa deste exercício é a configuração dos esquemas XDM com base relacional. No menu esquerdo, role até **Gerenciamento de dados** e selecione **Esquemas**. Clique em **+ Criar esquema**.

![OC do AJO](./images/ajoocdata1.png)

Selecione **Relacional**.

![OC do AJO](./images/ajoocdata2.png)

Selecione **Carregar arquivo DDL** e clique em **Escolher arquivos**.

![OC do AJO](./images/ajoocdata3.png)

Agora que seus esquemas XDM relacionais estão configurados e com dados sendo assimilados, você pode começar a usar esses dados para criar sua campanha orquestrada no próximo exercício.

## 3.8.1.2 assimilação de dados


## Próximas etapas

Vá para [Criar sua campanha orquestrada](./ex2.md){target="_blank"}

Voltar para [Adobe Journey Optimizer: Campanhas](./ajocampaigns.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
