---
title: Configurar implementações do SDK móvel do Assurance for Platform
description: Saiba como implementar a extensão Assurance em um aplicativo móvel.
feature: Mobile SDK,Assurance
jira: KT-14628
exl-id: e15774b2-2f52-400f-9313-bb4338a88918
source-git-commit: 576f85eda6e5888b9eafa15a705a99c3a70fed07
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 5%

---

# Configurar o Assurance

Saiba como configurar o Adobe Experience Platform Assurance em um aplicativo móvel.

O Assurance, formalmente conhecido como Projeto Griffon, foi projetado para ajudá-lo a inspecionar, testar, simular e validar a maneira como você coleta dados ou veicula experiências em seu aplicativo móvel.

O Assurance ajuda a inspecionar eventos brutos de SDK gerados pelo SDK móvel da Adobe Experience Platform. Todos os eventos coletados pelo SDK estão disponíveis para inspeção. Os eventos do SDK são carregados em uma exibição de lista classificada por tempo. Cada evento tem uma exibição detalhada que fornece mais detalhes. Exibições adicionais para procurar a configuração do SDK, elementos de dados, Estados compartilhados e versões de extensão do SDK também são fornecidas. Saiba mais sobre a [Garantia](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html) na documentação do produto.


## Pré-requisitos

* Aplicativo com SDKs instalado e configurado com êxito.

## Objetivos de aprendizagem

Nesta lição, você vai:

* Confirme se sua organização tem acesso (e solicite-o caso não tenha).
* Configure seu URL base.
* Adicione o código específico necessário do iOS.
* Conectar-se a uma sessão.

## Confirmar acesso

Confirme se sua organização tem acesso ao Assurance. Você, como usuário, deve ser adicionado ao perfil do Adobe Experience Platform. Consulte [Acesso de usuário](https://experienceleague.adobe.com/docs/experience-platform/assurance/user-access.html?lang=en) no Guia de garantia para obter mais informações.

## Implementação

Além da [instalação do SDK](install-sdks.md) geral, que você concluiu na lição anterior, a iOS também exige a seguinte adição para iniciar a sessão do Assurance para o seu aplicativo.

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL SceneDelegate]** no navegador Project do Xcode.

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



## Definir identificador do conjunto

É necessário fornecer um identificador de pacote exclusivo para seu aplicativo.

1. Abra o projeto no Xcode.
1. Selecione **[!DNL Luma]** no Navegador de projetos.
1. Selecione o destino **[!DNL Luma]**.
1. Selecione a guia **Assinatura e Recursos**.
1. Defina um **[!UICONTROL Identificador de Pacote]**.

   >[!IMPORTANT]
   >
   >Use um identificador de conjunto _exclusivo_ e substitua o identificador de conjunto `com.adobe.luma.tutorial.swiftui`, pois cada identificador de conjunto precisa ser exclusivo. Normalmente, você usa um formato de DNS reverso para cadeias de caracteres de ID de pacote, como `com.organization.brand.uniqueidentifier`. A versão Concluída deste tutorial, por exemplo, usa `com.adobe.luma.tutorial.swiftui`.


   ![Recursos de assinatura do Xcode](assets/xcode-signing-capabilities.png){zoomable="yes"}


## Configurar um URL de base

