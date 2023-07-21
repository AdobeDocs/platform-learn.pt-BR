---
title: Bootcamp - Customer Journey Analytics - Dos insights à ação
description: Bootcamp - Customer Journey Analytics - Dos insights à ação
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Audiences
exl-id: 7a38a0a4-46e4-41f2-9a75-316dfde7128f
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# 4.6 Dos insights à ação

## Metas

- Entenda como criar um público-alvo com base em uma exibição coletada no Customer Journey Analytics
- Usar este público no Real-Time CDP e no Adobe Journey Optimizer

## 4.6.1 Criar um público-alvo e publicá-lo

No seu projeto, você criou um filtro chamado **Sentimentos de chamada** e puderam exibir o número de usuários que tiveram suas chamadas para a central de atendimento classificadas como **positivo**. Agora é possível criar um segmento com esses usuários e ativá-los no jornada ou em canais de comunicação.

A primeira etapa é: no painel criado no último exercício, selecione a linha **1. Sensação de chamada - Positiva**, clique com o botão direito do mouse e selecione o **Criar público a partir da seleção** opção:

![demonstração](./images/aud1.png)

Em seguida, nomeie o público-alvo seguindo o modelo **yourLastName - A chamada de público do CJA parece positiva**:

![demonstração](./images/aud2.png)

Observe que é possível pré-visualizar o público-alvo que está sendo criado:

![demonstração](./images/aud3.png)

Por fim, clique em **Publish**.

![demonstração](./images/aud4.png)

## 4.6.2 Usar seu público-alvo como parte de um segmento

Volte para a Adobe Experience Platform e vá para **Segmentos > Navegar** e você poderá ver seu segmento criado no CJA pronto e disponível para ser usado em suas ativações e jornadas!

![demonstração](./images/aud5.png)

Agora vamos usar esse segmento em uma ativação do Facebook e em uma jornada do cliente!

## 4.6.3 Usar seu segmento no Real-Time CDP em tempo real

No Adobe Experience Platform, acesse **Segmentos > Navegar** e encontre o público-alvo que você criou no CJA:

![demonstração](./images/aud6.png)

Clique no seu segmento e em **Ativar para destino**:

![demonstração](./images/aud7.png)

Selecione o destino chamado **bootcamp-facebook** e clique em **Próxima**.

![demonstração](./images/aud8.png)

Clique em **Próxima** novamente.

![demonstração](./images/aud9.png)

Selecione o **Origem do seu público** e defina-a como **Diretamente dos clientes**, clique em **Próxima**.

![demonstração](./images/aud10.png)

Clique em **Concluir**.

![demonstração](./images/aud11.png)

Seu segmento agora está conectado aos Públicos-alvo personalizados da Facebook. Agora vamos usar esse mesmo segmento no Adobe Journey Optimizer.

## 4.6.4 Usar seu segmento no Adobe Journey Optimizer

No Adobe Experience Platform, clique em **Journey Optimizer** e, no menu do lado esquerdo, clique em **Jornadas** e comece a criar uma jornada clicando em **Criar Jornada**.

![demonstração](./images/aud20.png)

![demonstração](./images/aud21.png)

![demonstração](./images/aud22.png)

Em seguida, no menu do lado esquerdo, em **Eventos**, selecione **Qualificação do segmento** e arraste-a para a jornada:

![demonstração](./images/aud23.png)

Em Segmento, clique em **Editar** para selecionar um segmento:

![demonstração](./images/aud24.png)

Selecione o público criado anteriormente no CJA e clique em  **Salvar**.

![demonstração](./images/aud25.png)

Pronto! Aqui, é possível criar uma jornada para clientes que se qualificam para esse segmento.

[Voltar para Fluxo de Usuário 4](./uc4.md)

[Voltar para todos os processos](./../../overview.md)
