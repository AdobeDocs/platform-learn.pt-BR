---
title: Perfil
description: Saiba como coletar dados de perfil em um aplicativo móvel.
hide: true
source-git-commit: 4101425bd97e271fa6cc15157a7be435c034e764
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 2%

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


## Definir e atualizar atributos do usuário

Seria útil para direcionamento e/ou personalização saber rapidamente se um usuário fez uma compra no aplicativo antes. Vamos configurar isso no aplicativo Luma.

1. Navegue até **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** >  **[!UICONTROL MobileSDK]** no navegador do Projeto Xcode e localize o `func updateUserAttribute(attributeName: String, attributeValue: String)` função. Adicione o seguinte código:

   ```swift
   // Create a profile map
   var profileMap = [String: Any]()
   // Add attributes to profile map
   profileMap[attributeName] = attributeValue
   // Use profile map to update user attributes
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

   Este código:

   1. Configura um dicionário vazio chamado `profileMap`.

   1. Adiciona um elemento ao dicionário usando `attributeName` (por exemplo `isPaidUser`) e `attributeValue` (por exemplo `yes`).

   1. Usa o `profileMap` dicionário como um valor para o `attributeDict` parâmetro do `UserProfile.updateUserAttributes` chamada à API.

1. Navegue até **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Visualizações]** > **[!UICONTROL Produtos]** > **[!UICONTROL ProductView]** no navegador do Projeto Xcode e localize a chamada para `updateUserAttributes` (no código para Compras <img src="assets/purchase.png" width="15" /> botão):

   ```swift
   // Update attributes
   MobileSDK.shared.updateUserAttributes(attributeName: "isPaidUser", attributeValue: "yes")
   ```

A documentação adicional pode ser encontrada [aqui](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattribute).

## Obter atributos do usuário

Depois de atualizar o atributo de um usuário, ele estará disponível para outros SDKs Adobe, mas você também poderá recuperar os atributos explicitamente.

1. Navegue até **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Visualizações]** > Geral > **[!UICONTROL HomeView]** no navegador do Projeto Xcode e localize o `.onAppear` modificador. Adicione o seguinte código:

   ```swift
   // Get attributes
   UserProfile.getUserAttributes(attributeNames: ["isPaidUser"]) { attributes, error in
       if attributes?["isPaidUser"] as! String == "yes" {
           showBadgeForUser = true
       }
       else {
           showBadgeForUser = false
       }
   }
   ```

   Este código:

   1. Chama o `UserProfile.getUserAttributes` encerramento com a `iPaidUser` nome do atributo como elemento único na variável `attributeNames` matriz.
   1. Em seguida, verifica o valor de `isPaidUser` atributo e quando `yes`, coloca um selo na <img src="assets/paiduser.png" width="20" /> ícone na barra de ferramentas na parte superior direita.

A documentação adicional pode ser encontrada [aqui](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## Validar com garantia

1. Revise o [instruções de configuração](assurance.md) seção.
1. Instale o aplicativo.
1. Inicie o aplicativo usando o URL gerado pelo Assurance.
1. Execute o aplicativo para fazer logon e interagir com um produto.

   1. Mova o ícone do Assurance para a esquerda.
   1. Selecionar **[!UICONTROL Início]** na barra de guias.
   1. Para abrir a planilha de Logon, selecione o <img src="assets/login.png" width="15" /> botão.
   1. Para inserir um email e uma ID do cliente aleatórios, selecione <img src="assets/insert.png" width="15" /> botão .
   1. Selecionar **[!UICONTROL Logon]**.
   1. Selecionar **[!UICONTROL Produtos]** na barra de guias.
   1. Selecione um produto.
   1. Selecionar <img src="assets/saveforlater.png" width="15" />.
   1. Selecionar <img src="assets/addtocart.png" width="20" />.
   1. Selecionar <img src="assets/purchase.png" width="15" />.

      <img src="./assets/mobile-app-events-1.png" width="200"> <img src="./assets/mobile-app-events-2.png" width="200"> <img src="./assets/mobile-app-events-3.png" width="200">
   1. Retornar para **[!UICONTROL Início]** tela. Você deve ver uma medalha adicionada <img src="assets/person-badge-icon.png" width="15" />.

      <img src="./assets/personbadges.png" width="200">



1. Na interface do usuário do Assurance, você deve ver uma **[!UICONTROL UserProfileUpdate]** e **[!UICONTROL getUserAttributes]** eventos com o atualizado `profileMap` valor.
   ![validar perfil](assets/profile-validate.png)

>[!SUCCESS]
>
>Agora você configurou o aplicativo para atualizar atributos de perfis na Rede de borda e (quando configurado) com o Adobe Experience Platform.<br/>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Próximo: **[Mapear dados para o Adobe Analytics](analytics.md)**
