---
title: Foundation - Configuração da coleta de dados do Adobe Experience Platform e da extensão Web SDK - Implementação do Adobe Target
description: Foundation - Configuração da coleta de dados do Adobe Experience Platform e da extensão Web SDK - Implementação do Adobe Target
kt: 5342
doc-type: tutorial
exl-id: 31cdde2f-011d-442d-8e47-15a318a6c89d
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 2%

---

# 1.1.6 Implementação do Adobe Target

## Atualizar sua sequência de dados para usar o Adobe Target

Caso deseje enviar dados coletados pelo Web SDK para o Adobe Target e obter uma resposta do Adobe Target com uma experiência personalizada para cada cliente, siga estas etapas.

Vá para [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) e vá para **Datastreams**.

No canto superior direito da tela, selecione o nome da sandbox, que deve ser `--aepSandboxName--`. Abra a sequência de dados específica chamada `--aepUserLdap-- - Demo System Datastream`.

![Clique no ícone Configuração do Edge na navegação à esquerda](./images/edgeconfig1b.png)

Você verá isso. Para habilitar o Adobe Target, clique em **Adicionar Serviço**.

![Depurador da AEP](./images/aa2.png)

Você verá isso. Selecione o serviço **Adobe Target**, após o qual você pode fornecer informações adicionais. Clique em **Salvar**.

![Depurador da AEP](./images/at1.png)

## Próximas etapas

Ir para [Requisitos do esquema XDM 1.1.7 no Adobe Experience Platform](./ex7.md){target="_blank"}

Retorne à [Instalação da Coleção de Dados da Adobe Experience Platform e da extensão de marca da Web SDK](./data-ingestion-launch-web-sdk.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
