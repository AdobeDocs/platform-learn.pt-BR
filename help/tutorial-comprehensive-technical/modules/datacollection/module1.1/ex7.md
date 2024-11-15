---
title: Foundation - Configuração da coleta de dados do Adobe Experience Platform e da extensão SDK da Web - Requisitos do esquema XDM no Adobe Experience Platform
description: Foundation - Configuração da coleta de dados do Adobe Experience Platform e da extensão SDK da Web - Requisitos do esquema XDM no Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: 3fc4a1d6-4130-464e-98c0-5b9cac8051a0
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Requisitos do esquema XDM 1.1.7 no Adobe Experience Platform

Para garantir que o SDK da Web e o alloy.js possam assimilar dados no Adobe Experience Platform, há um requisito para que um Mixin XDM específico faça parte do Esquema XDM no Adobe Experience Platform.

Vá para [https://experience.adobe.com/platform](https://experience.adobe.com/platform) e faça logon.

![Depurador da AEP](./images/exp1.png)

Depois de fazer logon, selecione a sandbox apropriada clicando no texto **Produção** na linha azul na parte superior da tela. Selecione a sandbox `--aepSandboxName--`.

Depois de selecionar sua sandbox, você verá a alteração da tela e agora estará em sua sandbox.

![Depurador da AEP](./images/exp2.png)

No menu esquerdo, vá para **Esquemas** e abra o **Sistema de Demonstração - Esquema de Evento para o Site (Global v1.1)** Esquema.

![Depurador da AEP](./images/exp3.png)

Nesse esquema, você verá que o grupo de campos **ExperienceEvent do SDK da Web da AEP** foi adicionado. Este grupo de campos adiciona todos os campos mínimos obrigatórios ao esquema. Cada esquema de evento de experiência no Adobe Experience Platform que será usado pelo SDK da Web sempre exigirá que esse grupo de campos faça parte do esquema.

![Depurador da AEP](./images/exp4.png)

No [Módulo 1.2](./../module1.2/data-ingestion.md), você aprenderá a adicionar grupos de campos a esquemas.

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao módulo 1.1](./data-ingestion-launch-web-sdk.md)

[Voltar a todos os módulos](./../../../overview.md)
