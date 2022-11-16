---
title: Foundation - Configuração da coleta de dados da Adobe Experience Platform e da extensão do SDK da Web - Requisitos do esquema XDM no Adobe Experience Platform
description: Foundation - Configuração da coleta de dados da Adobe Experience Platform e da extensão do SDK da Web - Requisitos do esquema XDM no Adobe Experience Platform
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 8e17129c-633d-45bd-aa70-78cc3d3a2108
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# Requisitos do esquema XDM 1.7 no Adobe Experience Platform

Para garantir que o SDK da Web e o alloy.js sejam capazes de assimilar dados no Adobe Experience Platform, há um requisito para que uma Mistura XDM específica faça parte do Esquema XDM no Adobe Experience Platform.

Ir para [https://experience.adobe.com/platform](https://experience.adobe.com/platform) e faça logon.

![Depurador AEP](./images/exp1.png)

Depois de fazer logon, selecione a sandbox apropriada clicando no texto **Produto de produção** na linha azul na parte superior da tela. Selecionar a sandbox `--aepSandboxId--`.

Depois de selecionar a sandbox, você verá a tela mudar e agora estará na sandbox.

![Depurador AEP](./images/exp2.png)

No menu esquerdo, acesse **Esquemas** e abra o **Sistema de demonstração - Esquema de evento para site (Global v1.1)** Esquema.

![Depurador AEP](./images/exp3.png)

Nesse esquema, você verá que o grupo de campos **Mistura AEP Web SDK ExperienceEvent** foi adicionada. Esse grupo de campos adiciona todos os campos mínimos obrigatórios ao Esquema. Todo esquema de evento de experiência no Adobe Experience Platform que será usado pelo SDK da Web sempre exigirá que esse grupo de campos faça parte do esquema.

![Depurador AEP](./images/exp4.png)

Em [Módulo 2](./../module2/data-ingestion.md) você aprenderá a adicionar grupos de campo a schemas.

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao Módulo 1](./data-ingestion-launch-web-sdk.md)

[Voltar para todos os módulos](./../../overview.md)
