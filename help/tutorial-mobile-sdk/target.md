---
title: Realizar testes A/B em aplicativos móveis com Target e Platform Mobile SDK
description: Saiba como usar um teste A/B do Target no aplicativo móvel com o Platform Mobile SDK e o Adobe Target.
solution: Data Collection,Target
feature-set: Target
feature: A/B Tests
jira: KT-14641
exl-id: 87546baa-2d8a-4cce-b531-bec3782d2e90
source-git-commit: 4c9ac30ecc0f41b7d6cd9a6653bca50e602cbc13
workflow-type: tm+mt
source-wordcount: '1746'
ht-degree: 1%

---

# Otimizar e personalizar com o Adobe Target

Saiba como otimizar e personalizar as experiências em seus aplicativos móveis com o Platform Mobile SDK e o Adobe Target.

O Target fornece tudo o que você precisa para ajustar e personalizar as experiências dos clientes. O Target ajuda a maximizar a receita em sites da Web e para dispositivos móveis, aplicativos, mídia social e outros canais digitais. O Target pode executar testes A/B, testes multivariados, recomendar produtos e conteúdo, conteúdo do Target, personalizar conteúdo automaticamente com IA e muito mais. O foco desta lição está na funcionalidade de teste A/B do Target. Consulte a [Visão geral do Teste A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=en) para obter mais informações.

![Arquitetura](assets/architecture-at.png)

Antes de executar testes A/B com o Target, você deve garantir que as configurações e integrações adequadas estejam em vigor.

>[!NOTE]
>
>Essa lição é opcional e se aplica somente aos usuários do Adobe Target que desejam realizar testes A/B.


## Pré-requisitos

* O aplicativo com SDKs instalados e configurados foi criado e executado com sucesso.
* Acesse o Adobe Target com permissões, funções, espaços de trabalho e propriedades corretamente configuradas, conforme descrito [aqui](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=pt-BR).


## Objetivos de aprendizagem

Nesta lição, você vai:

* Atualize sua sequência de dados para integração com o Target.
* Atualize a propriedade da tag com a extensão do Offer Decisioning e do Target.
* Atualize seu esquema para capturar eventos de apresentação.
* Validar configuração no Assurance.
* Crie um teste A/B simples no Target.
* Atualize seu aplicativo para registrar a extensão Otimizer.
* Implemente o teste A/B no aplicativo.
* Validar a implementação no Assurance.


## Configurar

>[!TIP]
>
>Se você já configurou seu aplicativo como parte da lição [Ofertas da Journey Optimizer](journey-optimizer-offers.md), talvez já tenha realizado algumas das etapas desta seção de configuração.

### Atualizar configuração da sequência de dados

#### Adobe Target

Para garantir que os dados enviados do aplicativo móvel para o Experience Platform Edge Network sejam encaminhados para o Adobe Target, atualize a configuração da sequência de dados.

