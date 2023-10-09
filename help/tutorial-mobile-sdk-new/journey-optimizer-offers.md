---
title: Criar e exibir ofertas
description: Saiba como criar e exibir ofertas com o SDK móvel da plataforma e o Adobe Journey Optimizer Decision Management.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Offers
hide: true
exl-id: c08a53cb-683e-4487-afab-fd8828c3d830
source-git-commit: d7410a19e142d233a6c6597de92f112b961f5ad6
workflow-type: tm+mt
source-wordcount: '2618'
ht-degree: 3%

---

# Criar e exibir ofertas com o Gerenciamento de decisão

Saiba como mostrar ofertas da Gestão de decisões da Journey Optimizer em seus aplicativos móveis com o SDK móvel do Experience Platform.

O Gerenciamento de decisão da Journey Optimizer ajuda você a fornecer a melhor oferta e experiência aos seus clientes em todos os pontos de contato na hora certa. Depois de projetado, direcione o público com ofertas personalizadas.

![Arquitetura](assets/architecture-od.png)

A gestão de decisões facilita a personalização com uma biblioteca central de ofertas de marketing e um mecanismo de decisão que aplica regras e restrições a perfis em tempo real avançados criados pelo Adobe Experience Platform. Como resultado, ele permite enviar aos clientes a oferta certa na hora certa. Consulte [Sobre o Gerenciamento de decisão](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/get-started-decision/starting-offer-decisioning.html?lang=en) para obter mais informações.




>[!NOTE]
>
>Esta lição é opcional e se aplica somente aos usuários do Journey Optimizer que desejam usar a funcionalidade de Gestão de decisões para exibir ofertas em um aplicativo móvel.


## Pré-requisitos

* O aplicativo com SDKs instalados e configurados foi criado e executado com sucesso.
* Configure o aplicativo para Adobe Experience Platform.
* Acesso ao Journey Optimizer - Gerenciamento de decisões com as permissões adequadas para gerenciar ofertas e decisões, conforme descrito [aqui](https://experienceleague.adobe.com/docs/journey-optimizer/using/access-control/privacy/high-low-permissions.html?lang=en#decisions-permissions).


## Objetivos de aprendizagem

Nesta lição, você

* Atualize sua configuração do Edge para o Gerenciamento de decisão.
* Atualize sua propriedade de tag com a extensão Journey Optimizer - Decisioning.
* Atualize seu esquema para capturar eventos de apresentação.
* Valide a configuração no Assurance.
* Crie uma decisão de oferta com base em ofertas no Journey Optimizer - Gestão de decisões.
* Atualize seu aplicativo para registrar a extensão Otimizer.
* Implemente ofertas da Gestão de decisões no seu aplicativo.


## Configuração

>[!TIP]
>
>Se você já configurou o ambiente como parte da [Configurar testes A/B com o Target](target.md) lição, talvez você já tenha executado algumas etapas nesta seção de configuração.

### Atualizar configuração da sequência de dados

Para garantir que os dados enviados do aplicativo móvel para a Rede de borda sejam encaminhados para o Journey Optimizer - Gerenciamento de decisão, atualize sua configuração do Experience Edge .

1. Na interface da Coleção de dados, selecione **[!UICONTROL Datastreams]** e selecione seu fluxo de dados, por exemplo **[!DNL Luma Mobile App]**.
1. Selecionar ![Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) para **[!UICONTROL Experience Platform]** e selecione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Editar]** no menu de contexto.
1. No **[!UICONTROL Datastreams]** > ![Pasta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) >  **[!UICONTROL Adobe Experience Platform]** , certifique-se **[!UICONTROL Offer decisioning]**, **[!UICONTROL Segmentação de borda]**, e **[!UICONTROL Adobe Journey Optimizer]** são selecionados. Se também seguir a lição do Target, selecione **[!UICONTROL Destinos de personalização]** também. Consulte [Configurações do Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#aep) para obter mais informações.
1. Para salvar a configuração do fluxo de dados, selecione **[!UICONTROL Salvar]** .

   ![Configuração da sequência de dados da AEP](assets/datastream-aep-configuration-offers.png)




### Instalar a extensão Journey Optimizer - Decisioning tags

1. Navegue até **[!UICONTROL Tags]** e encontre sua propriedade de tag móvel e abra a propriedade.
1. Selecionar **[!UICONTROL Extensões]**.
1. Selecionar **[!UICONTROL Catálogo]**.
1. Procure por **[!UICONTROL Adobe Journey Optimizer - Decisão]** extensão.
1. Instale a extensão. A extensão não requer configuração adicional.

   ![Adicionar extensão do Decisioning](assets/tag-add-decisioning-extension.png)


### Atualizar seu esquema

1. Navegue até a interface da Coleção de dados e selecione **[!UICONTROL Esquemas]** do painel esquerdo.
1. Selecionar **[!UICONTROL Procurar]** na barra superior.
1. Selecione seu esquema para abri-lo.
1. No editor de esquema, selecione ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Adicionar]** ao lado de Grupos de campos.
1. No **[!UICONTROL Adicionar grupos de campos]** diálogo, ![Pesquisar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) pesquisar `proposition`, selecione **[!UICONTROL Evento de experiência - Interações de apresentação]** e selecione **[!UICONTROL Adicionar grupos de campos]**. Este grupo de campos coleta os dados do evento de experiência relevantes para ofertas: qual oferta é apresentada, como parte de qual coleção, decisão e outros parâmetros (consulte mais adiante nesta lição). Mas também o que está acontecendo com a oferta: ela é exibida, interage com, descartada e assim por diante.
   ![Apresentação](assets/schema-fieldgroup-proposition.png)
