---
title: Ativação de segmento para o Hub de eventos do Microsoft Azure - Configurar o Hub de eventos no Azure
description: Ativação de segmento para o Hub de eventos do Microsoft Azure - Configurar o Hub de eventos no Azure
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 1%

---

# 2.4.1 Configurar o ambiente do Microsoft Azure EventHub

Os Hubs de Eventos do Azure são um serviço de assinatura de publicação altamente escalável que pode assimilar milhões de eventos por segundo e transmiti-los em vários aplicativos. Isso permite processar e analisar as grandes quantidades de dados produzidos por seus dispositivos e aplicativos conectados.

## 2.4.1.1 O que são os Hubs de Eventos do Azure?

Os Hubs de Eventos do Azure são uma plataforma de transmissão de big data e um serviço de assimilação de eventos. Ele pode receber e processar milhões de eventos por segundo. Os dados enviados para um hub de eventos podem ser transformados e armazenados usando qualquer provedor de análise em tempo real ou adaptadores de armazenamento/agrupamento.

Os Hubs de Eventos representam a **porta de entrada** para um pipeline de eventos, geralmente chamado de assimilador de eventos em arquiteturas de solução. Um assimilador de eventos é um componente ou serviço que se situa entre editores de eventos (como o Adobe Experience Platform RTCDP) e consumidores de eventos para dissociar a produção de um fluxo de eventos do consumo desses eventos. Os Hubs de eventos fornecem uma plataforma de transmissão unificada com buffer de retenção de tempo, dissociando os produtores de eventos dos consumidores de eventos.

## 2.4.1.2 Criar um namespace de Hubs de eventos

Vá para [https://portal.azure.com/#home](https://portal.azure.com/#home) e selecione **Criar um recurso**.

![1-01-open-azure-portal.png](./images/1-01-open-azure-portal.png)

Na tela de recursos, digite **Event** na barra de pesquisa e selecione **Hubs de Eventos** na lista suspensa:

![1-02-pesquisar-evento-hubs.png](./images/1-02-search-event-hubs.png)

Clique em **Criar**:

![1-03-hub-de-eventos-create.png](./images/1-03-event-hub-create.png)

Se esta for a primeira vez que você cria um recurso no Azure, será necessário criar um novo **Grupo de recursos**. Se você já tiver um grupo de recursos, poderá selecioná-lo (ou criar um novo).

Selecione **Criar novo**, nomeie o grupo `--aepUserLdap---aep-enablement`.

![1-04-criar-grupo-recursos.png](./images/1-04-create-resource-group.png)

Complete o teste dos campos conforme indicado:

- Namespace : defina seu namespace; ele deve ser exclusivo, use o seguinte padrão `--aepUserLdap---aep-enablement`
- Local: **Europa Ocidental** refere-se ao datacenter do Azure em Amsterdã
- Camada de preços: **Básica**
- Unidades de Taxa de Transferência: **1**

![1-05-criar-namespace.png](./images/1-05-create-namespace.png)

Clique em **Revisar + criar**.

![1-06-namespace-review-create.png](./images/1-06-namespace-review-create.png)

Clique em **Criar**.

![1-07-namespace-create.png](./images/1-07-namespace-create.png)

A implantação do grupo de recursos pode levar de 1 a 2 minutos. Ao obter êxito, você verá a seguinte tela:

![1-08-namespace-deploy.png](./images/1-08-namespace-deploy.png)

## 2.4.1.3 Configurar o Hub de Eventos no Azure

Vá para [https://portal.azure.com/#home](https://portal.azure.com/#home) e selecione **Todos os recursos**.

![1-09-todos-os-recursos.png](./images/1-09-all-resources.png)

Na lista de recursos, selecione seu namespace `--aepUserLdap---aep-enablement`:

![1-10-list-resources.png](./images/1-10-list-resources.png)

Na tela de detalhes `--aepUserLdap---aep-enablement`, selecione **Hubs de Eventos**:

![1-11-eventub-namespace.png](./images/1-11-eventhub-namespace.png)

Clique em **+ Hub de Eventos**.

![1-12-adicionar-hub-evento.png](./images/1-12-add-event-hub.png)

Use `--aepUserLdap---aep-enablement-event-hub` como nome e clique em **Criar**.

![1-13-criar-hub-de-eventos.png](./images/1-13-create-event-hub.png)

Clique em **Hubs de Eventos** no namespace do hub de eventos. Agora você deve ver seu **Hub de Eventos** listado. Se esse for o caso, você poderá seguir para o próximo exercício.

![1-14-lista-hub-de-eventos.png](./images/1-14-event-hub-list.png)

## 2.4.1.4 Configurar sua conta de armazenamento do Azure

Para depurar a função do Hub de Eventos do Azure em exercícios posteriores, será necessário fornecer uma Conta de Armazenamento do Azure como parte da configuração do projeto do Visual Studio Code. Agora você criará essa Conta de Armazenamento do Azure.

Vá para [https://portal.azure.com/#home](https://portal.azure.com/#home) e selecione **Criar um Recurso**.

![1-15-hub-armazenamento.png](./images/1-15-event-hub-storage.png)

Insira **armazenamento** na pesquisa e selecione **Conta de Armazenamento** na lista.

![1-16-hub-de-eventos-pesquisa-armazenamento.png](./images/1-16-event-hub-search-storage.png)

Selecione **Criar**.

![1-17-hub-de-eventos-criar-armazenamento.png](./images/1-17-event-hub-create-storage.png)

Especifique o **Grupo de Recursos** (criado no início deste exercício), use `--aepUserLdap--aepstorage` como o nome da sua conta de Armazenamento e selecione **Armazenamento localmente redundante (LRS)** e clique em **Revisar + criar**.

![1-18-hub-de-eventos-criar-revisar-armazenamento.png](./images/1-18-event-hub-create-review-storage.png)

Clique em **Criar**.

![1-19-hub-evento-enviar-armazenamento.png](./images/1-19-event-hub-submit-storage.png)

A criação da Conta de Armazenamento levará alguns segundos:

![1-20-hub-de-eventos-implantar-armazenamento.png](./images/1-20-event-hub-deploy-storage.png)

Quando terminar, sua tela exibirá o botão **Ir para o recurso**.

Clique em **Microsoft Azure**.

![1-21-hub-de-eventos-implantar-pronto-armazenamento.png](./images/1-21-event-hub-deploy-ready-storage.png)

Sua Conta de Armazenamento agora está visível em **Recursos Recentes**.

![1-22-hub-implantação-recursos-lista.png](./images/1-22-event-hub-deploy-resources-list.png)

Próxima Etapa: [2.4.2 Configurar o Destino do Hub de Eventos do Azure no Adobe Experience Platform](./ex2.md)

[Voltar ao módulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Voltar a todos os módulos](./../../../overview.md)
