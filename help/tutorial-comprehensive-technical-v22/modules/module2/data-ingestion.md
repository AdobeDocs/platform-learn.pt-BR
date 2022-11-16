---
title: Foundation - Assimilação de dados
description: Foundation - Assimilação de dados
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: dbbc0539-ae1b-488d-b312-76a74d4d361f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 1%

---

# 2. Base - Ingestão de dados

**Autor: [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Neste módulo, o objetivo é aprender tudo sobre a assimilação de dados. Você aprenderá sobre a assimilação de dados em streaming e lote. Você implementará a assimilação de dados de streaming usando o Launch, para que o comportamento do cliente no site do Hands-On Lab seja transmitido à Adobe Experience Platform em tempo real. Você aprenderá sobre a assimilação de dados em lote usando um fluxo de trabalho do Adobe Experience Platform para obter um arquivo CSV, mapeá-lo em relação a um esquema XDM e assimilá-lo no Adobe Experience Platform.

## Objetivos de aprendizagem

- Saiba como criar um esquema XDM no Adobe Experience Platform
- Saiba como criar conjuntos de dados no Adobe Experience Platform
- Saiba como criar um endpoint de transmissão e configurar a extensão do Adobe Experience Platform no Launch
- Saiba como criar Regras no Launch para transmitir dados para o Adobe Experience Platform
- Saiba como integrar o Adobe Experience Platform Launch a uma página da Web
- Saiba como usar um fluxo de trabalho do Adobe Experience Platform para assimilar um arquivo CSV no Adobe Experience Platform

## Pré-requisitos

- Acesso ao Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acesso ao Adobe Experience Platform Launch: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Acesso ao [https://public.aepdemo.net](https://public.aepdemo.net)
- Acesso ao Postman

>[!IMPORTANT]
>
>Este tutorial foi criado para facilitar um formato específico de workshop. Ele usa sistemas e contas específicos aos quais você pode não ter acesso. Mesmo sem acesso, achamos que você ainda pode aprender muito lendo esse conteúdo muito detalhado. Se você participar de um dos workshops e precisar de suas credenciais de acesso, entre em contato com o representante do Adobe, que fornecerá as informações necessárias.

## Visão geral da arquitetura

Consulte a arquitetura abaixo, que destaca os componentes que serão discutidos e usados neste módulo.

![Visão geral da arquitetura](../../assets/images/architecturem2.png)

## Sandbox para usar

Para este módulo, use esta sandbox: `--module2sandbox--`.

>[!NOTE]
>
>Não se esqueça de instalar, configurar e usar a Extensão do Chrome, conforme referenciado em [0.1 - Instalar a extensão do Chrome para a documentação do Experience League](../module0/ex1.md)

## Exercícios

[2.1 Explorar o site](./ex1.md)

Neste exercício, você explorará o site que usará como parte dessa ativação.

[2.2 Configurar esquemas e definir identificadores](./ex2.md)

Neste exercício, você configurará os esquemas XDM necessários para capturar informações de perfil e comportamento do cliente. Em cada esquema XDM, também será necessário configurar um identificador principal para vincular todas as informações.

[2.3 Configurar conjuntos de dados](./ex3.md)

Neste exercício, você recuperará os conjuntos de dados necessários para capturar e armazenar informações de perfil e o comportamento do cliente.

[2.4 Assimilação de dados de fontes offline](./ex4.md)

Neste exercício, você irá ao site e ao aplicativo móvel e se comportará como um cliente, transmitindo dados para a plataforma.

[2.5 Zona de aterrissagem de dados](./ex5.md)

Configure seu conector de Origem da Zona de Aterrissagem de Dados com o armazenamento do Azure Blob.

[Resumo e benefícios](./summary.md)

Resumo deste módulo e visão geral dos benefícios.

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender tudo o que há para saber sobre a Adobe Experience Platform. Se você tiver dúvidas, queira compartilhar comentários gerais de suas sugestões sobre conteúdo futuro, entre em contato diretamente com Wouter Van Geluwe, enviando um email para **vangeluw@adobe.com**.

[Voltar para todos os módulos](../../overview.md)
