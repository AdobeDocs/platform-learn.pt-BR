---
title: Adobe Journey Optimizer - API de clima externa, ação de SMS e muito mais - Definir ações personalizadas
description: Adobe Journey Optimizer - API de clima externa, ação de SMS e muito mais - Definir ações personalizadas
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 3%

---

# 3.2.3 Definir uma ação personalizada

Neste exercício, você criará duas ações personalizadas usando o Adobe Journey Optimizer em combinação.

Faça login no Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`. Para alterar a sandbox, clique em **Produção (VA7)** e selecione a sandbox na lista. Neste exemplo, a sandbox é chamada de **AEP Enablement FY22**. Você estará na exibição **Página inicial** da sua sandbox `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

No menu esquerdo, role para baixo e clique em **Configurações**. Em seguida, clique no botão **Gerenciar** em **Ações**.

![Demonstração](./images/menuactions.png)

Você verá a lista **Ações**.

![Demonstração](./images/acthome.png)

Você definirá uma ação que envia um texto para um canal Slack.

## 3.2.3.1 Ação: Enviar texto para o canal Slack

Agora você usará um canal de Slack existente e enviará mensagens para esse Canal de Slack. O Slack tem uma API fácil de usar e usaremos o Adobe Journey Optimizer para acionar a API.

![Demonstração](./images/slack.png)

Clique em **Criar ação** para começar a adicionar uma nova ação.

![Demonstração](./images/adda.png)

Você verá um pop-up Ação vazio.

![Demonstração](./images/emptyact.png)

Como Nome da Ação, use `--aepUserLdap--TextSlack`. Neste exemplo, o Nome da Ação é `vangeluwTextSlack`.

Defina a Descrição como: `Send Text to Slack`.

![Demonstração](./images/slackname.png)

Para a **Configuração de URL**, use este:

- URL: `https://2mnbfjyrre.execute-api.us-west-2.amazonaws.com/prod`
- Método: **POST**

>[!NOTE]
>
>O URL acima se refere a uma função AWS Lambda que encaminhará sua solicitação para o canal Slack, como mencionado acima. Isso é feito para proteger o acesso a um canal de Slack de propriedade de Adobe. Se você tiver seu próprio canal Slack, deve criar um Aplicativo Slack por meio de [https://api.slack.com/](https://api.slack.com/). Em seguida, será necessário criar um Webhook de Entrada nesse Aplicativo Slack e substituir o URL acima pelo URL do Webhook de Entrada.

Você não precisa alterar os Campos de cabeçalho.

![Demonstração](./images/slackurl.png)

A **Autenticação** deve ser definida como **Sem Autenticação**.

![Demonstração](./images/slackauth.png)

Para os **Parâmetros de Ação**, você precisa definir quais campos devem ser enviados para o Slack. Logicamente, queremos que o Adobe Journey Optimizer e o Adobe Experience Platform sejam o cérebro da personalização, de modo que o texto a ser enviado para o Slack seja definido pelo Adobe Journey Optimizer e, em seguida, enviado para o Slack para execução.

Portanto, para os **Parâmetros de ação**, clique no ícone **Editar carga**.

![Demonstração](./images/slackmsgp.png)

Você verá uma janela pop-up vazia.

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

INFO: ao especificar os campos abaixo, esses campos ficarão acessíveis pela Jornada do cliente e você poderá preenchê-los dinamicamente na Jornada:

**&quot;toBeMapped&quot;: verdadeiro,**

**&quot;dataType&quot;: &quot;cadeia de caracteres&quot;,**

**&quot;rótulo&quot;: &quot;textToSlack&quot;**

Você verá isto:

![Demonstração](./images/slackmsgpopup1.png)

Clique em **Salvar**.

![Demonstração](./images/twiliomsgpopup2.png)

Role para cima e clique em **Salvar** mais uma vez para salvar sua Ação personalizada.

![Demonstração](./images/slackmsgpopup3.png)

Sua ação personalizada agora faz parte da lista **Ações**.

![Demonstração](./images/slackdone.png)

Você definiu eventos, fontes de dados externas e ações. Agora vamos consolidar tudo isso em uma jornada.

Próxima Etapa: [3.2.4 Crie sua jornada e mensagens](./ex4.md)

[Voltar ao Módulo 8](journey-orchestration-external-weather-api-sms.md)

[Voltar a todos os módulos](../../../overview.md)
