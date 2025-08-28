---
title: Implante seu código e publique seu aplicativo de forma privada
description: Implante seu código e publique seu aplicativo de forma privada
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 5a77ccdd-4000-4fb7-b696-dec40d01b41b
source-git-commit: 8219f3bd33448f90b87bf9ccb15738f1294e5965
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 1%

---

# 1.6.4 Implante seu código e publique seu aplicativo de forma privada

Publicar seu aplicativo de forma privada significa que ele está disponível no GenStudio for Performance Marketing sem precisar usar o parâmetro de sequência de consulta.

## 1.6.4.1 Publicar seu aplicativo

Ir para [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects){target="_blank"}.

>[!NOTE]
>
> A captura de tela abaixo mostra uma organização específica sendo selecionada. Quando você estiver assistindo a este tutorial, é muito provável que sua organização tenha um nome diferente. Quando se inscreveu neste tutorial, você recebeu os detalhes do ambiente que devem ser usados. Siga estas instruções.

Abra o projeto do Adobe IO com o App Builder, que deve ser o nome `--aepUserLdap-- GSPeM EXT`.

![Extensibilidade do GSPeM](./images/gspemextpub1.png)

Ir para **Produção**.

![Extensibilidade do GSPeM](./images/gspemextpub2.png)

Clique em **Publicar de forma privada**.

![Extensibilidade do GSPeM](./images/gspemextpub3.png)

Em seguida, é necessário preencher vários campos.

![Extensibilidade do GSPeM](./images/gspemextpub4.png)

Preencha os seguintes campos assim:

- **Título do aplicativo**: `--aepUserLdap-- - External DAM AWS S3`.
- **Descrição do aplicativo**: `External DAM AWS S3`
- **Email de contato**: digite seu endereço de email
- **Ícone de Aplicativo**: baixe e use esta imagem: [Imagem S3](./images/s3.jpeg)
- **Observação para o revisor**: AWS S3 DAM externo

Clique em **Enviar**.

![Extensibilidade do GSPeM](./images/gspemextpub5.png)

Clique em **Enviar**.

![Extensibilidade do GSPeM](./images/gspemextpub6.png)

## 1.6.4.2 Aprove seu aplicativo

>[!IMPORTANT]
>
>Esta etapa só pode ser executada por administradores do sistema no Adobe Admin Console. Se você não for um Administrador do sistema, não poderá executar isso. Entre em contato com o administrador do sistema para solicitar aprovação do aplicativo.

Depois que um desenvolvedor enviar um novo aplicativo para publicação, os administradores de sistema da sua organização serão notificados e precisarão revisar e aprovar.

Se você for um administrador do sistema, receberá esse email e poderá clicar em **Meu Exchange** para iniciar esse processo.

![Extensibilidade do GSPeM](./images/gspemextpub7.png)

No **Adobe Exchange**, os aplicativos do App Builder são exibidos e o aplicativo que acabou de ser enviado aguarda revisão. Clique no botão **Avaliação** do aplicativo `--aepUserLdap-- - External DAM AWS S3`.

![Extensibilidade do GSPeM](./images/gspemextpub8.png)

Adicione um comentário e clique em **Aprovar**.

![Extensibilidade do GSPeM](./images/gspemextpub9.png)

Seu aplicativo agora está aprovado e funcionará automaticamente no GenStudio for Performance Marketing, sem a necessidade de especificar o parâmetro da sequência de caracteres de consulta.

## Próximas etapas

Ir para [Resumo e Benefícios](./summary.md){target="_blank"}

Voltar para [GenStudio for Performance Marketing - Extensibilidade](./genstudioext.md){target="_blank"}

Voltar para [Todos os Módulos](./../../../overview.md){target="_blank"}
