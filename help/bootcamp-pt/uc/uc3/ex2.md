---
title: Bootcamp - Mesclagem física e digital - Journey Optimizer Crie seu evento - Brasil
description: Bootcamp - Mesclagem física e digital - Journey Optimizer Crie seu evento - Brasil
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 2133b560-09d8-419d-bb99-05d0f3df52cc
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# 3.2 Crise do evento

Faça logon no Adobe Journey Optimizer acessando uma [Adobe Experience Cloud]. Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a **Casa** no Journey Optimizer. Primeiro, usar você está usando o sandbox correto. O nome do sandbox que deve ser usado é `Bootcamp`. Para alternar de um sandbox para outro, clique em **Prod** e o sandbox na lista. Exemplo, o nome do sandbox é **Bootcamp**. Você na tag **Casa** da sua sandbox.`Bootcamp`

![ACOP](./images/acoptriglp.png)

Nenhum menu à esquerda, função para baixo e clique em **Configurações**. Em seguida, clique no botão **Gerenciar** em Eventos.

![ACOP](./images/acopmenu.png)

Você verá uma visão geral de todos os eventos. Clique em **Criar evento** para começar a criar seu próprio evento.

![ACOP](./images/emptyevent.png)

Uma nova janela de evento irá aparecer.

Em primeiro lugar, dê um dê seu evento como, por exemplo: `yourLastNameBeaconEntryEvent` e ➡ uma descrição como, por exemplo: `Beacon Entry Event`.

![ACOP](./images/eventdescription.png)

Em março,-se de que **Tipo** está definido como **Unitário** e, para a seleção de **Tipo de ID do evento**, **Sistema gerado**.

![ACOP](./images/eventidtype.png)

A seguinte é a seleção do esquema. Um esquema foi preparado para este exercício. Uso do esquema `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de selecionar o Schema, você verá vários campos, tendo a participação na lista **Campos**. Agora você deve passar o mouse sobre a **Campos** e dois pop-up. Clique em editar **Editar**.

![ACOP](./images/eventpayload.png)

Você verá uma janela pop-up de **Campos**, onde você deve mudar alguns dos campos que seguem para consolidar a jornada. Escolheremos outros problemas de perfil, ➡ os dados já existentes na Adobe Experience Platform

![ACOP](./images/eventfields.png)

Função para baixo até ver o objeto `Place context` e marque a caixa de seleção. Com, todo o contexto da localização do que será disponibilizado para a jornada. Clique em **Ok** para analisar as alterações.

![ACOP](./images/eventpayloadbr.png)

Em acompanhamento, você deve ver a tela abaixo. em **Salvar** mais uma vez para acompanhar a clique.

![ACOP](./images/eventsave.png)

Seu evento agora está configurado e salvo.

![ACOP](./images/eventdone.png)

Clique no seu evento para abrir a tela **Editar evento** mais uma vez. Passe o mouse sobre **Campos** para ver os 3 filtros. Clique em **Exibir**.

![ACOP](./images/viewevent.png)

Agora você verá um exemplo de carga esperada.
Seu evento tem um eventID de orquestração única, que você pode encontrar rolando para baixo útil útil visualiza `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventID é o que deve ser enviado à Adobe Experience Platform para acionar a jornada que você construirá em um dos relatórios publicados. -se deste eventID, você pode alterar a data.
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

Clique em **Ok** e, em seguida, clique em **resolver**.

Você terminou este exercício.

Próxima etapa: [3.3 Curie sua notificação e notificação push](./ex3.md)

[Retorno para Fluxo de monitoramento 3](./uc3.md)

[Retorno para Todos os compartilhados](../../overview.md)
