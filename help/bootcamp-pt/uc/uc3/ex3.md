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
source-wordcount: '843'
ht-degree: 0%

---

# 3.3 Promoção da notificação da jornada e da notificação

Neste exercício, você muda a jornada e a mensagem que precisa ser acionada quando uma mudança (beacon) usando o móvel.

Faça logon no Adobe Journey Optimizer acessando uma [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a da **Casa** no Journey Optimizer. Primeiro, usar você está usando o sandbox correto. O nome do sandbox que deve ser usado é `Bootcamp`. Para alternar de um sandbox para outro, clique em **Prod** e o sandbox na lista. Exemplo, o nome do sandbox é **Bootcamp**. Você na tag **Casa** da sua sandbox.`Bootcamp`

![ACOP](./images/acoptriglp.png)

## 3.3.1 Criar a sua jornada

Nenhum menu à esquerda, clique em **Jornadas**. Em seguida, clique em **Criar Jornada** para criar uma nova jornada.

![ACOP](./images/createjourney.png)

Você verá uma tela de vazia.

![ACOP](./images/journeyempty.png)

Não exercício anterior, você criou um novo **Evento**. Você conseguiu o evento `yourLastNameBeaconEntryEvent` e substituiu `yourLastName` pelo sobrenome. Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

Agora você deve este evento como o início desta Jornada. Você pode fazer o lado evento da tela e tendências pelo seu lista de eventos.

![ACOP](./images/eventlist.png)

é possível encontrar seu evento, e solte o evento na tela de jornada. Sua jornada deve ser seguido. Clique em **Ok** para analisar as alterações.

![ACOP](./images/journeyevent.png)

Como segunda etapa da jornada, você deve mudar uma ação **Push**. Vá para o lado esquerdo da tela para **Ações**, a ação **Push** e resolver a ação no segundo da jornada.

![ACOP](./images/journeyactions.png)

No lado direito da tela, agora você deve criar sua notificação push.

Defina uma **Categoria** como **Marketing** e uma superfície de push do push. Nesse caso, uma seleção de push a ser é **mmeeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Criar a sua mensagem

Clique em **Editar conteúdo**.

![ACOP](./images/emptymsg.png)

Em seguida, a tela abaixo é apresentada:

![ACOP](./images/emailmsglist.png)

Vamos definir a notificação da notificação.

Clique no campo de texto **Título**.

![Journey Optimizer](./images/msg5.png)

Na área de texto, **Olá**. Clique em nenhum momento personalizado.

![Journey Optimizer](./images/msg6.png)

Agora rara o token de personalização para o campo **Primeiro nome** que está doente em `profile.person.name.firstName`. Nenhum menu à esquerda, hierarquia **Atributos de perfil**, função para baixo/navegue para encontrar o elemento **Pessoa** e clique na posição para resolver um até chegar ao campo `profile.person.name.firstName`. Clique no domínio **+** para corrigir o campo à tela. Clique em **Salvar**.

![Journey Optimizer](./images/msg7.png)

Então, você muda para esta tela. Clique no domínio da personalização ao lado do **Corpo**.

![Journey Optimizer](./images/msg11.png)

Na área de texto, escreva `Bem-vindo(a)`.

![Journey Optimizer](./images/msg12.png)

Em seguida, clique em **Atributos Contextuais** e **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

Clique em **Eventos**.

![ACOP](./images/jomsg4.png)

Clique em nome no nome event, que deve ser visto do seu seguinte: **yourNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

Clique em **Inserir contexto**.

![ACOP](./images/jomsg6.png)

Clique em **Interação POI**.

![ACOP](./images/jomsg7.png)

Clique em **Detalhes do POI**.

![ACOP](./images/jomsg8.png)

Clique no ícone **+** no **Nome do POI**.
Em seguida, o seguinte é apresentado. Clique em **Salvar**.

![ACOP](./images/jomsg9.png)

Sua mensagem está pronta. Clique na seta no canto superior para acompanhar a sua jornada.

![ACOP](./images/jomsg11.png)

Clique em **Ok**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Envie uma mensagem para uma tela

Como terceira etapa da jornada, você deve mudar uma ação **sendMessageToScreen**. Vá para o lado esquerdo da tela para **Ações**, a ação **sendToScreen** e e solte a ação no terceiro da sua jornada. Em seguida, você verá a tela abaixo.

![ACOP](./images/jomsg15.png)

**sendMessageToScreen** é uma ação personalizada que irá publicar uma mensagem no **Endpoint** usado pela na loja. A ação **sendMessageTo** que movimenta a tela. Você pode mudar as escolhas rolando para baixo até **Parâmetros de ação**.

![ACOP](./images/jomsg16.png)

1999 &quot;Agora você precisa de acordo com as regras para cada domínio da ação&quot; . Fórum de dúvidas sobre o assunto...

| Parâmetro | valor |
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

Para definir valores, clique no **Editar**.

![ACOP](./images/jomsg17.png)

Em seguida, **Modo Avançado**.

![ACOP](./images/jomsg18.png)

Em seguida, cole o valor com base na tabela acima. Clique em **Ok**.

![ACOP](./images/jomsg19.png)

Repita esse processo para valores para cada campo.

>[!IMPORTANT]
>
>Para o campo ECID, há uma referência ao evento`yourLastNameBeaconEntryEvent`. Folha-se de `yourLastName` pelo seu sobrenome.

O resultado final deve ser seguido:

![ACOP](./images/jomsg20.png)

Função para cima e clique em **Ok**.

![ACOP](./images/jomsg21.png)

Você ainda precisa dar um Nome à sua jornada. Você pode fazer isso clicando no ícone **Propriedades** na parte superior direita da tela.

![ACOP](./images/journeyname.png)

Você pode o nome da jornada. Usar `yourLastName - Beacon Entry Journey`. Clique em **OK** para analisar as alterações.

![ACOP](./images/journeyname1.png)

Agora você pode publicar sua rotina em **Publish**.

![ACOP](./images/publishjourney.png)

Clique em **Publish** novamente.

![ACOP](./images/publish1.png)

Você verá uma barra de verde informa que sua agora está Publicada.

![ACOP](./images/published.png)

Sua jornada agora está ativa e pode ser acionada.

Você terminou este exercício.

Próxima etapa: [3.4 Teste sua jornada](./ex4.md)

[Retorno para Fluxo de monitoramento 3](./uc3.md)

[Retorno para Todos os compartilhados](../../overview.md)
