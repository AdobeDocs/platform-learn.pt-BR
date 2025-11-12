---
title: Tutorial Implementar o Adobe Experience Cloud em aplicativos para dispositivos móveis
description: Saiba como implementar os aplicativos móveis do Adobe Experience Cloud. Este tutorial o orienta por uma implementação de aplicativos Experience Cloud em um aplicativo Swift ou Android de amostra.
recommendations: noDisplay,catalog
last-substantial-update: 2023-11-29T00:00:00Z
exl-id: daff4214-d515-4fad-a224-f7589b685b55
source-git-commit: 342bb7efbe868622c4bc08e02568bce948fed61c
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 1%

---

# Tutorial Implementar o Adobe Experience Cloud em aplicativos para dispositivos móveis

Saiba como implementar aplicativos do Adobe Experience Cloud em seu aplicativo móvel usando o Adobe Experience Platform Mobile SDK.

O Experience Platform Mobile SDK é um SDK do lado do cliente que permite aos clientes da Adobe Experience Cloud interagir com aplicativos da Adobe e serviços de terceiros por meio do Adobe Experience Platform Edge Network. Consulte a [documentação do Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/) para obter informações mais detalhadas.

![Arquitetura](assets/architecture.png){zoomable="yes"}


Este tutorial o orienta pela implementação do Platform Mobile SDK em um aplicativo de amostra chamado Luma. O aplicativo Luma tem funcionalidade que permite a criação de uma implementação realista. Após concluir este tutorial, você deve estar pronto para começar a implementar todas as suas soluções de marketing por meio do Experience Platform Mobile SDK em seus próprios aplicativos móveis.

As lições foram projetadas para:

* iOS, usando a linguagem de programação Swift e a estrutura SwiftUI.
* Android, usando a linguagem de programação Kotlin e Java e a estrutura JetPack Compose.

Após concluir este tutorial, você será capaz de:

