---
title: Assimilar dados de transmissão
seo-title: Ingest streaming data | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Assimilar dados de transmissão
description: Nesta lição, você transmitirá dados no Experience Platform usando a Web SDK.
role: Data Engineer
feature: Data Ingestion
jira: KT-4348
thumbnail: 4348-ingest-streaming-data.jpg
exl-id: 09c24673-af8b-40ab-b894-b4d76ea5b112
source-git-commit: 97fba09ddba62cffe4428592ce25e4f26c3a5850
workflow-type: tm+mt
source-wordcount: '3316'
ht-degree: 0%

---

# Assimilar dados de transmissão

<!--1hr-->

Nesta lição, você transmitirá dados usando o Adobe Experience Platform Web SDK.

Outras maneiras comuns de transmitir dados para a Platform


>[!WARNING]
>
> O site do Luma usado neste tutorial deve ser substituído durante a semana de 16 de fevereiro de 2026. O trabalho realizado como parte deste tutorial pode não se aplicar ao novo site.

Há duas tarefas principais que devem ser concluídas na interface da Coleção de dados:

* Precisamos implementar o Web SDK no site da Luma para enviar dados sobre a atividade do visitante do site para a rede Experience Platform Edge. Faremos uma implementação simples usando tags (antigo Launch)

* Precisamos configurar um fluxo de dados, que informa à rede da Edge para onde encaminhar os dados. Vamos configurá-los para enviar os dados para o conjunto de dados `Luma Web Events` em nossa sandbox da Platform.

**Os engenheiros de dados** precisarão assimilar dados de transmissão fora deste tutorial. Ao implementar os SDKs da Web ou móvel da Adobe Experience Platform, normalmente um desenvolvedor da Web ou móvel está envolvido na criação da camada de dados e na configuração da propriedade de tag.

Antes de começar os exercícios, assista a estes dois pequenos vídeos para saber mais sobre a assimilação de dados por transmissão e o Web SDK:

