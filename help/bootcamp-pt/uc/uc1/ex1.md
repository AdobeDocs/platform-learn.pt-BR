---
title: Bootcamp - Perfil do cliente em tempo real - Do desconhecido ao conhecido no site - Brasil
description: Bootcamp - Perfil do cliente em tempo real - Do desconhecido ao conhecido no site - Brasil
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 853a69d2-5dac-413d-bb40-ef29604a26ae
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 1%

---

# 1.1 Do desconhecido em nosso site

## Contexto

A Adobe Experience Platform um papel importante na jornada. A plataforma é o documento da comunicação, o **sistema de experiência de registro**.

Plataforma é um ambiente em que a palavra cliente engloba mais do que conhecidos. Um visitante desconhecido no local também é um cliente do ponto de vista da Plataforma e, como tal, todo o comportamento de um visitante compartilhado também é enviado à Plataforma. Graças a essa abordagem, quando esse visitante eventualmente se torna um cliente conhecido, uma marca também pode mudar o que aconteceu antes. Isso ajuda a partir de uma perspectiva de gestão da experiência.

## Fluxo da jornada do cliente

Acessar [https://bootcamp.aepdemo.net](https://bootcamp.aepdemo.net). Clique em **Permitir tudo**.

![DSN](./images/web8.png)

Clique no canto do anúncio da Adobe superior da tela para abrir o Visualizador de perfil.

![Demonstração](./images/pv1.png)

Mostrar o painel do visualizador de perfil e no Perfil do cliente em tempo real com o **Experience Cloud ID** como o identificador para este cliente que ainda é desconhecido.

![Demonstração](./images/pv2.png)

Você também pode ver todos os Eventos de Experiência coletados com base no comportamento do cliente. A lista está vazia no momento, mas isso mudará em breve.

![Demonstração](./images/pv3.png)

Acesse a opção de menu **Application Services** e clique no produto **Real-Time CDP**.

![Demonstração](./images/pv4.png)

Você verá a página de detalhes do produto. Um Evento de experiência do tipo **Exibição do Produto** agora foi enviado para uma Adobe Experience Platform que utiliza o SDK da Web que revisou no Módulo 1. Abra o painel Visualizador de perfil e experiências **Eventos de experiência**.

![Demonstração](./images/pv5.png)

Acesse a opção de menu **Application Services** e clique no produto **Adobe Journey Optimizer**. Mais um Evento de experiência foi enviado para a Adobe Experience Platform.

![Demonstração](./images/pv7.png)

Abra o painel Visualizador de perfil. Agora você 2 Experiência do tipo **Visualização do produto**. 2008 é o comportamento é anônimo, cada clique é rastreado e perguntado na Adobe Experience Platform. Depois que o anônimo se tornar realidade, cliente mesclar todo o comportamento anônimo ao perfil conhecido.

![Demonstração](./images/pv8.png)

Agora vamos analisar seu perfil de cliente e usar seus comportamentos para a sua experiência do cliente no site.

Próxima etapa: [1.2 Visualizar seu perfil de cliente em tempo real - IU](./ex2.md)

[Retorno para Fluxo de monitoramento 1](./uc1.md)

[Retorno para Todos os compartilhados](../../overview.md)
