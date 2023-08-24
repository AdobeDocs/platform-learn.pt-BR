---
title: Mensagens no aplicativo do Adobe Journey Optimizer
description: Saiba como criar mensagens no aplicativo para um aplicativo móvel com o SDK móvel da plataforma e o Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
hide: true
source-git-commit: 7de7c7e13ea6d02f1193620e0cc35299e07d59e5
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 3%

---

# Mensagens no aplicativo do Adobe Journey Optimizer

Saiba como criar mensagens no aplicativo para aplicativos móveis com o SDK móvel da plataforma e o Adobe Journey Optimizer.

O Journey Optimizer permite criar suas jornadas e enviar mensagens no aplicativo para públicos-alvo direcionados. Antes de enviar mensagens no aplicativo com o Journey Optimizer, você deve garantir que as configurações e integrações adequadas estejam em vigor. Para entender o fluxo de dados de mensagens no aplicativo no Adobe Journey Optimizer, consulte [a documentação](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/inapp-configuration.html?lang=en).

>[!NOTE]
>
>Essa lição é opcional e se aplica somente aos usuários do Adobe Journey Optimizer que desejam enviar mensagens no aplicativo.


## Pré-requisitos

* O aplicativo com SDKs instalados e configurados foi criado e executado com sucesso.
* Acesso ao Adobe Journey Optimizer e permissões suficientes, conforme descrito [aqui](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). Além disso, você precisa de permissões suficientes para os seguintes recursos do Adobe Journey Optimizer.
   * Criar uma campanha.
* Conta de desenvolvedor paga do Apple com acesso suficiente para criar certificados, identificadores e chaves.
* Dispositivo ou simulador físico iOS para teste.
* [ID do aplicativo registrada com APN](journey-optimizer-push.md#register-app-id-with-apn)
* [Adicionadas suas credenciais de push do aplicativo na Coleção de dados](journey-optimizer-push.md#add-your-app-push-credentials-in-data-collection)
* [Extensão de tags do Adobe Journey Optimizer instalada](journey-optimizer-push.md#install-adobe-journey-optimizer-tags-extension)
* [Adobe Journey Optimizer implementado no aplicativo](journey-optimizer-push.md#implement-adobe-journey-optimizer-in-the-app)


## Validar com garantia

1. Revise o [instruções de configuração](assurance.md) seção.
1. Instale o aplicativo no dispositivo físico ou no simulador.
1. Inicie o aplicativo usando o URL gerado pelo Assurance.
1. Na interface do usuário do Assurance, selecione **[!UICONTROL Configurar]**.
   ![configurar clique](assets/push-validate-config.png)
1. Selecione o ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) botão ao lado de **[!UICONTROL Mensagens no aplicativo]**.
1. Selecione **[!UICONTROL Salvar]**.
   ![save](assets/assurance-in-app-config.png)
1. Selecionar **[!UICONTROL Mensagens no aplicativo]** no painel de navegação esquerdo.
1. Selecione o **[!UICONTROL Validação]** guia.
1. Confirme se não está recebendo erros.
   ![Validação no aplicativo](assets/assurance-in-app-validate.png)


## Criar sua própria mensagem no aplicativo

Para criar sua própria mensagem no aplicativo, você deve definir uma campanha no Journey Optimizer que acione uma mensagem no aplicativo com base nos eventos que ocorrem. Esses eventos podem ser:

* dados enviados para o Adobe Experience Platform,
* eventos principais de rastreamento, como ação ou estado ou coleção de dados PII, por meio das APIs genéricas principais móveis,
* eventos do ciclo de vida do aplicativo, como iniciar, instalar, atualizar, fechar ou falhar,
* eventos de geolocalização, como entrar ou sair de um ponto de interesse.

Neste tutorial, você usará as APIs genéricas e independentes de extensão do Mobile Core para facilitar o rastreamento de eventos de telas de usuários, ações e dados de PII. Os eventos gerados por essas APIs são publicados no hub de eventos do SDK e estão disponíveis para uso por extensões. Por exemplo, quando a extensão do Analytics é instalada, todos os dados de eventos de ações do usuário e telas do aplicativo são enviados para os endpoints de relatório apropriados do Analytics.

1. Na interface do Journey Optimizer, selecione **[!UICONTROL Campanhas]** do painel esquerdo.
1. Selecionar **[!UICONTROL Criar campanha]**.
1. No **[!UICONTROL Criar campanha]** tela:
   1. Selecionar **[!UICONTROL Mensagem no aplicativo]** e selecione **[!UICONTROL Aplicativo móvel Luma]** do **[!UICONTROL Superfície do aplicativo]** lista.
   1. Selecione **[!UICONTROL Criar]**
      ![Propriedades da campanha](assets/ajo-campaign-properties.png)
1. Na tela Campaign definition, em **[!UICONTROL Propriedades]**, insira um **[!UICONTROL Nome]** para a campanha, por exemplo `Luma - In-App Messaging Campaign`, e uma **[!UICONTROL Descrição]**, por exemplo `In-app messaging campaign for Luma app`.
   ![Nome da campanha](assets/ajo-campaign-properties-name.png)
1. Role para baixo até **[!UICONTROL Ação]** e selecione **[!UICONTROL Editar conteúdo]**.
1. No **[!UICONTROL Mensagem no aplicativo]** tela:
   1. Selecionar **[!UICONTROL Modal]** como o **[!UICONTROL Layout da mensagem]**.
   2. Enter `https://luma.enablementadobe.com/content/dam/luma/en/logos/Luma_Logo.png` para **[!UICONTROL URL de mídia]**.
   3. Insira um **[!UICONTROL Cabeçalho]**, por exemplo `Welcome to this Luma In-App Message` e insira um **[!UICONTROL Corpo]**, por exemplo `Triggered by pushing that button in the app...`.
   4. Enter **[!UICONTROL Ignorar]** como o **[!UICONTROL Texto do botão #1 (principal)]**.
   5. Observe como a visualização é atualizada.
   6. Selecionar **[!UICONTROL Revisar para ativar]**.
      ![Editor no aplicativo](assets/ajo-in-app-editor.png)
1. No **[!UICONTROL Revise para ativar (Luma - Campanha de mensagens no aplicativo)]** , selecione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) no **[!UICONTROL Agendar]** bloco.
   ![Revisar agendamento e selecionar agendamento](assets/ajo-review-select-schedule.png)
1. De volta ao **[!UICONTROL Luma - Campanha de mensagens no aplicativo]** , selecione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Editar acionadores]**.
1. No **[!UICONTROL Acionador de mensagem no aplicativo]** , você configura os detalhes da ação de rastreamento que aciona a mensagem no aplicativo:
   1. Para remover **[!UICONTROL Evento de inicialização de aplicativo]**, selecione ![Fechar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg) .
   1. Uso ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Adicionar condição]** criar repetidamente a seguinte lógica para **[!UICONTROL Mostrar mensagem se]**.
   1. Clique em **[!UICONTROL Concluído]**.
      ![Lógica de acionamento](assets/ajo-trigger-logic.png)

   Você definiu uma ação de rastreamento, onde a variável **[!UICONTROL Ação]** igual a `in-app` e a variável **[!UICONTROL Dados de contexto]** com a ação é um par de valores fundamental de `"showMessage" : "true"`.

1. De volta ao **[!UICONTROL Luma - Campanha de mensagens no aplicativo]** , selecione **[!UICONTROL Revisar para ativar]**.
1. No **[!UICONTROL Revise para ativar (Luma - Campanha de mensagens no aplicativo)]** , selecione **[!UICONTROL Ativar]**.
1. Você vê o seu **[!UICONTROL Luma - Campanha de mensagens no aplicativo]** com status **[!UICONTROL Ao vivo]** no **[!UICONTROL Campanhas]** lista.
   ![Lista de campanhas](assets/ajo-campaign-list.png)


## Acionamento da mensagem no aplicativo

Você tem todos os ingredientes em vigor para enviar uma mensagem no aplicativo. O que resta é como acionar essa mensagem no aplicativo no código.

1. Vá para Luma > Luma > Utils > MobileSDK no navegador do Projeto Xcode e localize o `func sendTrackAction(action: String, data: [String: Any]?)` e adicione o seguinte código, que chama a função `MobileCore.track` baseada nos parâmetros `action` e `data`.


   ```swift
   // send trackAction event
   MobileCore.track(action: action, data: data)
   ```

1. Ir para **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Visualizações]** > **[!UICONTROL Geral]** > **[!UICONTROL ConfigView]** no Navegador de projetos do Xcode. Localize o código do botão Mensagens no aplicativo e adicione o seguinte código:

   ```swift
   Task {
       AEPService.shared.sendTrackAction(action: "in-app", data: ["showMessage": "true"])
   }
   ```

