---
title: Ativação de Segmento para o Hub de Eventos do Microsoft Azure - Definir uma função do Azure
description: Ativação de Segmento para o Hub de Eventos do Microsoft Azure - Definir uma função do Azure
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: b4a76dbc-bcea-47f6-bee3-889982f26ba8
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 0%

---

# 13.5 Criar o projeto do Microsoft Azure

## 13.5.1 Conhecimento das funções do Hub de Eventos do Azure

As Funções do Azure permitem executar pequenos pedaços de código (chamados de **funções**) sem se preocupar com a infraestrutura de aplicativos. Com as Funções do Azure, a infraestrutura de nuvem fornece todos os servidores atualizados necessários para manter o aplicativo em execução em escala.

Uma função é **acionado** por um tipo específico de evento. Os acionadores compatíveis incluem responder a alterações nos dados, responder a mensagens (por exemplo, Hubs de Eventos), executar de acordo com um agendamento ou como resultado de uma solicitação HTTP.

As Funções do Azure são um serviço de computação sem servidor que permite executar código acionado pelo evento sem precisar provisionar ou gerenciar explicitamente a infraestrutura.

O Hubs de Eventos do Azure integra-se às Funções do Azure para uma arquitetura sem servidor.

## 13.5.2 Abra o código do Visual Studio e faça logon no Azure

O Visual Studio Code facilita...

- definir e vincular as funções do Azure aos Hubs de Eventos
- testar localmente
- implantar no Azure
- execução da função de log remoto

### Abrir código do Visual Studio

Para abrir o Visual Studio Code, digite **visual** na pesquisa do seu sistema operacional (Pesquisa em destaque no OSX, Pesquisa na barra de tarefas do Windows). Se não encontrá-lo, será necessário repetir as etapas descritas em [Exercício 0 - Pré-requisitos](./ex0.md).

![visual-studio-code-icon.png](./images/visual-studio-code-icon.png)

### Logon no Azure

Quando você faz logon com sua conta do Azure na qual costumava se registrar [Exercício 0 - Pré-requisitos](./ex0.md), o Visual Studio Code permitirá localizar e vincular todos os recursos do Event Hub.

Clique no botão **Azure** no Visual Studio Code. Se você não tiver essa opção, algo pode ter dado errado com a instalação das extensões necessárias.

Próxima seleção **Fazer logon no Azure**:

![3-01-vsc-open.png](./images/3-01-vsc-open.png)

Você será redirecionado para seu navegador para fazer logon. Lembre-se de selecionar a conta do Azure que você usou para registrar.

![3-02-vsc-select-account.png](./images/3-02-vsc-pick-account.png)

Quando vir a seguinte tela no seu navegador, você está conectado com o Visual Code Studio:

![3-03-vsc-login-ok.png](./images/3-03-vsc-login-ok.png)

Retorne ao Visual Code Studio (você verá o nome de sua assinatura do Azure, por exemplo **Assinatura do Azure 1**):

![3-04-vsc-logged-in.png](./images/3-04-vsc-logged-in.png)

## 13.5.3 Criar um projeto do Azure

Ao passar o mouse **Assinatura do Azure 1**, um menu aparecerá acima da seção, selecione **Criar Novo Projeto...**:

![3-05-vsc-create-project.png](./images/vsc2.png)

Selecione uma pasta local de sua escolha para salvar o projeto e clique em **Selecionar**:

![3-06-vsc-select-folder.png](./images/vsc3.png)

Agora você insere o assistente de criação de projetos. Selecionar **Javascript** como o idioma do seu projeto:

![3-07-vsc-select-language.png](./images/vsc4.png)

Selecionar **Acionador do Hub de Eventos do Azure** como o primeiro modelo de função do projeto:

![3-08-vsc-function-template.png](./images/vsc5.png)

Insira um nome para sua função, use o seguinte formato `--demoProfileLdap---aep-event-hub-trigger` e pressione enter:

![3-09-vsc-function-name.png](./images/vsc6.png)

Selecionar **Criar nova configuração de aplicativo local**:

![3-10-vsc-function-local-app-setting.png](./images/vsc7.png)

Selecione um namespace de hub de eventos. Você deve ver o Hub de eventos definido em **Exercício 2**. Neste exemplo, o namespace do Hub de eventos é **habilitação de vangeluw-aep**:

![3-11-vsc-function-select-namespace.png](./images/vsc8.png)

Selecione o Hub de eventos, você deve ver o Hub de eventos definido em **Exercício 2**. No meu caso, isso é **vangeluw-aep-enablement-event-hub**:

![3-12-vsc-function-select-eventhub.png](./images/vsc9.png)

Selecionar **RootManageSharedAccessKey** como sua política de Hub de eventos:

![3-13-vsc-function-select-eventhub-policy.png](./images/vsc10.png)

Inserir para usar **$Default**:

![3-14-vsc-eventhub-consumer-group.png](./images/vsc11.png)

Selecionar **Adicionar ao espaço de trabalho** sobre como abrir o projeto:

![3-15-vsc-project-add-to-workspace.png](./images/vsc12.png)

Após a criação do projeto, clique em **index.js** para abrir o arquivo no editor:

![3-16-vsc-open-index-js.png](./images/vsc13.png)

A carga enviada pelo Adobe Experience Platform para o seu Event Hub incluirá as IDs do segmento:

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

Substitua o código no index.js do código do Visual Studio pelo código abaixo. Esse código será executado sempre que a CDP em tempo real enviar qualificações de segmento para o destino do Hub de eventos. Em nosso exemplo, o código é apenas exibir e aprimorar a carga útil recebida. Mas você pode imaginar qualquer tipo de função para processar qualificações de segmento em tempo real.

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

## 13.5.4 Executar Projeto do Azure

Agora é hora de executar seu projeto. Nesta fase, não implantaremos o projeto no Azure. Nós o executaremos localmente no modo de depuração. Selecione o ícone Executar e clique na seta verde.

![3-17-vsc-run-project.png](./images/vsc14.png)

Na primeira vez que você executar o projeto no modo de depuração, será necessário anexar uma conta de armazenamento do Azure, clique em **Selecionar conta de armazenamento**.

![3-17-vsc-run-project.png](./images/vsc15.png)

Na lista de contas de armazenamento, selecione aquela que você criou como parte de [13.1.4 Configurar sua conta de armazenamento do Azure](./ex1.md). Sua conta de armazenamento é nomeada `--demoProfileLdap--aepstorage`, por exemplo: **mmeewisaepstorage**.

![3-22-vsc-select-storage-account.png](./images/vsc16.png)

Seu projeto está funcionando e agora está listando eventos no Hub de eventos. No próximo exercício, você demonstrará o comportamento no site de demonstração Luma que o qualificará para esses segmentos. Como resultado, você receberá uma carga de qualificação de segmento no terminal da função de acionador do Event Hub:

![3-23-vsc-application-started.png](./images/vsc17.png)

## 13.5.5 Parar o Projeto Azure

Para interromper o projeto, selecione a variável **Terminal** , clique em na janela do terminal e pressione **CMD-C** no OSX ou **CTRL-C** no Windows:

![3-24-vsc-application-stop.png](./images/vsc18.png)

Próxima etapa: [13.6 Cenário completo](./ex6.md)

[Voltar ao Módulo 13](./segment-activation-microsoft-azure-eventhub.md)

[Voltar para todos os módulos](./../../overview.md)
