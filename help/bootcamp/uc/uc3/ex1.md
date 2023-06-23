---
title: Bootcamp - Mesclagem física e digital - Use o aplicativo móvel e acione uma entrada de sinal
description: Bootcamp - Mesclagem física e digital - Use o aplicativo móvel e acione uma entrada de sinal
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: c33c973b-db8a-49ce-bd6c-a6c4fbe579a0
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# 3.1 Use o aplicativo móvel e acione uma entrada de sinal

## Instalar o aplicativo móvel

Antes de instalar o aplicativo, é necessário ativar **Rastreamento** no dispositivo iOS. Para fazer isso, acesse **Configurações** > **Privacidade e segurança** > **Rastreamento** e garantir que a opção **Permitir que aplicativos solicitem o rastreamento**.

![DSN](./../uc3/images/app4.png)

Acesse o Apple App Store e pesquise por `aepmobile-bootcamp`. Clique em **Instalar** ou **Baixar**.

![DSN](./../uc3/images/app1.png)

Depois que o aplicativo estiver instalado, clique em **Abertura**.

![DSN](./../uc3/images/app2.png)

Clique em **OK**.

![DSN](./../uc3/images/app9.png)

Clique em **Permitir**.

![DSN](./../uc3/images/app3.png)

Clique em **Concordo**.

![DSN](./../uc3/images/app7.png)

Clique em **Permitir ao usar o aplicativo**.

![DSN](./../uc3/images/app8.png)

Clique em **Permitir**.

![DSN](./../uc3/images/app5.png)

Agora você está no aplicativo, na página inicial, pronto para acessar a jornada do cliente.

![DSN](./../uc3/images/app12.png)

## Fluxo de jornada do cliente

Primeiro, é necessário fazer logon. Clique em **Logon**.

![DSN](./images/app13.png)

Depois de criar sua conta nos exercícios anteriores, você viu isso no site. Agora é necessário reutilizar o endereço de email da conta criada no aplicativo para fazer logon.

![Demonstração](./images/pv1.png)

Insira o endereço de email que você usou no site aqui e clique em **Logon**.

![DSN](./images/app14.png)

Você receberá uma confirmação de que está conectado e uma notificação por push.

![DSN](./images/app15.png)

Volte para a página inicial no aplicativo e você verá recursos adicionais aparecendo.

![DSN](./images/app17.png)

Primeiro, vá para **Produtos**. Clique em qualquer produto, neste exemplo **Café para ir**.

![DSN](./images/app19.png)

Você verá o **Café para ir** página do produto no aplicativo.

![DSN](./images/app20.png)

Agora você simulará um evento de entrada de beacon em um local de loja offline. O objetivo da simulação é personalizar a experiência do cliente nas telas da loja. Para visualizar a experiência na loja, foi criada uma página que mostrará dinamicamente as informações relevantes para o cliente que acabou de entrar na loja.

Antes de continuar, abra esta página da Web no computador: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

Você verá isto:

![DSN](./images/screen1.png)

Em seguida, volte para a página inicial. Clique em **sinal** ícone.

![DSN](./images/app23.png)

Você verá isso. Primeiro, selecione **Beacon de tela de bootcamp** e, em seguida, clique no link **entrada** botão. Isso permitirá simular uma entrada de sinal.

![DSN](./images/app21.png)

Agora, dê uma olhada na tela da loja. O último produto exibido aparecerá lá em 5 segundos.

![DSN](./images/screen2.png)

Em seguida, volte para **Produtos**. Clique em qualquer produto, neste exemplo **Bandeja de praia**.

![DSN](./images/app22.png)

Em seguida, volte para a página inicial. Clique em **sinal** ícone.

![DSN](./images/app23.png)

Você verá isso. Primeiro, selecione **Beacon de tela de bootcamp** e, em seguida, clique no link **entrada** botão novamente. Isso permitirá simular uma entrada de sinal.

![DSN](./images/app21.png)

Agora, dê uma olhada na tela da loja novamente. O último produto exibido aparecerá lá em 5 segundos.

![DSN](./images/screen3.png)

Agora também vamos dar uma olhada no seu Visualizador de perfil no site. Você verá muitos eventos que foram adicionados lá, apenas para mostrar que qualquer interação com um cliente é coletada e armazenada no Adobe Experience Platform.

![DSN](./images/screen4.png)

Nos próximos exercícios, você configurará e testará sua própria jornada de entrada de beacon.

Próxima etapa: [3.2 Criar o evento](./ex2.md)

[Voltar para Fluxo de Usuário 3](./uc3.md)

[Voltar a todos os módulos](../../overview.md)
