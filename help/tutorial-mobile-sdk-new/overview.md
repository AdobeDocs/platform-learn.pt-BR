---
title: Visão geral do tutorial Implementar o Adobe Experience Cloud em aplicativos para dispositivos móveis
description: Saiba como implementar os aplicativos móveis do Adobe Experience Cloud. Este tutorial o orienta por uma implementação de aplicativos Experience Cloud em um aplicativo Swift de amostra.
recommendations: noDisplay,catalog
hide: true
exl-id: 378bdf5d-c3ce-4a4c-b188-ab9e8265627f
source-git-commit: 8810829ec80b38afafbd4384005f5e145c5b5999
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 6%

---

# Tutorial Implementar a Adobe Experience Cloud em aplicativos para dispositivos móveis

Saiba como implementar aplicativos da Adobe Experience Cloud em seu aplicativo para dispositivos móveis usando o SDK móvel da Adobe Experience Platform.

O SDK móvel do Experience Platform é um SDK do lado do cliente que permite que os clientes da Adobe Experience Cloud interajam com aplicativos Adobe e serviços de terceiros por meio da rede de borda da Adobe Experience Platform. Consulte a [Documentação do SDK do Adobe Experience Platform Mobile](https://developer.adobe.com/client-sdks/home/) para obter informações mais detalhadas.

![Arquitetura](assets/architecture.png)


Este tutorial o orienta pela implementação do SDK móvel da Platform em um aplicativo de varejo de amostra chamado Luma. A variável [aplicativo Luma](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) O tem uma funcionalidade que permite a criação de uma implementação realista. Após concluir este tutorial, você deve estar pronto para começar a implementar todas as suas soluções de marketing por meio do SDK do Experience Platform Mobile em seus próprios aplicativos móveis.

As lições são projetadas para o iOS e escritas em Swift/SwiftUI, mas muitos dos conceitos também se aplicam ao Android™.

Após concluir este tutorial, você será capaz de:

* Crie um esquema usando grupos de campos padrão e personalizados.
* Configurar um fluxo de dados.
* Configure uma propriedade de tag móvel.
* Configurar um conjunto de dados de Experience Platform (opcional).
* Instale e implemente extensões de tag em um aplicativo.
* Passe corretamente os parâmetros de Experience Cloud para um [webview](web-views.md).
* Validar a implementação usando o [Adobe Experience Platform Assurance](assurance.md).
* Adicione os seguintes aplicativos/extensões do Adobe Experience Cloud:
   * [Adobe Experience Platform Edge (XDM)](events.md)
   * [Coleta de dados do ciclo de vida](lifecycle-data.md)
   * [Consentimento](consent.md)
   * [Identidade](identity.md)
   * [Perfil](profile.md)
   * [Places](places.md)
   * [Analytics](analytics.md)
   * [Experience Platform](platform.md)
   * [Mensagens por push com o Journey Optimizer](journey-optimizer-push.md)
   * [Mensagens no aplicativo com o Journey Optimizer](journey-optimizer-inapp.md)
   * [Gerenciamento de decisão com o Journey Optimizer](journey-optimizer-offers.md)
   * [Target](target.md)


>[!NOTE]
>
>Um tutorial de várias soluções semelhante está disponível para [SDK da Web](../tutorial-web-sdk/overview.md).

## Pré-requisitos

Nessas lições, presume-se que você tenha uma ID de Adobe e as permissões de nível de usuário necessárias para concluir os exercícios. Caso contrário, entre em contato com o administrador do Adobe para solicitar acesso.

* Em Coleção de dados, você deve ter:
   * **[!UICONTROL Plataformas]**— permission item **[!UICONTROL Dispositivo móvel]**
   * **[!UICONTROL Direitos de propriedade]**— permission itens para **[!UICONTROL Desenvolver]**, **[!UICONTROL Aprovar]**, **[!UICONTROL Publish]**, **[!UICONTROL Gerenciar extensões]**, e **[!UICONTROL Gerenciar ambientes]**.
   * **[!UICONTROL Direitos da empresa]**— permission itens para **[!UICONTROL Gerenciar propriedades]** e, se concluir a lição opcional de mensagens por push, **[!UICONTROL Gerenciar configurações do aplicativo]**

     Para obter mais informações sobre permissões de tags, consulte [Permissões de usuário para tags](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=pt-BR){target="_blank"} na documentação do produto.
* No Experience Platform, você deve ter:
   * **[!UICONTROL Modelagem de dados]**—itens de permissão para gerenciar e visualizar esquemas.
   * **[!UICONTROL Identity Management]**—itens de permissão para gerenciar e exibir namespaces de identidade.
   * **[!UICONTROL Coleta de dados]**—itens de permissão para gerenciar e exibir fluxos de dados.

   * Se você for o cliente de um aplicativo baseado em plataforma como o Real-Time CDP, Journey Optimizer ou Customer Journey Analytics e fizer as lições relacionadas que também deve ter:
      * **[!UICONTROL Gerenciamento de dados]**— itens de permissão para gerenciar e exibir conjuntos de dados.
      * Um desenvolvimento **sandbox** que você pode usar neste tutorial.

   * Para as lições do Journey Optimizer, você precisa de permissões para configurar o **serviço de notificação por push** e para criar um **superfície do aplicativo**, um **jornada**, um **mensagem**, e **predefinições de mensagem**. Para a Gestão de decisões, você precisa das permissões adequadas para **gerenciar ofertas** e **decisões** conforme descrito [aqui](https://experienceleague.adobe.com/docs/journey-optimizer/using/access-control/privacy/high-low-permissions.html?lang=en#decisions-permissions).

* Para o Adobe Analytics, você deve saber quais **conjuntos de relatórios** você pode usar o para concluir este tutorial.

* Para o Adobe Target, você deve ter permissão para criar e ativar atividades.


>[!NOTE]
>
>Como parte deste tutorial, você cria esquemas, conjuntos de dados, identidades e assim por diante. Se várias pessoas estiverem assistindo a este tutorial em uma única sandbox, considere anexar ou anexar uma identificação como parte de suas convenções de nomenclatura ao criar esses objetos. Por exemplo, adicione ` - <your name or initials>` ao nome do objeto que você foi instruído a criar.

>[!NOTE]
>
>Use o iOS como plataforma, [!DNL Swift] como a linguagem de programação, [!DNL SwiftUI] como a estrutura da interface e [!DNL Xcode] como o ambiente de desenvolvimento integrado (IDE). No entanto, muitos dos conceitos de implementação explicados são semelhantes para outras plataformas de desenvolvimento. Muitos já concluíram com sucesso este tutorial com pouca ou nenhuma experiência anterior de iOS/Swift(UI). Não é necessário ser um especialista para concluir as lições, mas você aprenderá mais com elas se ler e entender o código confortavelmente.


## Baixe o aplicativo Luma

Duas versões do aplicativo de amostra estão disponíveis para download. Ambas as versões podem ser baixadas/clonadas de [Github](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App). Você encontrará duas pastas:


1. [Início](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: um projeto sem código ou com código de espaço reservado para a maioria do código do SDK do Experience Platform Mobile que você precisa usar para concluir os exercícios práticos neste tutorial.
1. [Concluir](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: uma versão com a implementação completa para referência.

Se você quiser apenas experimentar o aplicativo final, também poderá baixá-lo diretamente da Apple App Store.

[<img src="assets/download-app.svg">](https://apps.apple.com/us/app/luma-app/id6466588487)

Vamos começar!

>[!SUCCESS]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Próximo: **[Criar um esquema XDM](create-schema.md)**
