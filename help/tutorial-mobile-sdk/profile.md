---
title: Coletar dados de perfil com o Platform Mobile SDK
description: Saiba como coletar dados de perfil em um aplicativo móvel.
jira: KT-14634
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: 4a0fa85c76c00fd505118692ea4b6cbe410f5839
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 1%

---

# Coletar dados de perfil

Saiba como coletar dados de perfil em um aplicativo móvel.

Você pode usar a extensão Profile para armazenar atributos sobre seu usuário no cliente. Essas informações podem ser usadas posteriormente para direcionar e personalizar mensagens em cenários online ou offline, sem precisar se conectar a um servidor para obter o desempenho ideal.

A extensão Perfil gerencia o CSOP (Perfil de operação do lado do cliente), fornece uma maneira de reagir a APIs, atualiza atributos de perfil do usuário e compartilha os atributos de perfil do usuário com o restante do sistema como um evento gerado.

Os dados do Perfil são usados por outras extensões para executar ações relacionadas ao perfil. Um exemplo é a extensão Mecanismo de regras que consome os dados do perfil e executa as regras com base nos dados do perfil. Saiba mais sobre a [extensão de perfil](https://developer.adobe.com/client-sdks/documentation/profile/) na documentação

>[!IMPORTANT]
>
>A funcionalidade de perfil descrita nesta lição é separada da funcionalidade de perfil do cliente em tempo real nos aplicativos da Adobe Experience Platform e da plataforma.


## Pré-requisitos

* O aplicativo com SDKs instalados e configurados foi criado e executado com sucesso.

## Objetivos de aprendizagem

Nesta lição, você vai:

* Definir ou atualizar atributos do usuário.
* Recuperar atributos do usuário.


## Definir e atualizar atributos do usuário

Seria útil para direcionamento e personalização no aplicativo saber rapidamente se um usuário fez uma compra no passado ou recentemente. Vamos configurar isso no aplicativo Luma.

>[!BEGINTABS]

>[!TAB iOS]

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!DNL MobileSDK]** no navegador do Projeto Xcode e localize a função `func updateUserAttribute(attributeName: String, attributeValue: String)`. Adicione o seguinte código:

   ```swift
   // Create a profile map, add attributes to the map and update profile using the map
   var profileMap = [String: Any]()
   profileMap[attributeName] = attributeValue
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

   Este código:

   1. Configura um dicionário vazio chamado `profileMap`.

   1. Adiciona um elemento ao dicionário usando `attributeName` (por exemplo `isPaidUser`) e `attributeValue` (por exemplo `yes`).

   1. Usa o dicionário `profileMap` como valor para o parâmetro `attributeDict` da chamada de API [`UserProfile.updateUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattributes).

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!DNL ProductView]** no navegador do Projeto Xcode e localize a chamada para `updateUserAttributes` (dentro do código do botão Compras ![Cartão de Crédito](/help/assets/icons/CreditCard.svg)). Adicione o seguinte código:

   ```swift
   // Update attributes
   MobileSDK.shared.updateUserAttribute(attributeName: "isPaidUser", attributeValue: "yes")
   ```

>[!TAB Android]

1. Navegue até **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL templates]** > **[!UICONTROL MobileSDK]** no navegador do Android Studio e localize a função `func updateUserAttribute(attributeName: String, attributeValue: String)`. Adicione o seguinte código:

   ```kotlin
   // Create a profile map, add attributes to the map and update profile using the map
   val profileMap = mapOf(attributeName to attributeValue)
   UserProfile.updateUserAttributes(profileMap)
   ```

   Este código:

   1. Configura um mapa vazio chamado `profileMap`.

   1. Adiciona um elemento ao mapa usando `attributeName` (por exemplo `isPaidUser`) e `attributeValue` (por exemplo `yes`).

   1. Usa o mapa `profileMap` como valor para o parâmetro `attributeDict` da chamada de API [`UserProfile.updateUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattributes).

1. Navegue até **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL visualizações]** > **[!UICONTROL ProductView.kt]** e localize a chamada para `updateUserAttributes` (dentro do código do botão Compras ![Cartão de Crédito](/help/assets/icons/CreditCard.svg)). Adicione o seguinte código:

   ```kotlin
   // Update attributes
   MobileSDK.shared.updateUserAttribute("isPaidUser", "yes")
   ```

>[!ENDTABS]

## Obter atributos do usuário

Depois de atualizar o atributo de um usuário, ele estará disponível para outros SDKs da Adobe, mas você também poderá recuperar os atributos explicitamente para permitir que seu aplicativo se comporte da maneira que você desejar.

>[!BEGINTABS]

>[!TAB iOS]

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!DNL HomeView]** no navegador do Projeto Xcode e localize o modificador `.onAppear`. Adicione o seguinte código:

   ```swift
   // Get attributes
   UserProfile.getUserAttributes(attributeNames: ["isPaidUser"]) { attributes, error in
       if attributes?.count ?? 0 > 0 {
           if attributes?["isPaidUser"] as? String == "yes" {
               showBadgeForUser = true
           }
           else {
               showBadgeForUser = false
           }
       }
   }
   ```

   Este código:

   1. Chama a API [`UserProfile.getUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes) com o nome de atributo `isPaidUser` como elemento único na matriz `attributeNames`.
   1. Em seguida, verifica o valor do atributo `isPaidUser` e, quando `yes`, coloca um selo no ícone ![UserCheckedOut](/help/assets/icons/UserCheckedOut.svg) na barra de ferramentas, na parte superior direita.

