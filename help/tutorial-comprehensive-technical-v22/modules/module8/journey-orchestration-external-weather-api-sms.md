---
title: Adobe Journey Optimizer - API de tempo externo, ação de SMS e muito mais
description: Adobe Journey Optimizer - API de tempo externo, ação de SMS e muito mais
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7f3d6dcb-845d-4ff1-97c3-8e93b8d2c624
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---

# 8. Adobe Journey Optimizer: Fontes de dados externas e ações personalizadas

**Autor: [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Neste módulo, você usará o Adobe Journey Optimizer para acompanhar o comportamento do cliente, tanto online quanto offline, e responder a ele de forma inteligente, contextual e em tempo real. Você já teve uma experiência prática inicial com o Adobe Journey Optimizer no Módulo 6. Neste exercício, você vai se aprofundar um pouco e explorar um caso de uso mais avançado no qual fontes de dados externas são usadas como parte de uma jornada.

## Objetivos de aprendizagem

- Saiba como criar eventos, fontes de dados externas e jornadas no Adobe Journey Optimizer
- Saiba como consumir informações meteorológicas da API Open Weather
- Saiba como usar destinos de ação personalizados, como Twilio e Slack, do Adobe Journey Optimizer

## Pré-requisitos

- Acesso ao Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acesso ao Adobe Journey Optimizer
- Acesso à API Open Weather

>[!IMPORTANT]
>
>Este tutorial foi criado para facilitar um formato específico de workshop. Ele usa sistemas e contas específicos aos quais você pode não ter acesso. Mesmo sem acesso, achamos que você ainda pode aprender muito lendo esse conteúdo muito detalhado. Se você participar de um dos workshops e precisar de suas credenciais de acesso, entre em contato com o representante do Adobe, que fornecerá as informações necessárias.

## Visão geral da arquitetura

Consulte a arquitetura abaixo, que destaca os componentes que serão discutidos e usados neste módulo.

![Visão geral da arquitetura](../../assets/images/architecturem12.png)

## Contexto comercial

Como marca, você tem investido muito na personalização de experiências online. Agora, você deseja ser tão contextual e relevante para experiências offline.
Neste módulo, você usará a presença de um cliente em uma loja offline para fornecer uma experiência personalizada dentro da loja, exibindo o conteúdo relevante para esse cliente em nossas telas na loja e, ao mesmo tempo, queremos fornecer uma mensagem de push ou SMS personalizada para esse mesmo cliente, tudo em tempo real.
Como marca, você também entende que o contexto afeta muito o interesse de um cliente, de modo que deseja trazer as informações do tempo atual da localização do cliente para decidir qual conteúdo ou promoção exibir.

## Sandbox para usar

Para este módulo, use esta sandbox: `--aepSandboxId--`.

>[!NOTE]
>
>Não se esqueça de instalar, configurar e usar a Extensão do Chrome, conforme referenciado em [0.1 - Instalar a extensão do Chrome para a documentação do Experience League](../module0/ex1.md)

## Exercícios

[8.1 Definir um evento](./ex1.md)

Saiba como definir um evento personalizado usando o Adobe Journey Optimizer.

[8.2 Definir uma fonte de dados externa](./ex2.md)

Saiba como configurar uma fonte de dados externa usando o Adobe Journey Optimizer.

[8.3 Definir uma ação personalizada](./ex3.md)

Saiba como definir uma ação externa usando o Adobe Journey Optimizer.

[8.4 Criar sua jornada e mensagens](./ex4.md)

Combine eventos, fontes de dados e ações em uma jornada inteligente e contextual.

[8.5 Acione sua jornada](./ex5.md)

Acione sua jornada específica.

[Resumo e benefícios](./summary.md)

Resumo deste módulo e visão geral dos benefícios.

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender tudo o que há para saber sobre a Adobe Experience Platform. Se você tiver dúvidas, queira compartilhar comentários gerais de suas sugestões sobre conteúdo futuro, entre em contato diretamente com Wouter Van Geluwe, enviando um email para **vangeluw@adobe.com**.

[Voltar para todos os módulos](../../overview.md)
