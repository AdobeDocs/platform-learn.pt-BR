---
title: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101
description: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 587be8bc-8ebe-4f30-99d8-ba88ce40caf7
source-git-commit: ead28f5631fc430c41e8c756b23dc69ffe19510e
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 0%

---

# 4.1 Customer Journey Analytics 101

## Objetivos

- Entender o serviço de aplicativo CJA
- Saiba como posicionar o CJA
- Entenda o fluxo de trabalho do CJA: da conexão de dados para insights

## 4.1.1 O que é o Customer Journey Analytics?

O Customer Journey Analytics (CJA) fornece um kit de ferramentas para as equipes de business intelligence e de ciência de dados para compilar e analisar dados entre canais (online e offline). Os recursos no CJA fornecem contexto e clareza para a complexa jornada do cliente de vários canais. O contexto fornecido leva a um insight acionável sobre a remoção de pontos problemáticos do processo de conversão do cliente, além de projetar e fornecer experiências excepcionais para os momentos mais importantes.

O CJA traz o Analysis Workspace para cima do Adobe Experience Platform. O Adobe Experience Platform é o cérebro para comunicação e orquestração e, com o CJA, as marcas agora podem contextualizar e visualizar todos esses dados, para que as equipes de negócios e de Insight possam aprender com isso ao analisar toda a jornada de clientes online para offline.

As equipes de negócios e de Insight podem conversar com o CJA, fazer perguntas e obter respostas rapidamente com a interface do usuário do Analysis Workspace que pode ser usada para arrastar e soltar, apontar e clicar.

![demonstração](./images/cja-adv-analysis1.png)

## 4.1.2 Principais vantagens

Os três principais benefícios para os clientes são:

- A capacidade de disponibilizar insights para todos (ou seja, democratizando o acesso aos dados)
- A capacidade de ver o cliente em uma jornada contextual (ou seja, os dados podem ser visualizados sequencialmente, abrangendo vários canais online e offline)
- A capacidade de aproveitar o poder dos dados sem a necessidade de (ou seja, permite que os humanos usem dados para explorar análises e insights profundos para ativação de marketing)

## 4.1.3 Por que escolher o Customer Journey Analytics?

O CJA não se destina a substituir um aplicativo de BI atual, como Power BI, Microestratégia, Locker ou Tableau. Esses aplicativos de BI são destinados a visualizar dados para criar painéis corporativos, de modo que todos em uma organização possam visualizar rapidamente métricas importantes.\
O objetivo do CJA é trazer o poder de análise para as equipes de negócios e de marketing, tornando-o uma ferramenta de análise &quot;obrigatória&quot; para essas personas.

Tradicionalmente, os aplicativos de BI são incapazes de permitir verdadeira inteligência do cliente:

- Eles não podem fazer atribuição e não fazem análise de jornada do cliente.
- Os aplicativos de BI precisam conhecer a questão com antecedência
- As consultas interativas são limitadas pela estrutura do banco de dados
- Habilidades SQL são necessárias.
- Os aplicativos de BI não dão a capacidade de perguntar por que algo aconteceu.
- Os aplicativos de BI não têm conexão direta com pontos de contato do cliente.

Por causa do acima, os usuários e analistas empresariais atingem os becos sem saída quase imediatamente, tornando a análise cara, lenta, inflexível e desconectada dos sistemas de ação.

Com o CJA, você pode ter uma visão 360 da jornada do cliente, usando dados offline e online, com as ferramentas certas para reduzir o tempo de insight, tornando os usuários de negócios independentes em entender por que algo aconteceu e como responder a ele.

![demonstração](./images/cja-use-case.png)

## 4.1.4 Entender o fluxo de trabalho do Customer Journey Analytics

Antes de iniciar os próximos exercícios, é importante entender quais etapas são necessárias para trazer dados do Adobe Experience Platform para o CJA, a fim de visualizá-los e obter alguns insights profundos. É o que chamamos de fluxo de trabalho do CJA. Vamos dar uma olhada nisso:

![demonstração](./images/cja-work-flow.jpg)

Antes de iniciar as etapas acima, não se esqueça da etapa 0, que é entender os dados disponíveis no Adobe Experience Platform.

**Lixo dentro, lixo fora.** Lembra? Você deve ter uma ideia clara de quais dados estão disponíveis e como os schemas no Adobe Experience Platform são configurados. Entender os dados no Adobe Experience Platform facilitará as coisas, não apenas na parte da conexão de dados, mas também ao criar visualizações e fazer análise.

## 4.1.5 Passo 0: Noções básicas sobre esquemas e conjuntos de dados do Adobe Experience Platform

Faça logon no Adobe Experience Platform acessando este URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer logon, você será direcionado para a página inicial do Adobe Experience Platform.

![Assimilação de dados](../uc1/images/home.png)

Antes de continuar, é necessário selecionar um **sandbox**. A sandbox a ser selecionada é chamada de ``Bootcamp``. Você pode fazer isso clicando no texto **[!UICONTROL Prod]** no canto superior direito da tela. Depois de selecionar a sandbox apropriada, você verá a tela mudar e agora estará na sandbox dedicada.

![Assimilação de dados](../uc1/images/sb1.png)

Consulte esses esquemas e conjuntos de dados no Adobe Experience Platform.

| Conjunto de dados | Esquema |
| ----------------- |-------------| 
| Sistema de demonstração - Conjunto de dados do evento para site (Global v1.1) | Sistema de demonstração - Esquema de evento para site (Global v1.1) |
| Sistema de demonstração - Conjunto de dados de eventos para Central de chamadas (Global v1.1) | Sistema de demonstração - Esquema de evento para Central de chamadas (Global v1.1) |
| Sistema de demonstração - Conjunto de dados de eventos para assistentes de voz (Global v1.1) | Sistema de demonstração - Esquema de evento para assistentes de voz (Global v1.1) |

Certifique-se de ter verificado pelo menos coisas como:

- Identidades: CRMID, phoneNumber, ECID, email. Quais identidades são os identificadores primários, quais são os identificadores secundários?
Você pode encontrar os identificadores abrindo um esquema e observando o objeto `_experienceplatform.identification.core`. Verificar o esquema [Sistema de demonstração - Esquema de evento para site (Global v1.1)](https://experience.adobe.com/platform/schema).

![demonstração](./images/identity.png)

- Explore o objeto de comércio dentro do esquema [Sistema de demonstração - Esquema de evento para site (Global v1.1)](https://experience.adobe.com/platform/schema).

![demonstração](./images/commerce.png)

- Visualize todas as [conjuntos de dados](https://experience.adobe.com/platform/dataset/browse?limit=50&amp;page=1&amp;sortDescending=1&amp;sortField=created) e analisar os dados

Agora você está pronto para começar a usar a interface do usuário do Customer Journey Analytics.

Próxima etapa: [4.2 Conectar conjuntos de dados do Adobe Experience Platform no Customer Journey Analytics](./ex2.md)

[Voltar para Fluxo de Usuário 4](./uc4.md)

[Voltar para todos os módulos](../../overview.md)
