---
title: Validar implementações do SDK da Web com o Experience Platform Debugger
description: Saiba como validar a implementação do SDK da Web da plataforma com o Adobe Experience Platform Debugger. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Debugger
exl-id: 150bb1b1-4523-4b44-bd4e-6cabc468fc04
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 5%

---

# Validar implementações do SDK da Web com o Experience Platform Debugger

Saiba como validar a implementação do SDK da Web da plataforma com o Adobe Experience Platform Debugger.

O Experience Platform Debugger é uma extensão disponível para navegadores Chrome e Firefox, que ajuda a visualizar a tecnologia Adobe implementada em suas páginas da Web. Baixe a versão do seu navegador preferido:

* [Extensão do Firefox](https://addons.mozilla.org/pt-BR/firefox/addon/adobe-experience-platform-dbg/)
* [Extensão do Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Se você nunca usou o depurador antes, e este é diferente do Adobe Experience Cloud Debugger mais antigo, talvez queira assistir a este vídeo de visão geral de cinco minutos:

>[!VIDEO](https://video.tv.adobe.com/v/32156?quality=12&learn=on)

Nesta lição, você usará o [Extensão do Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) para substituir a propriedade da tag codificada no [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html) com sua própria propriedade.

Essa técnica é chamada de alternância de ambiente e será útil posteriormente, ao trabalhar com tags em seu próprio site. Você pode carregar seu site em produção em seu navegador, mas com seu *desenvolvimento* ambiente de tags. Essa capacidade permite fazer e validar de forma segura as alterações nas tags, independentemente das suas versões de código normais. Afinal, essa separação das versões de tag de marketing de suas versões de código normais é um dos principais motivos pelos quais os clientes usam tags!

## Objetivos de aprendizagem

No final desta lição, você poderá usar o depurador para:

* Carregar uma biblioteca de tags alternativa
* Validar se o objeto XDM está capturando e enviando dados como esperado da Rede de Borda

## Pré-requisitos

Você está familiarizado com as tags de Coleta de dados e a variável [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target=&quot;_blank&quot;} e concluíram as seguintes lições anteriores no tutorial:

* [Configurar permissões](configure-permissions.md)
* [Configurar um esquema XDM](configure-schemas.md)
* [Configurar um namespace de identidade](configure-identities.md)
* [Configurar um conjunto de dados](configure-datastream.md)
* [Extensão do SDK da Web instalada na propriedade da tag](install-web-sdk.md)
* [Criar elementos de dados](create-data-elements.md)
* [Criar uma regra de tag](create-tag-rule.md)


## Carregar bibliotecas de tags alternativas com o Debugger

Este tutorial usa uma versão hospedada publicamente do [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Abra a página inicial e adicione um marcador a ela.

![Página inicial do Luma](assets/validate-luma-site.png)

O Experience Platform Debugger tem um recurso interessante que permite substituir uma biblioteca de tags existente por outra. Essa técnica é útil para validação e permite ignorar muitas etapas de implementação neste tutorial.

1. Certifique-se de ter o site Luma aberto e selecione o ícone de extensão do Experience Platform Debugger
1. O Debugger abrirá e mostrará alguns detalhes da implementação codificada, que não está relacionada a este tutorial (talvez seja necessário recarregar o site Luma após abrir o Debugger)
1. Confirme se o Debugger é &quot;**[!UICONTROL Conectado ao Luma]**&quot; como mostrado abaixo e selecione o &quot;**[!UICONTROL bloqueio]**&quot; para bloquear o Debugger para o site Luma.
1. Selecione o **[!UICONTROL Fazer logon]** e faça logon no Adobe Experience Cloud usando a ID do Adobe.
1. Agora vá para **[!UICONTROL Tags de Experience Platform]** na navegação à esquerda

   ![Tela da tag do Debugger](assets/validate-launch-screen.png)

1. Selecione o **[!UICONTROL Configuração]** guia
1. À direita de onde ele mostra o **[!UICONTROL Códigos de inserção da página]**, abra o **[!UICONTROL Ações]** e selecione **[!UICONTROL Substituir]**

   ![Selecione Ações > Substituir](assets/validate-switch-environment.png)

1. Como você é autenticado, o Debugger obterá as propriedades e os ambientes de tags disponíveis. Selecione seu `Web SDK Course` propriedade
1. Selecione seu `Development` ambiente
1. Selecione o **[!UICONTROL Aplicar]** botão

   ![Selecione a propriedade de tag alternativa](assets/validate-switch-selection.png)

1. O site Luma agora será recarregado _com sua propriedade de tag_.

   ![propriedade de tag substituída](assets/validate-switch-success.png)

À medida que você prossegue no tutorial, usará essa técnica de mapear o site Luma para sua própria propriedade de tag para validar a implementação do SDK da Web da plataforma. Ao começar a usar tags no site em produção, você pode usar essa mesma técnica para validar as alterações.

## Validar sua implementação no Experience Platform Debugger

Você pode usar o Debugger para validar a implementação do SDK da Web da plataforma e exibir os dados enviados para a Rede de borda da plataforma:

1. Ir para **[!UICONTROL Resumo]** no painel de navegação esquerdo, para ver os detalhes da propriedade da tag

   ![Guia Resumo](assets/validate-summary.png)

1. Agora vá para **[!UICONTROL Experience Platform Web SDK]** na navegação à esquerda para ver o **[!UICONTROL Solicitações de rede]**
1. Abra o **[!UICONTROL events]** (não se preocupe se essa captura de tela mostrar mais solicitações do que a sua, ela inclui solicitações de lições futuras e você pode ignorar por enquanto)

   ![Solicitação de SDK da Web da Adobe Experience Platform](assets/validate-aep-screen.png)

1. Observe como podemos ver a variável `web.webpagedetails.pageView` tipo de evento que especificamos em [!UICONTROL Enviar evento] e outras variáveis prontas para uso que seguem o `AEP Web SDK ExperienceEvent Mixin` format

   ![Detalhes do evento](assets/validate-event-pageViews.png)

1. Role para baixo até a `web` , selecione para abri-lo e inspecione o `webPageDetails.name`, `webPageDetails.server`e `webPageDetails.siteSection`. Eles devem corresponder às variáveis de camada de dados digitalData correspondentes na página inicial

   ![Guia Rede](assets/validate-xdm-content.png)

Também é possível validar os detalhes do Mapa de identidade:

1. Faça logon no site Luma usando as credenciais `test@adobe.com`/`test`

1. Retorne à [página inicial do Luma](https://luma.enablementadobe.com/content/luma/us/en.html)

1. Abra o **[!UICONTROL Experience Platform Web SDK]** na navegação à esquerda

   ![SDK da Web no Debugger](assets/identity-debugger-websdk-dark.png)

1. Selecione o **[!UICONTROL events]** linha para abrir detalhes em um pop-up

   ![SDK da Web no Debugger](assets/identity-deugger-websdk-event-dark.png)

1. Procure a variável **identityMap** na janela pop-up. Aqui você deve ver `lumaCrmId` com três chaves de authenticationState, id e primary:
   ![SDK da Web no Debugger](assets/identity-deugger-websdk-event-lumaCrmId-dark.png)


## Validar com ferramentas de desenvolvimento do navegador

Esses tipos de detalhes da solicitação também estão visíveis nas ferramentas do desenvolvedor da Web do navegador **Rede** (supondo que o site esteja carregando sua biblioteca de tags).

1. Abra as ferramentas do desenvolvedor da Web do navegador **Rede** e recarregue a página. Filtrar chamadas com `/ee` para localizar a chamada, selecione-a e, em seguida, procure no **Cabeçalhos** e **Carga** guia

   ![Guia Rede](assets/validate-dev-console.png)

1. Vá para o **Resposta** e observe como o valor ECID é incluído na resposta. Copie esse valor como você o usará para validar as informações do perfil no próximo exercício

   ![Guia Rede](assets/validate-dev-console-ecid.png)

   >[!NOTE]
   >
   >    Talvez você não veja a mesma quantidade de solicitações de carga que na captura de tela acima. Esta disparidade deve-se ao fato de as lições futuras para [configuração do Target](setup-target.md) foram concluídas no momento da captura de tela. Você pode ignorar essa diferença por enquanto.

Com um objeto XDM sendo acionado em uma página e com o conhecimento de como validar sua coleta de dados, você está pronto para configurar os aplicativos Adobe individuais usando o SDK da Web da plataforma.

[Próximo: ](setup-experience-platform.md)

>[!NOTE]
>
>Obrigado por investir seu tempo para aprender sobre o SDK da Web da Adobe Experience Platform. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
