---
title: Offer Decisioning - Teste sua decisão usando a API
description: Teste sua decisão usando a API
kt: 5342
doc-type: tutorial
exl-id: 52f90b9f-32ea-49c2-af5d-8742ca8b3b4e
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# 3.3.6 Testar sua decisão usando a API

## 3.3.6.1 Trabalhar com a API do Offer Decisioning usando o Postman

>[!IMPORTANT]
>
>Se você for um funcionário da Adobe, siga as instruções aqui para usar o [PostBuster](./../../../../modules/getting-started/gettingstarted/ex8.md).

Baixe [esta Coleção do Postman para Offer Decisioning](./../../../../assets/postman/postman_offer-decisioning.zip) na área de trabalho e descompacte-a. Você terá isto:

![API OD](./images/unzip.png)

Agora você tem este arquivo na área de trabalho:

- `_AJO- Decisioning Service.postman_collection.json`

No [Exercício 2.1.3 - Autenticação do Postman para o Adobe I/O](./../../../../modules/delivery-activation/rtcdp-b2c/rtcdpb2c-1/ex3.md), você instalou o Postman. Você precisará usar o Postman novamente para este exercício.

Abra o Postman e importe o arquivo `_AJO- Decisioning Service.postman_collection.json`. Em seguida, você terá essa coleção disponível no Postman.

![Nova integração do Adobe I/O](./images/postmanui.png)

Agora você tem tudo o que precisa no Postman para começar a interagir com o Adobe Experience Platform por meio das APIs.

Antes de poder usar as APIs abaixo, certifique-se de reautenticar usando a coleção **Adobe IO - OAuth** que você configurou no Exercício 2.1.3.

![Nova integração do Adobe I/O](./images/postmanui1.png)


### 3.3.6.2 Obter ofertas para o perfil do cliente

Clique para abrir a solicitação **POST - Obter Ofertas para Perfil de Cliente**. A primeira coisa a ser atualizada é a variável **Cabeçalho** para **x-sandbox-name**. Você deve defini-lo como `--aepSandboxName--`.

![API OD](./images/api23.png)

Para essa solicitação, há vários campos que precisam ser atualizados. Ir para **Corpo**.

- **xdm:placementId**
- **xdm:activityId**
- **xdm:id**
- **xdm:itemCount** (altere para um valor de escolha)

![API OD](./images/api24.png)

O campo **xdm:activityId** precisa ser preenchido. Você pode recuperá-lo na interface do usuário do Adobe Experience Platform, conforme indicado abaixo.

![API OD](./images/activityid.png)

O campo **[!UICONTROL xdm:placementId]** precisa ser preenchido. Você pode recuperá-lo na interface do usuário do Adobe Experience Platform, conforme indicado abaixo. No exemplo abaixo, você pode ver o placementId para o posicionamento **[!UICONTROL Web - Image]**.

![API OD](./images/placementid.png)

Para o campo **xdm:id**, insira o endereço de email do perfil do cliente para o qual você deseja solicitar uma oferta. Depois que todos os valores forem definidos como desejado, clique em **[!UICONTROL Enviar]**.

![API OD](./images/api24a.png)

Por fim, você verá o resultado de que tipo de oferta personalizada e quais ativos precisam ser exibidos para esse cliente. Neste exemplo, 2 itens foram solicitados e, como você pode ver, 2 ofertas personalizadas foram retornadas. 1 oferta para o Apple Watch e outra oferta para o Galaxy Watch 7.

![API OD](./images/api25.png)

Você concluiu este exercício agora.

## Próximas etapas

Ir para [Resumo e benefícios](./summary.md){target="_blank"}

Voltar para [Offer Decisioning](offer-decisioning.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
