---
title: Bootcamp - Mesclando físico e digital - Use o aplicativo móvel e acione entrada de beacon - Brasil
description: Bootcamp - Mesclando físico e digital - Use o aplicativo móvel e acione entrada de beacon - Brasil
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

# 3.1 Usar o aplicativo móvel e acionar uma entrada de beacon

## Instalar o aplicativo móvel

Antes de instalar o aplicativo, é necessário ativar **Rastreamento** no seu dispositivo iOS. Para fazer isso, acesse **Configurações** > **Privacidade e segurança** > **Rastreamento** e garantir que a opção **Permitir que aplicativos solicitem rastreamento**.

![DSN](./../uc3/images/app4.png)

Vá para a Apple App Store e pesquise por `aepmobile-bootcamp`. Clique em **Instalar** ou **Baixar**.

![DSN](./../uc3/images/app1.png)

Depois que o aplicativo estiver instalado, clique em **Abrir**.

![DSN](./../uc3/images/app2.png)

Clique em **OK**.

![DSN](./../uc3/images/app9.png)

Clique em **Permitir**.

![DSN](./../uc3/images/app3.png)

Clique em **Concordo**.

![DSN](./../uc3/images/app7.png)

Clique em **Permitir Ao Usar Aplicativo**.

![DSN](./../uc3/images/app8.png)

Clique em **Permitir**.

![DSN](./../uc3/images/app5.png)

Agora você está no aplicativo, na página inicial, pronto para passar pela jornada do cliente.

![DSN](./../uc3/images/app12.png)

## Fluxo de jornada do cliente

Primeiro de tudo, você precisa fazer logon. Clique em **Logon**.

![DSN](./images/app13.png)

Depois de criar sua conta nos exercícios anteriores, você viu isso no site. Agora é necessário reutilizar o endereço de email da conta criada no aplicativo para fazer logon.

![Demonstração](./images/pv1.png)

Digite o endereço de email que você usou no site aqui e clique em **Logon**.

![DSN](./images/app14.png)

Em seguida, você receberá uma confirmação de que está conectado e receberá uma notificação por push.

![DSN](./images/app15.png)

Retorne à página inicial no aplicativo e você verá recursos adicionais serem exibidos.

![DSN](./images/app17.png)

Primeiro, acesse **Produtos**. Clique em qualquer produto, neste exemplo **Café para ir**.

![DSN](./images/app19.png)

Você verá o **Café para ir** página do produto no aplicativo.

![DSN](./images/app20.png)

Agora você simulará um evento de entrada de beacon em um local de armazenamento offline. O objetivo de simular isso é personalizar a experiência do cliente nas telas da loja. Para visualizar a experiência na loja, uma página foi criada e mostrará dinamicamente as informações relevantes para o cliente que acabou de entrar na loja.

Antes de continuar, abra esta página da Web no seu computador: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

Você verá isso:

![DSN](./images/screen1.png)

Em seguida, volte para a página inicial. Clique no botão **beacon** ícone .

![DSN](./images/app23.png)

Você verá isso. Primeiro, selecione **Beacon de tela de bootcamp** e clique no botão **entrada** botão. Isso permitirá simular uma entrada de beacon.

![DSN](./images/app21.png)

Agora, dê uma olhada na tela da loja. Você verá o último produto exibido lá em 5 segundos.

![DSN](./images/screen2.png)

Então, volte para **Produtos**. Clique em qualquer produto, neste exemplo **Balão de praia - Tan**.

![DSN](./images/app22.png)

Em seguida, volte para a página inicial. Clique no botão **beacon** ícone .

![DSN](./images/app23.png)

Você verá isso. Primeiro, selecione **Beacon de tela de bootcamp** e clique no botão **entrada** novamente. Isso permitirá simular uma entrada de beacon.

![DSN](./images/app21.png)

Agora, dê uma olhada na tela da loja novamente. Você verá o último produto exibido lá em 5 segundos.

![DSN](./images/screen3.png)

Também vamos consultar seu Visualizador de perfil no site agora. Você verá muitos eventos que foram adicionados lá, apenas para mostrar que qualquer interação com um cliente é coletada e armazenada no Adobe Experience Platform.

![DSN](./images/screen4.png)

Nos próximos exercícios, você configurará e testará sua própria jornada de entrada de beacon.

Próxima etapa: [3.2 Criar seu evento](./ex2.md)

[Voltar para Fluxo de Usuário 3](./uc3.md)

[Voltar para todos os módulos](../../overview.md)
