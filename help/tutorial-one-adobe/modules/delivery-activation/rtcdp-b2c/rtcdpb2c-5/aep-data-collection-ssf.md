---
title: Coleta de dados da Adobe Experience Platform e encaminhamento pelo lado do servidor em tempo real
description: Neste módulo, você usará os conjuntos de dados, esquemas e a propriedade do Servidor de coleta de dados da Adobe Experience Platform configurados anteriormente para coletar dados e, em seguida, encaminhará esses dados do lado do servidor para um endpoint de escolha.
kt: 5342
doc-type: tutorial
exl-id: dbf5e995-9c2e-4f72-b336-e942cb22cde5
source-git-commit: 2d5ca888eb24c1f65b4ecd48030ec8d1659b7f84
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# 2.5 Conexões do Real-Time CDP: encaminhamento de eventos

Neste módulo, você usará os conjuntos de dados, esquemas e a propriedade do Cliente de coleta de dados da Adobe Experience Platform configurados anteriormente para coletar dados e, em seguida, encaminhará esses dados do lado do servidor para um endpoint de escolha.

Neste módulo, você irá:

- Criar uma propriedade do Servidor de coleta de dados da Adobe Experience Platform
- Instalar e usar a extensão do Adobe Cloud Connector na Coleção de dados da Adobe Experience Platform
- Criar um ponto de extremidade de função do Google e transmitir dados para ele
- Criar um terminal do AWS e transmitir dados para ele

## Objetivos de aprendizagem

- Familiarize-se com as propriedades do Adobe Experience Platform Data Collection Server e a nova extensão do Adobe Cloud Connector
- Entenda como reutilizar dados do Adobe Experience Platform Web SDK em soluções de terceiros, como Google e AWS
- Entenda a arquitetura por trás da Coleção de dados da Adobe Experience Platform e do encaminhamento pelo lado do servidor.

## Pré-requisitos

- Acesso à coleção de dados da Adobe Experience Platform e da Adobe Experience Platform
- Noções básicas sobre conjuntos de dados do Adobe Experience Platform e XDM

>[!NOTE]
>
>Não se esqueça de instalar, configurar e usar a Extensão do Chrome, conforme referenciado em [Instalar a extensão do Chrome para a documentação do Experience League](../../../getting-started/gettingstarted/ex1.md)

## Exercícios

[2.5.1 Criar uma propriedade de encaminhamento de eventos de coleta de dados](./ex1.md)

Neste exercício, você criará sua propriedade de Encaminhamento de eventos da Coleção de dados da Adobe Experience Platform.

[2.5.2 Atualize sua sequência de dados para disponibilizar os dados para sua propriedade de encaminhamento de eventos de coleta de dados](./ex2.md)

Neste exercício, você atualizará a sequência de dados existente para disponibilizar os dados coletados pela propriedade do Cliente de coleta de dados da Adobe Experience Platform à propriedade do Servidor de coleta de dados da Adobe Experience Platform.

[2.5.3 Criar e configurar um webhook personalizado](./ex3.md)

Neste exercício, você criará e configurará um webhook personalizado e começará a encaminhar dados coletados pelo Web SDK para esse webhook personalizado.

[2.5.4 Encaminhar eventos para GCP Pub/Sub](./ex4.md)

Neste exercício, você criará e configurará uma Google Cloud Function e começará a encaminhar dados coletados pelo Web SDK para a Google.

[2.5.5 Encaminhar eventos para o AWS Kinesis e o AWS S3](./ex5.md)

Neste exercício, você configurará o ambiente do AWS usando o AWS IAM, o AWS Kinesis, o AWS Firehose e o AWS S3; depois disso, iniciará o encaminhamento dos dados do evento coletados pelo Web SDK.

![Informantes técnicos](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo tudo o que há para saber sobre o Adobe Experience Platform e seus aplicativos. Em caso de dúvidas, envie um email para **techinsiders@adobe.com** para compartilhar comentários gerais sobre sugestões para conteúdo futuro. Entre em contato diretamente com o Tech Insiders.

[Voltar a todos os módulos](./../../../../overview.md)