1. Selecionar **[!UICONTROL Salvar]** para salvar as alterações no esquema.


## Validar configuração no Assurance

Para validar sua configuração no Assurance:

1. Vá para a interface do usuário do Assurance.
1. Selecionar **[!UICONTROL Configurar]** no painel esquerdo e selecione ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) ao lado de **[!UICONTROL Validar configuração]** abaixo **[!UICONTROL ADOBE JOURNEY OPTIMIZER DECISIONING]**.
1. Selecione **[!UICONTROL Salvar]**.
1. Selecionar **[!UICONTROL Validar configuração]** no painel esquerdo. A configuração da sequência de dados e a configuração do SDK em seu aplicativo são validadas.
   ![Validação da decisão do AJO](assets/ajo-decisioning-validation.png)


## Criar posicionamento

Antes de realmente criar ofertas, é necessário definir como e onde essas ofertas podem ser colocadas no aplicativo móvel. Na Gestão de decisões, você define disposições para essa finalidade e uma disposição para o canal móvel que oferece suporte a uma carga JSON:

1. Na interface do Journey Optimizer, selecione ![Componentes](https://spectrum.adobe.com/static/icons/workflow_18/Smock_OfferActivities_18_N.svg)  **[!UICONTROL Componentes]** de **[!UICONTROL GERENCIAMENTO DE DECISÃO]** no painel esquerdo.

1. Selecionar **[!UICONTROL Posicionamentos]** na barra superior.

1. Se nenhum posicionamento com o nome **[!UICONTROL JSON móvel]**,  **[!UICONTROL Dispositivo móvel]** as **[!UICONTROL Tipo de canal]** e **[!UICONTROL JSON]** as **[!UICONTROL Tipo de conteúdo]** estiver listado, é necessário criar uma disposição. Caso contrário, continue para [Criar ofertas](#create-offers).

Para criar a disposição JSON para dispositivos móveis:

1. Selecionar ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) Criar posicionamento.

   1. no **[!UICONTROL Detalhes]** , insira `Mobile JSON` como o **[!UICONTROL Nome]**, selecione **[!UICONTROL Dispositivo móvel]** de **[!UICONTROL Tipo de canal]** e **[!UICONTROL JSON]** de **[!UICONTROL Tipo de conteúdo]**.
   1. Selecionar **[!UICONTROL Salvar]** para salvar o posicionamento.

   ![Criar posicionamento](assets/ajo-create-placement.png)



## Criar ofertas

1. Na interface do Journey Optimizer, selecione ![Ofertas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Offers_18_N.svg)  **[!UICONTROL Ofertas]** de **[!UICONTROL GERENCIAMENTO DE DECISÃO]** no painel esquerdo.
1. No **[!UICONTROL Ofertas]** , selecione **[!UICONTROL Procurar]** para ver a lista de ofertas.
1. Selecionar **[!UICONTROL Criar oferta]**.
1. No **[!UICONTROL Nova oferta]** , selecione **[!UICONTROL Oferta personalizada]** e clique em **[!UICONTROL Próxima]**.
1. No **[!UICONTROL Detalhes]** etapa de **[!UICONTROL Criar nova oferta personalizada]**:
   1. Insira um **[!UICONTROL Nome]** para a oferta, por exemplo `Luma - Juno Jacket`e insira um **[!UICONTROL Data e hora de início]** e uma **[!UICONTROL Data e hora final]**. Fora dessas datas, a oferta não será selecionada pelo mecanismo de decisão.
   1. Selecione **[!UICONTROL Próximo]**.
      ![Ofertas - Detalhes](assets/ajo-offers-details.png)

1. No **[!UICONTROL Adicionar representações]** etapa de **[!UICONTROL Criar nova oferta personalizada]**:
   1. Selecionar ![Dispositivo móvel](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DevicePhone_18_N.svg) **[!UICONTROL Dispositivo móvel]** de **[!UICONTROL Canal]** e selecione **[!UICONTROL JSON móvel]** do **[!UICONTROL Posicionamento]** lista.
   1. Selecionar **[!UICONTROL Personalizado]** para **[!UICONTROL Conteúdo]**.
   1. Selecionar **[!UICONTROL Adicionar conteúdo]**. No **[!UICONTROL Adicionar personalização]** diálogo:
      1. Insira o seguinte JSON:

         ```json
         { 
             "title": "Juno Jacket",
             "text": "On colder-than-comfortable mornings, you'll love warming up in the Juno All-Ways Performanc Jacket, designed to compete with wind and chill. Built-in Cocona&trade; technology aids evaporation, while a special zip placket and stand-up collar keep your neck protected.", 
             "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/women/tops/jackets/wj06-purple_main.jpg" 
         }  
         ```

      1. Selecione **[!UICONTROL Salvar]**.
         ![Ofertas - Conteúdo personalizado](assets/ajo-offers-customcontent.png)
   1. Selecione **[!UICONTROL Próximo]**.
      ![Representações da oferta](assets/ajo-offers-representations.png)

1. No **[!UICONTROL Adicionar restrições]** etapa do **[!UICONTROL Criar nova oferta personalizada]**:
   1. Definir **[!UICONTROL Prioridade]** para `10`.
   1. Alternar **[!UICONTROL Incluir limite]** desativado.
   1. Selecione **[!UICONTROL Próximo]**.
      ![Ofertas - Restrições](assets/ajo-offers-constraints.png)

1. No **[!UICONTROL Revisão]** etapa de **[!UICONTROL Criar novo personalizado]** oferta:
   1. Revise a oferta e selecione **[!UICONTROL Concluir]**.
   1. No **[!UICONTROL Salvar oferta]** , selecione **[!UICONTROL Salvar e aprovar]**.

1. Repita as etapas de 3 a 8 para criar mais quatro ofertas com nomes e conteúdo diferentes. Todos os outros valores de configuração, por exemplo, Data e hora inicial ou Prioridade, são semelhantes à primeira oferta criada. Você pode criar e editar ofertas rapidamente.

   1. Na interface do Journey Optimizer, selecione ![Ofertas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Offers_18_N.svg) **[!UICONTROL Ofertas]** no painel esquerdo, selecione Offers na barra superior.
   1. Selecione a linha da oferta que você criou.
   1. No painel direito, selecione ![Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmall_18_N.svg) **[!UICONTROL Mais ações]** e, no menu de contexto, selecione ![Duplicar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Duplicate_18_N.svg) **[!UICONTROL Duplicar]**.

      Use a tabela abaixo para definir as quatro outras ofertas.

      | Nome da oferta | Conteúdo de oferta em JSON |
      |---|---|
      | Luma - Afirmar Garrafa de Água | `{ "title": "Affirm Water Bottle", "text": "You'll stay hydrated with ease with the Affirm Water Bottle by your side or in hand. Measurements on the outside help you keep track of how much you're drinking, while the screw-top lid prevents spills. A metal carabiner clip allows you to attach it to the outside of a backpack or bag for easy access.", "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/gear/fitness-equipment/ug06-lb-0.jpg" }` |
      | Luma - Tee fitness desejado | `{ "title": "Desiree Fitness Tee", "text": "When you're too far to turn back, thank yourself for choosing the Desiree Fitness Tee. Its ultra-lightweight, ultra-breathable fabric wicks sweat away from your body and helps keeps you cool for the distance.", "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/women/tops/tees/ws05-yellow_main.jpg" }` |
      | Luma - Adrienne Trek Jacket | `{ "title": "Adrienne Trek Jacket", "text": "You're ready for a cross-country jog or a coffee on the patio in the Adrienne Trek Jacket. Its style is unique with stand collar and drawstrings, and it fits like a jacket should.", "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/women/tops/jackets/wj08-gray_main.jpg" }` |
      | Luma - Camiseta fitness diário do Aero | `{ "title": "Adrienne Trek Jacket", "text": "You're ready for a cross-country jog or a coffee on the patio in the Adrienne Trek Jacket. Its style is unique with stand collar and drawstrings, and it fits like a jacket should.", "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/women/tops/jackets/wj08-gray_main.jpg" }` |

      {style="table-layout:fixed"}

1. Como etapa final, você deve criar uma oferta substituta, que é uma oferta enviada aos clientes se eles não estiverem qualificados para outras ofertas.
   1. Selecionar **[!UICONTROL Criar oferta]**.
   1. No **[!UICONTROL Detalhes]** etapa de **[!UICONTROL Criar nova oferta personalizada]**:
   1. Insira um **[!UICONTROL Nome]** para a oferta, por exemplo `Luma - Fallback Offer`e insira um **[!UICONTROL Data e hora de início]** e uma **[!UICONTROL Data e hora final]**.
   1. Selecione **[!UICONTROL Próximo]**.

1. No **[!UICONTROL Adicionar representações]** etapa do **[!UICONTROL Criar nova oferta personalizada]** tela:
   1. Selecionar ![Dispositivo móvel](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DevicePhone_18_N.svg) **[!UICONTROL Dispositivo móvel]** de **[!UICONTROL Canal]** e selecione **[!UICONTROL JSON móvel]** de **[!UICONTROL Posicionamento]** lista.
   1. Selecionar **[!UICONTROL Personalizado]** para **[!UICONTROL Conteúdo]**.
   1. Selecionar **[!UICONTROL Adicionar conteúdo]**. No **[!UICONTROL Adicionar personalização]** diálogo:
      1. Insira o seguinte JSON:

         ```json
         {  
             "title": "Luma",
             "text": "Your store for sports wear and equipment.", 
             "image": "https://luma.enablementadobe.com/content/dam/luma/en/logos/Luma_Logo.png" 
         }  
         ```

      1. Selecione **[!UICONTROL Salvar]**.
   1. Selecione **[!UICONTROL Próximo]**.


1. No **[!UICONTROL Revisão]** etapa de **[!UICONTROL Criar novo personalizado]** oferta:
   1. Revise a oferta e selecione **[!UICONTROL Concluir]**.
   1. No **[!UICONTROL Salvar oferta]** , selecione **[!UICONTROL Salvar e aprovar]**.

Agora você deve ter a seguinte lista de ofertas.
![Lista de ofertas](assets/ajo-offers-list.png)


## Criar uma coleção

Para apresentar uma oferta ao usuário do aplicativo móvel, você deve definir uma coleção de ofertas que consiste em uma ou mais ofertas criadas.

1. Na interface do Journey Optimizer, selecione **[!UICONTROL Ofertas]** do painel esquerdo.
1. Selecionar **[!UICONTROL Coleções]** na barra superior.
1. Selecionar ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Criar coleção]**.
1. No **[!UICONTROL Nova coleção]** , insira um **[!UICONTROL Nome]** para sua coleção, por exemplo `Luma - Mobile App Collection`, selecione **[!UICONTROL Criar coleção estática]** e clique em **[!UICONTROL Próxima]**.
1. Entrada **[!DNL Luma - Mobile App Collection]**, selecione as ofertas que deseja incluir na coleção. Para este tutorial, escolha as cinco ofertas que você criou. É possível filtrar facilmente a lista usando o campo de pesquisa, por exemplo, digitando **[!DNL Luma]**.
1. Selecione **[!UICONTROL Salvar]**.

   ![Ofertas - Coleção](assets/ajo-collection-offersselected.png)


