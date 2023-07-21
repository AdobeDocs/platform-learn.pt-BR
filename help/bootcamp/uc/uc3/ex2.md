---
title: Bootcamp - Mesclagem física e digital - Journey Optimizer Crie seu evento
description: Bootcamp - Mesclagem física e digital - Journey Optimizer Crie seu evento
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 3d47c686-c2d8-4961-a05b-0990025392fa
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# 3.2 Criar o evento

Faça logon no Adobe Journey Optimizer acessando [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a **Início**  exibir no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `Bootcamp`. Para alterar de uma sandbox para outra, clique em **Prod** e selecione a sandbox na lista. Neste exemplo, a sandbox é chamada de **Bootcamp2**. Você estará no **Início** exibição da sua sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

No menu esquerdo, role para baixo e clique em **Configurações**. Clique em **Gerenciar** botão em **Eventos**.

![ACOP](./images/acopmenu.png)

Você verá uma visão geral de todos os eventos disponíveis. Clique em **Criar evento** para começar a criar seu próprio evento.

![ACOP](./images/emptyevent.png)

Uma nova janela de evento vazia será exibida.

Primeiro de tudo, dê ao seu evento um nome como este: `yourLastNameBeaconEntryEvent` e adicione uma descrição como esta `Beacon Entry Event`.

![ACOP](./images/eventdescription.png)

Em seguida, verifique se **Tipo** está definida como **Unitário** e para o **Tipo de ID de evento** seleção, selecione **Gerado pelo sistema**.

![ACOP](./images/eventidtype.png)

O próximo é a seleção Esquema. Um esquema foi preparado para este exercício. Use o esquema `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de selecionar o esquema, você verá vários campos que estão sendo selecionados na **Campos** seção. Agora você deve passar o mouse sobre o **Campos** e você verá três ícones aparecendo. Clique no link **Editar** ícone.

![ACOP](./images/eventpayload.png)

Você verá um **Campos** pop-up de janela, na qual é necessário selecionar alguns dos campos necessários para personalizar a jornada.  Escolheremos outros atributos de perfil posteriormente, usando os dados já existentes no Adobe Experience Platform.

![ACOP](./images/eventfields.png)

Role para baixo até ver o objeto `Place context` e marque a caixa de seleção. Com isso, todo o contexto da localização do cliente será disponibilizado para a jornada. Clique em **Ok** para salvar as alterações.

![ACOP](./images/eventpayloadbr.png)

Você deverá ver isso. Clique em **Salvar** mais uma vez para salvar as alterações.

![ACOP](./images/eventsave.png)

Seu evento agora está configurado e salvo.

![ACOP](./images/eventdone.png)

Clique no evento novamente para abrir a **Editar evento** novamente. Focalizar **Campos** novamente para ver os 3 ícones. Clique no link **Exibir** ícone.

![ACOP](./images/viewevent.png)

Agora você verá um exemplo da carga útil esperada.
Seu evento tem uma eventID de orquestração exclusiva, que pode ser encontrada rolando para baixo nessa carga até que você veja `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

A ID do evento é o que precisa ser enviado para o Adobe Experience Platform para acionar a jornada que você criará em um dos próximos exercícios. Lembre-se dessa eventID, pois ela pode ser necessária posteriormente.
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

Clique em **Ok**, seguido por um clique em **Cancelar**.

Você terminou este exercício agora.

Próxima etapa: [3.3 Criar sua jornada e notificação por push](./ex3.md)

[Voltar para Fluxo de Usuário 3](./uc3.md)

[Voltar a todos os módulos](../../overview.md)
