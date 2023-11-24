---
title: Configurar o Assurance
description: Saiba como implementar a extensão Assurance em um aplicativo móvel.
feature: Mobile SDK,Assurance
hide: true
exl-id: 49d608e7-e9c4-4bc8-8a8a-5195f8e2ba42
source-git-commit: d1338390986a242c91051e94134f8d69e979c0b4
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 7%

---

# Configurar o Assurance

Saiba como configurar o Adobe Experience Platform Assurance em um aplicativo móvel.

O Assurance, formalmente conhecido como Projeto Griffon, foi projetado para ajudá-lo a inspecionar, testar, simular e validar a maneira como você coleta dados ou veicula experiências em seu aplicativo móvel.

O Assurance ajuda a inspecionar eventos brutos de SDK gerados pelo SDK móvel da Adobe Experience Platform. Todos os eventos coletados pelo SDK estão disponíveis para inspeção. Os eventos do SDK são carregados em uma exibição de lista classificada por tempo. Cada evento tem uma exibição detalhada que fornece mais detalhes. Exibições adicionais para procurar a configuração do SDK, elementos de dados, Estados compartilhados e versões de extensão do SDK também são fornecidas. Saiba mais sobre o [Assurance](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html) na documentação do produto.


## Pré-requisitos

* Aplicativo com SDKs instalado e configurado com êxito.

## Objetivos de aprendizagem

Nesta lição, você vai:

* Confirme se sua organização tem acesso (e solicite-o caso não tenha).
* Configure seu URL base.
* Adicione o código específico necessário do iOS.
* Conectar-se a uma sessão.

## Confirmar acesso

Confirme se sua organização tem acesso ao Assurance. Você, como usuário, deve ser adicionado ao perfil do Adobe Experience Platform. Consulte [Acesso do usuário](https://experienceleague.adobe.com/docs/experience-platform/assurance/user-access.html?lang=en) no guia do Assurance para obter mais informações.

## Implementação

Para além do quadro [Instalação do SDK](install-sdks.md), que você concluiu na lição anterior, o iOS também exige a seguinte adição para iniciar a sessão do Assurance para seu aplicativo.

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL SceneDelegate]** no navegador de projetos do Xcode.

1. Adicione o código a seguir a `func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>`:

   ```swift
   // Called when the app in background is opened with a deep link.
   if let deepLinkURL = URLContexts.first?.url {
       // Start the Assurance session
       Assurance.startSession(url: deepLinkURL)
   }
   ```

   Esse código inicia uma sessão de controle quando o aplicativo é colocado em segundo plano e aberto usando um deep link.

Mais informações podem ser encontradas [aqui](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/api-reference/){target="_blank"}.

<!-- not initially required

## Signing

Signing the application is only required for the [Create and send push notifications](journey-optimizer-push.md) and the [Create and send in-app messages](journey-optimizer-inapp.md) lessons in this tutorial. These lessons require an Apple provisioning profile which **requires a paid Apple developer account**.

To update the signing for the lessons that require that you sign the application:

1. Open the project in Xcode.
1. Select **[!DNL Luma]** in the Project navigator.
1. Select the **[!DNL Luma]** target.
1. Select the **Signing & Capabilities** tab.
1. Configure **[!UICONTROL Automatic manage signing]**, **[!UICONTROL Team]**, and **[!UICONTROL Bundle Identifier]**, or use your specific Apple development provisioning details. 
 
   >[!IMPORTANT]
   >
   >Ensure you use a _unique_ bundle identifier and replace the `com.adobe.luma.tutorial.swiftui` bundle identifier, as each bundle identifier needs to be unique. Typically, you use a reverse-DNS format for bundle ID strings, like `com.organization.brand.uniqueidentifier`. The Finished version of this tutorial, for example, uses `com.adobe.luma.tutorial.swiftui`.


    ![Xcode signing capabilities](assets/xcode-signing-capabilities.png){zoomable="yes"}

-->

## Configurar um URL de base

1. Vá para o seu projeto no Xcode.
1. Selecionar **[!DNL Luma]** no Navegador de projetos.
1. Selecione o **[!DNL Luma]** público-alvo.
1. Selecione o **Informações** guia.
1. Role para baixo até **Tipos de URL (1)** e abra a seção usando a divisa (>) se ainda não estiver aberta.
1. Definir **Identificador** ao Identificador de pacote de sua escolha e defina um **Esquemas de URL** de sua escolha.

   ![url de garantia](assets/assurance-url-type.png)

   >[!IMPORTANT]
   >
   >Certifique-se de usar um _único_ identificador do pacote, substitua o `com.adobe.luma.tutorial.swiftui` identificador de pacote, pois cada identificador de pacote deve ser exclusivo. Normalmente, você usa um formato de DNS reverso para sequências de ID de pacote, como `com.organization.brand.uniqueidentifier`.<br/>Da mesma forma, use um esquema de URL exclusivo, para substituir o já fornecido `lumatutorialswiftui` com seu esquema de URL exclusivo.

Para saber mais sobre Esquemas de URL no iOS, revise [Documentação da Apple](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target="_blank"}.

O Assurance funciona abrindo um URL, seja via navegador ou código QR. Esse URL começa com o URL de base que abre o aplicativo e contém parâmetros adicionais. Esses parâmetros exclusivos são usados para conectar a sessão.


