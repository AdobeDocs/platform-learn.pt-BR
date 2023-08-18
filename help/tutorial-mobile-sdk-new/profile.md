---
title: Perfil
description: Saiba como coletar dados de perfil em um aplicativo móvel.
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 1%

---

# Perfil

Saiba como coletar dados de perfil em um aplicativo móvel.

Você pode usar a extensão Profile para armazenar atributos sobre seu usuário no cliente. Essas informações podem ser usadas posteriormente para direcionar e personalizar mensagens em cenários online ou offline, sem precisar se conectar a um servidor para obter o desempenho ideal. A extensão Perfil gerencia o CSOP (Perfil de operação do lado do cliente), fornece uma maneira de reagir a APIs, atualiza atributos de perfil do usuário e compartilha os atributos de perfil do usuário com o restante do sistema como um evento gerado.

Os dados do Perfil são usados por outras extensões para executar ações relacionadas ao perfil. Um exemplo é a extensão Mecanismo de regras que consome os dados do perfil e executa as regras com base nos dados do perfil. Saiba mais sobre o [Extensão de perfil](https://developer.adobe.com/client-sdks/documentation/profile/) na documentação

>[!IMPORTANT]
>
>A funcionalidade de perfil descrita nesta lição é separada da funcionalidade de perfil do cliente em tempo real nos aplicativos da Adobe Experience Platform e da plataforma.


## Pré-requisitos

* O aplicativo com SDKs instalados e configurados foi criado e executado com sucesso.
* Importado o SDK do perfil.

  ```swift
  import AEPUserProfile
  ```

## Objetivos de aprendizagem

Nesta lição, você vai:

* Definir ou atualizar atributos do usuário.
* Recuperar atributos do usuário.


## Definir e atualizar

Seria útil para direcionamento e/ou personalização saber rapidamente se um usuário fez uma compra no aplicativo antes. Vamos configurar isso no aplicativo Luma.

1. Navegue até **[!UICONTROL ProductView]** (em **[!UICONTROL Visualizações]** > **[!UICONTROL Produtos]**) no projeto de aplicativo Xcode Luma e encontre a chamada para `updateUserAttributes` (no botão Purchases ):

   ```swift {highlight="8-9"}
   Button {
       Task {
           if ATTrackingManager.trackingAuthorizationStatus == .authorized {
               // Send purchase commerce experience event
               MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
               // Update attributes
               MobileSDK.shared.updateUserAttributes(attributeName: "isPaidUser", attributeValue: "yes")
           }
       }
       showPurchaseDialog.toggle()
   } label: {
       Label("", systemImage: "creditcard")
   }
   .alert(isPresented: $showPurchaseDialog, content: {
       Alert(title: Text( "Purchases"), message: Text("The selected item is purchased…"))
   })
   ```

2. Navegue até **[!UICONTROL MobileSDK]** e localize o `updateUserAttributes` função. Adicione o seguinte código destacado:

   ```swift {highlight="2-4"}
   func updateUserAttributes(attributeName: String, attributeValue: String) {
       var profileMap = [String: Any]()
       profileMap[attributeName] = attributeValue
       UserProfile.updateUserAttributes(attributeDict: profileMap)
   }
   ```

   Este código:

   1. Configura um dicionário vazio chamado `profileMap`.

   1. Adiciona um elemento ao dicionário usando `attributeName` (por exemplo `isPaidUser`) e `attributeValue` (por exemplo `yes`).

   1. Usa o `profileMap` dicionário como um valor para o `attributeDict` parâmetro do `UserProfile.updateUserAttributes` chamada à API.


Adicional `updateUserAttributes` a documentação pode ser encontrada [aqui](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattribute).

## Obtenha

Depois de atualizar o atributo de um usuário, ele estará disponível para outros SDKs Adobe, mas você também poderá recuperar os atributos explicitamente.

1. Navegue até **[!UICONTROL HomeView]** (em **[!UICONTROL Visualizações]** > **[!UICONTROL Geral]**) e encontre o `.onAppear` modificador. Adicione o seguinte código:

   ```swift {highlight="3-11"}
   .onAppear {
       // Track view screen
       MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: home")
       // Get attributes
       UserProfile.getUserAttributes(attributeNames: ["isPaidUser"]) { attributes, error in
           if attributes?["isPaidUser"] as! String == "yes" {
               showBadgeForUser = true
           }
           else {
               showBadgeForUser = false
           }
       }
   }
   ```

   Este código:

   1. Chama o `UserProfile.getUserAttributes` encerramento com a `iPaidUser` nome do atributo como elemento único na variável `attributeNames` matriz.
   1. Em seguida, verifica o valor de `isPaidUser` atributo e quando `yes`, coloca um selo no ícone Pessoa na parte superior direita.

Adicional `getUserAttributes` a documentação pode ser encontrada [aqui](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## Validar com garantia

1. Revise o [instruções de configuração](assurance.md) seção.
1. Instale o aplicativo.
1. Inicie o aplicativo usando o URL gerado pelo Assurance.
1. Execute o aplicativo para fazer logon e interagir com um produto.

   1. Mova o ícone do Assurance para a esquerda.
   1. Selecionar **[!UICONTROL Início]** na barra de guias.
   1. Para abrir a planilha de Logon, selecione o **[!UICONTROL Logon]** botão.
   1. Para inserir um email e uma ID do cliente aleatórios, selecione **[!UICONTROL A|]** botão .
   1. Selecionar **[!UICONTROL Logon]**.
   1. Selecionar **[!UICONTROL Produtos]** na barra de guias.
   1. Selecione um produto.
   1. Selecionar **[!UICONTROL Salvar para mais tarde]**.
   1. Selecionar **[!UICONTROL Adicionar ao carrinho]**.
   1. Selecionar **[!UICONTROL Comprar]**.
   1. Retornar para **[!UICONTROL Início]** tela. Você deve ver um botão de logon atualizado.

      <img src="./assets/mobile-app-events-1.png" width="200"> <img src="./assets/mobile-app-events-2.png" width="200"> <img src="./assets/mobile-app-events-3.png" width="200"> <img src="./assets/personbadges.png" width="200">

1. Você deve ver um **[!UICONTROL UserProfileUpdate]** e **[!UICONTROL getUserAttributes]** eventos na interface do usuário do Assurance com o `profileMap` valor.
   ![validar perfil](assets/profile-validate.png)

>[!SUCCESS]
>
>Agora você configurou o aplicativo para atualizar atributos de perfis na Rede de borda e (quando configurado) com o Adobe Experience Platform.<br/>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Próximo: **[Mapear dados para o Adobe Analytics](analytics.md)**
