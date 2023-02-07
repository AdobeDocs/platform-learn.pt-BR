---
title: Bootcamp - Personalização no call center - Brasil
description: Bootcamp - Personalização no call center - Brasil
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 5d824244766135cd4998feab48be7f6a69c42a70
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---

# 2.6 Personalização sem central de atendimento

Conforme discutido durante persona bootcamp experiência do cliente é algo que precisa acontecer de maneira omnichannel. Um call center geralmente é bastante desconectado do restante da jornada do cliente e isso, com a frequência, com experiências frustrantes do cliente, mas não preciso ser assim. Vamos mostrar um exemplo como ligar para o centro de conectado à Adobe Experience Platform, em tempo real.

## Fluxo da jornada do cliente

Sem clicando anterior, usando o aplicativo, você comprou um móvel não **Comprar**.

![DSN](./images/app20.png)

Vamos supor que você tem uma pergunta sobre o status do pedido, o que você faria? Normalmente, você ligaria para o centro de atendimento.

Antes de Para para o call center, você precisa de sabre **ID de fidelidade**. Você pode congelar ID de fidelidade no site.

![DSN](./images/cc1.png)

Caso, **ID de fidelidade** é **5863105**. Como parte de implementação persondo calendário de demonstração, Centro de Chamada (Nd.1) Alteração de  **ID de fidelidade**. O é **11373**, portanto, ou ID de fidelidade, um utilizador aninhado exemplo é **11373 5863105**.

Vamos fazer isso agora. Use seu telefone e ligue para o número **+1 (323) 745-1670**.

![DSN](./images/cc2.png)

Será solicitado que você insira de fidelidade, seguido de **#**. Digite de fidelidade.

![DSN](./images/cc3.png)

Você vem **Olá, teu nome**. Esse nome é retirado do Perfil do tempo real no Adobe Experience Platform. Você tem 3 escolhas. Pressione o número **1**, **Status do pedido**.

![DSN](./images/cc4.png)

Depois de expresso o status do seu pedido, você terá **1** para avançar menu ao principal ou pressionar 2. Pressione **2**.

![DSN](./images/cc5.png)

Em sua solicitado que você está disponível, selecionando um número entre 1 e 5, sendo 1. Faça a sua escolha.

![DSN](./images/cc6.png)

Sua música para o centro de será encerr.

Acesse [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de &quot;Faça&quot;, você vai acessar um início do logon no Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, você precisa selecionar um **sandbox**. O nome do sandbox a ser selecionado é ``Bootcamp``. É possível isto clicando texto **[!UICONTROL Produto de produção]** na linha azul na parte superior da tela. Depois de selecionar o [!UICONTROL sandbox] apropriado, você verá a tela mudando e agora está em seu [!UICONTROL sandbox] dedicado.

![Assimilação de dados](./images/sb1.png)

Sem menu à esquerda, acesse **Perfis** e **Procurar**.

![Perfil do cliente](./images/homemenu.png)

Selecione o **Namespace de identidade** **Email** e insira de e-mail do seu cliente de endereço. Clique em **Exibir**. Clique para te.

![DSN](./images/cc7.png)

Você tem um trajeto especial. Acesse **Eventos**.

![DSN](./images/cc8.png)

Evento em, você verá 2 eventos com um eventType de **callCenter**. O evento é o resultado da sua pergunta **Avalie a satisfação da sua chamada** da África do Sul).

![DSN](./images/cc9.png)

Função um pouco e você verá o que foi registrado selecion você ou um verificar o **Status do pedido**.

![DSN](./images/cc10.png)

Acesse **Associação de segmento**. Agora verá que você se qualifica em seu, em tempo real, com base nas interações que você tem por meio centro de atendimento. associações de segmento podem e devem ser usadas para impactar igual comunicação personalização em qualquer outro canal.

![DSN](./images/cc11.png)

Você terminou este.

[Retornar para Fluxo 2](./uc2.md)

[Retornar para Todos os Módulos](../../overview.md)