* Crie um esquema usando grupos de campos padrão e personalizados.
* Configurar um fluxo de dados.
* Configure uma propriedade de tag móvel.
* Configurar um conjunto de dados do Experience Platform (opcional).
* Instale e implemente extensões de tag em um aplicativo.
* Passe corretamente os parâmetros Experience Cloud para uma [exibição da Web](web-views.md).
* Valide a implementação usando o [Adobe Experience Platform Assurance](assurance.md).
* Adicione os seguintes aplicativos ou extensões do Adobe Experience Cloud:
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

     Para obter mais informações sobre permissões de marcas, consulte [Permissões de usuário para marcas](https://experienceleague.adobe.com/en/docs/experience-platform/tags/admin/user-permissions){target="_blank"} na documentação do produto.
* No Experience Platform, você deve ter:
   * **[!UICONTROL Modelagem de Dados]** — itens de permissão para gerenciar e exibir esquemas.
   * **[!UICONTROL Identity Management]** — itens de permissão para gerenciar e exibir namespaces de identidade.
   * **[!UICONTROL Coleção de dados]** — itens de permissão para gerenciar e exibir sequências de dados.

   * Se você for o cliente de um aplicativo baseado em plataforma como o Real-Time CDP, Journey Optimizer ou Customer Journey Analytics e planejar fazer as lições relacionadas, também deverá ter:
      * **[!UICONTROL Gerenciamento de dados]**—itens de permissão para gerenciar e exibir conjuntos de dados.
      * Uma **sandbox** de desenvolvimento que você pode usar para este tutorial.

   * Para as lições do Journey Optimizer, você precisa de permissões para configurar o **serviço de notificação por push** e criar uma **superfície de aplicativo**, uma **jornada**, uma **mensagem** e **predefinições de mensagem**. Além disso, para o Gerenciamento de decisões, você precisa das permissões adequadas para **gerenciar ofertas** e **decisões**, conforme descrito em [Níveis de permissão](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/access-control/high-low-permissions).

* Para o Adobe Analytics, você deve saber quais **conjuntos de relatórios** você pode usar para concluir este tutorial.

* Para o Adobe Target, você deve ter permissão para criar e ativar atividades.


>[!NOTE]
>
>Como parte deste tutorial, você cria esquemas, conjuntos de dados, identidades e assim por diante. Se várias pessoas estiverem assistindo a este tutorial em uma única sandbox, considere anexar ou anexar uma identificação como parte de suas convenções de nomenclatura ao criar esses objetos. Por exemplo, adicione ` - <your name or initials>` ao nome do objeto que você está instruído a criar.

## Histórico de versão

* 9 de setembro de 2025:
   * Versão Android do aplicativo com instruções.
   * Atualizações de alterações na superfície do aplicativo e na funcionalidade da campanha no Journey Optimizer.
* 29 de novembro de 2023: grande revisão com novos aplicativos de amostra e novas lições para mensagens no aplicativo, gestão de decisões e Adobe Target.
* 9 de março de 2022: Primeira publicação

## Baixe o aplicativo Luma

>[!BEGINTABS]

>[!TAB iOS]

Duas versões do aplicativo de amostra estão disponíveis para download. Ambas as versões podem ser baixadas/clonadas de [GitHub](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App). Há duas pastas:

1. [Início](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: um projeto sem código ou com código de espaço reservado para a maioria do código do Experience Platform Mobile SDK que você precisa usar para concluir os exercícios práticos neste tutorial.
1. [Término](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: uma versão com a implementação completa para referência.

Você usa o iOS como a plataforma, [!DNL Swift] como a linguagem de programação, [!DNL SwiftUI] como a estrutura da interface do usuário e [!DNL Xcode] como o ambiente de desenvolvimento integrado (IDE). No entanto, muitos dos conceitos de implementação explicados são semelhantes para outras plataformas de desenvolvimento. Muitos já concluíram com sucesso este tutorial com pouca ou nenhuma experiência de desenvolvimento anterior do iOS e Swift(UI). Não é necessário ser um especialista para concluir as lições, mas você aprenderá mais com elas se ler e entender o código confortavelmente.

Você pode baixar a versão final produzida do aplicativo na App Store.

[![Baixar](assets/download-app.svg)](https://apps.apple.com/us/app/luma-app/id6466588487)

>[!TAB Android]

Duas versões do aplicativo de amostra estão disponíveis para download. Ambas as versões podem ser baixadas ou clonadas de [GitHub](https://github.com/adobe/Luma-Android). Há duas pastas:

1. [Início](https://github.com/adobe/Luma-Android){target="_blank"}: um projeto sem código ou com código de espaço reservado para a maioria do código do Experience Platform Mobile SDK que você precisa usar para concluir os exercícios práticos neste tutorial.
1. [Término](https://github.com/adobe/Luma-Android){target="_blank"}: uma versão com a implementação completa para referência.

Você usa o Android como plataforma, [!DNL Kotlin]+[!DNL Java] como linguagem de programação, [!DNL JetPack Compose] como estrutura de interface do usuário e [!DNL Android Studio] como ambiente de desenvolvimento integrado (IDE). No entanto, muitos dos conceitos de implementação explicados são semelhantes para outras plataformas de desenvolvimento. Muitos já concluíram com sucesso este tutorial com pouca ou nenhuma experiência anterior do Android / Kotlin+Java / JetPack Compose. Não é necessário ser um especialista para concluir as lições, mas você aprenderá mais com elas se ler e entender o código confortavelmente.

Se preferir, você pode [participar de um teste para uma versão &#x200B;](https://play.google.com/apps/internaltest/4700642199234438150) do aplicativo da Google Play.


>[!ENDTABS]

Vamos começar!

>[!SUCCESS]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-os nesta [postagem de discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Próximo: **[Criar um esquema XDM](create-schema.md)**
