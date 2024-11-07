---
title: Ativação de segmento para o Hub de eventos do Microsoft Azure - Configurar o destino RTCDP do Hub de eventos no Adobe Experience Platform
description: Ativação de segmento para o Hub de eventos do Microsoft Azure - Configurar o destino RTCDP do Hub de eventos no Adobe Experience Platform
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# 2.4.2 Configurar o destino do Hub de eventos do Azure no Adobe Experience Platform

## 2.4.2.1 Identificar parâmetros de Conexão do Azure necessários

Para definir um destino de Hub de eventos no Adobe Experience Platform, você precisa de:

- Namespace dos Hubs de Eventos
- Hub de eventos
- Nome da chave SAS do Azure
- Chave SAS do Azure

O Hub de Eventos e o namespace EventHub foram definidos no exercício anterior: [Exercício 1 - Configurar Hub de Eventos no Azure](./ex1.md)

### Namespace dos Hubs de Eventos

Para pesquisar as informações acima no Portal do Azure, navegue até [https://portal.azure.com/#home](https://portal.azure.com/#home). Verifique se você está usando a conta correta do Azure.

Selecione **Todos os Recursos** no Portal do Azure:

![2-01-azure-all-resources.png](./images/2-01-azure-all-resources.png)

### Hub de eventos

Procure um recurso com o tipo de recurso **Namespace dos Hubs de Eventos**. Se você seguir as convenções de nomenclatura usadas no exercício anterior, o Namespace dos Hubs de Eventos será `--aepUserLdap---aep-enablement`. Anote-o, você precisará dele no próximo exercício.

![2-02-select-event-hubs-namespace.png](./images/2-02-select-event-hubs-namespace.png)

Clique no nome do Namespace dos Hubs de Eventos para obter os detalhes:

![2-03-select-event-hub.png](./images/2-03-select-event-hub.png)

Selecione **Hubs de Eventos** para obter uma lista de Hubs de Eventos definidos no Namespace de Hubs de Eventos. Caso tenha seguido as convenções de nomenclatura usadas no exercício anterior, você encontrará um Hub de Eventos chamado `--aepUserLdap---aep-enablement-event-hub`. Anote-o, você precisará dele no próximo exercício.

![2-04-hub-de-eventos-seleted.png](./images/2-04-event-hub-selected.png)

### Nome da chave SAS

Selecione **Políticas de acesso compartilhado** para seu **Namespace de Hubs de Eventos**

![2-05-select-sas.png](./images/2-05-select-sas.png)

Você verá uma lista de Políticas de acesso compartilhado. A Chave SAS que estamos procurando é **RootManageSharedAccessKey**. Este é o nome da chave SAS. Anote isso.

![2-06-sas-overview.png](./images/2-06-sas-overview.png)

### Valor da chave SAS

Clique em **RootManageSharedAccessKey** para obter o Valor da Chave SAS. E pressione o ícone **Copiar para a área de transferência** para copiar a **Chave primária**:

![2-07-sas-key-value.png](./images/2-07-sas-key-value.png)

### Resumo dos valores de destino

Neste ponto, você deve ter identificado todos os valores necessários para definir o destino do Azure Event Hub na CDP em tempo real do Adobe Experience Platform.

| Nome do atributo de destino | Valor do atributo de destino | Exemplo de valor |
|---|---|---|
| sasKeyName | Nome da chave SAS | RootManageSharedAccessKey |
| sasKey | Valor da chave SAS | srREx9ShJG1Rv7f/... |
| namespace | Namespace dos Hubs de Eventos | `--aepUserLdap---aep-enablement` |
| eventHubName | Hub de eventos | `--aepUserLdap---aep-enablement-event-hub` |

## 2.4.2.2 Criar destino do Hub de eventos do Azure no Adobe Experience Platform

Faça logon no Adobe Experience Platform acessando esta URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepSandboxName--``. Você pode fazer isso clicando no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. Depois de selecionar a sandbox apropriada, você verá a alteração da tela e agora estará em sua sandbox dedicada.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/sb1.png)

Vá para **Destinos** e vá para **Catálogo**.

![Assimilação de dados](./images/sb2a.png)

Selecione **Armazenamento na Nuvem**, vá para **Hubs de Eventos do Azure** e clique em **Configurar** ou **Configurar**:

![2-08-list-destinations.png](./images/2-08-list-destinations.png)

Preencha os valores de destino coletados no exercício anterior. Em seguida, clique em **Conectar ao Destino**.

![2-09-destination-values.png](./images/2-09-destination-values.png)

Se suas credenciais estiverem corretas, você verá uma confirmação: **Conectado**.

![2-09-destination-values.png](./images/2-09-destination-valuesa.png)

Agora é necessário inserir o nome e a descrição no formato `--aepUserLdap---aep-enablement`. Insira o **eventHubName** (veja o exercício anterior, ele tem a seguinte aparência: `--aepUserLdap---aep-enablement-event-hub`) e clique em **Avançar**.

![2-10-criar-destino.png](./images/2-10-create-destination.png)

Clique em **Salvar e sair**.

![2-11-save-exit-ativation.png](./images/2-11-save-exit-activation.png)

Seu destino foi criado e está disponível no Adobe Experience Platform.

![2-12-destination-created.png](./images/2-12-destination-created.png)

Próxima Etapa: [2.4.3 Criar um segmento](./ex3.md)

[Voltar ao módulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Voltar a todos os módulos](./../../../overview.md)