1. Na interface da Coleção de dados, selecione **[!UICONTROL Datastreams]** e selecione sua sequência de dados, por exemplo **[!DNL Luma Mobile App]**.
1. Selecione **[!UICONTROL Adicionar Serviço]** e selecione **[!UICONTROL Adobe Target]** na lista **[!UICONTROL Serviço]**.
1. Se você for cliente do Target Premium e quiser usar tokens de propriedade, insira o valor do **[!UICONTROL Token de propriedade]** do Target que deseja usar para essa integração. Usuários do Target Standard podem ignorar esta etapa.

   Você pode encontrar suas propriedades na interface do usuário de Destino, em **[!UICONTROL Administração]** > **[!UICONTROL Propriedades]**. Selecione ![Código](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg) para revelar o token de propriedade da propriedade que você deseja usar. O token de propriedade tem um formato como `"at_property": "xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"`; você só deve inserir o valor `xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx`.

   Opcionalmente, você pode especificar uma ID de ambiente do Target. O Target usa ambientes para organizar seus sites e ambientes de pré-produção para facilitar o gerenciamento e separar os relatórios. Os ambientes predefinidos incluem Produção, Preparo e Desenvolvimento. Consulte [Ambientes](https://experienceleague.adobe.com/docs/target/using/administer/environments.html?lang=en) e [ID do Ambiente de Destino](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html?lang=en#target-environment-id) para obter mais informações.

   Como opção, você pode especificar um namespace de ID de terceiros do Target para oferecer suporte à sincronização de perfis em um namespace de identidade (por exemplo, CRM ID). Consulte [Namespace de ID de terceiros do Target](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html?lang=en#target-third-party-id-namespace) para obter mais informações.

1. Selecione **[!UICONTROL Salvar]**.

   ![Adicionar Destino à sequência de dados](assets/edge-datastream-target.png)


#### Adobe Journey Optimizer

Para garantir que os dados enviados do aplicativo móvel para a Edge Network sejam encaminhados para o Journey Optimizer - Gerenciamento de decisão, atualize a configuração da sequência de dados.

1. Na interface da Coleção de dados, selecione **[!UICONTROL Datastreams]** e selecione sua sequência de dados, por exemplo **[!DNL Luma Mobile App]**.
1. Selecione ![Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) para **[!UICONTROL Experience Platform]** e selecione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Editar]** no menu de contexto.
1. Na tela **[!UICONTROL Datastreams]** > ![Folder](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) > **[!UICONTROL Adobe Experience Platform]**, verifique se o **[!UICONTROL Offer Decisioning]**, o **[!UICONTROL Edge Segmentation]** e o **[!UICONTROL Personalization Destinations]** estão selecionados. Se você também seguir as lições do Journey Optimizer, selecione **[!UICONTROL Adobe Journey Optimizer]**. Consulte [configurações do Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#aep) para obter mais informações.
1. Para salvar a configuração da sequência de dados, selecione **[!UICONTROL Salvar]**.

   ![Configuração da sequência de dados do AEP](assets/datastream-aep-configuration-target.png)


### Instalar a extensão de tags do Offer Decisioning e do Target

1. Navegue até **[!UICONTROL Tags]**, localize sua propriedade de tag móvel e abra a propriedade.
1. Selecione **[!UICONTROL Extensões]**.
1. Selecione **[!UICONTROL Catálogo]**.
1. Pesquise a extensão **[!UICONTROL Offer Decisioning e Target]**.
1. Instale a extensão. A extensão não requer configuração adicional.

   ![Adicionar extensão do Offer Decisioning e do Target](assets/tag-add-decisioning-extension.png)


### Atualizar seu esquema

1. Navegue até a interface Coleção de dados e selecione **[!UICONTROL Esquemas]** no painel esquerdo.
1. Selecione **[!UICONTROL Procurar]** na barra superior.
1. Selecione seu esquema para abri-lo.
1. No editor de esquema, selecione ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Adicionar]** ao lado de **[!UICONTROL Grupos de campos]**.
1. Na caixa de diálogo **[!UICONTROL Adicionar grupos de campos]**, procure `proposition`, selecione **[!UICONTROL Evento de Experiência - Interações de Apresentação]** e selecione **[!UICONTROL Adicionar grupos de campos]**.
   ![Proposta](assets/schema-fieldgroup-proposition.png)
1. Para salvar as alterações no esquema, selecione **[!UICONTROL Salvar]**.


### Validar configuração no Assurance

Para validar a configuração no Assurance:

1. Vá para a interface do Assurance.
1. Selecione **[!UICONTROL Configurar]** no painel esquerdo e selecione ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) ao lado de **[!UICONTROL Validar Instalação]** abaixo de **[!UICONTROL OFFER DECISIONING AND TARGET]**.
1. Selecione **[!UICONTROL Salvar]**.
1. Selecione **[!UICONTROL Validar instalação]** no painel esquerdo. A configuração do fluxo de dados é validada e a configuração do SDK no aplicativo.
   ![Validação da AJO Decisioning](assets/ajo-decisioning-validation.png)

## Criar um teste A/B

Há muitos tipos de atividades que você pode criar no Adobe Target e implementar em um aplicativo móvel, como mencionado na introdução. Para esta lição, você implementará um teste A/B.

1. Na interface do usuário do Target, selecione **[!UICONTROL Atividades]** na barra superior.
1. Selecione **[!UICONTROL Criar atividade]** e **[!UICONTROL Teste A/B]** no menu de contexto.
1. Na caixa de diálogo **[!UICONTROL Criar atividade de Teste A/B]**, selecione **[!UICONTROL Mobile]** como o **[!UICONTROL Type]**, selecione um espaço de trabalho na lista **[!UICONTROL Escolher Workspace]** e selecione sua propriedade na lista **[!UICONTROL Escolher propriedade]** se você for cliente do Target Premium e tiver especificado um token de propriedade na sequência de dados.
1. Selecione **[!UICONTROL Criar]**.
   ![Criar atividade do Target](assets/target-create-activity1.png)

