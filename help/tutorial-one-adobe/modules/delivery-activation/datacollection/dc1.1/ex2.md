---
title: Foundation - Configuração da coleção de dados do Adobe Experience Platform e da extensão Web SDK - Edge Network, fluxos de dados e coleção de dados do lado do servidor
description: Foundation - Configuração da coleção de dados do Adobe Experience Platform e da extensão Web SDK - Edge Network, fluxos de dados e coleção de dados do lado do servidor
kt: 5342
doc-type: tutorial
exl-id: f805b2a6-c813-4734-8a78-f8588ecd0683
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---

# 1.1.2 Edge Network, fluxos de dados e coleção de dados do lado do servidor

## Contexto

Neste exercício, você criará uma **sequência de dados**. Uma **sequência de dados** informa aos servidores da Rede de borda da Adobe para onde enviar os dados depois que eles forem coletados pelo Web SDK. Por exemplo, deseja enviar os dados para o Adobe Experience Platform? Adobe Analytics? Adobe Audience Manager? Adobe Target?

As sequências de dados são sempre gerenciadas na interface da Coleção de dados da Experience Platform e são críticas para a coleção de dados da Experience Platform com o [Web SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/web-sdk/home). Mesmo ao implementar o Web SDK com uma solução de gerenciamento de tags que não seja a Adobe, ainda é necessário criar um fluxo de dados.

Você implementará o Web SDK no navegador no próximo exercício. Dessa forma, você ficará mais claro sobre a aparência dos dados coletados. Por enquanto, estamos apenas informando ao fluxo de dados para onde encaminhar os dados.

## Criar um fluxo de dados

Em [Introdução](./../../../../modules/getting-started/gettingstarted/ex2.md), você já criou uma sequência de dados, mas não discutimos o plano de fundo e o motivo da sua criação.

Uma [sequência de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/datastreams/overview) informa aos servidores da Edge Network para onde enviar os dados após serem coletados pela Web SDK. Consulte a documentação de [adicionando serviços a uma sequência de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/datastreams/configure#add-services) para obter detalhes completos sobre para onde enviar seus dados por meio da sequência de dados.

Os fluxos de dados são gerenciados na interface da Coleção de dados da Experience Platform e são essenciais para a coleta de dados com o Web SDK, independentemente de você estar implementando o Web SDK por meio da Coleção de dados do Adobe Experience Platform.

Vamos revisar sua **[!UICONTROL sequência de dados]**:

Ir para [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/).

Clique em **[!UICONTROL Datastreams]** no menu esquerdo.

![Clique no ícone Datastream na navegação à esquerda](./images/edgeconfig1.png)

Abra a sequência de dados chamada `--aepUserLdap-- - Demo System Datastream`.

![Nomeie a sequência de dados e salve](./images/edgeconfig2.png)

Você verá os detalhes do seu fluxo de dados.

![Nomeie a sequência de dados e salve](./images/edgecfg1.png)

Clique em **...** ao lado de **Adobe Experience Platform** e clique em **Editar**.

![Nomeie a sequência de dados e salve](./images/edgecfg1a.png)

Você verá isso. No momento, você só habilitou o Adobe Experience Platform. Sua configuração será semelhante à configuração abaixo. (Dependendo do ambiente e da instância do Adobe Experience Platform, o Nome da sandbox pode ser diferente)

![Nomeie a sequência de dados e salve](./images/edgecfg2.png)

Você deve interpretar os campos abaixo desta forma:

Para esta sequência de dados...

- Todos os dados coletados serão armazenados na sandbox `--aepSandboxName--` no Adobe Experience Platform
- Todos os dados do Evento de experiência são coletados por padrão no conjunto de dados **Sistema de demonstração - Conjunto de dados do evento para o site (Global v1.1)**
- Todos os dados do perfil serão coletados por padrão no conjunto de dados **Sistema de demonstração - Conjunto de dados do perfil para site (Global v1.1)** (a assimilação de dados do perfil nativamente com o Web SDK atualmente ainda não é compatível com o Web SDK)
- Se você quiser usar o serviço de aplicativos **Offer Decisioning** para esta sequência de dados, será necessário marcar a caixa Offer Decisioning. (Isso fará parte do [Módulo 3.3](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-3/offer-decisioning.md))
- A **Segmentação do Edge** está habilitada por padrão, o que significa que os públicos qualificados serão avaliados na borda após a assimilação do tráfego de entrada
- Se quiser usar [destinos de personalização](https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/catalog/personalization/overview), marque a caixa para **Destinos do Personalization**.
- Se você quiser usar os recursos do **Adobe Journey Optimizer** nesta sequência de dados, será necessário marcar a caixa para **Adobe Journey Optimizer**.

Por enquanto, nenhuma outra configuração é necessária para o fluxo de dados.

## Próximas etapas

Ir para [1.1.3 Introdução à Coleção de Dados do Adobe Experience Platform](./ex3.md){target="_blank"}

Retorne à [Instalação da Coleção de Dados da Adobe Experience Platform e da extensão de marca da Web SDK](./data-ingestion-launch-web-sdk.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
