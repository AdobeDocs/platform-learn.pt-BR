---
title: Implementar uma camada de dados em uma página de produto
description: Implementar uma camada de dados em uma página de produto
exl-id: 0debf34a-48d4-4029-b790-7fd78865c334
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# Implementar uma camada de dados em uma página de produto

Para este tutorial, você implementa a Camada de dados do cliente do Adobe para um site de comércio eletrônico típico. Se ainda não o fez, leia [Como usar a camada de dados do cliente do Adobe](how-to-use-the-adobe-client-data-layer.md) primeiro para entender a Camada de dados do cliente do Adobe.

Vamos supor que o usuário navegue em seus produtos e clique em um cilindro de espuma para saber mais. O usuário acessa a página de detalhes do produto do cilindro de espuma.

## Criar uma página simples de detalhes do produto

1. Copie e cole o seguinte código em um novo arquivo HTML e salve-o em seu computador.

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

Dentro do `<head>` há uma tag `<script>` . É aqui que você coloca seu código JavaScript. Embora não seja necessário colocar a variável `<script>` dentro da `<head>` é recomendado. Isso garante que os dados estejam disponíveis para a camada de dados o mais rápido possível, para oferecer suporte a uma variedade de casos de uso.

## Adicionar a camada de dados do Adobe

1. Dentro do `<script>` adicione esse código que cria a variável `adobeDataLayer` e, em seguida, envia informações apropriadas de evento e dados para o array. Os dados estão em conformidade com o esquema XDM [você criou anteriormente](../configure-the-server/create-a-schema.md).

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

Neste exemplo, você fez dois empurrões para a camada de dados, cada um contendo um `event` chave. Inclusão de um `event` A chave não apenas comunica o evento que ocorreu na página, como também torna mais simples para o profissional de marketing criar as regras apropriadas dentro das tags.

O primeiro push para a camada de dados notifica os ouvintes (regras de tags) que o usuário visualizou a página. Ele também adiciona o nome da página e a seção do site à camada de dados.

O segundo push para a camada de dados notifica os ouvintes (regras de tags) que o usuário visualizou um produto. Ele também adiciona informações do produto à camada de dados.

## Adicionar código para rastreamento de adição de carrinho

Neste tutorial, você rastreia quando o usuário clica no [!UICONTROL Adicionar ao carrinho] botão.

1. Copie e cole esse código após o código da camada de dados. A função é chamada quando o usuário clica no botão [!UICONTROL Adicionar ao carrinho] botão.

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

Essa função verifica inicialmente se um carrinho já existe para um usuário.  Se o carrinho não existir, você empurra um `cartOpened` para a camada de dados. Mais tarde, você empurra um `productAddedToCart` na camada de dados. As informações do produto já existem na camada de dados, portanto, não é necessário adicioná-las novamente.

## Botão Adicionar atributo para adicionar ao carrinho

1. Adicione um `onclick` para a [!UICONTROL Adicionar ao carrinho] botão que chama o novo `onAddToCartClick` .

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

## Adicionar código para o rastreamento de download do aplicativo

Uma última coisa a ser rastreada é quando o usuário clica no _[!UICONTROL Baixar o aplicativo]_ link .

1. Para fazer isso, copie e cole esse código abaixo do código adicionado do carrinho. Essa função é chamada quando o usuário clica no botão _[!UICONTROL Baixar o aplicativo]_ link .

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

## Adicionar atributo para baixar o link do aplicativo

1. Adicione um `onclick` para a [!UICONTROL Baixar o aplicativo] link que chama seu novo `onDownloadAppClick` .

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

[Próximo: ](create-a-tags-property-and-install-extensions.md)

>[!NOTE]
>
>Obrigado por investir seu tempo para aprender sobre a coleta de dados. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
