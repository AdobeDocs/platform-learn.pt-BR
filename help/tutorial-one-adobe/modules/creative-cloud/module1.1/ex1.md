---
title: Introdução aos serviços da Firefly
description: Saiba como usar o Postman e o Adobe I/O para consultar APIs de serviços da Adobe Firefly
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: 5ee9c3b7cde5444ecceca4b01cc275d6263d8a59
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# 1.1.1 Introdução aos Serviços Firefly

Saiba como usar o Postman e o Adobe I/O para consultar APIs de serviços da Adobe Firefly.

## 1.1.1.1 Pré-requisitos

Antes de continuar com este exercício, você precisa ter concluído a configuração do [seu projeto do Adobe I/O](./../../../modules/getting-started/gettingstarted/ex6.md) e também precisa ter configurado um aplicativo para interagir com APIs, como o [Postman](./../../../modules/getting-started/gettingstarted/ex7.md) ou o [PostBuster](./../../../modules/getting-started/gettingstarted/ex8.md).

## 1.1.1.2 Adobe I/O - access_token

Na coleção **Adobe IO - OAuth**, selecione a solicitação denominada **POST - Obter Token de Acesso** e selecione **Enviar**. A resposta deve conter um novo **accestoken**.

![Postman](./images/ioauthresp.png){zoomable="yes"}

## 1.1.1.3 API de serviços do Firefly, imagem do texto 2

Agora que você tem um access_token válido e atualizado, você está pronto para enviar sua primeira solicitação às APIs de serviços da Firefly.

Selecione a solicitação denominada **POST - Firefly - T2I V3** da coleção **FF - Firefly Services Tech Insiders**.

![Firefly](./images/ff1.png){zoomable="yes"}

Copie o URL da imagem da resposta e abra-o em seu navegador da Web para exibir a imagem.

![Firefly](./images/ff2.png){zoomable="yes"}

Você deve ver uma bela imagem representando `horses in a field`.

![Firefly](./images/ff3.png){zoomable="yes"}

Fique à vontade para brincar com a solicitação da API antes de continuar com o próximo exercício.

## Próximas etapas

Vá para [Otimizar seu processo do Firefly usando o Microsoft Azure e URLs pré-assinadas](./ex2.md){target="_blank"}

Retorne para [Visão geral dos Serviços da Adobe Firefly](./firefly-services.md){target="_blank"}

Voltar para [Todos os módulos](./../../../overview.md){target="_blank"}
