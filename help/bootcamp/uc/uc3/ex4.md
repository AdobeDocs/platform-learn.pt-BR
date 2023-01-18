---
title: Bootcamp - Mesclagem física e digital - Teste sua jornada
description: Bootcamp - Mesclagem física e digital - Teste sua jornada
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: 45c77177-9ea9-4c3d-a40e-c04a747938eb
source-git-commit: ead28f5631fc430c41e8c756b23dc69ffe19510e
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 1%

---

# 3.4 Teste sua jornada

Para testar sua jornada, você precisará usar a ID de evento do evento criado no exercício 3.2, que tem a seguinte aparência.

![ACOP](./images/payloadeventID.png)

A ID do evento é o que precisa ser enviado para o Adobe Experience Platform para acionar a jornada. Neste exemplo, a eventID é:
`e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5`.

Abra o aplicativo móvel e vá para a página inicial. Clique no ícone de **Configurações**.

![DSN](./images/appsett.png)

Cole a eventID no campo **EventID de sinal** e clique em **Salvar**.

![DSN](./images/beacon1.png)

Antes de continuar, abra esta página da Web no seu computador: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

Você verá isso:

![DSN](./images/screen1.png)

Em seguida, volte para a página inicial. Clique no botão **beacon** ícone .

![DSN](./images/app23.png)

Você verá isso. Primeiro, selecione **Beacon de tela de bootcamp** e clique no botão **entrada** botão. Isso permitirá simular uma entrada de beacon.

![DSN](./images/app21.png)

Agora, dê uma olhada na tela da loja. Você verá o último produto exibido lá em 5 segundos.

![DSN](./images/beacon3.png)

Você também receberá sua notificação por push.

![DSN](./images/beacon2.png)

Você já terminou este exercício.

[Voltar para Fluxo de Usuário 3](./uc3.md)

[Voltar para todos os módulos](../../overview.md)