>[!TAB Android]

1. Navegue até **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.androi]** > **[!DNL views]** > **[!DNL HomeView.kt]** no navegador de projetos do Android Studio e localize o modificador `.onAppear`. Adicione o seguinte código:

   ```kotlin
   // Get attributes
   UserProfile.getUserAttributes(listOf("isPaidUser")) { attributes ->
       showBadgeForUser = attributes?.get("isPaidUser") == "yes"
   }
   ```

   Este código:

   1. Chama a API [`UserProfile.getUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes) com o nome de atributo `isPaidUser` como elemento único na matriz `attributeNames`.
   1. Em seguida, verifica o valor do atributo `isPaidUser`. Quando `yes`, o código substitui o ícone de pessoa por um ícone de selo na barra de ferramentas na parte superior direita.

>[!ENDTABS]

Consulte a [Referência da API](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes) para obter mais informações.

## Validar com o Assurance

1. Revise a seção [instruções de instalação](assurance.md#connecting-to-a-session) para conectar seu simulador ou dispositivo ao Assurance.
1. Execute o aplicativo para fazer logon e interagir com um produto.

>[!BEGINTABS]

>[!TAB iOS]

1. Selecione **[!UICONTROL Página inicial]** na barra de guias.
1. Mova o ícone do Assurance para a esquerda.
1. Para abrir a folha Logon, selecione o botão ![Usuário](/help/assets/icons/User.svg).

   <img src="./assets/mobile-app-events-1.png" width="300">

1. Para inserir um email e uma ID do cliente aleatórios, selecione o botão > .
1. Selecione **[!UICONTROL Logon]**.

   <img src="./assets/mobile-app-events-2.png" width="300">

1. Selecione **[!DNL Products]** na barra de guias.
1. Selecione um produto.
1. Selecione ![Coração](/help/assets/icons/Heart.svg).
1. Selecione ![ShoppingCart](/help/assets/icons/ShoppingCart.svg).
1. Selecione ![CreditCard](/help/assets/icons/CreditCard.svg).

   <img src="./assets/mobile-app-events-3.png" width="300">

1. Voltar à tela **[!UICONTROL Residencial]**. Você deve ver que uma medalha foi adicionada ![UserCheckedOut](/help/assets/icons/UserCheckedOut.svg).

   <img src="./assets/personbadges.png" width="300">


>[!TAB Android]

1. Selecione **[!UICONTROL Página inicial]** na barra de guias.
1. Mova o ícone do Assurance para a esquerda.
1. Para abrir a folha Logon, selecione o botão ![Usuário](/help/assets/icons/User.svg).

   <img src="./assets/mobile-app-events-1-android.png" width="300">

1. Para inserir um email e uma ID de cliente aleatórios, selecione **[!UICONTROL Gerar Email Aleatório]**.
1. Selecione **[!UICONTROL Logon]**.

   <img src="./assets/mobile-app-events-2-android.png" width="300">

1. Selecione **[!DNL Products]** na barra de guias.
1. Selecione um produto.
1. Selecionar ![Miniatura](/help/assets/icons/ThumbUp.svg)
1. Selecione ![ShoppingCart](/help/assets/icons/ShoppingCart.svg).
1. Selecione ![CreditCard](/help/assets/icons/CreditCard.svg).

   <img src="./assets/mobile-app-events-3-android.png" width="300">

1. Voltar à tela **[!UICONTROL Residencial]**. Você verá que o ícone de pessoa foi atualizado.

   <img src="./assets/personbadges-android.png" width="300">

>[!ENDTABS]


Na interface do usuário do Assurance, você deve ver eventos de **[!UICONTROL UserProfileUpdate]** e **[!UICONTROL getUserAttributes]** com o valor `profileMap` atualizado.

![validar perfil](assets/profile-validate.png){zoomable="yes"}

>[!SUCCESS]
>
>Agora você configurou seu aplicativo para atualizar atributos de perfis na Edge Network e (quando configurado) com o Adobe Experience Platform.
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-os nesta [postagem de discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=pt).

Próximo: **[Usar Locais](places.md)**
