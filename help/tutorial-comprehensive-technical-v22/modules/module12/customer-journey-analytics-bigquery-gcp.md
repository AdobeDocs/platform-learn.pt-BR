---
title: Assimilar e analisar dados do Google Analytics no Adobe Experience Platform com o Conector de fonte BigQuery
description: Assimilar e analisar dados do Google Analytics no Adobe Experience Platform com o Conector de fonte BigQuery
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: c9c28b5a-d158-49fa-9533-1a295876f6c4
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 2%

---

# 12. Assimilar e analisar dados do Google Analytics no Adobe Experience Platform com o Conector de fonte BigQuery

**Autores: [Victor de la Iglesia](https://www.linkedin.com/in/victordelaiglesia/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Neste módulo, você configurará sua própria instância da Google Cloud Platform, carregará dados de amostra na Google Cloud Platform e usará o BigQuery Source Connector para assimilar esses dados da Google Cloud Platform no Adobe Experience Platform. Por fim, você usará o Customer Journey Analytics para visualizar esses dados.

Os conectores de origem no Adobe Experience Platform facilitam o processo de inserção de dados no Adobe Experience Platform. O Google BigQuery é um dos conectores já disponíveis. Graças ao Adobe Experience Platform e ao BigQuery Source Connector, agora podemos trazer dados do Google Analytics para o Analysis Workspace no Customer Journey Analytics.

Além disso, podemos enriquecer esses dados do Google Analytics ao uni-los a outras fontes de dados, como CRM, Call Center ou dados de fidelidade no Customer Journey Analytics.

## Objetivos de aprendizagem

- Familiarize-se com a Google Cloud Platform e a interface do usuário BigQuery
- Assimilar dados do Google Analytics na Adobe Experience Platform
- Use o Customer Journey Analytics para executar análise de dados do Google Analytics
- Enriquecer dados Google Analytics com dados offline

## Pré-requisitos

- É preferível alguma familiaridade com o Customer Journey Analytics, mas não é obrigatório
- Acesso ao Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acesso ao Customer Journey Analytics
- Acesso à Google Cloud Platform e ao Google BigQuery
- **Baixar estes ativos**:
   - [JSON - Dados de exemplo: Dados de fidelidade](./../../assets/json/bqLoyalty.json)

>[!IMPORTANT]
>
>Este tutorial foi criado para facilitar um formato específico de workshop. Ele usa sistemas e contas específicos aos quais você pode não ter acesso. Mesmo sem acesso, achamos que você ainda pode aprender muito lendo esse conteúdo muito detalhado. Se você participar de um dos workshops e precisar de suas credenciais de acesso, entre em contato com o representante do Adobe, que fornecerá as informações necessárias.

## Visão geral da arquitetura

Consulte a arquitetura abaixo, que destaca os componentes que serão discutidos e usados neste módulo.

![Visão geral da arquitetura](../../assets/images/architecturem16.png)

## Sandbox para usar

Para este módulo, use esta sandbox: `--aepSandboxId--`.

>[!NOTE]
>
>Não se esqueça de instalar, configurar e usar a Extensão do Chrome, conforme referenciado em [0.1 - Instalar a extensão do Chrome para a documentação do Experience League](../module0/ex1.md)

## Exercícios

[12.1 Criar a conta da Google Cloud Platform](./ex1.md)

Crie a conta da Google Cloud Platform.

[12.2 Criar sua primeira query no BigQuery](./ex2.md)

Saiba como usar o BigQuery para preparar os dados para carregar no Platform.

[12.3 Conectar GCP e BigQuery ao Adobe Experience Platform](./ex3.md)

Saiba como configurar o conector de origem no Adobe Experience Platform.

[12.4 Carregar dados do BigQuery no Adobe Experience Platform](./ex4.md)

Saiba como configurar o conector de origem BigQuery no Adobe Experience Platform para assimilar seus dados do Google Analytics.

[12.5 Analisar dados do Google Analytics usando o Customer Journey Analytics](./ex5.md)

Saiba como analisar dados do Google Analytics no Customer Journey Analytics e combiná-los com dados de fidelidade.

[Resumo e benefícios](./summary.md)

Resumo deste módulo e visão geral dos benefícios.

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender tudo o que há para saber sobre a Adobe Experience Platform. Se você tiver dúvidas, queira compartilhar comentários gerais de suas sugestões sobre conteúdo futuro, entre em contato diretamente com Wouter Van Geluwe, enviando um email para **vangeluw@adobe.com**.

[Voltar para todos os módulos](../../overview.md)
