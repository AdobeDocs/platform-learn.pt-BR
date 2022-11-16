---
title: Foundation - Configuração da coleta de dados do Adobe Experience Platform e da extensão do SDK da Web - Implementar o Adobe Target
description: Foundation - Configuração da coleta de dados do Adobe Experience Platform e da extensão do SDK da Web - Implementar o Adobe Target
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 4aee8ae2-38ca-49a3-8f1b-57713d16f5b5
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# 1.6 Implementar o Adobe Target

## 1.6. Atualize seu conjunto de dados para usar o Adobe Target

Caso queira enviar dados coletados pelo SDK da Web para o Adobe Target e obter uma resposta do Adobe Target com uma experiência personalizada para cada cliente, siga essas etapas.

Ir para [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) e ir para **Datastreams**.

No canto superior direito da tela, selecione o nome da sandbox, que deve ser `--aepSandboxId--`. Abra o armazenamento de dados específico, que é nomeado como `--demoProfileLdap-- - Demo System Datastream`.

![Clique no ícone Configuração de borda no painel de navegação esquerdo](./images/edgeconfig1b.png)

Você verá isso. Para ativar o Adobe Target, clique em **+Adicionar serviço**.

![Depurador AEP](./images/aa2.png)

Você verá isso. Selecionar o serviço **Adobe Target**, depois disso, é possível fornecer informações adicionais opcionalmente. Nesse momento, não há necessidade de salvar isso, então clique em **Cancelar**.

![Depurador AEP](./images/at1.png)

Próxima etapa: [Requisitos do esquema XDM 1.7 no Adobe Experience Platform](./ex7.md)

[Voltar ao Módulo 1](./data-ingestion-launch-web-sdk.md)

[Voltar para todos os módulos](./../../overview.md)
