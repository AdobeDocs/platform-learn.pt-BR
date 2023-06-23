---
title: Implementar uma camada de dados em uma página de produto
description: Implementar uma camada de dados em uma página de produto
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: a72011a5-ea9c-45df-a0f3-5eb40bc99d3f
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Implementar uma camada de dados em uma página de produto

Para este tutorial, você implementará a Camada de dados do cliente Adobe para um site de comércio eletrônico típico. Se ainda não tiver feito isso, leia [Como usar a Camada de dados de clientes Adobe](how-to-use-the-adobe-client-data-layer.md) primeiro para entender como a Camada de dados de clientes Adobe funciona.

Vamos supor que o usuário navegue em seus produtos e clique em um cilindro de espuma para saber mais. O usuário acessa a página de detalhes do produto de cilindro de espuma.

Esta é a HTML da página de detalhes simples do produto:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Product Page</title>
    <script>
      // Code will go here.
    </script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button">Add to cart</button>
    <a href="https://example.com/download">Download the app</a>
  </body>
</html>
```

Como você deve ter notado, dentro do `<head>` há uma tag `<script>` tag. É aqui que você colocará seu código JavaScript. Não é necessário colocar o `<script>` tag no `<head>`, mas o envio de dados para a camada de dados assim que possível ajuda a garantir que ela esteja rapidamente disponível para o profissional de marketing enviar para o Adobe Experience Platform antes que o usuário saia da página.

Dentro do `<script>` , você começará criando o `adobeDataLayer` e, em seguida, enviar as informações apropriadas sobre eventos e dados para o array. Os dados estão em conformidade com o esquema XDM [você criou anteriormente](../configure-the-server/create-a-schema.md).

```js
window.adobeDataLayer = window.adobeDataLayer || [];
window.adobeDataLayer.push({
  "event": "pageViewed",
  "web": {
    "webPageDetails": {
      "name": "Foam Roller",
      "siteSection": "Equipment"
    },
  }
});
window.adobeDataLayer.push({
  "event": "productViewed",
  "productListItems": [
    {
      "SKU": "eqfr08",
      "currencyCode": "USD",
      "name": "Foam Roller",
      "priceTotal": 18.95
    }
  ]
});
```

Neste exemplo, você fez dois envios para a camada de dados, cada um contendo um `event` chave. Incluindo um `event` A chave não apenas comunica qual evento ocorreu na página, como também facilita para o profissional de marketing a criação de regras apropriadas dentro das Tags do Adobe Experience Platform.

O primeiro push para a camada de dados notifica os ouvintes (regras de tags) de que o usuário visualizou a página. Ele também adiciona o nome da página e a seção do site à camada de dados.

O segundo push para a camada de dados notifica os ouvintes (regras de tags) de que o usuário visualizou um produto. Também adiciona informações do produto à camada de dados.

## Adicionar ao carrinho

Você provavelmente também deseja rastrear quando o usuário clica na variável [!UICONTROL Adicionar ao carrinho] botão.

Para fazer isso, crie uma função que seja chamada quando o usuário clicar no [!UICONTROL Adicionar ao carrinho] botão.

```js
window.onAddToCartClick = function() {
  // In a real implementation, you would change this condition to 
  // only pass if a cart doesn't already exist. You would typically 
  // do this by checking a cookie or variable value.
  if (true) {
    window.adobeDataLayer.push({
      "event": "cartOpened",
    });
  }
  window.adobeDataLayer.push({
    "event": "productAddedToCart"
  });
};
```

Quando essa função é chamada, ela verifica primeiro se um carrinho já existe para um usuário. Normalmente, isso é feito verificando se um cookie ou uma variável específica existe. Se o carrinho não existir, você enviará um `cartOpened` na camada de dados. Posteriormente, você enviará um `productAddedToCart` na camada de dados. As informações do produto já existem na camada de dados, portanto, não é necessário adicioná-las novamente.

Adicionar um `onclick` atributo para o [!UICONTROL Adicionar ao carrinho] botão que chama seu novo `onAddToCartClick` função.

O resultado da sua página de HTML deve ser semelhante ao seguinte:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Product Page</title>
    <script>
      window.adobeDataLayer = window.adobeDataLayer || [];
      window.adobeDataLayer.push({
        "event": "pageViewed",
        "web": {
          "webPageDetails": {
            "name": "Foam Roller",
            "siteSection": "Equipment"
          },
        },
        "productListItems": [
          {
            "SKU": "eqfr08",
            "currencyCode": "USD",
            "name": "Foam Roller",
            "priceTotal": 18.95
          }
        ]
      });
      window.adobeDataLayer.push({
        "event": "productViewed"
      });
      window.onAddToCartClick = function() {
        // In a real implementation, you would change this condition to 
        // only pass if a cart doesn't already exist. You would typically 
        // do this by checking a cookie or variable value.
        if (true) {
          window.adobeDataLayer.push({
            "event": "cartOpened",
          });
        }
        window.adobeDataLayer.push({
          "event": "productAddedToCart"
        });
      };
    </script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download">Download the app</a>
  </body>
</html>
```

## Baixar o aplicativo

Uma última coisa a fazer é rastrear quando o usuário clica no _[!UICONTROL Baixar o aplicativo]_ link.

Para fazer isso, crie uma função que seja chamada quando o usuário clicar no _[!UICONTROL Baixar o aplicativo]_ link.

```js
window.onDownloadAppClick = function(event) {
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
};
```

Nesse caso, as informações sobre o link são colocadas dentro de um `eventInfo` chave. Conforme discutido em [Como usar a Camada de dados de clientes Adobe](how-to-use-the-adobe-client-data-layer.md), isso instrui a camada de dados a comunicar esses dados junto com o evento, mas a _não_ reter os dados na camada de dados. Para um clique em links, não é útil adicionar informações sobre o link clicado à camada de dados, pois ele não pertence à página como um todo e não se aplica a outros eventos que podem ocorrer.

Adicionar um `onclick` atributo para o [!UICONTROL Baixar o aplicativo] link que chama seu novo `onDownloadAppClick` função.

O resultado da sua página de HTML deve ser semelhante ao seguinte:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Product Page</title>
    <script>
      window.adobeDataLayer = window.adobeDataLayer || [];
      window.adobeDataLayer.push({
        "event": "pageViewed",
        "web": {
          "webPageDetails": {
            "name": "Foam Roller",
            "siteSection": "Equipment"
          },
        },
        "productListItems": [
          {
            "SKU": "eqfr08",
            "currencyCode": "USD",
            "name": "Foam Roller",
            "priceTotal": 18.95
          }
        ]
      });
      window.adobeDataLayer.push({
        "event": "productViewed"
      });
      window.onAddToCartClick = function() {
        // In a real implementation, you would change this condition to 
        // only pass if a cart doesn't already exist. You would typically 
        // do this by checking a cookie or variable value.
        if (true) {
          window.adobeDataLayer.push({
            "event": "cartOpened",
          });
        }
        window.adobeDataLayer.push({
          "event": "productAddedToCart"
        });
      };
      window.onDownloadAppClick = function() {
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
      };
    </script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download" onclick="onDownloadAppClick()">Download the app</a>
  </body>
</html>
```
