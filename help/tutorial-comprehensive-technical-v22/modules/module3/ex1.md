---
title: Foundation - Perfil do cliente em tempo real - De desconhecido para conhecido no site
description: Foundation - Perfil do cliente em tempo real - De desconhecido para conhecido no site
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 065d79c5-8979-4992-afb1-4da47bbff74b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 2%

---

# 3.1 De desconhecido para conhecido no site

## Contexto

A jornada de desconhecido para conhecido é um dos tópicos mais importantes entre as marcas nos dias de hoje, assim como a jornada do cliente desde a aquisição até a retenção.

A Adobe Experience Platform tem um papel enorme nesta jornada. Plataforma é o cérebro da comunicação, o &quot;sistema de experiência do registro&quot;.

A Platform é um ambiente no qual o termo cliente é mais amplo do que apenas os clientes conhecidos. Um visitante desconhecido no site também é um cliente da perspectiva da Platform e, como tal, todo o comportamento como um visitante desconhecido também é enviado para a Platform. Graças a essa abordagem, quando esse visitante se torna um cliente conhecido, uma marca pode visualizar o que aconteceu antes desse momento também. Isso ajuda na perspectiva de atribuição e otimização de experiência.

## Fluxo de jornada do cliente

Ir para [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Depois de fazer logon com sua Adobe ID, você verá isso. Clique no projeto do seu site para abri-lo.

![DSN](../module0/images/web8.png)

No **Telas** página, clique em **Executar**.

![DSN](../module1/images/web2.png)

Você verá seu site de demonstração aberto. Selecione o URL e copie-o para a área de transferência.

![DSN](../module0/images/web3.png)

Abra uma nova janela incógnita do navegador.

![DSN](../module0/images/web4.png)

Cole o URL do site de demonstração, que você copiou na etapa anterior. Em seguida, você será solicitado a fazer logon usando sua Adobe ID.

![DSN](../module0/images/web5.png)

Selecione o tipo de conta e conclua o processo de logon.

![DSN](../module0/images/web6.png)

Você verá seu site carregado em uma janela incógnita do navegador. Para cada demonstração, você precisará usar uma nova janela incógnita do navegador para carregar o URL do site de demonstração.

![DSN](../module0/images/web7.png)

Clique no ícone do logotipo do Adobe no canto superior esquerdo da tela para abrir o Visualizador de perfil.

![Demonstração](../module2/images/pv1.png)

Consulte o painel Visualizador de perfil e o Perfil do cliente em tempo real com a **Experience Cloud ID** como o identificador principal para este cliente atualmente desconhecido.

![Demonstração](../module2/images/pv2.png)

Você também pode ver todos os Eventos de experiência coletados com base no comportamento do cliente. A lista está vazia no momento, mas será alterada em breve.

![Demonstração](../module2/images/pv3.png)

Vá para o **Homens** categoria do produto. Em seguida, clique no produto **Montana Wind Jacket**.

![Demonstração](../module2/images/pv4.png)

Você verá a página de detalhes do produto. Um Evento de experiência do tipo **Exibição do produto** O foi enviado para o Adobe Experience Platform usando a implementação do SDK da Web que você revisou no Módulo 1.

![Demonstração](../module2/images/pv5.png)

Abra o painel Visualizador do provedor e dê uma olhada em seu **Eventos de experiência**.

![Demonstração](../module2/images/pv6.png)

Volte para o **Women** e clique em outro produto. Outro evento de experiência foi enviado para o Adobe Experience Platform.

![Demonstração](../module2/images/pv7.png)

Abra o painel Visualizador de perfil. Agora você verá dois Eventos de experiência do tipo **Exibição do produto**. Embora o comportamento seja anônimo, podemos rastrear cada clique e armazená-lo no Adobe Experience Platform. Quando o cliente anônimo se tornar conhecido, poderemos mesclar todos os comportamentos anônimos automaticamente no perfil conhecido.

![Demonstração](../module2/images/pv8.png)

Vá para a página Registrar/fazer logon . Clique em **CRIAR UMA CONTA**.

![Demonstração](../module2/images/pv9.png)

Preencha os detalhes e clique em **Registrar** depois disso, você será redirecionado para a página anterior.

![Demonstração](../module2/images/pv10.png)

Abra o painel Visualizador de perfil e acesse Perfil do cliente em tempo real. No painel Visualizador de perfil, você deve ver todos os seus dados pessoais exibidos, como o email e os identificadores de telefone adicionados recentemente.

![Demonstração](../module2/images/pv11.png)

No painel Visualizador de perfil, acesse Eventos de experiência. Você verá os 2 produtos que visualizou anteriormente no painel Visualizador de perfil. Ambos os eventos agora também estão conectados ao seu perfil &quot;conhecido&quot;.

![Demonstração](../module2/images/pv12.png)

Agora você assimilou dados no Adobe Experience Platform e vinculou esses dados a identificadores como ECIDs e endereços de email. O objetivo disso é entender o contexto comercial do que você está prestes a fazer. No próximo exercício, você começará a configurar tudo o que precisa para possibilitar a assimilação de dados.

### Navegar pelo aplicativo móvel

Depois de se tornar um cliente conhecido, é hora de começar a usar o aplicativo móvel. Abra o aplicativo móvel no iPhone e faça logon no aplicativo.

Se você não tiver mais o aplicativo instalado ou se não se lembrar de como instalá-lo, consulte aqui: [0.5 Usar o aplicativo móvel](../module0/ex5.md)

Após instalar o aplicativo conforme as instruções, você verá a página de aterrissagem do aplicativo com a marca Luma carregada. Clique no ícone da conta na parte superior esquerda da tela.

![Demonstração](./images/app_hp.png)

Na tela Logon , faça logon com o endereço de email usado no site da área de trabalho. Clique em **Logon**.

![Demonstração](./images/app_acc.png)

Vá para a tela inicial do aplicativo e clique em para abrir qualquer produto.

![Demonstração](./images/app_hp.png)

Você verá a página de detalhes do produto.

![Demonstração](./images/app_carst.png)

Vá para a tela inicial no aplicativo e passe o dedo à esquerda na tela para exibir o painel Visualizador de perfil. Você verá o produto que acabou de exibir no **Eventos de experiência** , juntamente com todas as visualizações de produtos da sessão do site anterior.

![Demonstração](./images/app_after_carst.png)

Agora, volte para o seu computador desktop e atualize a página inicial, depois disso você verá o produto aparecer lá também.

![Demonstração](./images/lb_x_aftermobile.png)

Agora você assimilou dados no Adobe Experience Platform e vinculou esses dados a identificadores como ECIDs e endereços de email. O objetivo deste exercício era entender o contexto comercial do que você está prestes a fazer. Agora você criou efetivamente um perfil de cliente em tempo real e entre dispositivos. No próximo exercício, você irá em frente e visualizará seu perfil no Adobe Experience Platform.

Próxima etapa: [3.2 Visualizar seu próprio perfil de cliente em tempo real - Interface do usuário](./ex2.md)

[Voltar ao Módulo 3](./real-time-customer-profile.md)

[Voltar para todos os módulos](../../overview.md)
