---
title: Criar e enviar mensagens no aplicativo com o SDK móvel da Platform
description: Saiba como criar e enviar mensagens no aplicativo para um aplicativo móvel com o SDK móvel da Platform e o Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: In App
exl-id: 6cb4d031-6172-4a84-b717-e3a1f5dc7d5d
source-git-commit: d353de71d8ad26d2f4d9bdb4582a62d0047fd6b1
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 5%

---

# Criar e enviar mensagens no aplicativo

Saiba como criar mensagens no aplicativo para aplicativos móveis com o SDK móvel do Experience Platform e o Journey Optimizer.

O Journey Optimizer permite criar campanhas para enviar mensagens no aplicativo a públicos-alvo direcionados. As campanhas no Journey Optimizer são usadas para fornecer conteúdo único a um público específico usando vários canais. Com campanhas, as ações são executadas simultaneamente, imediatamente ou com base em um cronograma especificado. Ao usar jornadas (consulte a [Notificações por push do Journey Optimizer](journey-optimizer-push.md) ), as ações são executadas em sequência.

![Arquitetura](assets/architecture-ajo.png)

Antes de enviar mensagens no aplicativo com o Journey Optimizer, você deve garantir que as configurações e integrações adequadas estejam em vigor. Para entender o fluxo de dados de mensagens no aplicativo no Journey Optimizer, consulte [a documentação](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/inapp-configuration.html?lang=en).

>[!NOTE]
>
>Essa lição é opcional e se aplica somente aos usuários do Journey Optimizer que desejam enviar mensagens no aplicativo.


## Pré-requisitos

* O aplicativo com SDKs instalados e configurados foi criado e executado com sucesso.
* Configure o aplicativo para Adobe Experience Platform.
* Acesso ao Journey Optimizer e permissões suficientes, conforme descrito [aqui](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html). Além disso, você precisa de permissão suficiente para os seguintes recursos do Journey Optimizer.
   * Gerenciar campanhas.
* Dispositivo ou simulador físico iOS para teste.


## Objetivos de aprendizagem

Nesta lição, você

* Crie uma Superfície de aplicativo no AJO.
* Instalar e configurar a extensão de tag do Journey Optimizer.
* Atualize seu aplicativo para registrar a extensão de tag da Journey Optimizer.
* Valide a configuração no Assurance.
* Defina sua própria experiência de campanha e mensagens no aplicativo no Journey Optimizer.
* Envie sua própria mensagem no aplicativo de dentro do aplicativo.

## Configuração

>[!TIP]
>
>Se você já tiver configurado seu ambiente como parte da [mensagens por push do Journey Optimizer](journey-optimizer-push.md) lição, talvez você já tenha executado algumas etapas nesta seção de configuração.


### Adicionar uma superfície de aplicativo na Coleção de dados

