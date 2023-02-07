---
title: Bootcamp - Mesclando físico e digital - Journey Optimizer Crie sua jornada e envie - Notificação do Brasil
description: Bootcamp - Mesclando físico e digital - Journey Optimizer Crie sua jornada e envie - Notificação do Brasil
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 5d824244766135cd4998feab48be7f6a69c42a70
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 2%

---

# 3.3 Notificação por push da sua jornada

Você vai configurar uma jornada e a mensagem que é, é, quando alguém inserir uma sinalização (beacon) usando o aplicativo móvel.

Faça logon sem acesso ao Adobe Journey Optimizer [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecion para a visualização da **Início** sem Journey Optimizer. Primeiro, verifique está usando caixa de proteção. O nome do fenômeno da sandbox que é usado `Bootcamp`. Para alternar de um sandbox para, clique em **Prod** e selecione a sandbox na lista. exemplo, o nome do sandbox é **Bootcamp**. Você estará na visualização da **Início**  fazer sua sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 Cristo da sua jornada

Sem menu à esquerda, clique em **Jornada**. Em **Criar Jornada** para jornada.

![ACOP](./images/createjourney.png)

Você verá uma tela de jornada vazia.

![ACOP](./images/journeyempty.png)

Sem exercício anterior, você criou um novo **Evento**. Você nomeou ou evento `yourLastNameBeaconEntryEvent` e substituiu `yourLastName` pelo seu sobrenome. Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

Agora você considerar este como a desta Jornada. Você pode fazer &quot; isso lado esquerdo da tela para o evento na lista de eventos.

![ACOP](./images/eventlist.png)

Selecione evento, arraste e solte o evento na tela de jornada. Sua jornada agora é um fenômeno semelhante ao seguinte. Clique em **Ok** para salvar suas alterações.

![ACOP](./images/journeyevent.png)

Como da jornada, você acha uma obra **Empurrar**. Vá para o lado esquerdo da tela **Ações** selecione uma ação **Empurrar** e arraste e solte a ação no segundo nó da jornada.

![ACOP](./images/journeyactions.png)

Não consta do relatório da Comissão, agora é empurrada sua notificação.

Defina a **Categoria** como **Marketing** e selecione um empurrar superfície que notificações empurrar. é caso, superfície push a ser selecionada **mmeeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Crie um seu canal

Clique em **Editar conteúdo**.

![ACOP](./images/emptymsg.png)

Em, tela exibida

![ACOP](./images/emailmsglist.png)

Vamos definir para conteúdo notificação por push.

Clique sem campo de texto **Título**.

![Journey Optimizer](./images/msg5.png)

Na cor da texto, comece **Hello**. Clique no ícone de personalização.

![Journey Optimizer](./images/msg6.png)

Agora você trazer token de personalização para o campo **Nome** que está armazenado `profile.person.name.firstName`. Sem menu à esquerda, selecione **Atributos do perfil**, o papel para baixo/navegue para o elemento **Pessoa** e panelinha na sede avançar um campo chegar `profile.person.name.firstName`. Clique em ícone **+** para campo à tela. Clique em **Salvar**.

![Journey Optimizer](./images/msg7.png)

Então, você vai retornar para esta tela. Clique no ícone de personalização ao lado do campo **Corpo**.

![Journey Optimizer](./images/msg11.png)

Na cor da texto, escreva `Bem-vindo(a)`.

![Journey Optimizer](./images/msg12.png)

Em  **Atributos contextuais** e **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

Clique em **Eventos**.

![ACOP](./images/jomsg4.png)

Clique no nome do seu evento, que é semelhante ao seguinte: **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

Clique em **Inserir contexto**.

![ACOP](./images/jomsg6.png)

Clique em **Interação de POI**.

![ACOP](./images/jomsg7.png)

Clique em **Detalhes do POI**.

![ACOP](./images/jomsg8.png)

Clique em **+** ícone no **Nome do POI**.
Em, seguinte. Clique em **Salvar**.

![ACOP](./images/jomsg9.png)

Sua agora! Clique na seta no canto superior esquerdo para retornar à sua jornada.

![ACOP](./images/jomsg11.png)

Clique em **Ok**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Envie uma para tela

Como é a jornada, você é uma obra.  **sendMessageToScreen**. Vá para o lado esquerdo da tela **Ações** selecione uma ação **sendMessageToScreen** e arraste e solte a ação no terceiro nó da sua jornada. Em, você vê a tela.

![ACOP](./images/jomsg15.png)

**sendMessageToScreen** é uma personque vai publicar uma mensagem **Endpoint** Usada pela exibição na loja. Uma ação **sendMessageToScreen** que múltiplas variáveis sejam definidas. Você visualizar essas variáveis rolando para baixo ver **Parâmetros de ação**.

![ACOP](./images/jomsg16.png)

Agora você definir os valores para cada parâmetro de ação. Siga esta tabela para entender, são necessários e onde.

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

Para definir bagunça valores clique em ícone **Editar**.

![ACOP](./images/jomsg17.png)

selecione **Modo avançado**.

![ACOP](./images/jomsg18.png)

Em, cole o valor com. Clique em **Ok**.

![ACOP](./images/jomsg19.png)

Repita Processesse para valores para cada campo.

>[!IMPORTANT]
>
>Para o campo ECID, há uma referência ao evento`yourLastNameBeaconEntryEvent`. Lembre-se de substituir  `yourLastName` pelo seu sobrenome.

O resultado último fenômeno semelhante ao seguinte:

![ACOP](./images/jomsg20.png)

Papel para cima e clique em **Ok**.

![ACOP](./images/jomsg21.png)

Você ainda precisa dar um Nome à sua jornada. Você pode fazer isso clicando no botão **Propriedades** no lado superior direito da tela.

![ACOP](./images/journeyname.png)

Você inserir o nome da jornada aqui. Use `yourLastName - Beacon Entry Journey`. Clique em **OK** para salvar suas alterações.

![ACOP](./images/journeyname1.png)

Agora você publicar sua jornada clicando **Publicar**.

![ACOP](./images/publishjourney.png)

Clique em **Publicar** Data

![ACOP](./images/publish1.png)

Você verá uma barra de confirmação verde informando que sua jornada agora está publicada.

![ACOP](./images/published.png)

Sua jornada agora está ativa e pode ser acionada.

Você terminou este.

Proxima. [3.4 Teste da sua jornada](./ex4.md)

[Retornar para Fluxo 3](./uc3.md)

[Retornar para Todos os Módulos](../../overview.md)
