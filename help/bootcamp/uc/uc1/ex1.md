---
title: Bootcamp - Perfil do cliente em tempo real - Do desconhecido ao conhecido no site
description: Bootcamp - Perfil do cliente em tempo real - Do desconhecido ao conhecido no site
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 32a084a3-4c04-4367-947e-f7151fdad73b
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 1%

---

# 1.1 De desconhecido para conhecido no site

## Contexto

A jornada do desconhecido para o conhecido é um dos tópicos mais importantes entre as marcas atualmente, assim como a jornada do cliente, desde a aquisição até a retenção.

O Adobe Experience Platform desempenha um papel importante nessa jornada. Plataforma são os cérebros para a comunicação, a **sistema de registro de experiência**.

Plataforma é um ambiente no qual a palavra cliente é mais ampla do que apenas os clientes conhecidos. Um visitante desconhecido no site também é um cliente da perspectiva da Platform e, como tal, todo o comportamento como um visitante desconhecido também é enviado para a Platform. Graças a essa abordagem, quando esse visitante eventualmente se torna um cliente conhecido, uma marca também pode visualizar o que aconteceu antes desse momento. Isso ajuda de uma perspectiva de atribuição e otimização de experiência.

## Fluxo de jornada do cliente

Ir para [https://bootcamp.aepdemo.net](https://bootcamp.aepdemo.net). Clique em **Permitir todos**.

![DSN](./images/web8.png)

Clique no ícone do logotipo do Adobe no canto superior esquerdo da tela para abrir o Visualizador de perfis.

![Demonstração](./images/pv1.png)

Dê uma olhada no painel Visualizador de perfis e no Perfil do cliente em tempo real com o **ID do Experience Cloud** como o identificador principal deste cliente atualmente desconhecido.

![Demonstração](./images/pv2.png)

Você também pode ver todos os Eventos de experiência que foram coletados com base no comportamento do cliente. A lista está vazia no momento, mas isso será alterado em breve.

![Demonstração](./images/pv3.png)

Vá para a **Serviços de aplicativos** e clique no produto **Real-Time CDP**.

![Demonstração](./images/pv4.png)

Você verá a página de detalhes do produto. Um Evento de experiência do tipo **Exibição do produto** agora foi enviado para a Adobe Experience Platform usando a implementação do SDK da Web que você analisou no Módulo 1. Abra o painel Visualizador de perfis e consulte sua **Eventos de experiência**.

![Demonstração](./images/pv5.png)

Vá para a **Serviços de aplicativos** e clique no produto **Adobe Journey Optimizer**. Outro evento de experiência foi enviado para o Adobe Experience Platform.

![Demonstração](./images/pv7.png)

Abra o painel Visualizador de perfis. Agora você verá dois Eventos de experiência do tipo **Exibição do produto**. Embora o comportamento seja anônimo, cada clique é rastreado e armazenado no Adobe Experience Platform. Assim que o cliente anônimo se tornar conhecido, poderemos unir todos os comportamentos anônimos automaticamente ao perfil conhecido.

![Demonstração](./images/pv8.png)

Agora vamos analisar o perfil do cliente e usar seu comportamento para personalizar sua experiência com o cliente no site.

Próxima etapa: [1.2 Visualizar seu próprio perfil de cliente em tempo real - Interface do usuário](./ex2.md)

[Voltar para Fluxo de Usuário 1](./uc1.md)

[Voltar a todos os módulos](../../overview.md)
