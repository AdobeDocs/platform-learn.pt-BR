---
title: Bootcamp - Real-time Customer Profile - De unknown to known on the website - Brasil
description: Bootcamp - Real-time Customer Profile - De unknown to known on the website - Brasil
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 1%

---

# 1.1 Desconhecido ao conhecido em nosso site

## Contexto

Adobe Experience Platform desempenha um papel importante jornada. A plataforma é o cérebro da comunicação **sistema de experiência**.

Plataforma é um ambiente em que palavra cliente englob um do que clientes conhecidos. Um visitante desconhecido nenhum site também é um cliente do ponto de vista da Plataforma e como tal, fazer o comportamento de um visitante desconhecido é enviado à Plataforma. Graças a Deus que quando se hora a visitante se, uma marca também um cliente conhecido, visualizar o que aconteceu antes daquele momento. Isso é uma ajuda do primeiro dia de otimização de atribuição e experiência.

## Fluxo da jornada do cliente

Acesse [https://bootcamp.aepdemo.net](https://bootcamp.aepdemo.net). Clique em **Permitir Tudo**.

![DSN](./images/web8.png)

Clique no logoda da Adobe no canto superior esquerdo tela para o Visualizador da .

![Demonstração](./images/pv1.png)

Verifique o painel do Visualizador de Esquema Não Perfil em tempo real o **Experience Cloud ID** Como identificador primário para este cliente que é desconhecido.

![Demonstração](./images/pv2.png)

Você também  todos os Eventos de Experiência coletados com base no comportamento do cliente. A lista está vazia no momento, mas mudará em breve.

![Demonstração](./images/pv3.png)

Acessar um menu de navegação **Serviços de aplicativos** e não produção **Real-Time CDP**.

![Demonstração](./images/pv4.png)

Você vê o começo do detalhes do produto. Evento de experiência do tipo **Exibição do produto** ágora foi enviado para a Adobe Experience Platform usando um implementação do SDK da Web que você revisou no Módulo 1. Abra o painel Visualizador de verifique seu **Eventos de experiência**.

![Demonstração](./images/pv5.png)

Acessar um menu de navegação **Serviços de aplicativos** e não produção **Adobe Journey Optimizer**. Mais um Evento de experiência foi enviado para um Adobe Experience Platform.

![Demonstração](./images/pv7.png)

Abra o painel Visualizador de. Agora você verá 2 Eventos de experiência do **Exibição do produto**. comportamento, anôn imo, cada um é armazenado na Adobe Experience Platform. depois de que o cliente anôn imo se tornar conhecido, o poderemos mesclar o comportamento imo automaticamente ao conhecido.

![Demonstração](./images/pv8.png)

Vamos agora analisar seu cliente para persongrave comportamento seu experiência não cliente.

Proxima. [1.2 Visualizar seu inimigo de cliente em tempo real - IU](./ex2.md)

[Retornar para Fluxo de Correio](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
