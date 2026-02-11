---
title: Configurar uma campanha com mensagens no aplicativo
description: Configurar uma campanha com mensagens no aplicativo
kt: 5342
doc-type: tutorial
exl-id: c40b9b8c-9717-403c-bf02-6b8f42a59c05
source-git-commit: 2d5ca888eb24c1f65b4ecd48030ec8d1659b7f84
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# 3.3.3 Configurar uma campanha com mensagens no aplicativo

Faça login no Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`. Você estará na exibição **Página inicial** da sua sandbox `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## 3.3.3.1 Configuração do canal de mensagens no aplicativo

No menu esquerdo, vá para **Canais** e selecione **Configurações de canal**. Clique em **Criar configuração de canal**.

![NoAplicativo](./images/inapp1.png)

Insira o nome: `--aepUserLdap--_In-app_Messages`, selecione o canal **Mensagens no aplicativo** e habilite as plataformas **Web**, **iOS** e **Android**.

![NoAplicativo](./images/inapp2.png)

Role para baixo para vê-lo.

![NoAplicativo](./images/inapp3.png)

Verifique se a **Página única** está habilitada.

Para **Web**, insira a URL do site que foi criado anteriormente como parte do módulo **Introdução**, que tem esta aparência: `https://dsn.adobe.com/web/--aepUserLdap---XXXX`. Não esqueça de alterar o **XXXX** para o código exclusivo do seu site.

Para **iOS** e **Android**, digite `com.adobe.dsn.dxdemo`.

![NoAplicativo](./images/inapp4.png)

Role para cima e clique em **Enviar**.

![NoAplicativo](./images/inapp5.png)

A configuração do canal agora está pronta para ser usada.

![NoAplicativo](./images/inapp6.png)

## 3.3.3.2 Configurar uma campanha agendada para Mensagens no aplicativo

No menu esquerdo, vá para **Campanhas** e clique em **Criar campanha**.

![NoAplicativo](./images/inapp7.png)

Selecione **Agendado - Marketing** e clique em **Criar**.

![NoAplicativo](./images/inapp8.png)

Insira o nome `--aepUserLdap-- - CitiSignal Fiber Max` e clique em **Ações**.

![NoAplicativo](./images/inapp9.png)

Clique em **+ Adicionar ação** e selecione **Mensagem no aplicativo**.

![NoAplicativo](./images/inapp10.png)

Selecione a configuração do canal de mensagens no aplicativo que você criou na etapa anterior, chamada: `--aepUserLdap--_In-app_Messages`. Clique em **Editar conteúdo**.

![NoAplicativo](./images/inapp11.png)

Você deverá ver isso. Clique em **Modal**.

![NoAplicativo](./images/inapp12.png)

Clique em **Alterar layout**.

![NoAplicativo](./images/inapp13.png)

Clique no ícone **URL de mídia** para escolher um ativo do AEM Assets.

![NoAplicativo](./images/inapp14.png)

Vá para a pasta **citisignal-images** e selecione o arquivo de imagem **neon-rabbit.jpg**. Clique em **Selecionar**.

![NoAplicativo](./images/inapp15.png)

Para o texto **Cabeçalho**, use: `CitiSignal Fiber Max`.
Para o texto **Corpo**, use: `Conquer lag with Fiber Max`.

![NoAplicativo](./images/inapp16.png)

Defina o **Botão #1 text** para: `Go to Plans`.
Defina o **target** para `com.adobe.dsn.dxdemo://plans`.

Clique em **Revisar para ativar**.

![NoAplicativo](./images/inapp17.png)

Clique em **Ativar**.

![NoAplicativo](./images/inapp18.png)

O status da sua campanha agora está definido como **Ativando**. Pode levar alguns minutos para que a campanha seja ativada.

![NoAplicativo](./images/inapp19.png)

Depois que o status for alterado para **Live**, você poderá testar sua campanha.

![NoAplicativo](./images/inapp20.png)

## 3.3.3.3 Testar sua campanha de Mensagens no aplicativo em dispositivos móveis

No dispositivo móvel, abra o aplicativo. Você deve ver a nova mensagem no aplicativo aparecer após iniciar o aplicativo. Clique no botão **Ir para Planos**.

![NoAplicativo](./images/inapp21.png)

Você será direcionado à página **Planos**.

![NoAplicativo](./images/inapp22.png)

## Próximas etapas

Voltar para [Adobe Journey Optimizer: Mensagens por push e no aplicativo](ajopushinapp.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