## Conectar-se a uma sessão

No Xcode:

1. Crie ou recrie e execute o aplicativo no simulador ou em um dispositivo físico do Xcode, usando ![Reproduzir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

   >[!TIP]
   >
   >Como opção, você pode querer &quot;limpar&quot; sua build, especialmente quando vir resultados inesperados. Para fazer isso, selecione **[!UICONTROL Limpar pasta de compilação...]** do Xcode **[!UICONTROL Produto]** menu.


1. No **[!UICONTROL Permitir que &quot;Aplicativo Luma&quot; use sua localização]** , selecione **[!UICONTROL Permitir ao usar o aplicativo]**.

   <img src="assets/geolocation-permissions.png" width="300">

1. No **[!UICONTROL &quot;Aplicativo Luma&quot; Deseja Enviar Notificações]** , selecione **[!UICONTROL Permitir]**.

   <img src="assets/notification-permissions.png" width="300">

1. Selecionar **[!UICONTROL Continuar...]** para permitir que o aplicativo acompanhe sua atividade.

   <img src="assets/tracking-continue.png" width="300">

1. No **[!UICONTROL Permitir que o &quot;Aplicativo Luma&quot; rastreie sua atividade nos aplicativos e sites de outras empresas]** , selecione **[!UICONTROL Permitir]**.

   <img src="assets/tracking-allow.png" width="300">


No navegador:

1. Vá para a interface da Coleção de dados.
1. Selecionar **[!UICONTROL Assurance]** do painel esquerdo.
1. Selecionar **[!UICONTROL Criar sessão]**.
1. Selecionar **[!UICONTROL Início]**.
1. Forneça um **[!UICONTROL Nome da sessão]** como `Luma Mobile App Session` e a variável **[!UICONTROL URL base]**, que são os Esquemas de URL inseridos no Xcode, seguidos por `://` Por exemplo: `lumatutorialswiftui://`
1. Selecione **[!UICONTROL Próximo]**.
   ![criação de sessão do assurance](assets/assurance-create-session.png)
1. No **[!UICONTROL Criar nova sessão]** caixa de diálogo modal:

   Se você estiver usando um dispositivo físico:

   * Selecionar **[!UICONTROL Digitalizar código QR]**. Para abrir o aplicativo, use a câmera do dispositivo físico para digitalizar o código QR e toque no link.

     ![código de controle de qualidade do assurance](assets/assurance-qr-code.png)

   Se estiver usando um simulador:

   1. Selecionar **[!UICONTROL Copiar link]**.
   1. Copie o deep link usando ![Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)  e use o deep link para abrir o aplicativo com o Safari no simulador.
      ![Link de cópia de garantia](assets/assurance-copy-link.png)

1. Quando o aplicativo é carregado, uma caixa de diálogo modal é exibida solicitando que você insira o PIN mostrado na etapa 7.

   <img src="assets/assurance-enter-pin.png" width="300">

   Insira o PIN e selecione **[!UICONTROL Conectar]**.


1. Se a conexão tiver sido bem-sucedida, você verá:
   * Um ícone do Assurance flutuando sobre seu aplicativo.

     <img src="assets/assurance-modal.png" width="300">

   * Atualizações de Experience Cloud provenientes da interface do usuário do Assurance, mostrando:

      1. Eventos de experiência provenientes do aplicativo.
      1. Detalhes de um evento selecionado.
      1. O dispositivo e a linha do tempo.

         ![eventos de garantia](assets/assurance-events.png)

Se tiver algum desafio, revise o [técnico](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/){target="_blank"} and [general documentation](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html){target="_blank"}.


## Verificar extensões

Para verificar se seu aplicativo está usando as extensões mais atualizadas:

1. Selecionar **[!UICONTROL Configurar]**.

1. Selecionar ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) para ![123](https://spectrum.adobe.com/static/icons/workflow_18/Smock_123_18_N.svg) **[!UICONTROL Versões de extensão]**.

1. Selecione **[!UICONTROL Salvar]**.

   ![Configurar versões de extensão](assets/assurance-configure-extension-versions.png)

1. Selecionar ![123](https://spectrum.adobe.com/static/icons/workflow_18/Smock_123_18_N.svg) **[!UICONTROL Versões de extensão]** para ter uma visão geral das extensões mais recentes disponíveis e das extensões usadas na sua versão do aplicativo.

   ![Versões de extensão](assets/assurance-extension-versions.png)

1. Para atualizar suas versões de extensão (por exemplo, **[!UICONTROL Mensagens]** e **[!UICONTROL Otimizar]**) selecionar o pacote (extensão) de **[!UICONTROL Dependências de pacote]** (por exemplo, **[!UICONTROL AEPMessaging]**) e, no menu de contexto, selecione **[!UICONTROL Atualizar pacote]**. O Xcode atualizará as dependências do pacote.


>[!NOTE]
>
>Depois de atualizar suas extensões (pacotes) no Xcode, feche e exclua sua sessão atual e repita todas as etapas de [Conectar-se a uma sessão](#connecting-to-a-session) e [Verificar extensões](#verify-extensions) para garantir que o Assurance relate corretamente as extensões corretas em uma nova sessão do Assurance.





>[!SUCCESS]
>
>Agora você configurou seu aplicativo para usar o Assurance para o restante do tutorial.
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)


Próximo: **[Implementar consentimento](consent.md)**