1. Na tela **[!UICONTROL Atividade sem título]**, na etapa **[!UICONTROL Experiências]**:

   1. Insira `luma-mobileapp-abtest` em **[!UICONTROL Selecionar Local]** abaixo de **[!UICONTROL LOCAL 1]**. Esse nome de local (geralmente chamado de mbox) é usado posteriormente na implementação do aplicativo.
   1. Selecione ![Divisa para baixo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) ao lado de **[!UICONTROL Conteúdo padrão]** e selecione **[!UICONTROL Criar oferta JSON]** no menu de contexto.
   1. Copie o seguinte JSON em **[!UICONTROL Insira um objeto JSON válido]**.

      ```json
      { 
          "title": "Luma Anaolog Watch",
          "text": "Designed to stand up to your active lifestyle, this women's Luma Analog Watch features a tasteful brushed chrome finish and a stainless steel, water-resistant construction for lasting durability.", 
          "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/gear/watches/Luma_Analog_Watch.jpg" 
      }
      ```

   1. Selecione **[!UICONTROL + Adicionar experiência]**.

      ![Experiência A](assets/target-create-activity-experienceA.png)

   1. Repita as etapas b e c para a Experiência B, mas use o seguinte JSON:

      ```json
      { 
          "title": "Aim Analog Watch",
          "text": "The flexible, rubberized strap is contoured to conform to the shape of your wrist for a comfortable all-day fit. The face features three illuminated hands, a digital read-out of the current time, and stopwatch functions.", 
          "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/gear/watches/Aim_Watch.jpg" 
      }
      ```

   1. Selecione **[!UICONTROL Próximo]**.

      ![Experiência B](assets/target-create-activity-experienceB.png)

1. Na etapa **[!DNL Targeting]**, revise a configuração do seu teste A/B. Por padrão, ambas as ofertas são alocadas igualmente entre todos os visitantes. Clique em **[!UICONTROL Avançar]** para continuar.

   ![Direcionamento](assets/taget-targeting.png)

1. Na etapa **[!UICONTROL Metas e configurações]**:

   1. Renomeie sua Atividade sem título, por exemplo, para `Luma Mobile SDK Tutorial - A/B Test Example`.
   1. Insira um **[!UICONTROL Objetivo]** para seu teste A/B, por exemplo `A/B Test for Luma mobile app tutorial`.
   1. Selecione **[!UICONTROL Conversão]**, **[!UICONTROL Visualizou uma mbox]** no bloco **[!UICONTROL Métrica de meta]** > **[!UICONTROL MINHA META PRIMÁRIA]** e digite o nome da sua localização (mbox), por exemplo `luma-mobileapp-abtest`.
   1. Selecione **[!UICONTROL Salvar e fechar]**.

      ![Configurações de metas](assets/target-goals.png)

1. De volta à tela **[!UICONTROL Todas as atividades]**:

   1. Selecione ![Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) na sua atividade.
   1. Selecione ![Reproduzir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg) **[!UICONTROL Ativar]** para ativar o teste A/B.

   ![Ativar](assets/target-activate.png)


## Implementar o Target no seu aplicativo

Conforme discutido nas lições anteriores, a instalação de uma extensão de tag móvel fornece apenas a configuração. Em seguida, instale e registre o Otimize SDK. Se essas etapas não estiverem claras, reveja a seção [Instalar SDKs](install-sdks.md).

>[!NOTE]
>
>Se você concluiu a seção [Instalar SDKs](install-sdks.md), o SDK já está instalado e você pode ignorar essa etapa.
>

1. No Xcode, verifique se [AEP Otimize](https://github.com/adobe/aepsdk-messaging-ios) foi adicionado à lista de pacotes nas dependências de pacotes. Consulte [Gerenciador de pacotes do Swift](install-sdks.md#swift-package-manager).
1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL AppDelegate]** no navegador de projetos Xcode.
1. Certifique-se de que `AEPOptimize` faça parte da sua lista de importações.

   `import AEPOptimize`

