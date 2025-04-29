---
title: Visão geral do tutorial Implementar o Adobe Experience Cloud em aplicativos para dispositivos móveis
description: Saiba como implementar os aplicativos móveis do Adobe Experience Cloud. Este tutorial o orienta por uma implementação dos aplicativos Experience Cloud em um aplicativo Swift de amostra.
recommendations: noDisplay,catalog
last-substantial-update: 2023-11-29T00:00:00Z
exl-id: daff4214-d515-4fad-a224-f7589b685b55
source-git-commit: c08671ae28955ff090baa7aa5a47246b2196ba20
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 4%

---

# Tutorial Implementar o Adobe Experience Cloud em aplicativos para dispositivos móveis

Saiba como implementar aplicativos da Adobe Experience Cloud em seu aplicativo para dispositivos móveis usando o SDK móvel da Adobe Experience Platform.

O Experience Platform Mobile SDK é um SDK do lado do cliente que permite aos clientes da Adobe Experience Cloud interagir com aplicativos da Adobe e serviços de terceiros por meio do Adobe Experience Platform Edge Network. Consulte a [documentação do Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/) para obter informações mais detalhadas.

![Arquitetura](assets/architecture.png)


Este tutorial o orienta pela implementação do Platform Mobile SDK em um aplicativo de varejo de amostra chamado Luma. O [aplicativo Luma](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) tem uma funcionalidade que permite a criação de uma implementação realista. Após concluir este tutorial, você deve estar pronto para começar a implementar todas as suas soluções de marketing pelo Experience Platform Mobile SDK em seus próprios aplicativos móveis.

As lições foram projetadas para o iOS e escritas em Swift/SwiftUI, mas muitos dos conceitos também se aplicam ao Android™.

Após concluir este tutorial, você será capaz de:

* Crie um esquema usando grupos de campos padrão e personalizados.
* Configurar um fluxo de dados.
* Configure uma propriedade de tag móvel.
* Configurar um conjunto de dados do Experience Platform (opcional).
* Instale e implemente extensões de tag em um aplicativo.
* Passe corretamente os parâmetros Experience Cloud para uma [exibição da Web](web-views.md).
* Valide a implementação usando o [Adobe Experience Platform Assurance](assurance.md).
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
>Um tutorial de várias soluções semelhante está disponível para o [Web SDK](../tutorial-web-sdk/overview.md).

## Permissões

Nessas lições, presume-se que você tenha uma Adobe ID e as permissões de nível de usuário necessárias para concluir os exercícios. Caso contrário, entre em contato com o administrador do Adobe para solicitar acesso.

* Em Coleção de dados, você deve ter:
   * **[!UICONTROL Plataformas]**—item de permissão **[!UICONTROL Celular]**
   * **[!UICONTROL Direitos de propriedade]**—itens de permissão para **[!UICONTROL Desenvolver]**, **[!UICONTROL Aprovar]**, **[!UICONTROL Publicar]**, **[!UICONTROL Gerenciar extensões]** e **[!UICONTROL Gerenciar ambientes]**.
   * **[!UICONTROL Direitos da Empresa]**—itens de permissão para **[!UICONTROL Gerenciar Propriedades]**

     Para obter mais informações sobre permissões de marcas, consulte [Permissões de usuário para marcas](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=pt-BR){target="_blank"} na documentação do produto.
* No Experience Platform, você deve ter:
   * **[!UICONTROL Modelagem de Dados]** — itens de permissão para gerenciar e exibir esquemas.
   * **[!UICONTROL Identity Management]** — itens de permissão para gerenciar e exibir namespaces de identidade.
   * **[!UICONTROL Coleção de dados]** — itens de permissão para gerenciar e exibir sequências de dados.

   * Se você for o cliente de um aplicativo baseado em plataforma como o Real-Time CDP, Journey Optimizer ou Customer Journey Analytics e fizer as lições relacionadas que também deve ter:
      * **[!UICONTROL Gerenciamento de dados]**—itens de permissão para gerenciar e exibir conjuntos de dados.
      * Uma **sandbox** de desenvolvimento que você pode usar para este tutorial.

   * Para as lições do Journey Optimizer, você precisa de permissões para configurar o **serviço de notificação por push** e criar uma **superfície de aplicativo**, uma **jornada**, uma **mensagem** e **predefinições de mensagem**. Para o Gerenciamento de decisões, você precisa das permissões adequadas para **gerenciar ofertas** e **decisões** conforme descrito [aqui](https://experienceleague.adobe.com/docs/journey-optimizer/using/access-control/privacy/high-low-permissions.html?lang=en#decisions-permissions).

* Para o Adobe Analytics, você deve saber quais **conjuntos de relatórios** você pode usar para concluir este tutorial.

* Para o Adobe Target, você deve ter permissão para criar e ativar atividades.


>[!NOTE]
>
>Como parte deste tutorial, você cria esquemas, conjuntos de dados, identidades e assim por diante. Se várias pessoas estiverem assistindo a este tutorial em uma única sandbox, considere anexar ou anexar uma identificação como parte de suas convenções de nomenclatura ao criar esses objetos. Por exemplo, adicione ` - <your name or initials>` ao nome do objeto que você está instruído a criar.

## Histórico de versão

* 29 de novembro de 2023: grande revisão com novos aplicativos de amostra e novas lições para mensagens no aplicativo, gestão de decisões e Adobe Target.
* 9 de março de 2022: Primeira publicação

## Baixe o aplicativo Luma

Duas versões do aplicativo de amostra estão disponíveis para download. Ambas as versões podem ser baixadas/clonadas do [Github](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App). Você encontrará duas pastas:


1. [Início](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: um projeto sem código ou com código de espaço reservado para a maioria do código do Experience Platform Mobile SDK que você precisa usar para concluir os exercícios práticos neste tutorial.
1. [Término](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: uma versão com a implementação completa para referência.

>[!NOTE]
>
>Você usa o iOS como a plataforma, [!DNL Swift] como a linguagem de programação, [!DNL SwiftUI] como a estrutura da interface do usuário e [!DNL Xcode] como o ambiente de desenvolvimento integrado (IDE). No entanto, muitos dos conceitos de implementação explicados são semelhantes para outras plataformas de desenvolvimento. Muitos já concluíram com sucesso este tutorial com pouca ou nenhuma experiência anterior de iOS/Swift(UI). Não é necessário ser um especialista para concluir as lições, mas você aprenderá mais com elas se ler e entender o código confortavelmente.


Você pode baixar a versão final produzida do aplicativo na App Store.

[![Baixar](assets/download-app.svg)](https://apps.apple.com/us/app/luma-app/id6466588487)


Vamos começar!

>[!SUCCESS]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-os nesta [postagem de discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Próximo: **[Criar um esquema XDM](create-schema.md)**
