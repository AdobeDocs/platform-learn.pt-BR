---
title: Bootcamp - Customer Journey Analytics - De insights à ação - Brasil
description: Bootcamp - Customer Journey Analytics - De insights à ação - Brasil
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Audiences
exl-id: 28b87e21-3168-447e-9a93-a6ae7e969657
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# 4.6 Dos insights à ação

## Objetivos

- Entenda como criar um público com base em uma visão coletada no Customer Journey Analytics
- Use esse público no CDP em tempo real e no Adobe Journey Optimizer

## 4.6.1 Crie uma audiência e publique-a

Em seu projeto, você criou um filtro chamado **Call Feelings** e conseguiu visualizar a quantidade de usuários que tiveram suas ligações ao call center classificadas como **positivas**. Agora, você poderá criar um segmento com esses usuários e ativação-los em jornadas ou em canais de comunicação.

O primeiro passo é: No painel criado no último exercício, selecione a linha **1. Call Feeling - Positive**, clique com o botão direito de seu mouse e selecione a opção **Create audience from selection**:

![demonstração](./images/aud1.png)

Em seguida, dar um nome para a sua audiência seguindo o modelo **seu LastName - cia audience call se sentindo positivo**:

![demonstração](./images/aud2.png)

Nota que é possível ter um preview da audiência que está sendo criado:

![demonstração](./images/aud3.png)

Para finalizar, clique em **Publicar**:

![demonstração](./images/aud4.png)

## 4.6.2 Usar sua audiência como parte de um segmento

Voltando para a Adobe Experience Platform, vá em **Segmentos > Navegar** e você o seu segmento criado no CJA pronto e disponível para ser usado nas suas ativações e jornadas!

![demonstração](./images/aud5.png)

Vamos agora usar esse segmento em uma mudança no Facebook e em uma jornada do cliente!

## 4.6.3 Use seu segmento na Real-Time CDP em tempo real

Na Adobe Experience Platform, vá em **Segments > Browse** e encontre a audiência que você criou no CJA:

![demonstração](./images/aud6.png)

Clique no seu segmento e, em seguida, clique em **Activate to Destination**:

![demonstração](./images/aud7.png)

destino da música chamada-facebook e, em seguida, clique em Próximo:

![demonstração](./images/aud8.png)

Em seguida, clique em Next novamente:

![demonstração](./images/aud9.png)

Selecione a opção **Origin of your audience** e defina como **Directly from customers** e clique em Next:

![demonstração](./images/aud10.png)

Por fim, na página **Avaliação** clique em Concluir!

![demonstração](./images/aud11.png)

Pronto! &quot;Agora o seu segmento está vinculado aos desafios deixados do Facebook&quot; .
Agora, vamos usar esse segmento no AJO!

## 4.6.4 Usar seu segmento no Adobe Journey Optimizer

Na interface da clique do Adobe Experience Platform em Journey Optimizer, em seguida, no menu lateral, clique em **Jornada** e criar a leitura uma em **Criar Jornada**:

![demonstração](./images/aud20.png)

![demonstração](./images/aud21.png)

![demonstração](./images/aud22.png)

Em seguida, sem menu lateral, em Eventos, **Qualificação de segmento** e-o até a jornada:

![demonstração](./images/aud23.png)

Em seguida, em **Segment** clique em **Edit** para selecionar um segmento:

![demonstração](./images/aud24.png)

Selecione a audiência que você criou no CJA e clique em **Save**:

![demonstração](./images/aud25.png)

Pronto! A partir daí você pode criar uma jornada para clientes que se qualifica para esse segmento!

[Go Back to User Flow 4](./uc4.md)

[Voltar para todos os processos](./../../overview.md)
