---
title: Criar e enviar notificações por push
description: Saiba como criar notificações por push para um aplicativo móvel com o SDK móvel da plataforma e o Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Push
hide: true
exl-id: 37d5b52e-c0d0-4ca1-9629-5c3dd2b2a5d5
source-git-commit: 5d34e510ef72190762c29b71359b362ef4be7b22
workflow-type: tm+mt
source-wordcount: '2734'
ht-degree: 2%

---

# Criar e enviar notificações por push

Saiba como criar notificações por push para aplicativos móveis com o SDK móvel do Experience Platform e o Journey Optimizer.

O Journey Optimizer permite criar jornadas e enviar mensagens para públicos-alvo direcionados. Antes de enviar notificações por push com o Journey Optimizer, você deve garantir que as configurações e integrações adequadas estejam em vigor. Para entender o fluxo de dados de notificações por push no Journey Optimizer, consulte [documentação](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-gs.html).

![Arquitetura](assets/architecture-ajo.png)

>[!NOTE]
>
>Essa lição é opcional e se aplica somente aos usuários do Journey Optimizer que desejam enviar notificações por push.


## Pré-requisitos

* O aplicativo foi criado e executado com sucesso com SDKs instalados e configurados.
* Configure o aplicativo para Adobe Experience Platform.
* Acesso ao Journey Optimizer e permissões suficientes, conforme descrito [aqui](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). Além disso, você precisa de permissão suficiente para os seguintes recursos do Journey Optimizer.
   * Crie uma superfície de aplicativo.
   * Criar uma jornada.
   * Criar uma mensagem.
   * Criar predefinições de mensagem.
* Conta de desenvolvedor paga do Apple com acesso suficiente para criar certificados, identificadores e chaves.
* Dispositivo ou simulador físico iOS para teste.

## Objetivos de aprendizagem

Nesta lição, você

* Registre a ID do aplicativo com o serviço de notificação por push (APNs) da Apple.
* Crie uma superfície de aplicativo no Journey Optimizer.
* Atualize seu esquema para incluir campos de mensagens de push.
* Instale e configure a extensão de tag da Journey Optimizer.
* Atualize seu aplicativo para registrar a extensão de tag da Journey Optimizer.
* Valide a configuração no Assurance.
* Enviar uma mensagem de teste do Assurance
* Defina seu próprio evento de notificação por push, jornada e experiência no Journey Optimizer.
* Envie sua própria notificação por push de dentro do aplicativo.


## Configuração

>[!TIP]
>
>Se você já configurou o ambiente como parte da [Mensagens no aplicativo do Journey Optimizer](journey-optimizer-inapp.md) lição, talvez você já tenha executado algumas etapas nesta seção de configuração.

### Registrar ID do aplicativo com APNs

As etapas a seguir não são específicas do Adobe Experience Cloud e foram projetadas para orientá-lo pela configuração de APNs.

#### Criar uma chave privada

1. No portal do desenvolvedor do Apple, navegue até **[!UICONTROL Chaves]**.
1. Para criar uma chave, selecione **[!UICONTROL +]**.
   ![criar nova chave](assets/mobile-push-apple-dev-new-key.png)

1. Forneça um **[!UICONTROL Nome da chave]**.
1. Selecione o **[!UICONTROL Serviço de notificação por push da Apple] (APNs)** caixa de seleção
1. Selecionar **[!UICONTROL Continuar]**.
   ![configurar nova chave](assets/mobile-push-apple-dev-config-key.png)
1. Revise a configuração e selecione **[!UICONTROL Registrar]**.
1. Baixe o `.p8` chave privada. Ela é usada na configuração da Superfície do aplicativo posteriormente nesta lição.
1. Anote o **[!UICONTROL ID da chave]**. É usado na configuração da Superfície do aplicativo.
1. Anote o **[!UICONTROL ID da equipe]**. É usado na configuração da Superfície do aplicativo.
   ![Detalhes da chave](assets/push-apple-dev-key-details.png)

