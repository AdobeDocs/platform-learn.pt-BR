---
title: Criar um elemento de dados e uma regra para rastrear downloads de aplicativos
description: Criar um elemento de dados e uma regra para rastrear downloads de aplicativos
feature: Web SDK
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: cb322540-e8ef-4226-b537-a67c7ca273f5
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 3%

---

# Criar um elemento de dados e uma regra para rastrear downloads de aplicativos

Como lembrete, ao rastrear quando um usuário clica na variável [!UICONTROL Baixar o aplicativo] , você será encaminhado para a camada de dados da seguinte maneira:

```js
window.adobeDataLayer.push({
  "event": "downloadAppClicked",
  "eventInfo": {
    "web": {
      "webInteraction": {
        "URL": "https://example.com/download",
        "name": "App Download",
        "type": "download"
      }
    }
  }
});
```

Você usou o `eventInfo` chave, que informa à camada de dados para comunicar esses dados junto com o evento, mas para _não_ reter os dados na camada de dados. Para um clique em links, não é útil adicionar informações sobre o link clicado à camada de dados, pois ele não se aplica a outros eventos que podem ocorrer posteriormente na página.

Para essa implementação, você enviará um evento de experiência para o Adobe Experience Platform contendo o resultado mesclado de (1) o estado calculado da camada de dados e (2) o conteúdo de `eventInfo`.

Para fazer isso, primeiro será necessário criar um elemento de dados que mescle essas duas partes de informações.

## Criar um elemento de dados

Para criar o elemento de dados apropriado, clique em [!UICONTROL Elementos de dados] no menu à esquerda. Clique em [!UICONTROL Adicionar elemento de dados] link.

Para o nome do elemento de dados, insira `computedStateAndEventInfo`. Para o [!UICONTROL Extensão] selecione [!UICONTROL Núcleo] se ainda não estiver selecionada. Para o [!UICONTROL Tipo de elemento de dados] selecione [!UICONTROL Objetos Mesclados]. Esse elemento de dados permite mesclar vários objetos profundamente. O resultado combinado é retornado pelo elemento de dados.

Para o primeiro objeto que você deseja incluir na mesclagem, insira `%event.fullState%`. Quando usado dentro de uma regra acionada por um [!UICONTROL Dados enviados] evento de regra, faz referência ao estado calculado da Camada de dados do cliente Adobe no momento em que a regra foi acionada.

Clique em [!UICONTROL Adicionar outro].

Para o segundo objeto, insira `%event.eventInfo%`. Quando usado dentro de uma regra acionada por um [!UICONTROL Dados enviados] evento da regra, faz referência ao `eventInfo` parte que foi enviada para a Camada de Dados de Clientes Adobe.

![elemento de dados computedStateAndEventInfo](../../../assets/implementation-strategy/computed-state-and-event-info-data-element.png)

O elemento de dados está concluído. Salve o elemento de dados clicando no ícone [!UICONTROL Salvar] botão.

## Criar uma regra

Para criar a regra de rastreamento de cliques na [!UICONTROL Baixar o aplicativo] primeiro clique em [!UICONTROL Regras] no menu à esquerda.

Clique em [!UICONTROL Adicionar regra].

Para o nome da regra, informe _Link para baixar aplicativo clicado_.

## Adicionar um evento

Clique em [!UICONTROL Adicionar] botão em [!UICONTROL Eventos]. Agora, você deve estar na exibição de evento. Para o [!UICONTROL Extensão] selecione [!UICONTROL Camada de dados de clientes Adobe]. Para o [!UICONTROL Tipo de evento] selecione [!UICONTROL Dados enviados].

Porque você deseja que essa regra seja acionada somente quando a variável `downloadAppClicked` for enviado para a camada de dados, selecione a variável [!UICONTROL Evento Específico] rádio em [!UICONTROL Ouvir] e tipo _downloadAppClicked_ no [!UICONTROL Evento / Chave para se inscrever]  campo de texto exibido.

![Baixar evento clicado no aplicativo](../../../assets/implementation-strategy/download-app-clicked-event.png)

Clique em [!UICONTROL  Manter alterações].

## Adicionar uma ação

Agora que você voltou à exibição de regra, clique no link [!UICONTROL Adicionar] botão em [!UICONTROL Ações]. Agora você deve estar na exibição de ação. Para o [!UICONTROL Extensão] selecione [!UICONTROL Adobe Experience Platform Web SDK]. Para o [!UICONTROL Tipo de ação] selecione [!UICONTROL Enviar evento].

No lado direito da tela, localize a variável [!UICONTROL Tipo] e selecione `web.webinteraction.linkClicks`.

Para o [!UICONTROL Dados XDM] , clique no botão seletor de elemento de dados e selecione [!UICONTROL computedStateAndEventInfo]. Este é o elemento de dados que você acabou de criar.

Para essa regra (diferente das outras regras criadas), você verificará a [!UICONTROL O documento será descarregado] caixa de seleção Basicamente, isso informa ao SDK que o usuário sairá da página ao clicar no link. Isso é importante porque permite que o SDK faça a solicitação de maneira que, mesmo que o usuário saia da página, a solicitação ainda continuará sendo executada em segundo plano e chegará ao servidor. Se essa caixa de seleção estiver desmarcada, a solicitação não será feita dessa maneira e, portanto, provavelmente será cancelada quando o documento atual for descarregado.

Você pode estar se perguntando: &quot;Isso soa bem. Por que essa opção não é sempre ativada, então?&quot;

Bem, é um pouco complicado, mas ao usar esse recurso, o SDK usa um método de navegador chamado [`sendBeacon`](https://developer.mozilla.org/pt-BR/docs/Web/API/Navigator/sendBeacon) para enviar a solicitação. Ao enviar uma solicitação usando `sendBeacon`, o navegador não permite que o SDK (ou qualquer outra coisa) acesse os dados retornados do servidor. Se o SDK usasse esse recurso para cada solicitação, ele nunca poderia receber dados do servidor. Por isso, é importante verificar a [!UICONTROL O documento será descarregado] marque a caixa de seleção somente quando o documento atual for descarregado, nesse caso, os dados de resposta poderão ser descartados mesmo assim.

![O documento descarregará a caixa de seleção](../../../assets/implementation-strategy/document-will-unload.png)

Salve a ação clicando no ícone [!UICONTROL Manter alterações] botão.

## Salve a regra

Sua regra agora deve estar concluída.

![Regra de link de download de aplicativo clicado](../../../assets/implementation-strategy/download-app-link-clicked-rule.png)

Salve a regra clicando em [!UICONTROL Salvar].
