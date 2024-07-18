---
title: Bootcamp - Journey Optimizer Criar sua jornada
description: Bootcamp - Journey Optimizer Criar sua jornada
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Journeys
exl-id: e4464502-60c8-4fba-a429-169b7a4516c8
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 2%

---

# 2.4 Testar a jornada

## Fluxo de jornada do cliente

Abra uma janela nova, limpa e incógnita do navegador e vá para [https://bootcamp.aepdemo.net](https://bootcamp.aepdemo.net). Clique em **Permitir tudo**. Com base no seu comportamento de navegação no fluxo de usuário anterior, você verá a personalização acontecer na página inicial do site.

![DSN](./images/web8a.png)

Clique no ícone **Perfil** no canto superior direito da tela.

![Demonstração](./images/web8b.png)

Clique em **Criar uma conta**.

![Demonstração](./images/pv5.png)

Preencha todos os campos do formulário. Use um valor real para endereço de email e número de telefone, pois ele será usado em exercícios posteriores para entrega de email e SMS.

![Demonstração](./images/pv7a.png)

Role para baixo. Agora é necessário inserir a eventID do evento personalizado criado no exercício 2.2. Você pode encontrá-lo aqui:

![ACOP](./images/payloadeventID.png)

A ID do evento é o que precisa ser enviado para o Adobe Experience Platform para acionar a jornada que você criou. Esta é a eventID neste exemplo: `19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f`

Preencha eventID no campo **ID do Evento de Criação de Conta** e clique em **Registrar**.

![Demonstração](./images/pv8a.png)

Você verá isso.

![Demonstração](./images/pv9.png)

Você também receberá esse e-mail, que é o e-mail que você mesmo criou como parte desse exercício.

![Demonstração](./images/pv10a.png)

Você terminou este exercício agora.

Próxima Etapa: [2.5 Instalar e usar o aplicativo móvel](./ex5.md)

[Voltar para Fluxo de Usuário 2](./uc2.md)

[Voltar a todos os módulos](../../overview.md)
