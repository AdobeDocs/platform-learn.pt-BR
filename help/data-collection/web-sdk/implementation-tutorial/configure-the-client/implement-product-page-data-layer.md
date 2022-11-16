---
title: Implementar uma camada de dados em uma página de produto
description: Implementar uma camada de dados em uma página de produto
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: a72011a5-ea9c-45df-a0f3-5eb40bc99d3f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Implementar uma camada de dados em uma página de produto

Neste tutorial, você implementará a Camada de dados do cliente do Adobe para um site de comércio eletrônico típico. Se ainda não o fez, leia [Como usar a camada de dados do cliente do Adobe](how-to-use-the-adobe-client-data-layer.md) primeiro para entender como a Camada de dados do cliente do Adobe opera.

Vamos supor que o usuário navegue em seus produtos e clique em um cilindro de espuma para saber mais. O usuário acessa a página de detalhes do produto do cilindro de espuma.

Aqui está a HTML para sua página de detalhes simples do produto:

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

Como você pode ter notado, dentro da `<head>` há uma tag `<script>` . É aqui que você coloca seu código JavaScript. Não é necessário colocar a variável `<script>` dentro da tag `<head>`, mas enviar dados para a camada de dados o mais rápido possível ajuda a garantir que ela esteja rapidamente disponível para o profissional de marketing enviar para a Adobe Experience Platform antes de o usuário sair da página.

Dentro do `<script>` , você começará criando a variável `adobeDataLayer` e, em seguida, enviando informações apropriadas de evento e dados para o array. Os dados estão em conformidade com o esquema XDM [você criou anteriormente](../configure-the-server/create-a-schema.md).

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

Neste exemplo, você fez dois empurrões para a camada de dados, cada um contendo um `event` chave. Inclusão de um `event` A chave não apenas comunica o evento que ocorreu na página, como também torna mais simples para o profissional de marketing criar regras apropriadas dentro das Tags do Adobe Experience Platform.

O primeiro push para a camada de dados notifica os ouvintes (regras de Tags) que o usuário visualizou a página. Ele também adiciona o nome da página e a seção do site à camada de dados.

O segundo push para a camada de dados notifica os ouvintes (regras de Tags) que o usuário visualizou um produto. Ele também adiciona informações do produto à camada de dados.

## Adicionar ao carrinho

Você também deve querer rastrear quando o usuário clicar no botão [!UICONTROL Adicionar ao carrinho] botão.

Para fazer isso, crie uma função chamada quando o usuário clicar no botão [!UICONTROL Adicionar ao carrinho] botão.

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

Quando essa função é chamada, verifica primeiro se um carrinho já existe para um usuário. Normalmente, isso seria feito verificando se um cookie ou variável específica existe. Se o carrinho não existir, você pressionará um `cartOpened` na camada de dados. Posteriormente, você pressionará um `productAddedToCart` na camada de dados. As informações do produto já existem na camada de dados, portanto, não é necessário adicioná-las novamente.

Adicione um `onclick` para a [!UICONTROL Adicionar ao carrinho] botão que chama o novo `onAddToCartClick` .

O resultado da sua página do HTML deve ser o seguinte:

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

Uma última coisa a fazer é rastrear quando o usuário clica no botão _[!UICONTROL Baixar o aplicativo]_ link .

Para fazer isso, crie uma função chamada quando o usuário clicar no botão _[!UICONTROL Baixar o aplicativo]_ link .

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

Nesse caso, as informações sobre o link são encapsuladas dentro de um `eventInfo` chave. Conforme discutido no [Como usar a camada de dados do cliente do Adobe](how-to-use-the-adobe-client-data-layer.md), isso instrui a camada de dados a comunicar esses dados juntamente com o evento, mas para _not_ mantenha os dados dentro da camada de dados. Para um clique em um link, não é útil adicionar informações sobre o link clicado à camada de dados porque ela não pertence à página como um todo e não se aplica a outros eventos que podem ocorrer.

Adicione um `onclick` para a [!UICONTROL Baixar o aplicativo] link que chama seu novo `onDownloadAppClick` .

O resultado da sua página do HTML deve ser o seguinte:

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
