---
title: Implementar a Adobe Experience Cloud com o tutorial do SDK da web
description: Saiba como implementar aplicativos Experience Cloud usando o Adobe Experience Platform Web SDK.
recommendations: catalog, noDisplay
source-git-commit: 12e6e9d06ae0d6945c165032d89fd0f801d94ff2
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 4%

---

# Implementar a Adobe Experience Cloud com o tutorial do SDK da web

Saiba como implementar aplicativos Experience Cloud usando o Adobe Experience Platform Web SDK.

O SDK da Web do Experience Platform é uma biblioteca JavaScript do lado do cliente que permite aos clientes da Adobe Experience Cloud interagir com aplicativos Adobe e serviços de terceiros por meio da rede de borda da Adobe Experience Platform. Consulte [Visão geral do SDK da Web da Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=pt-BR) para obter informações mais detalhadas.

![Arquitetura do SDK da Web do Experience Platform](assets/dc-websdk.png)

Este tutorial o orienta pela implementação do SDK da Web da Platform em um site de vendas de exemplo chamado Luma. A variável [Site Luma](https://luma.enablementadobe.com/content/luma/us/en.html) O tem uma camada de dados avançada e uma funcionalidade que permite a criação de uma implementação realista. Neste tutorial, você:

* Crie sua própria propriedade de tags em sua própria conta com uma implementação do SDK da Web da Platform para o site da Luma.
* Configure todos os recursos de coleção de dados para implementações do SDK da Web, como sequências de dados, esquemas e namespaces de identidade.
* Adicione os seguintes aplicativos do Adobe Experience Cloud:
   * **[Adobe Experience Platform](setup-experience-platform.md)** (e aplicativos criados na Platform, como Adobe Real-time Customer Data Platform, Adobe Journey Optimizer e Adobe Customer Journey Analytics)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**
* Implemente o encaminhamento de eventos para enviar os dados coletados pelo SDK da Web para destinos que não sejam Adobe.
* Valide sua própria implementação do SDK da Web da Platform usando o Experience Platform Debugger e o Assurance.

Após concluir este tutorial, você deve estar pronto para começar a implementar todos os seus aplicativos de marketing por meio do SDK da Web da Platform em seu próprio site!


>[!NOTE]
>
>Um tutorial de várias soluções semelhante está disponível para [SDK móvel](../tutorial-mobile-sdk/overview.md).

## Pré-requisitos

Todos os clientes do Experience Cloud podem usar o SDK da Web da plataforma. Não é um requisito licenciar um aplicativo baseado em plataforma, como o Real-time Customer Data Platform ou o Journey Optimizer, para usar o SDK da Web.

Nessas lições, presume-se que você tenha uma conta Adobe e as permissões necessárias para concluir as lições. Caso contrário, entre em contato com o administrador do Experience Cloud para solicitar acesso.

* Para **Coleta de dados**, você deve ter:
   * **[!UICONTROL Plataformas]**— permission para **[!UICONTROL Web]** e, se licenciado, **[!UICONTROL Edge]**
   * **[!UICONTROL Direitos de propriedade]**— permission para **[!UICONTROL Aprovar]**, **[!UICONTROL Desenvolver]**, **[!UICONTROL Editar propriedade]**, **[!UICONTROL Gerenciar ambientes]**, **[!UICONTROL Gerenciar extensões]**, e **[!UICONTROL Publish]**,
   * **[!UICONTROL Direitos da empresa]**— permission para **[!UICONTROL Gerenciar propriedades]**

     Para obter mais informações sobre permissões de tags, consulte [a documentação](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html).

* Para **Experience Platform**, você deve ter:

   * O acesso à **produção padrão**, **&quot;Prod&quot;** sandbox.
   * Acesso a **[!UICONTROL Gerenciar esquemas]** e **[!UICONTROL Exibir esquemas]** em **[!UICONTROL Modelagem de dados]**.
   * Acesso a **[!UICONTROL Gerenciar namespaces de identidade]** e **[!UICONTROL Exibir namespaces de identidade]** em **[!UICONTROL Identity Management]**.
   * Acesso a **[!UICONTROL Gerenciar fluxos de dados]** e **[!UICONTROL Exibir fluxos de dados]** em **[!UICONTROL Coleta de dados]**.
   * Se você for um cliente de um aplicativo baseado em plataforma e estiver concluindo o [Configurar Experience Platform](setup-experience-platform.md) você também deve ter:
      * Acesso a um **desenvolvimento** sandbox.
      * Todos os itens de permissão em **[!UICONTROL Gerenciamento de dados]**, e **[!UICONTROL Gerenciamento de perfis]**:

     Os recursos necessários devem estar disponíveis para todos os clientes do Experience Cloud, mesmo se você não for um cliente de um aplicativo baseado na plataforma, como o Real-Time CDP.

     Para obter mais informações sobre o controle de acesso da Platform, consulte [a documentação](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=pt-BR).

* Para o **Adobe Analytics** lição, você deve ter [Acesso de administrador às Configurações do conjunto de relatórios, Regras de processamento e Analysis Workspace](https://experienceleague.adobe.com/docs/analytics/admin/admin-console/home.html?lang=pt-BR)

* Para o **Adobe Target** lição, você deve ter [Editor ou Aprovador](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) acesso.

* Para o **Audience Manager** você deve ter acesso a criar, ler e gravar características, segmentos e destinos. Para obter mais informações, consulte o tutorial em [Controle De Acesso Baseado Em Função Do Audience Manager](https://experienceleague.adobe.com/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control.html?lang=en).


>[!NOTE]
>
>Presume-se que você esteja familiarizado com linguagens de desenvolvimento front-end como HTML e JavaScript. Você não precisa ser um especialista nessas linguagens, mas aprenderá mais com este tutorial se puder ler e entender o código.

## Carregar o site Luma

Carregue o [Site Luma](https://luma.enablementadobe.com/content/luma/us/en.html) em uma guia separada do navegador e marque-a como favorito para que você possa carregá-la facilmente sempre que necessário durante o tutorial. Você não precisa de acesso adicional ao Luma além de poder carregar nosso site de produção hospedado.

[![Site Luma](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)

Vamos começar!

[Próximo: ](configure-schemas.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar feedback geral ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
