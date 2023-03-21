---
title: Bootcamp - Customer Journey Analytics - De insights à ação
description: Bootcamp - Customer Journey Analytics - De insights à ação
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: e5c2ad88967d7f6a45d3a5cc09ca4c9bc9a62a08
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# 4.6 De insights à ação

## Metas

- Saiba como criar um público-alvo com base em uma exibição coletada no Customer Journey Analytics
- Usar este público-alvo no Real-Time CDP e Adobe Journey Optimizer

## 4.6.1 Criar um público-alvo e publicá-lo

No seu projeto, você criou um filtro chamado **Feelings de chamada** e puderam visualizar o número de usuários que tiveram suas chamadas para a central de atendimento classificadas como **positivo**. Agora é possível criar um segmento com esses usuários e ativá-los em jornadas ou canais de comunicação.

O primeiro passo é: No painel criado no último exercício, selecione a linha **1. Feed de chamada - Positivo**, clique com o botão direito do mouse e selecione o **Criar público-alvo a partir da seleção** opção:

![demonstração](./images/aud1.png)

Em seguida, dê um nome ao público-alvo seguindo o modelo **yourLastName - Chamada de público-alvo CJA positiva**:

![demonstração](./images/aud2.png)

Observe que é possível ter uma pré-visualização do público-alvo que está sendo criado:

![demonstração](./images/aud3.png)

Finalmente, clique em **Publicar**.

![demonstração](./images/aud4.png)

## 4.6.2 Usar seu público-alvo como parte de um segmento

Volte para a Adobe Experience Platform e acesse **Segmentos > Procurar** e você poderá ver seu segmento criado no CJA pronto e disponível para ser usado em suas ativações e jornadas!

![demonstração](./images/aud5.png)

Agora vamos usar esse segmento em uma ativação do Facebook e em uma jornada do cliente!

## 4.6.3 Usar seu segmento no Real-Time CDP em tempo real

No Adobe Experience Platform, acesse **Segmentos > Procurar** e encontre o público-alvo que você criou no CJA:

![demonstração](./images/aud6.png)

Clique no seu segmento e, em seguida, clique em **Ativar para destino**:

![demonstração](./images/aud7.png)

Selecione o destino com o nome **bootcamp-facebook** e, em seguida, clique em **Próximo**.

![demonstração](./images/aud8.png)

Clique em **Próximo** novamente.

![demonstração](./images/aud9.png)

Selecione o **Origem do público-alvo** e defina-a como **Diretamente dos clientes**, clique em **Próximo**.

![demonstração](./images/aud10.png)

Clique em **Concluir**.

![demonstração](./images/aud11.png)

Seu segmento agora está conectado aos Públicos-alvo personalizados da Facebook. Agora vamos usar o mesmo segmento no Adobe Journey Optimizer.

## 4.6.4 Usar seu segmento no Adobe Journey Optimizer

No Adobe Experience Platform, clique em **Journey Optimizer** e, em seguida, no menu à esquerda, clique em **Jornada** e comece a criar uma jornada clicando em **Criar Jornada**.

![demonstração](./images/aud20.png)

![demonstração](./images/aud21.png)

![demonstração](./images/aud22.png)

Em seguida, no menu lateral esquerdo, em **Eventos**, selecione **Qualificação do segmento** e arraste-o para a jornada:

![demonstração](./images/aud23.png)

Em Segmento, clique em **Editar** para selecionar um segmento:

![demonstração](./images/aud24.png)

Selecione o público-alvo criado anteriormente no CJA e clique em  **Salvar**.

![demonstração](./images/aud25.png)

Pronto! Aqui, você pode criar uma jornada para clientes qualificados para este segmento.

[Voltar para Fluxo de Usuário 4](./uc4.md)

[Voltar para todos os módulos](./../../overview.md)
