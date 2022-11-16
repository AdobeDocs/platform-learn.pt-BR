---
title: Consentimento
description: Saiba como implementar o consentimento em um aplicativo móvel.
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 7%

---

# Consentimento

Saiba como implementar o consentimento em um aplicativo móvel.

A extensão Adobe Experience Platform Consent para dispositivos móveis permite a coleta de preferências de consentimento do seu aplicativo móvel ao usar o SDK do Adobe Experience Platform Mobile e a extensão Edge Network. Saiba mais sobre o [Extensão de consentimento](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network)na documentação.

## Pré-requisitos

* Aplicativo criado e executado com êxito com SDKs instalados e configurados.

## Objetivos de aprendizagem

Nesta lição, você:

* Solicite consentimento ao usuário.
* Atualize a extensão com base na resposta do usuário.
* Saiba como obter o estado de consentimento atual.

## Solicitar consentimento

Se você seguiu o tutorial desde o início, lembre-se de definir a variável **[!UICONTROL Nível de consentimento padrão]** para &quot;Pendente&quot;. Para começar a coletar dados, você deve obter consentimento do usuário. Neste tutorial, obtenha consentimento simplesmente perguntando com um alerta, em um aplicativo real, se deseja consultar as práticas recomendadas de consentimento para sua região.

1. Você só deseja perguntar ao usuário uma vez. Uma maneira simples de gerenciar isso é simplesmente usando `UserDefaults`.
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

A extensão Consent mobile suprimirá/acrescentará/permitirá automaticamente o rastreamento com base no valor de consentimento atual. Você também pode acessar o estado de consentimento atual por conta própria:

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

## Validar com Controle de Controle

1. Revise o [Controle](assurance.md) lição.
1. Instale o aplicativo.
1. Inicie o aplicativo usando o URL gerado pelo Assurance.
1. Se você tiver adicionado o código acima corretamente, será solicitado a fornecer consentimento. Selecionar **Sim**.
   ![pop-up de consentimento](assets/mobile-consent-validate.png)
1. Você deve ver um **[!UICONTROL Preferências de consentimento atualizadas]** na interface do usuário de garantia.
   ![validar consentimento](assets/mobile-consent-update.png)

Próximo: **[Coletar dados do ciclo de vida](lifecycle-data.md)**

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender sobre o Adobe Experience Platform Mobile SDK. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)