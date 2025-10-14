---
title: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101
description: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
exl-id: 587be8bc-8ebe-4f30-99d8-ba88ce40caf7
source-git-commit: 901b90ca165a74bbc4f871469222064b70d0a20a
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---

# 4.1 Customer Journey Analytics 101

## Objetivos

- Entender o aplicativo do CJA
- Saiba como posicionar o CJA
- Entender o fluxo de trabalho do CJA: da conexão de dados aos insights

## 4.1.1 O que é o Customer Journey Analytics?

O Customer Journey Analytics (CJA) fornece um kit de ferramentas para as equipes de business intelligence e ciência de dados para compilar e analisar dados entre canais (online e offline). Os recursos no CJA fornecem contexto e clareza para a complexa jornada de clientes multicanal. O contexto fornecido leva a um insight acionável sobre como remover pontos problemáticos do processo de conversão do cliente e projetar e fornecer experiências excepcionais para os momentos mais importantes.

O CJA traz a Analysis Workspace para cima da Adobe Experience Platform. O Adobe Experience Platform é o cérebro para comunicação e orquestração e, com o CJA, as marcas agora podem contextualizar e visualizar todos esses dados, para que as equipes de negócios e insights possam aprender com eles, analisando a jornada completa online para offline do cliente.

As equipes de negócios e insights podem conversar com o CJA, fazer perguntas e obter respostas imediatamente com a interface de usuário amigável, baseada em arrastar e soltar, apontar e clicar do Analysis Workspace.

![demonstração](./images/cja-adv-analysis1.png)

## 4.1.2 Principais vantagens

Os três principais benefícios para os clientes são:

- A capacidade de disponibilizar insights para todos (ou seja, democratização do acesso aos dados)
- A capacidade de ver o cliente em uma jornada contextual (ou seja, os dados podem ser visualizados sequencialmente, abrangendo vários canais online e offline)
- A capacidade de aproveitar o potencial dos dados sem a necessidade de (ou seja, permite que os seres humanos usem os dados para explorar análises e insights profundos para ativação de marketing)

## 4.1.3 Por que escolher o Customer Journey Analytics?

O CJA não tem como objetivo substituir um aplicativo de BI atual, como Power BI, Microstrategy, Locker ou Tableau. Esses aplicativos de BI são destinados a visualizar dados para criar painéis corporativos, de modo que todos em uma organização possam observar rapidamente métricas importantes.\
O objetivo do CJA é trazer o poder de análise para as equipes de marketing e negócios, tornando-o uma ferramenta de análise &quot;obrigatório&quot; para essas personas.

Tradicionalmente, os aplicativos de BI não eram capazes de ativar a verdadeira inteligência do cliente:

- Eles não podem fazer atribuição e não fazem análise de jornada do cliente.
- Os aplicativos de BI precisam saber a pergunta antecipadamente
- As consultas interativas são limitadas pela estrutura do banco de dados
- Habilidades SQL são necessárias.
- Os aplicativos de BI não permitem que você pergunte por que algo aconteceu.
- Os aplicativos de BI não têm conexão direta com os pontos de contato do cliente.

Por causa disso, usuários empresariais e analistas perdem os limites quase imediatamente, tornando a análise cara, lenta, inflexível e desconectada dos sistemas de ação.

Com o CJA, você pode ter uma visão 360 da jornada do cliente, usando dados offline e online, com as ferramentas certas para reduzir o tempo de insight, tornando os usuários empresariais independentes para entender por que algo aconteceu e como responder a isso.

![demonstração](./images/cja-use-case.png)

## 4.1.4 Compreender o fluxo de trabalho do Customer Journey Analytics

Antes de iniciar os próximos exercícios, é fundamental entender quais etapas são necessárias para trazer dados do Adobe Experience Platform para o CJA, a fim de visualizá-los e obter alguns insights profundos. É o que chamamos de Fluxo de trabalho do CJA. Vamos dar uma olhada:

![demonstração](./images/cja-work-flow.jpg)

Antes de iniciar as etapas acima, não se esqueça da etapa 0, que é entender os dados disponíveis no Adobe Experience Platform.

**Lixo entra, lixo sai.** Lembrar? Você deve ter uma ideia clara de quais dados estão disponíveis e como os esquemas no Adobe Experience Platform são configurados. Entender os dados que estão no Adobe Experience Platform facilitará as coisas, não apenas na parte da conexão de dados, mas também ao criar visualizações e fazer análises.

## 4.1.5 Etapa 0: Noções básicas sobre esquemas e conjuntos de dados do Adobe Experience Platform

Faça logon no Adobe Experience Platform acessando esta URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](../uc1/images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``Bootcamp``. Você pode fazer isso clicando no texto **[!UICONTROL Prod]** no canto superior direito da tela. Depois de selecionar a sandbox apropriada, você verá a alteração da tela e agora estará em sua sandbox dedicada.

![Assimilação de dados](../uc1/images/sb1.png)

Consulte esses esquemas e conjuntos de dados na Adobe Experience Platform.

| Conjunto de dados | Esquema |
| ----------------- |-------------| 
| Sistema de demonstração - Conjunto de dados de evento para site (Global v1.1) | Sistema de demonstração - Esquema de evento para site (Global v1.1) |
| Sistema de demonstração - Conjunto de dados de evento para call center (Global v1.1) | Sistema de demonstração - Esquema de evento para call center (Global v1.1) |
| Sistema de demonstração - Conjunto de dados de evento para assistentes de voz (Global v1.1) | Sistema de demonstração - Esquema de evento para assistentes de voz (Global v1.1) |

Verifique pelo menos itens como:

- Identidades: CRMID, phoneNumber, ECID, email. Quais identidades são os identificadores principais, quais são os identificadores secundários?
Você pode encontrar os identificadores abrindo um esquema e observando o objeto `_experienceplatform.identification.core`. Consulte o esquema [Sistema de demonstração - Esquema de evento para o site (Global v1.1)](https://experience.adobe.com/platform/schema).

![demonstração](./images/identity.png)

- Explore o objeto de comércio dentro do esquema [Sistema de demonstração - Esquema de evento para o site (Global v1.1)](https://experience.adobe.com/platform/schema).

![demonstração](./images/commerce.png)

- Visualize todos os [conjuntos de dados](https://experience.adobe.com/platform/dataset/browse?limit=50&page=1&sortDescending=1&sortField=created) e examine os dados

Agora você está pronto para começar a usar a interface do usuário do Customer Journey Analytics.

Próxima etapa: [4.2 Conectar Conjuntos de Dados do Adobe Experience Platform no Customer Journey Analytics](./ex2.md)

[Voltar para Fluxo de Usuário 4](./uc4.md)

[Voltar a todos os módulos](../../overview.md)
