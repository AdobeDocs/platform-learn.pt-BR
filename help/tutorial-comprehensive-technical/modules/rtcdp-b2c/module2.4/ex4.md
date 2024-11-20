---
title: Audience Activation para o Hub de eventos do Microsoft Azure - Criar um público
description: Audience Activation para o Hub de eventos do Microsoft Azure - Criar um público
kt: 5342
doc-type: tutorial
exl-id: 56f6a6dc-82aa-4b64-a3f6-b6f59c484ccb
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 2%

---

# 2.4.4 Criar um público-alvo

## Introdução

Você criará um público-alvo simples:

- **Interesse em Planos** para os quais os clientes se qualificarão quando visitarem a página **Planos** do site de demonstração do CitiSignal.

### É bom saber

A Real-time CDP acionará uma ativação para um destino quando você se qualificar para um público-alvo que faça parte da lista de ativação desse destino. Quando esse for o caso, a carga de qualificação de público-alvo que será enviada para esse destino conterá **todos os públicos-alvo para os quais seu perfil de cliente se qualifica**.

O objetivo desse módulo é mostrar que a qualificação de público-alvo do seu Perfil de cliente é enviada para o seu destino do Hub de eventos em tempo quase real.

### Status do público

Uma qualificação de público-alvo no Adobe Experience Platform sempre tem uma propriedade de **status** e pode ser uma das seguintes:

- **realizado**: isso indica uma nova qualificação de público-alvo
- **saiu**: isso indica que o perfil não se qualifica mais para o público-alvo

## Criar o público

Faça logon no Adobe Experience Platform acessando esta URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepSandboxName--``. Depois de selecionar a sandbox apropriada, você verá a alteração da tela e agora estará em sua sandbox dedicada.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/sb1.png)

Ir para **Públicos-alvo**. Clique no botão **+ Criar público-alvo**.

![Assimilação de dados](./images/seg.png)

Selecione **Regra de compilação** e clique em **Criar**.

![Assimilação de dados](./images/seg1.png)

Nomeie seu público-alvo `--aepUserLdap-- - Interest in Plans`, defina o método de avaliação como **Edge** e adicione o nome da página do evento de experiência.

Clique em **Eventos** e arraste e solte o **XDM ExperienceEvent > Web > Detalhes da página da Web > Nome**. Insira **planos** como o valor:

![4-05-create-ee-2.png](./images/405createee2.png)

Arraste e solte o **XDM ExperienceEvent > `--aepTenantId--` > demoEnvironment > brandName**. Digite `--aepUserLdap--` como valor, defina o parâmetro de comparação como **contém** e clique em **Publish**:

![4-05-create-ee-2-brand.png](./images/405createee2brand.png)

Seu público-alvo foi publicado.

![4-05-create-ee-2-brand.png](./images/405createee2brand1.png)

Próxima etapa: [2.4.5 Ativar público-alvo](./ex5.md)

[Voltar ao módulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Voltar a todos os módulos](./../../../overview.md)
