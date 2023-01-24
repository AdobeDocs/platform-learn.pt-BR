---
title: Bootcamp - Mesclando físico e digital - Journey Optimizer Crie sua jornada e envie - Notificação do Brasil
description: Bootcamp - Mesclando físico e digital - Journey Optimizer Crie sua jornada e envie - Notificação do Brasil
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 3%

---

# 3.3 Criar sua jornada e notificação por push

Neste exercício, você configurará a jornada e a mensagem que precisam ser acionadas quando alguém entrar em um sinal usando o aplicativo móvel.

Faça logon no Adobe Journey Optimizer acessando [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para o **Início**  no Journey Optimizer. Primeiro, certifique-se de usar a sandbox correta. A sandbox a ser usada é chamada de `Bootcamp`. Para alterar de uma sandbox para outra, clique em **Prod** e selecione a sandbox na lista. Neste exemplo, a sandbox é chamada de **Bootcamp**. Você estará no **Início** exibição da sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 Criar a jornada

No menu esquerdo, clique em **Jornada**. Em seguida, clique em **Criar Jornada** para criar uma nova jornada.

![ACOP](./images/createjourney.png)

Você verá uma tela de jornada vazia.

![ACOP](./images/journeyempty.png)

No exercício anterior, você criou um novo **Evento**. Você o nomeou assim `yourLastNameBeaconEntryEvent` e substituído `yourLastName` com seu sobrenome. Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

Agora é necessário tomar esse evento como o início desta Jornada. Você pode fazer isso indo para o lado esquerdo da tela e procurando pelo evento na lista de eventos.

![ACOP](./images/eventlist.png)

Selecione seu evento, arraste-o e solte-o na tela de jornada. Sua jornada agora fica assim. Clique em **Ok** para salvar as alterações.

![ACOP](./images/journeyevent.png)

Como a segunda etapa da jornada, é necessário adicionar um **Empurrar** ação. Vá para o lado esquerdo da tela para **Ações**, selecione o **Empurrar** , em seguida, arraste e solte no segundo nó da jornada.

![ACOP](./images/journeyactions.png)

No lado direito da tela, agora é necessário criar a notificação por push.

Defina as **Categoria** para **Marketing** e selecione uma superfície de push que permite enviar notificações por push. Nesse caso, a superfície de pressão a ser selecionada é **mmeeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Criar sua mensagem

Clique em **Editar conteúdo**.

![ACOP](./images/emptymsg.png)

Você verá isso:

![ACOP](./images/emailmsglist.png)

Vamos definir o conteúdo da notificação por push.

Clique no botão **Título** campo de texto.

![Journey Optimizer](./images/msg5.png)

Na área de texto, comece a escrever **Oi**. Clique no ícone de personalização.

![Journey Optimizer](./images/msg6.png)

Agora é necessário trazer o token de personalização para o campo **Nome** armazenado em `profile.person.name.firstName`. No menu esquerdo, selecione **Atributos do perfil**, role para baixo/navegue até encontrar a variável **Pessoa** e clique na seta para ir um nível mais fundo até atingir o campo `profile.person.name.firstName`. Clique no botão **+** ícone para adicionar o campo à tela. Clique em **Salvar**.

![Journey Optimizer](./images/msg7.png)

Então você estará de volta. Clique no ícone de personalização ao lado do campo **Corpo**.

![Journey Optimizer](./images/msg11.png)

Na área de texto, escreva `Welcome at the `.

![Journey Optimizer](./images/msg12.png)

Em seguida, clique em **Atributos contextuais** e depois **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

Clique em **Eventos**.

![ACOP](./images/jomsg4.png)

Clique no nome do evento, que deve ter a seguinte aparência: **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

Clique em **Inserir contexto**.

![ACOP](./images/jomsg6.png)

Clique em **Interação de POI**.

![ACOP](./images/jomsg7.png)

Clique em **Detalhes do POI**.

![ACOP](./images/jomsg8.png)

Clique no botão **+** ícone ligado **Nome do POI**.
Você verá isso. Clique em **Salvar**.

![ACOP](./images/jomsg9.png)

Sua mensagem está pronta. Clique na seta no canto superior esquerdo para retornar à jornada.

![ACOP](./images/jomsg11.png)

Clique em **Ok**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Enviar uma mensagem para uma tela

Como a terceira etapa da jornada, é necessário adicionar um **sendMessageToScreen** ação. Vá para o lado esquerdo da tela para **Ações**, selecione o **sendMessageToScreen** , em seguida, arraste e solte no terceiro nó da jornada. Você verá isso.

![ACOP](./images/jomsg15.png)

O **sendMessageToScreen** ação é uma ação personalizada que publicará uma mensagem no endpoint usada pela exibição na loja. O **sendMessageToScreen** espera que várias variáveis sejam definidas. Você pode ver essas variáveis ao rolar para baixo até ver **Parâmetros de ação**.

![ACOP](./images/jomsg16.png)

Agora é necessário definir os valores para cada parâmetro de ação. Siga esta tabela para entender quais valores são exigidos em qualquer lugar.

| Parâmetro | Valor de  |
|:-------------:| :---------------:|
| DELIVERY | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| PRIMEIRO NOME | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| EVENTSUBJECT | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECTURL | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| SANDBOX | `'bootcamp'` |
| CONTAINERID | `''` |
| ACTIVITYID | `''` |
| PLACEMENTID | `''` |

{style=&quot;table-layout:auto&quot;}

Para definir esses valores, clique no botão **Editar** ícone .

![ACOP](./images/jomsg17.png)

Em seguida, selecione **Modo avançado**.

![ACOP](./images/jomsg18.png)

Em seguida, cole o valor com base na tabela acima. Clique em **Ok**.

![ACOP](./images/jomsg19.png)

Repita esse processo para adicionar valores para cada campo.

>[!IMPORTANT]
>
>Para o campo ECID, há uma referência para o evento `yourLastNameBeaconEntryEvent`. Certifique-se de substituir `yourLastName` pelo seu sobrenome.

O resultado final deve ficar assim:

![ACOP](./images/jomsg20.png)

Role para cima e clique **Ok**.

![ACOP](./images/jomsg21.png)

Você ainda precisa dar um Nome à sua jornada. Você pode fazer isso clicando no botão **Propriedades** no lado superior direito da tela.

![ACOP](./images/journeyname.png)

Você pode então inserir o nome da jornada aqui. Use `yourLastName - Beacon Entry Journey`. Clique em **OK** para salvar as alterações.

![ACOP](./images/journeyname1.png)

Agora você pode publicar sua jornada clicando em **Publicar**.

![ACOP](./images/publishjourney.png)

Clique em **Publicar** novamente.

![ACOP](./images/publish1.png)

Em seguida, você verá uma barra de confirmação verde informando que sua jornada foi publicada.

![ACOP](./images/published.png)

Sua jornada agora está ativa e pode ser acionada.

Você já terminou este exercício.

Próxima etapa: [3.4 Teste sua jornada](./ex4.md)

[Voltar para Fluxo de Usuário 3](./uc3.md)

[Voltar para todos os módulos](../../overview.md)
