---
title: Publicar a biblioteca
description: Publicar a biblioteca
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 2fc072df-24f2-4fea-848f-0a973deca2f8
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 4%

---

# Publicar a biblioteca

Agora é hora de implantar a biblioteca de tags em seu site.

## Criar uma biblioteca

Primeiro, você deve criar uma biblioteca que inclua as extensões, as regras e os elementos de dados criados. Para criar uma biblioteca, selecione [!UICONTROL Fluxo de publicação] no menu à esquerda.

Selecionar [!UICONTROL Adicionar biblioteca].

Você deve ver a visualização de criação da biblioteca.

![criação da biblioteca de tags](../../../assets/implementation-strategy/tags-library-creation.png)

Nomeie a biblioteca, como _Demonstração_. Selecionar [!UICONTROL Desenvolvimento] no [!UICONTROL Ambiente] lista suspensa. Clique em [!UICONTROL Adicionar todos os recursos alterados].

Agora você deve ver todas as extensões, regras e elementos de dados listados em [!UICONTROL Alterações de recursos]. Clique em [!UICONTROL Salvar e criar no desenvolvimento].

## Adicionar o código incorporado ao HTML

Agora é necessário adicionar uma tag de script ao HTML da página do produto que carrega a biblioteca de tags recém-criada.

Comece clicando em [!UICONTROL Ambientes] no menu à esquerda. Você deve ver três ambientes diferentes listados.

![Ambientes de tags](../../../assets/implementation-strategy/tags-environments.png)

Clique no ícone do pacote na [!UICONTROL Desenvolvimento] linha de ambiente. Você deve ver instruções para instalar o script da biblioteca do Launch na sua página.

![Instruções de instalação de tags](../../../assets/implementation-strategy/tags-installation-instructions.png)

Copie a tag do script (há um botão copiar para a área de transferência para conveniência). Abra o HTML da página do produto e insira a tag do script antes da tag `</head>` tag. O HTML final deve ter a seguinte aparência:

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
    <!--Swap this script tag with your own-->
    <script src="https://assets.adobedtm.com/xxxxxxxxxxxx/xxxxxxxxxxxx/launch-xxxxxxxxxxxx-development.min.js" async></script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download" onclick="onDownloadAppClick()">Download the app</a>
  </body>
</html>
```

Confira o [documentação de publicação para tags](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html?lang=pt-BR) se quiser saber mais sobre o processo de publicação.

Em seguida, você testará sua nova implementação.
