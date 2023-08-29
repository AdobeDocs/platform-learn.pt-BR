---
title: Visão geral do tutorial Implementar o Adobe Experience Cloud em aplicativos para dispositivos móveis
description: Saiba como implementar os aplicativos móveis do Adobe Experience Cloud. Este tutorial o orienta por uma implementação de aplicativos Experience Cloud em um aplicativo Swift de amostra.
recommendations: noDisplay,catalog
hide: true
source-git-commit: e364d70375f687b9c50691efd04a1db757fee364
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 11%

---

# Tutorial Implementar a Adobe Experience Cloud em aplicativos para dispositivos móveis

Saiba como implementar aplicativos da Adobe Experience Cloud em seu aplicativo para dispositivos móveis usando o SDK móvel da Adobe Experience Platform.

O SDK móvel do Experience Platform é um SDK do lado do cliente que permite que os clientes da Adobe Experience Cloud interajam com aplicativos Adobe e serviços de terceiros por meio da rede de borda da Adobe Experience Platform. Consulte a [Documentação do SDK do Adobe Experience Platform Mobile](https://developer.adobe.com/client-sdks/documentation/) para obter informações mais detalhadas.

![configurações de build](assets/data-collection-mobile-sdk.png)


Este tutorial o orienta pela implementação do SDK móvel da Platform em um aplicativo de varejo de amostra chamado Luma. A variável [aplicativo Luma](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) O tem uma funcionalidade que permite a criação de uma implementação realista. Após concluir este tutorial, você deve estar pronto para começar a implementar todas as suas soluções de marketing por meio do SDK do Experience Platform Mobile em seus próprios aplicativos móveis.

As lições são projetadas para o iOS e escritas em Swift/SwiftUI, mas muitos dos conceitos também se aplicam ao Android™.

Após concluir este tutorial, você será capaz de:

* Crie um esquema usando grupos de campos padrão e personalizados.
* Configurar um fluxo de dados.
* Configure uma propriedade de tag móvel.
* Configurar um conjunto de dados de Experience Platform (opcional).
* Instale e implemente extensões de tag em um aplicativo.
* Adicione os seguintes aplicativos/extensões do Adobe Experience Cloud:
   * [Adobe Experience Platform Edge (XDM)](events.md)
   * [Coleta de dados do ciclo de vida](lifecycle-data.md)
   * [Adobe Analytics via XDM](analytics.md)
   * [Consentimento](consent.md)
   * [Identidade](identity.md)
   * [Perfil](profile.md)
   * [Adobe Experience Platform](platform.md)
   * [Mensagens por push com o Journey Optimizer](journey-optimizer-push.md)
* Passe corretamente os parâmetros de Experience Cloud para um [webview](web-views.md).
* Validar a implementação usando o [Adobe Experience Platform Assurance](assurance.md).

>[!NOTE]
>
>Um tutorial de várias soluções semelhante está disponível para [SDK da Web](../tutorial-web-sdk/overview.md).

## Pré-requisitos

Nessas lições, presume-se que você tenha uma Adobe ID e as permissões necessárias para concluir os exercícios. Caso contrário, entre em contato com o administrador do Adobe para solicitar acesso.

* Em Coleção de dados, você deve ter:
   * **[!UICONTROL Plataformas]**— permission item **[!UICONTROL Dispositivo móvel]**
   * **[!UICONTROL Direitos de propriedade]**— permission itens para **[!UICONTROL Desenvolver]**, **[!UICONTROL Aprovar]**, **[!UICONTROL Publish]**, **[!UICONTROL Gerenciar extensões]**, e **[!UICONTROL Gerenciar ambientes]**.
   * **[!UICONTROL Direitos da empresa]**— permission itens para **[!UICONTROL Gerenciar propriedades]** e, se concluir a lição opcional de mensagens por push, **[!UICONTROL Gerenciar configurações do aplicativo]**

     Para obter mais informações sobre permissões de tags, consulte [Permissões de usuário para tags](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=pt-BR){target="_blank"} na documentação do produto.
* No Experience Platform, você deve ter:
   * **[!UICONTROL Modelagem de dados]**—itens de permissão para gerenciar e visualizar esquemas.
   * **[!UICONTROL Identity Management]**—itens de permissão para gerenciar e exibir namespaces de identidade.
   * **[!UICONTROL Coleta de dados]**—itens de permissão para gerenciar e exibir fluxos de dados.

   * Se você for o cliente de um aplicativo baseado em plataforma como Real-Time CDP, Journey Optimizer ou Customer Journey Analytics, também deverá ter:
      * **[!UICONTROL Gerenciamento de dados]**— itens de permissão para gerenciar e visualizar conjuntos de dados para concluir a _Exercícios opcionais da Platform_ (requer uma licença para um aplicativo baseado em plataforma ).
      * Um desenvolvimento **sandbox** que você pode usar neste tutorial.
* Para o Adobe Analytics, você deve saber quais **conjuntos de relatórios** você pode usar o para concluir este tutorial.

Todos os clientes do Experience Cloud devem ter acesso aos recursos necessários para implantar o SDK móvel.

Além disso, presume-se que você esteja familiarizado com [!DNL Swift]. Não é necessário ser um especialista para concluir as lições, mas você aprenderá mais com elas se ler e entender o código confortavelmente.

## Baixe o aplicativo Luma

Duas versões do aplicativo de amostra estão disponíveis para download.

1. [Empty](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: uma versão sem nenhum código Experience Cloud para concluir os exercícios práticos neste tutorial
1. [Completa Implementada](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: uma versão com implementação Experience Cloud completa para referência.

Vamos começar!

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Próximo: **[Criar um esquema XDM](create-schema.md)**.
