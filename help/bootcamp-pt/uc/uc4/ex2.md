---
title: Bootcamp - Customer Journey Analytics - Conectar conjuntos de dados Adobe Experience Platform em Customer Journey Analytics – Brasil
description: Bootcamp - Customer Journey Analytics - Conectar conjuntos de dados Adobe Experience Platform em Customer Journey Analytics – Brasil
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Connections
exl-id: 51078fca-f234-4e50-96ba-ee7f5e286869
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# 4.2 Conectar conjuntos de dados da Adobe Experience Platform sem Customer Journey Analytics

## Objetivos

- Compreenda um interface da conexão de dados
- Traga os dados da Adobe Experience Platform para o CJA
- Entenda uma ID da pessoa e uma compilação de dados
- Aprenda o conceito de transmissão de dados sem jornada do cliente

## 4.2.1 Conexão

Acesse [analytics.adobe.com](https://analytics.adobe.com) para acessar o Customer Journey Analytics.

Na página inicial do Customer Journey Analytics, acesse **Conexões**.

![demonstração](./images/cja2.png)

Aqui você pode ver todas as formas distribuídas entre o CJA e Plataforma. Essas tendências o mesmo objetivo dos conjuntos de informações no Adobe Analytics. Não no mundo, a coleta dos dados é completamente diferente. Todos os dados transmitidos de datasets da Adobe Experience Platform.

Vamos criar sua conexão. Clique em **Criar nova conexão**.

![demonstração](./images/cja4.png)

Você verá uma interface do usuário **Criar conexão**.

![demonstração](./images/cja5.png)

Agora você pode dar um nome à sua conexão.

Use este modelo de nomenclatura: `yourLastName – Omnichannel Data Connection`.

Exemplo: `vangeluw - Omnichannel Data Connection`

Você também deve o pedido da sandbox correta para usar. Nenhuma sandbox de menu, sua sandbox, que deve ser `Bootcamp`. Exemplo, o sandbox a ser usado é o **Bootcamp**. E também você deve o **Número médio de eventos diários** a **menos de 1 milhão**.

![demo](./images/cjasb.png)

Após selecionar sua sandbox, você pode começar a adicionar conjuntos de dados a esta conexão. Clique em **Adicionar conjuntos** de dados.

![demo](./images/cjasb1.png)

## 4.2.2 Selecione conjuntos de dados da Adobe Experience Platform

Pesquise o conjunto de dados `Demo System - Event Dataset for Website (Global v1.1)`. Clique em **+** para adicionar o conjunto de dados a esta conexão.

![demonstração](./images/cja7.png)

Agora pesquise e marque as caixas de seleção `Demo System - Event Dataset for Voice Assistants (Global v1.1)` e `Demo System - Event Dataset for Call Center (Global v1.1)`.

Em seguida, você verá a tela abaixo. Clique em **Próximo**.

![demonstração](./images/cja9.png)

## 4.2.3 ID da pessoa e compilação de dados

### ID da pessoa

O capítulo agora é conjuntos de dados. Para cada conjunto de dados selecionado, você verá um campo **ID de pessoa**. Cada conjunto de dados tem seu próprio campo de ID de pessoa.

![demonstração](./images/cja11.png)

Como você pode ver, a maioria deles tem o ID da seleção reconhecida. Isso mostra porque um identificador principal é selecionado em cada modelo na Adobe Experience Platform. Como exemplo, aqui está o esquema para `Demo System - Event Schema for Call Center (Global v1.1)`, onde você pode ver que o Identificador Primário está definido como `phoneNumber`.

![demonstração](./images/cja13.png)

Não é possível, você ainda pode mudar o identificador será usado para compilar conjuntos de dados para sua conexão. Você pode usar qualquer identificador no esquema vinculado ao seu conjunto de dados. Clique no menu exibido para exibir as IDs garantidas em cada conjunto de dados.

![demonstração](./images/cja14.png)

Dados de pessoa para cada, você pode definir IDs. Essa permite reunir conjuntos de dados diferentes de múltiplas origens no CJA. Imagine as pessoas que usam PS que mantêm e têm acesso para pesquisa o contexto e o motivo de um.

O nome do campo ID da pessoa não é importante, desde que o valor nos campos ID da pessoa correspondente. Digamos que temos `email` em um dataset e `emailAddress` em outro dataset definido como ID da pessoa. Se `delaigle@adobe.com` tiver o mesmo valor para o campo ID da pessoa em ambos os os conjuntos de dados, o CJA pode compilar os dados.

Compilação, compilação, comparação, comparação, comparação, anônimo para conhecido. Perguntas frequentes sobre as perguntas frequentes: [1}.](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html)


### Compilando os dados usando o ID da pessoa

Agora que você escolheu o desenvolvedor de dados conjuntos usando o ID da pessoa, selecionar `email` como ID da pessoa para cada conjunto de dados.

![demonstração](./images/cja15.png)

Acessar cada conjunto de dados para corrigir o ID da pessoa.

![demonstração](./images/cja12a.png)

Agora a o campo ID da pessoa encarregando o `email` na lista suspensa.

![demo](./images/cja17.png)

Depois de compilar os três conjuntos de dados, estamos prontos para continuar.

| conjunto de dados | ID de pessoa |
| ----------------- |-------------| 
| Sistema de demonstração - Conjunto de dados do evento para site (Global v1.1) | email |
| Sistema de demonstração - Conjunto de dados do evento para assistentes de voz (Global v1.1) | email |
| Sistema de demonstração - Conjunto de dados do evento para call center (global v1.1) | email |

Você também precisa garantir que, para cada conjunto de dados, essas opções estão habilitadas:

- Importar todos os novos dados
- Preencher todos os dados existentes
- Preencher tipo de fonte de dados com &quot;Outros&quot;
- Preencher a descrição com o mesmo nome do conjunto de dados

Clique em **Adicionar conjuntos de dados**.

![demonstração](./images/cja16.png)

Clique em **Salvar** e vá para o próximo exercício. Depois de criar sua **, pode levar algumas horas até que seus dados não no CJA.**

![demonstração](./images/cja20.png)

Próxima etapa: [4.3 Criar uma Visualização de Dados](./ex3.md)

[Retorno para Fluxo de monitoramento 4](./uc4.md)

[Retorno para Todos os compartilhados](./../../overview.md)
