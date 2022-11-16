---
title: Como usar a camada de dados do cliente do Adobe
description: Como usar a camada de dados do cliente do Adobe
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 33a5db8c-e49b-4073-b4d7-4abe19537fcb
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---

# Como usar a camada de dados do cliente do Adobe

Em [O que é uma camada de dados?](whats-a-data-layer.md), você aprendeu que há duas partes a serem consideradas ao discutir camadas de dados: o contêiner e o conteúdo. A Camada de dados do cliente do Adobe é o contêiner. Não importa como você [estruturar seus dados](../structuring-your-data.md) ou quais informações você escolhe colocar em seus dados. Os dados podem ser estruturados como [XDM](../structuring-your-data.md#xdm), como mostram os exemplos abaixo, ou você pode criar sua própria estrutura totalmente.

Idealmente, a equipe de engenharia da empresa é responsável por enviar os dados necessários para a camada de dados por meio do código na página. A equipe de marketing recupera dados da camada de dados, preferencialmente usando Tags do Adobe Experience Platform.

## Envio de dados para a camada de dados

A Camada de dados do cliente do Adobe é uma matriz JavaScript. Ao criar a Camada de dados do cliente do Adobe, ela começa vazia:

```js
window.adobeDataLayer = window.adobeDataLayer || [];
```

Para colocar dados na camada de dados, chame a função `push` método na matriz da camada de dados:

```js
window.adobeDataLayer.push({
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile"
  }
});
```

Você pode enviar dados adicionais para a camada de dados a qualquer momento, chamando `push` novamente.

```js
window.adobeDataLayer.push({
  "claims": {
    "status": "approved",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
});
```

## Como entender os dados enviados por push

Se você implementou as duas `push` , você acabaria com duas entradas na matriz da camada de dados. A camada de dados não é particularmente útil nesse estado. Normalmente, você deseja acessar o estado mesclado da camada de dados ou, em outras palavras, um único objeto que é o resultado combinado de todos os dados que você enviou para a camada de dados. Posteriormente, no tutorial, aprenderemos a acessar esse estado mesclado. Por enquanto, é suficiente entender que o estado calculado da camada de dados após as duas `push` As chamadas seriam as seguintes:

```json
{
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile",
    "status": "approved",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
}
```

## Remoção de dados

Às vezes, é necessário remover partes de dados da camada de dados. Isso é particularmente comum em aplicativos de página única quando o usuário navega de uma exibição para a próxima. Por exemplo, se o usuário navega de uma visualização de produto para uma visualização de contato, pode fazer sentido limpar quaisquer dados do produto na camada de dados, pois não é mais pertinente à exibição ativa.

Você pode remover um pedaço de dados, enviando um valor de `undefined` para a chave que deseja remover. Com base em nossos exemplos anteriores, se você desejar remover `status` na camada de dados, seu código seria o seguinte:

```js
window.adobeDataLayer.push({
  "claims": {
    "status": undefined
  }
});
```

O estado calculado da camada de dados não incluiria mais `status`:

```json
{
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
}
```

## Envio de eventos para a camada de dados

A Camada de dados do cliente do Adobe é usada não apenas para armazenar dados, mas também para comunicar quais eventos estão ocorrendo na página. Na verdade, você normalmente envia dados para a camada de dados _como resultado_ de um evento que ocorre na página. Esses eventos incluem (1) eventos de interação, como abrir um chat ou digitar um termo de pesquisa em uma barra de pesquisa ou (2) eventos de não interação, como impressão de um anúncio ou a conclusão de cálculos de desempenho de uma página da Web.

Para comunicar que um evento ocorreu na página, inclua um `event` no objeto que você envia para a camada de dados. Por exemplo, você pode comunicar que um usuário inseriu uma consulta de pesquisa em um campo de pesquisa.

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered"
});
```

Posteriormente, você aprenderá a acionar regras nas Tags do Adobe Experience Platform quando um evento específico for enviado para a camada de dados. Observe também que a variável `event` chave é _not_ incluído no estado calculado. Ele recebe um tratamento especial pela camada de dados.

## Envio de eventos e dados para a camada de dados

Notificar ouvintes de que o usuário inseriu uma consulta de pesquisa é útil, mas e se você desejar fornecer informações adicionais sobre o evento? Por exemplo, talvez você queira incluir a consulta de pesquisa do usuário. É possível fornecer esses dados de uma das duas formas a seguir:

1. Forneça os dados para que **é mantido** na camada de dados como parte do estado calculado da camada de dados.
2. Forneça os dados para que **não é retido** na camada de dados como parte do estado calculado da camada de dados.

Se você deseja manter os dados na camada de dados, normalmente depende de se você planeja fazer referência a esses dados durante toda a duração em que o usuário está na página. Caso contrário, a retenção dos dados dentro da camada de dados pode resultar em uma camada de dados desorganizada.

Este é um exemplo de envio de um evento com dados adicionais que **é mantido** na camada de dados:

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered",
  "siteKnowledge": {
    "supportSiteSearch": {
      "term": "roller",
      "locationInPage": "topSearchBar"
    }
  }
});
```

Depois disso `push` tenha lugar, `siteKnowledge` sempre será exibido no estado calculado da camada de dados até que a página seja descarregada (a menos que você remova ou substitua propositalmente `siteKnowledge`).

Por outro lado, este é um exemplo de envio de um evento com dados adicionais que **não é retido** na camada de dados:

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered",
  "eventInfo": {
    "siteKnowledge": {
      "supportSiteSearch": {
        "term": "roller",
        "locationInPage": "topSearchBar"
      }
    }
  }
});
```

Observe neste exemplo que `siteKnowledge` está envolvido dentro `eventInfo`. O `eventInfo` A chave recebe tratamento especial pela camada de dados. Informa à camada de dados que esses dados _should_ ser incluído no evento que é enviado para ouvintes, mas ele _não deve_ ser retidos dentro da camada de dados. Após os ouvintes (como as Tags do Adobe Experience Platform) serem notificados sobre o evento, esses dados serão esquecidos. O `siteKnowledge` A chave nunca será exibida dentro do estado calculado da camada de dados.

Cada vez que você chamar `push`, a Camada de dados do cliente do Adobe notifica todos os ouvintes. Posteriormente, aprenderemos a ouvir essas notificações das Tags do Adobe Experience Platform e a acionar as regras adequadamente.
