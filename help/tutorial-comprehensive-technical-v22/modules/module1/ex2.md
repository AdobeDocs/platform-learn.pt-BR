---
title: Foundation - Configuração da coleta de dados da Adobe Experience Platform e da extensão do SDK da Web - Rede de borda, Datastreams e Coleta de dados do lado do servidor
description: Foundation - Configuração da coleta de dados da Adobe Experience Platform e da extensão do SDK da Web - Rede de borda, Datastreams e Coleta de dados do lado do servidor
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 6f7c540f-3804-483d-90f9-b26b4a252b8b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 2%

---

# 1.2 Rede de borda, conjuntos de dados e coleta de dados do lado do servidor

## Contexto

Neste exercício, você criará um **Datastream**. A **Datastream** informa aos servidores da Adobe Edge onde enviar os dados após sua coleta pelo SDK da Web. Por exemplo, você deseja enviar os dados para o Adobe Experience Platform? Adobe Analytics? Adobe Audience Manager? Adobe Target?

Os conjuntos de dados são sempre gerenciados na interface do usuário da Coleta de dados da Adobe Experience Platform e são essenciais para a coleta de dados da Adobe Experience Platform com o SDK da Web. Mesmo ao implementar o SDK da Web com uma solução de gerenciamento de tags que não seja do Adobe, ainda será necessário criar o Datastream na interface do usuário da Coleta de dados da Adobe Experience Platform.

Você implementará o SDK da Web no navegador no próximo exercício. Assim, você terá mais clareza sobre a aparência dos dados coletados. Por enquanto, estamos apenas dizendo ao Datastream onde encaminhar os dados.

## Criar um conjunto de dados

Em [Exercício 0.2](./../module0/ex2.md) você já criou um Datastream, mas não discutimos o plano de fundo e a razão de ser do Datastream.

Um Datastream informa aos servidores da Adobe Edge onde enviar os dados após serem coletados pelo SDK da Web. Por exemplo, você deseja enviar os dados para o Adobe Experience Platform? Adobe Analytics? Adobe Audience Manager? Adobe Target? Os conjuntos de dados são gerenciados na interface do usuário da Coleta de dados da Adobe Experience Platform e são essenciais para a coleta de dados da plataforma com o SDK da Web, independentemente de você estar ou não implementando o SDK da Web por meio da Coleta de dados da Adobe Experience Platform.

Vamos revisar seu **[!UICONTROL Datastream]**:

Ir para [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/).

Clique em **[!UICONTROL Datastreams]** ou **[!UICONTROL Datastreams (Beta)]** no menu esquerdo.

![Clique no ícone Datastream no painel de navegação esquerdo](./images/edgeconfig1.png)

Procure seu Datastream, que é chamado de `--demoProfileLdap-- - Demo System Datastream`.

![Nomeie o armazenamento de dados e salve](./images/edgeconfig2.png)

Você verá os detalhes do seu Datastream.

![Nomeie o armazenamento de dados e salve](./images/edgecfg1.png)

Clique em **...** ao lado de **Adobe Experience Platform** e clique em **Editar**.

![Nomeie o armazenamento de dados e salve](./images/edgecfg1a.png)

Você verá isso. Neste momento, você só ativou o Adobe Experience Platform. Sua configuração será semelhante à configuração abaixo. (Dependendo do seu ambiente e da instância do Adobe Experience Platform, o Nome da sandbox pode ser diferente)

![Nomeie o armazenamento de dados e salve](./images/edgecfg2.png)

Você deve interpretar os campos abaixo desta forma:

Para este armazenamento de dados...

- Todos os dados coletados serão armazenados no `--aepSandboxId--` sandbox no Adobe Experience Platform
- Todos os dados do Evento de experiência são coletados por padrão no conjunto de dados **Sistema de demonstração - Conjunto de dados do evento para site (Global v1.1)**
- Todos os dados do Perfil serão coletados por padrão no conjunto de dados **Sistema de demonstração - Conjunto de dados de perfil para site (Global v1.1)** (a assimilação de dados de perfil nativamente com o SDK da Web no momento ainda não é compatível com o SDK da Web e será disponibilizada em um estágio posterior)
- Se quiser usar a variável **offer decisioning** serviço de aplicativos para esse Datastream, é necessário marcar a caixa Offer decisioning . (Isso fará parte de [Módulo 9](./../module9/offer-decisioning.md))
- Se quiser usar a variável **Segmentação de borda**, é necessário marcar a caixa de seleção Segmentação da borda.
- Se quiser usar a variável **Destinos de personalização**, é necessário marcar a caixa de seleção de Destinos de personalização .

Por enquanto, nenhuma outra configuração é necessária para seu Datastream.

Próxima etapa: [1.3 Introdução à coleta de dados do Adobe Experience Platform](./ex3.md)

[Voltar ao Módulo 1](./data-ingestion-launch-web-sdk.md)

[Voltar para todos os módulos](./../../overview.md)