>[!VIDEO](https://video.tv.adobe.com/v/28425?learn=on&enablevpops)

>[!VIDEO](https://video.tv.adobe.com/v/34141?learn=on&enablevpops)

>[!NOTE]
>
>Embora este tutorial se concentre na assimilação por transmissão de sites com o Web SDK, você também pode transmitir dados usando o [SDK Móvel](https://experienceleague.adobe.com/pt-br/docs/platform-learn/implement-mobile-sdk/overview), a [API do Edge Network Server](https://experienceleague.adobe.com/pt-br/docs/platform-learn/data-collection/server-api/overview) e a [API HTTP](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/connectors/streaming/http).

## Permissões necessárias

Na lição [Configurar Permissões](configure-permissions.md), você configura todos os controles de acesso necessários para concluir esta lição.

<!--
* Permission items **[!UICONTROL Launch]** > **[!UICONTROL Property Rights]** > **[!UICONTROL Approve]**, **[!UICONTROL Develop]**, **[!UICONTROL Manage Environments]**, **[!UICONTROL Manage Extensions]**, and **[!UICONTROL Publish]**
* Permission item **[!UICONTROL Launch]** > **[!UICONTROL Company Rights]** > **[!UICONTROL Manage Properties]**
* User-role access to the `Luma Tutorial Launch` product profile
* Admin-role access to the `Luma Tutorial Launch` product profile
* Permission items **[!UICONTROL Platform]** > **[!UICONTROL Data Ingestion]** > **[!UICONTROL View Sources]** and **[!UICONTROL Manage Sources]**
* Permission items **[!UICONTROL Platform]** > **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission items **[!UICONTROL Platform]** > **[!UICONTROL Profiles]** > **[!UICONTROL View Profiles]**, **[!UICONTROL Manage Profiles]** and **[!UICONTROL Export Audience Segment]**
* Permission item **[!UICONTROL Platform]** > **[!UICONTROL Sandbox Administration]** > **[!UICONTROL View Sandboxes]**
* Permission item **[!UICONTROL Platform]** > **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

<!--## Create a streaming source

1. Log into the [Experience Platform  user interface](https://experience.adobe.com/platform/)
1. Go to **[!UICONTROL Sources]** in the left navigation
1. Filter the list by selecting **[!UICONTROL Streaming]**
1. In the **[!UICONTROL HTTP API]** section, select the **[!UICONTROL Configure]** button
    ![Configure an HTTP API streaming source](assets/websdk-source-confiigureHTTPAPI.png)
1. On the **[!UICONTROL Authentication]** step, enter `Luma Web Events Source` as the **[!UICONTROL Account name]** and select the **[!UICONTROL Connect to source]** button (we don't need to enable authentication since the data will be originating from website visitors)
    ![Configure an HTTP API streaming source](assets/websdk-source-connectSource.png)
1. Once connected, select the **[!UICONTROL Next]** button to proceed to the next step in the workflow
1. On the **[!UICONTROL Select data]** step, choose **[!UICONTROL Existing Dataset]**, select your `Luma Web Events Dataset`, and then select the **[!UICONTROL Next]** button
    ![Select your dataset](assets/websdk-source-selectDataset.png)
1. On the **[!UICONTROL Dataflow detail]** step, select the **[!UICONTROL Next]** button:
    ![Select Next](assets/websdk-source-dataflowName.png)
    <!--What is a good practice for naming the data flow vs the source-->
<!--
1. On the **[!UICONTROL Review]** step, review your source details and select the **[!UICONTROL Finish]** button:
    ![Select Finish](assets/websdk-source-review.png)
-->

## Configurar o fluxo de dados

Primeiro, configuraremos o fluxo de dados. Um fluxo de dados informa ao Experience Platform Edge Network para onde enviar os dados depois de recebê-los da chamada do Web SDK. Por exemplo, deseja enviar os dados para o Experience Platform, Adobe Analytics ou Adobe Target? Os fluxos de dados são gerenciados na interface da Coleção de dados (antigo Launch) e são essenciais para a coleta de dados com o Web SDK.

![Web SDK, sequências de dados e diagrama do Edge Network](assets/dc-websdk-datastreams.png)

Para criar sua [!UICONTROL sequência de dados]:

1. Faça logon na [interface da Coleção de dados da Experience Platform](https://experience.adobe.com/launch/)
   <!--when will the edge config go live?-->

1. Selecione **[!UICONTROL Datastreams]** na navegação à esquerda
1. Selecione o botão **[!UICONTROL Nova sequência de dados]** no canto superior direito

   ![Selecionar sequências de dados na navegação à esquerda](assets/websdk-edgeConfig-clickNav.png)


1. Para o **[!UICONTROL Nome Amigável]**, digite `Luma Platform Tutorial` (adicione seu nome ao final, se várias pessoas da sua empresa estiverem fazendo este tutorial)
1. Selecione o botão **[!UICONTROL Salvar]**

   ![Nomeie o datastram e salve](assets/websdk-edgeConfig-name.png)

Na próxima tela, especifique para onde deseja enviar dados. Para enviar dados ao Experience Platform:

1. Alternar no **[!UICONTROL Adobe Experience Platform]** para expor campos adicionais
1. Para **[!UICONTROL Sandbox]**, selecione `Luma Tutorial`
1. Para **[!UICONTROL Conjunto de Dados do Evento]**, selecione `Luma Web Events Dataset`
1. Se você usar outros aplicativos da Adobe, sinta-se à vontade para explorar as outras seções para ver quais informações são necessárias na Configuração do Edge dessas outras soluções. Lembre-se de que o Web SDK foi desenvolvido não apenas para transmitir dados para o Experience Platform, mas também para substituir todas as bibliotecas JavaScript anteriores usadas por outros aplicativos da Adobe. A Configuração do Edge é usada para especificar os detalhes da conta de cada aplicativo para o qual você deseja enviar os dados.
1. Selecione **[!UICONTROL Salvar]**
   ![Configurar a sequência de dados e salvar](assets/websdk-edgeConfig-addEnvironment.png)

Depois que a configuração do Edge for salva, a tela resultante mostrará três ambientes que foram criados para desenvolvimento, armazenamento temporário e produção. Ambientes de desenvolvimento adicionais podem ser adicionados:
![Cada configuração do Edge pode ter vários ambientes](assets/websdk-edgeConfig-environments.png)
Todos os três ambientes contêm os detalhes da plataforma que você acabou de inserir. No entanto, esses detalhes podem ser configurados de formas diferentes por ambiente. Por exemplo, cada ambiente pode enviar dados para uma sandbox da Platform diferente. Neste tutorial, não faremos nenhuma personalização adicional no nosso fluxo de dados.

## Instalar a extensão Web SDK

### Adicionar uma propriedade do

Primeiro, devemos criar uma propriedade de tag (anteriormente uma propriedade de tag ). Uma propriedade é um container para todas as JavaScript, regras e outros recursos necessários para coletar detalhes de uma página da Web e enviá-los para vários locais.

Para criar uma propriedade:

1. Vá para **[!UICONTROL Propriedades]** na navegação à esquerda
1. Selecione o botão **[!UICONTROL Nova propriedade]**
   ![Adicionar uma nova propriedade](assets/websdk-property-addNewProperty.png)
1. Como o **[!UICONTROL Nome]**, digite `Luma Platform Tutorial` (adicione seu nome ao final, se várias pessoas da sua empresa estiverem fazendo este tutorial)
1. Como os **[!UICONTROL Domínios]**, digite `enablementadobe.com` (explicado mais tarde)
1. Selecione **[!UICONTROL Salvar]**
   ![Detalhes da propriedade](assets/websdk-property-propertyDetails.png)

<!--
After saving the property, you might see an error message like the one below. If so, this is because you don't actually have access to the property you just created. To fix this, we need to go to the Admin Console to give yourself access:
    ![Error after saving the profile](assets/websdk-property-errorCreating.png)

To give yourself access to the property:

1. In a separate browser tab, log into the [Admin Console](https://adminconsole.adobe.com/)
1. Go to **[!UICONTROL Products]** from the top navigation
1. Select **[!UICONTROL Adobe Experience Platform Launch]** on the left navigation
1. Go to your `Luma Tutorial Launch` product profile
1. Go to the **[!UICONTROL Permissions]** tab
1. On the **[!UICONTROL Properties]** row, select **[!UICONTROL Edit]**
    ![Edit the Property Permissions](assets/websdk-adminconsole-editPermissions.png)
1. Select the "+" icon to move your `Luma Platform Tutorial` property to the right-hand side and select the **[!UICONTROL Save]** button to update the permissions
   
    ![Add the new property](assets/websdk-adminconsole-addProperty.png)

Now switch back to your browser tab with the Data Collection interface still open. Reload the page and the `Luma Platform Tutorial` property should display in the list. Select to open the property:

![Luma Platform Tutorial should appear](assets/websdk-property-showsInList.png)
-->

## Adicionar a extensão Web SDK

Agora que você tem uma propriedade, é possível adicionar o Web SDK usando uma extensão. Uma extensão é um pacote de códigos que estende a interface e a funcionalidade da Coleção de dados. Para adicionar a extensão:

1. Abra a propriedade da tag
1. Vá para **[!UICONTROL Extensões]** na navegação à esquerda
1. Vá para a guia **[!UICONTROL Catálogo]**
1. Há muitas extensões disponíveis para tags. Filtrar o catálogo com o termo `Web SDK`
1. Na extensão do **[!UICONTROL Adobe Experience Platform Web SDK]**, selecione o botão **[!UICONTROL Instalar]**
   ![Instalar a extensão Adobe Experience Platform Web SDK](assets/websdk-property-addExtension.png)
1. Há várias configurações disponíveis para a extensão Web SDK, mas há apenas duas que vamos configurar para este tutorial. Atualize o **[!UICONTROL Domínio do Edge]** para `data.enablementadobe.com`. Essa configuração permite definir cookies primários com a implementação do Web SDK, o que é incentivado. Posteriormente nesta lição, você mapeará um site no domínio `enablementadobe.com` para a propriedade de tag. O CNAME do domínio `enablementadobe.com` já foi configurado, portanto, `data.enablementadobe.com` encaminhará para os servidores do Adobe. Ao implementar o Web SDK em seu próprio site, será necessário criar um CNAME para fins de coleta de dados, por exemplo, `data.YOUR_DOMAIN.com`
1. Na lista suspensa **[!UICONTROL Sequência de dados]**, selecione a sequência de dados `Luma Platform Tutorial`.
1. Fique à vontade para ver as outras opções de configuração (mas não as altere!) e selecione **[!UICONTROL Salvar]**
   <!--is edge domain required for first party? when will it break?-->
   <!--any other fields that should be highlighted-->
   ![](assets/websdk-property-configureExtension.png)



## Criar uma regra para enviar dados

Agora criaremos uma regra para enviar dados para a Platform. Uma regra é uma combinação de eventos, condições e ações que instruem as tags a fazer algo. Para criar uma regra:

1. Vá para **[!UICONTROL Regras]** na navegação à esquerda
1. Selecione o botão **[!UICONTROL Criar nova regra]**
   ![Criar uma regra](assets/websdk-property-createRule.png)
1. Atribua um nome à regra `All Pages - Library Loaded`
1. Em **[!UICONTROL Eventos]**, selecione o botão **[!UICONTROL Adicionar]**
   ![Nomear a regra e adicionar um evento](assets/websdk-property-nameRule.png)
1. Use a **[!UICONTROL Extensão de]**&#x200B;**[!UICONTROL do &lbrace;Core]** e selecione **[!UICONTROL Biblioteca Carregada (Início da Página)]** como o **[!UICONTROL Tipo de Evento]**. Essa configuração significa que nossa regra é acionada sempre que a biblioteca do Launch é carregada em uma página.
1. Selecione **[!UICONTROL Manter alterações]** para retornar à tela de regra principal
   ![Adicionar o evento de biblioteca carregada](assets/websdk-property-addEvent.png)
1. Deixe **[!UICONTROL Condições]** em branco, pois queremos que esta regra seja acionada em todas as páginas, de acordo com o nome que demos a ela
1. Em **[!UICONTROL Ações]**, selecione o botão **[!UICONTROL Adicionar]**
1. Use a **[!UICONTROL Adobe Experience Platform Web SDK]** **[!UICONTROL Extensão]** e selecione **[!UICONTROL Enviar Evento]** como o **[!UICONTROL Tipo de Ação]**
1. À direita, selecione **[!UICONTROL web.webpagedetails.pageViews]** na lista suspensa **[!UICONTROL Tipo]**. Este é um dos campos XDM em nosso `Luma Web Events Schema`
1. Selecione **[!UICONTROL Manter alterações]** para retornar à tela de regra principal
   ![Adicionar a ação Enviar Evento](assets/websdk-property-addAction.png)
1. Selecione **[!UICONTROL Salvar]** para salvar a regra\
   ![Salvar a regra](assets/websdk-property-saveRule.png)

## Publicar a regra em uma biblioteca

Em seguida, publicaremos a regra em nosso ambiente de desenvolvimento para que possamos verificar se ela funciona.

<!--
There are a few quick steps we must take in the **[!UICONTROL Publishing]** section of Launch.


### Create a host

Launch libraries can be hosted on Adobe's Content Delivery Network (CDN) or on your own servers. In this tutorial, we will use Adobe's CDN since it is faster to set up:

1. Go to **[!UICONTROL Hosts]** in the left navigation
1. Select the **[!UICONTROL Create New Host]** button
    ![Create a new host](assets/websdk-property-createHost.png)   
1. For the **[!UICONTROL Name]**, enter `Adobe CDN`
1. For the **[!UICONTROL Type]**, select **[!UICONTROL Managed by Adobe]**
1. Select the **[!UICONTROL Save]** button to complete the setup of the host
    ![Configure the host](assets/websdk-property-hostDetails.png)   

### Create an environment

Environments allow you to have different versions of a library in different publishing environments to accommodate your publishing workflow. For example, the fully tested version of your library can be published to a Production environment, while new changes are being created in a Development environment. You can also use different hosts for each environment. To create an environment:

1. Go to **[!UICONTROL Environments]** in the left navigation
1. Select the **[!UICONTROL Create New Environment]** button
    ![Create a new environment](assets/websdk-property-createEnvironment.png) 
1. Under **[!UICONTROL Development]** select **[!UICONTROL Select]**   
    ![Select the environment type](assets/websdk-property-selectEnvironment.png) 
1. For the **[!UICONTROL Name]**, enter `Development`
1. For the **[!UICONTROL Select Host]** dropdown, select `Adobe CDN`
1. Select the **[!UICONTROL Save]** button to complete the setup of the environment
    ![Configure the environment](assets/websdk-property-configureEnv.png)
1. You will see a modal with URL and other implementation details of this library. These are critical for a real Launch implementation, but we don't need to worry about them for this tutorial. Select the **[!UICONTROL Close]** button to exit the modal.

### Create and publish the library

Now let's bundle the contents of our property&mdash;currently an extension and a rule&mdash;into a library. 
-->

Para criar uma biblioteca:

1. Vá para **[!UICONTROL Fluxo de Publicação]** na navegação à esquerda
1. Selecione **[!UICONTROL Adicionar biblioteca]**
   ![Selecione Adicionar Biblioteca](assets/websdk-property-pubAddNewLib.png)
1. Para o **[!UICONTROL Nome]**, digite `Luma Platform Tutorial`
1. Para o **[!UICONTROL Ambiente]**, selecione `Development`
1. Selecione o botão **[!UICONTROL Adicionar todos os recursos alterados]**. (Além da extensão [!UICONTROL Adobe Experience Platform Web SDK] e da regra `All Pages - Library Loaded`, você também verá a extensão [!UICONTROL Core] adicionada, que contém a base do JavaScript exigida por todas as propriedades da Web do Launch.)
1. Selecione o botão **[!UICONTROL Salvar e criar para desenvolvimento]**
   ![Criar e criar a biblioteca](assets/websdk-property-buildLibrary.png)

A biblioteca pode levar alguns minutos para ser criada e, quando estiver concluída, exibirá um ponto verde à esquerda do nome da biblioteca:
![Compilação concluída](assets/websdk-property-buildComplete.png)

Como você pode ver na tela [!UICONTROL Fluxo de publicação], há muito mais no processo de publicação, que está além do escopo deste tutorial. Vamos usar uma única biblioteca em nosso ambiente de desenvolvimento.

## Validar os dados na solicitação

### Adicionar o Adobe Experience Platform Debugger

O Experience Platform Debugger é uma extensão disponível para o Chrome que ajuda a visualizar a tecnologia Adobe implementada nas páginas da Web. Baixe a versão do seu navegador de preferência:

* [Extensão do Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Se você nunca usou o Debugger antes (e este é diferente do Adobe Experience Cloud Debugger mais antigo), assista a este vídeo de visão geral de cinco minutos:

>[!VIDEO](https://video.tv.adobe.com/v/32156?learn=on&enablevpops)

### Abra o site Luma

Para este tutorial, usamos uma versão hospedada publicamente do site de demonstração do Luma. Vamos abri-lo e marcá-lo:

1. Em uma nova guia do navegador, abra o [site da Luma](https://newluma.enablementadobe.com).
1. Marque a página para uso no restante do tutorial

Este site hospedado explica por que usamos `enablementadobe.com` no campo [!UICONTROL Domínios] de nossa configuração inicial de propriedade de tag e por que usamos `data.enablementadobe.com` como nosso domínio próprio na extensão do [!UICONTROL Adobe Experience Platform Web SDK]. Veja, eu tinha um plano!

![Página inicial do Luma](assets/websdk-luma-homepage.png)

### Use o Experience Platform Debugger para mapear para a propriedade da tag

O Experience Platform Debugger tem um recurso interessante que permite substituir uma propriedade de tag existente por outra. Isso é útil para validação e permite ignorar muitas etapas de implementação neste tutorial.

1. Verifique se o site Luma está aberto e selecione o ícone da extensão do Experience Platform Debugger
1. O Debugger abrirá e mostrará alguns detalhes da implementação codificada, que não está relacionada a este tutorial (talvez seja necessário recarregar o site Luma depois de abrir o Debugger)
1. Confirme se o Depurador está &quot;**[!UICONTROL Conectado ao Luma]**&quot;, como mostrado abaixo, e selecione o ícone &quot;**[!UICONTROL bloquear]**&quot; para bloquear o Depurador no site Luma.
1. Selecione o botão **[!UICONTROL Entrar]** na parte superior direita para autenticar.
1. Agora vá para **[!UICONTROL Launch]** na navegação à esquerda
1. Selecione a guia Configuração
1. À direita do local onde ele mostra os **[!UICONTROL Códigos incorporados de página]**, abra a lista suspensa **[!UICONTROL Ações]** e selecione **[!UICONTROL Substituir]**
   ![Selecionar ações > Substituir](assets/websdk-debugger-replaceLibrary.png)
1. Como você está autenticado, o Debugger extrairá suas propriedades e ambientes disponíveis do Launch. Selecione sua propriedade `Luma Platform Tutorial`
1. Selecione seu ambiente `Development`
1. Selecione o botão **[!UICONTROL Aplicar]**
   ![Selecione a propriedade de marca alternativa](assets/websdk-debugger-selectProperty.png)
1. O site Luma recarregará agora _com sua propriedade de marca_. Socorro, fui hackeado! Brincadeira.
   ![propriedade de marca substituída](assets/websdk-debugger-propertyReplaced.png)
1. Vá para **[!UICONTROL Resumo]** na navegação à esquerda para ver os detalhes da sua propriedade [!UICONTROL Inicialização]
   ![Guia Resumo](assets/websdk-debugger-summary.png)
1. Agora vá para **[!UICONTROL AEP Web SDK]** na navegação à esquerda para ver as **[!UICONTROL Solicitações de Rede]**
1. Abrir a linha **[!UICONTROL eventos]**

   ![Solicitação do Adobe Experience Platform Web SDK](assets/websdk-debugger-platformNetwork.png)
1. Observe como podemos ver o tipo de evento `web.webpagedetails.pageView` que especificamos na ação [!UICONTROL Enviar Evento] e outras variáveis prontas para uso que seguem o formato `AEP Web SDK ExperienceEvent Mixin`
   ![Detalhes do evento](assets/websdk-debugger-eventDetails.png)
1. Esses tipos de detalhes de solicitação também estão visíveis na guia **Rede** das ferramentas de desenvolvedor da Web do navegador. Abra-o e recarregue a página. Filtre chamadas com `interact` para localizar a chamada, selecioná-la e procurar na guia **Cabeçalhos**, área **Carga da solicitação**.
   ![Guia Rede](assets/websdk-debugger-networkTab.png)
1. Vá para a guia **Resposta** e observe como o valor da ECID é incluído na resposta. Copie esse valor como você o usará para validar as informações do perfil no próximo exercício.
   ![Guia Rede](assets/websdk-debugger-networkTab-response.png)



## Validar os dados no Experience Platform

Você pode validar se os dados estão chegando na Platform observando os lotes de dados que chegam no `Luma Web Events Dataset`. (Eu sei, é chamada de assimilação de dados por transmissão, mas agora estou dizendo que chega em lotes!) Ele flui em tempo real para o Perfil, para que possa ser usado para segmentação e ativação em tempo real, mas é enviado em lotes a cada 15 minutos para o data lake.)

Para validar os dados:

1. Na interface do usuário da Platform, acesse **[!UICONTROL Conjuntos de dados]** na navegação à esquerda
1. Abra o `Luma Web Events Dataset` e confirme se um lote chegou. Lembre-se de que elas são enviadas a cada 15 minutos, portanto, talvez seja necessário aguardar até que o lote seja exibido.
1. Selecione o botão **[!UICONTROL Visualizar conjunto de dados]**
   ![Abrir o conjunto de dados](assets/websdk-platform-dataset.png)
1. Na modal de visualização, observe como é possível selecionar diferentes campos do esquema à esquerda para visualizar esses pontos de dados específicos:
   ![Visualizar os campos](assets/websdk-platform-datasetPreview.png)

Você também pode confirmar que o novo perfil está aparecendo:

1. Na interface do usuário da Platform, vá para **[!UICONTROL Perfis]** na navegação à esquerda
1. Selecione o namespace **[!UICONTROL ECID]** e procure seu valor de ECID (copie-o da resposta. O perfil terá sua própria ID, separada da ECID.
1. Selecione a **[!UICONTROL ID do Perfil]** para abrir o perfil
   ![Localizar e abrir o perfil](assets/websdk-platform-openProfile.png)
1. Selecione a guia **[!UICONTROL Eventos]** para ver as páginas que você visualizou
   ![Eventos de Perfil](assets/websdk-platform-profileEvents.png)\
   <!--![](assets/websdk-platform-confirmProfile.png)-->

## Adicionar dados personalizados ao evento

### Criar um elemento de dados para o nome da página

1. Na interface das marcas da Coleção de Dados, no canto superior direito da propriedade `Luma Platform Tutorial`, abra a lista suspensa **[!UICONTROL Selecionar uma Biblioteca de Trabalho]** e selecione sua biblioteca `Luma Platform Tutorial`. Essa configuração facilita a publicação de atualizações adicionais na nossa biblioteca.
1. Agora vá para **[!UICONTROL Elementos de dados]** na navegação à esquerda
1. Selecione o botão **[!UICONTROL Criar novo elemento de dados]**

   ![Criar um novo elemento de dados](assets/websdk-property-createNewDataElement.png)
1. Como o **[!UICONTROL Nome]**, digite `Page Name`
1. Como o **[!UICONTROL Tipo de Elemento de Dados]**, selecione `JavaScript Variable`
1. Como o **[!UICONTROL nome da variável do JavaScript]**, digite `digitalData.page.pageInfo.pageName`
1. Para ajudar a padronizar o formato dos valores, marque as caixas para **[!UICONTROL Forçar valor de minúsculas]** e **[!UICONTROL Limpar texto]**
1. Verifique se `Luma Platform Tutorial` está selecionado como a biblioteca de trabalho
1. Selecione **[!UICONTROL Salvar na biblioteca]**
   ![Criar um elemento de dados para o nome da página](assets/websdk-property-dataElement-pageName.png)

### Mapear o nome da página para o elemento de dados Objeto XDM

Agora mapearemos nosso nome de página para o Web SDK.

>[!IMPORTANT]
>
>Para concluir essa tarefa, precisamos garantir que seu usuário primeiro tenha acesso à sandbox de produção. Se você ainda não tiver acesso à sandbox de Produção de um perfil de produto diferente, abra rapidamente seu perfil do `Luma Tutorial Platform` e adicione o item de permissão **[!UICONTROL Sandboxes]** > **[!UICONTROL Prod]**. Depois de fazer isso, faça um SHIFT-Reload na página Elementos de dados para limpar seu cache
>![Adicionar a sandbox de produção](assets/websdk-property-permissionToLoadSchema.png)

Na página **[!UICONTROL Elementos de Dados]**:

1. Criar um novo elemento de dados
1. Como o **[!UICONTROL Nome]**, digite `XDM Object`
1. Como a **[!UICONTROL Extensão]**, selecione `Adobe Experience Platform Web SDK`
1. Como o **[!UICONTROL Tipo de Elemento de Dados]**, selecione `XDM object`
1. Como a **[!UICONTROL Sandbox]**, selecione sua `Luma Tutorial` sandbox
1. Como o **[!UICONTROL Esquema]**, selecione seu `Luma Web Events Schema`
1. Selecionar o campo `web.webPageDetails.name`
1. Como o **[!UICONTROL Valor]**, selecione o ícone para abrir a modal de seleção de elemento de dados e escolha seu `Page Name` elemento de dados
1. Selecione **[!UICONTROL Salvar na biblioteca]**
   ![Mapear o nome da página para o elemento de dados Objeto XDM](assets/websdk-property-dataElement-createXDMObject.png)

Esse mesmo processo é usado para mapear dados personalizados adicionais em seu site para campos XDM.

### Adicionar os dados XDM à sua ação Enviar evento

Agora que você tem dados mapeados para campos XDM, é possível incluí-los na ação Enviar evento:

1. Vá para a tela **[!UICONTROL Regras]**
1. Abra sua regra do `All Pages - Library Loaded`
1. Abrir a ação `Adobe Experience Platform Web SDK - Send Event`
1. Como os **[!UICONTROL dados XDM]**, selecione o ícone para abrir a modal de seleção de elemento de dados e escolha seu `XDM Object` elemento de dados
1. Selecione o botão **[!UICONTROL Manter alterações]**
   ![Adicionar os dados XDM à sua ação Enviar Evento](assets/websdk-property-addXDMtoSendEvent.png)
1. Agora, como você selecionou o `Luma Platform Tutorial` como sua biblioteca de trabalho para os últimos exercícios, as alterações recentes foram salvas diretamente na biblioteca. Em vez de ter que publicar nossas alterações por meio da tela Fluxo de publicação, você pode abrir a lista suspensa no botão azul e selecionar **[!UICONTROL Salvar na biblioteca e criar]**
   ![Salvar na Biblioteca e na Compilação](assets/websdk-property-saveAndBuildUpdatedSendEvent.png)

Isso inicia a criação de uma nova biblioteca de tags com as três alterações que você acabou de fazer.

### Validar os dados do XDM

Agora é possível recarregar a página inicial do Luma, enquanto mapeada para a propriedade da tag usando o Debugger, como você aprendeu anteriormente, e ver que o campo de nome da página é preenchido na solicitação.
![Validar os dados XDM](assets/websdk-debugger-pageName.png)

Também é possível validar se os dados do nome da página foram recebidos na Platform, visualizando o conjunto de dados e o perfil.

## Enviar identidades adicionais

Sua implementação do Web SDK agora está enviando eventos com a Experience Cloud ID (ECID) como o identificador principal. A ECID é gerada automaticamente pelo Web SDK e é exclusiva por dispositivo e navegador. Um único cliente pode ter várias ECIDs, dependendo do dispositivo e do navegador que está usando. Então, como podemos obter uma visualização unificada desse cliente e vincular sua atividade online aos nossos dados de CRM, Fidelidade e Compra offline? Fazemos isso coletando identidades adicionais durante a sessão e vinculando determinicamente seu perfil por meio da compilação de identidade.

Lembrando que mencionei que usaríamos a ECID e a CRM Id como identidades para os dados da Web na lição [Mapear identidades](map-identities.md). Portanto, vamos coletar a ID do CRM com o Web SDK.

### Adicionar elemento de dados para a ID do CRM

Primeiro, armazenamos a ID do CRM em um elemento de dados:

1. Na interface das tags, adicione um elemento de dados chamado `CRM Id`
1. Como o **[!UICONTROL Tipo de Elemento de Dados]**, selecione **[!UICONTROL Variável JavaScript]**
1. Como o **[!UICONTROL nome da variável do JavaScript]**, digite `digitalData.user.0.profile.0.attributes.username`
1. Selecione o botão **[!UICONTROL Salvar na Biblioteca]** (`Luma Platform Tutorial` ainda deve ser sua biblioteca de trabalho)
   ![Adicionar Elemento de Dados para a Id do CRM](assets/websdk-property-dataElement-crmId.png)

### Adicionar a ID do CRM ao elemento de dados do Mapa de identidade

Agora que capturamos o valor da ID do CRM, devemos associá-lo a um tipo de elemento de dados especial chamado de elemento de dados do [!UICONTROL Mapa de identidade]:

1. Adicionar um elemento de dados chamado `Identities`
1. Como a **[!UICONTROL Extensão]**, selecione **[!UICONTROL Adobe Experience Platform Web SDK]**
1. Como o **[!UICONTROL Tipo de Elemento de Dados]**, selecione **[!UICONTROL Mapa de identidade]**
1. Como o **[!UICONTROL Namespace]**, digite `Luma CRM Id`, que é o [!UICONTROL namespace] que criamos em uma lição anterior

   >[!WARNING]
   >
   >A extensão do Adobe Experience Platform Web SDK versão 2.2 permite selecionar o Namespace em uma lista suspensa pré-preenchida usando os valores reais na conta da Platform. Infelizmente, esse recurso ainda não é &quot;sensível à sandbox&quot; e, portanto, o valor `Luma CRM Id` pode não aparecer na lista suspensa. Isso pode impedir que você conclua este exercício. Publicaremos uma solução alternativa depois de confirmada.

1. Como a **[!UICONTROL ID]**, selecione o ícone para abrir a modal de seleção de elemento de dados e escolha seu elemento de dados `CRM Id`
1. Como o **[!UICONTROL Estado autenticado]**, selecione **[!UICONTROL Autenticado]**
1. Verificar **[!UICONTROL Primário]**

   >[!TIP]
   >
   > A Adobe recomenda enviar identidades que representem uma pessoa, como `Luma CRM Id`, como a identidade [!UICONTROL principal].
   >
   > Se o mapa de identidade contiver o identificador de pessoa (por exemplo, `Luma CRM Id`), o identificador de pessoa se tornará a identidade [!UICONTROL principal]. Caso contrário, `ECID` se tornará a identidade [!UICONTROL primária].

1. Selecione o botão **[!UICONTROL Salvar na Biblioteca]** (`Luma Platform Tutorial` ainda deve ser sua biblioteca de trabalho)
   ![Adicionar a ID do CRM ao elemento de dados do Mapa de Identidade](assets/websdk-property-dataElement-identityMap.png)

>[!NOTE]
>
>Você pode passar vários identificadores usando o tipo de dados [!UICONTROL Mapa de identidade].

### Adicionar o elemento de dados do Mapa de identidade ao Objeto XDM

Há mais um elemento de dados que deve ser atualizado: o elemento de dados Objeto XDM. Pode parecer estranho ter que atualizar três elementos de dados separados para transmitir essa identidade, mas esse processo foi projetado para ser dimensionado para várias identidades. Não se preocupe, estamos quase terminando esta lição!

1. Abra o elemento de dados Objeto XDM
1. Abrir o campo XDM do IdentityMap
1. Como o **[!UICONTROL Elemento de dados]**, selecione o ícone para abrir a modal de seleção de elemento de dados e escolha seu `Identities` elemento de dados
1. Agora, como você selecionou o `Luma Platform Tutorial` como sua biblioteca de trabalho para os últimos exercícios, as alterações recentes foram salvas diretamente na biblioteca. Em vez de precisar publicar suas alterações por meio da tela Fluxo de publicação, você pode abrir a lista suspensa no botão azul e selecionar **[!UICONTROL Salvar na biblioteca e criar]**
   ![Adicionar o elemento de dados IdentityMap ao Objeto XDM](assets/websdk-property-dataElement-addIdentitiesToXDMObject.png)


### Validar a identidade

Para validar se a ID do CRM agora está sendo enviada pelo Web SDK:

1. Abra o [site da Luma](https://newluma.enablementadobe.com)
1. Mapeie-o para a propriedade de tag usando o Depurador, de acordo com as instruções anteriores
1. Selecione o link **Logon** na parte superior direita do site Luma
1. Fazer logon usando as credenciais `test@test.com`/`test`
1. Depois de autenticada, inspecione a chamada do Experience Platform Web SDK no Depurador (**[!UICONTROL Adobe Experience Platform Web SDK]** > **[!UICONTROL Solicitações de Rede]** > **[!UICONTROL eventos]** da solicitação mais recente) e você deverá ver o `lumaCrmId`:
   ![Validar a identidade no Depurador](assets/websdk-debugger-confirmIdentity.png)
1. Procure o perfil de usuário usando o namespace e o valor da ECID novamente. No perfil, você verá a ID do CRM e também a ID de fidelidade, além dos detalhes do perfil, como o nome e o número de telefone. Todas as identidades e dados foram compilados em um único perfil do cliente em tempo real!
   ![Validar a identidade na Platform](assets/websdk-platform-lumaCrmIdProfile.png)


## Recursos adicionais

* [Implementar a Adobe Experience Cloud com o SDK da Web](/help/tutorial-web-sdk/overview.md)
* [Documentação de assimilação de streaming](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=pt-BR)
* [Referência da API de assimilação de fluxo](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)

Excelente trabalho! Havia muitas informações sobre o Web SDK e o Launch. Há muito mais envolvido em uma implementação completa, mas essas são as noções básicas para ajudar você a começar e ver os resultados na Platform.

>[!NOTE]
>
>Agora que você concluiu a lição Assimilação de streaming, pode remover a sandbox [!UICONTROL Prod] do seu perfil de produto `Luma Tutorial Platform`


Engenheiros de dados, se desejar, podem pular para a [lição executar consultas](run-queries.md).

Arquitetos de dados, você pode seguir para [políticas de mesclagem](create-merge-policies.md)!