## Validar usando seu aplicativo

1. Abra o aplicativo em um dispositivo ou no simulador.

1. Vá para a **[!UICONTROL Configurações]** guia.

1. Toque **[!UICONTROL Mensagem no aplicativo]**. Você vê a mensagem no aplicativo aparecer no seu aplicativo.

   <img src="assets/ajo-in-app-message.png" width="300" />


## Validar no Assurance

Você pode validar as mensagens no aplicativo na interface do usuário do Assurance.

1. Selecionar **[!UICONTROL Mensagens no aplicativo]**.
1. Selecionar **[!UICONTROL Lista de Eventos]**.
1. Selecione um **[!UICONTROL Exibir mensagem]** entrada.
1. Inspect é o evento bruto, especialmente o `html`, que contém o layout completo e o conteúdo da mensagem no aplicativo.
   ![Mensagem no aplicativo do Assurance](assets/assurance-in-app-display-message.png)


## Implementar no aplicativo

Agora você deve ter todas as ferramentas para começar a adicionar notificações por push, quando relevante e aplicável, ao aplicativo Luma. Por exemplo, receber o usuário ao fazer logon no aplicativo ou ao se aproximar de uma geolocalização específica.

>[!SUCCESS]
>
>Agora você habilitou o aplicativo para mensagens no aplicativo e adicionou uma campanha de mensagens no aplicativo usando o Adobe Journey Optimizer e a extensão Adobe Journey Optimizer para o SDK do Adobe Experience Platform Mobile.<br/>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Próximo: **[Conclusão e próximas etapas](conclusion.md)**