## Criar uma decisão

A etapa final é definir uma decisão, que é a combinação de um ou mais escopos de decisão e sua oferta substituta.

Um escopo de decisão é uma combinação de um posicionamento específico (por exemplo, HTML em um email ou JSON em um aplicativo móvel) e um ou mais critérios de avaliação.

Um critério de avaliação é a combinação de

* uma coleção de ofertas,
* regras de elegibilidade: por exemplo, a oferta está disponível somente para um público-alvo específico?
* um método de classificação: quando várias ofertas estão disponíveis para seleção, qual método você usa para classificá-las (por exemplo, por prioridade de oferta, usando uma fórmula ou um modelo de IA).

Consulte [Etapas principais para criar e gerenciar ofertas](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/get-started-decision/key-steps.html?lang=en) se você quiser entender melhor como as disposições, regras, classificações, ofertas, representações, coleções, decisões e assim por diante, interagem e se relacionam entre si. Esta lição está focada apenas no uso do resultado de uma decisão em vez da flexibilidade na definição de decisões no Journey Optimizer - Gestão de decisões.

1. Na interface do Journey Optimizer, selecione **[!UICONTROL Ofertas]** do painel esquerdo.
1. Selecionar **[!UICONTROL Decisões]** na barra superior.
1. Selecionar ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Criar decisão]**.
1. No **[!UICONTROL Detalhes]** etapa de **[!UICONTROL Criar uma nova decisão de oferta]**:
   1. Insira um **[!UICONTROL Nome]** para a decisão, por exemplo `Luma - Mobile App Decision`, insira **[!UICONTROL Data e hora de início]** e **[!UICONTROL Data e hora final]**.
   1. Selecione **[!UICONTROL Próximo]**.

