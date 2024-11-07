---
title: Foundation - Configuração da coleta de dados do Adobe Experience Platform e da extensão SDK da Web - Implementação do Adobe Target
description: Foundation - Configuração da coleta de dados do Adobe Experience Platform e da extensão SDK da Web - Implementação do Adobe Target
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# 1.1.6 Implementação do Adobe Target

## 1.1.6.1 Atualizar a sequência de dados para usar o Adobe Target

Caso queira enviar dados coletados pelo SDK da Web para a Adobe Target e obter uma resposta do Adobe Target com uma experiência personalizada para cada cliente, siga estas etapas.

Vá para [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) e vá para **Datastreams**.

No canto superior direito da tela, selecione o nome da sandbox, que deve ser `--aepSandboxName--`. Abra a sequência de dados específica chamada `--aepUserLdap-- - Demo System Datastream`.

![Clique no ícone Configuração do Edge na navegação à esquerda](./images/edgeconfig1b.png)

Você verá isso. Para habilitar o Adobe Target, clique em **+Adicionar Serviço**.

![Depurador da AEP](./images/aa2.png)

Você verá isso. Selecione o serviço **Adobe Target**, após o qual você pode fornecer informações adicionais. No momento, não há necessidade de salvar, então clique em **Cancelar**.

![Depurador da AEP](./images/at1.png)

Próxima etapa: [Requisitos do esquema XDM 1.1.7 no Adobe Experience Platform](./ex7.md)

[Voltar ao módulo 1.1](./data-ingestion-launch-web-sdk.md)

[Voltar a todos os módulos](./../../../overview.md)
