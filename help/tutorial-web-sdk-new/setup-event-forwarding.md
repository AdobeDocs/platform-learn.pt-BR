---
title: Configurar uma propriedade de encaminhamento de eventos
description: Saiba como usar a propriedade de encaminhamento de eventos usando dados do SDK da Web do Experience Platform. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Web SDK,Tags,Event Forwarding
source-git-commit: 367789cfb0800fee7d020303629f57112e52464f
workflow-type: tm+mt
source-wordcount: '1862'
ht-degree: 3%

---

# Configurar uma propriedade de encaminhamento de eventos

Saiba como usar a propriedade de encaminhamento de eventos usando dados do SDK da Web do Experience Platform.

O encaminhamento de eventos é um novo tipo de propriedade disponível em Coleção de dados. O encaminhamento de eventos oferece a capacidade de enviar dados para fornecedores de terceiros que não sejam de Adobe diretamente da Adobe Experience Platform Edge Network, em vez do navegador tradicional do lado do cliente. Saiba mais sobre as vantagens do encaminhamento de eventos no [Visão geral do encaminhamento de eventos](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=en).


![Diagrama do SDK da Web e do encaminhamento de eventos](assets/dc-websdk-eventforwarding.png)

Para usar o encaminhamento de eventos na Adobe Experience Platform, os dados devem ser enviados para a Rede de borda da Adobe Experience Platform primeiro usando uma ou mais das três opções a seguir:

* [SDK da Web da Adobe Experience Platform](overview.md)
* [SDK móvel da Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/)
  <!--* [Server-to-Server API](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-s2s.html?lang=en)-->


>[!NOTE]
>O SDK da Web da Platform e o SDK móvel da Platform não exigem implantação por meio de tags. No entanto, é recomendado usar tags para implantar esses SDKs.

Depois de concluir as lições anteriores neste tutorial, você deve enviar dados para a Rede de borda da Platform usando o SDK da Web. Quando os dados estiverem na Platform Edge Network, você poderá ativar o encaminhamento de eventos e usar uma propriedade de encaminhamento de eventos para enviar dados a soluções que não sejam de Adobe.

## Objetivos de aprendizagem

Neste final desta lição, você poderá:

* Criar uma propriedade de encaminhamento de eventos
* Vincular uma propriedade de encaminhamento de eventos a uma sequência de dados do SDK da Web da plataforma
* Entender as diferenças entre as regras e os elementos de dados da propriedade de tag e as regras e os elementos de dados da propriedade de encaminhamento de eventos
* Criar um elemento de dados de encaminhamento de eventos
* Configurar uma regra de encaminhamento de eventos
* Validar se uma propriedade de encaminhamento de eventos está enviando dados com êxito


## Pré-requisitos

