---
title: Serviços inteligentes
description: Serviços inteligentes
kt: 5342
audience: Data Engineer, Data Architect, Data Scientist
doc-type: tutorial
activity: develop
exl-id: 99b56722-95bf-4c51-b4d6-8b5a8e5fd936
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 3%

---

# 5. Serviços inteligentes

**Autores: [Diptiman Badajena](https://www.linkedin.com/in/diptiman-badajena-1b178019/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Neste módulo, você aprenderá a configurar, configurar e usar os Serviços inteligentes Adobe Experience Platform.

## Objetivos de aprendizagem

- Familiarize-se com o Adobe Experience Platform
- Configurar esquema/conjunto de dados para usar com os Serviços inteligentes
- Criar uma nova instância do Customer AI
- Painel de pontuação e segmentação

## Pré-requisitos

- Acesso ao Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)

>[!IMPORTANT]
>
>Este tutorial foi criado para facilitar um formato específico de workshop. Ele usa sistemas e contas específicos aos quais você pode não ter acesso. Mesmo sem acesso, achamos que você ainda pode aprender muito lendo esse conteúdo muito detalhado. Se você participar de um dos workshops e precisar de suas credenciais de acesso, entre em contato com o representante do Adobe, que fornecerá as informações necessárias.

## Visão geral da arquitetura

Consulte a arquitetura abaixo, que destaca os componentes que serão discutidos e usados neste módulo.

![Visão geral da arquitetura](../../assets/images/architecturem5.png)

## Sandbox para usar

Para este módulo, use esta sandbox: `--module10sandbox--`.

>[!NOTE]
>
>Não se esqueça de instalar, configurar e usar a Extensão do Chrome, conforme referenciado em [0.1 - Instalar a extensão do Chrome para a documentação do Experience League](../module0/ex1.md)

## Exercícios

[5.1 AI do cliente - Preparação de dados (Assimilar)](./ex1.md)

Os dados do cliente são assimilados e transformados com o Experience Data Model (XDM) no Adobe Experience Platform. Especificamente, todos os conjuntos de dados que são usados nos Serviços inteligentes devem estar em conformidade com o esquema XDM Consumer ExperienceEvent (CEE).

[5.2 Customer AI - Criar uma nova instância (Configurar)](./ex2.md)

O analista de marketing configura as previsões desejadas especificando regras de negócios e identificando dados relevantes. Após configurar o modelo, agende as execuções e as pontuações de revisão.

[5.3 Customer AI - Painel de pontuação e segmentação (Predict &amp; Take Action)](./ex3.md)

Depois que os modelos terminarem o treinamento e a pontuação, as pontuações serão gravadas de volta na Platform. Você pode decidir quais ações tomar com as previsões, como definir segmentos, criar painéis personalizados etc.

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender tudo o que há para saber sobre a Adobe Experience Platform. Se você tiver dúvidas, queira compartilhar comentários gerais de suas sugestões sobre conteúdo futuro, entre em contato diretamente com Wouter Van Geluwe, enviando um email para **vangeluw@adobe.com**.

[Voltar para todos os módulos](../../overview.md)
