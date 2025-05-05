---
title: Audience Activation para o Hub de eventos do Microsoft Azure - definir uma função do Azure
description: Audience Activation para o Hub de eventos do Microsoft Azure - definir uma função do Azure
kt: 5342
doc-type: tutorial
exl-id: 2ce9dcfc-4b2c-48b4-b554-8a30abb850f3
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# 2.4.6 Criar seu projeto do Microsoft Azure

## Familiarizando-se com as funções do Azure Event Hub

As Funções do Azure permitem executar pequenos pedaços de código (chamados **funções**) sem se preocupar com a infraestrutura do aplicativo. Com as Funções do Azure, a infraestrutura em nuvem fornece todos os servidores atualizados necessários para manter seu aplicativo em execução em escala.
Uma função é **acionada** por um tipo específico de evento. Os acionadores compatíveis incluem responder a alterações nos dados, responder a mensagens (por exemplo, Hubs de Eventos), executadas em uma programação ou como o resultado de uma solicitação HTTP.
As Funções do Azure são um serviço de computação sem servidor que permite executar código acionado por eventos sem precisar provisionar ou gerenciar explicitamente a infraestrutura.
Os Hubs de Eventos do Azure se integram às Funções do Azure para uma arquitetura sem servidor.

## Abrir código do Visual Studio e fazer logon no Azure

O Visual Studio Code facilita...
- definir e vincular funções do Azure aos Hubs de Eventos- testar localmente- implantar no Azure- execução da função de log remoto

### Abrir Visual Studio Code

### Fazer logon no Azure

Ao fazer logon com sua conta do Azure usada para registrar no exercício anterior, o Visual Studio Code permitirá localizar e vincular todos os recursos do Hub de Eventos.
Abra o Visual Studio Code e clique no ícone **Azure**.
Próxima seleção **Entrar no Azure**:
![3-01-vsc-open.png](./images/301vscopen.png)
Você será redirecionado ao seu navegador para fazer logon. Lembre-se de selecionar a conta do Azure que você usou para registrar.
Ao ver a tela a seguir no navegador, você está conectado com o Visual Code Studio:
![3-03-vsc-login-ok.png](./images/303vscloginok.png)
Retorne ao Visual Code Studio (você verá o nome da sua assinatura do Azure, por exemplo **Assinatura do Azure 1**):
![3-04-vsc-logged-in.png](./images/304vscloggedin.png)

## Criar um projeto do Azure

Clique em **Criar projeto de função...**:
![3-05-vsc-create-project.png](./images/vsc2.png)
Selecione ou crie uma pasta local de sua escolha para salvar o projeto e clique em **Selecionar**:
![3-06-vsc-select-folder.png](./images/vsc3.png)
Agora você entrará no assistente de criação de projeto. Clique em **Javascript** como a linguagem do projeto:
![3-07-vsc-select-language.png](./images/vsc4.png)
Em seguida, selecione **Modelo v4**.
![3-07-vsc-select-language.png](./images/vsc4a.png)
Selecione **Acionador do Hub de Eventos do Azure** como o primeiro modelo de função do seu projeto:
![3-08-vsc-function-template.png](./images/vsc5.png)
Digite um nome para a função, use o seguinte formato `--aepUserLdap---aep-event-hub-trigger` e pressione enter:
![3-09-vsc-function-name.png](./images/vsc6.png)
Selecione **Criar nova configuração de aplicativo local**:
![3-10-vsc-function-local-app-setting.png](./images/vsc7.png)
Clique para selecionar o Namespace do Hub de Eventos que você criou anteriormente, que se chama `--aepUserLdap---aep-enablement`.
![3-11-vsc-function-select-namespace.png](./images/vsc8.png)
Em seguida, clique para selecionar o Hub de Eventos criado anteriormente, chamado `--aepUserLdap---aep-enablement-event-hub`.
![3-12-vsc-function-select-eventub.png](./images/vsc9.png)
Clique para selecionar **RootManageSharedAccessKey** como sua política do Hub de Eventos:
![3-13-vsc-function-select-eventub-policy.png](./images/vsc10.png)
Selecione **Adicionar ao espaço de trabalho** para saber como abrir seu projeto:
![3-15-vsc-project-add-to-workspace.png](./images/vsc12.png)
Você pode então receber uma mensagem como esta. Nesse caso, clique em **Sim, eu confio nos autores**.
![3-15-vsc-project-add-to-workspace.png](./images/vsc12a.png)
Após criar o projeto, abra o arquivo `--aepUserLdap---aep-event-hub-trigger.js` no editor:
![3-16-vsc-open-index-js.png](./images/vsc13.png)
A carga enviada pelo Adobe Experience Platform para o Hub de eventos será semelhante a:

