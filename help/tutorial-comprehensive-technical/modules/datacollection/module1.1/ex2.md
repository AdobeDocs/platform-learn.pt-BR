---
title: Foundation - Configuração da coleção de dados da Adobe Experience Platform e da extensão SDK da Web - Edge Network, fluxos de dados e coleção de dados do lado do servidor
description: Foundation - Configuração da coleção de dados da Adobe Experience Platform e da extensão SDK da Web - Edge Network, fluxos de dados e coleção de dados do lado do servidor
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# 1.1.2 Edge Network, fluxos de dados e coleção de dados do lado do servidor

## Contexto

Neste exercício, você criará um **Datastream**. Um **Datastream** informa aos servidores Adobe Edge para onde enviar os dados depois que eles são coletados pelo SDK da Web. Por exemplo, deseja enviar os dados para o Adobe Experience Platform? Adobe Analytics? Adobe Audience Manager? Adobe Target?

As sequências de dados são sempre gerenciadas na interface do usuário da Coleção de dados da Adobe Experience Platform e são essenciais para a coleta de dados da Adobe Experience Platform com o SDK da Web. Mesmo ao implementar o SDK da Web com uma solução de gerenciamento de tags que não seja de Adobe, ainda será necessário criar a sequência de dados na interface da Coleção de dados da Adobe Experience Platform.

Você implementará o SDK da Web no navegador no próximo exercício. Dessa forma, você ficará mais claro sobre a aparência dos dados coletados. Por enquanto, estamos apenas informando ao fluxo de dados para onde encaminhar os dados.

## Criar um fluxo de dados

No [Exercício 0.2](./../../../modules/gettingstarted/gettingstarted/ex2.md), você já criou um Datastream, mas não discutimos o plano de fundo e o motivo para pertencer ao Datastream.

Uma sequência de dados informa aos servidores da Adobe Edge para onde enviar os dados depois que eles são coletados pelo SDK da Web. Por exemplo, deseja enviar os dados para o Adobe Experience Platform? Adobe Analytics? Adobe Audience Manager? Adobe Target? Os fluxos de dados são gerenciados na interface do usuário da Coleção de dados da Adobe Experience Platform e são essenciais para a coleção de dados da plataforma com o SDK da Web, independentemente de você estar implementando ou não o SDK da Web por meio da Coleção de dados da Adobe Experience Platform.

Vamos revisar sua **[!UICONTROL Sequência de dados]**:

Ir para [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/).

Clique em **[!UICONTROL Datastreams]** ou **[!UICONTROL Datastreams (Beta)]** no menu esquerdo.

![Clique no ícone Datastream na navegação à esquerda](./images/edgeconfig1.png)

Procure pela sua sequência de dados, chamada `--aepUserLdap-- - Demo System Datastream`.

![Nomeie a sequência de dados e salve](./images/edgeconfig2.png)

Você verá os detalhes da sequência de dados.

![Nomeie a sequência de dados e salve](./images/edgecfg1.png)

Clique em **...** ao lado de **Adobe Experience Platform** e clique em **Editar**.

![Nomeie a sequência de dados e salve](./images/edgecfg1a.png)

Você verá isso. No momento, você só habilitou o Adobe Experience Platform. Sua configuração será semelhante à configuração abaixo. (Dependendo do ambiente e da instância do Adobe Experience Platform, o Nome da sandbox pode ser diferente)

![Nomeie a sequência de dados e salve](./images/edgecfg2.png)

Você deve interpretar os campos abaixo desta forma:

Para esta sequência de dados...

- Todos os dados coletados serão armazenados na sandbox `--aepSandboxName--` no Adobe Experience Platform
- Todos os dados do Evento de experiência são coletados por padrão no conjunto de dados **Sistema de demonstração - Conjunto de dados do evento para o site (Global v1.1)**
- Todos os dados do perfil serão coletados por padrão no conjunto de dados **Sistema de demonstração - Conjunto de dados do perfil para site (Global v1.1)** (a assimilação de dados do perfil nativamente com o SDK da Web atualmente ainda não é suportada pelo SDK da Web e será disponibilizada em um estágio posterior)
- Se você quiser usar o serviço de aplicativo **Offer decisioning** para esta Sequência de Dados, será necessário marcar a caixa Offer decisioning. (Isso fará parte do [Módulo 3.3](./../../../modules/ajo-b2c/module3.3/offer-decisioning.md))
- Se quiser usar a **Segmentação do Edge**, marque a caixa Segmentação do Edge.
- Se você quiser usar os **Destinos do Personalization**, será necessário marcar a caixa para Destinos do Personalization.

Por enquanto, nenhuma outra configuração é necessária para sua sequência de dados.

Próxima Etapa: [1.1.3 Introdução à Coleção de Dados do Adobe Experience Platform](./ex3.md)

[Voltar ao módulo 1.1](./data-ingestion-launch-web-sdk.md)

[Voltar a todos os módulos](./../../../overview.md)