* Uma licença de software que inclui encaminhamento de eventos. O encaminhamento de eventos é um recurso pago da Coleção de dados. Entre em contato com a equipe de conta do Adobe para obter mais detalhes.
* Encaminhamento de eventos habilitado na sua organização Experience Cloud.
* Permissão de usuário para encaminhamento de eventos. (Em [Admin Console](https://adminconsole.adobe.com/), no produto Adobe Experience Platform Launch, itens de permissão para[!UICONTROL Plataformas] > [!UICONTROL Edge] e todos [!UICONTROL Direitos de propriedade]). Depois de concedido, você deve ver [!UICONTROL Encaminhamento de evento] na navegação à esquerda da interface da Coleção de dados:
  ![Propriedades do encaminhamento de eventos](assets/event-forwarding-menu.png)

* SDK da Web ou móvel do Adobe Experience Platform configurado para enviar dados para a Rede de borda. Você deve ter concluído as seguintes lições deste tutorial:

   * Configuração inicial

      * [Configurar um esquema XDM](configure-schemas.md)
      * [Configurar um namespace de identidade](configure-identities.md)
      * [Configurar uma sequência de dados](configure-datastream.md)

   * Configuração de tags

      * [Instalação da extensão do SDK da Web](install-web-sdk.md)
      * [Criar elementos de dados](create-data-elements.md)
      * [Criar identidades](create-identities.md)
      * [Criar uma regra de tag](create-tag-rule.md)
      * [Validar com o Adobe Experience Platform Debugger](validate-with-debugger.md)


## Criar uma propriedade de encaminhamento de eventos

Comece criando uma propriedade de encaminhamento de eventos:

1. Abra o [Interface da coleção de dados](https://experience.adobe.com/#/data-collection)
1. Selecionar **[!UICONTROL Encaminhamento de evento]** na navegação à esquerda
1. Selecione **[!UICONTROL Nova propriedade]**.
   ![Propriedades do encaminhamento de eventos](assets/event-forwarding-new.png)

1. Nomeie a propriedade. Nesse caso `Server-Side - Web SDK Course`

1. Selecione **[!UICONTROL Salvar]**.
   ![salvar propriedade de encaminhamento de eventos](assets/event-forwarding-save.png)

## Configurar o fluxo de dados

Para que o encaminhamento de eventos use os dados enviados para a rede de borda, você deve vincular a propriedade de encaminhamento de eventos recém-criada ao mesmo fluxo de dados usado para enviar dados para soluções Adobe.

Para configurar o Target na sequência de dados:

1. Ir para [Coleta de dados](https://experience.adobe.com/#/data-collection){target="blank"} interface
1. Na navegação à esquerda, selecione **[!UICONTROL Datastreams]**
1. Selecione o criado anteriormente `Luma Web SDK: Development Environment` sequência de dados

   ![Selecione a sequência de dados do SDK da Web Luma](assets/datastream-luma-web-sdk-development.png)

1. Selecionar **[!UICONTROL Adicionar serviço]**
   ![Adicionar um serviço à sequência de dados](assets/event-forwarding-datastream-addService.png)
1. Selecionar **[!UICONTROL Encaminhamento de evento]** como o **[!UICONTROL Serviço]**

1. No **[!UICONTROL ID da propriedade]** selecione o nome que você deu à propriedade de encaminhamento de eventos, nesse caso, `Server-Side - Web SDK Course`

1. No **[!UICONTROL ID do ambiente]** selecione o ambiente de tag ao qual você está vinculando o ambiente de encaminhamento de eventos, nesse caso `Development`

   >[!TIP]
   >
   >    Para enviar dados a um ambiente de encaminhamento de eventos fora da organização do Adobe, selecione **[!UICONTROL Inserir IDs manualmente]** e cole em uma ID. A ID é fornecida quando você cria uma propriedade de encaminhamento de eventos.

1. Selecione **[!UICONTROL Salvar]**.

   ![Ativação da sequência de dados de encaminhamento de eventos](assets/event-forwarding-datastream-enable.png)

Repita essas etapas para fluxos de dados de preparo e produção quando estiver pronto para promover as alterações por meio do fluxo de publicação.

## Encaminhar dados da Platform Edge Network para uma solução não-Adobe

Neste exercício, você aprenderá a configurar um elemento de dados de encaminhamento de eventos, configurar uma regra de encaminhamento de eventos e validar o usando uma ferramenta de terceiros chamada [Webhook.site](https://webhook.site/).

>[!NOTE]
>
>Um webhook é uma maneira de integrar sistemas diferentes em tempo semirreal. [Webhook.site](https://webhook.site/) O é uma ferramenta de terceiros que permite inspecionar, testar e automatizar facilmente (com o construtor visual de Ações personalizadas ou WebhookScript) qualquer solicitação HTTP ou email de entrada.

>[!IMPORTANT]
>
>Você já deve ter criado e mapeado elementos de dados para um objeto XDM, bem como configurado regras de tags e criado essas alterações em uma biblioteca para um ambiente de tags para continuar. Caso contrário, consulte **Configuração de tags** etapas no [pré-requisitos](setup-event-forwarding.md#prerequisites) seção. Essas etapas garantem que os dados sejam enviados para a Rede de borda da Platform e, a partir daí, você pode configurar uma propriedade de encaminhamento de eventos para encaminhar dados a uma solução que não seja de Adobe.


### Criar um elemento de dados de encaminhamento de eventos

O objeto XDM configurado anteriormente usando a extensão de tag do SDK da Web da Platform se torna a fonte de dados dos elementos de dados em uma propriedade de encaminhamento de eventos. Você usa os mesmos dados que já configurou na propriedade de tag como uma fonte de dados para o encaminhamento de eventos.

>[!IMPORTANT]
>
>Há uma diferença importante na sintaxe ao referenciar campos XDM no encaminhamento de eventos em comparação a outros contextos. Para referenciar dados em uma propriedade de encaminhamento de eventos, o caminho do elemento de dados deve incluir o `arc.event` prefixo:
>
> * `arc` significa Contexto de resposta da Adobe.
> * Por exemplo: `arc.event.xdm.web.webPageDetails.URL`
>
>Se esse caminho for especificado incorretamente, os dados não serão coletados.

Neste exercício, você encaminhará a altura da janela de visualização do navegador e a ID do Experience Cloud do objeto XDM para um webhook. O caminho do campo XDM é determinado pelo esquema XDM criado durante o [Configurar um esquema XDM](configure-schemas.md) lição.

>[!TIP]
>
>Você também pode encontrar o caminho do objeto XDM usando as ferramentas de rede do navegador da Web, filtrando para `/ee` solicitações, abertura do sinal [!UICONTROL **Carga**] e detalhando a variável que você está procurando. Em seguida, clique com o botão direito do mouse e selecione &quot;Copiar caminho da propriedade&quot;. Veja um exemplo de Altura da janela de visualização do navegador:
> ![Caminho XDM do encaminhamento de eventos](assets/event-forwarding-xdm-path.png)

1. Vá para a **[!UICONTROL Encaminhamento de evento]** propriedade que você criou recentemente

1. Na navegação à esquerda, selecione **[!UICONTROL Elementos de dados]**

1. Selecione para **[!UICONTROL Criar novo elemento de dados]**

   ![Novo elemento de dados do encaminhamento de eventos](assets/event-forwarding-new-dataelement.png)

1. **[!UICONTROL Nome]** o elemento de dados `environment.browserDetails.viewportHeight`

1. Em **[!UICONTROL Extensão]**, sair `CORE`

1. Em **[!UICONTROL Tipo de elemento de dados]**, selecione `Path`

1. Digite o caminho do Objeto XDM que contém a Altura da janela de visualização do navegador `arc.event.xdm.environment.browserDetails.viewportHeight`

1. Selecionar **[!UICONTROL Salvar]**

   ![Caminho ECID para encaminhamento de eventos](assets/event-forwarding-browser-viewpoirt-height.png)


1. Criar outro elemento de dados

1. **[!UICONTROL Nome]** it `ecid`

1. Em **[!UICONTROL Extensão]**, sair `CORE`

1. Em **[!UICONTROL Tipo de elemento de dados]**, selecione `Path`

1. Digite o caminho do objeto XDM que contém a ID do Experience Cloud `arc.event.xdm.identityMap.ECID.0.id`

1. Selecionar **[!UICONTROL Salvar]**

   ![Caminho ECID para encaminhamento de eventos](assets/event-forwarding-ecid.png)

   >[!CAUTION]
   >
   > Certifique-se de incluir o `arc.event.` prefixo no caminho. Além disso, siga o caso exato como o nome do campo Objeto XDM — o namespace da ECID deve estar em maiúsculas.


   >[!TIP]
   >
   Ao trabalhar com seu próprio site, você pode encontrar o caminho do objeto XDM com as ferramentas de rede do navegador da Web, filtrando por `/ee` solicitações, abertura do sinal [!UICONTROL **Carga**] e detalhando a variável que você está procurando. Em seguida, clique com o botão direito do mouse e selecione &quot;Copiar caminho da propriedade&quot;. Veja um exemplo de Altura da janela de visualização do navegador:
   ![Caminho XDM do encaminhamento de eventos](assets/event-forwarding-xdm-path.png)

### Instalar a extensão Adobe Cloud Connector

Para enviar dados para locais de terceiros, primeiro instale o [!UICONTROL Adobe Cloud Connector] extensão.

1. Selecionar **[!UICONTROL Extensões]** na navegação à esquerda

1. Selecione o **[!UICONTROL Catálogo]** guia

1. Procure por **[!UICONTROL Adobe Cloud Connector]**, selecione **[!UICONTROL Instalar]**

   ![Caminho ECID para encaminhamento de eventos](assets/event-forwarding-adobe-cloud-connector.png)

Não há configuração de extensão necessária. Com essa extensão, agora é possível encaminhar dados para uma solução não Adobe!

### Criar uma regra de encaminhamento de eventos

Há algumas diferenças principais entre a configuração de regras em uma propriedade de tag e uma regra em uma propriedade de encaminhamento de eventos:

* **[!UICONTROL Eventos] &amp; [!UICONTROL Condições]**:

   * **Tags**: todas as regras são acionadas por um Evento que deve ser especificado na regra, por exemplo, `Library Loaded - Page Top`. As condições são opcionais.
   * **Encaminhamento de eventos**: presume-se que cada evento enviado à Platform Edge Network seja um acionador para encaminhar dados. Por conseguinte, não existem [!UICONTROL Eventos] que devem ser selecionadas nas regras de encaminhamento de eventos. Para gerenciar quais eventos acionam uma regra de encaminhamento de eventos, você deve configurar condições.

* **Tokenização do elemento de dados**:

   * **Tags**: os nomes dos elementos de dados são tokenizados com um `%` no início e no fim do nome do elemento de dados quando usado em uma regra. Por exemplo, `%viewportHeight%`.

   * **Encaminhamento de eventos**: os nomes dos elementos de dados são tokenizados com `{{` no início e `}}` no final do nome do elemento de dados, quando usado em uma regra. Por exemplo, `{{viewportHeight}}`.

* **Sequência de ações de regra**:

   * A seção Ações de uma regra de encaminhamento de eventos é sempre executada sequencialmente. Certifique-se de que a ordem das ações esteja correta ao salvar uma regra. Essa sequência de execução não pode ser executada de forma assíncrona como com tags.

<!--
  * **Tags**: Rule actions can easily be reordered using drag-and-drop functionality.
  * **Event forwarding**: Rule actions are always executed sequentially. Make sure the order of actions is correct when you save a rule.
-->

Para configurar uma regra para encaminhar dados para o seu webhook, primeiro obtenha o webhook pessoal:

1. Ir para [Webhook.site](https://webhook.site)

1. Localizar **Seu URL exclusivo**, você usará isso como a solicitação de URL na regra de encaminhamento de eventos

1. Selecionar **[!UICONTROL Copiar para a área de transferência]**

1. Deixe essa janela aberta, pois você poderá validar os dados do encaminhamento de eventos em tempo real que estão sendo capturados pelo Webhook

   ![Copiar URL do Webhook](assets/event-forwarding-webhook.png)

1. Voltar **[!UICONTROL Coleta de dados]** > **[!UICONTROL Encaminhamento de evento]** > **[!UICONTROL Regras]** na navegação à esquerda

1. Selecionar **[!UICONTROL Criar nova regra]**

   ![Nova regra para encaminhamento de eventos](assets/event-forwarding-new-rules.png)

1. Nomear como `all events - ad cloud connector - webhook`

1. Adicionar uma ação

1. Em **[!UICONTROL Extensão]**, selecione **[!UICONTROL Adobe Cloud Connector]**

1. Em **[!UICONTROL Tipo de ação]**, selecione **[!UICONTROL Fazer chamada de busca]**

1. Cole o URL do Webhook no **[!UICONTROL URL]** campo

   ![Copiar URL do Webhook](assets/event-forwarding-rule.png)

1. Em **[Parâmetros de consulta]**, você adicionará ambos os elementos de dados criados anteriormente.

1. No **[!UICONTROL Chave]** tipo de coluna em `viewPortHeight`. No **[!UICONTROL Valor]** , insira o `{{environment.browserDetails.viewportHeight}}` elemento de dados ao digitá-lo ou selecioná-lo no ícone seletor de elemento de dados

1. Selecionar [!UICONTROL **+ Adicionar outro**] para adicionar outro parâmetro de consulta

1. No **[!UICONTROL Chave]** tipo de coluna em `ecid`. Na coluna Valor, insira a variável `{{ecid}}` elemento de dados

1. Selecionar **[!UICONTROL Manter alterações]**

   ![Adicionar parâmetro de consulta](assets/event-forwarding-rule-query-parameter.png)

1. Sua regra deve parecer com abaixo

1. Selecionar **[!UICONTROL Salvar]**

   ![Salvar regra de encaminhamento de eventos](assets/event-forwarding-rule-save.png)

### Criar a biblioteca

Crie uma biblioteca e crie todas as alterações no ambiente de desenvolvimento do encaminhamento de eventos, como você faria normalmente em uma propriedade de tag.

>[!NOTE]
>
Se não tiver vinculado as propriedades de encaminhamento de eventos de Preparo e Produção à sequência de dados, você verá o ambiente de desenvolvimento como a única opção para criar uma biblioteca no.

![Salvar regra de encaminhamento de eventos](assets/event-forwarding-initial-build.png)

## Validar regra de encaminhamento de eventos

Agora você pode validar sua propriedade de encaminhamento de eventos usando o Platform Debugger e o Webhook.site:

1. Siga as etapas para [alternar a biblioteca de tags](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) no [Site de demonstração da Luma](https://luma.enablementadobe.com/content/luma/us/en/men.html) à propriedade de tag do SDK da Web para a qual você mapeou sua propriedade de encaminhamento de eventos na sequência de dados.

1. Antes de recarregar a página, no Experience Platform Debugger, abra **[!UICONTROL Logs]** na navegação à esquerda

1. Selecione o **[!UICONTROL Edge]** e selecione **[!UICONTROL Conectar]** para visualizar as solicitações da Platform Edge Network

   ![Sessão de rede de borda do encaminhamento de eventos](assets/event-forwarding-edge-session.png)

1. Recarregar a página

1. Você verá solicitações adicionais que dão visibilidade das solicitações do lado do servidor enviadas pela Platform Edge Network para o WebHook

1. A solicitação para focalizar a validação é aquela que mostra o URL totalmente construído sendo enviado pela rede de borda

   ![Depurador de encaminhamento de eventos](assets/event-forwarding-debugger.png)


1. Observe os parâmetros de cadeia de caracteres de consulta viewPortHeight e ecid

   ![Cadeias de caracteres de consulta de validação do encaminhamento de eventos](assets/event-forwarding-validate-data.png)

1. Eles correspondem aos dados vistos no objeto XDM

   ![Dados correspondentes do encaminhamento de eventos](assets/event-forwarding-matching-data.png)

1. Por último, valide as correspondências de dados no [Webhook.site](https://webhook.site) e também visualizando a janela aberta do Webhook

   ![Dados do site do webhook de encaminhamento de eventos](assets/event-forwarding-webhook-data.png)

Parabéns! Você configurou o encaminhamento de eventos!

[Próximo: ](conclusion.md)

>[!NOTE]
>
Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar feedback geral ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)