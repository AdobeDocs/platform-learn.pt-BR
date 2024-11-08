---
title: Assimilar e analise dados do Google Analytics no Adobe Experience Platform com o conector Source do BigQuery
description: Assimilar e analise dados do Google Analytics no Adobe Experience Platform com o conector Source do BigQuery
kt: 5342
doc-type: tutorial
source-git-commit: f19f6b4a44a34af3c9545eb7f8735ef6ccf5d6c7
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 4.2 Assimilar e analisar dados do Google Analytics no Adobe Experience Platform com o conector Source do BigQuery

**Autores: [Victor de la Iglesia](https://www.linkedin.com/in/victordelaiglesia/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Neste módulo, você configurará sua própria instância da Google Cloud Platform, carregará dados de amostra na Google Cloud Platform e usará o BigQuery Source Connector para assimilar esses dados da Google Cloud Platform na Adobe Experience Platform. Por fim, você usará o Customer Journey Analytics para visualizar esses dados.

Os conectores do Source no Adobe Experience Platform facilitam o processo de entrada de dados no Adobe Experience Platform. O Google BigQuery é um dos conectores já disponíveis. Graças ao Adobe Experience Platform e ao Conector BigQuery Source, agora podemos trazer dados Google Analytics para o Analysis Workspace no Customer Journey Analytics.

Além disso, podemos enriquecer esses dados do Google Analytics unindo-os a outras fontes de dados, como CRM, Call Center ou dados de fidelidade no Customer Journey Analytics.

## Objetivos de aprendizagem

- Familiarize-se com a Google Cloud Platform e a interface do usuário do BigQuery
- Assimilar dados do Google Analytics no Adobe Experience Platform
- Usar Customer Journey Analytics para executar análise de dados de Google Analytics
- Enriquecer dados do Google Analytics com dados offline

## Pré-requisitos

- Alguma familiaridade com o Customer Journey Analytics é preferível, mas não é obrigatória
- Acesso ao Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acesso ao Customer Journey Analytics
- Acesso à Google Cloud Platform e ao Google BigQuery
- **Baixar estes ativos**:
   - [JSON - Dados de amostra: Dados de fidelidade](./../../../assets/json/bqLoyalty.json)

>[!NOTE]
>
>Não se esqueça de instalar, configurar e usar a Extensão do Chrome, conforme referenciado em [0.1 - Instalar a extensão do Chrome para a documentação do Experience League](../../gettingstarted/gettingstarted/ex1.md)

## Exercícios

[4.2.1 Criar sua conta da Google Cloud Platform](./ex1.md)

Crie sua conta da Google Cloud Platform.

[4.2.2 Crie sua primeira consulta no BigQuery](./ex2.md)

Saiba como usar o BigQuery para preparar os dados para carregamento na Platform.

[4.2.3 Conectar o GCP e o BigQuery ao Adobe Experience Platform](./ex3.md)

Saiba como configurar o conector de origem no Adobe Experience Platform.

[4.2.4 Carregar dados do BigQuery no Adobe Experience Platform](./ex4.md)

Saiba como configurar o conector de origem do BigQuery no Adobe Experience Platform para assimilar seus dados de Google Analytics.

[4.2.5 Analisar dados do Google Analytics usando o Customer Journey Analytics](./ex5.md)

Saiba como analisar dados de Google Analytics no Customer Journey Analytics e combiná-los com dados de fidelidade.

[Resumo e benefícios](./summary.md)

Resumo desse módulo e visão geral dos benefícios.

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo tudo o que há para saber sobre o Adobe Experience Platform e seus aplicativos. Em caso de dúvidas, envie um email para **techinsiders@adobe.com** para compartilhar comentários gerais sobre sugestões para conteúdo futuro. Entre em contato diretamente com o Tech Insiders.

[Voltar a todos os módulos](../../../overview.md)
