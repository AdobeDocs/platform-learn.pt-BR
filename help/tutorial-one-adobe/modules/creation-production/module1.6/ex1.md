---
title: ADOBE IO e APP BUILDER
description: ADOBE IO e APP BUILDER
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
source-git-commit: 52234e7b3b6743db79dec570b1a1f2d3ac4cf1ab
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 1%

---

# 1.6.1 Adobe IO e App Builder

## 1.6.1.1 Crie seu projeto do Adobe I/O

Ir para [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}.

![Extensibilidade do GSPeM](./images/gspemext1.png)

Selecione a instância correta no canto superior direito da tela. Sua instância é `--aepImsOrgName--`.

>[!NOTE]
>
> A captura de tela abaixo mostra uma organização específica sendo selecionada. Quando você estiver assistindo a este tutorial, é muito provável que sua organização tenha um nome diferente. Quando se inscreveu neste tutorial, você recebeu os detalhes do ambiente que devem ser usados. Siga estas instruções.

Em seguida, selecione **Criar projeto a partir do modelo**.

![Extensibilidade do GSPeM](./images/gspemext2.png)

Selecione **App Builder**.

![Extensibilidade do GSPeM](./images/gspemext4.png)

Digite o nome `--aepUserLdap-- GSPeM EXT`. Clique em **Salvar**.

![Extensibilidade do GSPeM](./images/gspemext5.png)

Você deveria ver algo assim.

![Extensibilidade do GSPeM](./images/gspemext6.png)

## 1.6.1.2 Configurar seu ambiente de desenvolvimento

Para criar, enviar e implantar seu aplicativo extensível, seu ambiente de desenvolvimento local no computador deve ter os seguintes aplicativos e pacotes instalados:

- Node.js (versão 20.x ou superior)
- npm (empacotado com Node.js)
- Interface de linha de comando (CLI) do Adobe Developer

Caso esses aplicativos ou pacotes ainda não estejam instalados no computador, siga estas etapas.

### Node.js e npm

Ir para [https://nodejs.org/en/download](https://nodejs.org/en/download). Você deve ver isso, com vários comandos de terminal que precisam ser executados para ter o Node.js e o npm instalados. Os comandos mostrados aqui são aplicáveis ao MacBook.

![Extensibilidade do GSPeM](./images/gspemext7.png)

Primeiro, abra uma nova janela do terminal. Cole e execute o comando mencionado na linha 2 da captura de tela:

`curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash`

Em seguida, execute o comando na linha 5 da captura de tela:

`\. "$HOME/.nvm/nvm.sh"`

Após executar os dois comandos com êxito, execute este comando:

`node -v`

Você deve ver um número de versão sendo retornado.

![Extensibilidade do GSPeM](./images/gspemext8.png)

Em seguida, execute este comando:

`npm -v`

Você deve ver um número de versão sendo retornado.

![Extensibilidade do GSPeM](./images/gspemext9.png)

Se os dois últimos comandos retornarem com êxito um número de versão, sua configuração desses dois recursos será bem-sucedida.

### Interface de linha de comando (CLI) do Adobe Developer

Para instalar a interface de linha de comando (CLI) do Adobe Developer, execute o seguinte comando em uma janela de terminal:

`npm install -g @adobe/aio-cli`

A execução deste comando pode levar alguns minutos. O resultado final deve ser semelhante ao seguinte:

![Extensibilidade do GSPeM](./images/gspemext10.png)

A interface de linha de comando (CLI) do Adobe Developer agora também foi instalada com êxito.

Agora você configurou os elementos básicos para poder executar um projeto do App Builder.

## Próximas etapas

Vá para [Criar seu bucket do AWS S3](./ex2.md){target="_blank"}

Voltar para [GenStudio for Performance Marketing - Extensibilidade](./genstudioext.md){target="_blank"}

Voltar para [Todos os Módulos](./../../../overview.md){target="_blank"}
