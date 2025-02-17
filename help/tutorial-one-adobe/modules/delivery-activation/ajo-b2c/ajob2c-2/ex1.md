---
title: Adobe Journey Optimizer - API de clima externa, ação de SMS e muito mais - Definir um evento
description: Adobe Journey Optimizer - API de clima externa, ação de SMS e muito mais
kt: 5342
doc-type: tutorial
exl-id: bde4290a-59d1-4471-83a7-1cad69f94ff1
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 2%

---

# 3.2.1 Definir um evento

Faça login no Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`. Você estará na exibição **Página inicial** da sua sandbox `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

No menu esquerdo, role para baixo e clique em **Configurações**. Em seguida, clique no botão **Gerenciar** em **Eventos**.

![ACOP](./images/acopmenu.png)

Você verá uma visão geral de todos os eventos disponíveis. Clique em **Criar evento** para começar a criar seu próprio evento.

![ACOP](./images/emptyevent.png)

Uma nova janela de evento vazia será exibida.
Como nome do Evento, use `--aepUserLdap--GeofenceEntry`.

Defina a Descrição como: `Geofence Entry Event`.

Verifique se o **Tipo** está definido como **Unitário** e, para a seleção do **Tipo de ID de Evento**, selecione **Gerado pelo Sistema**

![Demonstração](./images/evname.png)

Em seguida, é necessário selecionar um schema. Todos os esquemas mostrados aqui são Esquemas do Adobe Experience Platform.

![Demonstração](./images/evschema.png)

Você observará que nem todos os esquemas são exibidos. Há muito mais esquemas disponíveis no Adobe Experience Platform.
Para aparecer nessa lista, um esquema precisa ter um grupo de campos muito específico vinculado a ele. O grupo de campos necessário para aparecer aqui é chamado `Orchestration eventID`.

Vamos ver rapidamente como esses esquemas são definidos no Adobe Experience Platform.

No menu esquerdo, vá para **Schemas** e abra-o em uma nova guia do navegador. Em **Esquemas**, vá para **Procurar** para ver a lista de Esquemas disponíveis.
Abra o Esquema `Demo System - Event Schema for Website (Global v1.1)`.

![Assimilação de dados](./images/schemas.png)

Depois de abrir o Esquema, você verá que o grupo de campos `Orchestration eventID` faz parte do esquema.
Este grupo de campos tem apenas dois campos, `_experience.campaign.orchestration.eventID` e `originJourneyID`.

![Assimilação de dados](./images/schemageo.png)

Quando esse grupo de campos e esse campo de ID de evento específico fizerem parte de um esquema, esse esquema estará disponível para uso no Adobe Journey Optimizer.

Volte para a configuração do evento no Adobe Journey Optimizer.

![Demonstração](./images/evschema.png)

Nesse caso de uso, você deseja acompanhar um Evento Geofence para entender se um cliente está em um local específico, portanto, agora, selecione o Esquema `Demo System - Event Schema for Website (Global v1.1)` como o Esquema do seu Evento.

![Demonstração](./images/evschema1.png)

Em seguida, o Adobe Journey Optimizer selecionará automaticamente alguns campos obrigatórios, mas você poderá editar os campos que são disponibilizados para o Adobe Journey Optimizer.

Clique no ícone de **lápis** para editar os campos.

![Demonstração](./images/editfields.png)

Em seguida, você verá uma janela pop-up com uma hierarquia de esquema que permite selecionar campos.

![Demonstração](./images/popup.png)

Campos como ECID e a Orchestration eventID são obrigatórios e, como tal, pré-selecionados.

No entanto, um profissional de marketing precisa ter acesso flexível a todos os pontos de dados que fornecem contexto a uma jornada. Portanto, vamos selecionar os seguintes campos no mínimo (encontrados no nó de contexto Local ):

- Cidade

Quando terminar, clique em **OK**.

![Demonstração](./images/popupok.png)

O Adobe Journey Optimizer também precisa de um Identificador para identificar o cliente. Como o Adobe Journey Optimizer é vinculado ao Adobe Experience Platform, o Identificador principal de um Esquema é tomado automaticamente como o Identificador da Jornada.
O identificador principal também levará em conta automaticamente o Gráfico de identidade completo do Adobe Experience Platform e vinculará todos os comportamentos em todas as identidades, dispositivos e canais disponíveis ao mesmo perfil, para que o Adobe Journey Optimizer seja contextual, relevante e consistente. Clique em **Salvar**.

![Demonstração](./images/eventidentifier.png)

Seu evento fará parte da lista de eventos disponíveis.

![Demonstração](./images/eventlist.png)

Finalmente, você precisa recuperar o `Orchestration eventID` para seu evento personalizado.

Abra o evento novamente clicando nele na lista de eventos.
No seu Evento, clique no ícone **Exibir carga** ao lado de **Campos**.

![Demonstração](./images/fieldseyepayload.png)

Clicar no ícone **Exibir carga** abre uma amostra de carga XDM para este evento. Role para baixo na **Carga** até ver a linha `eventID`.

![Demonstração](./images/fieldseyepayloadev.png)

Anote o `eventID` como você vai precisar dele na última vez para testar sua configuração.

Neste exemplo, o `eventID` é `4df8dc10731eba7b0c37af83a9db38d4de7aa6aebcce38196d9d47929b9c598e`.

Agora você definiu o evento que acionará a jornada que estamos criando. Quando a jornada for acionada, os campos de geofence como Cidade e quaisquer outros que você tenha escolhido (como País, Latitude e Longitude) serão disponibilizados para a jornada.

Conforme discutido na descrição do caso de uso, precisamos fornecer promoções contextuais que dependam do tempo. Para obter informações sobre o clima, precisaremos definir uma fonte de dados externa que nos fornecerá as informações sobre o clima desse local. Você usará o serviço **API do OpenWeather** para nos fornecer essas informações.

## Próximas etapas

Ir para [3.2.2 Definir uma fonte de dados externa](./ex2.md){target="_blank"}

Voltar para [Adobe Journey Optimizer: Fontes de dados externas e ações personalizadas](journey-orchestration-external-weather-api-sms.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
