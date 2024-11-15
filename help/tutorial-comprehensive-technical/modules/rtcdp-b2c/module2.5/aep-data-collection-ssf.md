---
title: Coleta de dados da Adobe Experience Platform e encaminhamento pelo lado do servidor em tempo real
description: Neste módulo, você usará os conjuntos de dados, esquemas e a propriedade do Servidor de coleta de dados da Adobe Experience Platform configurados anteriormente para coletar dados e, em seguida, encaminhará esses dados do lado do servidor para um endpoint de escolha.
kt: 5342
doc-type: tutorial
exl-id: aa3ab1eb-6fee-4ea9-9a0d-0d8ca803d7c2
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# 2.5 Conexões do Real-Time CDP: encaminhamento de eventos

**Autor: [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/), [Clement Delalande](https://www.linkedin.com/in/clement-delalande/)**

Neste módulo, você usará os conjuntos de dados, esquemas e a propriedade do Cliente de coleta de dados da Adobe Experience Platform configurados anteriormente para coletar dados e, em seguida, encaminhará esses dados do lado do servidor para um endpoint de escolha.

Neste módulo, você irá:

- Criar uma propriedade do Servidor de coleta de dados da Adobe Experience Platform
- Instale e use a extensão Adobe Cloud Connector na Coleção de dados da Adobe Experience Platform
- Criar um ponto de extremidade de função do Google e transmitir dados para ele
- Criar um terminal do AWS e transmitir dados para ele

Assista a este vídeo para entender o valor, a jornada do cliente e o processo de configuração:

>[!VIDEO](https://video.tv.adobe.com/v/331987?quality=12&learn=on)

## Objetivos de aprendizagem

- Familiarize-se com as propriedades do Adobe Experience Platform Data Collection Server e a nova extensão do Adobe Cloud Connector
- Entenda como reutilizar dados do SDK da Web da Adobe Experience Platform em soluções de terceiros, como Google e AWS
- Entenda a arquitetura por trás da Coleção de dados da Adobe Experience Platform e do encaminhamento pelo lado do servidor.

## Pré-requisitos

- Acesso à coleção de dados da Adobe Experience Platform e da Adobe Experience Platform
- Noções básicas sobre conjuntos de dados do Adobe Experience Platform e XDM

>[!NOTE]
>
>Não se esqueça de instalar, configurar e usar a Extensão do Chrome, conforme referenciado em [Instalar a extensão do Chrome para a documentação do Experience League](../../gettingstarted/gettingstarted/ex1.md)

## Exercícios

[2.5.1 Criar uma propriedade de encaminhamento de eventos de coleta de dados](./ex1.md)

Neste exercício, você criará sua propriedade de Encaminhamento de eventos da Coleção de dados da Adobe Experience Platform.

[2.5.2 Atualize sua sequência de dados para disponibilizar os dados para sua propriedade de encaminhamento de eventos de coleta de dados](./ex2.md)

Neste exercício, você atualizará a sequência de dados existente para disponibilizar os dados coletados pela propriedade do Cliente de coleta de dados da Adobe Experience Platform à propriedade do Servidor de coleta de dados da Adobe Experience Platform.

[2.5.3 Criar e configurar um webhook personalizado](./ex3.md)

Neste exercício, você criará e configurará um webhook personalizado e começará a encaminhar dados coletados pelo SDK da Web para esse webhook personalizado.

[2.5.4 Criar e configurar uma função de nuvem do Google](./ex4.md)

Neste exercício, você criará e configurará uma Google Cloud Function e começará a encaminhar dados coletados pelo SDK da Web para a Google.

[2.5.5 Encaminhar eventos para o ecossistema da AWS](./ex5.md)

Neste exercício, você configurará o ambiente do AWS usando o AWS API Gateway, o AWS Kinesis, o AWS Firehose e o AWS S3; depois disso, iniciará o encaminhamento dos dados do evento coletados pelo SDK da Web.

[Resumo e benefícios](./summary.md)

Resumo desse módulo e visão geral dos benefícios.

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo tudo o que há para saber sobre o Adobe Experience Platform e seus aplicativos. Em caso de dúvidas, envie um email para **techinsiders@adobe.com** para compartilhar comentários gerais sobre sugestões para conteúdo futuro. Entre em contato diretamente com o Tech Insiders.

[Voltar a todos os módulos](../../../overview.md)