1. Verifique se `Optimize.self` faz parte da matriz de extensões que você está registrando.

   ```swift
   let extensions = [
       AEPIdentity.Identity.self,
       Lifecycle.self,
       Signal.self,
       Edge.self,
       AEPEdgeIdentity.Identity.self,
       Consent.self,
       UserProfile.self,
       Places.self,
       Messaging.self,
       Optimize.self,
       Assurance.self
   ]
   ```

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!DNL MobileSDK]** no navegador do Projeto Xcode. Localize a função ` func updatePropositionAT(ecid: String, location: String) async`. Adicione o seguinte código:

   ```swift
   // set up the XDM dictionary, define decision scope and call update proposition API
   Task {
       let ecid = ["ECID" : ["id" : ecid, "primary" : true] as [String : Any]]
       let identityMap = ["identityMap" : ecid]
       let xdmData = ["xdm" : identityMap]
       let decisionScope = DecisionScope(name: location)
       Optimize.clearCachedPropositions()
       Optimize.updatePropositions(for: [decisionScope], withXdm: xdmData)
   }
   ```

   Esta função:

   * configura um dicionário XDM `xdmData`, contendo a ECID para identificar o perfil para o qual você deve apresentar o teste A/B e
   * define um `decisionScope`, uma matriz de locais onde apresentar o teste A/B.

   Em seguida, a função chama duas APIs: [`Optimize.clearCachedPropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#clearpropositions) e [`Optimize.updatePropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#updatepropositions). Essas funções limpam todas as propostas em cache e atualizam as propostas para esse perfil. Uma apresentação neste contexto é a experiência (oferta) selecionada na atividade do Target (seu teste A/B) e que você definiu em [Criar um teste A/B](#create-an-ab-test).

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Personalization]** > **[!DNL TargetOffersView]** no navegador de projetos Xcode. Localize a função `func onPropositionsUpdateAT(location: String) async {` e inspecione o código dessa função. A parte mais importante dessa função é a chamada à API [`Optimize.onPropositionsUpdate`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#onpropositionsupdate), que:
   * recupera as apresentações do perfil atual com base no escopo da decisão (que é o local definido no Teste A/B),
   * recupera a oferta da proposta,
   * desenvolve o conteúdo da oferta para que ela possa ser exibida corretamente no aplicativo e
   * aciona a ação `displayed()` na oferta que envia um evento de volta para o Platform Edge Network informando que a oferta é exibida.

1. Ainda em **[!DNL TargetOffersView]**, adicione o seguinte código ao modificador `.onFirstAppear`. Esse código garante que a chamada de retorno para atualizar as ofertas seja registrada apenas uma vez.

   ```swift
   // Invoke callback for offer updates
   Task {
       await self.onPropositionsUpdateAT(location: location)
   }
   ```

1. Ainda em **[!DNL TargetOffersView]**, adicione o seguinte código ao modificador `.task`. Esse código atualiza as ofertas quando a exibição é atualizada.

   ```swift
   // Clear and update offers
   await self.updatePropositionsAT(ecid: currentEcid, location: location)
   ```

Você pode enviar parâmetros do Target adicionais (como parâmetros de mbox, perfil, produto ou pedido) em uma solicitação de consulta de personalização para a rede da Experience Edge, adicionando-os em um dicionário de dados ao chamar a API [`Optimize.updatePropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#updatepropositions). Consulte para obter mais informações [Parâmetros do Target](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/#target-parameters).


## Validar usando o aplicativo

1. Recrie e execute o aplicativo no simulador ou em um dispositivo físico do Xcode, usando ![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

1. Vá para a guia **[!UICONTROL Personalização]**.

1. Role para baixo até a parte inferior e você verá uma das duas ofertas definidas no teste A/B exibida no bloco **[!UICONTROL TARGET]**.

   <img src="assets/target-app-offer.png" width="300">


## Validar a implementação no Assurance

Para validar o teste A/B no Assurance:

1. Revise a seção [instruções de instalação](assurance.md#connecting-to-a-session) para conectar seu simulador ou dispositivo ao Assurance.
1. Selecione **[!UICONTROL Configurar]** no painel esquerdo e selecione ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) ao lado de **[!UICONTROL Revisar e simular]** abaixo de **[!UICONTROL OFFER DECSIONING AND TARGET]**.
1. Selecione **[!UICONTROL Salvar]**.
1. Selecione **[!UICONTROL Revisar e simular]** no painel esquerdo. A configuração do fluxo de dados é validada e a configuração do SDK no aplicativo.
1. Selecione **[!UICONTROL Solicitações]** na barra superior. Você vê suas solicitações de **[!DNL Target]**.
   ![Validação da AJO Decisioning](assets/assurance-decisioning-requests.png)

1. Você pode explorar as guias **[!UICONTROL Simular]** e **[!UICONTROL Lista de Eventos]** para obter mais funcionalidades, verificando sua configuração de ofertas do Target.

## Próximas etapas

Agora você deve ter todas as ferramentas para começar a adicionar mais testes A/B ou outras atividades do Target (como Direcionamento de experiência, Teste multivariado), quando relevante e aplicável, ao seu aplicativo. Há informações mais detalhadas disponíveis no [repositório do GitHub para a extensão Otimize](https://github.com/adobe/aepsdk-optimize-ios), onde você também pode encontrar um link para um [tutorial](https://opensource.adobe.com/aepsdk-optimize-ios/#/tutorials/README) dedicado sobre como rastrear ofertas da Adobe Target.

>[!SUCCESS]
>
>Você habilitou o aplicativo para testes A/B e exibiu os resultados de um teste A/B com a extensão Offer Decisioning e Target para o Adobe Experience Platform Mobile SDK.
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-os nesta [postagem de discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Próxima: **[Conclusão e próximas etapas](conclusion.md)**
