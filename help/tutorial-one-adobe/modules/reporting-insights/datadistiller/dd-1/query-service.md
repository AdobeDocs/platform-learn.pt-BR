---
title: Serviço de consultas
description: Serviço de consultas
kt: 5342
doc-type: tutorial
exl-id: 881dcff5-3637-4b67-9e61-88690babe83b
source-git-commit: 5eb5432251ee7193909ed4ec7decd0d94d0843a2
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 1%

---

# 2.1 Serviço de consulta

Neste módulo, você obterá uma visualização prática do Serviço de consulta da Adobe Experience Platform. O Serviço de consulta permite realizar consultas omnicanal em todos os dados de aplicativos da Adobe Experience Cloud, unindo e analisando dados no Adobe Campaign, Analytics, Audience Manager, Target e Advertising Cloud e outros dados de clientes carregados/inseridos no Adobe Experience Platform.

O Serviço de consulta é uma ferramenta sem servidor. Ele suporta queries SQL e conectividade de vários aplicativos cliente através de sua compatibilidade PostgreSQL.
Usaremos dados que foram inseridos na plataforma usando dados de interação na Web e interações da central de atendimento em combinação com dados de fidelidade do cliente carregados na plataforma.

## Objetivos de aprendizagem

- Familiarizar-se com a interface do usuário do Adobe Experience Platform
- Conectar-se ao Serviço de consulta e executar suas consultas SQL
- Explorar conjuntos de dados na Adobe Experience Platform
- Conecte o Tableau ou o Power BI ao Serviço de consulta da Adobe Experience Platform para criar visualizações e relatórios

## Pré-requisitos

- Alguma familiaridade com o SQL é preferível, mas não é necessária
- Acesso ao Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Conjuntos de dados (conjunto de dados usado durante o laboratório, pré-carregado para você)
- PostgreSQL
- Desktop Tableau ou Microsoft Power BI

>[!NOTE]
>
>Não se esqueça de instalar, configurar e usar a Extensão do Chrome, conforme referenciado em [Instalar a extensão do Chrome para a documentação do Experience League](../../../getting-started/gettingstarted/ex1.md)

## Exercícios

[2.1.1 Pré-requisitos](./ex1.md)

Será necessário instalar o PSQL para executar os queries neste exercício de ativação. Dependendo do sistema operacional, será necessário instalar o Microsoft Power BI ou o Tableau. Os usuários do Windows podem escolher entre Power BI ou Tableau. Os usuários do Mac devem instalar o Tableau.

[2.1.2 Introdução](./ex2.md)

Neste exercício, você explorará a interface do usuário do serviço de consulta da Adobe Experience Platform, aprenderá sobre conjuntos de dados, localizará suas consultas e finalmente configurará uma conexão do PSQL.

[2.1.3 Uso do Serviço de consulta](./ex3.md)

Neste exercício, você aprenderá sobre a sintaxe básica do Serviço de consulta e poderá identificar os atributos do esquema XDM na sua consulta.

[2.1.4 Consultas, consultas, consultas... e análise de churn](./ex4.md)

Neste exercício, você fará consultas e aprenderá sobre as Funções definidas pelo Adobe ao fazer algumas análises de churn. No final disso, você escreverá um query para preparar um conjunto de dados para uso no Microsoft Power BI.

[2.1.5 Gerar um conjunto de dados a partir de um query](./ex5.md)

Neste exercício, você gerará um conjunto de dados a partir de uma consulta executada no anterior e usará esse conjunto de dados nos próximos exercícios.

[2.1.6 Serviço de consulta e Power BI](./ex6.md)

Neste exercício, você conectará o Power BI ao Adobe Experience Platform e ao Serviço de consulta para executar a Análise de interação do Callcenter.

[2.1.7 Serviço de consulta e Tableau](./ex7.md)

Neste exercício, você conectará o Tableau ao Adobe Experience Platform e ao Serviço de consulta para executar a Análise de interação do Callcenter.

[2.1.8 API do serviço de consulta](./ex8.md)

Neste exercício, você usará a API do Serviço de consulta para gerenciar modelos de consulta e agendamentos de consulta.

[Resumo e benefícios](./summary.md)

Resumo desse módulo e visão geral dos benefícios.

![Informantes técnicos](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo tudo o que há para saber sobre o Adobe Experience Platform e seus aplicativos. Em caso de dúvidas, envie um email para **techinsiders@adobe.com** para compartilhar comentários gerais sobre sugestões para conteúdo futuro. Entre em contato diretamente com o Tech Insiders.

[Voltar a todos os módulos](./../../../../overview.md)
