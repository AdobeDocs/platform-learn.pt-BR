---
title: Visão geral
description: Ponto de partida para engenheiros de dados, analistas de dados, arquitetos de dados, cientistas de dados, engenheiros de orquestração e profissionais de marketing para obter uma compreensão completa do valor comercial da Adobe Experience Platform e de todos os seus serviços de aplicativos.
doc-type: multipage-overview
hide: false
exl-id: 88c19383-c185-40f0-b118-6cb82db0ce0e
source-git-commit: 7d2f5f842559b2d6d9f115f3993268a4b36a0fe0
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 2%

---

# Tutorial técnico completo da Adobe Experience Platform

## Visão geral

Este tutorial é o ponto de partida perfeito para engenheiros de dados, analistas de dados, arquitetos de dados, cientistas de dados, engenheiros de orquestração e profissionais de marketing a fim de obter uma compreensão completa do valor comercial da Adobe Experience Platform e de todos os seus serviços de aplicativos. Cada lição se concentra em um verdadeiro desafio que as empresas enfrentam no complexo ecossistema de personalização de hoje e detalha como o Experience Platform soluciona esse desafio em vários exercícios práticos.

Este tutorial é muito diverso e oferece insights claros nos seguintes aplicativos:

- Adobe Experience Platform
- Coleção de dados da Adobe Experience Platform
- Real-time CDP
- Adobe Journey Optimizer
- Customer Journey Analytics

Este tutorial não se concentra apenas em aplicativos Adobe, mas leva em conta o ecossistema mais amplo em que as marcas operam. Para fazer isso, em algumas lições, há um foco em como os aplicativos _não-Adobe_ se integram ao Adobe Experience Platform. Dessa forma, você compreenderá detalhadamente como os seguintes aplicativos funcionarão em conjunto com a Adobe Experience Platform:

- Amazon: AWS Lambda, AWS S3, AWS Kinesis
- Google: Google Cloud Platform, Google BigQuery, Google Display&amp;Video 360, Google AdWords
- Microsoft: Power BI, Azure EventHub, Armazenamento de blobs do Azure
- Salesforce: Tableau
- Apache Kafka
- Postman
- ...

Após concluir os exercícios neste tutorial, você será capaz de:

- Configurar esquemas, grupos de campos, conjuntos de dados e identidades
- Configure uma propriedade de Coleção de dados da Adobe Experience Platform e a nova extensão SDK da Web na Coleção de dados da Adobe Experience Platform
- Transmita dados para o Adobe Experience Platform em tempo real usando a Coleção de dados da Adobe Experience Platform
- Assimilação de dados em lote no Adobe Experience Platform usando um fluxo de trabalho ou usando um aplicativo de extração, transformação e carregamento (ETL)
- Visualizar e usar o Perfil do cliente em tempo real no Adobe Experience Platform
- Criar segmentos
- Consumir várias APIs do Adobe Experience Platform
- Usar o SQL para consultar seus dados no Adobe Experience Platform
- Configurar e executar jornadas em tempo real com base em acionadores
- Usar a Real-time CDP para realizar ações ativando um segmento para vários destinos
- Use o Customer Journey Analytics para criar relatórios sobre dados de clientes omnicanal de várias fontes, incluindo o Google BigQuery

## Pré-requisitos

