---
title: Identidade
description: Saiba como coletar dados de identidade em um aplicativo móvel.
exl-id: cbcd1708-29e6-4d74-be7a-f75c917ba2fa
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 4%

---

# Identidade

Saiba como coletar dados de identidade em um aplicativo móvel.

O serviço de identidade da Adobe Experience Platform ajuda você a obter uma melhor visão de seus clientes e seus comportamentos ao unir identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real. Campos de identidade e namespaces são a cola que une diferentes fontes de dados para criar o perfil do cliente em tempo real de 360 graus.

Saiba mais sobre o [Extensão de identidade](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network) e [serviço de identidade](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=pt-BR) na documentação.

## Pré-requisitos

* Aplicativo criado e executado com êxito com SDKs instalados e configurados.

## Objetivos de aprendizagem

Nesta lição, você:

* Atualize uma identidade padrão.
* Configure uma identidade personalizada.
* Atualize uma identidade personalizada.
* Valide o gráfico de identidade.
* Obtenha ECID e outras identidades.

## Atualizar uma identidade padrão

Comece atualizando o mapa de identidade do usuário quando ele fizer logon.

1. Navegar para `Login.swift` se o aplicativo Luma e a função chamada `loginButt`.

   No aplicativo de amostra Luma, não há validação de nome de usuário ou senha. Basta tocar nos botões para &quot;fazer logon&quot;.

1. Crie o `IdentityMap` e `IdentityItem`.

   ```swift
   let identityMap: IdentityMap = IdentityMap()
   let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
   ```

1. Adicione o `IdentityItem` para `IdentityMap`

   ```swift
   identityMap.add(item:emailIdentity, withNamespace: "Email")
   ```

1. Chame `updateIdentities` para enviar os dados para a Rede de borda da plataforma.

   ```swift
   Identity.updateIdentities(with: identityMap)
   ```

>[!NOTE]
>
>Você pode enviar várias identidades em uma única chamada updateIdentities . Também é possível modificar identidades enviadas anteriormente.


## Configurar um namespace de identidade personalizado

Os namespaces de identidade são componentes de [Serviço de identidade](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=en) que servem como indicadores do contexto a que uma identidade se refere. Por exemplo, eles distinguem um valor de &quot;name@email.com&quot; como um endereço de email ou &quot;443522&quot; como uma ID de CRM numérica.

1. Na interface da Coleta de dados, selecione **[!UICONTROL Identidades]** no painel de navegação esquerdo.
1. Selecionar **[!UICONTROL Criar namespace de identidade]**.
1. Forneça uma **[!UICONTROL Nome de exibição]** de `Luma CRM ID` e um **[!UICONTROL Símbolo de identidade]** valor de `lumaCrmId`.
1. Selecionar **[!UICONTROL ID entre dispositivos]**.
1. Selecione **[!UICONTROL Criar]**.

![criar namespace de identidade](assets/mobile-identity-create.png)

## Atualizar uma identidade personalizada

Agora que você criou uma identidade personalizada, comece a coletá-la modificando a variável `updateIdentities` código adicionado na etapa anterior. Basta criar um IdentityItem e adicioná-lo ao IdentityMap. Veja como o bloco de código completo deve ser:

```swift
//Hardcoded identity values
let emailAddress = "testuser@gmail.com"
let crmId = "112ca06ed53d3db37e4cea49cc45b71e"

// Create identity map
let identityMap: IdentityMap = IdentityMap()
// Add email (standard)
let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
identityMap.add(item:emailIdentity, withNamespace: "Email")
// Add lumaCrmId (custom)
let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
identityMap.add(item: crmIdentity, withNamespace: "lumaCrmId")
// Update
Identity.updateIdentities(with: identityMap)
```

## Remover uma identidade

Você pode usar `removeIdentity` para remover a identidade do IdentityMap do lado do cliente armazenado. A extensão Identity interrompe o envio do identificador para a Rede de borda. Usar essa API não remove o identificador do Gráfico de perfil do usuário do lado do servidor ou do Gráfico de identidade.

Adicione o seguinte `removeIdentity` código para o botão de logout, clique em `Account.swift`.

```swift
// Logout
let logout = UIAlertAction(title: "Logout", style: .destructive, handler: { (action) -> Void in
    isLoggedIn = false;
    ////Hardcoded identity values
    let emailAddress = "testuser@gmail.com"
    let crmId = "112ca06ed53d3db37e4cea49cc45b71e"
    // Adobe Experience Platform - Remove Identity
    Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
    Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCrmId")
})
```

>[!NOTE]
>Nos exemplos acima, `crmId` e `emailAddress` são codificados, mas em um aplicativo real, os valores seriam dinâmicos.

## Validar com Controle de Controle

1. Revise o [instruções de configuração](assurance.md) e conecte seu simulador ou dispositivo ao Controle.
1. No aplicativo, selecione o ícone Conta na parte inferior direita.

   ![conta de aplicativo luma](assets/mobile-identity-login.png)
1. Selecione o **Fazer logon** botão.
1. Você tem a opção de inserir um nome de usuário e senha, ambos são opcionais e você pode simplesmente selecionar **Fazer logon**.

   ![logon do aplicativo luma](assets/mobile-identity-login-final.png)
1. Procure na interface do usuário da Web do Controle de qualidade do `Edge Identity Update Identities` do `com.adobe.griffon.mobile` fornecedor.
1. Selecione o evento e revise os dados na `ACPExtensionEventData` objeto. Você deve ver as identidades que atualizou.
   ![validar atualização de identidades](assets/mobile-identity-validate-assurance.png)

## Validar com gráfico de identidade

Depois de concluir as etapas na [lição de Experience Platform](platform.md), você também poderá confirmar a captura de inatividade no visualizador de gráficos de identidade das Plataformas:

![validar gráfico de identidade](assets/mobile-identity-validate.png)


Próximo: **[Perfil](profile.md)**

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender sobre o Adobe Experience Platform Mobile SDK. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)