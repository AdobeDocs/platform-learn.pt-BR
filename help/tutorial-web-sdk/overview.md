---
title: Implementar a Adobe Experience Cloud com o tutorial do SDK da web
description: Saiba como implementar os aplicativos da Experience Cloud usando o SDK da Web da Adobe Experience Platform.
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: 6488faee86a53585bdbf03e069c4d6cf7e81d096
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 26%

---

# Implementar a Adobe Experience Cloud com o tutorial do SDK da web

Saiba como implementar os aplicativos da Experience Cloud usando o SDK da Web da Adobe Experience Platform.

O Experience Platform Web SDK é uma biblioteca JavaScript do lado do cliente que permite que clientes do Adobe Experience Cloud interajam com aplicativos Adobe e serviços de terceiros por meio da Rede de borda Adobe Experience Platform. Consulte [Visão geral do SDK da Web da Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=pt-BR) para obter informações mais detalhadas.

Este tutorial o orienta pela implementação do SDK da Web da plataforma em um site de varejo de amostra chamado Luma. O site [](https://luma.enablementadobe.com/content/luma/us/en.html)Luma tem uma camada de dados avançada e uma funcionalidade que permite a construção de uma implementação realista. Após concluir este tutorial, você deve estar pronto para começar a implementar todas as suas soluções de marketing por meio do SDK da Web da plataforma em seu próprio site.

[![Site Luma](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html).


## Objetivos de aprendizagem

Após concluir o tutorial, você poderá:

* Configurar datastreams

* Criar esquemas XDM

* Adicione os seguintes aplicativos do Adobe Experience Cloud:
   * **[Adobe Experience Platform](setup-experience-platform.md)** (e aplicativos criados na plataforma, como Adobe Real-time Customer Data Platform, Adobe Journey Optimizer e Adobe Customer Journey Analytics)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**

* Criar regras de tag e elementos de dados do objeto XDM para enviar dados para aplicativos Adobe

* Validar a implementação usando o Adobe Experience Platform Debugger

* Capturar consentimento do usuário

* Encaminhar dados para terceiros com o encaminhamento de eventos

>[!NOTE]
>
>Um tutorial de várias soluções semelhante está disponível para [SDK móvel](../tutorial-mobile-sdk/overview.md).

## Pré-requisitos

Todos os clientes do Experience Cloud podem usar o SDK da Web da plataforma. Não é um requisito licenciar um aplicativo baseado em plataforma como o Real-time Customer Data Platform ou o Journey Optimizer para usar o SDK da Web.

Nessas lições, presume-se que você tenha uma conta Adobe e a variável [permissões necessárias](configure-permissions.md) para concluir as lições. Caso contrário, entre em contato com o administrador do Experience Cloud para solicitar acesso.

Além disso, pressupõe-se que você esteja familiarizado com linguagens de desenvolvimento front-end como HTML e JavaScript. Você não precisa ser um especialista nesses idiomas, mas aproveite ao máximo este tutorial para ler e entender o código.

Vamos começar!

[Próximo: ](configure-permissions.md)

>[!NOTE]
>
>Obrigado por investir seu tempo para aprender sobre o SDK da Web da Adobe Experience Platform. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
