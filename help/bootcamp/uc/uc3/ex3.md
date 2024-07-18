---
title: Bootcamp - Mesclagem física e digital - Journey Optimizer Crie sua jornada e notificação por push
description: Bootcamp - Mesclagem física e digital - Journey Optimizer Crie sua jornada e notificação por push
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: be8c23ec-c5f8-4abc-849f-994446072a84
source-git-commit: cd59a41f4533f18a54d80298ee9faf3a8ba3c6e7
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 1%

---

# 3.3 Criar sua jornada e notificação por push

Neste exercício, você configurará a jornada e a mensagem que precisam ser acionadas quando alguém entrar em um beacon usando o aplicativo móvel.

Faça login no Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `Bootcamp`. Para alterar a sandbox, clique em **Prod** e selecione a sandbox na lista. Neste exemplo, a sandbox é chamada **Bootcamp**. Você estará na exibição **Página inicial** da sua sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 Criar sua jornada

No menu esquerdo, clique em **Jornadas**. Em seguida, clique em **Criar Jornada** para criar uma nova jornada.

![ACOP](./images/createjourney.png)

Você verá uma tela de jornada vazia.

![ACOP](./images/journeyempty.png)

No exercício anterior, você criou um novo **Evento**. Você o nomeou desta forma `yourLastNameBeaconEntryEvent` e substituiu `yourLastName` pelo seu sobrenome. Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

Agora, é necessário tomar este evento como o início desta Jornada. Você pode fazer isso indo para o lado esquerdo da tela e procurando seu evento na lista de eventos.

![ACOP](./images/eventlist.png)

Selecione o evento, arraste e solte-o na tela de jornada. Sua jornada agora está assim. Clique em **Ok** para salvar suas alterações.

![ACOP](./images/journeyevent.png)

Como segunda etapa da jornada, você precisa adicionar uma ação **Push**. Vá para o lado esquerdo da tela para **Ações**, selecione a ação **Push** e arraste-a e solte-a no segundo nó da jornada.

![ACOP](./images/journeyactions.png)

No lado direito da tela, agora é necessário criar a notificação por push.

Defina a **Categoria** como **Marketing** e selecione uma superfície de push que permita enviar notificações por push. Nesse caso, a superfície de push a ser selecionada é **meeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Criar a mensagem

Clique em **Editar conteúdo**.

![ACOP](./images/emptymsg.png)

Você verá isto:

![ACOP](./images/emailmsglist.png)

Vamos definir o conteúdo da notificação por push.

Clique no campo de texto **Título**.

![Journey Optimizer](./images/msg5.png)

Na área de texto comece a gravar **Olá**. Clique no ícone de personalização.

![Journey Optimizer](./images/msg6.png)

Agora é necessário trazer o token de personalização para o campo **Nome**, que está armazenado em `profile.person.name.firstName`. No menu esquerdo, selecione **Atributos do Perfil**, role para baixo/navegue até encontrar o elemento **Pessoa** e clique na seta para ir um nível mais fundo até chegar ao campo `profile.person.name.firstName`. Clique no ícone **+** para adicionar o campo à tela. Clique em **Salvar**.

![Journey Optimizer](./images/msg7.png)

Você estará de volta aqui. Clique no ícone de personalização ao lado do campo **Corpo**.

![Journey Optimizer](./images/msg11.png)

Na área de texto, escreva `Welcome at the `.

![Journey Optimizer](./images/msg12.png)

Em seguida, clique em **Atributos Contextuais** e depois em **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

Clique em **Eventos**.

![ACOP](./images/jomsg4.png)

Clique no nome do evento, que deve ser semelhante a: **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

Clique em **Inserir contexto**.

![ACOP](./images/jomsg6.png)

Clique em **Interação de POI**.

![ACOP](./images/jomsg7.png)

Clique em **Detalhes do POI**.

![ACOP](./images/jomsg8.png)

Clique no ícone **+** em **Nome do POI**.
Você verá isso. Clique em **Salvar**.

![ACOP](./images/jomsg9.png)

Sua mensagem agora está pronta. Clique na seta no canto superior esquerdo para voltar à jornada.

![ACOP](./images/jomsg11.png)

Clique em **Ok**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Enviar uma mensagem para uma tela

Como terceira etapa da jornada, é necessário adicionar uma ação **sendMessageToScreen**. Vá para o lado esquerdo da tela para **Actions**, selecione a ação **sendMessageToScreen** e arraste e solte-a no terceiro nó da jornada. Você verá isso.

![ACOP](./images/jomsg15.png)

A ação **sendMessageToScreen** é uma ação personalizada que publicará uma mensagem no ponto de extremidade usado pela exibição na loja. A ação **sendMessageToScreen** espera que várias variáveis sejam definidas. Você pode ver essas variáveis rolando para baixo até ver **Parâmetros de ação**.

![ACOP](./images/jomsg16.png)

Agora é necessário definir os valores de cada parâmetro de ação. Siga esta tabela para entender quais valores são necessários e onde.

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

Para definir esses valores, clique no ícone **Editar**.

![ACOP](./images/jomsg17.png)

Em seguida, selecione **Modo Avançado**.

![ACOP](./images/jomsg18.png)

Em seguida, cole o valor com base na tabela acima. Clique em **Ok**.

![ACOP](./images/jomsg19.png)

Repita esse processo para adicionar valores a cada campo.

>[!IMPORTANT]
>
>Para o campo ECID, há uma referência ao evento `yourLastNameBeaconEntryEvent`. Substitua `yourLastName` pelo seu sobrenome.

O resultado final deve ficar assim:

![ACOP](./images/jomsg20.png)

Role para cima e clique em **Ok**.

![ACOP](./images/jomsg21.png)

Você ainda precisa dar um Nome à sua jornada. Você pode fazer isso clicando no ícone **Lápis** na parte superior esquerda da tela.

![ACOP](./images/journeyname.png)

Em seguida, você pode inserir o nome da jornada aqui. Use `yourLastName - Beacon Entry Journey`. Clique em **OK** para salvar suas alterações.

![ACOP](./images/journeyname1.png)

Agora você pode publicar sua jornada clicando em **Publish**.

![ACOP](./images/publishjourney.png)

Clique novamente em **Publish**.

![ACOP](./images/publish1.png)

Você verá uma barra de confirmação verde informando que a jornada foi publicada.

![ACOP](./images/published.png)

Sua jornada agora está ativa e pode ser acionada.

Você terminou este exercício agora.

Próxima etapa: [3.4 Testar sua jornada](./ex4.md)

[Voltar para Fluxo de Usuário 3](./uc3.md)

[Voltar a todos os módulos](../../overview.md)
