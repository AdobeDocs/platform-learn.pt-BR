---
title: Ativação de segmento para o Hub de eventos do Microsoft Azure - Criar um segmento de fluxo
description: Ativação de segmento para o Hub de eventos do Microsoft Azure - Criar um segmento de fluxo
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: de3824bd-553c-4281-8edf-29abcc28a8e7
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 1%

---

# 13.3 Criar um segmento

## 13.3.1 Introdução

Você criará um segmento simples:

- **Interesse em equipamentos** para os quais os perfis do cliente serão qualificados quando visitarem a **Equipamento** página do site de demonstração Luma.

### Bom saber

A CDP em tempo real acionará uma ativação para um destino quando você se qualificar para um segmento que faz parte da lista de ativação desse destino. Quando esse for o caso, a carga da qualificação de segmento que será enviada para esse destino conterá **todos os segmentos para os quais seu perfil se qualifica**.

O objetivo desse módulo é mostrar que a qualificação de segmento do Perfil do cliente é enviada para **your** destino do hub de eventos em tempo real.

### Status do segmento

Uma qualificação de segmento no Adobe Experience Platform sempre tem uma **status**-e pode ser um dos seguintes:

- **realizado**: isso indica uma nova qualificação de segmento
- **existente**: isso indica uma qualificação de segmento existente
- **encerrado**: isso indica que o perfil não se qualifica mais para o segmento

## 13.3.2 Construir o segmento

A criação de um segmento é explicada detalhadamente em [Módulo 6](../module6/real-time-cdp-build-a-segment-take-action.md).

### Criar segmento

Faça logon no Adobe Experience Platform acessando este URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer logon, você será direcionado para a página inicial do Adobe Experience Platform.

![Assimilação de dados](../module2/images/home.png)

Antes de continuar, é necessário selecionar um **sandbox**. A sandbox a ser selecionada é chamada de ``--aepSandboxId--``. Você pode fazer isso clicando no texto **[!UICONTROL Produto de produção]** na linha azul na parte superior da tela. Depois de selecionar a sandbox apropriada, você verá a tela mudar e agora estará na sandbox dedicada.

![Assimilação de dados](../module2/images/sb1.png)

Ir para **Segmentos**. Clique no botão **+ Criar segmento** botão.

![Assimilação de dados](./images/seg.png)

Dê um nome ao seu segmento `--demoProfileLdap-- - Interest in Equipment` e adicione o evento de experiência do nome da página:

Clique em **Eventos** e arrastar e soltar **XDM ExperienceEvent > Web > Detalhes da página da Web > Nome**. Enter **equipamento** como o valor:

![4-05-create-ee-2.png](./images/4-05-create-ee-2.png)

Arrastar e soltar **XDM ExperienceEvent > `--aepTenantIdSchema--` > demoEnvironment > brandName**. Enter `--demoProfileLdap--` como o valor, defina o parâmetro de comparação como **contém** e clique em **Salvar**:

![4-05-create-ee-2-brand.png](./images/4-05-create-ee-2-brand.png)

### Definição de PQL

O PQL do segmento se parece com:

```code
CHAIN(xEvent, timestamp, [C0: WHAT(web.webPageDetails.name.equals("equipment", false) and _experienceplatform.demoEnvironment.brandName.contains("--demoProfileLdap--", false))])
```

Próxima etapa: [13.4 Ativar segmento](./ex4.md)

[Voltar ao Módulo 13](./segment-activation-microsoft-azure-eventhub.md)

[Voltar para todos os módulos](./../../overview.md)
