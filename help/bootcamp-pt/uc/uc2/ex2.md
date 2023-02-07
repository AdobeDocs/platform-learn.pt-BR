---
title: Bootcamp - Journey Optimizer Create your event - Brasil
description: Bootcamp - Journey Optimizer Create your event - Brasil
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 5d824244766135cd4998feab48be7f6a69c42a70
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# 2.2 Evento de emissão de moeda eletrônica

Faça logon sem acesso ao Adobe Journey Optimizer [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecion para a visualização da **Início** sem Journey Optimizer. Primeiro, verifique está usando caixa de proteção. O nome do fenômeno da sandbox que é usado `Bootcamp`. Para alternar de um sandbox para, clique em Prod e selecione na sandbox lista. exemplo, o nome do sandbox é **Bootcamp**. Você estará na visualização da **Início** fazer sua sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

Sem menu à esquerda, papel para baixo **Configurações**. Em, nada **Gerenciar** amante **Eventos**.

![ACOP](./images/acopmenu.png)

Você verá uma visão geral de eventos disponíveis. Clique em **Criar evento** para começar um te.

![ACOP](./images/emptyevent.png)

Uma nova janela de evento irá aparecer.

![ACOP](./images/emptyevent1.png)

Em lugar, dê um nome ao evento como, por exemplo: `seuSobrenomeAccountCreationEvent` e adicione uma descrição como, por exemplo: `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Em, certifique **Tipo** status **Unitário** e, para a seleção de **Tipo de ID do evento** selecione **Sistema gerado**.

![ACOP](./images/eventidtype.png)

Um seguinte é um seleção. Esquema foi preparado para este. Usar um esquema `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de selecionar o Schema, você verá vários campos sendo selecionados na seção **Campos**. Agora Você Passou o mouse sobre a seção **Campos** e três ícones serão pop-up exibidos. Clique em ícone **Editar**.

![ACOP](./images/eventpayload.png)

Você verá uma janela pop-up de **Campos**, onde você deve selecionar alguns dos campos precisamos para persono e-mail. Escolheremos os outros atributos de existentes, utilizando os dados na Adobe Experience Platform.

![ACOP](./images/eventfields.png)

Sem objeto `_experienceplatform.demoEnvironment`, pcertifique-se de selecionar os campos **brandLogo** e **brandName**.

![ACOP](./images/eventpayloadbr.png)

Sem objeto `_experienceplatform.identification.core`, certifique-se de selecionar o campo **email**.

![ACOP](./images/eventpayloadbrid.png)

Clique em **Ok** para salvar suas alterações.

![ACOP](./images/saveok.png)

Em... Clique em **Salvar**  mais uma vez para salvar suas alterações..

![ACOP](./images/eventsave.png)

Seu evento agora está configurado e salvo.

![ACOP](./images/eventdone.png)

Clique em no es, para mais uma vez tela **Editar evento**. Passe o mouse sobre **Campos** para ver os 3 ícones outra vez. Clique em ícone **Exibir carga**.

![ACOP](./images/viewevent.png)

Agora, você é um exemplo da folha.
Seu evento tem um eventID de orquestração único, que você está soberando para abaixo, visualizar até `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventID é o que deve enviado à Adobe Experience Platform para acionar uma jornada que construirá em um dos exercícios. Lembre-se do deste eventID, você precisar dele posteriormente.
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

Clique em **Ok** e, em, companhia **Cancelar**.

Agora, você terminou este.

Proxima. [ 2.3 Crie sua mensagem de correio eletrônico](./ex3.md)

[Retornar para Fluxo 2](./uc2.md)

[Retornar para Todos os Módulos](../../overview.md)