1. Vá para o seu projeto no Xcode.
1. Selecione **[!DNL Luma]** no Navegador de projetos.
1. Selecione o destino **[!DNL Luma]**.
1. Selecione a guia **Informações**.
1. Para adicionar uma URL base, role para baixo até **Tipos de URL** e selecione o botão **+**.
1. Defina **Identificador** para o Identificador de Pacote de sua escolha e defina um **Esquemas de URL** de sua escolha.

   ![url de garantia](assets/assurance-url-type.png)

   >[!IMPORTANT]
   >
   >Use um identificador de conjunto _exclusivo_ e substitua o identificador de conjunto `com.adobe.luma.tutorial.swiftui`, pois cada identificador de conjunto deve ser exclusivo. Normalmente, você usa um formato de DNS reverso para cadeias de caracteres de ID de pacote, como `com.organization.brand.uniqueidentifier`. Você pode usar o mesmo identificador de conjunto usado em [Definir identificador de conjunto](#define-bundle-identifier).<br/>Da mesma forma, use um esquema de URL exclusivo e substitua o `lumatutorialswiftui` já fornecido pelo seu esquema de URL exclusivo.

Para saber mais sobre os Esquemas de URL na iOS, consulte a [documentação da Apple](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target="_blank"}.

O Assurance funciona abrindo um URL, seja via navegador ou código QR. Esse URL começa com o URL de base que abre o aplicativo e contém parâmetros adicionais. Esses parâmetros exclusivos são usados para conectar a sessão.


## Conectar-se a uma sessão

No Xcode:

1. Compile ou recompile e execute o aplicativo no simulador ou em um dispositivo físico do Xcode, usando ![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

   >[!TIP]
   >
   >Como opção, você pode querer &quot;limpar&quot; sua build, especialmente quando vir resultados inesperados. Para fazer isso, selecione **[!UICONTROL Limpar pasta de compilação...]** no menu Xcode **[!UICONTROL Produto]**.


1. Na caixa de diálogo **[!UICONTROL Permitir que o &quot;Aplicativo Luma&quot; use sua localização]**, selecione **[!UICONTROL Permitir ao Usar o Aplicativo]**.

   <img src="assets/geolocation-permissions.png" width="300">

1. Na caixa de diálogo **[!UICONTROL &quot;Aplicativo Luma&quot; Deseja Enviar Notificações]**, selecione **[!UICONTROL Permitir]**.

   <img src="assets/notification-permissions.png" width="300">

1. Selecione **[!UICONTROL Continuar...]** para permitir que o aplicativo acompanhe sua atividade.

   <img src="assets/tracking-continue.png" width="300">

1. Na caixa de diálogo **[!UICONTROL Permitir que o &quot;Aplicativo Luma&quot; acompanhe sua atividade nos aplicativos e sites de outras empresas]**, selecione **[!UICONTROL Permitir]**.

   <img src="assets/tracking-allow.png" width="300">


No navegador:

1. Vá para a interface da Coleção de dados.
1. Selecione **[!UICONTROL Garantia]** no painel esquerdo.
1. Selecione **[!UICONTROL Criar Sessão]**.
1. Selecione **[!UICONTROL Iniciar]**.
1. Forneça um **[!UICONTROL Nome da Sessão]**, como `Luma Mobile App Session` e a **[!UICONTROL URL Base]**, que são os Esquemas de URL inseridos no Xcode, seguido de `://` Por exemplo: `lumatutorialswiftui://`
1. Selecione **[!UICONTROL Próximo]**.
   ![criar sessão de garantia](assets/assurance-create-session.png)
1. Na caixa de diálogo modal **[!UICONTROL Criar nova sessão]**:

   Se você estiver usando um dispositivo físico:

   * Selecione **[!UICONTROL Digitalizar código QR]**. Para abrir o aplicativo, use a câmera do dispositivo físico para digitalizar o código QR e toque no link.

     ![código de garantia de qualidade](assets/assurance-qr-code.png)

   Se estiver usando um simulador:

   1. Selecione **[!UICONTROL Copiar Link]**.
   1. Copie o deep link usando ![Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) e use o deep link para abrir o aplicativo com o Safari no simulador.
      ![Link da cópia de garantia](assets/assurance-copy-link.png)

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

Se você tiver desafios, confira a [documentação técnica](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/){target="_blank"} e a [documentação geral](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html){target="_blank"}.


## Verificar extensões

Para verificar se seu aplicativo está usando as extensões mais atualizadas:

1. Selecione **[!UICONTROL Configurar]**.

1. Selecione ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) para ![123](https://spectrum.adobe.com/static/icons/workflow_18/Smock_123_18_N.svg) **[!UICONTROL Versões de Extensão]**.

1. Selecione **[!UICONTROL Salvar]**.

   ![Configurar versões de extensão](assets/assurance-configure-extension-versions.png)

1. Selecione ![123](https://spectrum.adobe.com/static/icons/workflow_18/Smock_123_18_N.svg) **[!UICONTROL Versões de Extensão]** para ter uma visão geral das extensões mais recentes disponíveis e das extensões usadas na sua versão do aplicativo.

   ![Versões de extensão](assets/assurance-extension-versions.png)

1. Para atualizar suas versões de extensão (por exemplo, **[!UICONTROL Mensagens]** e **[!UICONTROL Otimizar]**), selecione o pacote (extensão) de **[!UICONTROL Dependências de Pacote]** (por exemplo, **[!UICONTROL AEPMessaging]**) e, no menu de contexto, selecione **[!UICONTROL Atualizar Pacote]**. O Xcode atualizará as dependências do pacote.


>[!NOTE]
>
>Depois de atualizar suas extensões (pacotes) no Xcode, feche e exclua sua sessão atual e repita todas as etapas de [Conectando-se a uma sessão](#connecting-to-a-session) e [Verificar extensões](#verify-extensions) para garantir que o Assurance relate corretamente as extensões corretas em uma nova sessão do Assurance.





>[!SUCCESS]
>
>Agora você configurou seu aplicativo para usar o Assurance para o restante do tutorial.
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-os nesta [postagem de Discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)


Próximo: **[Implementar Consentimento](consent.md)**