1. No **[!UICONTROL Adicionar escopos de decisão]** etapa de **[!UICONTROL Criar uma nova decisão de oferta]**:
   1. Selecionar **[!UICONTROL JSON móvel]** de **[!UICONTROL Posicionamento]** lista.
   1. No **[!UICONTROL Critérios de avaliação]** bloco, selecione ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Adicionar]**.
      1. No **[!UICONTROL Adicionar coleção de ofertas]** selecione sua coleção de ofertas. Por exemplo, **[!DNL Luma - Mobile App Collection]**.
      1. Selecionar **[!UICONTROL Adicionar]**.
         ![Decisão - Selecionar coleção](assets/ajo-decision-selectcollection.png)
   1. Assegure que **[!UICONTROL Nenhum]** está selecionado para **[!UICONTROL Elegibilidade]**, e **[!UICONTROL Prioridade da oferta]** está selecionado como **[!UICONTROL Método de classificação]**.
   1. Selecione **[!UICONTROL Próximo]**.
      ![Escopos de decisão](assets/ajo-decision-scopes.png).
1. No **[!UICONTROL Adicionar oferta substituta]** etapa de **[!UICONTROL Criar uma nova decisão de oferta]**:
   1. Selecione a oferta substituta, por exemplo, a variável **[!DNL Luma - Fallback offer]**.
   1. Selecione **[!UICONTROL Próximo]**.
