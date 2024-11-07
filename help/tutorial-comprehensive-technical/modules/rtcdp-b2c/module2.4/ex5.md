---
title: Ativação de segmento para o Hub de eventos do Microsoft Azure - defina uma função do Azure
description: Ativação de segmento para o Hub de eventos do Microsoft Azure - defina uma função do Azure
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 0%

---

# 2.4.5 Criar seu projeto do Microsoft Azure

## 2.4.5.1 Familiarizando-se com as funções do Hub de eventos do Azure

O Azure Functions permite executar pequenos pedaços de código (chamados de **funções**) sem se preocupar com a infraestrutura do aplicativo. Com as Funções do Azure, a infraestrutura em nuvem fornece todos os servidores atualizados necessários para manter seu aplicativo em execução em escala.

Uma função é **acionada** por um tipo específico de evento. Os acionadores compatíveis incluem responder a alterações nos dados, responder a mensagens (por exemplo, Hubs de Eventos), executadas em uma programação ou como o resultado de uma solicitação HTTP.

As Funções do Azure são um serviço de computação sem servidor que permite executar código acionado por eventos sem precisar provisionar ou gerenciar explicitamente a infraestrutura.

Os Hubs de Eventos do Azure se integram às Funções do Azure para uma arquitetura sem servidor.

## 2.4.5.2 Abrir o Visual Studio Code e fazer logon no Azure

O Visual Studio Code facilita...

- definir e vincular funções do Azure aos Hubs de Eventos
- testar localmente
- implantar no Azure
- execução da função de log remoto

### Abrir Visual Studio Code

Para abrir o Visual Studio Code, digite **visual** na pesquisa do seu sistema operacional (pesquisa Spotlight no OSX, pesquisa na Barra de Tarefas do Windows). Se não o encontrar, você precisará repetir as etapas descritas em [Exercício 0 - Pré-requisitos](./ex0.md).

![visual-studio-code-icon.png](./images/visual-studio-code-icon.png)

### Fazer logon no Azure

Ao fazer logon com sua conta do Azure que você usou para registrar no [Exercício 0 - Pré-requisitos](./ex0.md), o Visual Studio Code permitirá localizar e associar todos os recursos do Hub de Eventos.

Clique no ícone do **Azure** no Visual Studio Code. Se você não tiver essa opção, algo pode ter dado errado com a instalação das extensões necessárias.

Próxima seleção **Entrar no Azure**:

![3-01-vsc-open.png](./images/3-01-vsc-open.png)

Você será redirecionado ao seu navegador para fazer logon. Lembre-se de selecionar a conta do Azure que você usou para registrar.

![3-02-vsc-pick-account.png](./images/3-02-vsc-pick-account.png)

Ao ver a tela a seguir no navegador, você está conectado com o Visual Code Studio:

![3-03-vsc-login-ok.png](./images/3-03-vsc-login-ok.png)

Retorne ao Visual Code Studio (você verá o nome da sua assinatura do Azure, por exemplo **Assinatura do Azure 1**):

![3-04-vsc-logged-in.png](./images/3-04-vsc-logged-in.png)

## 2.4.5.3 Criar um projeto do Azure

Quando você passar o mouse sobre a **Assinatura do Azure 1**, um menu será exibido acima da seção, selecione **Criar novo projeto...**:

![3-05-vsc-create-project.png](./images/vsc2.png)

Selecione uma pasta local de sua escolha para salvar o projeto e clique em **Selecionar**:

![3-06-vsc-select-folder.png](./images/vsc3.png)

Agora você entrará no assistente de criação de projeto. Selecione **Javascript** como o idioma do projeto:

![3-07-vsc-select-language.png](./images/vsc4.png)

Selecione **Acionador do Hub de Eventos do Azure** como o primeiro modelo de função do seu projeto:

![3-08-vsc-function-template.png](./images/vsc5.png)

Digite um nome para a função, use o seguinte formato `--aepUserLdap---aep-event-hub-trigger` e pressione enter:

