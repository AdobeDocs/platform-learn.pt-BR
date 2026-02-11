---
title: Configurar o ambiente de desenvolvimento
description: Configurar o ambiente de desenvolvimento
kt: 5342
doc-type: tutorial
exl-id: c9bfb327-362f-4475-89da-8e9788940d56
source-git-commit: ce3ee3dde103383a6f7897cba36d548058879ea7
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 2%

---

# 1.7.1 Configuração do ambiente de desenvolvimento

## 1.7.1.1 Crie seu projeto do Adobe I/O

Ir para [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}.

Selecione a instância correta no canto superior direito da tela. Sua instância é `--aepImsOrgName--`.

>[!NOTE]
>
> A captura de tela abaixo mostra uma organização específica sendo selecionada. Quando você estiver assistindo a este tutorial, é muito provável que sua organização tenha um nome diferente. Quando se inscreveu neste tutorial, você recebeu os detalhes do ambiente que devem ser usados. Siga estas instruções.

Em seguida, selecione **Criar projeto a partir do modelo**.

![Extensibilidade do GSPeM](./images/commerceagent1.png)

Selecione **App Builder**.

![Extensibilidade do GSPeM](./images/commerceagent2.png)

Digite o nome `--aepUserLdap-- vangeluw Commerce Events`. Clique em **Salvar**.

![Extensibilidade do GSPeM](./images/commerceagent4.png)

Você deveria ver algo assim.

![Extensibilidade do GSPeM](./images/commerceagent5.png)

Clique em **+ Adicionar serviço** e selecione **API**.

![Extensibilidade do GSPeM](./images/commerceagent6.png)

Pesquise e selecione a API **Eventos de E/S**. Clique em **Next**.

![Extensibilidade do GSPeM](./images/commerceagent7.png)

Altere o nome da credencial para `vangeluw Commerce Events - Production`. Clique em **Salvar API configurada**.

![Extensibilidade do GSPeM](./images/commerceagent8.png)

Você deverá ver isso. Clique em **+ Adicionar serviço** e selecione **API**.

![Extensibilidade do GSPeM](./images/commerceagent9.png)

Pesquise e selecione a API **API de Gerenciamento de E/S**. Clique em **Next**.

![Extensibilidade do GSPeM](./images/commerceagent10.png)

Clique em **Salvar API configurada**.

![Extensibilidade do GSPeM](./images/commerceagent11.png)

Você deverá ver isso. Clique em **+ Adicionar serviço** e selecione **API**.

![Extensibilidade do GSPeM](./images/commerceagent12.png)

Pesquise e selecione a API **Adobe Commerce as a Cloud Service**. Clique em **Next**.

![Extensibilidade do GSPeM](./images/commerceagent13.png)

Selecione **Autenticação de Servidor para Servidor**. Clique em **Next**.

![Extensibilidade do GSPeM](./images/commerceagent14.png)

Clique em **Next**.

![Extensibilidade do GSPeM](./images/commerceagent15.png)

Selecionar **Padrão - Cloud Manager**. Clique em **Salvar API configurada**.

![Extensibilidade do GSPeM](./images/commerceagent16.png)

Você deverá ver isso. Clique em **+ Adicionar serviço** e selecione **API**.

![Extensibilidade do GSPeM](./images/commerceagent17.png)

Pesquise e selecione a API **Adobe I/O Events para Adobe Commerce**. Clique em **Next**.

![Extensibilidade do GSPeM](./images/commerceagent18.png)

Clique em **Salvar API configurada**.

![Extensibilidade do GSPeM](./images/commerceagent19.png)

Seu projeto agora está configurado e pode ser usado.

![Extensibilidade do GSPeM](./images/commerceagent20.png)

## 1.7.1.2 Configurar seu ambiente de desenvolvimento

Para criar, enviar e implantar seu aplicativo extensível, seu ambiente de desenvolvimento local no computador deve ter os seguintes aplicativos e pacotes instalados:

- Node.js (versão 20.x ou superior)
- npm (empacotado com Node.js)
- Interface de linha de comando (CLI) do Adobe Developer

Caso esses aplicativos ou pacotes ainda não estejam instalados no computador, siga estas etapas.

### Node.js e npm

Ir para [https://nodejs.org/en/download](https://nodejs.org/en/download). Você deve ver isso, com vários comandos de terminal que precisam ser executados para ter o Node.js e o npm instalados. Os comandos mostrados aqui são aplicáveis ao MacBook.

![Extensibilidade do GSPeM](./images/commerceagent21.png)

Primeiro, abra uma nova janela do terminal. Cole e execute o comando mencionado na linha 2 da captura de tela:

`curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash`

Em seguida, execute o comando na linha 5 da captura de tela:

`\. "$HOME/.nvm/nvm.sh"`

Após executar os dois comandos com êxito, execute este comando:

`node -v`

Você deve ver um número de versão sendo retornado.

![Extensibilidade do GSPeM](./images/commerceagent22.png)

Em seguida, execute este comando:

`npm -v`

Caso o NPM ainda não esteja instalado, você poderá instalá-lo usando este comando: `npm install -g npm@11.9.0`.

Você deve ver um número de versão sendo retornado.

![Extensibilidade do GSPeM](./images/commerceagent23.png)

Se os dois últimos comandos retornarem com êxito um número de versão, sua configuração desses dois recursos será bem-sucedida.

### Interface de linha de comando (CLI) do Adobe Developer

Para instalar a interface de linha de comando (CLI) do Adobe Developer, execute o seguinte comando em uma janela de terminal:

`npm install -g @adobe/aio-cli`

A execução deste comando pode levar alguns minutos. O resultado final deve ser semelhante ao seguinte:

![Extensibilidade do GSPeM](./images/commerceagent24.png)

A interface de linha de comando (CLI) do Adobe Developer agora também foi instalada com êxito.

### Extensão SDK da interface de linha de comando (CLI) do Adobe Developer para Commerce

Para instalar a extensão Adobe I/O SDK para Commerce, execute o seguinte comando em uma janela de terminal:

`npm install @adobe/aio-commerce-sdk`

![Extensibilidade do GSPeM](./images/commerceagent25.png)

### Plug-ins do Adobe Commerce para a CLI do Adobe I/O

Para instalar os plug-ins do Adobe Commerce para a CLI do Adobe I/O, execute o seguinte comando em uma janela de terminal:

`aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime`

![Extensibilidade do GSPeM](./images/commerceagent26.png)

Agora você configurou os elementos básicos para poder executar um projeto do App Builder, em combinação com o Adobe Commerce, o Adobe I/O Events e o Adobe I/O Runtime.

## Próximas etapas

Ir para [Usar Cursor.ai para desenvolver seu projeto](./ex2.md){target="_blank"}

Volte para as [Ferramentas de desenvolvedor inteligente para o Adobe Commerce](./aiassisteddev.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
