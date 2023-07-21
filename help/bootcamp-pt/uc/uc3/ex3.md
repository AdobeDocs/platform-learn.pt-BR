---
title: Bootcamp - Mesclagem física e digital - Journey Optimizer Crie sua jornada e push - Notificação do Brasil
description: Bootcamp - Mesclagem física e digital - Journey Optimizer Crie sua jornada e push - Notificação do Brasil
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: a4ef6eaf-6b39-4450-82bf-7db99595a323
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 1%

---

# 3.3 Promoção da notificação da jornada e da notificação

Neste exercício, você muda a jornada e a mensagem que precisa ser acionada quando uma mudança (beacon) usando o móvel.

Faça logon no Adobe Journey Optimizer acessando a [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a da **Início** sem Journey Optimizer. Primeiro, usar você está usando o sandbox correto. O nome do sandbox que deve ser usado é `Bootcamp`. Para alternar de um sandbox para outro, clique em **Prod** e o sandbox na lista. Exemplo, o nome do sandbox é **Bootcamp**. Você está na da **Início**  fazer seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 Criar a sua jornada

Sem menu à esquerda, clique em **Jornadas**. Em seguida, clique em **Criar Jornada** para criar uma nova jornada.

![ACOP](./images/createjourney.png)

Você verá uma tela de vazia.

![ACOP](./images/journeyempty.png)

Não exercício anterior, você criou um novo **Evento**. Você consegue o evento `yourLastNameBeaconEntryEvent` e substituiu `yourLastName` pelo seu sobrenome. Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

Agora você deve este evento como o início desta Jornada. Você pode fazer o lado evento da tela e tendências pelo seu lista de eventos.

![ACOP](./images/eventlist.png)

é possível encontrar seu evento, e solte o evento na tela de jornada. Sua jornada deve ser seguido. Clique em **Ok** para proteger o cliente.

![ACOP](./images/journeyevent.png)

Como segunda etapa da jornada, você deve mudar uma ação **Push**. Vá para o lado esquerdo da tela para **Ações**, uma ação **Push** e ➡ e nó solte a ação no segundo da jornada.

![ACOP](./images/journeyactions.png)

No lado direito da tela, agora você deve criar sua notificação push.

Definir um **Categoria** como **Marketing** e envio da superfície de push que muda o envio de. Nesse caso, a estratégia de push a seleção é **meeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Criar a sua mensagem

Clique em **Editar conteúdo**.

![ACOP](./images/emptymsg.png)

Em seguida, a tela abaixo é apresentada:

![ACOP](./images/emailmsglist.png)

Vamos definir a notificação da notificação.

Clique no campo de texto **Título**.

![Journey Optimizer](./images/msg5.png)

Na área de texto, início **Olá**. Clique em nenhum momento personalizado.

![Journey Optimizer](./images/msg6.png)

Agora precisa o token de personalização para o campo **Nome** que está presente em `profile.person.name.firstName`. Sem menu à esquerda, **Atributos do perfil**, role para baixo/navegue para encontrar o elemento **Person** e clique na seta para explorar um nível até chegar ao campo `profile.person.name.firstName`. Clique no ➡ **+** para o campo à tela. Clique em **Salvar**.

![Journey Optimizer](./images/msg7.png)

Então, você muda para esta tela. Clique no domínio da personalização ao lado do campo **Corpo**.

![Journey Optimizer](./images/msg11.png)

Na área de texto, tela `Bem-vindo(a)`.

![Journey Optimizer](./images/msg12.png)

Em seguida, clique em  **Atributos contextuais** e **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

Clique em **Eventos**.

![ACOP](./images/jomsg4.png)

Clique no nome nome nome, que deve ser observador do seu seguinte: **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

Clique em **Contexto do local**.

![ACOP](./images/jomsg6.png)

Clique em **Interação de POI**.

![ACOP](./images/jomsg7.png)

Clique em **Detalhes do POI**.

![ACOP](./images/jomsg8.png)

Clique em não **+** ícone não **Nome do POI**.
Em seguida, o seguinte é apresentado. Clique em **Salvar**.

![ACOP](./images/jomsg9.png)

Sua mensagem está pronta. Clique na seta no canto superior para acompanhar a sua jornada.

![ACOP](./images/jomsg11.png)

Clique em **Ok**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Envie uma mensagem para uma tela

Como etapa da jornada, você deve mudar uma ação  **sendMessageToScreen**. Vá para o lado esquerdo da tela para **Ações**, uma ação **sendMessageToScreen** e pesquisas e solte a ação no terceiro nó da sua jornada. Em seguida, você verá a tela abaixo.

![ACOP](./images/jomsg15.png)

**sendMessageToScreen** é uma ação exclusiva que publica uma mensagem no **Endpoint** para usar pela compra na loja. Uma ação **sendMessageToScreen** espera que pode mudar o que é preciso. Você pode alterar essa seleção rolando para baixo até **Parâmetros de ação**.

![ACOP](./images/jomsg16.png)

1999 &quot;Agora você precisa de acordo com as regras para cada domínio da ação&quot; . Fórum de dúvidas sobre o assunto...

| Parâmetro | Valor de  |
|:-------------:| :---------------:|
| ENTREGA | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| NOME | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| EVENTSUBJECT | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECTURL | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| SANDBOX | `'bootcamp'` |
| CONTAINERID | `''` |
| ACTIVITYID | `''` |
| PLACEMENTID | `''` |

{style="table-layout:auto"}

Para definir valores, clique no monitoramento **Editar**.

![ACOP](./images/jomsg17.png)

Em seguida, **Modo avançado**.

![ACOP](./images/jomsg18.png)

Em seguida, cole o valor com base na tabela acima. Clique em **Ok**.

![ACOP](./images/jomsg19.png)

Repita esse processo para valores para cada campo.

>[!IMPORTANT]
>
>Para o campo ECID, há uma referência ao evento`yourLastNameBeaconEntryEvent`. -se de substituir  `yourLastName` pelo seu sobrenome.

O resultado final deve ser seguido:

![ACOP](./images/jomsg20.png)

Função para cima e clique em **Ok**.

![ACOP](./images/jomsg21.png)

Você ainda precisa dar um Nome à sua jornada. Você pode fazer isso clicando no link **Propriedades** no lado superior direito da tela.

![ACOP](./images/journeyname.png)

Você pode o nome da jornada. Use `yourLastName - Beacon Entry Journey`. Clique em **OK** para proteger o cliente.

![ACOP](./images/journeyname1.png)

Agora você pode publicar sua rotina em **Publish**.

![ACOP](./images/publishjourney.png)

Clique em **Publish** novamente.

![ACOP](./images/publish1.png)

Você verá uma barra de verde informa que sua agora está Publicada.

![ACOP](./images/published.png)

Sua jornada agora está ativa e pode ser acionada.

Você terminou este exercício.

Próxima etapa: [3.4 Testa sua jornada](./ex4.md)

[Retorno para Fluxo de monitoramento 3](./uc3.md)

[Retorno para Todos os compartilhados](../../overview.md)
