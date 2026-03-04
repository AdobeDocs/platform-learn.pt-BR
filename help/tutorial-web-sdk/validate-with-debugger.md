---
title: Validar implementações do Web SDK com o Experience Platform Debugger
description: Saiba como validar a implementação do Platform Web SDK com o Adobe Experience Platform Debugger. Esta lição é parte do tutorial Implementar a Adobe Experience Cloud com o SDK da web.
feature: Web SDK,Tags,Debugger
jira: KT-15405
exl-id: 150bb1b1-4523-4b44-bd4e-6cabc468fc04
source-git-commit: 4e5fe50c1ec7a867fed57700b35851b859680fef
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 2%

---

# Validar implementações do Web SDK com o Experience Platform Debugger

Saiba como validar a implementação do SDK da web da Adobe Experience Platform com o Adobe Experience Platform Debugger.


O Experience Platform Debugger é uma [extensão do Chrome](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) que ajuda a visualizar a tecnologia Adobe implementada nas suas páginas da Web. O Experience Platform Debugger e o console do desenvolvedor do navegador são as melhores maneiras de validar e depurar os aspectos do lado do navegador da implementação do Web SDK. O Adobe Experience Platform Assurance, abordado na próxima lição, fornece a melhor visualização dos dados à medida que eles entram e saem do Platform Edge Network.

![Diagrama de validação do Web SDK e do Adobe Experience Platform](assets/dc-websdk-validation.png)


Se você nunca usou o Debugger antes, assista a este vídeo de visão geral de cinco minutos:

