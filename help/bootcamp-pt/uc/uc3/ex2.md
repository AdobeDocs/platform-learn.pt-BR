---
title: Bootcamp - Combinação física e digital - Journey Optimizer Crie seu evento - Brasil
description: Bootcamp - Combinação física e digital - Journey Optimizer Crie seu evento - Brasil
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 5d824244766135cd4998feab48be7f6a69c42a70
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 3.2 Evento de emissão de moeda eletrônica

Faça logon sem acesso ao Adobe Journey Optimizer [Adobe Experience Cloud]. Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecion **Início** sem Journey Optimizer. Primeiro, verifique está usando caixa de proteção. O nome do fenômeno da sandbox que é usado `Bootcamp`. Para alternar de um sandbox para, clique em **Prod** e selecione a sandbox na lista. exemplo, o nome do sandbox é **Bootcamp**. Você estará na visualização da **Início** fazer sua sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

Sem menu à esquerda, papel para baixo **Configurações**. Em, nada **Gerenciar** em Eventos.

![ACOP](./images/acopmenu.png)

Você verá uma visão geral de eventos disponíveis. Clique em **Criar evento** para começar um te.

![ACOP](./images/emptyevent.png)

Uma nova janela de evento irá aparecer.

Em lugar, dê um nome ao evento como, por exemplo: `yourLastNameBeaconEntryEvent` e adicione uma descrição como, por exemplo: `Beacon Entry Event`.

![ACOP](./images/eventdescription.png)

Em, certifique **Tipo** status **Unitário** e, para a seleção de **Tipo de ID do evento** selecione **Sistema gerado**.

![ACOP](./images/eventidtype.png)

Um seguinte é um seleção. Esquema foi preparado para este. Usar um esquema `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de selecionar o Schema, você verá vários campos sendo selecionados na seção **Campos**. Agora Você Passou o mouse sobre a seção **Campos** e três ícones serão pop-up exibidos. Clique no ícone de **Editar**.

![ACOP](./images/eventpayload.png)

Você verá uma janela pop-up de **Campos**, onde você deve selecionar alguns dos campos que precisamos para persona jornada. Escolheremos os outros atributos de existentes, utilizando os dados na Adobe Experience Platform

![ACOP](./images/eventfields.png)

Papel para baixo sobre o objeto `Place context` Marque um caixa de seleção. Com isso, fazer o contexto da localização do cliente disponibilizado para uma jornada. Clique em **Ok** para salvar suas alterações.

![ACOP](./images/eventpayloadbr.png)

Em, você deverá por um abaixo. Clique em **Salvar** mais uma vez para salvar suas alterações.

![ACOP](./images/eventsave.png)

Seu evento agora está configurado e salvo.

![ACOP](./images/eventdone.png)

Clique em no es, para a tela **Editar evento** mais uma vez. Passe o mouse sobre **Campos** para os 3 ícones. Clique em ícone **Exibir**.

![ACOP](./images/viewevent.png)

Agora verá um exemplo do payload.
Seu evento tem um evento de orquestração único, que você está rolando para baixo, visualizador do site `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventID é o que deve enviado à Adobe Experience Platform para acionar uma jornada que construirá em um dos exercícios. Lembre-se do deste eventID, você precisar dele posteriormente.
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

Clique em **Ok** e, em, companhia **Cancelar**.

Você terminou este.

Proxima. [3.3 Notificação por push da sua jornada](./ex3.md)

[Retornar para Fluxo 3](./uc3.md)

[Retornar para Todos os Módulos](../../overview.md)
