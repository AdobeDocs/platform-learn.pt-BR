---
title: Bootcamp - Customer Journey Analytics - De insights à ação - Brasil
description: Bootcamp - Customer Journey Analytics - De insights à ação - Brasil
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 28b87e21-3168-447e-9a93-a6ae7e969657
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# 4.6 Dos insights à ação

## Objetivos

- Entenda como criar um público com base em uma visão coletada no Customer Journey Analytics
- Usar esse público no CDP em tempo real e no Adobe Journey Optimizer

## 4.6.1 Criação uma audiência e publique-a

Em seu projeto, você criou um filtro chamado **Sentimentos de chamada** e a quantidade de usuários que possuem ligações ao call center como **avaliação**. Agora, você pode criar um segmento com esses usuários e-los em jornadas ou em canais de comunicação.

O primeiro passo é: No histórico criado no último exercício, a linha **1. Sensação de chamada - Positiva**, clique com o botão direito de seu mouse e seleção a opção **Criar público a partir da seleção**:

![demonstração](./images/aud1.png)

Em seguida, dar um nome para a sua tarefa seguindo o modelo **yourLastName - sensação positiva na chamada de público da cia**:

![demonstração](./images/aud2.png)

Nota que é possível ter um preview da audiência que está sendo criado:

![demonstração](./images/aud3.png)

Para finalizar, clique em **Publicar**:

![demonstração](./images/aud4.png)

## 4.6.2 Usar sua audiência como parte de um segmento

Voltando para a Adobe Experience Platform, vá em **Segmentos > Navegar** e você conseguirá visualizar o seu filho criado no CJA pronto e disponível para ser usado nas suas ativações e jornadas!

![demonstração](./images/aud5.png)

Vamos agora usar esse segmento em uma mudança no Facebook e em uma jornada do cliente!

## 4.6.3 Usar seu segmento na Real-Time CDP em tempo real

Na Adobe Experience Platform, vá em **Segmentos > Navegar** e encontrar a audiência que é criada no CJA:

![demonstração](./images/aud6.png)

Clique no seu segmento e, em seguida, clique em **Ativar para destino**:

![demonstração](./images/aud7.png)

destino da música chamada-facebook e, em seguida, clique em Próximo:

![demonstração](./images/aud8.png)

Em seguida, clique em Próximo novembro:

![demonstração](./images/aud9.png)

a seleção **Origem do seu público** e ➡ como **Diretamente dos clientes** e clique em Próximo:

![demonstração](./images/aud10.png)

Por fim, na página **Revisão** clique em Terminar!

![demonstração](./images/aud11.png)

Pronto! &quot;Agora o seu segmento está vinculado aos desafios deixados do Facebook&quot; .
Agora, vamos usar esse segmento no AJO!

## 4.6.4 Usar seu segmento no Adobe Journey Optimizer

Na interface da Adobe Experience Platform clique em Journey Optimizer, em seguida, sem menu lateral, clique em **Jornadas** e começar a criar uma vez corrigir em **Criar Jornada**:

![demonstração](./images/aud20.png)

![demonstração](./images/aud21.png)

![demonstração](./images/aud22.png)

Em seguida, sem menu lateral, em Eventos, **Qualificação do segmento** e pesquisas-o até à jornada:

![demonstração](./images/aud23.png)

Em seguida, em **Segmento** clique em **Editar** para selecionar um segmento:

![demonstração](./images/aud24.png)

audiência que é criada no CJA e clique em **Salvar**:

![demonstração](./images/aud25.png)

Pronto! A partir daí você pode criar uma jornada para clientes que se qualifica para esse segmento!

[Voltar para Fluxo de Usuário 4](./uc4.md)

[Voltar para todos os processos](./../../overview.md)
