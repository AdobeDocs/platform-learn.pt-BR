---
title: mensagens por push do Adobe Journey Optimizer
description: Saiba como criar mensagens de push para um aplicativo móvel com o SDK móvel da plataforma e o Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Push
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 2%

---

# mensagens por push do Adobe Journey Optimizer

Saiba como criar mensagens de push para aplicativos móveis com o SDK móvel da plataforma e o Adobe Journey Optimizer.

O Journey Optimizer permite criar suas jornadas e enviar mensagens para públicos-alvo direcionados. Antes de enviar notificações por push com o Journey Optimizer, você deve garantir que as configurações e integrações adequadas estejam em vigor. Para entender o fluxo de dados de notificações por push no Adobe Journey Optimizer, consulte [a documentação](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-gs.html).

>[!NOTE]
>
>Esta lição é opcional e se aplica somente aos usuários do Adobe Journey Optimizer que desejam enviar mensagens de push.


## Pré-requisitos

* O aplicativo com SDKs instalados e configurados foi criado e executado com sucesso.
* Acesso ao Adobe Journey Optimizer e permissões suficientes, conforme descrito [aqui](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). Além disso, você precisa de permissões suficientes para os seguintes recursos do Adobe Journey Optimizer.
   * Crie uma superfície de aplicativo.
   * Criar uma jornada
   * Criar uma mensagem.
   * Criar predefinições de mensagem.
* Conta de desenvolvedor paga do Apple com acesso suficiente para criar certificados, identificadores e chaves.
* Dispositivo iOS físico para teste.

## Objetivos de aprendizagem

Nesta lição, você vai:

* Registrar a ID do aplicativo no serviço de notificação por push (APN) da Apple.
* Criar um **[!UICONTROL Superfície do aplicativo]** no AJO.
* Atualize seu **[!UICONTROL schema]** para incluir campos de mensagens por push.
* Instalar e configurar o **[!UICONTROL Adobe Journey Optimizer]** extensão de tag.
* Atualize seu aplicativo para incluir a extensão de tag do AJO.
* Valide a configuração no Assurance.
* Envie uma mensagem de teste.


## Registrar ID do aplicativo com APN

As etapas a seguir não são específicas do Adobe Experience Cloud e foram projetadas para orientá-lo pela configuração do APN.

### Criar uma chave privada

1. No portal do desenvolvedor do Apple, navegue até **[!UICONTROL Chaves]**.
1. Para criar uma chave, selecione **[!UICONTROL +]**.
   ![criar nova chave](assets/mobile-push-apple-dev-new-key.png)

1. Forneça um **[!UICONTROL Nome da chave]**.
1. Selecione o **[!UICONTROL APN]** caixa de seleção
1. Selecionar **[!UICONTROL Continuar]**.
   ![configurar nova chave](assets/mobile-push-apple-dev-config-key.png)
1. Revise a configuração e selecione **[!UICONTROL Registrar]**.
1. Baixe o `.p8` chave privada. É usado na configuração da Superfície do aplicativo.
1. Anote o [!UICONTROL ID da chave]. É usado na configuração da Superfície do aplicativo.
1. Anote o [!UICONTROL ID da equipe]. É usado na configuração da Superfície do aplicativo.
   ![Detalhes da chave](assets/push-apple-dev-key-details.png)