A documentação adicional pode ser [encontrado aqui](https://help.apple.com/developer-account/#/devcdfbb56a3).

#### Adicionar uma superfície de aplicativo na Coleção de dados

1. No [Interface da coleção de dados](https://experience.adobe.com/br/data-collection/), selecione **[!UICONTROL Superfícies do aplicativo]** no painel esquerdo.
1. Para criar uma configuração, selecione **[!UICONTROL Criar superfície do aplicativo]**.
   ![página inicial da superfície de aplicativo](assets/push-app-surface.png)
1. Insira um **[!UICONTROL Nome]** para a configuração do, por exemplo `Luma App Tutorial`  .
1. De **[!UICONTROL Configuração do aplicativo móvel]**, selecione **[!UICONTROL Apple iOS]**.
1. Insira a ID do pacote do aplicativo móvel na **[!UICONTROL ID do aplicativo (ID do pacote iOS)]** campo. Por exemplo,  `com.adobe.luma.tutorial.swiftui`.
1. Ligue o **[!UICONTROL Credenciais por push]** para adicionar suas credenciais.
1. Arraste e solte o `.p8` **Chave de autenticação da notificação por push do Apple** arquivo.
1. Forneça o **[!UICONTROL ID da chave]**, uma sequência de 10 caracteres atribuída durante a criação de `p8` chave de autenticação. Ele pode ser encontrado no campo **[!UICONTROL Chaves]** na guia **Certificados, identificadores e perfis** página das páginas do portal Apple Developer. Consulte também [Criar uma chave privada](#create-a-private-key).
1. Forneça o **[!UICONTROL ID da equipe]**. A ID da equipe é um valor que pode ser encontrado na variável **Associação** ou na parte superior da página do portal Apple Developer. Consulte também [Criar uma chave privada](#create-a-private-key).
1. Selecione **[!UICONTROL Salvar]**.

   ![configuração da superfície do aplicativo](assets/push-app-surface-config.png)

### Atualizar configuração da sequência de dados

Para garantir que os dados enviados do aplicativo móvel para a Rede de borda sejam encaminhados para a Journey Optimizer, atualize a configuração da Experience Edge.

1. Na interface da Coleção de dados, selecione **[!UICONTROL Datastreams]** e selecione seu fluxo de dados, por exemplo **[!DNL Luma Mobile App]**.
1. Selecionar ![Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) para **[!UICONTROL Experience Platform]** e selecione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Editar]** no menu de contexto.
1. No **[!UICONTROL Datastreams]** > ![Pasta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) >  **[!UICONTROL Adobe Experience Platform]** tela:

   1. Se ainda não estiver selecionado, selecione **[!UICONTROL Conjunto de dados do perfil de push do AJO]** de **[!UICONTROL Conjunto de dados do perfil]**. Este conjunto de dados de perfil é necessário ao usar o `MobileCore.setPushIdentifier` Chamada de API (consulte [Registrar token de dispositivo para notificações por push](#register-device-token-for-push-notifications)), que garante que o identificador exclusivo de notificações por push (também conhecido como identificador por push) seja armazenado como parte do perfil do usuário.

   1. **[!UICONTROL Adobe Journey Optimizer]** está selecionada. Consulte [Configurações do Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#aep) para obter mais informações.

   1. Para salvar a configuração do fluxo de dados, selecione **[!UICONTROL Salvar]**.

   ![Configuração da sequência de dados da AEP](assets/datastream-aep-configuration.png)



### Instalar extensão de tags do Journey Optimizer

Para que seu aplicativo funcione com a Journey Optimizer, é necessário atualizar a propriedade da tag.

1. Navegue até **[!UICONTROL Tags]** > **[!UICONTROL Extensões]** > **[!UICONTROL Catálogo]**,
1. Abra a propriedade, por exemplo **[!DNL Luma Mobile App Tutorial]**.
1. Selecionar **[!UICONTROL Catálogo]**.
1. Procure por **[!UICONTROL Adobe Journey Optimizer]** extensão.
1. Instale a extensão.
1. No **[!UICONTROL Instalar extensão]** caixa de diálogo
   1. Selecione um ambiente, por exemplo **[!UICONTROL Desenvolvimento]**.
   1. Selecione o **[!UICONTROL Conjunto de dados do evento de experiência de rastreamento de push do AJO]** conjunto de dados da **[!UICONTROL Conjunto de dados do evento]** lista.
   1. Selecionar **[!UICONTROL Salvar na biblioteca e criar]**.
      ![Configurações de extensão do AJO](assets/push-tags-ajo.png)

>[!NOTE]
>
>Se você não vir **[!UICONTROL Conjunto de dados do evento de experiência de rastreamento de push do AJO]** como opção, entre em contato com o atendimento ao cliente.
>

## Validar configuração com o Assurance

1. Revise o [instruções de configuração](assurance.md#connecting-to-a-session) seção para conectar seu simulador ou dispositivo ao Assurance.
1. Na interface do usuário do Assurance, selecione **[!UICONTROL Configurar]**.
   ![configurar clique](assets/push-validate-config.png)
1. Selecionar ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) ao lado de **[!UICONTROL Depuração push]**.
1. Selecione **[!UICONTROL Salvar]**.
   ![save](assets/push-validate-save.png)
1. Selecionar **[!UICONTROL Depuração push]** no painel de navegação esquerdo.
1. Selecione o **[!UICONTROL Validar configuração]** guia.
1. Selecione seu dispositivo na **[!UICONTROL Cliente]** lista.
1. Confirme se não está recebendo erros.
   ![validar](assets/push-validate-confirm.png)
1. Selecione o **[!UICONTROL Enviar push de teste]** guia.
1. (opcional) Altere os detalhes padrão para **[!UICONTROL Título]** e **[!UICONTROL Corpo]**
1. Selecionar ![Bug](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bug_18_N.svg) **[!UICONTROL Enviar notificação por push de teste]**.
1. Verifique a **[!UICONTROL Resultados do teste]**.
1. Você deve ver a notificação por push de teste aparecer no aplicativo.

   <img src="assets/luma-app-push.png" width="300" />


## Assinatura

A assinatura do aplicativo Luma é necessária somente para o [Criar e enviar notificações por push](journey-optimizer-push.md) e a variável [Criar e enviar mensagens no aplicativo](journey-optimizer-inapp.md) lições neste tutorial. Essas lições exigem um perfil de provisionamento do Apple que **requer uma conta paga de desenvolvedor do Apple**.

Para atualizar a assinatura do seu aplicativo:

1. Acesse seu aplicativo no Xcode.
1. Selecionar **[!DNL Luma]** no Navegador de projetos.
1. Selecione o **[!DNL Luma]** público-alvo.
1. Selecione o **Assinatura e recursos** guia.
1. Configurar **[!UICONTROL Gerenciar assinatura automaticamente]**, **[!UICONTROL Equipe]**, e **[!UICONTROL Identificador do pacote]** ou use seus detalhes específicos de provisionamento de desenvolvimento do Apple.

   >[!IMPORTANT]
   >
   >Certifique-se de usar um _único_ identificador do pacote e substitua o `com.adobe.luma.tutorial.swiftui` identificador de pacote, pois cada identificador de pacote precisa ser exclusivo. Normalmente, você usa um formato de DNS reverso para sequências de ID de pacote, como `com.organization.brand.uniqueidentifier`. A versão Concluída deste tutorial, por exemplo, usa `com.adobe.luma.tutorial.swiftui`.


   ![Recursos de assinatura do Xcode](assets/xcode-signing-capabilities.png){zoom=&quot;yes&quot;}


## Adicionar recursos de notificação por push ao seu aplicativo

>[!IMPORTANT]
>
>Para implementar e testar a notificação por push em um aplicativo iOS, você deve ter uma **pago** Conta de desenvolvedor do Apple. Se você não tiver uma conta paga de desenvolvedor do Apple, ignore o restante desta lição.

1. No Xcode, selecione **[!DNL Luma]** do **[!UICONTROL METAS]** , selecione a **[!UICONTROL Assinatura e recursos]** , selecione a **[!UICONTROL + Recurso]** e selecione **[!UICONTROL Notificações por push]**. Isso permitirá que seu aplicativo receba notificações por push.

1. Em seguida, será necessário adicionar uma Extensão de notificação ao aplicativo. Volte para o **[!DNL General]** e selecione a guia **[!UICONTROL +]** ícone na parte inferior da **[!UICONTROL METAS]** seção.

1. Você será solicitado a selecionar o modelo para seu novo alvo. Selecionar **[!UICONTROL Extensão de Serviço de Notificação]** e selecione **[!UICONTROL Próxima]**.

1. Na próxima janela, use `NotificationExtension` como o nome da extensão e clique no botão **[!UICONTROL Concluir]** botão.

Agora você deve ter uma extensão de notificação por push adicionada ao seu aplicativo, semelhante à tela abaixo.

![Extensão de notificações por push](assets/xcode-signing-capabilities-pushnotifications.png)


## Implementar o Journey Optimizer no aplicativo

Conforme discutido nas lições anteriores, a instalação de uma extensão de tag móvel fornece apenas a configuração. Em seguida, você deve instalar e registrar o SDK de mensagens. Se essas etapas não estiverem claras, revise o [Instalar SDKs](install-sdks.md) seção.

>[!NOTE]
>
>Se você concluiu o [Instalar SDKs](install-sdks.md) , o SDK já estará instalado e você poderá ignorar essa etapa.
>

1. No Xcode, verifique se [Mensagens AEP](https://github.com/adobe/aepsdk-messaging-ios.git) é adicionado à lista de pacotes nas Dependências de pacote. Consulte [Gerenciador de pacotes Swift](install-sdks.md#swift-package-manager).
1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]** no navegador do Projeto Xcode.
1. Assegurar `AEPMessaging` faz parte da lista de importações.

   `import AEPMessaging`

1. Assegurar `Messaging.self` O faz parte da matriz de extensões que você está registrando.

   ```swift
   let extensions = [
       AEPIdentity.Identity.self,
       Lifecycle.self,
       Signal.self,
       Edge.self,
       AEPEdgeIdentity.Identity.self,
       Consent.self,
       UserProfile.self,
       Places.self,
       Messaging.self,
       Optimize.self,
       Assurance.self
   ]
   ```

## Registrar token de dispositivo para notificações por push

1. Adicione o [`MobileCore.setPushIdentifier`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setpushidentifier) API para o `func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data)` função.

   ```swift
   // Send push token to Mobile SDK
   MobileCore.setPushIdentifier(deviceToken)
   ```

   Essa função recupera o token do dispositivo exclusivo para o dispositivo no qual o aplicativo está instalado. Em seguida, define o token para delivery de notificação por push usando a configuração definida e que depende do Serviço de notificação por push (APNs) da Apple.

>[!IMPORTANT]
>
>A variável `MobileCore.updateConfigurationWith(configDict: ["messaging.useSandbox": true])` determina se as notificações por push estão usando uma sandbox APNs ou um servidor de produção para enviar notificações por push. Ao testar seu aplicativo no simulador ou em um dispositivo, verifique se `messaging.useSandbox` está definida como `true` para que você receba notificações por push. Ao implantar seu aplicativo para produção a ser testada usando o Testflight da Apple, verifique se definiu `messaging.useSandbox` para `false` caso contrário, seu aplicativo de produção não poderá receber notificações por push.


## Criar sua própria notificação por push

Para criar sua própria notificação por push, você deve definir um evento no Journey Optimizer que acione uma jornada que controle o envio de uma notificação por push.

### Atualizar seu esquema

Você definirá um novo tipo de evento, ainda não disponível como parte da lista de eventos definidos no esquema. Você usará esse tipo de evento posteriormente ao acionar notificações por push.

1. Na interface do Journey Optimizer, selecione **[!UICONTROL Esquemas]** do painel esquerdo.
1. Selecionar **[!UICONTROL Procurar]** na barra de guias.
1. Selecione seu esquema, por exemplo **[!DNL Luma Mobile App Event Schema]** para abri-lo.
1. No Editor de esquemas:
   1. Selecione o **[!UICONTROL eventType]** campo.
   1. No **[!UICONTROL Propriedades do campo]** rolar para baixo para ver a lista de valores possíveis para o tipo de evento. Selecionar **[!UICONTROL Adicionar linha]**, e adicione `application.test` como o **[!UICONTROL VALOR]** e `[!UICONTROL Test event for push notification]` como o `DISPLAY NAME`.
   1. Selecione **[!UICONTROL Aplicar]**.
   1. Selecione **[!UICONTROL Salvar]**.
      ![Adicionar valor a tipos de evento](assets/ajo-update-schema-eventtype-enum.png)

### Definir um evento

Os eventos no Journey Optimizer permitem acionar as jornadas de forma unitária para enviar mensagens, como por exemplo notificações por push. Consulte [Sobre eventos](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configure-journeys/events-journeys/about-events.html?lang=en) para obter mais informações.

1. Na interface do Journey Optimizer, selecione **[!UICONTROL Configurações]** do painel esquerdo.

1. No **[!UICONTROL Painel]** , selecione a **[!UICONTROL Gerenciar]** botão na caixa **[!UICONTROL Eventos]** bloco.

1. No **[!UICONTROL Eventos]** , selecione **[!UICONTROL Criar evento]**.

1. No **[!UICONTROL Editar event1]** painel:

   1. Enter `LumaTestEvent` como o **[!UICONTROL Nome]** do evento.
   1. Forneça um **[!UICONTROL Descrição]**, por exemplo `Test event to trigger push notifications in Luma app`.

   1. Selecione o esquema de evento de experiência de aplicativo móvel criado anteriormente no [Criar um esquema XDM](create-schema.md) do **[!UICONTROL Esquema]** lista, por exemplo **[!DNL Luma Mobile App Event Schema v.1]**.
   1. Selecionar ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) ao lado da **[!UICONTROL Campos]** lista.

      ![Editar etapa 1 do evento](assets/ajo-edit-event1.png)

      No **[!UICONTROL Campos]** , verifique se os seguintes campos estão selecionados (sobre os campos padrão que estão sempre selecionados (**[!UICONTROL _id]**, **[!UICONTROL id]**, e **[!UICONTROL carimbo de data e hora]**). Você pode alternar, usando a lista suspensa, entre **[!UICONTROL Selecionado]**, **[!UICONTROL Todos]** e **[!UICONTROL Principal]** ou use o ![Pesquisar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) campo.

      * **[!UICONTROL Aplicativo identificado (id)]**,
      * **[!UICONTROL Tipo de evento (eventType)]**,
      * **[!UICONTROL Principal (primary)]**.

      ![Editar campos de evento](assets/ajo-event-fields.png)

      Em seguida, selecione **[!UICONTROL Ok]**.

   1. Selecionar ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) ao lado da **[!UICONTROL Condição de id de evento]** campo.

      1. No **[!UICONTROL Adicionar uma condição de id de evento]** , arraste e solte **[!UICONTROL Tipo de evento (eventType)]** em para **[!UICONTROL Arraste e solte um elemento aqui]**.
      1. No popover, role até a parte inferior e selecione **[!UICONTROL application.test]** (que é o tipo de evento adicionado anteriormente à lista de tipos de evento como parte de [Atualizar seu esquema](#update-your-schema)). Em seguida, role para cima e selecione **[!UICONTROL Ok]**.
      1. Selecionar **[!UICONTROL Ok]** para salvar a condição.
         ![Editar condição de evento](assets/ajo-edit-condition.png)

   1. Selecionar **[!UICONTROL ECID (ECID)]** do **[!UICONTROL Namespace]** lista. Automaticamente, o **[!UICONTROL Identificador de perfil]** o campo é preenchido com **[!UICONTROL A ID do primeiro elemento da chave ECID para o mapa identityMap]**.
   1. Selecione **[!UICONTROL Salvar]**.
      ![Editar etapa 2 do evento](assets/ajo-edit-event2.png)

Você acabou de criar uma configuração de evento baseada no schema de eventos de experiência do aplicativo móvel criado anteriormente como parte deste tutorial. Essa configuração de evento filtrará os eventos de experiência recebidos usando seu tipo de evento específico (`application.test`), para garantir que apenas eventos com esse tipo específico, iniciados a partir do aplicativo móvel, acionarão a jornada que você criou na próxima etapa. Em um cenário real, talvez você queira enviar notificações por push de um serviço externo, no entanto, os mesmos conceitos se aplicam: no aplicativo externo, envie um evento de experiência para o Experience Platform que tem campos específicos que você pode usar para aplicar condições antes que esses eventos acionem uma jornada.

### Criar a jornada

A próxima etapa é criar a jornada que aciona o envio da notificação por push ao receber o evento apropriado.

1. Na interface do Journey Optimizer, selecione **[!UICONTROL Jornadas]** do painel esquerdo.
1. Selecionar **[!UICONTROL Criar Jornada]**.
1. No **[!UICONTROL Jornada propriedades]** painel:

   1. Insira um **[!UICONTROL Nome]** para a jornada, por exemplo `Luma - Test Push Notification Journey`.
   1. Insira um **[!UICONTROL Descrição]** para a jornada, por exemplo `Journey for test push notifications in Luma mobile app`.
   1. Assegurar **[!UICONTROL Permitir reentrada]** está selecionado e definido **[!UICONTROL Período de espera de reentrada]** para **[!UICONTROL 30]** **[!UICONTROL Segundos]**.
   1. Selecionar **[!UICONTROL Ok]**.
      ![Propriedades da jornada](assets/ajo-journey-properties.png)

1. De volta à tela da jornada, a partir da **[!UICONTROL EVENTOS]**, arraste e solte seu ![Evento](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Globe_18_N.svg) **[!DNL LumaTestEvent]** na tela onde ele aparece **[!UICONTROL Selecionar um evento de entrada ou uma atividade de público-alvo de leitura]**.

   * No **[!UICONTROL Eventos: LumaTestEvent]** , insira um **[!UICONTROL Rótulo]**, por exemplo `Luma Test Event`.

1. No **[!UICONTROL AÇÕES]** lista suspensa, arrastar e soltar ![Push](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PushNotification_18_N.svg) **[!UICONTROL Push]** no ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) aparecendo à direita do **[!DNL LumaTestEvent]** atividade. No **[!UICONTROL Ações: push]** painel:

   1. Forneça um **[!UICONTROL Rótulo]**, por exemplo `Luma Test Push Notification`, forneça uma **[!UICONTROL Descrição]**, por exemplo `Test push notification for Luma mobile app`, selecione **[!UICONTROL Transacional]** do **[!UICONTROL Categoria]** e selecione **[!DNL Luma]** do **[!UICONTROL Superfície de push]**.
   1. Selecionar ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Editar conteúdo]** para começar a editar a notificação por push real.
      ![Propriedades de push](assets/ajo-push-properties.png)

      No **[!UICONTROL Notificação por push]** editor:

      1. Insira um **[!UICONTROL Título]**, por exemplo `Luma Test Push Notification` e insira um **[!UICONTROL Corpo]**, por exemplo `Test push notification for Luma mobile app`.
      1. Para salvar e sair do editor, selecione ![Divisa esquerda](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronLeft_18_N.svg).
         ![Enviar editor](assets/ajo-push-editor.png)

   1. Para salvar e concluir a definição de notificação por push, selecione **[!UICONTROL Ok]**.

1. Sua jornada deve ser parecida com a exibida abaixo. Selecionar **[!UICONTROL Publish]** para publicar e ativar sua jornada.
   ![Jornada concluída](assets/ajo-journey-finished.png)


## Acionar a notificação por push

Você tem todos os ingredientes em vigor para enviar uma notificação por push. O que resta é como acionar essa notificação por push. Em essência, é o mesmo que você viu antes: basta enviar um evento de experiência com a carga útil adequada (como em [Eventos](events.md)).

Desta vez, o evento de experiência que você está prestes a enviar não foi construído criando um dicionário XDM simples. Você usará um `struct` representando uma carga de notificação por push. Definir um tipo de dados dedicado é uma maneira alternativa de implementar a construção de cargas de evento de experiência no seu aplicativo.

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL Modelo]** > **[!UICONTROL XDM]** > **[!UICONTROL TestPushPayload]** no navegador do Projeto Xcode e inspecione o código.

   ```swift
   import Foundation
   
   // MARK: - TestPush
   struct TestPushPayload: Codable {
      let application: Application
      let eventType: String
   }
   
   // MARK: - Application
   struct Application: Codable {
      let id: String
   }
   ```

   O código é uma representação da seguinte carga simples que você enviará para acionar a jornada de notificação por push de teste

   ```json
   {
      "eventType": string,
      "application" : [
          "id": string
      ]
   }
   ```

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** no navegador do Projeto Xcode e adicione o seguinte código a `func sendTestPushEvent(applicationId: String, eventType: String)`:

   ```swift
   // Create payload and send experience event
   Task {
       let testPushPayload = TestPushPayload(
           application: Application(
               id: applicationId
           ),
           eventType: eventType
       )
       // send the final experience event
       await sendExperienceEvent(
           xdm: testPushPayload.asDictionary() ?? [:]
       )
   }
   ```

   Esse código cria uma `testPushPayload` instância usando os parâmetros fornecidos para a função (`applicationId` e `eventType`) e, em seguida, chama `sendExperienceEvent` ao converter a carga em um dicionário. Esse código, desta vez, também leva em conta os aspectos assíncronos de chamar o SDK do Adobe Experience Platform usando o modelo de simultaneidade do Swift com base em `await` e `async`.

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL ConfigView]** no navegador do Projeto Xcode. Na definição do Botão de notificação por push, adicione o seguinte código para enviar a carga do evento de experiência de notificação por push de teste para acionar a jornada sempre que esse botão for tocado.

   ```swift
   // Setting parameters and calling function to send push notification
   Task {
       let eventType = testPushEventType
       let applicationId = Bundle.main.bundleIdentifier ?? "No bundle id found"
       await MobileSDK.shared.sendTestPushEvent(applicationId: applicationId, eventType: eventType)
   }
   ```


## Validar usando seu aplicativo

1. Recrie e execute o aplicativo no simulador ou em um dispositivo físico do Xcode, usando ![Reproduzir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

1. Vá para a **[!UICONTROL Configurações]** guia.

1. Toque **[!UICONTROL Notificação por push]**. Você vê a notificação por push aparecer em seu aplicativo.

   <img src="assets/ajo-test-push.png" width="300" />


## Próximas etapas

Agora você deve ter todas as ferramentas para lidar com notificações por push no seu aplicativo. Por exemplo, você pode criar uma jornada no Journey Optimizer que envia uma notificação por push de boas-vindas quando um usuário do aplicativo faz logon. Ou uma notificação por push de confirmação quando um usuário compra um produto no aplicativo. Ou insere a geofence de um local (como você verá na [Places](places.md) lição).

>[!SUCCESS]
>
>Agora você ativou o aplicativo para notificação por push usando o Journey Optimizer e a extensão Journey Optimizer para o SDK móvel do Experience Platform.<br/>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Próximo: **[Criar e enviar mensagens no aplicativo](journey-optimizer-inapp.md)**
