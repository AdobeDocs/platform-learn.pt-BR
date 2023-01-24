---
title: Bootcamp - Real-time Customer Profile - De unknown to known on the website - Brasil
description: Bootcamp - Real-time Customer Profile - De unknown to known on the website - Brasil
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 1%

---

# 1.1 De desconhecido para conhecido no site

## Contexto

A jornada de desconhecido para conhecido é um dos tópicos mais importantes entre as marcas nos dias de hoje, assim como a jornada do cliente desde a aquisição até a retenção.

A Adobe Experience Platform tem um papel enorme nesta jornada. Plataforma é o cérebro da comunicação, **sistema de experiência**.

A Platform é um ambiente no qual o termo cliente é mais amplo do que apenas os clientes conhecidos. Um visitante desconhecido no site também é um cliente da perspectiva da Platform e, como tal, todo o comportamento como um visitante desconhecido também é enviado para a Platform. Graças a essa abordagem, quando esse visitante se torna um cliente conhecido, uma marca pode visualizar o que aconteceu antes desse momento também. Isso ajuda na perspectiva de atribuição e otimização de experiência.

## Fluxo de jornada do cliente

Ir para [https://bootcamp.aepdemo.net](https://bootcamp.aepdemo.net). Clique em **Permitir Tudo**.

![DSN](./images/web8.png)

Clique no ícone do logotipo do Adobe no canto superior esquerdo da tela para abrir o Visualizador de perfil.

![Demonstração](./images/pv1.png)

Consulte o painel Visualizador de perfil e o Perfil do cliente em tempo real com a **Experience Cloud ID** como o identificador principal para este cliente atualmente desconhecido.

![Demonstração](./images/pv2.png)

Você também pode ver todos os Eventos de experiência coletados com base no comportamento do cliente. A lista está vazia no momento, mas será alterada em breve.

![Demonstração](./images/pv3.png)

Vá para o **Serviços de aplicativos** e clique no produto **Real-Time CDP**.

![Demonstração](./images/pv4.png)

Você verá a página de detalhes do produto. Um Evento de experiência do tipo **Exibição do produto** O foi enviado para o Adobe Experience Platform usando a implementação do SDK da Web que você revisou no Módulo 1. Abra o painel Visualizador de perfil e dê uma olhada em seu **Eventos de experiência**.

![Demonstração](./images/pv5.png)

Vá para o **Serviços de aplicativos** e clique no produto **Adobe Journey Optimizer**. Outro evento de experiência foi enviado para o Adobe Experience Platform.

![Demonstração](./images/pv7.png)

Abra o painel Visualizador de perfil. Agora você verá dois Eventos de experiência do tipo **Exibição do produto**. Embora o comportamento seja anônimo, cada clique é rastreado e armazenado no Adobe Experience Platform. Quando o cliente anônimo se tornar conhecido, poderemos mesclar todos os comportamentos anônimos automaticamente no perfil conhecido.

![Demonstração](./images/pv8.png)

Agora vamos analisar o perfil do cliente e usar seu comportamento para personalizar a experiência do cliente no site.

Próxima etapa: [1.2 Visualizar seu próprio perfil de cliente em tempo real - Interface do usuário](./ex2.md)

[Voltar para Fluxo de Usuário 1](./uc1.md)

[Voltar para todos os módulos](../../overview.md)
