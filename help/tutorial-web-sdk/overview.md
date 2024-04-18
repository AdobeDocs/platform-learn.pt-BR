---
title: Implementar a Adobe Experience Cloud com o tutorial do SDK da web
description: Saiba como implementar aplicativos Experience Cloud usando o Adobe Experience Platform Web SDK.
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: 15bc08bdbdcb19f5b086267a6d94615cbfe1bac7
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 11%

---

# Implementar a Adobe Experience Cloud com o tutorial do SDK da web

>[!CAUTION]
>
>Esperamos publicar grandes alterações neste tutorial na terça-feira, 23 de abril de 2024. Depois desse ponto, muitos exercícios serão alterados e talvez seja necessário reiniciar o tutorial desde o início para concluir todas as lições.


Saiba como implementar aplicativos Experience Cloud usando o Adobe Experience Platform Web SDK.

O SDK da Web do Experience Platform é uma biblioteca JavaScript do lado do cliente que permite aos clientes da Adobe Experience Cloud interagir com aplicativos Adobe e serviços de terceiros por meio do Edge Network Adobe Experience Platform. Consulte [Visão geral do SDK da Web da Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=pt-BR) para obter informações mais detalhadas.

Este tutorial o orienta pela implementação do SDK da Web da Platform em um site de vendas de exemplo chamado Luma. A variável [Site Luma](https://luma.enablementadobe.com/content/luma/us/en.html) O tem uma camada de dados avançada e uma funcionalidade que permite a criação de uma implementação realista. Após concluir este tutorial, você deve estar pronto para começar a implementar todas as suas soluções de marketing por meio do SDK da Web da Platform em seu próprio site.

[![Site Luma](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)


## Objetivos de aprendizagem

Após concluir o tutorial, você será capaz de:

* Configurar datastreams

* Criar esquemas XDM

* Adicione os seguintes aplicativos do Adobe Experience Cloud:
   * **[Adobe Experience Platform](setup-experience-platform.md)** (e aplicativos criados na Platform, como Adobe Real-time Customer Data Platform, Adobe Journey Optimizer e Adobe Customer Journey Analytics)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**

* Criar regras de tag e elementos de dados de objeto XDM para enviar dados para aplicativos do Adobe

* Validar a implementação usando o Adobe Experience Platform Debugger

* Capturar consentimento do usuário

* Encaminhar dados a terceiros com encaminhamento de eventos

>[!NOTE]
>
>Um tutorial de várias soluções semelhante está disponível para [SDK móvel](../tutorial-mobile-sdk/overview.md).

## Pré-requisitos

Todos os clientes do Experience Cloud podem usar o SDK da Web da plataforma. Não é um requisito licenciar um aplicativo baseado em plataforma, como o Real-time Customer Data Platform ou o Journey Optimizer, para usar o SDK da Web.

Nessas lições, presume-se que você tenha uma conta Adobe e a variável [permissões necessárias](configure-permissions.md) para completar as lições. Caso contrário, entre em contato com o administrador do Experience Cloud para solicitar acesso.

Além disso, pressupõe-se que você esteja familiarizado com linguagens de desenvolvimento front-end como HTML e JavaScript. Você não precisa ser um especialista nessas linguagens, mas aprenderá mais com este tutorial se puder ler e entender o código.

Vamos começar!

[Próximo: ](configure-permissions.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