1. No **[!UICONTROL Resumo]** etapa de **[!UICONTROL Criar uma nova decisão de oferta]**:
   1. Selecione **[!UICONTROL Concluir]**.
   1. No **[!UICONTROL Salvar decisão de oferta]** , selecione **[!UICONTROL Salvar e ativar]**.
   1. No **[!UICONTROL Decisões]** você verá sua decisão com o status **[!UICONTROL Ao vivo]**.

Sua decisão de oferta, que consiste em um conjunto de ofertas, agora está pronta para uso. Para usar a decisão em seu aplicativo, você precisa consultar no código o escopo da decisão.

1. Na interface do Journey Optimizer, selecione **[!UICONTROL Ofertas]**.
1. Selecionar **[!UICONTROL Decisões]** na barra superior.
1. Selecione sua decisão, por exemplo **[!DNL Luma - Mobile App Decision]**.
1. No **[!UICONTROL Escopos de decisão]** bloco, selecione ![Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) **[!UICONTROL Copiar]**.
1. No menu contextual, selecione **[!UICONTROL Escopo da decisão]**.
   ![Copiar escopo da decisão](assets/ajo-copy-decisionscope.png)
1. Use qualquer editor de texto para colar o escopo de decisão para uso posterior. O escopo de decisão tem o seguinte formato JSON.

   ```json
   {
       "xdm:activityId":"xcore:offer-activity:xxxxxxxxxxxxxxx",
       "xdm:placementId":"xcore:offer-placement:xxxxxxxxxxxxxxx"
   }
   ```

