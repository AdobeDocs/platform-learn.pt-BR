---
title: Use o cursor para desenvolver seu projeto
description: Use o cursor para desenvolver seu projeto
kt: 5342
doc-type: tutorial
exl-id: c73498b6-5e08-41b5-81a9-c0a76a6e2792
source-git-commit: 25901342e8d9c46b0edce3b2092b9f1d66ba5849
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 0%

---

# 1.7.2 Use o cursor para desenvolver o projeto

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

Em seguida, é necessário configurar as ferramentas de extensibilidade do Commerce para o Cursor. Digite o seguinte comando e execute-o.

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

Ao instalar as ferramentas de extensibilidade do Commerce para o Cursor, agora há um servidor MCP disponível como parte de seu ambiente de Cursor. Nos próximos exercícios, você usará esse servidor MCP para ajudá-lo a desenvolver e implantar o projeto do construtor de aplicativos.

## 1.7.2.2 Configurar seu webhook

Para este exercício, você precisará de um webhook que precisa ser configurado para que, quando um pedido for criado, o evento de pedido possa ser transmitido para esse webhook. Neste exercício, você usará um terminal de exemplo usando [https://pipedream.com/requestbin](https://pipedream.com/requestbin).

Vá para [https://pipedream.com/requestbin](https://pipedream.com/requestbin), crie uma conta e um espaço de trabalho. Depois que o espaço de trabalho for criado, você verá algo semelhante a isso.

Clique em **copiar** para copiar a url. Você precisará especificar esse url no próximo exercício. A URL neste exemplo é `https://eodts05snjmjz67.m.pipedream.net`.

![Cursor + Commerce](./images/webhook1.png)

## 1.7.2.3 Criar aplicativo com cursor

Abrir cursor. Clique em **Abrir projeto**.

![Cursor + Commerce](./images/cursorai14.png)

Navegue até a pasta que você criou, a qual deve se chamar `--aepUserLdap---commerce`. Nessa pasta, selecione a pasta chamada `commerce-integration-starter-kit`. Clique em **Abrir**.

![Cursor + Commerce](./images/cursorai15.png)

Você deverá ver isso. Antes de continuar, verifique se a pasta de nível superior aberta no Cursor é `commerce-integration-starter-kit`.

![Cursor + Commerce](./images/cursorai16.png)

Use o atalho de teclado `Cmd + Shift + J` para abrir as configurações do Cursor. Você deverá ver isso. Ir para **Ferramentas&amp; MCP**.

![Cursor + Commerce](./images/cursorai17.png)

Habilite o servidor MCP **extensibilidade-comércio**. Depois de concluído, clique em **X** para fechar a janela.

![Cursor + Commerce](./images/cursorai18.png)

Copie o prompt a seguir e cole-o no Cursor. Clique no botão **enviar**.

`I would like to build an app that subscribes to order created events and sends them to a configurable URL with basic authentication`

![Cursor + Commerce](./images/cursorai19.png)

O cursor iniciará o raciocínio e a execução. O cursor solicitará a confirmação algumas vezes. Quando isso acontecer, clique em **Executar**. Isso pode acontecer de 5 a 10 vezes, dependendo do raciocínio e das configurações.

![Cursor + Commerce](./images/cursorai20.png)

Após alguns minutos, vocês verão algo assim.

![Cursor + Commerce](./images/cursorai21.png)

A próxima etapa, conforme indicado pelo Cursor, é criar um arquivo com o nome `.env` e fornecer as variáveis necessárias.

## 1.7.2.4 Crie seu arquivo .env

Selecione o arquivo **env.dist**. Digite o comando `Cmd + C` e depois o comando `Cmd + V`.

![Cursor + Commerce](./images/cursorai22.png)

Renomeie o arquivo recém-criado para `.env`.

![Cursor + Commerce](./images/cursorai23.png)

Em seguida, você precisa fornecer os valores para todas as variáveis no arquivo **.env**.

![Cursor + Commerce](./images/cursorai24.png)

Aqui é onde você pode encontrar todas as informações necessárias.

### Endpoints do Commerce

Você pode encontrar essas variáveis acessando [https://experience.adobe.com](https://experience.adobe.com). Clique em **Commerce**.

![Cursor + Commerce](./images/cursorai25.png)

Você deverá ver isso. Clique no ícone **informações** ao lado do ambiente ACCS, que deve ser nomeado como `--aepUserLdap-- - ACCS`. Copie os valores dos pontos de extremidade REST e GraphQL.

Neste exemplo, esses são os valores a serem copiados. Cole-as ao lado das variáveis abaixo no arquivo **.env** nas linhas 6 e 7.


- **COMMERCE_BASE_URL** = https://na1-sandbox.api.commerce.adobe.com/Lkp3U7tvTBNAmpFvwnZJ4B/
- **COMMERCE_GRAPHQL_ENDPOINT** = https://na1-sandbox.api.commerce.adobe.com/Lkp3U7tvTBNAmpFvwnZJ4B/graphql

![Cursor + Commerce](./images/cursorai26.png)

Isso deve ser inserido no arquivo **.env**.

![Cursor + Commerce](./images/cursorai26a.png)

### Variáveis de projeto do Adobe I/O

Você pode encontrar essas variáveis acessando [https://developer.adobe.com/console](https://developer.adobe.com/console). Vá para **Projetos** e clique para abrir o projeto do Adobe I/O que você criou no exercício anterior, que deve ser nomeado como `--aepUserLdap-- Commerce Events`.

![Cursor + Commerce](./images/cursorai27.png)

Ir para **Produção**.

![Cursor + Commerce](./images/cursorai28.png)

Vá para **Servidor a Servidor do OAuth**. Você deverá ver isso.

![Cursor + Commerce](./images/cursorai29.png)

Copie os valores dos campos **ID do Cliente**, **Segredo do Cliente**, **ID da Conta Técnica**, **Email da Conta Técnica** e **ID da Organização** e cole-os ao lado das variáveis abaixo no arquivo **.env**, nas linhas 13 a 17.

- **OAUTH_CLIENT_ID**= **ID do Cliente**
- **OAUTH_CLIENT_SECRET**= **Segredo do Cliente**
- **OAUTH_TECHNICAL_ACCOUNT_ID**= **ID da Conta Técnica**
- **OAUTH_TECHNICAL_ACCOUNT_EMAIL**= **Email de Conta Técnica**
- **OAUTH_ORG_ID**= **ID da Organização**

Isso deve ser inserido no arquivo **.env**.

![Cursor + Commerce](./images/cursorai29a.png)

### COMMERCE_ADOBE_IO_EVENTS_MERCHANT_ID

Para o campo **COMMERCE_ADOBE_IO_EVENTS_MERCHANT_ID=**, insira o valor `--aepUserLdap--_commerce_events` na linha 34 do arquivo **.env**.

Isso deve ser inserido no arquivo **.env**.

![Cursor + Commerce](./images/cursorai30.png)

### Configurações do Workspace

Para recuperar essas variáveis, volte para o projeto do Adobe I/O e clique em **Visão geral do Workspace**.

Depois de acessar a **visão geral do Workspace**, examine a URL, que deve ter esta aparência: **https://developer.adobe.com/console/projects/133309/4566206088345586770/workspaces/4566206088345619105/details**.

O primeiro número deste exemplo, 133309, é o valor a ser usado para o campo **IO_CONSUMER_ID**.
O segundo número neste exemplo, 4566206088345586770, é o valor a ser usado para o campo **IO_PROJECT_ID**.
O terceiro número deste exemplo, 4566206088345619105, é o valor a ser usado para o campo **IO_WORKSPACE_ID**.

![Cursor + Commerce](./images/cursorai31.png)

- **IO_CONSUMER_ID**= 133309
- **IO_PROJECT_ID**= 4566206088345586770
- **IO_WORKSPACE_ID**= 4566206088345619105

Copie esses valores e cole-os ao lado das variáveis abaixo no arquivo **.env** nas linhas 42 a 44.

![Cursor + Commerce](./images/cursorai32.png)

### EVENT_PREFIX

Para o campo **EVENT_PREFIX =**, insira o valor `--aepUserLdap--_` na linha 47 do arquivo **.env**.

Isso deve ser inserido no arquivo **.env**.

![Cursor + Commerce](./images/cursorai33.png)

### Webhook

Para o campo **ORDER_WEBHOOK_URL**, você deve colar a URL do webhook criado anteriormente neste exercício, que deve ter esta aparência: `https://eodts05snjmjz67.m.pipedream.net`.

Isso deve ser inserido no arquivo **.env**.

![Cursor + Commerce](./images/cursorai34.png)

### Credenciais do App Builder

Você deve atualizar as seguintes variáveis no arquivo **.env** nas linhas 54-55:

- **NAMESPACE_DE_TEMPO_DE_EXECUÇÃO_AIO**=
- **AUTENTICAÇÃO_DE_TEMPO_DE_EXECUÇÃO_AIO**=

Você pode recuperar os valores dessas variáveis voltando para o projeto do Adobe I/O. Vá para **visão geral do Workspace** e clique em **Baixar tudo**.

![Cursor + Commerce](./images/cursorai35.png)

Um arquivo como este será baixado. Abra esse arquivo usando um editor de texto.

![Cursor + Commerce](./images/cursorai36.png)

Role para a direita até ver **tempo de execução**. Você deverá ver o campo **nome**, que contém o valor de **AIO_RUNTIME_NAMESPACE**.

![Cursor + Commerce](./images/cursorai37.png)

Role para a direita até ver **auth**, que contém o valor de **AIO_RUNTIME_AUTH**.

![Cursor + Commerce](./images/cursorai38.png)

Cole ambos os valores no arquivo **.env** nas linhas 54-55, você deve ter isso.

![Cursor + Commerce](./images/cursorai39.png)

O arquivo **.env** está completamente configurado.

## 1.7.2.5 workspace.json

Na etapa anterior, você baixou um arquivo como este do projeto do Adobe I/O.

![Cursor + Commerce](./images/cursorai36.png)

Renomeie esse arquivo e use o nome `workspace.json`.

![Cursor + Commerce](./images/cursorai40.png)

Copie o arquivo no diretório **scripts**>**integração**>**configuração**.

![Cursor + Commerce](./images/cursorai41.png)

## 1.7.2.6 Login do Adobe I/O

Volte para a janela do terminal que você usou antes. Digite o comando `aio login`.

![Cursor + Commerce](./images/cursorai44.png)

Você deve ver isso depois de fazer logon por meio do navegador.

![Cursor + Commerce](./images/cursorai45.png)

## 1.7.2.7 Pronto para implantar

Copie o prompt a seguir e cole-o no Cursor. Clique no botão **enviar**.

`Please deploy this code to Adobe I/O`

![Cursor + Commerce](./images/cursorai42.png)

Clique em **Executar** para permitir a ação. O cursor poderá solicitar várias vezes a confirmação de uma ação.

![Cursor + Commerce](./images/cursorai43.png)

A implantação será concluída após alguns minutos.

![Cursor + Commerce](./images/cursorai46.png)

Copie o prompt a seguir e cole-o no Cursor. Clique no botão **enviar**.

`run the onboarding to commerce`

![Cursor + Commerce](./images/cursorai50.png)

Após alguns minutos, vocês devem ver isso.

![Cursor + Commerce](./images/cursorai51.png)

Copie o prompt a seguir e cole-o no Cursor. Clique no botão **enviar**.

`subscribe to commerce events`

![Cursor + Commerce](./images/cursorai47.png)

Após alguns minutos, vocês devem ver isso.

![Cursor + Commerce](./images/cursorai49.png)

## 1.7.2.8 Verificar configuração no Adobe Commerce as a Cloud Service

Ir para [https://experience.adobe.com](https://experience.adobe.com). Clique em **Commerce**.

![Cursor + Commerce](./images/cursorai60.png)

Clique no ambiente Adobe Commerce as a Cloud Service para abri-lo e fazer logon.

![Cursor + Commerce](./images/cursorai61.png)

Vá para **Sistema** e depois para **Assinaturas de Eventos**.

![Cursor + Commerce](./images/cursorai62.png)

Você deverá ver essa lista de assinaturas de evento.

![Cursor + Commerce](./images/cursorai63.png)

Vá para **Lojas** e depois para **Configuração**.

![Cursor + Commerce](./images/cursorai64.png)

Vá para **Adobe Services** e selecione **Adobe I/O Events**. Você deverá ver que o campo **Configuração do Adobe I/O Workspace** tem um valor de alguns asteriscos e o campo **ID do Comerciante** também deve ter um valor como `--aepUserLdap--_commerce_events`.

![Cursor + Commerce](./images/cursorai65.png)

Com essa configuração implementada, agora você pode testar sua configuração.

## 1.7.2.9 Testar seu cenário

Abra o site.

![Cursor + Commerce](./images/cursorai101.png)

Vá para **Inspeções** e clique em qualquer produto.

![Cursor + Commerce](./images/cursorai102.png)

Configure o produto e clique em **Adicionar ao carrinho**.

![Cursor + Commerce](./images/cursorai103.png)

Clique no ícone **Carrinho** e selecione **Check-out**.

![Cursor + Commerce](./images/cursorai104.png)

Preencha seus detalhes e clique em **Fazer pedido**.

![Cursor + Commerce](./images/cursorai105.png)

Você deverá ver uma confirmação do pedido.

![Cursor + Commerce](./images/cursorai106.png)

Alterne para o aplicativo de webhook. Agora você deve ver um evento de entrada para o pedido que acabou de ser confirmado.

![Cursor + Commerce](./images/cursorai107.png)

## Depuração do Adobe I/O 1.7.2.10

Retorne ao projeto do Adobe I/O. Vá para **visão geral do Workspace**. Vocês devem ver algo semelhante a isso. Role para baixo um pouco.

![Cursor + Commerce](./images/cursorai108.png)

Clique para abrir a **Sincronização de Pedidos da Commerce**.

![Cursor + Commerce](./images/cursorai109.png)

Vá para **Rastreamento de Depuração**. Você pode encontrar os eventos de entrada mais recentes lá, juntamente com sua carga útil. Isso é útil para entender quais eventos foram processados e se foram processados com êxito.

![Cursor + Commerce](./images/cursorai110.png)

## Próximas etapas

Voltar para [Ferramentas de Desenvolvedor Inteligente para o Adobe Commerce](./aiassisteddev.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
