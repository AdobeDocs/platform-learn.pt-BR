---
title: Bootcamp - Customer Journey Analytics - Conectar conjuntos de dados Adobe Experience Platform no Customer Journey Analytics
description: Bootcamp - Customer Journey Analytics - Conectar conjuntos de dados Adobe Experience Platform no Customer Journey Analytics
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Connections
exl-id: 47e02021-019c-4ea4-a7a8-003deef7c9e5
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 1%

---

# 4.2 Conectar conjuntos de dados do Adobe Experience Platform no Customer Journey Analytics

## Objetivos

- Entender a interface da conexão de dados
- Trazer dados do Adobe Experience Platform para o CJA
- Entender a ID de pessoa e a compilação de dados
- Saiba mais sobre o conceito de transmissão de dados no Customer Journey Analytics

## 4.2.1 Conexão

Acesse [analytics.adobe.com](https://analytics.adobe.com) para acessar o Customer Journey Analytics.

Na página inicial do Customer Journey Analytics, vá para **Conexões**.

![demonstração](./images/cja2.png)

Aqui você pode ver todas as diferentes conexões feitas entre o CJA e a Platform. Essas conexões têm o mesmo objetivo que os conjuntos de relatórios no Adobe Analytics. Mas a coleta de dados é totalmente diferente. Todos os dados vêm dos conjuntos de dados da Adobe Experience Platform.

Vamos criar sua primeira conexão. Clique em **Criar nova conexão**.

![demonstração](./images/cja4.png)

Você verá a interface do usuário **Criar conexão**.

![demonstração](./images/cja5.png)

Agora você pode dar um nome à sua conexão.

Use esta convenção de nomenclatura: `yourLastName – Omnichannel Data Connection`.

Exemplo: `vangeluw - Omnichannel Data Connection`

Você também precisa selecionar a sandbox correta para usar. No menu da sandbox, selecione sua sandbox, que deve ser `Bootcamp`. Neste exemplo, a sandbox a ser usada é **Bootcamp**. E você também precisa definir o **número médio de eventos diários** para **menos de 1 milhão**.

![demonstração](./images/cjasb.png)

Depois de selecionar a sandbox, você pode começar a adicionar conjuntos de dados a essa conexão. Clique em **Adicionar conjuntos de dados**.

![demonstração](./images/cjasb1.png)

## 4.2.2 Selecionar conjuntos de dados do Adobe Experience Platform

Pesquisar o conjunto de dados `Demo System - Event Dataset for Website (Global v1.1)`. Clique em **+** para adicionar o conjunto de dados a esta conexão.

![demonstração](./images/cja7.png)

Agora pesquise e marque as caixas de seleção de `Demo System - Profile Dataset for Loyalty (Global v1.1)` e `Demo System - Event Dataset for Call Center (Global v1.1)`.

Então você terá isto. Clique em **Next**.

![demonstração](./images/cja9.png)

## 4.2.3 Compilação de ID de pessoa e dados

### ID de pessoa

A meta agora é unir esses conjuntos de dados. Para cada conjunto de dados selecionado, você verá um campo chamado **ID de pessoa**. Cada conjunto de dados tem seu próprio campo ID de pessoa.

![demonstração](./images/cja11.png)

Como você pode ver, a maioria deles tem a ID de pessoa selecionada automaticamente. Isso ocorre porque um Identificador primário é selecionado em cada esquema no Adobe Experience Platform. Como exemplo, aqui está o esquema para `Demo System - Event Schema for Call Center (Global v1.1)`, no qual você pode ver que o Identificador Principal está definido como `phoneNumber`.

![demonstração](./images/cja13.png)

No entanto, você ainda pode influenciar qual identificador será usado para compilar conjuntos de dados para sua conexão. Você pode usar qualquer identificador configurado no esquema vinculado ao seu conjunto de dados. Clique na lista suspensa para explorar as IDs disponíveis em cada conjunto de dados.

![demonstração](./images/cja14.png)

Como mencionado, você pode definir IDs de pessoa diferentes para cada conjunto de dados. Isso permite reunir diferentes conjuntos de dados de várias origens no CJA. Imagine trazer o NPS ou dados de pesquisa que seriam muito interessantes e úteis para entender o contexto e por que algo aconteceu.

O nome do campo ID de pessoa não é importante, desde que o valor nos campos ID de pessoa corresponda. Por exemplo, se a ID de pessoa for `email` em um conjunto de dados e `emailAddress` em outro, e `dnb-bootcamp@adobe.com` for o mesmo valor para o campo de ID de pessoa em ambos os conjuntos de dados, o CJA poderá compilar os dados.

Atualmente, existem algumas outras limitações, como compilar o comportamento anônimo para conhecido. Revise as Perguntas Frequentes aqui: [Perguntas Frequentes](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html).

### Costura de dados usando a ID de pessoa

Agora que você entende o conceito de compilação de conjuntos de dados usando a ID de pessoa, vamos escolher `email` como sua ID de pessoa para cada conjunto de dados.

![demonstração](./images/cja15.png)

Acesse cada conjunto de dados para atualizar a ID de pessoa.

![demonstração](./images/cja12a.png)

Agora preencha o campo ID de pessoa escolhendo o `email` na lista suspensa.

![demonstração](./images/cja17.png)

Depois de compilar os três conjuntos de dados, estamos prontos para continuar.

| conjunto de dados | ID de pessoa |
| ----------------- |-------------| 
| Sistema de demonstração - Conjunto de dados de evento para site (Global v1.1) | email |
| Sistema de demonstração - Conjunto de dados de perfil para fidelidade (Global v1.1) | email |
| Sistema de demonstração - Conjunto de dados de evento para call center (Global v1.1) | email |

Você também precisa garantir que, para cada conjunto de dados, essas opções estejam habilitadas:

- Importar todos os novos dados
- Preencher retroativamente todos os dados existentes

Clique em **Adicionar conjuntos de dados**.

![demonstração](./images/cja16.png)

Clique em **Salvar** e vá para o próximo exercício.
Após criar sua **Conexão**, pode levar algumas horas até que seus dados estejam disponíveis no CJA.

![demonstração](./images/cja20.png)

Próxima Etapa: [4.3 Criar uma Exibição de Dados](./ex3.md)

[Voltar para Fluxo de Usuário 4](./uc4.md)

[Voltar a todos os módulos](./../../overview.md)