## Implementar ofertas no aplicativo

Conforme discutido nas lições anteriores, a instalação de uma extensão de tag móvel fornece apenas a configuração. Em seguida, instale e registre o SDK Otimize. Se essas etapas não estiverem claras, revise o [Instalar SDKs](install-sdks.md) seção.

>[!NOTE]
>
>Se você concluiu o [Instalar SDKs](install-sdks.md) , o SDK já estará instalado e você poderá ignorar essa etapa.
>

1. No Xcode, verifique se [Otimização da AEP](https://github.com/adobe/aepsdk-messaging-ios.git) é adicionado à lista de pacotes nas Dependências de pacote. Consulte [Gerenciador de pacotes Swift](install-sdks.md#swift-package-manager).
1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]** no navegador do Projeto Xcode.
1. Assegurar `AEPOptimize` faz parte da lista de importações.

   `import AEPOptimize`

1. Assegurar `Optimize.self` O faz parte da matriz de extensões que você está registrando.

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

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** no navegador do Projeto Xcode. Localize o `func updatePropositionOD(ecid: String, activityId: String, placementId: String, itemCount: Int) async` função. Adicione o seguinte código:

   ```swift
   // set up the XDM dictionary, define decision scope and call update proposition API
   Task {  
      let ecid = ["ECID" : ["id" : ecid, "primary" : true] as [String : Any]]
      let identityMap = ["identityMap" : ecid]
      let xdmData = ["xdm" : identityMap]
      let decisionScope = DecisionScope(activityId: activityId, placementId: placementId, itemCount: UInt(itemCount))
      Optimize.clearCachedPropositions()
      Optimize.updatePropositions(for: [decisionScope], withXdm: xdmData)
   }
   ```

   Esta função:

   * configura um dicionário XDM `xdmData`, contendo a ECID para identificar o perfil para o qual você deve apresentar as ofertas.
   * define `decisionScope`, um objeto baseado na decisão definida na interface do Journey Optimizer - Gestão de decisões e definido por meio do escopo de decisão copiado do [Criar uma decisão](#create-a-decision).  O aplicativo Luma usa um arquivo de configuração (`decisions.json`) que recupera os parâmetros do escopo, com base no seguinte formato JSON:

     ```swift
     "scopes": [
         {
             "name": "name of the scope",
             "activityId": "xcore:offer-activity:xxxxxxxxxxxxxxx",
             "placementId": "xcore:offer-placement:xxxxxxxxxxxxxxx",
             "itemCount": 2
         }
     ]
     ```

     No entanto, você pode usar qualquer tipo de implementação para garantir que as APIs de otimização obtenham os parâmetros adequados (`activityId`, `placementId` e, `itemCount`), para construir um válido [`DecisionScope`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#decisionscope) para sua implementação.
   * O chama duas APIs: [`Optimize.clearCachePropositions`](https://support.apple.com/en-ie/guide/mac-help/mchlp1015/mac)  e [`Optimize.updatePropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#updatepropositions).  Essas funções limpam todas as propostas em cache e atualizam as propostas para esse perfil.

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!UICONTROL Personalização]** > **[!UICONTROL EdgeOffersView]** no navegador do Projeto Xcode. Localize o `func onPropositionsUpdateOD(activityId: String, placementId: String, itemCount: Int) async` e inspecione o código dessa função. A parte mais importante dessa função é a [`Optimize.onPropositionsUpdate`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#onpropositionsupdate) chamada à API, que

   * recupera as apresentações do perfil atual com base no escopo de decisão (que você definiu na Journey Optimizer - Gestão de decisões),
   * recupera a oferta da proposta,
   * desenvolve o conteúdo da oferta para que ela possa ser exibida corretamente no aplicativo e
   * aciona o `displayed()` ação na oferta que enviará um evento de volta para a Rede de borda informando que a oferta é exibida.

1. Ainda em **[!DNL EdgeOffersView]**, adicione o seguinte código à `.onFirstAppear` modificador. Esse código garantirá que a chamada de retorno para atualização das ofertas seja registrada apenas uma vez.

   ```swift
   // Invoke callback for offer updates
   Task {
       await self.onPropositionsUpdateOD(activityId: decision.activityId, placementId: decision.placementId, itemCount: decision.itemCount)
   }
   ```

1. Ainda em **[!UICONTROL EdgeOffersView]**, adicione o seguinte código à `.task` modificador. Esse código atualizará as ofertas quando a visualização for atualizada.

   ```swift
   // Clear and update offers
   await self.updatePropositionsOD(ecid: currentEcid, activityId: decision.activityId, placementId: decision.placementId, itemCount: decision.itemCount)
   ```



## Validar usando o aplicativo

1. Recrie e execute o aplicativo no simulador ou em um dispositivo físico do Xcode, usando ![Reproduzir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

1. Vá até a guia **[!DNL Personalisation]**.

1. Selecione **[!DNL Edge Personalisation]**.

1. Role para cima e veja duas ofertas aleatórias exibidas a partir da coleção que você definiu no **[!DNL DECISION LUMA - MOBILE APP DECISION]** bloco.

   <img src="assets/ajo-app-offers.png" width="300">

   As ofertas são aleatórias, pois você deu a todas as ofertas a mesma prioridade e a classificação da decisão é baseada na prioridade.


## Validar implementação no Assurance

Para validar a implementação das ofertas no Assurance:

1. Revise o [instruções de configuração](assurance.md#connecting-to-a-session) seção para conectar seu simulador ou dispositivo ao Assurance.
1. Selecionar **[!UICONTROL Configurar]** no painel esquerdo e selecione ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) ao lado de **[!UICONTROL Revisar e simular]** abaixo **[!UICONTROL ADOBE JOURNEY OPTIMIZER DECISIONING]**.
1. Selecione **[!UICONTROL Salvar]**.
1. Selecionar **[!UICONTROL Revisar e simular]** no painel esquerdo. A configuração da sequência de dados é validada e a configuração do SDK em seu aplicativo.
1. Selecionar **[!UICONTROL Solicitações]** na barra superior. Você vê o seu **[!UICONTROL Ofertas]** solicitações.
   ![Validação da decisão do AJO](assets/assurance-decisioning-requests.png)

1. Você pode explorar **[!UICONTROL Simular]** e **[!UICONTROL Lista de Eventos]** para obter mais funcionalidades, verificando a configuração do Journey Optimizer Decision Management.

## Próximas etapas

Agora você deve ter todas as ferramentas para começar a adicionar mais funcionalidade à implementação do Journey Optimizer - Gestão de decisões. Por exemplo:

* aplicar parâmetros diferentes às suas ofertas (por exemplo, prioridade, limite)
* coletar atributos de perfil no aplicativo (consulte [Perfil](profile.md)) e usar esses atributos de perfil para criar públicos-alvo. Em seguida, use esses públicos-alvo como parte das regras de qualificação na sua decisão.
* combinar mais de um escopo de decisão.

>[!SUCCESS]
>
>Você ativou o aplicativo para exibir ofertas usando a extensão Journey Optimizer - Decisioning para o SDK móvel do Experience Platform.<br/>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Próximo: **[Realizar testes A/B](target.md)**
