---
title: Coleta de dados - FAC - Configure sua conta Snowflake
description: Foundation - FAC - Configure sua conta Snowflake
kt: 5342
doc-type: tutorial
exl-id: e72cdbfc-5b42-411f-9c63-e886776deabe
source-git-commit: d26d4735c92498d56beb7859ec67a0c3e174fc25
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# 3.1.1 Configurar o ambiente Snowflake

## 3.1.1.1 Criar sua conta

Ir para [https://snowflake.com](https://snowflake.com). Clique em **INICIAR GRATUITAMENTE**.

![FAC](./images/sf1.png)

Insira seus detalhes e clique em **Continuar**.

![FAC](./images/sf2.png)

Insira seus detalhes, escolha seu provedor de nuvem e clique em **Introdução**.

![FAC](./images/sf3.png)

Insira seus detalhes ou clique em **Ignorar** (x2).

![FAC](./images/sf4.png)

Você verá isso. Verifique seu email e clique no email de confirmação enviado para você.

![FAC](./images/sf5.png)

Clique no link do email de confirmação para ativar sua conta e definir seu nome de usuário e senha. Clique em **Introdução**. Você precisará usar esse nome de usuário e senha no próximo exercício.

![FAC](./images/sf6.png)

Você será conectado ao Snowflake. Clique em **Ignorar por agora**.

![FAC](./images/sf7.png)

## 3.1.1.2 Criar o banco de dados

Vá para **Dados > Bancos de dados**. Clique em **+ Banco de Dados**.

![FAC](./images/db1.png)

Use o nome **CITISIGNAL** para o banco de dados. Clique em **CRIAR**.

![FAC](./images/db2.png)

## 3.1.1.3 Criar tabelas

Agora você pode começar a criar suas tabelas no Snowflake. Você encontrará scripts abaixo para executar o para criar suas tabelas.

### Tabela CK_PERSONS

Clique em **+ Criar**, em **Tabela** e em **Padrão**.

![FAC](./images/tb1.png)

Você verá isso. Copie a consulta abaixo e cole-a no Snowflake. Selecione o banco de dados **CITISIGNAL** no canto superior esquerdo da tela antes de criar a tabela.

```sql
create or replace TABLE CITISIGNAL.PUBLIC.CK_PERSONS (
	PERSON_ID NUMBER(38,0) NOT NULL,
	NAME VARCHAR(255),
	AGE NUMBER(38,0),
	EMAIL VARCHAR(255),
	PHONE_NUMBER VARCHAR(20),
	GENDER VARCHAR(10),
	OCCUPATION VARCHAR(100),
	ISATTMOBILESUB BOOLEAN,
	primary key (PERSON_ID)
);
```

Clique em **Criar tabela**.

![FAC](./images/tb2.png)

Depois que o script for executado, você poderá encontrar sua tabela em **Bancos de dados > CITISIGNAL > PÚBLICO**.

![FAC](./images/tb3.png)

### Tabela CK_HOUSEHOLDS

Clique em **+ Criar**, em **Tabela** e em **Padrão**.

![FAC](./images/tb1.png)

Você verá isso. Copie a consulta abaixo e cole-a no Snowflake. Selecione o banco de dados **CITISIGNAL** no canto superior esquerdo da tela antes de criar a tabela.

```sql
create or replace TABLE CITISIGNAL.PUBLIC.CK_HOUSEHOLDS (
	HOUSEHOLD_ID NUMBER(38,0) NOT NULL,
	ADDRESS VARCHAR(255),
	CITY VARCHAR(100),
	STATE VARCHAR(50),
	POSTAL_CODE VARCHAR(20),
	COUNTRY VARCHAR(100),
	ISELIGIBLEFORFIBER BOOLEAN,
	PRIMARY_PERSON_ID NUMBER(38,0),
	ISFIBREENABLED BOOLEAN,
	primary key (HOUSEHOLD_ID)
);
```

Clique em **Criar tabela**.

![FAC](./images/tb4.png)

Depois que o script for executado, você poderá encontrar sua tabela em **Bancos de dados > CITISIGNAL > PÚBLICO**.

![FAC](./images/tb5.png)

### Tabela CK_USERS

Clique em **+ Criar**, em **Tabela** e em **Padrão**.

![FAC](./images/tb1.png)

Você verá isso. Copie a consulta abaixo e cole-a no Snowflake. Selecione o banco de dados **CITISIGNAL** no canto superior esquerdo da tela antes de criar a tabela.

```sql
create or replace TABLE CITISIGNAL.PUBLIC.CK_USERS (
	USER_ID NUMBER(38,0) NOT NULL,
	PERSON_ID NUMBER(38,0),
	HOUSEHOLD_ID NUMBER(38,0),
	primary key (USER_ID),
	foreign key (PERSON_ID) references CITISIGNAL.PUBLIC.CK_PERSONS(PERSON_ID),
	foreign key (HOUSEHOLD_ID) references CITISIGNAL.PUBLIC.CK_HOUSEHOLDS(HOUSEHOLD_ID)
);
```

Clique em **Criar tabela**.

![FAC](./images/tb6.png)

Depois que o script for executado, você poderá encontrar sua tabela em **Bancos de dados > CITISIGNAL > PÚBLICO**.

![FAC](./images/tb7.png)

### Tabela CK_MONTHLY_DATA_USAGE

Clique em **+ Criar**, em **Tabela** e em **Padrão**.

![FAC](./images/tb1.png)

Você verá isso. Copie a consulta abaixo e cole-a no Snowflake. Selecione o banco de dados **CITISIGNAL** no canto superior esquerdo da tela antes de criar a tabela.

```sql
create or replace TABLE CITISIGNAL.PUBLIC.CK_MONTHLY_DATA_USAGE (
	USAGE_ID NUMBER(38,0) NOT NULL autoincrement start 1 increment 1 noorder,
	USER_ID NUMBER(38,0),
	MONTH DATE,
	DATA_USAGE_GB NUMBER(10,2),
	primary key (USAGE_ID)
);
```

Clique em **Criar tabela**.

![FAC](./images/tb8.png)

Depois que o script for executado, você poderá encontrar sua tabela em **Bancos de dados > CITISIGNAL > PÚBLICO**.

![FAC](./images/tb9.png)

### Tabela CK_MOBILE_DATA_USAGE

Clique em **+ Criar**, em **Tabela** e em **Padrão**.

![FAC](./images/tb1.png)

Você verá isso. Copie a consulta abaixo e cole-a no Snowflake. Selecione o banco de dados **CITISIGNAL** no canto superior esquerdo da tela antes de criar a tabela.


```sql
create or replace TABLE CITISIGNAL.PUBLIC.CK_MOBILE_DATA_USAGE (
	USAGE_ID NUMBER(38,0) NOT NULL autoincrement start 1 increment 1 noorder,
	USER_ID NUMBER(38,0),
	DATE DATE,
	TIME TIME(9),
	APP_NAME VARCHAR(255),
	DATA_USAGE_MB NUMBER(10,2),
	NETWORK_TYPE VARCHAR(50),
	DEVICE_TYPE VARCHAR(50),
	COUNTRY_CODE VARCHAR(10),
	primary key (USAGE_ID)
);
```

Clique em **Criar tabela**.

![FAC](./images/tb10.png)

Depois que o script for executado, você poderá encontrar sua tabela em **Bancos de dados > CITISIGNAL > PÚBLICO**.

![FAC](./images/tb11.png)

Todas as tabelas foram criadas.


## 3.1.1.4 Assimilar dados de amostra

Agora é possível começar a carregar dados de amostra no banco de dados.

...

Você concluiu a configuração no Snowflake.


Próxima Etapa: [3.1.2 Criar esquemas, modelo de dados e links](./ex2.md)

[Voltar ao módulo 3.1](./fac.md)

[Voltar a todos os módulos](../../../overview.md)
