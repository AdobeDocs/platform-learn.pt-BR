---
title: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101 - Brasil
description: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101 - Brasil
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 3272d288185415b4604fe48f18c19f8f06e6dce0
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# 4.1 Customer Journey Analytics 101

## Objetivos

- Entenda o que é o CJA
- Entenda qual é o papel do CJA
- Entenda o workflow do CJA: da conexão de dados aos insights

## 4.1.1 O que é o Customer Journey Analytics?

O Customer Journey Analytics (CJA) fornece uma interface em que os tempos de Analytics, Negócios e Tecnologia conseguem unir todos os dados da companhia e analisar uma jornada entre canais (online e offline) ponta cliente de ponta. O CJA é capaz de fornecer e clareza para essa jornada, trazendo uma visão acionável em dificuldades sem processo de conversão e possibilidades oitandos pontos.

O traz CJA no Analysis Workspace conectado à Adobe Experience Platform. Um Adobe Experience Platform é o comunicação e da orquestração e, com o CJA, como Marcas podem contextualização e visualizar todos esses dados, para que as equipes de negócios e insights possam Analando hoje uma jornada on line para offline do cliente.

Como equipes de negócios e insights podem conversar com o CJA, &quot;fazer perguntas e respostas em real com a interface do usuário de arrastar e soltar, apontar e tempo e passo de usar usar a Analysis Workspace.

![demonstração](./images/cja-adv-analysis1.png)

## 4.1.2 vantagens Principais

Os três principais benefícios para os clientes são:

- Um acordo para todos, ou ainda, democracia, o calendário dos disponibilizar.
- Um acordo de ver o cliente em uma jornada contextual (ou, os dados podem ser visualizados encialmente, abrangendo múltiplos on-line e off-line).
- Um acordo de aproveitar o poder de um necessidade (ou, permite que indivíduos usem para desbloquear insights e análises das para ativação de).

## 4.1.3 ## 4.1.3 Por que escolher o Customer Journey Analytics?

O CJA não se destina a substituir um aplicativo de BI atualidade, como Power BI, Locker ou Tableau. O as usas aplicativos de BI são visualizar corporais para possam para que objetivo um painéis, rapidamente métricas. importantes. O objetivo JJA é trazer de análise para as equipes de Marketing Negócios, tornando-o da análise obrigatória.



Tradicionalmente, os aplicativos de BI têm incapazes de permitir uma verdadeira inteligente clientes:

- Eles não podem &quot;fazer atribuição e não fazem de jornada do cliente.
- Os aplicativos de BI precisam sabre a pergunta com antecedência
- Como consultas interativas são limitadas estrutura do banco de dados
- Habilidades de SQL são necessárias.
- Os aplicativos de BI permitem que você pergun te o de acontecimento.
- Os aplicativos de BI conexão direta com os de não é.

Portanto, usuários de negócios e analistas chegam a becos sem saída imediatamente, tornando uma análise cara, lenta, flexível e desconectada dos sistemas de ação.

Com o Cvocê pode ter uma visão Jjornada do cliente, usando fline e online, com as certas para reduzir o tempo de insight, tornando os usuários de negócios para o que respondem a isso.

![demonstração](./images/cja-use-case.png)

## 4.1.4 Compreensão do fluxo do trabalho do Customer Journey Analytics

Antes de os exercícios, é Adobe Experience Platform para os necessárias para o Cos Jalizá-los alguns insights. É o que chamamos de fluxo de trabalho do CJA. Vamos verificar:

![demonstração](./images/cja-work-flow.jpg)

Antes de etapas, não se esqueça da Adobe Experience Platform, que é os.

**Lixo dentro, lixo fora.** Você tem uma ideia de cidadania disponíveis e os esquemas na Adobe Experience Platform são configurados. Compreender os dados que estão na Adobe Experience Platform facilitará as coisas, não só na parte de conexão de dados, mas também na hora de construir visualização e análises.

## 4.1.5 Etapa 0: Compreender esquemas e conjuntos de dados da Adobe Experience Platform

Faça logon na Adobe Experience Platform acessando um URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de &quot;Faça&quot;, você vai acessar um início do logon no Adobe Experience Platform.

![Assimilação de dados](../uc1/images/home.png)

Antes de continuar, você precisa selecionar um **sandbox**. O nome do sandbox a ser selecionado é ``Bootcamp``. Você pode fazer isso clicando no ícone **[!UICONTROL Prod]** não canto superior da tela. Depois de selecionar o sandbox apropriado, você verá a tela mudando e agora está em sua sandbox dedicado.

![Assimilação de dados](../uc1/images/sb1.png)

Verifique os esquemas e conjuntos de dados na Adobe Experience Platform.

| Conjunto de dados | Esquema |
| ----------------- |-------------| 
| Sistema de demonstração - Conjunto de dados do evento para site (Global v1.1) | Sistema de demonstração - Esquema de evento para site (Global v1.1) |
| Sistema de demonstração - Conjunto de dados de eventos para Central de chamadas (Global v1.1) | Sistema de demonstração - Esquema de evento para Central de chamadas (Global v1.1) |
| Sistema de demonstração - Conjunto de dados de eventos para assistentes de voz (Global v1.1) | Sistema de demonstração - Esquema de evento para assistentes de voz (Global v1.1) |

Certifique-se de ter verificado ao menos:

- Identidades: entidades CRMID, phoneNumber, ECID, email. Quais identidades são os identificadores primários, nuns são identificadores secundários?

Você pode, os identificadores abrindo um schema e observando o objeto `_experienceplatform.identification.core`. Verifique no schema [Sistema de demonstração - Esquema de evento para site (Global v1.1)](https://experience.adobe.com/platform/schema).

![demonstração](./images/identity.png)

- Explore o objeto de comércio do esquema [Sistema de demonstração - Esquema de evento para site (Global v1.1)](https://experience.adobe.com/platform/schema).

![demonstração](./images/commerce.png)

- Visualizar todos os os [conjuntos de dados](https://experience.adobe.com/platform/dataset/browse?limit=50&amp;page=1&amp;sortDescending=1&amp;sortField=created) e verifique os dados

Agora você está pronto para usar uma interface usuário do Customer Journey Analytics.

Proxima. [4.2 Conjuntos de dados conectados da Adobe Experience Platform no Customer Journey Analytics](./ex2.md)

[Retornar para Fluxo 4](./uc4.md)

[Retornar para Todos os Módulos](../../overview.md)
