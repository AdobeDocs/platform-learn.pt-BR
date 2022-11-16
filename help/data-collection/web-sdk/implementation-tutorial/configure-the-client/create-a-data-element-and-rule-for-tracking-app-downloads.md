---
title: Criar um elemento de dados e uma regra para rastrear downloads de aplicativos
description: Criar um elemento de dados e uma regra para rastrear downloads de aplicativos
feature: Web SDK
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: cb322540-e8ef-4226-b537-a67c7ca273f5
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 3%

---

# Criar um elemento de dados e uma regra para rastrear downloads de aplicativos

Como lembrete, ao rastrear quando um usuário clica no [!UICONTROL Baixar o aplicativo] , você foi enviado para a camada de dados da seguinte maneira:

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

Você usou o `eventInfo` , que informa à camada de dados para comunicar esses dados juntamente com o evento, mas para _not_ mantenha os dados dentro da camada de dados. Para um clique em um link, não é útil adicionar informações sobre o link clicado à camada de dados, pois não é aplicável a outros eventos que podem ocorrer posteriormente na página.

Para essa implementação, você enviará um evento de experiência para o Adobe Experience Platform contendo o resultado mesclado de (1) o estado calculado da camada de dados e (2) o conteúdo de `eventInfo`.

Para fazer isso, primeiro você precisará criar um elemento de dados que mescle essas duas partes de informações.

## Criar um elemento de dados

Para criar o elemento de dados apropriado, clique em [!UICONTROL Elementos de dados] no menu à esquerda. Em seguida, clique no botão [!UICONTROL Adicionar elemento de dados] link .

Para o nome do elemento de dados, insira `computedStateAndEventInfo`. Para o [!UICONTROL Extensão] , selecione [!UICONTROL Núcleo] se ainda não estiver selecionado. Para o [!UICONTROL Tipo de elemento de dados] , selecione [!UICONTROL Objetos Mesclados]. Esse elemento de dados permite mesclar profundamente vários objetos. O resultado mesclado é retornado pelo elemento de dados.

Para o primeiro objeto que deseja incluir na mesclagem, insira `%event.fullState%`. Quando usado em uma regra acionada por uma [!UICONTROL Dados enviados] evento de regra, isso faz referência ao estado calculado da Camada de dados do cliente do Adobe no momento em que a regra foi acionada.

Clique em [!UICONTROL Adicionar outro].

Para o segundo objeto, digite `%event.eventInfo%`. Quando usado em uma regra acionada por uma [!UICONTROL Dados enviados] evento de regra, isso faz referência à variável `eventInfo` parte que foi enviada para a Camada de dados do cliente do Adobe.

![elemento de dados computedStateAndEventInfo](../../../assets/implementation-strategy/computed-state-and-event-info-data-element.png)

O elemento de dados foi concluído. Salve o elemento de dados clicando no botão [!UICONTROL Salvar] botão.

## Criar uma regra

Para criar a regra para rastrear cliques no [!UICONTROL Baixar o aplicativo] link, primeiro clique [!UICONTROL Regras] no menu à esquerda.

Clique em [!UICONTROL Adicionar regra].

Para o nome da regra, insira _Link do aplicativo de download clicado_.

## Adicionar um evento

Clique no botão [!UICONTROL Adicionar] botão abaixo [!UICONTROL Eventos]. Agora você mostra estar na exibição de evento. Para o [!UICONTROL Extensão] , selecione [!UICONTROL Camada de dados do cliente Adobe]. Para o [!UICONTROL Tipo de evento] , selecione [!UICONTROL Dados enviados].

Porque você deseja que essa regra seja acionada somente quando a variável `downloadAppClicked` for enviado para a camada de dados, selecione a [!UICONTROL Evento específico] rádio debaixo de [!UICONTROL Ouça] e tipo _downloadAppClicked_ na [!UICONTROL Evento / Chave para se registrar]  campo de texto exibido.

![Evento de download do aplicativo clicado](../../../assets/implementation-strategy/download-app-clicked-event.png)

Clique em [!UICONTROL  Manter alterações].

## Adicionar uma ação

Agora que você está de volta à exibição de regra, clique no botão [!UICONTROL Adicionar] botão abaixo [!UICONTROL Ações]. Agora você deve estar na exibição de ação. Para o [!UICONTROL Extensão] , selecione [!UICONTROL Adobe Experience Platform Web SDK]. Para o [!UICONTROL Tipo de ação] , selecione [!UICONTROL Enviar evento].

No lado direito da tela, encontre a variável [!UICONTROL Tipo] e selecione `web.webinteraction.linkClicks`.

Para o [!UICONTROL Dados XDM] , clique no botão seletor de elemento de dados e selecione [!UICONTROL computedStateAndEventInfo]. Este é o elemento de dados que você acabou de criar.

Para esta regra (diferente das outras regras que você criou), você verificará o [!UICONTROL O documento será descarregado] caixa de seleção. Isso basicamente informa ao SDK que o usuário estará navegando para fora da página ao clicar no link. Isso é importante, pois permite que o SDK faça a solicitação de maneira que, mesmo que o usuário saia da página, a solicitação ainda continue sendo executada em segundo plano e alcance o servidor. Se essa caixa de seleção estiver desmarcada, a solicitação não será feita dessa maneira e, portanto, provavelmente será cancelada quando o documento atual for descarregado.

Você pode estar se perguntando: &quot;Isso parece legal. Por que essa opção nem sempre está ativada?&quot;

Bem, é um pouco complicado, mas ao usar esse recurso, o SDK usa um método de navegador chamado [`sendBeacon`](https://developer.mozilla.org/pt-BR/docs/Web/API/Navigator/sendBeacon) para enviar a solicitação. Ao enviar uma solicitação usando `sendBeacon`, o navegador não permite que o SDK (ou qualquer outra coisa) acesse quaisquer dados retornados do servidor. Se o SDK usasse esse recurso para cada solicitação, o SDK nunca poderia receber dados do servidor. Por isso, é importante verificar a variável [!UICONTROL O documento será descarregado] caixa de seleção somente quando o documento atual for descarregado, nesse caso, os dados de resposta poderão ser descartados de qualquer maneira.

![O documento descarregará a caixa de seleção](../../../assets/implementation-strategy/document-will-unload.png)

Salve a ação clicando no botão [!UICONTROL Manter alterações] botão.

## Salve a regra

Sua regra deve estar concluída.

![Baixar regra clicada no link do aplicativo](../../../assets/implementation-strategy/download-app-link-clicked-rule.png)

Salve a regra clicando em [!UICONTROL Salvar].
