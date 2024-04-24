---
title: Validar implementações do SDK da Web com o Experience Platform Debugger
description: Saiba como validar a implementação do SDK da Web da sua plataforma com o Adobe Experience Platform Debugger. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Web SDK,Tags,Debugger
exl-id: 150bb1b1-4523-4b44-bd4e-6cabc468fc04
source-git-commit: aeff30f808fd65370b58eba69d24e658474a92d7
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 1%

---

# Validar implementações do SDK da Web com o Experience Platform Debugger

Saiba como validar a implementação do SDK da Web da sua plataforma com o Adobe Experience Platform Debugger.

O Experience Platform Debugger é uma extensão disponível para os navegadores Chrome e Firefox, que ajuda a visualizar a tecnologia de Adobe implementada nas páginas da Web. Baixe a versão do seu navegador de preferência:

* [Extensão do Firefox](https://addons.mozilla.org/pt-BR/firefox/addon/adobe-experience-platform-dbg/)
* [Extensão do Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Se você nunca usou o depurador antes (e este é diferente do Adobe Experience Cloud Debugger mais antigo), assista a este vídeo de visão geral de cinco minutos:

>[!VIDEO](https://video.tv.adobe.com/v/32156?learn=on)

Nesta lição, você usa o [Extensão do Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) para substituir a propriedade de tag codificada na [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html) com sua própria propriedade.

Essa técnica é chamada de alternação de ambiente e será útil posteriormente, ao trabalhar com tags em seu próprio site. Você pode carregar seu site em produção em seu navegador, mas com seus *desenvolvimento* ambiente de tags. Essa capacidade permite fazer e validar de forma segura as alterações nas tags independentemente das suas versões de código normais. Afinal, essa separação das versões de tag de marketing das versões regulares de código é um dos principais motivos pelos quais os clientes usam tags!

## Objetivos de aprendizagem

No final desta lição, você poderá usar o depurador para:

* Carregar uma biblioteca de tags alternativa
* Validar se o evento XDM do lado do cliente está capturando e enviando dados conforme esperado para o Edge Network da plataforma
* Habilitar o Edge Trace para exibir solicitações do lado do servidor enviadas pelo Platform Edge Network

## Pré-requisitos

Você está familiarizado com as tags de Coleção de dados e a [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} e concluíram as lições anteriores no tutorial:

* [Configurar um esquema XDM](configure-schemas.md)
* [Configurar um namespace de identidade](configure-identities.md)
* [Configurar uma sequência de dados](configure-datastream.md)
* [Extensão SDK da Web instalada na propriedade da tag](install-web-sdk.md)
* [Criar elementos de dados](create-data-elements.md)
* [Criar identidades](create-identities.md)
* [Criar regras de tag](create-tag-rule.md)

## Carregar bibliotecas de tags alternativas com o Debugger

O depurador de Experience Platform tem um recurso interessante que permite substituir uma biblioteca de tags existente por outra. Essa técnica é útil para validação e permite ignorar muitas etapas de implementação neste tutorial.

1. Verifique se você tem o [Site de demonstração da Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} abra e selecione o ícone da extensão do Experience Platform Debugger
1. O Debugger abrirá e mostrará alguns detalhes da implementação codificada (talvez seja necessário recarregar o site Luma depois de abrir o Debugger)
1. Confirme se o Debugger é &quot;**[!UICONTROL Conectado ao Luma]**&quot; como mostrado abaixo e selecione o &quot;**[!UICONTROL bloquear]**&quot; para bloquear o Debugger no site Luma.
1. Selecione o **[!UICONTROL Conectar]** e faça logon no Adobe Experience Cloud usando sua ID de Adobe.
1. Agora vá para **[!UICONTROL Tags do Experience Platform]** na navegação à esquerda

   ![Tela de tag do depurador](assets/validate-launch-screen.png)

1. Selecione o **[!UICONTROL Configuração]** guia
1. À direita de onde ele mostra a **[!UICONTROL Códigos incorporados de página]**, abra o **[!UICONTROL Ações]** e selecione **[!UICONTROL Substituir]**

   ![Selecione Ações > Substituir](assets/validate-switch-environment.png)

1. Como você está autenticado, o Debugger extrairá suas propriedades e ambientes de tag disponíveis. Selecione sua propriedade; nesse caso, `Web SDK Course 3`
1. Selecione o `Development` ambiente
1. Selecione o **[!UICONTROL Aplicar]** botão

   ![Selecionar a propriedade de tag alternativa](assets/validate-switch-selection.png)

1. O site Luma será recarregado agora _com sua própria propriedade de tag_.

   ![propriedade de tag substituída](assets/validate-switch-success.png)

À medida que você prossegue no tutorial, usa essa técnica de mapear o site Luma para sua própria propriedade de tag para validar a implementação do SDK da Web da Platform. Ao começar a usar tags no site de produção, você pode usar essa mesma técnica para validar as alterações à medida que elas são feitas no ambiente de desenvolvimento de tags.

## Validar solicitações de rede do lado do cliente com o Experience Platform Debugger

Você pode usar o Debugger para validar beacons do lado do cliente acionados a partir da implementação do SDK da Web da Platform para exibir os dados enviados para a Rede de borda da Platform:

1. Ir para **[!UICONTROL Resumo]** na navegação à esquerda, para ver os detalhes da propriedade da tag

   ![Guia Resumo](assets/validate-summary.png)

1. Agora vá para **[!UICONTROL Experience Platform Web SDK]** na navegação à esquerda para ver o **[!UICONTROL Solicitações de rede]**
1. Abra o **[!UICONTROL events]** linha

   ![Solicitação do SDK da Web do Adobe Experience Platform](assets/validate-aep-screen.png)

1. Observe como você pode ver a `web.webpagedetails.pageView` tipo de evento que você especificou em seu [!UICONTROL Atualizar variável] e outras variáveis prontas para uso que seguem a `AEP Web SDK ExperienceEvent` grupo de campos

   ![Detalhes do evento](assets/validate-event-pageViews.png)

1. Role para baixo até `web` objeto, selecione para abri-lo e inspecionar o `webPageDetails.name`, `webPageDetails.server`, e `webPageDetails.siteSection`. Eles devem corresponder aos `digitalData` variáveis de camada de dados na página inicial

>[!TIP]
>
> Para visualizar e comparar as `digitalData` camada de dados na página inicial:
>
> 1. Na página inicial do Luma, abra as ferramentas de desenvolvedor do navegador. No caso do Chrome, selecione o botão `F12` no teclado
> 1. Selecione o **[!UICONTROL Console]** guia
> 1. Enter `digitalData` e selecione `Enter` no teclado para exibir os valores da camada de dados

![Guia Rede](assets/validate-xdm-content.png)

Também é possível validar os detalhes do Mapa de identidade:

1. Faça logon no site Luma usando as credenciais `test@adobe.com`/`test`

1. Retorne à [página inicial do Luma](https://luma.enablementadobe.com/content/luma/us/en.html)

1. Abra o **[!UICONTROL Experience Platform Web SDK]** na navegação à esquerda

   ![SDK da Web no Debugger](assets/identity-debugger-websdk-dark.png)

1. Selecione o **[!UICONTROL events]** linha para abrir detalhes em um pop-up

   ![SDK da Web no Debugger](assets/identity-deugger-websdk-event-dark.png)

1. Procure por **identityMap** na janela pop-up. Aqui você deve ver `lumaCrmId` com três chaves de authenticatedState, id e primary:
   ![SDK da Web no Debugger](assets/identity-deugger-websdk-event-lumaCrmId-dark.png)

### Validar solicitações do lado do cliente com ferramentas de desenvolvimento do navegador

Esses tipos de detalhes da solicitação também estão visíveis nas ferramentas do desenvolvedor da Web do navegador **Rede** (supondo que o site esteja carregando a biblioteca de tags).

1. Abra as ferramentas do desenvolvedor da Web do navegador. **Rede** e recarregue a página. Filtrar chamadas com `/ee` para localizar a chamada, selecione-a e procure no **Cabeçalhos** e **Carga** guia

   ![Guia Rede](assets/validate-dev-console.png)

1. Vá para a **Resposta** e observe como o valor ECID é incluído na resposta. Copie esse valor como você o usará para validar as informações do perfil no próximo exercício

   ![Guia Rede](assets/validate-dev-console-ecid.png)

   >[!NOTE]
   >
   > O valor da ECID está visível na resposta da rede. Ela não está incluída no `identityMap` parte da solicitação de rede, nem é armazenada nesse formato em um cookie.

## Validar solicitações de rede do lado do servidor com o Experience Platform Debugger

Como você aprendeu na [Configurar um fluxo de dados](configure-datastream.md) lição, o SDK da Web da Platform envia primeiro os dados da propriedade digital para o Platform Edge Network. Em seguida, o Platform Edge Network faz solicitações adicionais do lado do servidor para os serviços correspondentes ativados no fluxo de dados. Você pode validar as solicitações do lado do servidor feitas pelo Platform Edge Network usando o Rastreamento de borda no Debugger.

<!--Furthermore, you can also validate the fully processed payload after it reaches an Adobe application by using [Adobe Experience Platform Assurance](https://experienceleague.adobe.com/en/docs/experience-platform/assurance/home). -->


### Ativar o Edge Trace

Para ativar o Edge Trace:

1. Na navegação à esquerda de **[!UICONTROL Experience Platform Debugger]** selecionar **[!UICONTROL Logs]**
1. Selecione o **[!UICONTROL Edge]** e selecione **[!UICONTROL Conectar]**

   ![Connect Edge Trace](assets/analytics-debugger-edgeTrace.png)

1. Está vazio por enquanto

   ![Rastreamento de Borda Conectado](assets/analytics-debugger-edge-connected.png)

1. Atualize o [Página inicial da Luma](https://luma.enablementadobe.com/) e verificar **[!UICONTROL Experience Platform Debugger]** novamente, para ver os dados aparecerem.

   ![Rastreamento de borda de beacon do Analytics](assets/validate-edge-trace.png)

Nesse ponto, não é possível visualizar solicitações de Edge Network da Platform indo para aplicativos de Adobe porque você não ativou nenhum no fluxo de dados. Em lições futuras, você usa o Edge Trace para visualizar as solicitações do lado do servidor de saída para aplicativos Adobe e encaminhamento de eventos. Mas, primeiro, conheça outra ferramenta para validar as solicitações do lado do servidor feitas pelo Platform Edge Network — Adobe Experience Platform Assurance!

[Próximo: ](validate-with-assurance.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar feedback geral ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
