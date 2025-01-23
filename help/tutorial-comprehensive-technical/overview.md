---
title: Visão geral
description: Ponto de partida para engenheiros de dados, analistas de dados, arquitetos de dados, cientistas de dados, engenheiros de orquestração e profissionais de marketing para obter uma compreensão completa do valor comercial da Adobe Experience Platform e de todos os seus serviços de aplicativos.
doc-type: multipage-overview
exl-id: 88c19383-c185-40f0-b118-6cb82db0ce0e
source-git-commit: bd46be455f88007174f7e6be9a1ce5f508edc09b
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 2%

---

# Tutorial técnico completo da Adobe Experience Platform

![Informantes técnicos](./assets/images/techinsiders.png){width="50px" align="left"}

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
- Configure uma propriedade de Coleção de dados do Adobe Experience Platform e a nova extensão do Web SDK na Coleção de dados do Adobe Experience Platform
- Transmita dados para o Adobe Experience Platform em tempo real usando a Coleção de dados da Adobe Experience Platform
- Assimilação de dados em lote no Adobe Experience Platform usando um fluxo de trabalho ou usando um aplicativo de extração, transformação e carregamento (ETL)
- Visualizar e usar o Perfil do cliente em tempo real no Adobe Experience Platform
- Criar públicos-alvo
- Consumir várias APIs do Adobe Experience Platform
- Usar o SQL para consultar seus dados no Adobe Experience Platform
- Configurar e executar jornadas em tempo real com base em acionadores
- Usar a Real-time CDP para realizar ações ativando um público-alvo para vários destinos
- Use o Customer Journey Analytics para criar relatórios sobre dados de clientes omnicanal de várias fontes, incluindo o Google BigQuery

## Pré-requisitos

Se você quiser usar este tutorial usando sua própria instância do Adobe Experience Platform, siga as instruções [aqui](./setup.md) para preparar sua organização para o tutorial.

