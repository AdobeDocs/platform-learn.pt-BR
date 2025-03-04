---
title: Foundation - Assimilação de dados - De desconhecido para conhecido no site
description: Foundation - Assimilação de dados - De desconhecido para conhecido no site
kt: 5342
doc-type: tutorial
exl-id: 0971dc78-f45d-41b0-a588-ae3c5c6588d8
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 1%

---

# 1.2.1 De desconhecido para conhecido no site

## Contexto

A jornada do desconhecido para o conhecido é um dos tópicos mais importantes entre as marcas atualmente, assim como a jornada do cliente, desde a aquisição até a retenção.

O Adobe Experience Platform desempenha um papel importante nessa jornada. Plataforma é o cérebro para a comunicação, a experiência do sistema de registro.

Plataforma é um ambiente no qual a palavra **cliente** é mais ampla do que apenas os **clientes** conhecidos. Isso é algo muito importante a ser mencionado ao falar com as marcas: um visitante desconhecido no site também é um cliente da perspectiva da Platform e, como tal, todo o comportamento como visitante desconhecido também é enviado para a Platform. Graças a essa abordagem, quando esse cliente eventualmente se torna um cliente conhecido, uma marca também pode visualizar o que aconteceu antes desse momento. Isso ajuda de uma perspectiva de atribuição e otimização de experiência.

## O que você vai fazer

Agora, você assimilará dados na Adobe Experience Platform e esses dados serão vinculados a identificadores como ECIDs e endereços de email. O objetivo disso é entender o contexto de negócios do que você está prestes a fazer de uma perspectiva de configuração. No próximo exercício, você começará a configurar tudo o que precisa para tornar possível a assimilação de dados em seu próprio ambiente de sandbox.

### Fluxo de Jornada do cliente

Ir para [https://dsn.adobe.com](https://dsn.adobe.com). Depois de fazer logon com sua Adobe ID, você verá isso. Clique nos 3 pontos **...** do projeto do site e clique em **Executar** para abri-lo.

![DSN](./../../datacollection/dc1.1/images/web8.png)

Você verá seu site de demonstração aberto. Selecione o URL e copie-o para a área de transferência.

![DSN](./../../../getting-started/gettingstarted/images/web3.png)

Abra uma nova janela incógnita do navegador.

![DSN](./../../../getting-started/gettingstarted/images/web4.png)

Cole o URL do site de demonstração que você copiou na etapa anterior. Você será solicitado a fazer logon usando sua Adobe ID.

Selecione o tipo de conta e conclua o processo de logon.

Em seguida, você verá seu site carregado em uma janela incógnita do navegador. Para cada demonstração, será necessário usar uma janela do navegador nova e incógnita para carregar o URL do site de demonstração.

Clique no ícone do logotipo do Adobe no canto superior esquerdo da tela para abrir o Visualizador de perfis.

![Demonstração](./images/pv1.png)

Consulte o painel Visualizador de perfis e o Perfil do cliente em tempo real com a **Experience Cloud ID** como o identificador principal para este cliente atualmente desconhecido.

![Demonstração](./images/pv2.png)

Você também pode ver todos os Eventos de experiência que foram coletados com base no comportamento do cliente. A lista está vazia no momento, mas isso será alterado em breve.

![Demonstração](./images/pv3.png)

Vá para a categoria de produto **Celulares e dispositivos**. Em seguida, clique no produto **iPhone 15 Pro**.

![Demonstração](./images/pv4.png)

Você verá a página de detalhes do produto. Um Evento de Experiência do tipo **Exibição do Produto** foi enviado ao Adobe Experience Platform usando a implementação do Web SDK que você analisou no módulo anterior.

![Demonstração](./images/pv5.png)

Abra o painel Visualizador de perfis e veja seus **Eventos de experiência**.

>[!NOTE]
>
>Se você não visualizar o evento imediatamente, atualize a página.

![Demonstração](./images/pv6.png)

Volte para a página de categoria **Telefones e dispositivos** e clique em outro produto. Outro evento de experiência foi enviado para o Adobe Experience Platform.

Abra o painel Visualizador de perfis. Você verá dois Eventos de Experiência do tipo **Exibição do Produto**. Embora o comportamento seja anônimo, com o consentimento adequado em vigor, podemos rastrear cada clique e armazená-lo no Adobe Experience Platform. Assim que o cliente anônimo se tornar conhecido, poderemos unir todos os comportamentos anônimos automaticamente ao perfil conhecido.

![Demonstração](./images/pv7.png)

Clique em **Entrar** para ir para a página de Registro/Logon.

![Demonstração](./images/pv8.png)

Clique em **Criar uma conta**.

![Demonstração](./images/pv9.png)

Preencha seus detalhes e clique em **Registrar**; depois disso, você será redirecionado para a página anterior.

![Demonstração](./images/pv10.png)

Abra o painel Visualizador de perfis e vá para Perfil do cliente em tempo real. No painel Visualizador de perfis, você deve ver todos os seus dados pessoais exibidos, como emails recém-adicionados e identificadores de telefone.

![Demonstração](./images/pv11.png)

No painel Visualizador de perfis, acesse Eventos de experiência. Você verá os dois produtos que visualizou antes no painel Visualizador de perfis. Ambos os eventos agora também estão conectados ao seu perfil &quot;conhecido&quot;.

![Demonstração](./images/pv12.png)

Agora você assimilou dados na Adobe Experience Platform e vinculou esses dados a identificadores como ECIDs e endereços de email. O objetivo disso é entender o contexto de negócios do que você está prestes a fazer. No próximo exercício, você começará a configurar tudo o que precisa para tornar possível toda a assimilação de dados.

## Próximas etapas

Ir para [1.2.2 Configurar Esquemas e Definir Identificadores](./ex2.md){target="_blank"}

Voltar para [Assimilação de dados](./data-ingestion.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
