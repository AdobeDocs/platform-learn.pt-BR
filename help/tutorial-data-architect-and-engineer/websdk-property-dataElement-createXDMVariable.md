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
source-git-commit: 45fec5b2a82e12bdc4a9d017664e8c11d5625cef
workflow-type: tm+mt
source-wordcount: '2966'
ht-degree: 0%

---

# Assimilar dados de transmissão

<!--1hr-->

Nesta lição, você transmitirá dados usando o Adobe Experience Platform Web SDK.

>[!WARNING]
>
> O site do Luma usado neste tutorial deve ser substituído durante a semana de 16 de fevereiro de 2026. O trabalho realizado como parte deste tutorial pode não se aplicar ao novo site.

Há duas tarefas principais: coleta de dados

* Implemente o Web SDK no site Luma para transmitir eventos do cliente para o Experience Platform Edge Network.

* Configure uma sequência de dados para que a Edge Network encaminhe os dados para nosso `Luma Web Events Dataset` no Experience Platform.

**Os engenheiros de dados** precisarão assimilar dados de transmissão fora deste tutorial. Embora os desenvolvedores da Web normalmente implementem o Web SDK em um site, é importante saber como o processo funciona. Mesmo se você não for um desenvolvedor da Web, deverá ser capaz de concluir essa implementação básica.

Antes de começar os exercícios, assista a estes dois pequenos vídeos para saber mais sobre a assimilação de dados por transmissão e o Web SDK:

