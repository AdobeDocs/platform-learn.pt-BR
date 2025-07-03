---
title: Adobe Journey Optimizer - API de clima externa, ação de SMS e muito mais - Definir ações personalizadas
description: Adobe Journey Optimizer - API de clima externa, ação de SMS e muito mais - Definir ações personalizadas
kt: 5342
doc-type: tutorial
exl-id: 92752e84-3bbe-4d11-b187-bd9fdbbee709
source-git-commit: e3d3b8e3abdea1766594eca53255df024129cb2c
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 3%

---

# 3.2.3 Definir uma ação personalizada

Neste exercício, você criará uma ação personalizada para enviar uma mensagem a um canal do Slack.

Faça login no Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`. Você estará na exibição **Página inicial** da sua sandbox `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

Agora você usará um canal existente do Slack e enviará mensagens para esse canal do Slack. O Slack tem uma API fácil de usar e você usará o Adobe Journey Optimizer para acionar a API.

![Demonstração](./images/slack.png)

No menu esquerdo, role para baixo e clique em **Configurações**. Em seguida, clique no botão **Gerenciar** em **Ações**.

![Demonstração](./images/menuactions.png)

Você verá a lista **Ações**. Clique em **Criar ação**.

![Demonstração](./images/acthome.png)

Você verá um pop-up Ação vazio.

![Demonstração](./images/emptyact.png)

Como Nome da Ação, use `--aepUserLdap--TextSlack`.

Defina a Descrição como: `Send Message to Slack`.

Para a **Configuração de URL**, use este:

- URL: `https://2mnbfjyrre.execute-api.us-west-2.amazonaws.com/prod`
- Método: **POST**

>[!NOTE]
>
>O URL acima se refere a uma função AWS Lambda que encaminhará sua solicitação para o canal do Slack, como mencionado acima. Isso é feito para proteger o acesso a um canal do Slack de propriedade da Adobe. Se você tiver seu próprio canal do Slack, deve criar um Aplicativo Slack por meio de [https://api.slack.com/](https://api.slack.com/). Em seguida, é necessário criar um Webhook de Entrada nesse Aplicativo Slack e substituir a URL acima pela URL do Webhook de Entrada.

![Demonstração](./images/slackname.png)

A **Autenticação** deve ser definida como **Sem Autenticação**.

![Demonstração](./images/slackauth.png)

Em **Cargas**, é necessário definir quais campos devem ser enviados para o Slack. Logicamente, você deseja que o Adobe Journey Optimizer e o Adobe Experience Platform sejam o cérebro da personalização, de modo que o texto a ser enviado para o Slack deve ser definido pelo Adobe Journey Optimizer e, em seguida, enviado para o Slack para execução.

Para a **Solicitação**, clique no ícone **Editar Carga**.

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

Você verá isso. Clique em **Salvar**.

![Demonstração](./images/slackmsgpopup1.png)

Role para cima e clique em **Salvar** mais uma vez para salvar sua ação.

![Demonstração](./images/slackmsgpopup3.png)

Sua ação personalizada agora faz parte da lista **Ações**.

![Demonstração](./images/slackdone.png)

Você definiu eventos, fontes de dados externas e ações. A seguir, você combinará tudo isso em uma jornada.

## Próximas etapas

Ir para [3.2.4 Criar sua jornada e mensagens](./ex4.md){target="_blank"}

Voltar para [Adobe Journey Optimizer: Fontes de dados externas e ações personalizadas](journey-orchestration-external-weather-api-sms.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