- Acesso ao Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acesso à Coleção de Dados do Adobe Experience Platform: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Acesso ao sistema de demonstração: [https://dsn.adobe.com/](https://dsn.adobe.com/)

## Vídeos

Você pode encontrar muitos vídeos interessantes dos nossos webinários da Tech Academy, de acampamentos e muito mais no nosso [canal do Experience Makers Community YouTube](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw).

## Conclusão e certificação

Este tutorial faz parte de um curso de certificação Adobe. Você pode se inscrever no curso junto com este tutorial acessando [https://certification.adobe.com](https://certification.adobe.com).

Para cada módulo que você concluir usando o tutorial abaixo, você precisa enviar uma prova de conclusão como indicado [aqui](./completion.md).

## Conteúdo

Para verificar o status do conteúdo abaixo, vá para a [página de status](./status.md).

[0. Introdução](./modules/gettingstarted/gettingstarted/getting-started.md)

Neste módulo fundamental, você configurará tudo para poder acessar e usar o ambiente de demonstração.

**Investimento de tempo:** 30 minutos

### 1. Coleta de dados

[1.1 Foundation - Configuração da coleção de dados da Adobe Experience Platform e do Web SDK](./modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md)

Neste módulo fundamental, você aprenderá sobre a Coleção de dados do Adobe Experience Platform e a nova extensão do Web SDK.

**Investimento de tempo:** 30 minutos

[1.2 Foundation - Assimilação de dados](./modules/datacollection/module1.2/data-ingestion.md)

Neste módulo fundamental, você assimilará dados de várias fontes na Adobe Experience Platform

**Investimento de tempo:** 120 minutos

[1.3 Composição de público-alvo federado](./modules/datacollection/module1.3/fac.md)

Neste módulo, você aprenderá a configurar um modelo de Federated Audiences e gerar públicos usando dados federados.

**Investimento de tempo:** 90 minutos

### 2. Real-Time CDP B2C

[2.1 Foundation - Perfil do cliente em tempo real](./modules/rtcdp-b2c/module2.1/real-time-customer-profile.md)

Neste módulo fundamental, você explorará o Perfil do cliente em tempo real no Adobe Experience Platform usando a interface e a API.

**Investimento de tempo:** 90 minutos

[2.2 Serviços inteligentes](./modules/rtcdp-b2c/module2.2/intelligent-services.md)

Neste módulo, você aprenderá a configurar, configurar e usar os Serviços inteligentes da Adobe Experience Platform.

**Investimento de tempo:** 60 minutos

[2.3 Real-Time CDP - Criar um público-alvo e realizar ações](./modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md)

Neste módulo, você configurará um público-alvo e o ativará para vários destinos, incluindo Google DV360, Adobe Target e AWS S3.

**Investimento de tempo:** 90 minutos

[2.4 Real-Time CDP: Audience Activation para o Hub de eventos do Microsoft Azure](./modules/rtcdp-b2c/module2.4/segment-activation-microsoft-azure-eventhub.md)

Neste módulo, você configurará um destino do Microsoft Azure EventHub como destino em tempo real para a CDP em tempo real do Adobe Experience Platform. Você também configurará e implantará uma função do Azure que será acionada em tempo real sempre que a Adobe Experience Platform fornecer uma carga de público-alvo para seu destino do Azure EventHub. A Azure Function que você acionará mostrará o mecanismo dos recursos de ativação da Adobe Experience Platform Real-time CDP.
Como parte desse módulo, você também compreenderá o que aciona a Real-time CDP para realmente fornecer uma carga útil a um destino especificado. Também discutiremos o status de uma qualificação de público-alvo e como ela está relacionada à ativação.

**Investimento de tempo:** 90 minutos

[2.5 Conexões do Real-Time CDP: encaminhamento de eventos](./modules/rtcdp-b2c/module2.5/aep-data-collection-ssf.md)

Neste módulo, você usará os conjuntos de dados, esquemas e a propriedade de Coleção de dados da Adobe Experience Platform configurados anteriormente para coletar dados e, em seguida, encaminhará esses dados do lado do servidor para vários endpoints, como o Google Cloud Platform Pub/Sub e o AWS Kinesis.

**Investimento de tempo:** 90 minutos

[2.6 Transmitir dados do Apache Kafka para o Real-Time CDP](./modules/rtcdp-b2c/module2.6/aep-apache-kafka.md)

Neste módulo, você aprenderá a configurar seu próprio cluster do Apache Kafka, definir tópicos, produtores e consumidores e transmitir dados para o Adobe Experience Platform usando o Conector de coletor do Adobe Experience Platform para Kafka Connect.

**Investimento de tempo:** 90 minutos

### 3. Adobe Journey Optimizer B2C

[3.1 Adobe Journey Optimizer: Orquestração](./modules/ajo-b2c/module3.1/journey-orchestration-create-account.md)

Neste módulo, você usará o Adobe Journey Optimizer para criar uma jornada baseada em acionador.

**Investimento de tempo:** 60 minutos

[3.2 Adobe Journey Optimizer: fontes de dados externas e ações personalizadas](./modules/ajo-b2c/module3.2/journey-orchestration-external-weather-api-sms.md)

Neste módulo, você usará o Adobe Journey Optimizer para ouvir o comportamento do cliente, online e offline, e responder a ele de forma inteligente, contextual e em tempo real por vários canais.

**Investimento de tempo:** 90 minutos

[3.3 Adobe Journey Optimizer: Offer Decisioning](./modules/ajo-b2c/module3.3/offer-decisioning.md)

Neste módulo, você usará o serviço de aplicativos Adobe Experience Platform - Offers/Decisioning de forma prática para configurar as Ofertas personalizadas e sua própria Atividade de oferta.

**Investimento de tempo:** 120 minutos

[3.4 Adobe Journey Optimizer: Jornadas baseadas em eventos](./modules/ajo-b2c/module3.4/journeyoptimizer.md)

Neste módulo, você aprenderá tudo o que há para saber sobre o Journey Optimizer, que ajuda as empresas a projetar e entregar experiências conectadas, contextuais e personalizadas aos clientes.

**Investimento de tempo:** 120 minutos

### 4. Adobe Customer Journey Analytics

[Customer Journey Analytics 4.1: Criar um painel usando o Analysis Workspace sobre o Adobe Experience Platform](./modules/cja-b2c/module4.1/customer-journey-analytics-build-a-dashboard.md)

Neste módulo, você obterá insights online e offline configurando um painel contendo dados omnicanal como Interações de Site, Interações de Aplicativo Móvel, Interações da Central de Atendimento, Interações na Loja e muito mais.

**Investimento de tempo:** 120 minutos

[4.2 Customer Journey Analytics: Assimilar e analise dados de Google Analytics no Adobe Experience Platform com o conector de Source do BigQuery](./modules/cja-b2c/module4.2/customer-journey-analytics-bigquery-gcp.md)

Neste módulo, você configurará sua própria instância da Google Cloud Platform, carregará dados de demonstração na Google Cloud Platform e usará o BigQuery Source Connector para assimilar esses dados da Google Cloud Platform na Adobe Experience Platform. Por fim, você usará o Customer Journey Analytics para visualizar esses dados.

**Investimento de tempo:** 120 minutos

### 5. Data Distiller

[5.1 Serviço de consulta](./modules/datadistiller/module5.1/query-service.md)

Neste módulo, você aprenderá a usar o Adobe Experience Platform Query Service.

**Investimento de tempo:** 90 minutos

![Informantes técnicos](./assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Em caso de dúvidas, envie um email para **techinsiders@adobe.com** para compartilhar comentários gerais sobre sugestões para conteúdo futuro. Entre em contato diretamente com o Tech Insiders.
