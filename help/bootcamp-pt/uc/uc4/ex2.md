---
title: Bootcamp - Customer Journey Analytics - Connect Adobe Experience Platform Datasets in Customer Journey Analytics - Brasil
description: Bootcamp - Customer Journey Analytics - Connect Adobe Experience Platform Datasets in Customer Journey Analytics - Brasil
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 3272d288185415b4604fe48f18c19f8f06e6dce0
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 2%

---

# 4.2 Conjuntos de dados conectados da Adobe Experience Platform no Customer Journey Analytics

## Objetivos

- Compreenda a UI da conexão de dados
- Traga os dados da Adobe Experience Platform para o CJA
- Entenda a ID da informação
- Aprenda o conceito de streaming de dados na Jornada do cliente

## 4.2.1 Conexão

Acesse [analytics.adobe.com](https://analytics.adobe.com) para acessar o Customer Journey Analytics.

Na inicial do Customer Journey Analytics, acesse **Conexões**.

![demonstração](./images/cja2.png)

Aqui você pode, como diferentes, feitas entre o JA e a Plataforma. conexões têm o objetivo dos conjuntos de relatórios no Adobe Analytics. Não entanto, um coleta dos dados é completamente Diferente. Todos os dados vêm de datasets da Adobe Experience Platform.

Vá à primeira conexão. Clique em **Criar nova conexão**.

![demonstração](./images/cja4.png)

Você verá uma interface do usuário **Criar conexão** IU.

![demonstração](./images/cja5.png)

Agora você pode um nome à sua conexão.

Utilizar a abreviatura de nomenclatura: `yourLastName – Omnichannel Data Connection`.

Exemplo: `vangeluw - Omnichannel Data Connection`

Você também o sanbox para usar. Sem sandbox de menu, selecione sandbox, fenômenos que `Bootcamp`. exemplo, ou sandbox a ser usado o **Bootcamp**. E você também fenômenos definir o **Número médio de eventos diários** para **menos de 1 milhão**.

![demonstração](./images/cjasb.png)

Após selecionar sandbox, você começar um datasets conexão uma esta. Clique em **Adicionar conjuntos de dados**.

![demonstração](./images/cjasb1.png)

## 4.2.2 Selecione conjuntos de dados do Adobe Experience Platform

Pesquisar o conjunto de dados `Demo System - Event Dataset for Website (Global v1.1)`. Clique em **+** para o conjunto de dados a esta

![demonstração](./images/cja7.png)

Ágora da Pesquisa e do Cargo seleção `Demo System - Event Dataset for Voice Assistants (Global v1.1)` e `Demo System - Event Dataset for Call Center (Global v1.1)`.

Em, você vê a tela. Clique em **Próximo**.

![demonstração](./images/cja9.png)

## 4.2.3 ID da nuvem de dados

### ID da empresa

O objetivo agora é juntar bagunça os conjuntos de dados. Para cada conjunto de dados selecionado, você verá um campo **ID da pessoa**. Cada conjunto de dados tem seu campo de ID de Referência.

![demonstração](./images/cja11.png)

Como você pode ver um maioria deles, o automaticamente. Isso ocorre Porque um identificador principal é selecionado em esquema na Adobe Experience Platform. Como exemplo, está aqui esquema para `Demo System - Event Schema for Call Center (Global v1.1)`, onde você pode ver o Identificador que existe `phoneNumber`.

![demonstração](./images/cja13.png)

Não entanto, você influenciar da qual será identificador compilar para seus conexão. Você pode usar identificador não configurado no esquema para emitir conjunto de dados. Clique no menu suspenso para explorar os IDs disponíveis em cada conjunto de dados.

![demonstração](./images/cja14.png)

Conforme mencionado você pode diferentes IDs de definir para cada conjunto de dados. Isso permite reunir diferentes conjuntos de dados de múltiplas no CJA. Imagine-se trazer PS ou de pesquisa que seriam interessantes e úteis Nário o o de um acontecimento.

O nome do campo ID da não é importante desde, que o valor em campos ID da corresponda. Digamos que temos `email` conjunto de dados em um e `emailAddress` em outro dataset como ID da. Se `delaigle@adobe.com` tiver o valo para o campo da pessoa conjuntos de dados o CJA poderá compilar os dados.

Atualmente, existem alguns outras, como compilar ou comportamento imo para conhecido. Consulte como frequentes perguntas: [Perguntas frequentes](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html?lang=pt-BR).


### Compilando os dados usando o ID da moeda

Agora que você compreende o conceito de compilar datasets usando o ID da > escolher `email` como ID da para.

![demonstração](./images/cja15.png)

Acesse cada dataset para atualizar ID da.

![demonstração](./images/cja12a.png)

Agora preencha o campo ID da escolh endo o `email` na lista suspensa.

![demonstração](./images/cja17.png)

Depois de compilar os três datasets, prontos para continuar.

| conjunto de dados | ID de pessoa |
| ----------------- |-------------| 
| Sistema de demonstração - Conjunto de dados do evento para site (Global v1.1) | email |
| Sistema de demonstração - Conjunto de dados de eventos para assistentes de voz (Global v1.1) | email |
| Sistema de demonstração - Conjunto de dados de eventos para Central de chamadas (Global v1.1) | email |

Você também precisa garantir que, para cada dataset, e opções habilitadas:

- Importantes todos os dados
- Preencher todos os dados existentes
- Preencher tipo de fonte de dados com &quot;Outros&quot;
- Preencher um descrição com o do servidor do conjunto de dados

Clique em **Adicionar conjuntos de dados**.

![demonstração](./images/cja16.png)

Clique em **Salvar** e vá para o próximo. DE **Conexão**, o autor de hoje, o senhor deputado agora que possui dados estejam não disponíveis CJA.

![demonstração](./images/cja20.png)

Proxima. [4.3 Crie uma Visualização de Dados](./ex3.md)

[Retornar para Fluxo 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)
