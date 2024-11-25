---
title: Configurar o endpoint da API HTTP no Adobe Experience Platform
description: Configurar o endpoint da API HTTP no Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: a29dd01d-4415-45d6-ad52-7f14aef60565
source-git-commit: 6485bfa1c75c43bb569f77c478a273ace24a61d4
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 6%

---

# 2.6.3 Configurar o endpoint de transmissão da API HTTP no Adobe Experience Platform

Antes de configurar o Conector do Adobe Experience Platform Sink no Kafka, é necessário criar um Conector do Source da API HTTP no Adobe Experience Platform. O URL do ponto de extremidade de transmissão da API HTTP é necessário para configurar o Conector do coletor do Adobe Experience Platform.

Para criar um Conector Source da API HTTP, faça logon no Adobe Experience Platform acessando esta URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepSandboxName--``. Depois de selecionar a sandbox apropriada, você verá a alteração da tela e agora estará em sua sandbox dedicada.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/sb1.png)

No menu esquerdo, vá para **Fontes** e role para baixo no **Catálogo de Fontes** até ver **API HTTP**. Clique em **Instalação**.

![Assimilação de dados](./images/kaep1.png)

Clique em **Nova conta**. Use `--aepUserLdap-- - Kafka` como o nome da sua conexão de API HTTP, neste caso **vangeluw - Kafka**. Habilite a caixa de seleção para **Compatível com XDM**. Clique em **Conectar à origem**.

![Assimilação de dados](./images/kaep2.png)

Você verá isso, clique em **Avançar**.

![Assimilação de dados](./images/kaep3.png)

Selecione **Conjunto de dados existente**, abra o menu suspenso. Pesquise e selecione o conjunto de dados **Sistema de demonstração - Conjunto de dados de evento para Call Center (Global v1.1)**.

Clique em **Next**.

![Assimilação de dados](./images/kaep4.png)

Clique em **Concluir**.

![Assimilação de dados](./images/kaep8.png)

Em seguida, você verá uma visão geral do HTTP API Source Connector que acabou de criar.

Você precisará copiar a URL do **endpoint de transmissão**, que se parece com a abaixo, como você precisará dela no próximo exercício.

`https://dcs.adobedc.net/collection/63751d0f299eeb7aa48a2f22acb284ed64de575f8640986d8e5a935741be9067`

![Assimilação de dados](./images/kaep9.png)

Você concluiu este exercício.

Próxima etapa: [2.6.4 Instale e configure o Kafka Connect e o Conector do Coletor do Adobe Experience Platform](./ex4.md)

[Voltar ao módulo 2.6](./aep-apache-kafka.md)

[Voltar a todos os módulos](../../../overview.md)