![3-09-vsc-function-name.png](./images/vsc6.png)

Selecione **Criar nova configuração de aplicativo local**:

![3-10-vsc-function-local-app-setting.png](./images/vsc7.png)

Selecione um namespace de hub de eventos. Você deve ver o Hub de Eventos definido no **Exercício 2**. Neste exemplo, o namespace do Hub de Eventos é **vangeluw-aep-enablement**:

![3-11-vsc-function-select-namespace.png](./images/vsc8.png)

Selecione seu Hub de Eventos. Você deve ver o Hub de Eventos que você definiu no **Exercício 2**. No meu caso, que é **vangeluw-aep-enablement-event-hub**:

![3-12-vsc-function-select-eventub.png](./images/vsc9.png)

Selecione **RootManageSharedAccessKey** como sua política do Hub de Eventos:

![3-13-vsc-function-select-eventub-policy.png](./images/vsc10.png)

Digite para usar o **$Padrão**:

![3-14-vsc-eventub-consumer-group.png](./images/vsc11.png)

Selecione **Adicionar ao espaço de trabalho** para saber como abrir seu projeto:

![3-15-vsc-project-add-to-workspace.png](./images/vsc12.png)

Após criar o projeto, clique em **index.js** para abrir o arquivo no editor:

![3-16-vsc-open-index-js.png](./images/vsc13.png)

A carga enviada pelo Adobe Experience Platform para o seu Hub de eventos incluirá as IDs de segmento:

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

Substitua o código no index.js do Visual Studio Code pelo código abaixo. Esse código será executado sempre que a Real-time CDP enviar qualificações de segmento para o destino do Hub de eventos. No nosso exemplo, o código é apenas sobre exibição e aprimoramento da carga útil recebida. Mas você pode imaginar qualquer tipo de função para processar qualificações de segmento em tempo real.

```javascript
// Marc Meewis - Solution Consultant Adobe - 2020
// Adobe Experience Platform Enablement - Module 13

// Main function
// -------------
// This azure function is fired for each segment activated to the Adobe Exeperience Platform Real-time CDP Azure 
// Eventhub destination
// This function enriched the received segment payload with the name fo the segment. 
// You can replace this function with any logic that is require to process and deliver
// Adobe Experience Platform segments in real-time to any application or platform that 
// would need to act upon an AEP segment qualiification.
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

## 2.4.5.4 Executar projeto do Azure

Agora é hora de executar o projeto. Nesta etapa, não implantaremos o projeto no Azure. Vamos executá-lo localmente no modo de depuração. Selecione o ícone Executar e clique na seta verde.

![3-17-vsc-run-project.png](./images/vsc14.png)

Na primeira vez que você executar seu projeto no modo de depuração, precisará anexar uma conta de armazenamento do Azure, clique em **Selecionar conta de armazenamento**.

![3-17-vsc-run-project.png](./images/vsc15.png)

Na lista de contas de armazenamento, selecione aquela que você criou como parte da [13.1.4 Configurar sua Conta de Armazenamento do Azure](./ex1.md). Sua conta de armazenamento é chamada `--aepUserLdap--aepstorage`, por exemplo: **mmeewisaepstorage**.

![3-22-vsc-select-storage-account.png](./images/vsc16.png)

Seu projeto está em execução e está listando eventos no Hub de eventos. No próximo exercício, você demonstrará o comportamento no site de demonstração da Luma que irá qualificá-lo para esses segmentos. Como resultado, você receberá uma carga de qualificação de segmento no terminal da função de acionador do Hub de eventos:

![3-23-vsc-application-started.png](./images/vsc17.png)

## 2.4.5.5 Interromper projeto do Azure

Para interromper o projeto, selecione a guia **Terminal**, clique na janela do terminal e pressione **CMD-C** no OSX ou **CTRL-C** no Windows:

![3-24-vsc-application-stop.png](./images/vsc18.png)

Próxima Etapa: [2.4.6 Cenário completo](./ex6.md)

[Voltar ao módulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Voltar a todos os módulos](./../../../overview.md)
