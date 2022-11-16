---
title: Customer Journey Analytics - Conectar conjuntos de dados do Adobe Experience Platform no Customer Journey Analytics
description: Customer Journey Analytics - Conectar conjuntos de dados do Adobe Experience Platform no Customer Journey Analytics
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 3b1ffdda-6b9f-4463-8a50-a8a85c3aaf76
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 4%

---

# 11.2 Conectar conjuntos de dados do Adobe Experience Platform no Customer Journey Analytics

## Objetivos

- Entender a interface do usuário da conexão de dados
- Trazer dados do Adobe Experience Platform para o CJA
- Entender a ID de pessoa e a compilação de dados
- Saiba mais sobre o conceito de transmissão de dados no Customer Journey Analytics

## Conexão 11.2.1

Ir para [analytics.adobe.com](https://analytics.adobe.com) para acessar o Customer Journey Analytics.

Na página Customer Journey Analytics-homepage, acesse **Conexões**.

![demonstração](./images/cja2.png)

Aqui você pode ver todas as diferentes conexões feitas entre o CJA e a Platform. Essas conexões têm o mesmo objetivo dos conjuntos de relatórios no Adobe Analytics. Mas a coleta dos dados é totalmente diferente. Todos os dados vêm de conjuntos de dados da Adobe Experience Platform.

Vamos criar sua primeira conexão. Clique em **Criar nova conexão**.

![demonstração](./images/cja4.png)

Você verá o **Criar conexão** IU.

![demonstração](./images/cja5.png)

Agora você pode dar um nome à sua conexão.

Use esta convenção de nomenclatura: `--demoProfileLdap-- – Omnichannel Data Connection`.

Exemplo: `vangeluw - Omnichannel Data Connection`

Você também precisa selecionar a sandbox correta para usar. No menu sandbox, selecione a sandbox que deve ser `Bootcamp`. Neste exemplo, a sandbox a ser usada é **Bootcamp**. E você também precisa definir a variável **Número médio de eventos diários** para **menos de 1 milhão**.

![demonstração](./images/cjasb.png)

Após selecionar sua sandbox, os conjuntos de dados disponíveis serão atualizados.

![demonstração](./images/cjasb1.png)

## 11.2.2 Selecionar conjuntos de dados do Adobe Experience Platform

Pesquisar pelo conjunto de dados `Demo System - Event Dataset for Website (Global v1.1)`. Clique em **+** para adicionar o conjunto de dados a essa conexão.

![demonstração](./images/cja7.png)

Agora pesquise e marque as caixas de seleção para `Demo System - Event Dataset for Voice Assistants (Global v1.1)` e `Demo System - Event Dataset for Call Center (Global v1.1)`.

Você terá isso. Clique em **Próximo**.

![demonstração](./images/cja9.png)

## 11.2.3 ID de pessoa e identificação de dados

### ID de pessoa

### ID de pessoa

O objetivo agora é unir esses conjuntos de dados. Para cada conjunto de dados selecionado, você verá um campo chamado **ID da pessoa**. Cada conjunto de dados tem seu próprio campo ID de pessoa .

![demonstração](./images/cja11.png)

Como você pode ver, a maioria deles tem a ID de pessoa selecionada automaticamente. Isso ocorre porque um Identificador primário é selecionado em cada esquema no Adobe Experience Platform. Como exemplo, aqui está o esquema para `Demo System - Event Schema for Call Center (Global v1.1)`, onde você pode ver que o Identificador primário está definido como `phoneNumber`.

![demonstração](./images/cja13.png)

No entanto, você ainda pode influenciar qual identificador será usado para unir conjuntos de dados para sua conexão. Você pode usar qualquer identificador configurado no esquema vinculado ao conjunto de dados. Clique na lista suspensa para explorar as IDs disponíveis em cada conjunto de dados.

![demonstração](./images/cja14.png)

Como mencionado, você pode definir IDs de pessoa diferentes para cada conjunto de dados. Isso permite reunir diferentes conjuntos de dados de várias origens no CJA. Imagine trazer dados de NPS ou pesquisa que seriam muito interessantes e úteis para entender o contexto e por que algo aconteceu.

O nome do campo ID de pessoa não é importante, desde que o valor nos campos ID de pessoa corresponda. Digamos que temos `email` em um conjunto de dados e `emailAddress` em outro conjunto de dados definido como ID de pessoa. If `delaigle@adobe.com` for o mesmo valor para o campo ID de pessoa em ambos os conjuntos de dados, o CJA poderá compilar os dados.

Atualmente, existem outras limitações, como unir o comportamento anônimo ao conhecido. Leia as Perguntas frequentes aqui: [Perguntas frequentes](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html?lang=pt-BR).

### Como configurar os dados usando a ID de pessoa

Agora que você entende o conceito de compilação de conjuntos de dados usando a ID de pessoa, vamos escolher `email` como a ID de pessoa para cada conjunto de dados.

![demonstração](./images/cja15.png)

Vá para cada conjunto de dados para atualizar a ID de pessoa.

![demonstração](./images/cja12a.png)

Agora preencha o campo ID de pessoa escolhendo a variável `email` na lista suspensa.

![demonstração](./images/cja17.png)

Depois de compilar os três conjuntos de dados, estamos prontos para continuar.

| conjunto de dados | ID de pessoa |
| ----------------- |-------------| 
| Sistema de demonstração - Conjunto de dados do evento para site (Global v1.1) | email |
| Sistema de demonstração - Conjunto de dados de eventos para assistentes de voz (Global v1.1) | email |
| Sistema de demonstração - Conjunto de dados de eventos para Central de chamadas (Global v1.1) | email |

Também é necessário garantir que, para cada conjunto de dados, essas opções estejam habilitadas:

- Importar todos os novos dados
- Preenchimento retroativo de todos os dados existentes

Clique em **Adicionar conjuntos de dados**.

![demonstração](./images/cja16.png)

Clique em **Salvar** e vá para o próximo exercício.
Depois de criar a **Conexão** pode levar algumas horas até que seus dados estejam disponíveis no CJA.

![demonstração](./images/cja20.png)

Próxima etapa: [11.3 Criar uma visualização de dados](./ex3.md)

[Volte para o Módulo 11](./customer-journey-analytics-build-a-dashboard.md)

[Voltar para todos os módulos](./../../overview.md)
