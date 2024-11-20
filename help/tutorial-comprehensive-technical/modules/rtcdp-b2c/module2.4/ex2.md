---
title: Ativação de segmento para o Hub de eventos do Microsoft Azure - Configurar o Hub de eventos no Azure
description: Ativação de segmento para o Hub de eventos do Microsoft Azure - Configurar o Hub de eventos no Azure
kt: 5342
doc-type: tutorial
exl-id: 0c2e94ec-00e8-4f47-add7-ca3a08151225
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 1%

---

# 2.4.2 Configurar o ambiente do Microsoft Azure EventHub

Os Hubs de Eventos do Azure são um serviço de assinatura de publicação altamente escalável que pode assimilar milhões de eventos por segundo e transmiti-los em vários aplicativos. Isso permite processar e analisar as grandes quantidades de dados produzidos por seus dispositivos e aplicativos conectados.

## O que são Hubs de Eventos do Azure?

Os Hubs de Eventos do Azure são uma plataforma de transmissão de big data e um serviço de assimilação de eventos. Ele pode receber e processar milhões de eventos por segundo. Os dados enviados para um hub de eventos podem ser transformados e armazenados usando qualquer provedor de análise em tempo real ou adaptadores de armazenamento/agrupamento.

Os Hubs de Eventos representam a **porta de entrada** para um pipeline de eventos, geralmente chamado de assimilador de eventos em arquiteturas de solução. Um assimilador de eventos é um componente ou serviço que se situa entre editores de eventos (como o Adobe Experience Platform RTCDP) e consumidores de eventos para dissociar a produção de um fluxo de eventos do consumo desses eventos. Os Hubs de eventos fornecem uma plataforma de transmissão unificada com buffer de retenção de tempo, dissociando os produtores de eventos dos consumidores de eventos.

## Criar um namespace de Hubs de Eventos

Vá para [https://portal.azure.com/#home](https://portal.azure.com/#home) e selecione **Criar um recurso**.

![1-01-open-azure-portal.png](./images/101openazureportal.png)

Na tela de recursos, digite **Event** na barra de pesquisa. Localize o cartão **Hubs de Eventos**, clique em **Criar** e em **Hubs de Eventos**.

![1-02-pesquisar-evento-hubs.png](./images/102searcheventhubs.png)

Se esta for a primeira vez que você cria um recurso no Azure, será necessário criar um novo **Grupo de recursos**. Se você já tiver um grupo de recursos, poderá selecioná-lo (ou criar um novo).

Clique em **Criar novo** e nomeie o grupo `--aepUserLdap---aep-enablement`, clique em **OK**.

![1-04-criar-grupo-recursos.png](./images/104createresourcegroup.png)

Preencha o restante dos campos conforme indicado:

- Namespace : defina seu namespace; ele deve ser exclusivo, use o seguinte padrão `--aepUserLdap---aep-enablement`
- Local: escolha qualquer local
- Camada de preços: **Básica**
- Unidades de Taxa de Transferência: **1**

Clique em **Revisar + criar**.

![1-05-criar-namespace.png](./images/105createnamespace.png)

Clique em **Criar**.

![1-07-namespace-create.png](./images/107namespacecreate.png)

A implantação do grupo de recursos pode levar de 1 a 2 minutos. Ao obter êxito, você verá a seguinte tela:

![1-08-namespace-deploy.png](./images/108namespacedeploy.png)

## Configurar o Hub de Eventos no Azure

Vá para [https://portal.azure.com/#home](https://portal.azure.com/#home) e selecione **Todos os recursos**.

![1-09-todos-os-recursos.png](./images/109allresources.png)

Na lista de recursos, clique no Namespace do Hub de Eventos `--aepUserLdap---aep-enablement`:

![1-10-list-resources.png](./images/110listresources.png)

Na tela de detalhes `--aepUserLdap---aep-enablement`, vá para **Entidades** e clique em **Hubs de Eventos**:

![1-11-eventub-namespace.png](./images/111eventhubnamespace.png)

Clique em **+ Hub de Eventos**.

![1-12-adicionar-hub-evento.png](./images/112addeventhub.png)

Use `--aepUserLdap---aep-enablement-event-hub` como nome e clique em **Revisar + Criar**.

![1-13-criar-hub-de-eventos.png](./images/113createeventhub.png)

Clique em **Criar**.

![1-13-criar-hub-de-eventos.png](./images/113createeventhub1.png)

Em **Hubs de Eventos** no namespace do hub de eventos, você verá seu **Hub de Eventos** listado.

![1-14-lista-hub-de-eventos.png](./images/114eventhublist.png)

## Configurar sua Conta de Armazenamento do Azure

Para depurar a função do Hub de Eventos do Azure em exercícios posteriores, será necessário fornecer uma Conta de Armazenamento do Azure como parte da configuração do projeto do Visual Studio Code. Agora você criará essa Conta de Armazenamento do Azure.

Vá para [https://portal.azure.com/#home](https://portal.azure.com/#home) e selecione **Criar um Recurso**.

![1-15-hub-armazenamento.png](./images/115eventhubstorage.png)

Insira a **conta de armazenamento** na pesquisa, localize o cartão da **Conta de Armazenamento** e clique em **Conta de armazenamento**.

![1-16-hub-de-eventos-pesquisa-armazenamento.png](./images/116eventhubsearchstorage.png)

Especifique o **Grupo de Recursos** (criado no início deste exercício), use `--aepUserLdap--aepstorage` como o nome da sua conta de Armazenamento e selecione **Armazenamento localmente redundante (LRS)** e clique em **Revisar + criar**.

![1-18-hub-de-eventos-criar-revisar-armazenamento.png](./images/118eventhubcreatereviewstorage.png)

Clique em **Criar**.

![1-19-hub-evento-enviar-armazenamento.png](./images/119eventhubsubmitstorage.png)

A criação da nossa conta de armazenamento levará alguns segundos:

![1-20-hub-de-eventos-implantar-armazenamento.png](./images/120eventhubdeploystorage.png)

Quando terminar, sua tela exibirá o botão **Ir para o recurso**.

Clique em **Página inicial**.

![1-21-hub-de-eventos-implantar-pronto-armazenamento.png](./images/121eventhubdeployreadystorage.png)

Sua Conta de Armazenamento agora está visível em **Recursos Recentes**.

![1-22-hub-implantação-recursos-lista.png](./images/122eventhubdeployresourceslist.png)

Próxima Etapa: [2.4.3 Configurar o Destino do Hub de Eventos do Azure no Adobe Experience Platform](./ex3.md)

[Voltar ao módulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Voltar a todos os módulos](./../../../overview.md)
