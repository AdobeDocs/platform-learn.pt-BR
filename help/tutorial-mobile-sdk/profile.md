---
title: Coletar dados de perfil com o SDK móvel da Platform
description: Saiba como coletar dados de perfil em um aplicativo móvel.
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: d353de71d8ad26d2f4d9bdb4582a62d0047fd6b1
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 1%

---

# Coletar dados de perfil

Saiba como coletar dados de perfil em um aplicativo móvel.

Você pode usar a extensão Profile para armazenar atributos sobre seu usuário no cliente. Essas informações podem ser usadas posteriormente para direcionar e personalizar mensagens em cenários online ou offline, sem precisar se conectar a um servidor para obter o desempenho ideal. A extensão Perfil gerencia o CSOP (Perfil de operação do lado do cliente), fornece uma maneira de reagir a APIs, atualiza atributos de perfil do usuário e compartilha os atributos de perfil do usuário com o restante do sistema como um evento gerado.

Os dados do Perfil são usados por outras extensões para executar ações relacionadas ao perfil. Um exemplo é a extensão Mecanismo de regras que consome os dados do perfil e executa as regras com base nos dados do perfil. Saiba mais sobre o [Extensão de perfil](https://developer.adobe.com/client-sdks/documentation/profile/) na documentação

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

Seria útil para direcionamento e/ou personalização no aplicativo saber rapidamente se um usuário fez uma compra no passado ou recentemente. Vamos configurar isso no aplicativo Luma.

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** >  **[!DNL MobileSDK]** no navegador do Projeto Xcode e localize o `func updateUserAttribute(attributeName: String, attributeValue: String)` função. Adicione o seguinte código:

   ```swift
   // Create a profile map, add attributes to the map and update profile using the map
   var profileMap = [String: Any]()
   profileMap[attributeName] = attributeValue
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

   Este código:

   1. Configura um dicionário vazio chamado `profileMap`.

   1. Adiciona um elemento ao dicionário usando `attributeName` (por exemplo `isPaidUser`) e `attributeValue` (por exemplo `yes`).

   1. Usa o `profileMap` dicionário como um valor para o `attributeDict` parâmetro do [`UserProfile.updateUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattributes) chamada à API.

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!DNL ProductView]** no navegador do Projeto Xcode e localize a chamada para `updateUserAttributes` (no código para Compras <img src="assets/purchase.png" width="15" /> botão). Adicione o seguinte código:

   ```swift
   // Update attributes
   MobileSDK.shared.updateUserAttribute(attributeName: "isPaidUser", attributeValue: "yes")
   ```


## Obter atributos do usuário

Depois de atualizar o atributo de um usuário, ele fica disponível para outros SDKs Adobe, mas você também pode recuperar atributos explicitamente, para permitir que seu aplicativo se comporte da maneira que você quiser.

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!DNL HomeView]** no navegador do Projeto Xcode e localize o `.onAppear` modificador. Adicione o seguinte código:

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

   1. Chama o [`UserProfile.getUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes) API com o `isPaidUser` nome do atributo como elemento único na variável `attributeNames` matriz.
   1. Em seguida, verifica o valor de `isPaidUser` atributo e quando `yes`, coloca um selo na <img src="assets/paiduser.png" width="20" /> ícone na barra de ferramentas na parte superior direita.

A documentação adicional pode ser encontrada [aqui](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## Validar com garantia

1. Revise o [instruções de configuração](assurance.md#connecting-to-a-session) seção para conectar seu simulador ou dispositivo ao Assurance.
1. Execute o aplicativo para fazer logon e interagir com um produto.

   1. Mova o ícone do Assurance para a esquerda.
   1. Selecionar **[!UICONTROL Início]** na barra de guias.
   1. Para abrir a planilha de Logon, selecione o <img src="assets/login.png" width="15" /> botão.

      <img src="./assets/mobile-app-events-1.png" width="300">

   1. Para inserir um email e uma ID do cliente aleatórios, selecione <img src="assets/insert.png" width="15" /> botão .
   1. Selecionar **[!UICONTROL Logon]**.

      <img src="./assets/mobile-app-events-2.png" width="300">

   1. Selecionar **[!DNL Products]** na barra de guias.
   1. Selecione um produto.
   1. Selecionar <img src="assets/saveforlater.png" width="15" />.
   1. Selecionar <img src="assets/addtocart.png" width="20" />.
   1. Selecionar <img src="assets/purchase.png" width="15" />.

      <img src="./assets/mobile-app-events-3.png" width="300">

   1. Retornar para **[!UICONTROL Início]** tela. Você verá que uma medalha foi adicionada <img src="assets/person-badge-icon.png" width="15" />.

      <img src="./assets/personbadges.png" width="300">



1. Na interface do usuário do Assurance, você deve ver uma **[!UICONTROL UserProfileUpdate]** e **[!UICONTROL getUserAttributes]** eventos com o atualizado `profileMap` valor.
   ![validar perfil](assets/profile-validate.png)

>[!SUCCESS]
>
>Agora você configurou o aplicativo para atualizar atributos de perfis na Rede de borda e (quando configurado) com o Adobe Experience Platform.
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Próximo: **[Usar locais](places.md)**
