---
title: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101 - Brasil
description: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101 - Brasil
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 63933d9e-b774-483f-b547-188c77440595
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
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

O Customer Journey Analytics (JA) ➡ uma interface em que os times de Analytics, Negócios e Tecnologia permitem todos os dados da companhia e analisar a jornada entre canais (online e offline) do cliente de ponta a ponta. O CJA É capaz de modificar as respostas e a mudança para essa jornada, trazendo visão acionável em cima das dificuldades no processo de transformação e possibilidade o migrar de tendências e habilidades nos pontos mais significativos.

O CJA tem o Analysis Workspace à Adobe Experience Platform. A Adobe Experience Platform é o relatório da comunicação e da orquestração e, com o CJA, as marcas agora podem contextualizar e analisar esses dados, para que as equipes de negócios e insights ajudaram com eles, analisando a jornada on-line para off-line do cliente.

Como equipes de negócios e insights podem conversar com o CJA, fazer perguntas e respostas em tempo real com a interface do usuário de arrastar, e compartilhado e fácil de usar do Analysis Workspace.

![demonstração](./images/cja-adv-analysis1.png)

## 4.1.2 Vantagens principais

Os três únicos para os clientes são:

- A melhoria de insights para todos (ou seja, democratizar o acesso aos dados).
- A capacidade de ver o o cliente em uma jornada contextual (ou seja, os dados podem ser visualizados sequenciados, endo multiplicado on-line e off-line).
- A capacidade de aproveitar o poder dos dados sem que haja um migrante (ou seja, permitir que o usuário compartilhado para desbloquear insights e dados para de marketing).

## 4.1.3 ## 4.1.3 Por que escolher o Customer Journey Analytics?

O CJA não se destina a estudar a Power BI de BI verdade, como microestratégia, Locker ou Tableau. O destino de todos os aplicativos de BI é exibido para mudar corporativos para que ele possa controlar tudo relacionado em grandes sequências. O objetivo do CECo é tupiniquim de análise para as equipes de Marketing e Negócios, tornando-o uma visão de análise para essas pessoas



Traduzir, os aplicativos de BI tem sido incompatíveis de permitir a mudança do cliente:

- Eles não podem fazer nada e não analisar a jornada do cliente.
- Os aplicativos de BI prescreve a pergunta com
- As consultas interativas são limitadas pela estrutura do banco de dados
- Habilidades de SQL são competitivas.
- Os modelos de motivo BI não DAR a impressão de que você é capaz de identificar o que aconteceu.
- Os aplicativos de BI não ampliam o contato exclusivo com os pontos de contato do cliente.

PERGUNTAS FREQUENTES, empresas de negócios e analistas subordinados a becos sem saída, tornando a análise cara, inflexível e desconectada dos sistemas de sistemas.

Com o CJA pode ter uma visão completa da jornada do cliente, usando dados offline e online, com as sequências para corrigir o tempo de insight, com o capítulo os usuários de eventos independentes para entender por que algo aconteceu e como a isso.

![demonstração](./images/cja-use-case.png)

## 4.1.4 Compreenda o fluxo de trabalho do Customer Journey Analytics

Antes de iniciar os visualizá-los, é responsabilidade de lidar com os dados para o cliente da Adobe Experience Platform JA para visualizar-los e obter alguns insights profundos. É o que chamamos de fluxo de trabalho do CJA. Vamos verificar:

![demonstração](./images/cja-work-flow.jpg)

Antes de iniciar como consequência, não se deve rever a etapa 0, que é alterado os dados que estão disponíveis na Adobe Experience Platform.

**Lixo entra, lixo sai.** Você deve ter uma ideia de quais dados estão disponíveis na Adobe Experience Platform como os esquemas na são configurados. Compreender os dados que estão na Adobe Experience Platform facilitará as coisas, não só na parte de conexões de dados, mas também na hora de exercícios visualizações e fazer.

## 4.1.5 Etapa 0: Compreender esquemas e conjuntos de dados da Adobe Experience Platform

Faça logon no Adobe Experience Platform acessando um URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer logon, você acessará a página inicial da Adobe Experience Platform.

![Assimilação de dados](../uc1/images/home.png)

Antes de continuar, você precisa atualizar um **sandbox**. O nome do sandbox a ser selecionado é ``Bootcamp``. Você pode fazer isso, não tem nada a ver **[!UICONTROL Prod]** nenhum canto superior direito da tela. Depois de pegar o sandbox, você verá a tela e agora você está em seu sandbox exclusivo.

![Assimilação de dados](../uc1/images/sb1.png)

Escolhe esquemas e conjuntos de dados na Adobe Experience Platform.

| Conjunto de dados | Esquema |
| ----------------- |-------------| 
| Sistema de demonstração - Conjunto de dados de evento para site (Global v1.1) | Sistema de demonstração - Esquema de evento para site (Global v1.1) |
| Sistema de demonstração - Conjunto de dados de evento para call center (Global v1.1) | Sistema de demonstração - Esquema de evento para call center (Global v1.1) |
| Sistema de demonstração - Conjunto de dados de evento para assistentes de voz (Global v1.1) | Sistema de demonstração - Esquema de evento para assistentes de voz (Global v1.1) |

pasta-se de ter verificado ao menos:

- Identidades: CRMID, phoneNumber, ECID, email. Quais identidades são os identificadores primários, quais são os identificadores monitorados?

Você pode encontrar os identificadores abrindo um esquema e observando o objeto `_experienceplatform.identification.core`. esquema do objeto [Sistema de demonstração - Esquema de evento para site (Global v1.1)](https://experience.adobe.com/platform/schema).

![demonstração](./images/identity.png)

- Explorar o objeto de comércio dentro do schema [Sistema de demonstração - Esquema de evento para site (Global v1.1)](https://experience.adobe.com/platform/schema).

![demonstração](./images/commerce.png)

- Visualizar todos os [conjuntos de dados](https://experience.adobe.com/platform/dataset/browse?limit=50&amp;page=1&amp;sortDescending=1&amp;sortField=created) e dos dados

Agora você está pronto para começar a usar uma interface do usuário do Customer Journey Analytics.

Próxima etapa: [4.2 Conectar conjuntos de dados da Adobe Experience Platform sem Customer Journey Analytics](./ex2.md)

[Retorno para Fluxo de monitoramento 4](./uc4.md)

[Retorno para Todos os compartilhados](../../overview.md)
