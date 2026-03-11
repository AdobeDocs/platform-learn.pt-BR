---
title: Dimensionar fragmentos de conteúdo com o servidor ChatGPT e MCP
description: Dimensionar fragmentos de conteúdo com o servidor ChatGPT e MCP
kt: 5342
doc-type: tutorial
exl-id: b7105351-e9de-4b2c-b3d7-2d4c8627f852
source-git-commit: a57050bf40105a0b0c6d4ce615aa640e878ece12
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 1%

---

# 1.6.3 Dimensionar fragmentos de conteúdo com o servidor ChatGPT e MCP

>[!IMPORTANT]
>
>Para concluir este exercício, você precisa ter acesso a um ambiente de trabalho do AEM Sites e do Assets CS com EDS e os vários agentes do AEM precisam estar habilitados para a organização IMS que você está usando.
>
>Se você ainda não tiver esse ambiente, vá para o exercício [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Siga as instruções aqui e você terá acesso a esse ambiente.

>[!IMPORTANT]
>
>Se você configurou anteriormente um programa do AEM CS com um ambiente do AEM Sites e do Assets CS, pode ser que sua sandbox do AEM CS tenha hibernado. Considerando que a deshibernação de uma sandbox desse tipo leva de 10 a 15 minutos, seria uma boa ideia iniciar o processo de deshibernação agora para que você não precise aguardar mais tarde.

## 1.6.3.1 Criar modelo de fragmento de conteúdo

Volte para o ambiente de Autor do Adobe Experience Manager, para **Ferramentas** e vá para **Navegador de Configuração**.

![Agentes da AEM](./images/aemagentscfm1.png)

Clique em **Criar**.

![Agentes da AEM](./images/aemagentscfm2.png)

Use `Content Fragments` para os campos **Título** e **Nome**.

Verifique se as opções **Modelos de fragmento do conteúdo** e **Consultas GraphQL persistidas** estão habilitadas.

Clique em **Criar**.

![Agentes da AEM](./images/aemagentscfm3.png)

Volte para o ambiente de autor do Adobe Experience Manager e vá para **Fragmentos de conteúdo**.

![Agentes da AEM](./images/aemagentscf1.png)

Vá para **Modelos de fragmentos do conteúdo**, selecione sua configuração **Fragmentos do conteúdo** e clique em **Criar**.

![Agentes da AEM](./images/aemagentscfm4.png)

Use o nome `--aepUserLdap-- - CitiSignal CFM`. Clique em **Criar e abrir**.

![Agentes da AEM](./images/aemagentscfm5.png)

Você deverá ver isso. Arraste e solte um campo **Texto de linha única** sobre a tela.

![Agentes da AEM](./images/aemagentscfm6.png)

Altere o campo **Rótulo do campo** para `Header`.

![Agentes da AEM](./images/aemagentscfm7.png)

Volte para **Tipos de Dados**. Arraste e solte um campo **Texto de linha única** sobre a tela.

![Agentes da AEM](./images/aemagentscfm8.png)

Altere o campo **Rótulo do campo** para `Subheader`.

![Agentes da AEM](./images/aemagentscfm9.png)

Volte para **Tipos de Dados**. Arraste e solte um campo **Texto de várias linhas** na tela.

![Agentes da AEM](./images/aemagentscfm10.png)

Altere o campo **Rótulo do campo** para `Detail Description`.

![Agentes da AEM](./images/aemagentscfm11.png)

Volte para **Tipos de Dados**. Arraste e solte um campo **Texto de linha única** sobre a tela.

![Agentes da AEM](./images/aemagentscfm12.png)

Altere o campo **Rótulo do campo** para `CTA Text`.

![Agentes da AEM](./images/aemagentscfm13.png)

Volte para **Tipos de Dados**. Arraste e solte um campo **Texto de linha única** sobre a tela.

![Agentes da AEM](./images/aemagentscfm14.png)

Altere o campo **Rótulo do campo** para `CTA Link`. Clique em **Salvar**.

![Agentes da AEM](./images/aemagentscfm15.png)

Você deverá ver isso.

![Agentes da AEM](./images/aemagentscfm16.png)

Selecione o modelo de fragmento de conteúdo e clique em **Publicar**.

![Agentes da AEM](./images/aemagentscfm17.png)

Clique em **Publicar**.

![Agentes da AEM](./images/aemagentscfm18.png)

## 1.6.3.2 Criar fragmento de conteúdo

Volte para o ambiente de autor do Adobe Experience Manager e vá para **Fragmentos de conteúdo**.

![Agentes da AEM](./images/aemagentscf1.png)

Você deverá ver isso. Clique em **Criar** e selecione **Pasta**.

![Agentes da AEM](./images/aemagentscf2.png)

Digite o título: `--aepUserLdap-- - CF`. Clique em **Criar**.

![Agentes da AEM](./images/aemagentscf3.png)

Volte para o ambiente de Autor do Adobe Experience Manager e vá para **Assets**.

![Agentes da AEM](./images/aemagentscfmm1.png)

Vá para **Arquivos**.

![Agentes da AEM](./images/aemagentscfmm2.png)

Selecione a pasta que acabou de criar, que deve se chamar `--aepUserLdap-- - CF` e clique em **Propriedades**.

![Agentes da AEM](./images/aemagentscfmm3.png)

Vá para **Cloud Services** e clique no ícone **pasta**.

![Agentes da AEM](./images/aemagentscfmm4.png)

Selecione a configuração de nuvem criada anteriormente, que deve se chamar **Fragmentos de conteúdo**. Clique em **Selecionar**.

![Agentes da AEM](./images/aemagentscfmm5.png)

Você deverá ver isso. Clique em **Salvar e fechar**.

![Agentes da AEM](./images/aemagentscfmm6.png)

Volte para o ambiente de autor do Adobe Experience Manager e vá para **Fragmentos de conteúdo**.

![Agentes da AEM](./images/aemagentscf1.png)

Você deverá ver isso. Clique em **Criar** e selecione **Fragmento do conteúdo**.

![Agentes da AEM](./images/aemagentscf4.png)

Selecione o **Modelo de fragmento de conteúdo** criado anteriormente, que deve ser nomeado como `--aepUserLdap-- - CitiSignal CFM`. Use o nome `--aepUserLdap-- CitiSignal Fiber Max`.

Clique em **Criar e abrir**.

![Agentes da AEM](./images/aemagentscf5.png)

Você deverá ver isso.

![Agentes da AEM](./images/aemagentscf5a.png)

Preencha os campos desta forma:

- **Cabeçalho**: `CitiSignal Fiber Max`
- **Subcabeçalho**: `Experience high speed internet now`
- **Descrição detalhada**:

```
Experience the future of connectivity with CitiSignal Fiber Max, the ultimate solution for high-speed internet. Designed for homes and businesses that demand performance, Fiber Max delivers blazing-fast fiber speeds, ensuring seamless streaming, ultra-responsive gaming, and crystal-clear video calls.

Key Features:

Unmatched Speed: Enjoy lightning-fast downloads and uploads powered by cutting-edge fiber technology.
Reliable Performance: Consistent connectivity for work, entertainment, and everything in between.
Future-Ready: Built to handle the growing demands of smart homes and digital lifestyles.
Unlimited Potential: No data caps, no throttling—just pure speed.
Why Choose CitiSignal Fiber Max? Stay ahead with internet that works as hard as you do. Whether you’re powering a remote office or streaming in 4K, Fiber Max ensures you never miss a beat.
```

**Texto do CTA**: `Upgrade now by signing your new contract!`
**Link do CTA**: `https://techinsiders68.adobedemosystem.com/`

Clique em **Publicar** e selecione **Agora**.

![Agentes da AEM](./images/aemagentscf6.png)

Clique em **Publicar**.

![Agentes da AEM](./images/aemagentscf7.png)

## 1.6.3.3 Configurar o servidor MCP no ChatGPT

>[!NOTE]
>
>O uso do Adobe Marketing Agent no ChatGPT requer o seguinte:
>- uma versão paga do ChatGPT Enterprise da OpenAI
>- usar o cliente Web ChatGPT Enterprise

Vá para [https://chatgpt.com/](https://chatgpt.com/){target="_blank"} e faça logon usando os detalhes de sua conta. Depois de fazer logon, você deverá ver isso. Clique no seu nome de usuário e selecione **Configurações**.

![GPTchat](./images/chatgpt2.png)

Vá para **Aplicativos** e selecione **Configurações avançadas**.

![GPTchat](./images/chatgpt3.png)

Ative o **Modo de desenvolvedor** e clique em **Voltar**.

![GPTchat](./images/chatgpt4.png)

Clique em **Criar aplicativo**.

![GPTchat](./images/chatgpt5.png)

Preencha os campos desta forma:

- **Nome**: `aem`
- **URL do Servidor MCP**: `https://mcp.adobeaemcloud.com/adobe/mcp/content`
- **Autenticação**: `OAuth`

Marque a caixa de seleção **Entendo e desejo continuar**.

Clique em **Criar**.

![GPTchat](./images/chatgpt6.png)

O ChatGPT agora tentará se conectar à sua conta da Adobe. Selecione **Permitir acesso** e você terá que fazer logon com sua conta da Adobe.

Depois de fazer logon, você deve ver que seu Adobe Marketing Agent agora está conectado com êxito.

![GPTchat](./images/chatgpt8.png)

## 1.6.3.4 Usar o servidor MCP do AEM no ChatGPT

Feche esta janela.

![Agent Orchestrator](./images/chatgpt8.png)

Você deverá ver isso. Clique no ícone **+**, vá para **Mais** e selecione **aem**.

![Agent Orchestrator](./images/chatgpt10.png)

Digite o prompt a seguir e clique em **Enviar**.

```
I just created a new custom mcp server named 'aem'. what can I do with that?
```

![Agent Orchestrator](./images/chatgpt11.png)

Você deveria ver algo assim. Digite o prompt a seguir e clique em **Enviar**.

```
use the author url https://author-pXXXXXX-eXXXXXXX.adobeaemcloud.com/ from now on
```

![Agent Orchestrator](./images/chatgpt12.png)

Você deveria ver algo assim. Digite o prompt a seguir e clique em **Enviar**.

```
find the content fragment --aepUserLdap-- - CitiSignal Fiber Max and make a variation called --aepUserLdap-- - CitiSignal Fiber Max (FR), then translate all fields into french
```

![Agent Orchestrator](./images/chatgpt13.png)

Clique em **CreateFragmentVariation**.

![Agent Orchestrator](./images/chatgpt14.png)

Clique em **UpdateFragment**.

![Agent Orchestrator](./images/chatgpt15.png)

Você deverá ver isso. A variação do fragmento foi criada com sucesso.

![Agent Orchestrator](./images/chatgpt16.png)

Agora você também pode ver sua nova variação na interface do usuário do AEM.

![Agent Orchestrator](./images/chatgpt17.png)

Em seguida, use o ChatGPT para traduzir o fragmento de conteúdo em mais variações. Digite o prompt a seguir e clique em **Enviar**.

```
now do the same thing for the 5 top country's languages that CitiSignal does business with
```

![Agent Orchestrator](./images/chatgpt18.png)

Confirme sua escolha de idioma.

![Agent Orchestrator](./images/chatgpt23.png)

Clique em **CreateFragmentVariation**.

![Agent Orchestrator](./images/chatgpt22.png)

Clique em **UpdateFragment**.

![Agent Orchestrator](./images/chatgpt24.png)

Repita esse processo para cada idioma selecionado. Depois de concluído, você verá algo assim.

![Agent Orchestrator](./images/chatgpt26.png)

Volte para a interface do usuário do AEM e atualize a tela. Agora você pode ver suas novas variações no fragmento de conteúdo.

![Agent Orchestrator](./images/chatgpt27.png)

## Próximas etapas

Voltar para [AEM e Agentes](./aemagents.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
