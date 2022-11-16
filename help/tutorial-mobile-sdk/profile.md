---
title: Perfil
description: Saiba como coletar dados de perfil em um aplicativo móvel.
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 2%

---

# Perfil

Saiba como coletar dados de perfil em um aplicativo móvel.

Você pode usar a extensão Profile para armazenar atributos sobre seu usuário no cliente. Essas informações podem ser usadas posteriormente para direcionar e personalizar mensagens durante cenários online ou offline, sem precisar se conectar a um servidor para obter o melhor desempenho. A extensão Profile gerencia o CSOP (Client-Side Operation Profile), fornece uma maneira de reagir a APIs, atualiza os atributos do perfil do usuário e compartilha os atributos do perfil do usuário com o restante do sistema como um evento gerado.

Os dados do perfil são usados por outras extensões para executar ações relacionadas ao perfil. Um exemplo é a extensão do Mecanismo de regras que consome os dados do perfil e executa regras com base nos dados do perfil. Saiba mais sobre o [Extensão do perfil](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile) na documentação

>[!IMPORTANT]
>
>A funcionalidade Perfil descrita nesta lição é separada da funcionalidade Perfil do cliente em tempo real no Adobe Experience Platform e nos aplicativos baseados na plataforma.


## Pré-requisitos

* Aplicativo criado e executado com êxito com SDKs instalados e configurados.
* Importado o SDK do perfil.

   ```swift
   import AEPUserProfile
   ```

## Objetivos de aprendizagem

Nesta lição, você:

* Defina ou atualize os atributos do usuário.
* Recupere os atributos do usuário.


## Definir e atualizar

Seria útil para direcionamento e/ou personalização saber rapidamente se um usuário tinha feito uma compra no aplicativo antes. Vamos configurar isso no aplicativo Luma.

1. Navegue até `Cart.swift`

1. Adicione o código abaixo à `processOrder() `.

   ```swift
   var profileMap = [String: Any]()
   profileMap["isPaidUser"] = "yes"
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

A equipe de personalização também pode desejar direcionar com base no nível de fidelidade do usuário. Vamos configurar isso no aplicativo Luma.

1. Navegue até `Account.swift`

1. Adicione o código abaixo à `showUserInfo()` .

   ```swift
   var profileMap = [String: Any]()
   profileMap["loyaltyLevel"] = loyaltyLevel
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

Adicional `updateUserAttributes` a documentação pode ser encontrada [here](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile/profile-api-references#update-user-attributes).

## Obtenha

Depois de atualizar o atributo do usuário, ele estará disponível para outros SDKs do Adobe, mas você também poderá recuperar atributos explicitamente.

```swift
UserProfile.getUserAttributes(attributeNames: ["isPaidUser","loyaltyLevel"]){
    attributes, error in
    print("Profile: getUserAttributes: ",attributes as Any)
}
```

Adicional `getUserAttributes` a documentação pode ser encontrada [here](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile/profile-api-references#get-user-attributes).

## Validar com Controle de Controle

1. Revise o [instruções de configuração](assurance.md) seção.
1. Instale o aplicativo.
1. Inicie o aplicativo usando o URL gerado pelo Assurance.
1. Selecione o ícone Conta e selecione Logon. Observação: você não tem credenciais.
1. Feche os menus de logon e selecione o ícone Conta novamente. Isso leva você à tela de detalhes da conta, onde `loyaltyLevel` está definida.
1. Você deve ver um **[!UICONTROL UserProfileUpdate]** na interface do usuário de controle com o evento atualizado `profileMap` valor.
   ![validar perfil](assets/mobile-profile-validate.png)

Próximo: **[Mapear dados para o Adobe Analytics](analytics.md)**

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender sobre o Adobe Experience Platform Mobile SDK. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)