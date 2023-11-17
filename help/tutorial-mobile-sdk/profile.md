---
title: Perfil
description: Saiba como coletar dados de perfil em um aplicativo móvel.
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: 94ca4a238c241518219fb2e8d73f775836f86d86
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 2%

---

# Perfil

Saiba como coletar dados de perfil em um aplicativo móvel.

>[!INFO]
>
> Este tutorial será substituído por um novo tutorial usando um novo aplicativo móvel de amostra no final de novembro de 2023

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

1. Navegue até `Cart.swift`

1. Adicione o código abaixo a `processOrder() `função.

   ```swift
   var profileMap = [String: Any]()
   profileMap["isPaidUser"] = "yes"
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

A equipe de personalização também pode querer definir metas com base no nível de fidelidade do usuário. Vamos configurar isso no aplicativo Luma.

1. Navegue até `Account.swift`

1. Adicione o código abaixo a `showUserInfo()` função.

   ```swift
   var profileMap = [String: Any]()
   profileMap["loyaltyLevel"] = loyaltyLevel
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

Adicional `updateUserAttributes` a documentação pode ser encontrada [aqui](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattribute).

## Obtenha

Depois de atualizar o atributo de um usuário, ele estará disponível para outros SDKs Adobe, mas você também poderá recuperar os atributos explicitamente.

```swift
UserProfile.getUserAttributes(attributeNames: ["isPaidUser","loyaltyLevel"]){
    attributes, error in
    print("Profile: getUserAttributes: ",attributes as Any)
}
```

Adicional `getUserAttributes` a documentação pode ser encontrada [aqui](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## Validar com garantia

1. Revise o [instruções de configuração](assurance.md) seção.
1. Instale o aplicativo.
1. Inicie o aplicativo usando o URL gerado pelo Assurance.
1. Selecione o ícone Conta e selecione Logon. Observação: você não tem nenhuma credencial.
1. Feche os menus de logon e selecione o ícone Conta novamente. Isso exibe a tela de detalhes da conta, onde `loyaltyLevel` está definido.
1. Você deve ver um **[!UICONTROL UserProfileUpdate]** evento na interface do usuário do Assurance com o `profileMap` valor.
   ![validar perfil](assets/mobile-profile-validate.png)

Próximo: **[Mapear dados para o Adobe Analytics](analytics.md)**

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar feedback geral ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)