1. No [Interface da coleção de dados](https://experience.adobe.com/br/data-collection/), selecione **[!UICONTROL Superfícies do aplicativo]** no painel esquerdo.
1. Para criar uma configuração, selecione **[!UICONTROL Criar superfície do aplicativo]**.
   ![página inicial da superfície de aplicativo](assets/push-app-surface.png)
1. Insira um **[!UICONTROL Nome]** para a configuração do, por exemplo `Luma App Tutorial`  .
1. De **[!UICONTROL Configuração do aplicativo móvel]**, selecione **[!UICONTROL Apple iOS]**.
1. Insira a ID do pacote do aplicativo móvel na **[!UICONTROL ID do aplicativo (ID do pacote iOS)]** campo. Por exemplo,  `com.adobe.luma.tutorial.swiftui`.
1. Selecione **[!UICONTROL Salvar]**.

   ![configuração da superfície do aplicativo](assets/push-app-surface-config-inapp.png)

### Atualizar configuração da sequência de dados

Para garantir que os dados enviados do aplicativo móvel para a Rede de borda sejam encaminhados para a Journey Optimizer, atualize a configuração da Experience Edge.



1. Na interface da Coleção de dados, selecione **[!UICONTROL Datastreams]** e selecione seu fluxo de dados, por exemplo **[!DNL Luma Mobile App]**.
1. Selecionar ![Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) para **[!UICONTROL Experience Platform]** e selecione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Editar]** no menu de contexto.
1. No **[!UICONTROL Datastreams]** > ![Pasta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) >  **[!UICONTROL Adobe Experience Platform]** , certifique-se **[!UICONTROL Adobe Journey Optimizer]** está selecionada. Consulte [Configurações do Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#aep) para obter mais informações.
1. Para salvar a configuração do fluxo de dados, selecione **[!UICONTROL Salvar]**.


   ![Configuração da sequência de dados da AEP](assets/datastream-aep-configuration.png)


### Instalar extensão de tags do Journey Optimizer

Para que seu aplicativo funcione com a Journey Optimizer, é necessário atualizar a propriedade da tag.

1. Navegue até **[!UICONTROL Tags]** > **[!UICONTROL Extensões]** > **[!UICONTROL Catálogo]**.
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
>Se você não vir `AJO Push Tracking Experience Event Dataset` como opção, entre em contato com o atendimento ao cliente.
>

### Implementar o Journey Optimizer no aplicativo

Conforme discutido nas lições anteriores, a instalação de uma extensão de tag móvel fornece apenas a configuração. Em seguida, você deve instalar e registrar o SDK de mensagens. Se essas etapas não estiverem claras, revise o [Instalar SDKs](install-sdks.md) seção.

>[!NOTE]
>
>Se você concluiu o [Instalar SDKs](install-sdks.md) , o SDK já estará instalado e você poderá ignorar essa etapa.
>

1. No Xcode, verifique se [Mensagens AEP](https://github.com/adobe/aepsdk-messaging-ios) é adicionado à lista de pacotes nas Dependências de pacote. Consulte [Gerenciador de pacotes Swift](install-sdks.md#swift-package-manager).
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


## Validar configuração com o Assurance

1. Revise o [instruções de configuração](assurance.md#connecting-to-a-session) seção para conectar seu simulador ou dispositivo ao Assurance.
1. Na interface do usuário do Assurance, selecione **[!UICONTROL Configurar]**.
   ![configurar clique](assets/push-validate-config.png)
1. Selecione o ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) botão ao lado de **[!UICONTROL Mensagens no aplicativo]**.
1. Selecione **[!UICONTROL Salvar]**.
   ![save](assets/assurance-in-app-config.png)
1. Selecionar **[!UICONTROL Mensagens no aplicativo]** no painel de navegação esquerdo.
1. Selecione o **[!UICONTROL Validação]** guia. Confirme se não está recebendo erros.

   ![Validação no aplicativo](assets/assurance-in-app-validate.png)


## Criar sua própria mensagem no aplicativo

Para criar sua própria mensagem no aplicativo, você deve definir uma campanha no Journey Optimizer que acione uma mensagem no aplicativo com base nos eventos que ocorrem. Esses eventos podem ser:

* dados enviados para o Adobe Experience Platform,
* eventos principais de rastreamento, como ação ou estado ou coleção de dados PII, por meio das APIs genéricas principais móveis,
* eventos do ciclo de vida do aplicativo, como iniciar, instalar, atualizar, fechar ou falhar,
* eventos de geolocalização, como entrar ou sair de um ponto de interesse.

Neste tutorial, você usará as APIs do Mobile Core genéricas e independentes de extensão (consulte [APIs genéricas principais para dispositivos móveis](https://developer.adobe.com/client-sdks/documentation/mobile-core/#mobile-core-generic-apis)) para facilitar o rastreamento de eventos de telas de usuários, ações e dados de PII. Os eventos gerados por essas APIs são publicados no hub de eventos do SDK e estão disponíveis para uso por extensões. O hub de eventos do SDK fornece a estrutura de dados principal vinculada a todas as extensões do SDK da plataforma móvel, mantendo uma lista de extensões registradas e módulos internos, uma lista de ouvintes de eventos registrados e um banco de dados de estado compartilhado.

O hub de eventos do SDK publica e recebe dados de eventos de extensões registradas para simplificar as integrações com o Adobe e soluções de terceiros. Por exemplo, quando a extensão Otimize é instalada, todas as solicitações e interações com o mecanismo de oferta da Journey Optimizer - Gestão de decisões são tratadas pelo hub de eventos.

1. Na interface do Journey Optimizer, selecione **[!UICONTROL Campanhas]** do painel esquerdo.
1. Selecionar **[!UICONTROL Criar campanha]**.
1. No **[!UICONTROL Criar campanha]** tela:
   1. Selecionar **[!UICONTROL Mensagem no aplicativo]** e selecione uma superfície de aplicativo na **[!UICONTROL Superfície do aplicativo]** lista, por exemplo **[!DNL Luma Mobile App]**.
   1. Selecione **[!UICONTROL Criar]**
      ![Propriedades da campanha](assets/ajo-campaign-properties.png)
1. Na tela Campaign definition, em **[!UICONTROL Propriedades]**, insira um **[!UICONTROL Nome]** para a campanha, por exemplo `Luma - In-App Messaging Campaign`, e uma **[!UICONTROL Descrição]**, por exemplo `In-app messaging campaign for Luma app`.
   ![Nome da campanha](assets/ajo-campaign-properties-name.png)
1. Role para baixo até **[!UICONTROL Ação]** e selecione **[!UICONTROL Editar conteúdo]**.
1. No **[!UICONTROL Mensagem no aplicativo]** tela:
   1. Selecionar **[!UICONTROL Modal]** como o **[!UICONTROL Layout da mensagem]**.
   2. Enter `https://luma.enablementadobe.com/content/dam/luma/en/logos/Luma_Logo.png` para o **[!UICONTROL URL de mídia]**.
   3. Insira um **[!UICONTROL Cabeçalho]**, por exemplo `Welcome to this Luma In-App Message` e insira um **[!UICONTROL Corpo]**, por exemplo `Triggered by pushing that button in the app...`.
   4. Enter **[!UICONTROL Ignorar]** como o **[!UICONTROL Texto do botão #1 (principal)]**.
   5. Observe como a visualização é atualizada.
   6. Selecionar **[!UICONTROL Revisar para ativar]**.
      ![Editor no aplicativo](assets/ajo-in-app-editor.png)
1. No **[!UICONTROL Revise para ativar (Luma - Campanha de mensagens no aplicativo)]** , selecione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) no **[!UICONTROL Agendar]** bloco.
   ![Revisar agendamento e selecionar agendamento](assets/ajo-review-select-schedule.png)
1. De volta ao **[!DNL Luma - In-App Messaging Campaign]** , selecione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Editar acionadores]**.
1. No **[!UICONTROL Acionador de mensagem no aplicativo]** , você configura os detalhes da ação de rastreamento que aciona a mensagem no aplicativo:
   1. Para remover **[!UICONTROL Evento de inicialização de aplicativo]**, selecione ![Fechar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg) .
   1. Uso ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Adicionar condição]** criar repetidamente a seguinte lógica para **[!UICONTROL Mostrar mensagem se]**.
   1. Clique em **[!UICONTROL Concluído]**.
      ![Lógica de acionamento](assets/ajo-trigger-logic.png)

   Você definiu uma ação de rastreamento, onde a variável **[!UICONTROL Ação]** igual a `in-app` e a variável **[!UICONTROL Dados de contexto]** com a ação é um par de valores fundamental de `"showMessage" : "true"`.

1. De volta ao **[!DNL Luma - In-App Messaging Campaign]** , selecione **[!UICONTROL Revisar para ativar]**.
1. No **[!UICONTROL Revise para ativar (Luma - Campanha de mensagens no aplicativo)]** , selecione **[!UICONTROL Ativar]**.
1. Você vê o seu **[!DNL Luma - In-App Messaging Campaign]** com status **[!UICONTROL Ao vivo]** no **[!UICONTROL Campanhas]** lista.
   ![Lista de campanhas](assets/ajo-campaign-list.png)


## Acionar a mensagem no aplicativo

Você tem todos os ingredientes em vigor para enviar uma mensagem no aplicativo. O que resta é como acionar essa mensagem no aplicativo.

1. Ir para **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** no navegador do Projeto Xcode. Localize o `func sendTrackAction(action: String, data: [String: Any]?)` e adicione o seguinte código, que chama a função [`MobileCore.track`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction) baseada nos parâmetros `action` e `data`.


   ```swift
   // Send trackAction event
   MobileCore.track(action: action, data: data)
   ```

1. Ir para **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL ConfigView]** no Navegador de projetos do Xcode. Localize o código do botão Mensagens no aplicativo e adicione o seguinte código:

   ```swift
   // Setting parameters and calling function to send in-app message
   Task {
       MobileSDK.shared.sendTrackAction(action: "in-app", data: ["showMessage": "true"])
   }
   ```

## Validar usando seu aplicativo

1. Recrie e execute o aplicativo no simulador ou em um dispositivo físico do Xcode, usando ![Reproduzir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

1. Vá para a **[!UICONTROL Configurações]** guia.

1. Toque **[!UICONTROL Mensagem no aplicativo]**. Você vê a mensagem no aplicativo aparecer no seu aplicativo.

   <img src="assets/ajo-in-app-message.png" width="300" />


## Validar implementação no Assurance

Você pode validar as mensagens no aplicativo na interface do usuário do Assurance.

1. Revise o [instruções de configuração](assurance.md#connecting-to-a-session) seção para conectar seu simulador ou dispositivo ao Assurance.
1. Selecionar **[!UICONTROL Mensagens no aplicativo]**.
1. Selecionar **[!UICONTROL Lista de Eventos]**.
1. Selecione um **[!UICONTROL Exibir mensagem]** entrada.
1. Inspect é o evento bruto, especialmente o `html`, que contém o layout completo e o conteúdo da mensagem no aplicativo.
   ![Mensagem no aplicativo do Assurance](assets/assurance-in-app-display-message.png)


## Próximas etapas

Agora você deve ter todas as ferramentas para começar a adicionar mensagens no aplicativo, quando relevante e aplicável. Por exemplo, promover produtos com base em interações específicas que você está rastreando no aplicativo.

>[!SUCCESS]
>
>Você habilitou o aplicativo para mensagens no aplicativo e adicionou uma campanha de mensagens no aplicativo usando o Journey Optimizer e a extensão Journey Optimizer para o SDK móvel do Experience Platform.
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Próximo: **[Criar e exibir ofertas](journey-optimizer-offers.md)**
