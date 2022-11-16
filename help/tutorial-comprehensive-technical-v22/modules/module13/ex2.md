---
title: Ativação de Segmento para o Hub de Eventos do Microsoft Azure - Configurar o destino RTCDP do Hub de Eventos no Adobe Experience Platform
description: Ativação de Segmento para o Hub de Eventos do Microsoft Azure - Configurar o destino RTCDP do Hub de Eventos no Adobe Experience Platform
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: b42b4ccb-1952-480b-b538-c1bd661e29eb
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# 13.2 Configurar o destino do Hub de eventos do Azure no Adobe Experience Platform

## 13.2.1 Identificar os parâmetros necessários da conexão do Azure

Para definir um destino de Hub de eventos no Adobe Experience Platform, você precisa de:

- Namespace dos Hubs de Eventos
- Hub de eventos
- Nome da chave SAS do Azure
- Chave SAS do Azure

O Event Hub e o namespace EventHub foram definidos no exercício anterior: [Exercício 1 - Configurar Hub de Eventos no Azure](./ex1.md)

### Namespace dos Hubs de Eventos

Para pesquisar as informações acima no Portal do Azure, navegue até [https://portal.azure.com/#home](https://portal.azure.com/#home). Certifique-se de que você esteja usando a conta correta do Azure.

Selecionar **Todos os recursos** no Portal do Azure:

![2-01-azure-all-resources.png](./images/2-01-azure-all-resources.png)

### Hub de eventos

Procurar um recurso com tipo de recurso **Namespace dos Hubs de Eventos**, se você seguiu as convenções de nomenclatura usadas no exercício anterior, o Namespace dos Hubs de Eventos será `--demoProfileLdap---aep-enablement`. Tome nota disso, você precisará dele no próximo exercício.

![2-02-select-event-hubs-namespace.png](./images/2-02-select-event-hubs-namespace.png)

Clique no nome do Namespace do Hubs de Eventos para obter os detalhes:

![2-03-select-event-hub.png](./images/2-03-select-event-hub.png)

Selecionar **Hubs de evento** para obter uma lista de Hubs de evento definidos no Namespace de Hubs de Evento, se você seguir as convenções de nomenclatura usadas no exercício anterior, você encontrará um Hub de Evento chamado `--demoProfileLdap---aep-enablement-event-hub`. Tome nota disso, você precisará dele no próximo exercício.

![2-04-event-hub-seleted.png](./images/2-04-event-hub-selected.png)

### Nome da chave SAS

Selecionar **Políticas de acesso compartilhadas** para seu **Namespace dos Hubs de Eventos**

![2-05-select-sas.png](./images/2-05-select-sas.png)

Você verá uma lista de Políticas de acesso compartilhadas. A chave SAS que estamos procurando é **RootManageSharedAccessKey**. Este é o nome da Chave SAS. Anote.

![2-06-sas-overview.png](./images/2-06-sas-overview.png)

### Valor-chave SAS

Clique no botão **RootManageSharedAccessKey** para obter o valor da chave SAS. E pressione a tecla **Copiar para a área de transferência** ícone para copiar o **Chave primária**:

![2-07-sas-key-value.png](./images/2-07-sas-key-value.png)

### Resumo dos valores de destino

Nesse ponto, você deve ter identificado todos os valores necessários para definir o destino do Hub de eventos do Azure na CDP em tempo real do Adobe Experience Platform.

| Nome do atributo de destino | Valor do atributo de destino | Exemplo de valor |
|---|---|---|
| sasKeyName | Nome da chave SAS | RootManageSharedAccessKey |
| sasKey | Valor-chave SAS | srREx9ShJG1Rv7f/... |
| namespace | Namespace dos Hubs de Eventos | `--demoProfileLdap---aep-enablement` |
| eventHubName | Hub de eventos | `--demoProfileLdap---aep-enablement-event-hub` |

## 13.2.2 Criar destino de Hub de Eventos do Azure no Adobe Experience Platform

Faça logon no Adobe Experience Platform acessando este URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer logon, você será direcionado para a página inicial do Adobe Experience Platform.

![Assimilação de dados](../module2/images/home.png)

Antes de continuar, é necessário selecionar um **sandbox**. A sandbox a ser selecionada é chamada de ``--aepSandboxId--``. Você pode fazer isso clicando no texto **[!UICONTROL Produto de produção]** na linha azul na parte superior da tela. Depois de selecionar a sandbox apropriada, você verá a tela mudar e agora estará na sandbox dedicada.

![Assimilação de dados](../module2/images/sb1.png)

Ir para **Destinos**, em seguida, vá para **Catálogo**.

![Assimilação de dados](./images/sb2a.png)

Selecionar **Armazenamento na nuvem** e ir para **Hubs de Eventos do Azure** e clique em **Configurar** ou **Configurar**:

![2-08-list-destination.png](./images/2-08-list-destinations.png)

Preencha os valores de destino coletados no exercício anterior. Em seguida, clique em **Conectar ao destino**.

![2-09-destination-values.png](./images/2-09-destination-values.png)

Se suas credenciais estiverem corretas, você verá uma confirmação: **Conectado**.

![2-09-destination-values.png](./images/2-09-destination-valuesa.png)

Agora é necessário inserir o nome e a descrição no formato `--demoProfileLdap---aep-enablement`. Insira o **eventHubName** (ver exercício anterior, tem esta aparência: `--demoProfileLdap---aep-enablement-event-hub`) e clique em **Próximo**.

![2-10-create-destination.png](./images/2-10-create-destination.png)

Clique em **Salvar e sair**.

![2-11-save-exit-ativation.png](./images/2-11-save-exit-activation.png)

Seu destino agora é criado e está disponível no Adobe Experience Platform.

![2-12-destination-created.png](./images/2-12-destination-created.png)

Próxima etapa: [13.3 Criar um segmento](./ex3.md)

[Voltar ao Módulo 13](./segment-activation-microsoft-azure-eventhub.md)

[Voltar para todos os módulos](./../../overview.md)