A documentação adicional pode ser [encontrado aqui](https://help.apple.com/developer-account/#/devcdfbb56a3).

## Adicionar suas credenciais de push do aplicativo na Coleção de dados

1. No [Interface da coleção de dados](https://experience.adobe.com/br/data-collection/), selecione **[!UICONTROL Superfícies do aplicativo]** no painel esquerdo.
1. Para criar uma configuração, selecione **[!UICONTROL Criar Superfícies do Aplicativo]**.
   ![página inicial da superfície de aplicativo](assets/push-app-surface.png)
1. Insira um **[!UICONTROL Nome]** para a configuração do, por exemplo `Luma App Tutorial`  .
1. Em Configuração do Aplicativo Móvel, selecione **[!UICONTROL Apple iOS]**.
1. Insira a ID do pacote do aplicativo móvel no campo ID do aplicativo (ID do pacote iOS). Se você estiver seguindo junto com o aplicativo Luma, esse valor será `com.adobe.luma.tutorial.swiftui`.
1. Ligue o **[!UICONTROL Credenciais por push]** botão para adicionar suas credenciais.
1. Arraste e solte o `.p8` **Chave de autenticação da notificação por push do Apple** arquivo.
1. Forneça o **[!UICONTROL ID da chave]**, uma sequência de 10 caracteres atribuída durante a criação de `p8` chave de autenticação. Ele pode ser encontrado em **[!UICONTROL Chaves]** guia em **Certificados, identificadores e perfis** página das páginas do portal Apple Developer.
1. Forneça o **[!UICONTROL ID da equipe]**. A ID da equipe é um valor que pode ser encontrado na variável **Associação** ou na parte superior das páginas do portal Apple Developer.
1. Selecione **[!UICONTROL Salvar]**.

   ![configuração da superfície do aplicativo](assets/push-app-surface-config.png)

## Instalar extensão de tags do Adobe Journey Optimizer

1. Navegue até **[!UICONTROL Tags]** > **[!UICONTROL Extensões]** > **[!UICONTROL Catálogo]**,
1. Abra a propriedade, por exemplo **[!UICONTROL Tutorial do aplicativo móvel Luma]**.
1. Selecionar **[!UICONTROL Catálogo]**.
1. Procure por **[!UICONTROL Adobe Journey Optimizer]** extensão.
1. Instale a extensão.
1. No **[!UICONTROL Instalar extensão]** caixa de diálogo
   1. Selecione um ambiente, por exemplo **[!UICONTROL Desenvolvimento]**.
   1. Selecione o **[!UICONTROL Conjunto de dados do evento de experiência de rastreamento de push do AJO]** conjunto de dados da **[!UICONTROL Conjunto de dados do evento]** lista suspensa.
      ![Configurações de extensão do AJO](assets/push-tags-ajo.png)
   1. Selecionar **[!UICONTROL Salvar na biblioteca e criar]**.

>[!NOTE]
>
>Se você não vir `AJO Push Tracking Experience Event Dataset` como opção, entre em contato com o atendimento ao cliente.
>

## Implementar a Adobe Journey Optimizer no aplicativo

Conforme discutido nas lições anteriores, a instalação de uma extensão de tag móvel fornece apenas a configuração. Em seguida, você deve instalar e registrar o SDK de mensagens. Se essas etapas não estiverem claras, revise o [Instalar SDKs](install-sdks.md) seção.

>[!NOTE]
>
>Se você concluiu o [Instalar SDKs](install-sdks.md) , o SDK já estará instalado e você poderá pular para a etapa #7.
>

1. No Xcode, verifique se [Mensagens AEP](https://github.com/adobe/aepsdk-messaging-ios.git) é adicionado à lista de pacotes nas Dependências de pacote. Consulte [Gerenciador de pacotes Swift](install-sdks.md#swift-package-manager).
1. Abra o Xcode e navegue até **[!UICONTROL AppDelegate]**.
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

1. Adicione o `MobileCore.setPushIdentifier` para o `application(_, didRegisterForRemoteNotificationsWithDeviceToken)` função.

   ```swift {highlight="7"}
   func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
       // Required to log the token
       let tokenParts = deviceToken.map { data in String(format: "%02.2hhx", data) }
       let token = tokenParts.joined()
       Logger.notifications.info("didRegisterForRemoteNotificationsWithDeviceToken - device token: \(token)")
   
       // Send push token to Experience Platform
       MobileCore.setPushIdentifier(deviceToken)
       currentDeviceToken = token
   }
   ```

   Essa função recupera o token do dispositivo exclusivo para o dispositivo no qual o aplicativo está instalado e envia o token para o Adobe Apple para entrega de mensagens de push.

## Validar enviando uma mensagem de push de teste

1. Revise o [instruções de configuração](assurance.md) seção.
1. Instale o aplicativo no dispositivo físico ou no simulador.
1. Inicie o aplicativo usando o URL gerado pelo Assurance.
1. Na interface do usuário do Assurance, selecione **[!UICONTROL Configurar]**.
   ![configurar clique](assets/push-validate-config.png)
1. Selecione o ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) botão ao lado de **[!UICONTROL Depuração push]**.
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
1. Você deve ver a notificação por push no aplicativo.

   <img src="assets/luma-app-push.png" width="300" />


>[!SUCCESS]
>
>Agora você habilitou o aplicativo para notificação por push usando a extensão Adobe Journey Optimizer para o SDK do Adobe Experience Platform Mobile.<br/>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Próximo: **[Conclusão e próximas etapas](conclusion.md)**
