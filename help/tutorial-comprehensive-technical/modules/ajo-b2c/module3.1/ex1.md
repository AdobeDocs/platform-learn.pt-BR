---
title: Journey Optimizer Crie seu evento
description: Journey Optimizer Crie seu evento
kt: 5342
doc-type: tutorial
exl-id: b132ad78-aaa3-458d-9895-0935f8ba88bb
source-git-commit: f843c50af04d744a7d769f320b5b55a5e6d25ffd
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 1%

---

# 3.1.1 Criar o evento

Faça login no Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`.

![ACOP](./images/acoptriglp.png)

No menu esquerdo, role para baixo e clique em **Configurações**. Em seguida, clique no botão **Gerenciar** em **Eventos**.

![ACOP](./images/acopmenu.png)

Você verá uma visão geral de todos os eventos disponíveis. Clique em **Criar evento** para começar a criar seu próprio evento.

![ACOP](./images/emptyevent.png)

Uma nova janela de evento vazia será exibida.

![ACOP](./images/emptyevent1.png)

Primeiro, dê ao seu Evento um Nome como este: `--aepUserLdap--AccountCreationEvent`.
Defina a descrição como `Account Creation Event`, verifique se **Type** está definido como **Unitary** e para a seleção **Tipo de ID de Evento**, selecione **Gerado pelo Sistema**.

![ACOP](./images/eventdescription.png)

O próximo é a seleção Esquema. Use o esquema `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de selecionar o esquema, você verá vários campos sendo selecionados na seção **Carga**. Agora você deve passar o mouse sobre a seção **Carga** e verá três ícones pop-up. Clique no ícone **Editar**.

![ACOP](./images/eventpayload.png)

Você verá um pop-up de janela **Campos**, no qual é necessário selecionar alguns dos campos necessários para personalizar o email.  Escolheremos outros atributos de perfil posteriormente, usando os dados já existentes no Adobe Experience Platform.

![ACOP](./images/eventfields.png)

No objeto `--aepTenantId--.demoEnvironment`, selecione os campos **brandLogo** e **brandName**.

![ACOP](./images/eventpayloadbr.png)

No objeto `--aepTenantId--.identification.core`, certifique-se de selecionar o campo **email**. Clique em **Ok** para salvar suas alterações.

![ACOP](./images/eventpayloadbrid.png)

Você deverá ver isso. Defina o **Namespace** como **ECID (ECID)**. Clique em **Salvar**.

![ACOP](./images/eventsave.png)

Seu evento agora está configurado e salvo.

![ACOP](./images/eventdone.png)

Clique no evento novamente para abrir a tela **Editar Evento** novamente. Passe o mouse sobre o campo **Carga** novamente para ver os 3 ícones novamente. Clique no ícone **Exibir carga**.

![ACOP](./images/viewevent.png)

Agora você verá um exemplo da carga útil esperada.

![ACOP](./images/fullpayload.png)

Seu Evento tem uma eventID de orquestração exclusiva, que você pode encontrar rolando para baixo nessa carga até ver `_experience.campaign.orchestration.eventID`.

A ID de evento é o que precisa ser enviado para o Adobe Experience Platform para acionar a jornada que você criará a seguir. Lembre-se dessa eventID, pois ela será necessária em um dos próximos exercícios.
`"eventID": "5ae9b8d3f68eb555502b0c07d03ef71780600c4bd0373a4065c692ae0bfbd34d"`

Clique em **Ok**.

![ACOP](./images/payloadeventID.png)

Clique em **Cancelar**.

![ACOP](./images/payloadeventID1.png)

Você terminou este exercício agora.

Próxima etapa: [3.1.2 Criar fragmentos a serem usados na sua mensagem](./ex2.md)

[Voltar ao módulo 3.1](./journey-orchestration-create-account.md)

[Voltar a todos os módulos](../../../overview.md)
