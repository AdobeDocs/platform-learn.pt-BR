---
title: Serviço de query
description: Serviço de query
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 74943e52-8a7e-4db7-9407-7deeab008fa7
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 1%

---

# 4. Serviço de query

**Autores: [Marc Meewis](https://www.linkedin.com/in/marcmeewis/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Neste módulo, você obterá uma visualização prática do Serviço de query do Adobe Experience Platform. O Serviço de query permite executar consultas omnicanais em todos os dados de aplicativos do Adobe Experience Cloud, unindo e analisando dados no Adobe Campaign, Analytics, Audience Manager, Target e Advertising Cloud e outros dados de clientes carregados/inseridos no Adobe Experience Platform.

O Serviço de query é uma ferramenta sem servidor. Ele oferece suporte a consultas SQL e conectividade de vários aplicativos clientes por meio de sua compatibilidade com PostgreSQL.
Usaremos dados que foram inseridos na plataforma usando os Dados de interação da Web, as Interações do call center em combinação com os Dados de fidelidade do cliente carregados na plataforma.

## Objetivos de aprendizagem

- Familiarize-se com a interface do usuário do Adobe Experience Platform
- Conecte-se ao Serviço de Consulta e execute suas consultas SQL
- Explorar conjuntos de dados no Adobe Experience Platform
- Conecte o Tableau ou o Power BI ao Serviço de query da Adobe Experience Platform para criar visualizações e relatórios

## Pré-requisitos

- É preferível alguma familiaridade com o SQL, mas não é obrigatório
- Acesso ao Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Conjuntos de dados (conjunto de dados usado em laboratório, pré-carregado para você)
- PostgreSQL
- Tableau ou Microsoft Power BI Desktop
- **Baixar estes ativos**:
   - [JSON - Dados de exemplo: Interações do site](./../../assets/json/ee.json)
   - [JSON - Dados de exemplo: Interações da central de atendimento](./../../assets/json/callcenter.json)
   - [JSON - Dados de exemplo: Fidelidade](./../../assets/json/loyalty.json)

>[!IMPORTANT]
>
>Este tutorial foi criado para facilitar um formato específico de workshop. Ele usa sistemas e contas específicos aos quais você pode não ter acesso. Mesmo sem acesso, achamos que você ainda pode aprender muito lendo esse conteúdo muito detalhado. Se você participar de um dos workshops e precisar de suas credenciais de acesso, entre em contato com o representante do Adobe, que fornecerá as informações necessárias.

## Visão geral da arquitetura

Consulte a arquitetura abaixo, que destaca os componentes que serão discutidos e usados neste módulo.

![Visão geral da arquitetura](../../assets/images/architecturem7.png)

## Sandbox para usar

Para este módulo, use esta sandbox: `--module7sandbox--`.

>[!NOTE]
>
>Não se esqueça de instalar, configurar e usar a Extensão do Chrome, conforme referenciado em [0.1 - Instalar a extensão do Chrome para a documentação do Experience League](../module0/ex1.md)

## Exercícios

[Pré-requisitos 4.0](./ex0.md)

Você precisará instalar o PSQL para executar as consultas neste exercício de ativação. Dependendo do sistema operacional, será necessário instalar o Microsoft Power BI ou o Tableau. Os usuários do Windows podem escolher entre Power BI ou Tableau. Os usuários do Mac devem instalar o Tableau.

[4.1 Introdução](./ex1.md)

Neste exercício, você explorará a Interface do usuário do Adobe Experience Platform Query Service, aprenderá sobre conjuntos de dados, encontrará suas consultas e finalmente configurará uma conexão do PSQL.

[4.2 Uso do serviço de query](./ex2.md)

Neste exercício, você aprenderá sobre a sintaxe básica do Serviço de query e poderá identificar os atributos do esquema XDM em sua query.

[4.3 Consultas, consultas, consultas... e análise de churn](./ex3.md)

Neste exercício, você fará consultas, aprenderá sobre as funções definidas pelo Adobe enquanto faz alguma análise de rotatividade. No final disso, você gravará um query para preparar um conjunto de dados para uso no Microsoft Power BI.

[4.4 Gerar um conjunto de dados a partir de um query](./ex4.md)

Neste exercício, você gerará um conjunto de dados de um query executado no anterior e usará esse conjunto de dados nos próximos exercícios.

[4.5 Serviço e Power BI de query](./ex5.md)

Neste exercício, você se conectará ao Adobe Experience Platform e ao Serviço de query para executar a Análise de interação do Callcenter.

[4.6 Serviço de consulta e Tableau](./ex6.md)

Neste exercício, você conectará o Tableau à Adobe Experience Platform e ao Serviço de query para executar a Análise de interação do Callcenter.

[4.7 API do serviço de consulta](./ex7.md)

Neste exercício, você usará a API do Serviço de query para gerenciar templates de query e agendamentos de query.

[Resumo e benefícios](./summary.md)

Resumo deste módulo e visão geral dos benefícios.

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender tudo o que há para saber sobre a Adobe Experience Platform. Se você tiver dúvidas, queira compartilhar comentários gerais de suas sugestões sobre conteúdo futuro, entre em contato diretamente com Wouter Van Geluwe, enviando um email para **vangeluw@adobe.com**.

[Voltar para todos os módulos](../../overview.md)