>[!VIDEO](https://video.tv.adobe.com/v/32156?learn=on&enablevpops)

Nesta lição, você usa a [extensão do Adobe Experience Platform Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) para substituir a propriedade de tag codificada no [site de demonstração Luma](https://luma.enablementadobe.com) com sua própria propriedade.

Essa técnica é chamada de alternação de ambiente e será útil posteriormente, ao trabalhar com tags em seu próprio site. Ele permite carregar o site de produção em seu navegador, mas com sua biblioteca de tags de *desenvolvimento*. Essa capacidade permite fazer e validar de forma segura as alterações nas tags independentemente das suas versões de código normais. Afinal, essa separação das versões de tag de marketing das versões regulares de código é um dos principais motivos pelos quais os clientes usam tags!

## Objetivos de aprendizagem

No final desta lição, você poderá usar o depurador para:

* Carregar uma biblioteca de tags alternativa
* Validar se o evento XDM do lado do cliente está capturando e enviando dados conforme esperado para o Platform Edge Network
* Ativar o Edge Trace para exibir solicitações do lado do servidor enviadas pelo Platform Edge Network

## Pré-requisitos

Você está familiarizado com as tags da Coleção de dados e o [site de demonstração Luma](https://luma.enablementadobe.com/){target="_blank"} e concluiu as lições anteriores no tutorial:

* [Configurar um esquema XDM](configure-schemas.md)
* [Configurar um namespace de identidade](configure-identities.md)
* [Configurar uma sequência de dados](configure-datastream.md)
* [Extensão do Web SDK instalada na propriedade da tag](install-web-sdk.md)
* [Criar elementos de dados](create-data-elements.md)
* [Capturar identidades](create-identities.md)
* [Criar regras de tag](create-tag-rule.md)

## Carregar bibliotecas de tags alternativas com o Debugger

O Experience Platform Debugger tem um recurso interessante que permite substituir uma biblioteca de tags existente por outra. Essa técnica é útil para validação e permite ignorar muitas etapas de implementação neste tutorial.

1. Verifique se o [site de demonstração do Luma](https://luma.enablementadobe.com){target="_blank"} está aberto e selecione o ícone da extensão do Experience Platform Debugger
1. O Debugger abrirá e mostrará alguns detalhes da implementação codificada (talvez seja necessário recarregar o site Luma depois de abrir o Debugger)
1. Confirme se o Depurador está &quot;**[!UICONTROL Conectado ao Luma]**&quot;, como mostrado abaixo, e selecione o ícone &quot;**[!UICONTROL bloquear]**&quot; para bloquear o Depurador no site Luma.
1. Selecione o botão **[!UICONTROL Entrar]**, entre no Adobe Experience Cloud usando sua Adobe ID e selecione sua Organização.

   >[!TIP]
   >
   > Se o depurador exibir seu nome de usuário em vez do nome da organização depois de entrar, saia e tente novamente.


   ![Tela de tag do depurador](assets/validate-launch-screen.png)

1. Agora, vá para **[!UICONTROL Tags do Experience Platform]** no painel de navegação esquerdo
1. Selecione a guia **[!UICONTROL Configuração]**
1. À direita do local onde ele mostra os **[!UICONTROL Códigos incorporados de página]**, abra a lista suspensa **[!UICONTROL Ações]** e selecione **[!UICONTROL Substituir]**

   ![Selecionar ações > Substituir](assets/validate-switch-environment.png)

1. Como você está autenticado, o Debugger extrairá suas propriedades e ambientes de tag disponíveis. Selecione sua propriedade
1. Selecione seu ambiente `Development`
   ![Selecione a propriedade de marca alternativa](assets/validate-switch-selection.png)

   >[!TIP]
   >
   > Se você não conseguir selecionar sua propriedade e ambiente usando os menus suspensos, vá para [!UICONTROL Marcas] > [!UICONTROL Ambientes] > [!UICONTROL Desenvolvimento] > [!UICONTROL Instalar] e selecione o ícone para copiar o código incorporado e colá-lo no Depurador:
   > ![Selecione a propriedade de marca alternativa](assets/validate-copy-embed-code.png)

1. Selecione o botão **[!UICONTROL Aplicar]**

1. O site Luma recarregará agora _com sua própria propriedade de tag_.

   ![propriedade de marca substituída](assets/validate-switch-success.png)

À medida que você prossegue no tutorial, usa essa técnica de mapear o site Luma para sua própria propriedade de tag para validar a implementação do Platform Web SDK. Ao usar tags em seu próprio site, você pode usar essa mesma técnica para validar bibliotecas de tags de desenvolvimento em seu site de produção.



## Validar com o Debugger

### Validar solicitações de rede e XDM

Você pode usar o Debugger para validar beacons do lado do cliente acionados a partir da implementação do Platform Web SDK para exibir os dados enviados para o Platform Edge Network:

1. Vá para **[!UICONTROL Resumo]** na navegação à esquerda para ver os detalhes da propriedade da marca

   ![Guia Resumo](assets/validate-summary.png)

1. Agora, vá para **[!UICONTROL Experience Platform Web SDK]** na navegação à esquerda para ver as **[!UICONTROL Solicitações de Rede]**
1. Abrir a linha **[!UICONTROL eventos]**

   ![Solicitação do Adobe Experience Platform Web SDK](assets/validate-aep-screen.png)

1. Observe como você pode ver o tipo de evento `web.webPageDetails.pageView` especificado na ação [!UICONTROL Atualizar variável] e outras variáveis prontas para uso que seguem o grupo de campos `AEP Web SDK ExperienceEvent`

   ![Detalhes do evento](assets/validate-event-pageViews.png)

1. Role para baixo até o objeto `web`, selecione para abri-lo e inspecionar o `webPageDetails.name`. Eles devem corresponder às `adobeDataLayer` variáveis de camada de dados correspondentes na página inicial

>[!TIP]
>
> Para exibir e comparar a camada de dados `adobeDataLayer` na página inicial:
>
> 1. Na página inicial do Luma, abra as ferramentas de desenvolvedor do navegador. No caso do Chrome, selecione o botão `F12` no teclado
> 1. Selecione a guia **[!UICONTROL Console]**
> 1. Digite `adobeDataLayer` e selecione `Enter` no teclado para exibir os valores da camada de dados

![Guia Rede](assets/validate-xdm-content.png)

Valide os eventos e as variáveis definidos nas páginas do produto, no carrinho e na página de confirmação de pedido.

### Validar mapa de identidade

Também é possível validar os detalhes do Mapa de identidade:

1. Selecione **[!DNL Sign In]** no [site Luma](https://luma.enablementadobe.com/){target=_blank}. Selecione **[!DNL Create Account]** e crie uma conta usando as credenciais `test@test.com`/`test`

1. Use o atalho **[!UICONTROL Ir para o mais recente]** no Depurador para ir rapidamente para o evento mais recente do Web SDK (é a última coluna). Selecione a linha **[!UICONTROL eventos]** para abrir a modal de detalhes.

1. Pesquise por **identityMap** no modal. Aqui você deve ver `lumaCrmId` com três chaves de authenticatedState, id e designação primária:
   ![Web SDK no Depurador](assets/identity-deugger-websdk-event-lumaCrmId-dark.png)

## Validar com as ferramentas do desenvolvedor do navegador

Muitos desenvolvedores da Web podem preferir visualizar a implementação nas ferramentas do desenvolvedor do navegador. Isso é especialmente importante, pois nem todos os navegadores são compatíveis com a extensão Debugger. Além disso, devido à estrutura flexível, há detalhes adicionais de implementação que você pode inspecionar, como cookies e detalhes de resposta.

### Validar solicitações de rede

Os detalhes da solicitação do Web SDK também estão visíveis na guia **Rede** das ferramentas de desenvolvedor da Web do navegador (supondo que o site esteja carregando sua biblioteca de marcas).

1. Abra a guia **Rede** das ferramentas de desenvolvedor da Web do navegador e recarregue a página. Filtrar chamadas com `/ee` para localizar a chamada, selecioná-la e procurar na guia **Cabeçalhos** e na guia **Carga**

   ![Guia Rede](assets/validate-dev-console.png)

1. Vá para a guia **Preview** e observe como o valor da ECID é incluído na resposta da rede.

   ![Guia Rede](assets/validate-dev-console-ecid.png)

   >[!NOTE]
   >
   > O valor da ECID está visível na resposta da rede. Ela não está incluída na parte `identityMap` da solicitação de rede, nem está armazenada nesse formato em um cookie.

### Cookies do SDK da Web

Enquanto estivermos nas ferramentas do desenvolvedor, vamos dar uma olhada em alguns dos conjuntos de cookies do Web SDK no navegador. Abra Aplicativo > Cookies > https://luma.enablementadobe.com

Você deve ver vários cookies definidos pelo Web SDK:

* kndctr_[IMS_ORGID]_AdobeOrg_identity: armazena dados relacionados à ECID
* kndctr_[IMS_ORGID]_AdobeOrg_cluster: armazena o local do data center usado para que as chamadas de rede subsequentes sejam roteadas para os mesmos servidores da Edge
* AMCV_[IMS_ORGID]%40AdobeOrg: este é o cookie AMCV herdado usado pelas bibliotecas Experience Cloud pré-Web SDK e está definido porque deixamos a configuração padrão **[!UICONTROL Migrar ECID para VisitorAPI para a SDK]** da Web selecionada na extensão de tags Adobe Experience Platform Web SDK. Essa configuração é importante ter sido ativada durante a migração das páginas de bibliotecas mais antigas para o Web SDK, mas pode ser desativada depois que todas as páginas forem migradas por um determinado período.

![Guia Cookies](assets/debugger-cookies.png)

Se você limpar esses cookies e recarregar a página, poderá notar alguns cookies adicionais de terceiros definidos no domínio `.demdex.net`. Eles foram definidos porque deixamos a configuração padrão **[!UICONTROL Usar cookies de terceiros]**: **[!UICONTROL Habilitada]** na extensão de marcas do Adobe Experience Platform Web SDK. Se o navegador não permitir cookies de terceiros, eles serão removidos quando você recarregar a página.

![Cookies Demdex](assets/debugger-demdex-cookies.png)


### Armazenamento local da Luma

O site de demonstração Luma usa tecnologias estritamente do lado do cliente, como HTML, CSS e JavaScript. Não há mecanismos de armazenamento de back-end, além da implementação do Experience Cloud usada pelo estado padrão do site. Informações como detalhes de nome de usuário são armazenadas localmente em seu navegador usando o localStorage. Portanto, se você excluir essas informações ou usar uma janela de incognitor, você notará que talvez precise recriar uma conta de usuário de teste criada anteriormente.

![Armazenamento local](assets/debugger-local-storage.png)


Em seguida, saiba como validar essas solicitações de rede quando elas são recebidas e transmitidas do Platform Edge Network usando o Adobe Experience Platform Assurance!

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [postagem de discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/adobe-experience-platform-18/tutorial-discussion-implement-adobe-experience-cloud-with-web-sdk-tutorial-248848?profile.language=pt)
