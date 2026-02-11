---
title: Use o Cursor.ai para desenvolver seu projeto
description: Use o Cursor.ai para desenvolver seu projeto
kt: 5342
doc-type: tutorial
source-git-commit: 2bfa7f4bee54df8411c96b001224d2986e9fcaf9
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# 1.7.2 Use o Cursor.ai para desenvolver seu projeto

## 1.7.2.1 Configurar o diretório e as ferramentas

Na área de trabalho, crie um novo diretório com o nome `--aepUserLdap---commerce`

![Commerce e Agente](./images/cursorai1.png)

Clique com o botão direito do mouse em sua pasta e selecione **Novo Terminal na Pasta**.

![Commerce e Agente](./images/cursorai2.png)

Você deverá ver isso.

![Commerce e Agente](./images/cursorai3.png)

Agora é necessário clonar um repositório Github existente, que você pode visualizar [https://github.com/adobe/commerce-integration-starter-kit](https://github.com/adobe/commerce-integration-starter-kit).

Esse repositório é o kit inicial de integração da Adobe que usa o Adobe Developer App Builder para melhorar a confiabilidade da conexão em tempo real e reduzir o tempo de comercialização das integrações entre o Adobe Commerce e outros sistemas de back-office, como ERPs, CRMs e PIMs.

![Commerce e Agente](./images/cursorai4.png)

Há várias maneiras de clonar esse repositório, neste exemplo, é usado o Terminal.

Digite o seguinte comando na janela Terminal e execute-o.

`git clone https://github.com/adobe/commerce-integration-starter-kit`

![Commerce e Agente](./images/cursorai5.png)

Após alguns segundos, você deverá ver esse resultado.

![Commerce e Agente](./images/cursorai6.png)

Em seguida, navegue até a pasta que acabou de ser criada. Digite o seguinte comando e execute-o.

`cd commerce-integration-starter-kit`

![Commerce e Agente](./images/cursorai7.png)

Você deverá ver isso.

![Commerce e Agente](./images/cursorai8.png)

Em seguida, é necessário configurar as ferramentas de extensibilidade do Commerce para Cursor.ai. Digite o seguinte comando e execute-o.

`aio commerce extensibility tools-setup`

![Commerce e Agente](./images/cursorai9.png)

Selecione **Diretório atual**.

![Commerce e Agente](./images/cursorai10.png)

Selecione **Cursor**.

![Commerce e Agente](./images/cursorai11.png)

Selecione **npm**.

![Commerce e Agente](./images/cursorai12.png)

Após alguns minutos, vocês devem ver isso.

![Commerce e Agente](./images/cursorai13.png)

Ao instalar as ferramentas de extensibilidade do Commerce para o Cursor.ai, agora há um servidor MCP disponível como parte de seu ambiente Cursor.ai. Nos próximos exercícios, você usará esse servidor MCP para ajudá-lo a desenvolver e implantar o projeto do construtor de aplicativos.

## 1.7.2.2 Configurar seu webhook

Para este exercício, você precisará de um webhook que precisa ser configurado para que, quando um pedido for criado, o evento de pedido possa ser transmitido para esse webhook. Neste exercício, você usará um terminal de exemplo usando [https://pipedream.com/requestbin](https://pipedream.com/requestbin).

Vá para [https://pipedream.com/requestbin](https://pipedream.com/requestbin), crie uma conta e um espaço de trabalho. Depois que o espaço de trabalho for criado, você verá algo semelhante a isso.

Clique em **copiar** para copiar a url. Você precisará especificar esse url no próximo exercício. A URL neste exemplo é `https://eodts05snjmjz67.m.pipedream.net`.

![Cursor.ai + Commerce](./images/webhook1.png)

## 1.7.2.3 Cursor.ai

Abrir Cursor.ai. Clique em **Abrir projeto**.

![Cursor.ai + Commerce](./images/cursorai14.png)

Navegue até a pasta que você criou, a qual deve se chamar `--aepUserLdap---commerce`. Nessa pasta, selecione a pasta chamada `commerce-integration-starter-kit`. Clique em **Abrir**.

![Cursor.ai + Commerce](./images/cursorai15.png)

Você deverá ver isso. Antes de continuar, verifique se a pasta de nível superior que está aberta em Cursor.ai é `commerce-integration-starter-kit`.

![Cursor.ai + Commerce](./images/cursorai16.png)

`I would like to build an app that subscribes to order created events and sends them to a configurable URL with basic authentication`

## Próximas etapas

Voltar para [Ferramentas de Desenvolvedor Inteligente para o Adobe Commerce](./aiassisteddev.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}