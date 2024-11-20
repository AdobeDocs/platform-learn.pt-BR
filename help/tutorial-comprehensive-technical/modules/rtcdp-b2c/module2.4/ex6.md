---
title: Audience Activation para o Hub de eventos do Microsoft Azure - defina uma função do Azure
description: Audience Activation para o Hub de eventos do Microsoft Azure - defina uma função do Azure
kt: 5342
doc-type: tutorial
exl-id: c39fea54-98ec-45c3-a502-bcf518e6fd06
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '723'
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

- definir e vincular funções do Azure aos Hubs de Eventos
- testar localmente
- implantar no Azure
- execução da função de log remoto

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

Selecione uma pasta local de sua escolha para salvar o projeto e clique em **Selecionar**:

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

Após criar o projeto, clique em **index.js** para abrir o arquivo no editor:

![3-16-vsc-open-index-js.png](./images/vsc13.png)

A carga enviada pelo Adobe Experience Platform para o seu Hub de eventos incluirá as IDs de público-alvo:

```json
[{
"segmentMembership": {
"ups": {
"ca114007-4122-4ef6-a730-4d98e56dce45": {
"lastQualificationTime": "2020-08-31T10:59:43Z",
"status": "realized"
},
"be2df7e3-a6e3-4eb4-ab12-943a4be90837": {
"lastQualificationTime": "2020-08-31T10:59:56Z",
"status": "realized"
},
"39f0feef-a8f2-48c6-8ebe-3293bc49aaef": {
"lastQualificationTime": "2020-08-31T10:59:56Z",
"status": "realized"
}
}
},
"identityMap": {
"ecid": [{
"id": "08130494355355215032117568021714632048"
}]
}
}]
```

Substitua o código no index.js do Visual Studio Code pelo código abaixo. Esse código será executado sempre que a Real-time CDP enviar qualificações de público-alvo para o destino do Hub de eventos. No nosso exemplo, o código é apenas sobre exibição e aprimoramento da carga útil recebida. Mas você pode imaginar qualquer tipo de função para processar qualificações de público em tempo real.

```javascript
// Marc Meewis - Solution Consultant Adobe - 2020
// Adobe Experience Platform Enablement - Module 2.4

// Main function
// -------------
// This azure function is fired for each audience activated to the Adobe Exeperience Platform Real-time CDP Azure 
// Eventhub destination
// This function enriched the received audience payload with the name of the audience. 
// You can replace this function with any logic that is require to process and deliver
// Adobe Experience Platform audiences in real-time to any application or platform that 
// would need to act upon an AEP audience qualification.
// 

module.exports = async function (context, eventHubMessages) {

    return new Promise (function (resolve, reject) {

        context.log('Message : ' + JSON.stringify(eventHubMessages, null, 2));

        resolve();

    });    

};
```

O resultado deve ficar assim:

![3-16b-vsc-edit-index-js.png](./images/vsc1.png)

## Executar projeto do Azure

Agora é hora de executar o projeto. Nesta etapa, não implantaremos o projeto no Azure. Vamos executá-lo localmente no modo de depuração. Selecione o ícone Executar e clique na seta verde.

![3-17-vsc-run-project.png](./images/vsc14.png)

Na primeira vez que você executar o projeto no modo de depuração, precisará anexar uma conta de armazenamento do Azure, clicar em **Selecionar conta de armazenamento** e selecionar a conta de armazenamento criada anteriormente, chamada de `--aepUserLdap--aepstorage`.

Seu projeto está em execução e está listando eventos no Hub de eventos. No próximo exercício, você demonstrará o comportamento no site de demonstração do CitiSignal que o qualificará para públicos-alvo. Como resultado, você receberá uma carga de qualificação de público-alvo no terminal da função de acionador do Hub de eventos.

![3-24-vsc-application-stop.png](./images/vsc18.png)

## Parar Projeto do Azure

Para interromper o projeto, vá para a **PILHA DE CHAMADAS** no VSC, clique na seta do projeto em execução e clique em **Parar**.

![3-24-vsc-application-stop.png](./images/vsc17.png)

Próxima Etapa: [2.4.7 Cenário completo](./ex7.md)

[Voltar ao módulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Voltar a todos os módulos](./../../../overview.md)
