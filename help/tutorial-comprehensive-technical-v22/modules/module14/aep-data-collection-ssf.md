---
title: Coleta de dados do Adobe Experience Platform e encaminhamento pelo lado do servidor em tempo real
description: Neste módulo, você usará os conjuntos de dados, esquemas e as propriedades do Adobe Experience Platform Data Collection Server configurados anteriormente para coletar dados e, em seguida, encaminhar esse servidor de dados para um terminal de escolha.
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: c157ca52-c84f-4398-a658-2b6067e41707
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 1%

---

# 14. Conexões Real-Time CDP: Encaminhamento de evento

**Autor: [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/), [Clement Delalande](https://www.linkedin.com/in/clement-delalande/)**

Neste módulo, você usará os conjuntos de dados, esquemas e a propriedade Cliente da coleta de dados do Adobe Experience Platform configurados anteriormente para coletar dados e, em seguida, encaminhar esse servidor de dados para um terminal de escolha.

Neste módulo, você:

- Criar uma propriedade do Adobe Experience Platform Data Collection Server
- Instalar e usar a extensão Adobe Cloud Connector na Coleta de dados do Adobe Experience Platform
- Criar um endpoint da função Google e dados de fluxo para ele
- Criar um terminal AWS e enviar dados para ele

Assista a este vídeo para entender o valor, a jornada do cliente e o processo de configuração:

>[!VIDEO](https://video.tv.adobe.com/v/331987?quality=12&learn=on)

## Objetivos de aprendizagem

- Familiarize-se com as propriedades do Adobe Experience Platform Data Collection Server e a nova extensão do Adobe Cloud Connector
- Entenda como reutilizar dados do SDK da Web da Adobe Experience Platform em soluções de terceiros como Google e AWS
- Entenda a arquitetura por trás da coleta de dados do Adobe Experience Platform e do encaminhamento pelo lado do servidor.

## Pré-requisitos

- Acesso à coleta de dados do Adobe Experience Platform e da Adobe Experience Platform
- Noções básicas sobre conjuntos de dados e XDM da Adobe Experience Platform

>[!IMPORTANT]
>
>Este tutorial foi criado para facilitar um formato específico de workshop. Ele usa sistemas e contas específicos aos quais você pode não ter acesso. Mesmo sem acesso, achamos que você ainda pode aprender muito lendo esse conteúdo muito detalhado. Se você participar de um dos workshops e precisar de suas credenciais de acesso, entre em contato com o representante do Adobe, que fornecerá as informações necessárias.

## Visão geral da arquitetura

Consulte a arquitetura abaixo, que destaca os componentes que serão discutidos e usados neste módulo.

![Visão geral da arquitetura](../../assets/images/architecturem21.png)

## Sandbox para usar

Para este módulo, use esta sandbox: `--aepSandboxId--`.

>[!NOTE]
>
>Não se esqueça de instalar, configurar e usar a Extensão do Chrome, conforme referenciado em [0.1 - Instalar a extensão do Chrome para a documentação do Experience League](../module0/ex1.md)

## Exercícios

[14.1 Criar uma propriedade de Encaminhamento de evento de coleta de dados](./ex1.md)

Nesse exercício, você criará sua propriedade Adobe Experience Platform Data Collection Event Forwarding .

[14.2 Atualize seu conjunto de dados para disponibilizar os dados para sua propriedade de Encaminhamento de eventos da coleta de dados](./ex2.md)

Neste exercício, você atualizará seu conjunto de dados existente para disponibilizar os dados coletados pela propriedade Cliente de coleta de dados do Adobe Experience Platform para a propriedade do Servidor de coleta de dados da Adobe Experience Platform.

[14.3 Criar e configurar um webhook personalizado](./ex3.md)

Neste exercício, você criará e configurará um webhook personalizado e começará a encaminhar dados coletados pelo SDK da Web para esse webhook personalizado.

[14.4 Criar e configurar uma função da Google Cloud](./ex4.md)

Neste exercício, você criará e configurará uma Função da Google Cloud e começará a encaminhar dados coletados pelo SDK da Web para o Google.

[14.5 Encaminhar eventos para o ecossistema do AWS](./ex5.md)

Neste exercício, você configurará seu ambiente AWS usando o AWS API Gateway, o AWS Kinesis, o AWS Firehose e o AWS S3, após o que iniciará o encaminhamento dos dados do evento coletados pelo SDK da Web.

[Resumo e benefícios](./summary.md)

Resumo deste módulo e visão geral dos benefícios.

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender tudo o que há para saber sobre a Adobe Experience Platform. Se você tiver dúvidas, queira compartilhar comentários gerais de suas sugestões sobre conteúdo futuro, entre em contato diretamente com Wouter Van Geluwe, enviando um email para **vangeluw@adobe.com**.

[Voltar para todos os módulos](../../overview.md)
