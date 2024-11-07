---
title: Ativação de segmento para o Hub de eventos do Microsoft Azure - Criar um segmento de transmissão
description: Ativação de segmento para o Hub de eventos do Microsoft Azure - Criar um segmento de transmissão
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# 2.4.3 Criar um segmento

## 2.4.3.1 Introdução

Você criará um segmento simples:

- **Interesse no Equipamento** para o qual os perfis de clientes se qualificarão ao visitar a página **Equipamento** do site de demonstração Luma.

### É bom saber

A Real-time CDP acionará uma ativação para um destino quando você se qualificar para um segmento que faz parte da lista de ativação desse destino. Quando esse for o caso, a carga de qualificação de segmento que será enviada para esse destino conterá **todos os segmentos para os quais seu perfil se qualifica**.

O objetivo deste módulo é mostrar que a qualificação de segmento do seu Perfil de cliente é enviada para o destino do hub de eventos **your** em tempo real.

### Status do segmento

Uma qualificação de segmento no Adobe Experience Platform sempre tem uma propriedade de **status** e pode ser uma das seguintes:

- **realizado**: isso indica uma nova qualificação de segmento
- **existente**: isso indica uma qualificação de segmento existente
- **saiu**: isso indica que o perfil não se qualifica mais para o segmento

## 2.4.3.2 Criar o segmento

A criação de um segmento é explicada detalhadamente no [Módulo 2.3](./../../../modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md).

### Criar segmento

Faça logon no Adobe Experience Platform acessando esta URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepSandboxName--``. Você pode fazer isso clicando no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. Depois de selecionar a sandbox apropriada, você verá a alteração da tela e agora estará em sua sandbox dedicada.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/sb1.png)

Vá para **Segmentos**. Clique no botão **+ Criar segmento**.

![Assimilação de dados](./images/seg.png)

Nomeie seu segmento `--aepUserLdap-- - Interest in Equipment` e adicione o evento de experiência de nome de página:

Clique em **Eventos** e arraste e solte o **XDM ExperienceEvent > Web > Detalhes da página da Web > Nome**. Digite **equipamento** como valor:

![4-05-create-ee-2.png](./images/4-05-create-ee-2.png)

Arraste e solte o **XDM ExperienceEvent > `--aepTenantId--` > demoEnvironment > brandName**. Insira `--aepUserLdap--` como valor, defina o parâmetro de comparação como **contém** e clique em **Salvar**:

![4-05-create-ee-2-brand.png](./images/4-05-create-ee-2-brand.png)

### Definição do PQL

A PQL do seu segmento é semelhante a:

```code
CHAIN(xEvent, timestamp, [C0: WHAT(web.webPageDetails.name.equals("equipment", false) and _experienceplatform.demoEnvironment.brandName.contains("--aepUserLdap--", false))])
```

Próxima etapa: [2.4.4 Ativar segmento](./ex4.md)

[Voltar ao módulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Voltar a todos os módulos](./../../../overview.md)
