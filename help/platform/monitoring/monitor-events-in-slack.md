---
title: Monitorar eventos no Slack
description: Saiba como receber notificações do Experience Platform no Slack integrando com um proxy de webhook do Adobe App Builder.
feature: Monitoring
role: Developer, Admin
level: Intermediate
duration: 519
last-substantial-update: 2026-02-24T00:00:00Z
jira: KT-20339
exl-id: 6d4a072c-9eef-4a38-9459-9e1cbd66bfb5
source-git-commit: 4ec7a800ef963f9b1257e2f246428abff32e9b94
workflow-type: tm+mt
source-wordcount: '1539'
ht-degree: 0%

---

# Monitorar eventos do Experience Platform no Slack

Saiba como receber notificações do Experience Platform no Slack integrando com um proxy de webhook do Adobe App Builder. Engenheiros de dados e administradores podem querer receber notificações proativas no Slack da Adobe Experience Platform para monitorar a integridade de suas implementações da plataforma. Este tutorial descreve as etapas de arquitetura e implementação para conectar o Adobe I/O Events ao Slack usando o Adobe App Builder.


>[!VIDEO](https://video.tv.adobe.com/v/3480200?captions=por_br&learn=on)

## Por que um proxy de webhook?

Não é possível conectar diretamente o Adobe I/O Events a um Webhook de entrada do Slack devido a uma incompatibilidade de protocolo no processo de verificação.

* **O desafio**: ao registrar um webhook no Adobe I/O Events, o Adobe envia uma solicitação de &quot;Desafio&quot; (um `GET` ou `POST`) para o seu ponto de extremidade. Seu endpoint deve processar com êxito esse desafio e retornar o valor específico para confirmar a propriedade.

* **Limitação**: os webhooks de entrada do Slack foram criados apenas para assimilar cargas JSON para mensagens. Eles não têm lógica para reconhecer ou responder ao handshake de desafio de verificação da Adobe.

* **A Solução**: implantar um proxy de webhook intermediário usando o Adobe App Builder. Esse proxy fica entre o Adobe e o Slack para:
   1. Intercepte a solicitação do Adobe e responda ao desafio de verificação.
   1. Formate o conteúdo em uma mensagem compatível com o Slack e encaminhe-a para o Slack.

* **Método de entrega**: Ações de Tempo de Execução.  As ações de tempo de execução vêm empacotadas com o Adobe App Builder. Ao usar uma Ação em tempo de execução (ação que não seja da Web) como o manipulador de eventos, o Adobe I/O Events lida automaticamente com a verificação de assinatura e respostas de desafio. As ações em tempo de execução são a abordagem recomendada, pois exigem menos código e fornecem segurança integrada.

## Visão geral da arquitetura

### O que é o Adobe Developer Console?

O Adobe Developer Console é o portal central para gerenciar projetos, APIs e credenciais da Adobe. É onde você cria seu projeto, configura a autenticação e registra seus webhooks.

### O que é o App Builder?

O Adobe App Builder é uma estrutura completa que permite que desenvolvedores corporativos criem aplicativos nativos em nuvem.

* **Provisionamento**: o App Builder não está habilitado por padrão; ele deve ser provisionado para sua organização como um recurso. Verifique se sua organização tem o direito **[!DNL App Builder]**.

* **Modelo de Projeto**: os projetos do App Builder são criados especificamente usando o modelo **[!UICONTROL App Builder]** no [!DNL Developer Console] ([!UICONTROL Projeto do Modelo] > [!UICONTROL App Builder]). O modelo configura automaticamente os espaços de trabalho e ambientes de tempo de execução necessários.

* **Guia de Introdução do App Builder**: consulte a documentação [para provisionar e criar seu primeiro projeto a partir do modelo](https://developer.adobe.com/app-builder/docs/get_started/app_builder_get_started/first-app){target=_blank}.

### O que é o Adobe I/O Runtime?

O Adobe I/O Runtime é a plataforma sem servidor que capacita o App Builder. Ele permite que os desenvolvedores implantem o código (Funções como um serviço) executado em resposta a solicitações HTTP sem gerenciar a infraestrutura do servidor.

Nesta implementação, usamos uma **Ação**. Uma ação é uma função sem estado (escrita em Node.js) executada no Adobe I/O Runtime. Nossa Ação serve como o endpoint HTTP público com o qual o Adobe I/O Events se comunica.

Para obter mais informações, consulte a [documentação do Adobe I/O Runtime](https://developer.adobe.com/runtime/){target=_blank}.

## Guia de implementação

### Pré-requisitos

Antes de iniciar, verifique se você tem o seguinte:

* **Acesso ao Adobe Developer Console**: você deve ter acesso a um Administrador do Sistema ou à [função de Desenvolvedor](../admin/add-developers.md) em uma organização que tenha o App Builder habilitado.

  >[!TIP]
  > Para verificar o provisionamento do App Builder, faça logon no [Adobe Developer Console](https://developer.adobe.com/console/){target=_blank}, verifique se você está na organização desejada, selecione **[!UICONTROL Criar projeto a partir do modelo]** e verifique se o modelo do App Builder está disponível. Se não estiver, consulte a seção de perguntas frequentes sobre o App Builder &quot;[Como obter o App Builder](https://developer.adobe.com/app-builder/docs/intro_and_overview/faq#how-to-get-app-builder){target=_blank}&quot;


* **Node.js &amp; npm**: este projeto requer Node.js, que inclui NPM (Gerenciador de Pacotes de Nós). O NPM é usado para instalar a CLI do Adobe e gerenciar dependências de projetos.

   * [Baixar Node.js (versão LTS recomendada)](https://nodejs.org/){target=_blank}
   * [Guia de Introdução](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm){target=_blank} - Um guia sobre como verificar sua instalação.

* **`aio CLI`**: Instalado via terminal: `npm install -g @adobe/aio-cli`
* **Configuração do Aplicativo Slack**: você precisa de um aplicativo Slack configurado em seu espaço de trabalho com um **Webhook de entrada** ativado.

   * [Criar um aplicativo Slack](https://api.slack.com/apps){target=_blank}
   * [Guia de Webhooks de Entrada do Slack](https://docs.slack.dev/messaging/sending-messages-using-incoming-webhooks/){target=_blank} - Siga este guia para criar seu aplicativo e gerar a URL do Webhook (começa com `https://hooks.slack.com/`...).

### Etapa 1: criar um projeto no Adobe Developer Console

Primeiro, crie um projeto com o modelo App Builder no Adobe Developer Console:

1. Fazer logon no [Adobe Developer Console](https://developer.adobe.com/console)
1. Selecione **[!UICONTROL Criar projeto a partir do modelo]**
1. Selecione o modelo do App Builder
1. Insira um Título de Projeto, por exemplo `Slack webhook integration`
1. Selecione **[!UICONTROL Salvar]**

### Inicializar o ambiente de tempo de execução

Execute os seguintes comandos no terminal para criar a estrutura do projeto:

#### Fazer logon em `aio`

```
aio login
```

#### Etapa 2: inicializar um novo projeto do App Builder

```
aio app init slack-webhook-proxy
```

1. Selecione sua organização e pressione **Enter**
1. Selecione o Projeto criado na etapa anterior (por exemplo, `Slack webhook integration`) e pressione **Enter**
1. Selecione a opção **[!UICONTROL Somente Modelos com Suporte em Minha Organização]**
1. Ignorar a seção de exemplo pressionando **Enter**
1. Quando solicitado, verifique se os seguintes componentes estão selecionados (o círculo deve ser preenchido) e pressione **Enter**:
   1. **[!UICONTROL Ações: implantar ações de Tempo de Execução]**
   1. **[!UICONTROL Eventos: Publicar no Adobe I/O Events]**
   1. **[!UICONTROL Web Assets: implantar em ativos estáticos hospedados]**
1. Com as setas para cima e para baixo, navegue pela lista de entrada e escolha **[!UICONTROL Adobe Experience Platform: Perfil do Cliente em Tempo Real]** e pressione **Enter**
1. As ações **[!UICONTROL genéricas]** são geradas automaticamente
1. Escolha o **[!UICONTROL Pure HTML/JS]** para a interface e pressione **Enter**
1. Mantenha **[!UICONTROL genérico]** como a ação de exemplo para mostrar como acessar um nome de API externa e pressione **Enter**
1. Mantenha o **[!UICONTROL publish-events]** como o nome de ação de exemplo para criar mensagens no formato de eventos na nuvem e pressione **Enter**

A inicialização do aplicativo deve ser concluída.

#### Navegue até o diretório do projeto

```
cd slack-webhook-proxy
```

#### Adicionar a ação da Web

```
aio app add action
```

1. Escolha **[!UICONTROL Somente Modelos Com Suporte em Minha Organização]** e pressione **Enter**
2. Veja a ação **[!UICONTROL publish-events]** na tabela apresentada; pressione **Espaço** para selecionar a ação. Se o círculo ao lado do nome for preenchido conforme mostrado no tutorial em vídeo, pressione **Enter**
3. Nomear a ação `webhook-proxy`

### Etapa 3: atualizar o código de ação de proxy

Em um editor de texto ou IDE, crie/modifique o arquivo `actions/webhook-proxy/index.js` com o seguinte código. Essa implementação encaminha eventos para o Slack. A verificação de assinatura e o tratamento de desafio são automáticos ao usar o registro de Ação em tempo de execução.

```javascript
const fetch = require("node-fetch");
const { Core } = require("@adobe/aio-sdk");
 
/**
 * Adobe I/O Events to Slack Runtime Proxy
 *
 * Receives events from Adobe I/O Events and forwards them to Slack.
 * Signature verification and challenge handling are automatic when
 * using Runtime Action registration (non-web action).
 */
async function main(params) {
  const logger = Core.Logger("webhook-proxy", { level: params.LOG_LEVEL || "info" });
 
  try {
    logger.info(`Event received: ${JSON.stringify(params)}`);
 
    // Forward to Slack
    return forwardToSlack(params, params.SLACK_WEBHOOK_URL, logger);
 
  } catch (error) {
    logger.error(`Error: ${error.message}`);
    return { statusCode: 500, body: { error: "Internal server error" } };
  }
}
 
/**
 * Forwards the event payload to Slack
 */
async function forwardToSlack(payload, webhookUrl, logger) {
  if (!webhookUrl) {
    logger.error("SLACK_WEBHOOK_URL not configured");
    return { statusCode: 500, body: { error: "Server configuration error" } };
  }
 
  // Extract Adobe headers passed to runtime action
  const headers = {
    "x-adobe-event-code": payload["x-adobe-event-code"],
    "x-adobe-event-id": payload["x-adobe-event-id"],
    "x-adobe-provider": payload["x-adobe-provider"]
  };
 
  const slackMessage = buildSlackMessage(payload, headers);
 
  const response = await fetch(webhookUrl, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(slackMessage)
  });
 
  if (!response.ok) {
    const errorText = await response.text();
    logger.error(`Slack API error: ${response.status} - ${errorText}`);
    return { statusCode: response.status, body: { error: errorText } };
  }
 
  logger.info("Event forwarded to Slack");
  return { statusCode: 200, body: { success: true } };
}
 
/**
 * Builds a Slack Block Kit message from the event payload
 */
function buildSlackMessage(payload, headers) {
  // Adobe passes event code as x-adobe-event-code header (available in params for runtime actions)
  const eventType = headers["x-adobe-event-code"] ||
                    payload["x-adobe-event-code"] ||
                    payload.event_code ||
                    payload.type ||
                    payload.event_type ||
                    "Adobe Event";
  const eventId = headers["x-adobe-event-id"] || payload["x-adobe-event-id"] || payload.event_id || payload.id || "N/A";
  const eventData = payload.data || payload.event || payload;
 
  return {
    blocks: [
      {
        type: "header",
        text: { type: "plain_text", text: `Event: ${eventType}`, emoji: true }
      },
      {
        type: "section",
        fields: formatDataFields(eventData)
      },
      { type: "divider" },
      {
        type: "context",
        elements: [{
          type: "mrkdwn",
          text: `*Event ID:* ${eventId}  |  *Time:* ${new Date().toISOString()}`
        }]
      }
    ]
  };
}
 
/**
 * Formats event data as Slack mrkdwn fields
 */
function formatDataFields(data, maxFields = 10) {
  if (typeof data !== "object" || data === null) {
    return [{ type: "mrkdwn", text: `*Payload:*\n${String(data)}` }];
  }
 
  const entries = Object.entries(data);
  if (entries.length === 0) {
    return [{ type: "mrkdwn", text: "_No data provided_" }];
  }
 
  return entries.slice(0, maxFields).map(([key, value]) => ({
    type: "mrkdwn",
    text: `*${key}:*\n${typeof value === "object" ? `\`\`\`${JSON.stringify(value)}\`\`\`` : value}`
  }));
}
 
exports.main = main;
```

### Etapa 4: configurar a ação

A configuração da ação em `app.config.yaml` é crítica. Usar web: não para criar uma ação que não seja da Web que possa ser registrada como uma Ação em tempo de execução no Developer Console.

```yaml
application:
  runtimeManifest:
    packages:
      slack-webhook-proxy:
        license: Apache-2.0
        actions:
          webhook-proxy:
            function: actions/webhook-proxy/index.js
            web: no
            runtime: nodejs:22
            inputs:
              LOG_LEVEL: info
              SLACK_WEBHOOK_URL: $SLACK_WEBHOOK_URL
            annotations:
              require-adobe-auth: false
              final: true
```

#### Por que `web: no?`

Ao usar uma ação que não seja da Web e registrá-la por meio da opção &quot;Ação em tempo de execução&quot; no Developer Console, o Adobe I/O Events automaticamente:

* Lida com verificação de desafio (tanto `GET` quanto `POST`)
* Verifica assinaturas digitais antes de invocar sua ação
* Encadeia uma ação de validador de assinatura na frente da sua ação

Isso significa que seu código só precisa lidar com a lógica de negócios (encaminhamento para o Slack).

### Etapa 4: atualizar as variáveis de ambiente

Para gerenciar credenciais com segurança, usamos variáveis de ambiente. Crie/modifique o arquivo `.env` na raiz do seu projeto para adicionar a URL do webhook do Slack. Certifique-se de mostrar os arquivos ocultos no sistema se você não visualizar o arquivo `.env`:

```
# ... other .env file content ...
 
SLACK_WEBHOOK_URL=https://hooks.slack.com/services/YOUR/WEBHOOK/URL
```

### Etapa 5: implantar a ação

Depois que as variáveis de ambiente forem definidas, implante a ação. Certifique-se de estar na raiz do seu projeto, ou seja, `slack-webhook-proxy`, ao executar este comando no terminal.

```
aio app deploy
```

Sua ação é implantada no Adobe I/O Runtime e está disponível na Developer Console para registro.

### Etapa 6: registrar a ação no Adobe Developer Console

Agora que sua ação foi implantada, registre-a como destino para Eventos da Adobe.

1. Navegue até o [Adobe Developer Console](https://developer.adobe.com/console){target=_blank} e abra o projeto do App Builder.
1. Escolha seu **[!UICONTROL Workspace]**
1. Selecione **[!UICONTROL Adicionar Serviço]** e **[!UICONTROL Evento]**.
1. Selecione **[!UICONTROL Adobe Experience Platform]** como o produto.
1. Selecione **[!UICONTROL Notificações da plataforma]** como o tipo de evento.
1. Selecione os eventos específicos (ou todos) que você deseja ser notificado no Slack e selecione **[!UICONTROL Próximo]**.
1. Selecione ou [crie sua credencial do OAuth](https://experienceleague.adobe.com/pt-br/docs/platform-learn/tutorials/api/platform-api-authentication){target=_blank}.
1. Configurar **[!UICONTROL detalhes do registro de eventos]**:
   1. **[!UICONTROL Nome do Registro]**: dê um nome descritivo a seu registro.
   1. **[!UICONTROL Descrição do registro]**: verifique se isso é explícito para que outros colaboradores possam saber o que ele faz.
   1. Selecionar **[!UICONTROL Próximo]**
   1. **[!UICONTROL Método de Entrega]**: Selecionar **[!UICONTROL Ação em Tempo de Execução]** (não &quot;Webhook&quot;).
   1. **[!UICONTROL Ação em tempo de execução]**: escolha `webhook-proxy` na lista suspensa (atualize a página caso não a veja).
1. Selecione **[!UICONTROL Salvar Eventos Configurados]**.


### Etapa 7: validar com um evento de amostra

Você pode testar todo o fluxo de ponta a ponta clicando no ícone &#39;Enviar evento de amostra&#39; ao lado de qualquer evento configurado.

O evento de amostra é enviado no canal que você configurou ao criar seu aplicativo Slack e o webhook; Você deve ver algo semelhante ao seguinte:

![Exemplo de um evento de monitoramento no Slack](../assets/slack-monitor.png)

Parabéns, você integrou o Slack com êxito aos eventos do Experience Platform!

### Problemas comuns

Estes são alguns problemas que você pode ter ao configurar o proxy e algumas maneiras potenciais de resolvê-los.

* **Não é possível ver organizações IMS**: se você não vir sua lista de organizações IMS ao executar `aio app init`, tente o seguinte. Execute o `aio logout` no Terminal, faça logoff do Experience Cloud no navegador da Web padrão e execute o `aio login` novamente.
* **Ação não exibida na lista suspensa**: verifique se `web: no` está definido em `app.config.yaml`. Somente ações que não sejam da Web aparecem na lista suspensa Ação em tempo de execução. Atualize a página do Developer Console após a implantação.
* **Falha na verificação da assinatura**: se você vir isso nos logs de ativação, significa que o validador interno do Adobe rejeitou a solicitação. Isso não deve acontecer com eventos legítimos do Adobe. Verifique se o registro de evento está configurado corretamente.
* **O Slack não está recebendo mensagens**: verifique se `SLACK_WEBHOOK_URL` está definido corretamente no arquivo `.env` e se o Webhook de Entrada está habilitado no aplicativo Slack.
* **Tempo limite da ação**: as ações de tempo de execução têm um tempo limite de 60 segundos. Se a ação demorar mais, considere usar a abordagem de registro em diário.
