---
title: Transmitir dados do Apache Kafka para o Adobe Experience Platform
description: Neste módulo, você aprenderá a configurar seu próprio cluster do Apache Kafka, definir tópicos, produtores e consumidores e transmitir dados para o Adobe Experience Platform usando o Conector de coletor do Adobe Experience Platform para Kafka Connect.
kt: 5342
doc-type: tutorial
exl-id: 28c63675-272e-46ff-88fc-6cd4096d66ca
source-git-commit: 2d5ca888eb24c1f65b4ecd48030ec8d1659b7f84
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 1%

---

# 2.6 Transmitir dados do Apache Kafka para o Adobe Experience Platform

Neste módulo, você aprenderá a configurar seu próprio cluster do Apache Kafka, definir tópicos, produtores e consumidores e transmitir dados para o Adobe Experience Platform usando o Conector de dissipador do Adobe Experience Platform pelo Kafka Connect.

## Objetivos de aprendizagem

- Executar uma configuração básica de um cluster Kafka local
- Crie um tópico Kafka, use um produtor Kafka e um consumidor Kafka
- Configurar o Kafka Connect e o conector do Adobe Experience Platform Sink
- Produza eventos manualmente e veja esses eventos serem assimilados no Adobe Experience Platform
- Use uma biblioteca existente de produtores do Twitter do Kafka Connect para transmitir dados do Twitter para o Adobe Experience Platform

## Pré-requisitos

- O Java JDK23 ou superior precisa ser instalado no computador. Você pode baixar esse JDK aqui: [https://www.oracle.com/java/technologies/javase-jdk11-downloads.html](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)
- Acesso ao Adobe Experience Platform

>[!NOTE]
>
>Não se esqueça de instalar, configurar e usar a Extensão do Chrome, conforme referenciado em [Instalar a extensão do Chrome para a documentação do Experience League](../../../getting-started/gettingstarted/ex1.md)

## Exercícios

[2.6.1 Introdução ao Apache Kafka](./ex1.md)

Neste exercício, você aprenderá sobre as noções básicas do Apache Kafka

[2.6.2 Instalar e configurar o cluster Kafka](./ex2.md)

Neste exercício, você baixará, instalará e configurará seu cluster básico Apache Kafka.

[2.6.3 Configurar o endpoint de transmissão da API HTTP no Adobe Experience Platform](./ex3.md)

Neste exercício, você configurará um Conector HTTP API Source no Adobe Experience Platform.

[2.6.4 Instale e configure o Kafka Connect e o Conector do dissipador do Adobe Experience Platform](./ex4.md)

Neste exercício, você usará o Kafka Connect para instalar e usar o Adobe Experience Platform Sink Connector e enviará eventos para o Adobe Experience Platform manualmente.

![Informantes técnicos](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo tudo o que há para saber sobre o Adobe Experience Platform e seus aplicativos. Em caso de dúvidas, envie um email para **techinsiders@adobe.com** para compartilhar comentários gerais sobre sugestões para conteúdo futuro. Entre em contato diretamente com o Tech Insiders.

[Voltar a todos os módulos](./../../../../overview.md)