>[!VIDEO](https://video.tv.adobe.com/v/28425?learn=on&enablevpops)

>[!VIDEO](https://video.tv.adobe.com/v/34141?learn=on&enablevpops)

>[!NOTE]
>
>Embora este tutorial se concentre na assimilação por transmissão de sites com o Web SDK, você também pode transmitir dados usando o [SDK Móvel](https://experienceleague.adobe.com/pt-br/docs/platform-learn/implement-mobile-sdk/overview), a [API do Edge Network Server](https://experienceleague.adobe.com/pt-br/docs/platform-learn/data-collection/server-api/overview) e a [API HTTP](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/connectors/streaming/http).

## Permissões necessárias

Na lição [Configurar Permissões](configure-permissions.md), você configura todos os controles de acesso necessários para concluir esta lição.


## Configurar o fluxo de dados

Primeiro, configuraremos o fluxo de dados. Um fluxo de dados informa ao Experience Platform Edge Network para onde enviar os dados depois de recebê-los da chamada do Web SDK. Por exemplo, deseja enviar os dados para o Experience Platform, Adobe Analytics ou Adobe Target?

![Web SDK, sequências de dados e diagrama do Edge Network](assets/dc-websdk-datastreams.png)

Para criar sua [!UICONTROL sequência de dados]:

1. Verifique se você ainda está na sandbox ` Luma Tutorial`
1. Selecione **[!UICONTROL Datastreams]** na navegação à esquerda
1. Selecione o botão **[!UICONTROL Nova sequência de dados]** no canto superior direito

   ![Selecionar sequências de dados na navegação à esquerda](assets/websdk-datastream-newDatastream.png)


1. Para o **[!UICONTROL Nome]**, digite `Luma Platform Tutorial` (adicione seu nome ao final, se várias pessoas da sua empresa estiverem fazendo este tutorial)
1. Selecione o botão **[!UICONTROL Salvar]**

   ![Nomeie o datastram e salve](assets/websdk-datastream-name.png)

Quando os dados chegam à Edge, o [!UICONTROL Datastream] encaminha-os para os [!UICONTROL Serviços] configurados. Para enviar dados ao Experience Platform:

1. Selecione **[!UICONTROL Adicionar Serviço]**
   ![Adicionar Serviço](assets/websdk-datastream-addService.png)

1. Selecionar `Adobe Experience Platform`
1. Selecione seu `Luma Web Events Dataset`
1. Selecione **[!UICONTROL Salvar]**

   ![Selecione seu conjunto de dados e salve](assets/websdk-datastream-addPlatformService.png)

Embora haja uma opção de Conjunto de dados de perfil na configuração da sequência de dados, ela não deve ser usada para enviar dados normais do Perfil individual XDM para a Plataforma. Essa configuração só deve ser usada para enviar consentimento, token de push e detalhes da região de atividade do usuário.

As caixas de seleção para [!UICONTROL Offer Decisioning], [!UICONTROL Segmentação do Edge], [!UICONTROL Destinos do Personalization] e [!UICONTROL Adobe Journey Optimizer] permitem ativar dados no Edge, mas não são usadas neste tutorial.

## Implementar o Web SDK

### Adicionar uma propriedade do

Primeiro, devemos criar uma propriedade de tag (anteriormente uma propriedade de tag ). Uma propriedade é um container para todas as JavaScript, regras e outros recursos necessários para coletar detalhes de uma página da Web e enviá-los para vários locais.

Para criar uma propriedade:

1. Vá para **[!UICONTROL Tags]** na navegação à esquerda
1. Selecionar **[!UICONTROL Nova Propriedade]**
   ![Adicionar uma nova propriedade](assets/websdk-property-addNewProperty.png)
1. Como o **[!UICONTROL Nome]**, digite `Luma Platform Tutorial` (adicione seu nome ao final, se várias pessoas da sua empresa estiverem fazendo este tutorial)
1. Como os **[!UICONTROL Domínios]**, digite `enablementadobe.com` (explicado mais tarde)
1. Selecione **[!UICONTROL Salvar]**
   ![Detalhes da propriedade](assets/websdk-property-propertyDetails.png)


### Adicionar extensões à propriedade

Agora que você tem uma propriedade, é possível adicionar o Web SDK usando uma extensão. Uma extensão é um pacote de códigos que adiciona funcionalidade à propriedade e à implementação da tag. Para adicionar a extensão:

1. Abra a propriedade da tag
1. Vá para **[!UICONTROL Extensões]** na navegação à esquerda
1. Vá para a guia **[!UICONTROL Catálogo]**
1. Há muitas extensões disponíveis para tags. Filtrar o catálogo com o termo `Web SDK`
1. Selecione a extensão **[!UICONTROL Adobe Experience Platform Web SDK]** para abrir o painel lateral
1. Selecione o botão **[!UICONTROL Instalar]**
   ![Instalar a extensão Adobe Experience Platform Web SDK](assets/websdk-property-addExtension.png)
1. Há várias configurações disponíveis para a extensão Web SDK, mas há apenas duas que vamos configurar para este tutorial. Atualize o **[!UICONTROL Domínio do Edge]** para `data.enablementadobe.com`. Essa configuração permite definir cookies primários com a implementação do Web SDK, o que é incentivado. Ao implementar o Web SDK em seu próprio site, recomendamos criar um CNAME para fins de coleta de dados, por exemplo, `data.YOUR_DOMAIN.com`
1. Na seção **[!UICONTROL Sequências de dados]**, para o Ambiente de produção, selecione a sandbox do `Luma Tutorial` e a sequência de dados do `Luma Platform Tutorial`.
1. Fique à vontade para ver as outras opções de configuração (mas não as altere!) e selecione **[!UICONTROL Salvar]**
   ![Configurar a extensão do Web SDK](assets/websdk-property-configureExtension.png)

Na tela Catálogo de extensões, instale a extensão Camada de dados do cliente Adobe. Essa extensão nos ajudará a ler a camada de dados do site Luma:

![Instalar a extensão da Camada de Dados do Cliente Adobe](assets/websdk-property-installACDLExtension.png)

Nenhuma configuração é necessária na extensão, portanto, salve-a na biblioteca.

## Criar uma regra para enviar dados

Agora criaremos uma regra para enviar dados para a Platform. Uma regra é uma combinação de eventos, condições e ações que instruem as tags a fazer algo. Para criar uma regra:

1. Navegue até **[!UICONTROL Regras]**
1. Selecione o botão **[!UICONTROL Criar nova regra]**
   ![Criar uma regra](assets/websdk-property-createRule.png)
1. Atribua um nome à regra `adobeDataLayer event`
1. Em **[!UICONTROL Eventos]**, selecione o botão **[!UICONTROL Adicionar]**
   ![Nomear a regra e adicionar um evento](assets/websdk-property-nameRule.png)
1. Use a **[!UICONTROL Extensão]** da **[!UICONTROL Camada de Dados do Cliente da Adobe]** e selecione **[!UICONTROL Dados Enviados por Push]** como o **[!UICONTROL Tipo de Evento]**.
1. Selecione **[!UICONTROL Ouvir]**. **[!UICONTROL Todos os eventos]**.
1. Selecione **[!UICONTROL Manter alterações]** para retornar à tela de regra principal
   ![Adicionar o evento de biblioteca carregada](assets/websdk-property-addEvent.png)
1. Em **[!UICONTROL Ações]**, selecione o botão **[!UICONTROL Adicionar]**
1. Use a **[!UICONTROL Adobe Experience Platform Web SDK]** **[!UICONTROL Extensão]** e selecione **[!UICONTROL Enviar Evento]** como o **[!UICONTROL Tipo de Ação]**
1. À direita, selecione **[!UICONTROL Exibições de página de detalhes da página da Web]** na lista suspensa **[!UICONTROL Tipo]**. Isso preenche o campo eventType de nosso `Luma Web Events Schema`
1. Selecione **[!UICONTROL Manter alterações]** para retornar à tela de regra principal
   ![Adicionar a ação Enviar Evento](assets/websdk-property-addAction.png)
1. Selecione **[!UICONTROL Salvar]** para salvar a regra\
   ![Salvar a regra](assets/websdk-property-saveRule.png)

## Publicar a regra em uma biblioteca

Em seguida, publicaremos a regra em nosso ambiente de desenvolvimento para que possamos verificar se ela funciona.


Para criar uma biblioteca:

1. Vá para **[!UICONTROL Fluxo de Publicação]** na navegação à esquerda
1. Selecione **[!UICONTROL Adicionar biblioteca]**
   ![Selecione Adicionar Biblioteca](assets/websdk-property-pubAddNewLib.png)
1. Para o **[!UICONTROL Nome]**, digite `Luma Platform Tutorial`
1. Para o **[!UICONTROL Ambiente]**, selecione `Development`
1. Selecione o botão **[!UICONTROL Adicionar todos os recursos alterados]**. (Além da extensão [!UICONTROL Adobe Experience Platform Web SDK] e da regra `adobeDataLayer event`, você também verá a extensão [!UICONTROL Core] adicionada, que contém a base do JavaScript exigida por todas as propriedades da Web de marcas.)
1. Selecione o botão **[!UICONTROL Salvar e criar para desenvolvimento]**
   ![Criar e criar a biblioteca](assets/websdk-property-buildLibrary.png)

A biblioteca pode levar alguns minutos para ser criada e, quando estiver concluída, exibirá um ponto verde à esquerda do nome da biblioteca:
![Compilação concluída](assets/websdk-property-buildComplete.png)

Como você pode ver na tela [!UICONTROL Fluxo de publicação], há muito mais no processo de publicação, que está além do escopo deste tutorial. Vamos usar uma única biblioteca em nosso ambiente de desenvolvimento.

## Validar os dados na solicitação

### Adicionar o Adobe Experience Platform Debugger

O Experience Platform Debugger é uma extensão disponível para o Chrome que ajuda a visualizar a tecnologia Adobe implementada nas páginas da Web. Baixe a versão do seu navegador de preferência:

* [Extensão do Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Se você nunca usou o Debugger antes, assista a este vídeo de visão geral de cinco minutos:

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
1. Agora vá para **[!UICONTROL Tags do Experience Platform]** na navegação à esquerda
1. Selecione a guia Configuração
1. À direita do local onde ele mostra os **[!UICONTROL Códigos incorporados de página]**, abra a lista suspensa **[!UICONTROL Ações]** e selecione **[!UICONTROL Substituir]**
   ![Selecionar ações > Substituir](assets/websdk-debugger-replaceLibrary.png)
1. Como você está autenticado, o Debugger extrairá suas propriedades e ambientes de tag disponíveis. Selecione sua propriedade `Luma Platform Tutorial`
1. Selecione seu ambiente `Development`
1. Selecione o botão **[!UICONTROL Aplicar]**
   ![Selecione a propriedade de marca alternativa](assets/websdk-debugger-selectProperty.png)
1. O site Luma recarregará agora _com sua propriedade de marca_.
   ![propriedade de marca substituída](assets/websdk-debugger-propertyReplaced.png)
1. Vá para **[!UICONTROL Resumo]** na navegação à esquerda para ver os detalhes da propriedade [!UICONTROL tag]
   ![Guia Resumo](assets/websdk-debugger-summary.png)
1. Agora vá para **[!UICONTROL Experience Platform Web SDK]** na navegação à esquerda para ver as **[!UICONTROL Solicitações de Rede]**
1. Selecionar a linha **[!UICONTROL eventos]**

   ![Solicitação do Adobe Experience Platform Web SDK](assets/websdk-debugger-platformNetwork.png)

1. Observe como podemos ver o tipo de evento `web.webpagedetails.pageView` especificado em nossa ação [!UICONTROL Enviar Evento]
   ![Solicitação do Adobe Experience Platform Web SDK](assets/websdk-debugger-eventDetails.png)


1. Os detalhes da solicitação também estão visíveis na guia **Rede** das ferramentas do desenvolvedor da Web do navegador. Abra-o e recarregue a página. Filtre chamadas com `interact` para localizar a chamada, selecioná-la e procurar na guia **Cabeçalhos**, área **Carga da solicitação**.
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

O Web SDK preenche muitos campos XDM automaticamente, mas é inevitável personalizar a implementação para coletar campos adicionais do site. Isso se torna muito complexo, mas aqui estão alguns exemplos simples.

### Criar um elemento de dados para armazenar dados XDM

1. Navegue de volta para a propriedade da tag `Luma Platform Tutorial`
1. Abra a lista suspensa **[!UICONTROL Selecionar uma Biblioteca de Trabalho]** e selecione sua biblioteca `Luma Platform Tutorial`. Essa configuração facilita a publicação de atualizações adicionais na nossa biblioteca.
1. Agora vá para **[!UICONTROL Elementos de dados]** na navegação à esquerda
1. Selecione o botão **[!UICONTROL Criar novo elemento de dados]**

   ![Criar um novo elemento de dados](assets/websdk-property-createNewDataElement.png)

Na página **[!UICONTROL Elementos de Dados]**:


1. Como o **[!UICONTROL Nome]**, digite `XDM data`
1. Como a **[!UICONTROL Extensão]**, selecione `Adobe Experience Platform Web SDK`
1. Como o **[!UICONTROL Tipo de Elemento de Dados]**, selecione `Variable`
1. Como a **[!UICONTROL Sandbox]**, selecione sua `Luma Tutorial` sandbox
1. Como o **[!UICONTROL Esquema]**, selecione seu `Luma Web Events Schema`
1. Verifique se `Luma Platform Tutorial` está selecionado como a biblioteca de trabalho
1. Selecione **[!UICONTROL Salvar na biblioteca]**
   ![Mapear o nome da página para o elemento de dados Objeto XDM](assets/websdk-property-dataElement-createXDMVariable.png)

### Criar um elemento de dados para o nome da página

1. Criar um novo elemento de dados
1. Como o **[!UICONTROL Nome]**, digite `Page Name`
1. Como o **[!UICONTROL Tipo de Elemento de Dados]**, selecione `JavaScript Variable`
1. Como o **[!UICONTROL nome da variável do JavaScript]**, digite `adobeDataLayer.0.page.name`
1. Para ajudar a padronizar o formato dos valores, marque as caixas para **[!UICONTROL Forçar valor de minúsculas]** e **[!UICONTROL Limpar texto]**
1. Selecione **[!UICONTROL Salvar na biblioteca]**
   ![Criar um elemento de dados para o nome da página](assets/websdk-property-dataElement-pageName.png)


### Adicionar os dados XDM à sua ação Enviar evento

Agora que você tem dados mapeados para campos XDM, é possível incluí-los na ação Enviar evento:

1. Vá para a tela **[!UICONTROL Regras]**
1. Abra sua regra do `adobeDataLayer event`
1. Abrir a ação `Adobe Experience Platform Web SDK - Send Event`
1. Como o **[!UICONTROL XDM]**, selecione o ícone para abrir a modal de seleção de elemento de dados e escolha seu `XDM data` elemento de dados
1. Selecione **[!UICONTROL Manter alterações]**
   ![Adicionar os dados XDM à sua ação Enviar Evento](assets/websdk-property-addXDMtoSendEvent.png)

1. Adicionar uma nova ação à regra
1. Selecione a `Adobe Experience Platform Web SDK` **[!UICONTROL Extensão]**
1. Selecione o `Update Variable` **[!UICONTROL Tipo de ação]**
1. Popular seu elemento de dados `Page Name` como `web.webPageDetails.name`
1. Selecione **[!UICONTROL Manter alterações]**
   ![Adicionar a ação Atualizar Variável à sua regra](assets/websdk-property-addUpdateVariableAction.png)

1. Reorganize as [!UICONTROL Ações] para que a [!UICONTROL Variável de atualização] seja acionada antes do [!UICONTROL Enviar evento]
1. Agora, como você selecionou o `Luma Platform Tutorial` como sua biblioteca de trabalho para os últimos exercícios, as alterações recentes foram salvas diretamente na biblioteca. Em vez de ter que publicar nossas alterações por meio da tela Fluxo de publicação, você pode abrir a lista suspensa e selecionar **[!UICONTROL Salvar na biblioteca e criar]**
   ![Salvar na Biblioteca e na Compilação](assets/websdk-property-saveAndBuildUpdatedSendEvent.png)

Isso inicia a criação de uma nova biblioteca de tags com as três alterações que você acabou de fazer.

### Validar os dados do XDM

Agora é possível recarregar a página inicial do Luma, enquanto mapeada para a propriedade da tag usando o Debugger, como você aprendeu anteriormente, e ver que o campo de nome da página é preenchido na solicitação.
![Validar os dados XDM](assets/websdk-debugger-pageName.png)

Também é possível validar se os dados do nome da página foram recebidos na Platform, visualizando o conjunto de dados e o perfil.

## Enviar identidades adicionais

Sua implementação do Web SDK agora está enviando eventos com a Experience Cloud ID (ECID) como o identificador principal. A ECID é gerada automaticamente pelo Web SDK e é exclusiva por dispositivo e navegador. Um único cliente pode ter várias ECIDs, dependendo do dispositivo e do navegador que está usando. Então, como podemos obter uma visualização unificada desse cliente e vincular sua atividade online aos nossos dados de CRM, Fidelidade e Compra offline? Fazemos isso coletando identidades adicionais durante a sessão e permitindo que o Serviço de identidade as vincule deterministicamente.

Lembrando que mencionei que usaríamos a ECID e a CRM Id como identidades para os dados da Web na lição [Mapear identidades](map-identities.md). Portanto, vamos coletar a ID do CRM com o Web SDK.

### Adicionar elemento de dados para a ID do CRM

Primeiro, armazenamos a ID do CRM em um elemento de dados:

1. Na interface das tags, adicione um elemento de dados chamado `CRM Id`
1. Como o **[!UICONTROL Tipo de Elemento de Dados]**, selecione **[!UICONTROL Variável JavaScript]**
1. Como o **[!UICONTROL nome da variável do JavaScript]**, digite `adobeDataLayer.0.user.id`
1. Selecione o botão **[!UICONTROL Salvar na Biblioteca]** (`Luma Platform Tutorial` ainda deve ser sua biblioteca de trabalho)
   ![Adicionar Elemento de Dados para a Id do CRM](assets/websdk-property-dataElement-crmId.png)

### Adicionar a ID do CRM ao elemento de dados do Mapa de identidade

Agora que capturamos o valor da ID do CRM, devemos associá-lo a um tipo de elemento de dados especial chamado de elemento de dados do [!UICONTROL Mapa de identidade]:

1. Adicionar um elemento de dados chamado `Identity Map`
1. Como a **[!UICONTROL Extensão]**, selecione **[!UICONTROL Adobe Experience Platform Web SDK]**
1. Como o **[!UICONTROL Tipo de Elemento de Dados]**, selecione **[!UICONTROL Mapa de identidade]**
1. Como o **[!UICONTROL Namespace]**, selecione ou digite `Luma CRM Id`, que é o [!UICONTROL namespace] que criamos em uma lição anterior.

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

### Adicionar o elemento de dados do Mapa de identidade à variável XDM

Agora, devemos atualizar a ação Variável XDM em nossa Regra para incluir o Mapa de identidade. Não se preocupe, estamos quase terminando esta lição!

1. Abra sua regra do `adobeDataLayer event`
1. Abrir a ação `Update variable`
1. Selecione o elemento de dados `Identity Map` para o campo XDM `identityMap`.
1. Selecione **[!UICONTROL Manter alterações]**
   ![Adicionar o elemento de dados IdentityMap ao Objeto XDM](assets/websdk-property-dataElement-addIdentitiesToXDMVariable.png)
1. Como você selecionou `Luma Platform Tutorial` como sua biblioteca de trabalho para os últimos exercícios, selecione **[!UICONTROL Salvar na biblioteca e criar]**

   ![Salvar e criar a biblioteca](assets/websdk-property-saveAndBuild.png)

<!--U1770721295408-->

### Validar a identidade

Para validar se a ID do CRM agora está sendo enviada pelo Web SDK:

1. Abra o [site da Luma](https://luma.enablementadobe.com/content/luma/us/en.html)
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

Excelente trabalho! Havia muitas informações sobre a Web SDK e tags. Há muito mais envolvido em uma implementação completa, mas essas são as noções básicas para ajudar você a começar e ver os resultados na Platform.

>[!NOTE]
>
>Agora que você concluiu a lição Assimilação de streaming, pode remover a sandbox [!UICONTROL Prod] do seu perfil de produto `Luma Tutorial Platform`


Engenheiros de dados, se desejar, podem pular para a [lição executar consultas](run-queries.md).

Arquitetos de dados, você pode seguir para [políticas de mesclagem](create-merge-policies.md)!
