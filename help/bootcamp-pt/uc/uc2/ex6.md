---
title: Bootcamp - Personalização no call center - Brasil
description: Bootcamp - Personalização no call center - Brasil
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# 2.6 Personalização na central de atendimento

Como já foi discutido várias vezes durante o bootcamp, personalizar a experiência do cliente é algo que deve acontecer de forma omnicanal. Geralmente, uma central de atendimento é bastante desconectada do resto da jornada do cliente e isso geralmente resulta em experiências frustrantes para o cliente, mas não precisa ser. Vamos mostrar um exemplo de como a central de atendimento pode ser facilmente conectada ao Adobe Experience Platform, em tempo real.

## Fluxo de Jornada do cliente

No exercício anterior, usando o aplicativo móvel, você comprou um produto clicando no botão **Comprar** botão.

![DSN](./images/app20.png)

Vamos supor que você tem uma pergunta sobre o status do seu pedido, o que você faria? Normalmente, você chamaria a central de atendimento.

Antes de ligar para a central de atendimento, você precisa saber seu **ID de fidelidade**. Você pode encontrar sua ID de fidelidade no Visualizador de perfil do site.

![DSN](./images/cc1.png)

Nesse caso, a variável **ID de fidelidade** é **5863105**. Como parte da implementação personalizada do recurso call center no ambiente de demonstração, é necessário adicionar um prefixo à **ID de fidelidade**. O prefixo é **11373**, portanto, a ID de fidelidade a ser usada neste exemplo é **11373 5863105**.

Vamos fazer isso agora. Use seu telefone e ligue para o número **+1 (323) 745-1670**.

![DSN](./images/cc2.png)

Você será solicitado a inserir sua ID de fidelidade, seguido por **#**. Insira sua ID de fidelidade.

![DSN](./images/cc3.png)

Você vai ouvir **Olá, primeiro nome**. Esse nome é obtido do Perfil do cliente em tempo real no Adobe Experience Platform. Você então tem três opções. Número da imprensa **1**, **Status do pedido**.

![DSN](./images/cc4.png)

Depois de ouvir o status do pedido, você terá a opção de pressionar **1** para voltar ao menu principal ou, em seguida, pressione 2. Press **2**.

![DSN](./images/cc5.png)

Você será solicitado a classificar sua experiência na central de atendimento, selecionando um número entre 1 e 5, sendo 1 baixo e 5 alto. Faça sua escolha.

![DSN](./images/cc6.png)

Sua chamada para a central de atendimento agora terminará.

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você será direcionado para a página inicial do Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, é necessário selecionar um **sandbox**. A sandbox a ser selecionada é chamada de ``Bootcamp``. Você pode fazer isso clicando no texto **[!UICONTROL Produto de produção]** na linha azul na parte superior da tela. Depois de selecionar a [!UICONTROL sandbox], você verá a tela mudar e agora você estará em seu [!UICONTROL sandbox].

![Assimilação de dados](./images/sb1.png)

No menu esquerdo, acesse **Perfis** e **Procurar**.

![Perfil do cliente](./images/homemenu.png)

Selecione o **Namespace de identidade** **Email** e insira o endereço de email do perfil do cliente. Clique em **Exibir**. Clique em para abrir o perfil.

![DSN](./images/cc7.png)

Você verá seu perfil de cliente novamente. Ir para **Eventos**.

![DSN](./images/cc8.png)

Em eventos, você verá 2 eventos com um eventType de **callCenter**. O primeiro evento é o resultado da sua resposta à pergunta **Avalie a satisfação da sua chamada**.

![DSN](./images/cc9.png)

Role um pouco para baixo e você verá o evento que foi gravado quando você selecionou a opção para verificar a **Status do pedido**.

![DSN](./images/cc10.png)

Ir para **Associação de segmento**. Agora você verá que 2 segmentos se qualificam no seu perfil, em tempo real, com base nas interações que você teve por meio da central de atendimento. Essas associações de segmento podem e devem ser usadas para afetar o que a comunicação e a personalização ocorrem em qualquer outro canal.

![DSN](./images/cc11.png)

Você já terminou este exercício.

[Voltar para Fluxo de Usuário 2](./uc2.md)

[Voltar para todos os módulos](../../overview.md)
