---
title: Como usar a Camada de dados de clientes Adobe
description: Como usar a Camada de dados de clientes Adobe
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 33a5db8c-e49b-4073-b4d7-4abe19537fcb
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---

# Como usar a Camada de dados de clientes Adobe

Entrada [O que é uma camada de dados?](whats-a-data-layer.md)No entanto, você aprendeu que há duas partes a serem consideradas ao discutir camadas de dados: o container e o conteúdo. A Camada de dados de clientes Adobe é o container. Não importa como você [estruturar seus dados](../structuring-your-data.md) ou quais informações você escolhe incluir em seus dados. Os dados podem ser estruturados como [XDM](../structuring-your-data.md#xdm), como mostram os exemplos abaixo, ou você pode criar totalmente sua própria estrutura.

Idealmente, a equipe de engenharia da empresa é responsável por enviar todos os dados necessários para a camada de dados por meio do código na página. A equipe de marketing recupera os dados da camada de dados, de preferência usando tags do Adobe Experience Platform.

## Envio de dados para a camada de dados

A Camada de dados de clientes Adobe é uma matriz JavaScript. Quando você cria a Camada de dados de clientes Adobe, ela começa vazia:

```js
window.adobeDataLayer = window.adobeDataLayer || [];
```

Para colocar dados na camada de dados, chame o `push` na matriz da camada de dados:

```js
window.adobeDataLayer.push({
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile"
  }
});
```

É possível enviar dados adicionais para a camada de dados a qualquer momento, chamando `push` novamente.

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

## Compreensão dos dados enviados

Se você implementou as duas versões anteriores `push` , você acabaria com duas entradas na matriz da camada de dados. A camada de dados não é particularmente útil nesse estado. Normalmente, você deseja acessar o estado mesclado da camada de dados ou, em outras palavras, um único objeto que seja o resultado combinado de todos os dados enviados para a camada de dados. Posteriormente, aprenderemos como acessar esse estado mesclado no tutorial. Por enquanto, é suficiente entender que o estado calculado da camada de dados após nossos dois `push` seriam as seguintes:

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

Às vezes, você deve remover dados da camada de dados. Isso é particularmente comum em aplicativos de página única quando o usuário navega de uma visualização para outra. Por exemplo, se o usuário navegar de uma exibição de produto para uma exibição de contato, pode ser interessante apagar quaisquer dados de produto na camada de dados, pois eles não são mais pertinentes à exibição ativa.

Você pode remover dados enviando um valor de `undefined` para a chave que deseja remover. Com base em nossos exemplos anteriores, se desejar remover `status` na camada de dados, o código seria semelhante ao seguinte:

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

A Camada de dados do cliente Adobe não é usada apenas para armazenar dados, mas também para comunicar quais eventos estão ocorrendo na página. Na verdade, você normalmente envia dados para a camada de dados _como resultado_ de um evento que ocorre na página. Esses eventos incluem (1) eventos de interação, como abrir um bot de chat ou digitar um termo de pesquisa em uma barra de pesquisa ou (2) eventos não interativos, como a impressão de um anúncio ou a conclusão de cálculos de desempenho da página da Web.

Para comunicar que um evento ocorreu na página, inclua uma `event` no objeto enviado para a camada de dados. Por exemplo, talvez você queira comunicar que um usuário inseriu uma consulta de pesquisa em um campo de pesquisa.

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered"
});
```

Posteriormente, você aprenderá a acionar regras em Tags do Adobe Experience Platform quando um evento específico for enviado para a camada de dados. Observe também que a `event` a chave é _não_ incluído no estado calculado. Ele recebe tratamento especial pela camada de dados.

## Enviar eventos e dados para a camada de dados

Notificar os ouvintes de que o usuário inseriu uma consulta de pesquisa é útil, mas e se você quiser fornecer informações adicionais sobre o evento? Por exemplo, talvez você queira incluir a consulta de pesquisa do usuário. Você pode fornecer esses dados de uma das duas formas a seguir:

1. Forneça dados para que ele **é retido** na camada de dados como parte do estado calculado da camada de dados.
2. Forneça dados para que ele **não está retido** na camada de dados como parte do estado calculado da camada de dados.

Se você deseja reter os dados na camada de dados geralmente depende de se você planeja fazer referência a esses dados ao longo da duração do usuário na página. Caso contrário, reter os dados dentro da camada de dados pode resultar em uma camada de dados desorganizada.

Este é um exemplo de envio de um evento com dados adicionais que **é retido** na camada de dados:

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

Depois disso `push` ocorre, `siteKnowledge` sempre serão exibidas no estado calculado da camada de dados até que a página seja descarregada (a menos que você remova ou substitua propositalmente `siteKnowledge`).

Por outro lado, aqui está um exemplo de envio de um evento com dados adicionais que **não está retido** na camada de dados:

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

Observe neste exemplo que `siteKnowledge` está encapsulado `eventInfo`. A variável `eventInfo` A chave do recebe tratamento especial pela camada de dados. Informa à camada de dados que esses dados _deve_ ser incluído com o evento que é enviado aos ouvintes, mas _não deve_ ser retidos dentro da camada de dados. Depois que os ouvintes (como Tags do Adobe Experience Platform) são notificados do evento, esses dados são essencialmente esquecidos. A variável `siteKnowledge` A chave nunca aparecerá dentro do estado calculado da camada de dados.

Sempre que você ligar `push`, a Camada de dados do cliente Adobe notifica todos os ouvintes. Posteriormente, aprenderemos a ouvir essas notificações das Tags do Adobe Experience Platform e acionar regras apropriadas.
