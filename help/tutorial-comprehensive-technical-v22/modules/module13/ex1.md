---
title: Ativação de Segmento para o Hub de Eventos do Microsoft Azure - Configurar Hub de Eventos no Azure
description: Ativação de Segmento para o Hub de Eventos do Microsoft Azure - Configurar Hub de Eventos no Azure
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 9434ac83-5554-48bf-838c-7346d571efbf
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 1%

---

# 13.1 Configurar o ambiente do Microsoft Azure EventHub

O Hubs de Eventos do Azure é um serviço de assinatura de publicação altamente escalável que pode assimilar milhões de eventos por segundo e fazer o stream deles em vários aplicativos. Isso permite processar e analisar a grande quantidade de dados produzidos por seus dispositivos e aplicativos conectados.

## 13.1.1 O que é o Hubs de Eventos do Azure?

O Hubs de eventos do Azure é uma grande plataforma de transmissão de dados e serviço de assimilação de eventos. Ele pode receber e processar milhões de eventos por segundo. Os dados enviados para um hub de eventos podem ser transformados e armazenados usando qualquer provedor de análise em tempo real ou adaptadores de armazenamento/agrupamento.

O Hubs de evento representa a variável **porta da frente** para um pipeline de evento, normalmente chamado de ingresso de evento em arquiteturas de solução. Um assimilador de eventos é um componente ou serviço que se situa entre editores de eventos (como Adobe Experience Platform RTCDP) e consumidores de eventos para dissociar a produção de um fluxo de eventos do consumo desses eventos. O Event Hubs fornece uma plataforma de transmissão unificada com buffer de retenção de tempo, dissociando produtores de eventos dos consumidores de eventos.

## 13.1.2 Criar um namespace de Hubs de evento

Ir para [https://portal.azure.com/#home](https://portal.azure.com/#home) e selecione **Criar um recurso**.

![1-01-open-azure-portal.png](./images/1-01-open-azure-portal.png)

Na tela de recursos, digite **Evento** na barra de pesquisa e selecione **Hubs de evento** na lista suspensa:

![1-02-search-event-hubs.png](./images/1-02-search-event-hubs.png)

Clique em **Criar**:

![1-03-event-hub-create.png](./images/1-03-event-hub-create.png)

Se esta for a primeira vez que você cria um recurso no Azure, será necessário criar um novo **Grupo de recursos**. Se você já tiver um grupo de recursos, poderá selecioná-lo (ou criar um novo).

Selecionar **Criar novo**, nomeie o grupo `--demoProfileLdap---aep-enablement`.

![1-04-create-resource-group.png](./images/1-04-create-resource-group.png)

Complete o teste dos campos conforme indicado:

- Namespace : Defina seu namespace, ele deve ser exclusivo, use o seguinte padrão `--demoProfileLdap---aep-enablement`
- Localização: **Europa Ocidental** refere-se ao datacenter do Azure em Amsterdam
- Nível de preços: **Básico**
- Unidades de Taxa de Transferência: **1**

![1-05-create-namespace.png](./images/1-05-create-namespace.png)

Clique em **Revisar + criar**.

![1-06-namespace-review-create.png](./images/1-06-namespace-review-create.png)

Clique em **Criar**.

![1-07-namespace-create.png](./images/1-07-namespace-create.png)

A implantação do seu grupo de recursos pode levar de 1 a 2 minutos, quando for bem-sucedida, você verá a seguinte tela:

![1-08-namespace-deploy.png](./images/1-08-namespace-deploy.png)

## 13.1.3 Configurar seu Hub de Eventos no Azure

Ir para [https://portal.azure.com/#home](https://portal.azure.com/#home) e selecione **Todos os recursos**.

![1-09-all-resources.png](./images/1-09-all-resources.png)

Na lista de recursos, selecione o `--demoProfileLdap---aep-enablement` namespace:

![1-10-list-resources.png](./images/1-10-list-resources.png)

Em `--demoProfileLdap---aep-enablement` tela de detalhes, selecione **Hubs de evento**:

![1-11-eventhub-namespace.png](./images/1-11-eventhub-namespace.png)

Clique em **+ Hub de eventos**.

![1-12-add-event-hub.png](./images/1-12-add-event-hub.png)

Use `--demoProfileLdap---aep-enablement-event-hub` como o nome e clique em **Criar**.

![1-13-create-event-hub.png](./images/1-13-create-event-hub.png)

Clique em **Hubs de evento** no namespace do hub de eventos. Agora você deve ver seu **Hub de eventos** listado. Se for esse o caso, você pode passar para o próximo exercício.

![1-14-event-hub-list.png](./images/1-14-event-hub-list.png)

## 13.1.4 Configurar sua conta de armazenamento do Azure

Para depurar sua função do Hub de Eventos do Azure em exercícios posteriores, você precisará fornecer uma Conta de Armazenamento do Azure como parte da configuração do projeto do Visual Studio Code. Agora você criará essa Conta de Armazenamento do Azure.

Ir para [https://portal.azure.com/#home](https://portal.azure.com/#home) e selecione **Criar um recurso**.

![1-15-event-hub-storage.png](./images/1-15-event-hub-storage.png)

Enter **armazenamento** na pesquisa e selecione **Conta de armazenamento** na lista.

![1-16-event-hub-search-storage.png](./images/1-16-event-hub-search-storage.png)

Selecione **Criar**.

![1-17-event-hub-create-storage.png](./images/1-17-event-hub-create-storage.png)

Especifique seu **Grupo de recursos** (criado no início deste exercício), use `--demoProfileLdap--aepstorage` como o nome da conta de Armazenamento e selecione **Armazenamento local redundante (LRS)**, depois clique em **Revisar + criar**.

![1-18-event-hub-create-review-storage.png](./images/1-18-event-hub-create-review-storage.png)

Clique em **Criar**.

![1-19-event-hub-submit-storage.png](./images/1-19-event-hub-submit-storage.png)

A criação da Conta de Armazenamento levará alguns segundos:

![1-20-event-hub-deploy-storage.png](./images/1-20-event-hub-deploy-storage.png)

Quando terminar, a tela exibirá a variável **Ir para recurso** botão.

Clique em **Microsoft Azure**.

![1-21-event-hub-deploy-ready-storage.png](./images/1-21-event-hub-deploy-ready-storage.png)

Sua conta de armazenamento agora está visível em **Recursos recentes**.

![1-22-event-hub-deploy-resources-list.png](./images/1-22-event-hub-deploy-resources-list.png)

Próxima etapa: [13.2 Configurar o destino do Hub de eventos do Azure no Adobe Experience Platform](./ex2.md)

[Voltar ao Módulo 13](./segment-activation-microsoft-azure-eventhub.md)

[Voltar para todos os módulos](./../../overview.md)
