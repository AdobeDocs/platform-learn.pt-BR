---
title: Consentimento
description: Saiba como implementar o consentimento em um aplicativo móvel.
feature: Mobile SDK,Consent
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: bc53cb5926f708408a42aa98a1d364c5125cb36d
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 6%

---

# Consentimento

Saiba como implementar o consentimento em um aplicativo móvel.

>[!INFO]
>
> Este tutorial será substituído por um novo tutorial usando um novo aplicativo móvel de amostra no final de novembro de 2023

A extensão móvel do Adobe Experience Platform Consent permite a coleta de preferências de consentimento do aplicativo móvel ao usar o SDK móvel da Adobe Experience Platform e a extensão de rede de borda. Saiba mais sobre o [Extensão de consentimento](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/), na documentação.

## Pré-requisitos

* O aplicativo com SDKs instalados e configurados foi criado e executado com sucesso.

## Objetivos de aprendizagem

Nesta lição, você vai:

* Solicitar consentimento do usuário.
* Atualize a extensão com base na resposta do usuário.
* Saiba como obter o estado de consentimento atual.

## Solicitar consentimento

Se tiver seguido o tutorial desde o início, você se lembrará de definir a variável **[!UICONTROL Nível de consentimento padrão]** para &quot;Pendente&quot;. Para começar a coletar dados, você deve obter o consentimento do usuário. Neste tutorial, obtenha consentimento simplesmente perguntando com um alerta: em um aplicativo do mundo real, você pode consultar as práticas recomendadas de consentimento para sua região.

1. Você só deseja perguntar ao usuário uma vez. Uma maneira simples de gerenciar isso é usando `UserDefaults`.
1. Navegue até `Home.swift`.
1. Adicione o código a seguir a `viewDidLoad()`.

   ```swift
   let defaults = UserDefaults.standard
   let consentKey = "askForConsentYet"
   let hidePopUp = defaults.bool(forKey: consentKey)
   ```

1. Se o usuário não tiver visto o alerta antes, exiba-o e atualize o consentimento com base em sua resposta. Adicione o código a seguir a `viewDidLoad()`.

   ```swift
   if(hidePopUp == false){
       //Consent Alert
       let alert = UIAlertController(title: "Allow Data Collection?", message: "Selecting Yes will begin data collection", preferredStyle: .alert)
       alert.addAction(UIAlertAction(title: "Yes", style: .default, handler: { action in
           //Update Consent -> "yes"
           let collectConsent = ["collect": ["val": "y"]]
           let currentConsents = ["consents": collectConsent]
           Consent.update(with: currentConsents)
           defaults.set(true, forKey: consentKey)
       }))
       alert.addAction(UIAlertAction(title: "No", style: .cancel, handler: { action in
           //Update Consent -> "no"
           let collectConsent = ["collect": ["val": "n"]]
           let currentConsents = ["consents": collectConsent]
           Consent.update(with: currentConsents)
           defaults.set(true, forKey: consentKey)
       }))
       self.present(alert, animated: true)
   }
   ```


## Obter estado de consentimento atual

A extensão Consent mobile suprimirá/pendente/permitirá automaticamente o rastreamento com base no valor de consentimento atual. Você também pode acessar o estado de consentimento atual sozinho:

1. Navegue até `Home.swift`.
1. Adicione o código a seguir a `viewDidLoad()`.

```swift
Consent.getConsents{ consents, error in
    guard error == nil, let consents = consents else { return }
    guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
    guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
    print("Consent getConsents: ",jsonStr)
}
```

No exemplo acima, você está simplesmente imprimindo o status de consentimento para o console. Em um cenário real, você pode usá-lo para modificar quais menus ou opções são mostrados ao usuário.

## Validar com garantia

1. Revise o [Assurance](assurance.md) lição.
1. Instale o aplicativo.
1. Inicie o aplicativo usando o URL gerado pelo Assurance.
1. Se você adicionou o código acima corretamente, será solicitado a fornecer consentimento. Selecionar **Sim**.
   ![pop-up de consentimento](assets/mobile-consent-validate.png)
1. Você deve ver um **[!UICONTROL Preferências de consentimento atualizadas]** evento na interface do usuário do Assurance.
   ![validar consentimento](assets/mobile-consent-update.png)

Próximo: **[Coletar dados do ciclo de vida](lifecycle-data.md)**

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)