```json
{
  "identityMap": {
    "ecid": [
      {
        "id": "36281682065771928820739672071812090802"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "94db5aed-b90e-478d-9637-9b0fad5bba11": {
        "createdAt": 1732129904025,
        "lastQualificationTime": "2024-11-21T07:33:52Z",
        "mappingCreatedAt": 1732130611000,
        "mappingUpdatedAt": 1732130611000,
        "name": "vangeluw - Interest in Plans",
        "status": "realized",
        "updatedAt": 1732129904025
      }
    }
  }
}
```

Atualize o código em seu `--aepUserLdap---aep-event-hub-trigger.js` do Visual Studio Code com o código abaixo. Esse código será executado sempre que a Real-time CDP enviar qualificações de público-alvo para o destino do Hub de eventos. Neste exemplo, o código é apenas para exibir a carga útil recebida, mas você pode imaginar qualquer tipo de função adicional para processar as qualificações do público-alvo em tempo real e usar o ecossistema do pipeline de dados.
A linha 11 no seu arquivo `--aepUserLdap---aep-event-hub-trigger.js` atualmente mostra isto:

```javascript
context.log('Event hub message:', message);
```

Altere a linha 11 em `--aepUserLdap---aep-event-hub-trigger.js` para que tenha esta aparência:

```javascript
context.log('Event hub message:', JSON.stringify(message));
```

A carga útil total deve ser desta forma:

```javascript
const { app } = require('@azure/functions');

app.eventHub('--aepUserLdap---aep-event-hub-trigger', {
    connection: '--aepUserLdap--aepenablement_RootManageSharedAccessKey_EVENTHUB',
    eventHubName: '--aepUserLdap---aep-enablement-event-hub',
    cardinality: 'many',
    handler: (messages, context) => {
        if (Array.isArray(messages)) {
            context.log(`Event hub function processed ${messages.length} messages`);
            for (const message of messages) {
                context.log('Event hub message:', message);
            }
        } else {
            context.log('Event hub function processed message:', messages);
        }
    }
});
```


O resultado deve ficar assim:
![3-16b-vsc-edit-index-js.png](./images/vsc1.png)

## Executar projeto do Azure

Agora é hora de executar o projeto. Nesta etapa, não implantaremos o projeto no Azure. Vamos executá-lo localmente no modo de depuração. Selecione o ícone Executar e clique na seta verde.
![3-17-vsc-run-project.png](./images/vsc14.png)
Na primeira vez que você executar seu projeto no modo de depuração, precisará anexar uma conta de armazenamento do Azure, clique em **Selecionar conta de armazenamento**.
![3-17-vsc-run-project.png](./images/vsc14a.png)
e selecione a conta de armazenamento criada anteriormente, chamada `--aepUserLdap--aepstorage`.
![3-17-vsc-run-project.png](./images/vsc14b.png)
Seu projeto está em execução e está listando eventos no Hub de eventos. No próximo exercício, você demonstrará o comportamento no site de demonstração do CitiSignal que o qualificará para públicos-alvo. Como resultado, você receberá uma carga de qualificação de público-alvo no terminal da função de acionador do Hub de eventos.
![3-24-vsc-application-stop.png](./images/vsc18.png)

## Parar Projeto do Azure

Para interromper o projeto, vá para a **PILHA DE CHAMADAS** no VSC, clique na seta do projeto em execução e clique em **Parar**.
![3-24-vsc-application-stop.png](./images/vsc17.png)

## Próximas etapas

Ir para [2.4.7 Cenário completo](./ex7.md){target="_blank"}
Voltar para [Real-Time CDP: Audience Activation para o Hub de Eventos do Microsoft Azure](./segment-activation-microsoft-azure-eventhub.md){target="_blank"}
Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