- Acesso ao Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acesso à Coleção de Dados do Adobe Experience Platform: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Acesso ao sistema de demonstração: [https://dashboard.adobedemo.com/](https://dashboard.adobedemo.com/)

## Vídeos

Você pode encontrar muitos vídeos interessantes dos nossos eventos da Academia de Tecnologia, das acampamentos e muito mais no nosso [canal da YouTube da Comunidade Experience Makers](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw).

## Conteúdo

[0. Introdução](./modules/gettingstarted/gettingstarted/getting-started.md)

- **Público-alvo:** todos os participantes do Tutorial Técnico Abrangente do Adobe Experience Platform
- **Pré-requisitos:** Acesso ao Sistema de Demonstração Seguinte, Adobe Experience Platform e Coleção de Dados do Adobe Experience Platform.
- **Descrição:** Neste módulo fundamental, você configurará tudo para poder acessar e usar o ambiente de demonstração.
- **Investimento de tempo:** 30 minutos

### 1. Coleta de dados

[1.1 Foundation - Configuração da coleção de dados da Adobe Experience Platform e do SDK da Web](./modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md)

- **Público-alvo:** Engenheiro de dados, Arquiteto de dados
- **Pré-requisitos:** Acesso à Coleção de Dados da Adobe Experience Platform e da Adobe Experience Platform.
- **Descrição:** Neste módulo fundamental, você aprenderá sobre a Coleção de dados da Adobe Experience Platform e a nova extensão SDK da Web.
- **Investimento de tempo:** 30 minutos

[1.2 Foundation - Assimilação de dados](./modules/datacollection/module1.2/data-ingestion.md)

- **Público-alvo:** Engenheiro de dados, Arquiteto de dados
- **Pré-requisitos:** Acesso à Coleção de Dados da Adobe Experience Platform e da Adobe Experience Platform.
- **Descrição:** Neste módulo fundamental, você assimilará dados do site na Plataforma
- **Investimento de tempo:** 120 minutos

[1.3 Composição de público-alvo federado](./modules/datacollection/module1.3/fac.md)

- **Público-Alvo:** Analista De Dados, Engenheiro De Dados, Arquiteto De Dados
- **Pré-requisitos:** Acesso ao Adobe Experience Platform
- **Descrição:** Neste módulo, você aprenderá a configurar seu próprio cluster do Apache Kafka, definir tópicos, produtores e consumidores e transmitir dados para a Adobe Experience Platform usando o Adobe Experience Platform Sink Connector for Kafka Connect.
- **Investimento de tempo:** 90 minutos

### 2. Real-Time CDP B2C

[2.1 Foundation - Perfil do cliente em tempo real](./modules/rtcdp-b2c/module2.1/real-time-customer-profile.md)

- **Público-Alvo:** Engenheiro De Dados, Arquiteto De Dados, Profissional De Marketing
- **Pré-requisitos:** Acesso ao Adobe Experience Platform e ao Postman
- **Descrição:** Neste módulo fundamental, você explorará o Perfil do Cliente em Tempo Real no Adobe Experience Platform utilizando a interface e a API.
- **Investimento de tempo:** 90 minutos
- **Baixar estes ativos**:
   - [coleções do Postman](./assets/postman/postman_profile.zip)

[2.2 Serviços inteligentes](./modules/rtcdp-b2c/module2.2/intelligent-services.md)

- **Público-Alvo:** Engenheiro De Dados, Arquiteto De Dados, Cientista De Dados
- **Pré-requisitos:** Acesso ao Adobe Experience Platform, Serviços inteligentes
- **Descrição:** Neste módulo, você aprenderá a instalar, configurar e usar os Serviços Inteligentes da Adobe Experience Platform.
- **Investimento de tempo:** 60 minutos

[2.3 Real-Time CDP - Criar um segmento e tomar medidas](./modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md)

- **Público-Alvo:** Arquiteto De Dados, Engenheiro De Orquestração, Profissional De Marketing
- **Pré-requisitos:** Acesso ao Adobe Experience Platform, Real-time CDP, Adobe Audience Manager, Adobe Target, AWS S3
- **Descrição:** Neste módulo, você configurará um segmento, o habilitará para Segmentação de Streaming e ativará o segmento para vários destinos, incluindo Google DV360, Google AdWords, Adobe Audience Manager, Adobe Target e destinos S3 como Salesforce Marketing Cloud.
- **Investimento de tempo:** 90 minutos

[2.4 Real-Time CDP: Ativação de segmentos para o Hub de eventos do Microsoft Azure](./modules/rtcdp-b2c/module2.4/segment-activation-microsoft-azure-eventhub.md)

- **Público-Alvo:** Engenheiro De Dados, Arquiteto De Dados, Analista De Dados
- **Pré-requisitos:** Acesso ao Adobe Experience Platform, Real-time CDP e Microsoft Azure
- **Descrição:** Neste módulo, você configurará um destino do Microsoft Azure EventHub como um destino em tempo real para o Adobe Experience Platform Real-time CDP. Você também configurará e implantará uma função do Azure que será acionada em tempo real sempre que a Adobe Experience Platform entregar uma carga de segmento para seu destino do Azure EventHub. A Azure Function que você acionará mostrará o mecanismo dos recursos de ativação da Adobe Experience Platform Real-time CDP.
Como parte desse módulo, você também compreenderá o que aciona a Real-time CDP para realmente fornecer uma carga útil a um destino especificado. Também discutiremos o status de uma qualificação de segmento e como ela está relacionada à ativação.
- **Investimento de tempo:** 90 minutos

[2.5 Conexões do Real-Time CDP: encaminhamento de eventos](./modules/rtcdp-b2c/module2.5/aep-data-collection-ssf.md)

- **Público-Alvo:** Engenheiro De Dados, Arquiteto De Dados, Analista De Dados
- **Pré-requisitos:** Acesso às propriedades de Conexões, Marcas e Encaminhamento de Eventos da Real-Time CDP
- **Descrição:** Neste módulo, você usará os conjuntos de dados, esquemas e a propriedade de Coleção de dados da Adobe Experience Platform previamente configurados para coletar dados e, em seguida, encaminhará esses dados do lado do servidor para um ponto de extremidade de escolha.
- **Investimento de tempo:** 90 minutos

[2.6 Transmitir dados do Apache Kafka para o Real-Time CDP](./modules/rtcdp-b2c/module2.6/aep-apache-kafka.md)

- **Público-Alvo:** Analista De Dados, Engenheiro De Dados, Arquiteto De Dados
- **Pré-requisitos:** Acesso ao Adobe Experience Platform
- **Descrição:** Neste módulo, você aprenderá a configurar seu próprio cluster do Apache Kafka, definir tópicos, produtores e consumidores e transmitir dados para a Adobe Experience Platform usando o Adobe Experience Platform Sink Connector for Kafka Connect.
- **Investimento de tempo:** 90 minutos

### 3. Adobe Journey Optimizer B2C

[3.1 Adobe Journey Optimizer: Orquestração](./modules/ajo-b2c/module3.1/journey-orchestration-create-account.md)

- **Público-alvo:** Engenheiro de Dados, Arquiteto de Dados, Engenheiro de Orquestração
- **Pré-requisitos:** Acesso ao Adobe Experience Platform e ao Adobe Journey Optimizer
- **Descrição:** Neste módulo, você usará o Adobe Journey Optimizer para criar uma jornada baseada em gatilho.
- **Investimento de tempo:** 60 minutos

[3.2 Adobe Journey Optimizer: fontes de dados externas e ações personalizadas](./modules/ajo-b2c/module3.2/journey-orchestration-external-weather-api-sms.md)

- **Público-Alvo:** Engenheiro De Dados, Arquiteto De Dados, Engenheiro De Orquestração, Profissional De Marketing
- **Pré-requisitos:** Acesso a Adobe Experience Platform, Adobe Journey Optimizer, API de Tempo Aberto, Twilio
- **Descrição:** Neste módulo, você usará o Adobe Journey Optimizer para ouvir o comportamento do cliente, tanto online quanto offline, e responder a ele de forma inteligente, contextual e em tempo real através de vários canais.
- **Investimento de tempo:** 90 minutos

[3.3 Adobe Journey Optimizer: Offer Decisioning](./modules/ajo-b2c/module3.3/offer-decisioning.md)

- **Público-Alvo:** Engenheiro De Dados, Arquiteto De Dados, Engenheiro De Orquestração, Profissional De Marketing
- **Pré-requisitos:** Acesso ao Adobe Experience Platform e ao Offer Decisioning
- **Descrição:** Neste módulo, você usará o serviço de aplicativos Adobe Experience Platform - Ofertas/Decisão de forma prática para configurar Ofertas Personalizadas e sua própria Atividade de Oferta.
- **Investimento de tempo:** 120 minutos

[3.4 Adobe Journey Optimizer: Jornadas baseadas em eventos](./modules/ajo-b2c/module3.4/journeyoptimizer.md)

- **Público-Alvo:** Profissional De Marketing Por Email, Especialista Em Orquestração, Engenheiro De Dados, Arquiteto De Dados, Analista De Dados
- **Pré-requisitos:** Acesso ao Adobe Experience Platform e ao Journey Optimizer
- **Descrição:** Neste módulo, você aprenderá tudo o que há para saber sobre o Journey Optimizer, que ajuda as empresas a projetar e entregar experiências conectadas, contextuais e personalizadas aos seus clientes.
- **Investimento de tempo:** 120 minutos

### 4. Adobe Customer Journey Analytics

[Customer Journey Analytics 4.1: Criar um painel usando o Analysis Workspace sobre o Adobe Experience Platform](./modules/cja-b2c/module4.1/customer-journey-analytics-build-a-dashboard.md)

- **Público-Alvo:** Engenheiro De Dados, Arquiteto De Dados, Analista De Dados
- **Pré-requisitos:** Acesso ao Adobe Experience Platform e Customer Journey Analytics
- **Descrição:** Neste módulo, você acessará insights online offline configurando um painel contendo dados omnicanal, como Interações de Site, Interações de Aplicativo Móvel, Interações da Central de Atendimento, Interações na Loja e muito mais.
- **Investimento de tempo:** 120 minutos

[4.2 Customer Journey Analytics: Assimilar e analise dados de Google Analytics no Adobe Experience Platform com o conector de Source do BigQuery](./modules/cja-b2c/module4.2/customer-journey-analytics-bigquery-gcp.md)

- **Público-Alvo:** Engenheiro De Dados, Arquiteto De Dados, Analista De Dados
- **Pré-requisitos:** Acesso ao Adobe Experience Platform, Customer Journey Analytics, Google Cloud Platform, Google BigQuery
- **Descrição:** Neste módulo, você configurará sua própria instância da Google Cloud Platform, carregará dados de demonstração na Google Cloud Platform e usará o BigQuery Source Connector para assimilar esses dados da Google Cloud Platform na Adobe Experience Platform. Por fim, você usará o Customer Journey Analytics para visualizar esses dados.
- **Investimento de tempo:** 120 minutos
- **Baixar estes ativos**:
   - [JSON - Dados de amostra: Demonstração - Dados de fidelidade](./assets/json/bqLoyalty.json)

### 5. Data Distiller

[5.1 Serviço de consulta](./modules/datadistiller/module5.1/query-service.md)

- **Público-alvo:** engenheiro de dados, arquiteto de dados, analista de dados, especialista em BI
- **Pré-requisitos:** Acesso ao Adobe Experience Platform, Serviço de Consulta, Power BI Tableau
- **Descrição:** Neste módulo, você aprenderá a usar o Serviço de Consulta da Adobe Experience Platform.
- **Investimento de tempo:** 90 minutos
- **Baixar estes ativos**:
   - [JSON - Dados de amostra: Sistema de demonstração - Conjunto de dados de evento para site](./assets/json/ee.json)
   - [JSON - Dados de amostra: Sistema de demonstração - Conjunto de dados de evento para Call Center](./assets/json/callcenter.json)
   - [JSON - Dados de amostra: Sistema de demonstração - Conjunto de dados do perfil para fidelidade](./assets/json/loyalty.json)





