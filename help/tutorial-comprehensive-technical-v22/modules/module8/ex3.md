---
title: Adobe Journey Optimizer - API de Tempo Externo, Ação de SMS e muito mais - Definir ações personalizadas
description: Adobe Journey Optimizer - API de Tempo Externo, Ação de SMS e muito mais - Definir ações personalizadas
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7ee5aee9-3740-4eee-9f53-a44fdb564a00
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# 8.3 Definir uma ação personalizada

Neste exercício, você criará duas ações personalizadas usando o Adobe Journey Optimizer em combinação.

Faça logon no Adobe Journey Optimizer acessando [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Você será redirecionado para o **Início**  no Journey Optimizer. Primeiro, certifique-se de usar a sandbox correta. A sandbox a ser usada é chamada de `--aepSandboxId--`. Para alterar de uma sandbox para outra, clique em **Produto de produção (VA7)** e selecione a sandbox na lista. Neste exemplo, a sandbox é chamada de **Ativação AEP FY22**. Você estará no **Início** exibição da sandbox `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

No menu esquerdo, role para baixo e clique em **Configurações**. Em seguida, clique no botão **Gerenciar** botão abaixo **Ações**.

![Demonstração](./images/menuactions.png)

Você verá o **Ações** lista.

![Demonstração](./images/acthome.png)

Você definirá uma ação que envia um texto para um canal de Slack.

## 8.3.1 Ação: Enviar texto para canal de Slack

Agora você usará um canal de Slack existente e enviará mensagens para esse canal de Slack. O Slack tem uma API fácil de usar e usaremos o Adobe Journey Optimizer para acionar a API.

![Demonstração](./images/slack.png)

Clique em **Criar ação** para começar a adicionar uma nova ação.

![Demonstração](./images/adda.png)

Você verá um pop-up de Ação vazio.

![Demonstração](./images/emptyact.png)

Como um Nome para a Ação, use `--demoProfileLdap--TextSlack`. Neste exemplo, o Nome da ação é `vangeluwTextSlack`.

Defina Descrição como: `Send Text to Slack`.

![Demonstração](./images/slackname.png)

Para o **Configuração de URL** use esta opção:

- URL: `https://2mnbfjyrre.execute-api.us-west-2.amazonaws.com/prod`
- Método: **POST**

>[!NOTE]
>
>O URL acima se refere a uma função AWS Lambda que encaminhará sua solicitação para o canal Slack, como mencionado acima. Isso é feito para proteger o acesso a um canal Slack de propriedade do Adobe. Se você tiver seu próprio canal Slack, deve criar um aplicativo Slack por meio de [https://api.slack.com/](https://api.slack.com/), é necessário criar um Webhook de entrada nesse aplicativo do Slack e, em seguida, substituir o URL acima pelo URL do Webhook de entrada.

Não é necessário alterar os Campos de cabeçalho.

![Demonstração](./images/slackurl.png)

**Autenticação** deve ser definido como **Sem Autenticação**.

![Demonstração](./images/slackauth.png)

Para o **Parâmetros de ação**, é necessário definir quais campos devem ser enviados para o Slack. Na lógica, queremos que o Adobe Journey Optimizer e o Adobe Experience Platform sejam o cérebro da personalização, de modo que o texto a ser enviado para o Slack deve ser definido pelo Adobe Journey Optimizer e enviado para o Slack para execução.

Assim para o **Parâmetros de ação**, clique no botão **Editar carga** ícone .

![Demonstração](./images/slackmsgp.png)

Em seguida, você verá uma janela pop-up vazia.

![Demonstração](./images/slackmsgpopup.png)

Copie o texto abaixo e cole-o na janela pop-up vazia.

```json
{
 "text": {
  "toBeMapped": true,
  "dataType": "string",
  "label": "textToSlack"
 }
}
```

FYI: ao especificar os campos abaixo, esses campos ficarão acessíveis na Jornada do cliente e você poderá preenchê-los dinamicamente a partir da Jornada:

**&quot;toBeMapped&quot;: true,**

**&quot;dataType&quot;: &quot;string&quot;,**

**&quot;label&quot;: &quot;textToSlack&quot;**

Você verá isso:

![Demonstração](./images/slackmsgpopup1.png)

Clique em **Salvar**.

![Demonstração](./images/twiliomsgpopup2.png)

Role para cima e clique **Salvar** mais uma vez para salvar sua ação personalizada.

![Demonstração](./images/slackmsgpopup3.png)

Sua ação personalizada agora faz parte do **Ações** lista.

![Demonstração](./images/slackdone.png)

Você definiu eventos, uma fonte de dados externa e ações. Agora vamos consolidar tudo isso em uma jornada.

Próxima etapa: [8.4 Criar sua jornada e mensagens](./ex4.md)

[Voltar ao Módulo 8](journey-orchestration-external-weather-api-sms.md)

[Voltar para todos os módulos](../../overview.md)
