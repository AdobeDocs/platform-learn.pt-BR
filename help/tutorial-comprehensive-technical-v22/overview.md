---
title: Visão geral
description: Ponto de partida para engenheiros de dados, analistas de dados, arquitetos de dados, cientistas de dados, engenheiros de orquestração e profissionais de marketing para obter uma compreensão completa do valor comercial da Adobe Experience Platform e de todos os seus serviços de aplicativos.
doc-type: multipage-overview
hide: false
exl-id: 88c19383-c185-40f0-b118-6cb82db0ce0e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1869'
ht-degree: 1%

---

# Tutorial técnico completo da Adobe Experience Platform

## Visão geral

Este tutorial é o ponto de partida perfeito para engenheiros de dados, analistas de dados, arquitetos de dados, cientistas de dados, engenheiros de orquestração e profissionais de marketing para obter uma compreensão completa do valor comercial da Adobe Experience Platform e de todos os seus serviços de aplicativos. Cada lição se concentra em um verdadeiro desafio que as empresas enfrentam no complexo ecossistema de personalização de hoje e detalha como o Experience Platform resolve esse desafio em vários exercícios práticos. Assista a este vídeo para entender os problemas que a Adobe Experience Platform ajudará a resolver.

>[!VIDEO](https://video.tv.adobe.com/v/344237?quality=12&enable=on)

Este tutorial é muito diverso e oferece insights claros nos seguintes aplicativos:

- Adobe Experience Platform
- Coleção de dados da Adobe Experience Platform
- Real-time CDP
- Adobe Journey Optimizer
- Customer Journey Analytics
- Offer Decisioning

Este tutorial não se concentra apenas em aplicativos de Adobe, mas leva em consideração o ecossistema mais amplo no qual as marcas operam. Para fazer isso, em algumas lições há um foco em como _non-Adobe_ os aplicativos são integrados ao Adobe Experience Platform. Dessa forma, você terá uma compreensão profunda de como os seguintes aplicativos funcionarão em conjunto com o Adobe Experience Platform:

- Amazon: AWS Lambda, AWS S3, AWS Kinesis
- Google: Google Cloud Platform, Google BigQuery, Google Display&amp;Video 360, Google AdWords
- Microsoft: Power BI, Azure EventHub, Armazenamento Azure Blob
- Salesforce: Tableau
- Apache Kafka
- Postman
- ...

Após concluir este tutorial, você poderá:

- Configurar esquemas, misturas, conjuntos de dados e identidades
- Configure uma propriedade de Coleta de dados do Adobe Experience Platform e configure a nova extensão do SDK da Web na Coleta de dados do Adobe Experience Platform
- Transmitir dados para o Adobe Experience Platform em tempo real usando a Coleta de dados da Adobe Experience Platform, o Gerenciador de tags da Google ou o Amazon Alexa
- Faça a assimilação de dados em lote no Adobe Experience Platform usando um workflow ou usando um aplicativo de extração, transformação e carregamento (ETL)
- Visualizar e usar o Perfil do cliente em tempo real no Adobe Experience Platform
- Criar segmentos
- Consumir várias APIs do Adobe Experience Platform
- Usar o SQL para consultar seus dados no Adobe Experience Platform
- Configurar, treinar e classificar modelos de aprendizado de máquina no Adobe Experience Platform
- Use o Journey Orchestration para configurar jornadas em tempo real, baseadas em acionadores
- Use a CDP em tempo real para tomar medidas ativando um segmento para vários destinos
- Use o Customer Journey Analytics para criar relatórios sobre dados de clientes omnicanais de várias fontes, incluindo o Google BigQuery

## Pré-requisitos

- Acesso ao Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acesso à coleta de dados do Adobe Experience Platform: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Acesso ao sistema de demonstração: [https://dashboard.adobedemo.com/](https://dashboard.adobedemo.com/)

>[!IMPORTANT]
>
>Este tutorial foi criado para facilitar um formato específico de workshop. Ele usa sistemas e contas específicos aos quais você pode não ter acesso. Mesmo sem acesso, achamos que você ainda pode aprender muito lendo esse conteúdo muito detalhado. Se você participar de um dos workshops e precisar de suas credenciais de acesso, entre em contato com o representante do Adobe, que fornecerá as informações necessárias.

## Sobre este tutorial

Nessas lições, você implementará o Adobe Experience Platform e o Application Services usando um site de demonstração que suporta vários setores. O site de demonstração e o aplicativo móvel têm uma camada de dados avançada e uma funcionalidade que permitirá a criação de uma implementação realista. Ele fornece acesso a marcas de demonstração, como **Luma**, **Signal do Haqqani**, **Notícias da EXP**, **MÚTUO365**, **Carvelo** e vários outros. Você criará sua própria propriedade do Cliente de coleta de dados da Adobe Experience Platform, em sua própria organização do Experience Cloud, e a mapeará ao seu site de demonstração. Isso gerará dados enviados para sua própria instância do Adobe Experience Platform.

## Arquitetura

Antes de começar com os exercícios práticos, dê uma olhada na Arquitetura por trás deste tutorial. Como você pode ver na Visão geral acima, este tutorial aprofundará alguns recursos e funcionalidades do Adobe Experience Platform, mas também discutirá várias integrações em uma variedade de Fontes e Destinos. Para entender adequadamente a arquitetura por trás deste tutorial e o posicionamento geral do Adobe Experience Platform em seu ecossistema Enterprise, comece revisando o vídeo e o diagrama da arquitetura.

Ir para [Arquitetura](./architecture.md).


## Vídeos

![Vídeos](./assets/images/yt.jpeg)

Você pode encontrar muitos vídeos interessantes de nossos eventos da Tech Academy, de Bootcamps e muito mais em nossa página [Canal YouTube da comunidade do Experience Makers](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw).

Vários vídeos foram criados e mostram elementos de ativação e integrações eficientes entre aplicativos Adobe Experience Platform e não Adobe. Clique no link abaixo para encontrar uma visão geral desses vídeos.

Ir para [Vídeos](./videos.md).



## Como a conclusão do tutorial técnico abrangente para o Adobe Experience Platform é avaliada?

Se você estiver participando deste tutorial como um parceiro de Adobe ou funcionário de Adobe, é necessário enviar seu progresso após concluir cada módulo de capacitação.

Você pode encontrar os requisitos e o processo para enviar a conclusão aqui: [Medição da conclusão](./completion.md)

## Conteúdo

[0. Introdução](./modules/module0/getting-started.md)

- **Público-alvo:** Todos os participantes do tutorial técnico abrangente do Adobe Experience Platform
- **Pré-requisitos:** Acesso ao sistema de demonstração Em seguida, Coleta de dados do Adobe Experience Platform e Adobe Experience Platform. Acesso à ID de configuração padrão do seu ambiente Adobe Experience Platform.
- **Descrição:** Neste módulo fundamental, você configurará tudo para acessar e usar o ambiente de demonstração.
- **Investimento de tempo:** 30 minutos

[1. Foundation - Configuração da coleta de dados e do SDK da Web da Adobe Experience Platform](./modules/module1/data-ingestion-launch-web-sdk.md)

- **Público-alvo:** Engenheiro de dados, arquiteto de dados
- **Pré-requisitos:** Acesso à coleta de dados do Adobe Experience Platform e da Adobe Experience Platform.
- **Descrição:** Neste módulo fundamental, você aprenderá sobre a Coleta de dados da Adobe Experience Platform e a nova extensão do SDK da Web.
- **Investimento de tempo:** 30 minutos

[2. Base - Ingestão de dados](./modules/module2/data-ingestion.md)

- **Público-alvo:** Engenheiro de dados, arquiteto de dados
- **Pré-requisitos:** Acesso à coleta de dados do Adobe Experience Platform e da Adobe Experience Platform.
- **Descrição:** Neste módulo fundamental, você assimilará dados do site na Platform
- **Investimento de tempo:** 120 minutos

[3. Base - Perfil do cliente em tempo real](./modules/module3/real-time-customer-profile.md)

- **Público-alvo:** Engenheiro de dados, arquiteto de dados, profissional de marketing
- **Pré-requisitos:** Acesso ao Adobe Experience Platform e Postman
- **Descrição:** Neste módulo fundamental, você explorará o Perfil do cliente em tempo real no Adobe Experience Platform, utilizando a interface do usuário e a API.
- **Investimento de tempo:** 90 minutos
- **Baixar estes ativos**:
   - [Coleções do Postman](./assets/postman/postman_profile.zip)

[4. Serviço de query](./modules/module4/query-service.md)

- **Público-alvo:** Engenheiro de dados, arquiteto de dados, analista de dados, especialista em BI
- **Pré-requisitos:** Acesso ao Adobe Experience Platform, Serviço de query, Power BI ou Tableau
- **Descrição:** Neste módulo, você aprenderá a usar o Serviço de query do Adobe Experience Platform.
- **Investimento de tempo:** 90 minutos
- **Baixar estes ativos**:
   - [JSON - Dados de exemplo: Sistema de demonstração - Conjunto de dados do evento para site](./assets/json/ee.json)
   - [JSON - Dados de exemplo: Sistema de demonstração - Conjunto de dados de eventos para central de atendimento](./assets/json/callcenter.json)
   - [JSON - Dados de exemplo: Sistema de demonstração - Conjunto de dados de perfil para fidelidade](./assets/json/loyalty.json)

[5. Serviços inteligentes](./modules/module5/intelligent-services.md)

- **Público-alvo:** Engenheiro de dados, arquiteto de dados, cientista de dados
- **Pré-requisitos:** Acesso à Adobe Experience Platform, Serviços inteligentes
- **Descrição:** Neste módulo, você aprenderá a configurar, configurar e usar os Serviços inteligentes Adobe Experience Platform.
- **Investimento de tempo:** 60 minutos

[6. Real-Time CDP - Crie um segmento e execute uma ação](./modules/module6/real-time-cdp-build-a-segment-take-action.md)

- **Público-alvo:** Arquiteto de dados, engenheiro de orquestração, profissional de marketing
- **Pré-requisitos:** Acesso ao Adobe Experience Platform, CDP em tempo real, Adobe Audience Manager, Adobe Target, AWS S3
- **Descrição:** Neste módulo, você configurará um segmento, o ativará para a Segmentação de fluxo e ativará o segmento para vários destinos, incluindo Google DV360, Google AdWords, Adobe Audience Manager, Adobe Target e destinos S3 como o Salesforce Marketing Cloud.
- **Investimento de tempo:** 90 minutos

[7. Adobe Journey Optimizer: Orquestração](./modules/module7/journey-orchestration-create-account.md)

- **Público-alvo:** Engenheiro de dados, arquiteto de dados, engenheiro de orquestração
- **Pré-requisitos:** Acesso ao Adobe Experience Platform e Adobe Journey Optimizer
- **Descrição:** Neste módulo, você usará o Adobe Journey Optimizer para criar uma jornada baseada em acionador.
- **Investimento de tempo:** 60 minutos

[8. Adobe Journey Optimizer: Fontes de dados externas e ações personalizadas](./modules/module8/journey-orchestration-external-weather-api-sms.md)

- **Público-alvo:** Engenheiro de dados, Arquiteto de dados, Engenheiro de orquestração, profissional de marketing
- **Pré-requisitos:** Acesso ao Adobe Experience Platform, Adobe Journey Optimizer, API Open Weather, Twilio
- **Descrição:** Neste módulo, você usará o Adobe Journey Optimizer para acompanhar o comportamento do cliente, tanto online quanto offline, e responder a ele de forma inteligente, contextual e em tempo real em vários canais.
- **Investimento de tempo:** 90 minutos

[9. Adobe Journey Optimizer: offer decisioning](./modules/module9/offer-decisioning.md)

- **Público-alvo:** Engenheiro de dados, Arquiteto de dados, Engenheiro de orquestração, profissional de marketing
- **Pré-requisitos:** Acesso ao Adobe Experience Platform e ao Offer Decisioning
- **Descrição:** Neste módulo, você usará o serviço de aplicativo Adobe Experience Platform - Offers/Decisioning de forma prática para configurar as Ofertas personalizadas e sua própria Atividade de oferta.
- **Investimento de tempo:** 120 minutos

[10. Adobe Journey Optimizer: Jornadas baseadas em eventos](./modules/module10/journeyoptimizer.md)

- **Público-alvo:** Email Marketer, Especialista em Orquestração, Engenheiro de Dados, Arquiteto de Dados, Analista de Dados
- **Pré-requisitos:** Acesso ao Adobe Experience Platform e Journey Optimizer
- **Descrição:** Neste módulo, você aprenderá tudo o que há para saber sobre o Journey Optimizer, o que ajuda as empresas a projetar e fornecer experiências conectadas, contextuais e personalizadas para seus clientes.
- **Investimento de tempo:** 120 minutos

[11. Customer Journey Analytics: Criar um painel usando o Analysis Workspace sobre o Adobe Experience Platform](./modules/module11/customer-journey-analytics-build-a-dashboard.md)

- **Público-alvo:** Engenheiro de dados, Arquiteto de dados, Analista de dados
- **Pré-requisitos:** Acesso ao Adobe Experience Platform e ao Customer Journey Analytics
- **Descrição:** Neste módulo, você entrará online em insights offline configurando um painel contendo dados omnicanais como Interações de site, Interações de aplicativo móvel, Interações do call center, Interações na loja e muito mais.
- **Investimento de tempo:** 120 minutos

[12. Customer Journey Analytics: Assimilar e analisar dados do Google Analytics no Adobe Experience Platform com o Conector de fonte BigQuery](./modules/module12/customer-journey-analytics-bigquery-gcp.md)

- **Público-alvo:** Engenheiro de dados, Arquiteto de dados, Analista de dados
- **Pré-requisitos:** Acesso ao Adobe Experience Platform, Customer Journey Analytics, Google Cloud Platform, Google BigQuery
- **Descrição:** Neste módulo, você configurará sua própria instância da Google Cloud Platform, carregará dados de demonstração na Google Cloud Platform e usará o BigQuery Source Connector para assimilar esses dados da Google Cloud Platform no Adobe Experience Platform. Por fim, você usará o Customer Journey Analytics para visualizar esses dados.
- **Investimento de tempo:** 120 minutos
- **Baixar estes ativos**:
   - [JSON - Dados de exemplo: Demonstração - Dados de fidelidade](./assets/json/bqLoyalty.json)

[13. Real-Time CDP: Ativação de Segmento para o Hub de Eventos do Microsoft Azure](./modules/module13/segment-activation-microsoft-azure-eventhub.md)

- **Público-alvo:** Engenheiro de dados, Arquiteto de dados, Analista de dados
- **Pré-requisitos:** Acesso ao Adobe Experience Platform, CDP em tempo real e Microsoft Azure
- **Descrição:** Neste módulo, você configurará um destino EventHub do Microsoft Azure como um destino em tempo real para a CDP em tempo real do Adobe Experience Platform. Você também irá configurar e implantar uma função do Azure que será acionada em tempo real sempre que o Adobe Experience Platform fornecer uma carga de segmento ao seu destino do Azure EventHub. A Função do Azure que você acionará mostrará o mecanismo dos recursos de ativação da CDP em tempo real do Adobe Experience Platform.
Como parte desse módulo, você também terá uma compreensão do que aciona a CDP em tempo real para realmente fornecer uma carga para um destino especificado. Também discutiremos o status de uma qualificação de segmento e como ela está relacionada à ativação.
- **Investimento de tempo:** 90 minutos

[14. Conexões Real-Time CDP: Encaminhamento de evento](./modules/module14/aep-data-collection-ssf.md)

- **Público-alvo:** Engenheiro de dados, Arquiteto de dados, Analista de dados
- **Pré-requisitos:** Acesso às propriedades Conexões, Tags e Encaminhamento de eventos do Real-Time CDP
- **Descrição:** Neste módulo, você usará os conjuntos de dados, esquemas e a propriedade Coleta de dados do Adobe Experience Platform configurados anteriormente para coletar dados e, em seguida, encaminhar esse servidor de dados para um terminal de escolha.
- **Investimento de tempo:** 90 minutos

[15. Transmitir dados do Apache Kafka para o Real-Time CDP](./modules/module15/aep-apache-kafka.md)

- **Público-alvo:** Analista de dados, engenheiro de dados, arquiteto de dados
- **Pré-requisitos:** Acesso ao Adobe Experience Platform
- **Descrição:** Neste módulo, você aprenderá a configurar seu próprio cluster Apache Kafka, definir tópicos, produtores e consumidores e transmitir dados para o Adobe Experience Platform usando o Adobe Experience Platform Sink Connector para Kafka Connect.
- **Investimento de tempo:** 90 minutos

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender tudo o que há para saber sobre a Adobe Experience Platform. Se você tiver dúvidas, queira compartilhar comentários gerais de suas sugestões sobre conteúdo futuro, entre em contato diretamente com Wouter Van Geluwe, enviando um email para **vangeluw@adobe.com**.
