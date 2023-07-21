---
title: Bootcamp - Mesclagem física e digital - Teste sua jornada
description: Bootcamp - Mesclagem física e digital - Teste sua jornada
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 45c77177-9ea9-4c3d-a40e-c04a747938eb
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 1%

---

# 3.4 Testar a jornada

Para testar sua jornada, será necessário usar a ID de evento do evento criado no exercício 3.2, que tem esta aparência.

![ACOP](./images/payloadeventID.png)

A ID do evento é o que precisa ser enviado ao Adobe Experience Platform para acionar a jornada. Neste exemplo, a eventID é:
`e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5`.

Abra o aplicativo móvel e vá para a página inicial. Clique no ícone de **Configurações**.

![DSN](./images/appsett.png)

Cole sua eventID no campo **EventID de sinal** e clique em **Salvar**.

![DSN](./images/beacon1.png)

Antes de continuar, abra esta página da Web no computador: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

Você verá isto:

![DSN](./images/screen1.png)

Em seguida, volte para a página inicial. Clique em **sinal** ícone.

![DSN](./images/app23.png)

Você verá isso. Primeiro, selecione **Beacon de tela de bootcamp** e, em seguida, clique no link **entrada** botão. Isso permitirá simular uma entrada de sinal.

![DSN](./images/app21.png)

Agora, dê uma olhada na tela da loja. O último produto exibido aparecerá lá em 5 segundos.

![DSN](./images/beacon3.png)

Você também receberá sua notificação por push.

![DSN](./images/beacon2.png)

Você terminou este exercício agora.

[Voltar para Fluxo de Usuário 3](./uc3.md)

[Voltar a todos os módulos](../../overview.md)
