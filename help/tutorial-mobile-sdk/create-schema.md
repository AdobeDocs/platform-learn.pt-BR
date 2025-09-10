---
title: Criar um esquema XDM para implementações do Platform Mobile SDK
description: Saiba como criar um esquema XDM para eventos de aplicativos móveis.
feature: Mobile SDK,Schemas
jira: KT-14624
exl-id: c6b0d030-437a-4afe-b7d5-5a7831877983
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 2%

---

# Criar um esquema do XDM

Saiba como criar um esquema XDM para eventos de aplicativos móveis.

A padronização e a interoperabilidade são os principais conceitos por trás da Adobe Experience Platform. O Experience Data Model (XDM), orientado pela Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.

## O que são esquemas XDM?

O XDM é uma especificação documentada publicamente projetada para melhorar o potencial das experiências digitais. Ela fornece estruturas e definições comuns que permitem que qualquer aplicativo se comunique com os serviços da plataforma. Seguindo os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum que pode fornecer insights de maneira mais rápida e integrada. Você obtém insights valiosos das ações do cliente, define públicos do cliente por meio de segmentos e usa atributos do cliente para fins de personalização.

A Experience Platform usa esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, fica mais fácil manter o significado e, portanto, obter valor dos dados.

Antes que os dados possam ser assimilados na Platform, um esquema deve ser composto para descrever a estrutura dos dados e fornecer restrições ao tipo de dados que podem estar contidos em cada campo. Os esquemas consistem em uma classe base e zero ou mais grupos de campos de esquema.

Para obter mais informações sobre o modelo de composição de esquema, incluindo princípios de design e práticas recomendadas, consulte as [noções básicas da composição de esquema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) ou a lista de reprodução [Modelar os dados de experiência do cliente com o XDM](https://experienceleague.adobe.com/en/playlists/experience-platform-model-your-customer-experience-data-with-xdm).

>[!TIP]
>
>Se você estiver familiarizado com a Referência de design de solução (SDRs) do Analytics, poderá considerar um esquema como um SDR mais robusto. Consulte [Criar e manter um Documento de Referência de Design de Solução (SDR)](https://experienceleague.adobe.com/en/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr) para obter mais informações.

## Pré-requisitos

Para concluir a lição, você deve ter permissão para criar um esquema do Experience Platform.

## Objetivos de aprendizagem

Nesta lição, você vai:

* Criar um esquema na interface da Coleção de dados
* Adicionar um grupo de campos padrão ao esquema
* Criar e adicionar um grupo de campos personalizado ao esquema

## Navegar até esquemas

1. Faça logon na Adobe Experience Cloud.

1. Verifique se você está na sandbox da Experience Platform que está usando para este tutorial.

1. Abra o alternador de aplicativos ![Alternador de aplicativos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) (na parte superior direita),

1. Selecione **[!UICONTROL Coleção de dados]** no menu.

   ![Logon no Experience Cloud](assets/experiencecloud-login.png){zoomable="yes"}

   >[!NOTE]
   >
   > Os clientes de aplicativos baseados em plataforma, como o Real-Time CDP, devem usar uma sandbox de desenvolvimento para este tutorial. Outros clientes usam a sandbox de produção padrão.


1. Selecione ![Esquemas](/help/assets/icons/Schemas.svg) **[!UICONTROL Esquemas]** em **[!UICONTROL Gerenciamento de dados]** no painel esquerdo.

   ![tela inicial das marcas](assets/mobile-schema-navigate.png){zoomable="yes"}

Agora você está na página principal de esquemas e uma lista dos esquemas existentes é apresentada a você. Você também pode ver guias correspondentes aos blocos de construção principais de um schema:

* **Grupos de campos** são componentes reutilizáveis que definem um ou mais campos para capturar dados específicos, como detalhes pessoais, preferências de hotel ou endereço.
* **Classes** definem os aspectos comportamentais dos dados que o esquema contém. Por exemplo: `XDM ExperienceEvent` captura séries temporais, dados de evento e `XDM Individual Profile` captura dados de atributo sobre um indivíduo.
* **Os tipos de dados** são usados como tipos de campo de referência em classes ou grupos de campos da mesma forma que os campos literais básicos.

As descrições acima são uma visão geral de alto nível. Para obter mais detalhes, consulte o vídeo [Blocos de construção de esquema](https://experienceleague.adobe.com/en/docs/platform-learn/tutorials/schemas/schema-building-blocks) ou leia [Noções básicas sobre a composição de esquema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) na documentação do produto.

Neste tutorial, você usa o grupo de campos Evento de experiência do consumidor e cria um personalizado para demonstrar o processo.

>[!NOTE]
>
>O Adobe continua a adicionar mais grupos de campos padrão e eles devem ser usados sempre que possível. Esses campos são entendidos implicitamente pelos serviços da Experience Platform e fornecem maior consistência quando usados em componentes da plataforma. O uso de grupos de campos padrão fornece benefícios tangíveis, como mapeamento automático no Analytics e recursos de IA na Platform.

## Arquitetura de esquema do aplicativo Luma

Em um cenário real, o processo de design do schema pode ser semelhante a:

* Colete os requisitos de negócios.
* Localize grupos de campos pré-criados para atender ao máximo de requisitos possível.
* Crie grupos de campos personalizados para qualquer lacuna.

Para fins de aprendizado, você usa grupos de campos pré-criados e personalizados.

* **Evento de experiência do consumidor**: grupo de campos pré-criado que tem muitos campos comuns.
* **Informações do aplicativo**: grupo de campos personalizado criado para imitar os conceitos do TrackState/TrackAction Analytics.

<!--Later in the tutorial, you can [update the schema](lifecycle-data.md) to include the **[!UICONTROL AEP Mobile Lifecycle Details]** field group.-->

## Criar um esquema

1. Selecione ![AddCircle](/help/assets/icons/AddCircle.svg) **[!UICONTROL Create Schema]**.

1. No diálogo **[!UICONTROL Criar um esquema]**, selecione **[!UICONTROL Manual]**. Use **[!UICONTROL Selecionar]** para continuar.

   ![Manual de esquema](assets/schema-manual.png){zoomable="yes"}

1. Na etapa **[!UICONTROL Selecionar uma classe]** do assistente **[!UICONTROL Criar esquema]**, selecione **[!UICONTROL Evento de experiência]** abaixo de **[!UICONTROL Selecione uma classe base para este esquema]**.

1. Selecione **[!UICONTROL Próximo]**.

   ![Classe base do Assistente de Esquema](assets/schema-wizard-base-class.png){zoomable="yes"}

1. Na etapa **[!UICONTROL Nome e revisão]** do assistente **[!UICONTROL Criar esquema]**, insira um **[!UICONTROL Nome para exibição do esquema]**, por exemplo `Luma Mobile Event Schema` e uma [!UICONTROL Descrição], por exemplo `Schema for Luma mobile app experience events`.

   >[!NOTE]
   >
   >Se você estiver assistindo a este tutorial com várias pessoas em uma única sandbox ou se estiver usando uma conta compartilhada, considere anexar ou anexar uma identificação como parte de suas convenções de nomenclatura. Por exemplo, em vez de `Luma Mobile App Event Schema`, use `Luma Mobile App Event Schema - Joe Smith`. Consulte também a observação em [Visão geral](overview.md).

1. Selecione **[!UICONTROL Concluir]** para concluir o assistente.

   ![Nome e revisão do esquema](assets/schema-wizard-name-and-review.png){zoomable="yes"}


1. Selecione ![Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **Adicionar** ao lado de **[!UICONTROL Grupos de campos]**.

   ![Adicione um grupo de campos](assets/add-field-group.png){zoomable="yes"}

1. Pesquisar por `Consumer Experience Event`.

1. Selecione ![Visualizar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Preview_18_N.svg) para visualizar os campos e/ou ler a descrição para obter mais detalhes antes de selecionar um grupo de campos.

1. Selecione **Evento de experiência do consumidor**.

1. Selecione **[!UICONTROL Adicionar grupos de campos]**.

   ![Selecionando grupo de campos](assets/schema-select-field-groups.png){zoomable="yes"}

   Você é redirecionado à tela principal de composição do esquema, onde é possível ver todos os campos disponíveis.

1. Selecione **[!UICONTROL Salvar]**.
1. Selecione ![Esquemas](/help/assets/icons/Schemas.svg) **[!UICONTROL Esquemas]** em **[!UICONTROL Gerenciamento de dados]** para retornar à interface principal de **[!UICONTROL Esquemas]**.

>[!NOTE]
>
>Lembre-se de que não é necessário usar todos os campos em um grupo. Também é possível remover campos para ajudar a manter o esquema conciso e compreensível. Se for útil, você pode considerar um esquema como uma camada de dados vazia. No aplicativo, você preenche os valores relevantes no momento apropriado.

O grupo de campos [!UICONTROL Evento de Experiência do Consumidor] tem um tipo de dados chamado [!UICONTROL Informações da Web], que descreve eventos como exibição de página e cliques em links. No momento da escrita, não há uma paridade de aplicativo móvel para este recurso, portanto, você vai criar o seu próprio.

## Criar um tipo de dados personalizado


Você começa criando um tipo de dados personalizado que descreve os dois eventos:

* Exibição de tela
* Interação do aplicativo

1. Selecione a guia **[!UICONTROL Tipos de dados]**.

1. Selecione **[!UICONTROL Criar tipo de dados]**.

   ![Selecionar menu de tipo de dados](assets/schema-datatype-create.png){zoomable="yes"}

1. Forneça um **[!UICONTROL Nome de exibição]** e uma **[!UICONTROL Descrição]**, por exemplo `App Information` e `Custom data type describing "Screen Views" & "App Actions"`

   ![Fornecendo nome e descrição](assets/schema-datatype-name.png){zoomable="yes"}

   >[!TIP]
   >
   > Sempre use [!UICONTROL nomes para exibição] legíveis e descritivos para seus campos personalizados. Essa prática torna os campos personalizados mais acessíveis aos profissionais de marketing quando os campos são exibidos em serviços downstream, como o construtor de segmentos.


1. Para adicionar um campo, selecione o botão ![De adição](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg).


1. Este campo é um objeto de contêiner para interação com o aplicativo, portanto, forneça um camel-case **[!UICONTROL Nome do campo]** `appInteraction`, **[!UICONTROL Nome de exibição]** `App Interaction` e selecione `Object` na lista **[!UICONTROL Tipo]**.

1. Selecione **[!UICONTROL Aplicar]**.

   ![Adicionando novo evento de ação do aplicativo](assets/schema-datatype-app-action.png){zoomable="yes"}

1. Para medir com que frequência uma ação ocorreu, adicione um campo selecionando o botão ![Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) ao lado do objeto **[!UICONTROL appInteraction]** que você criou.

1. Dê a ele um camel-case **[!UICONTROL Nome do campo]** `appAction`, **[!UICONTROL Nome de exibição]** de `App Action` e **[!UICONTROL Tipo]** `Measure`.

   Esta etapa seria equivalente a um evento bem-sucedido no Adobe Analytics.

1. Selecione **[!UICONTROL Aplicar]**.

   ![Adicionando campo de nome da ação](assets/schema-datatype-action-name.png){zoomable="yes"}

1. Adicione um campo descrevendo o tipo de interação selecionando o botão ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) ao lado do objeto **[!UICONTROL appInteraction]**.

1. Dê a ele um **[!UICONTROL Nome do campo]** `name`, **[!UICONTROL Nome de exibição]** de `Name` e **[!UICONTROL Tipo]** `String`.

   Esta etapa é equivalente a uma dimensão no Adobe Analytics.

   ![Selecionando aplicar](assets/schema-datatype-apply.png){zoomable="yes"}

1. Role para baixo do painel direito e selecione **[!UICONTROL Aplicar]**.

1. Para criar um objeto `appStateDetails` contendo um campo **[!UICONTROL Measure]** chamado `screenView` e dois campos **[!UICONTROL String]** chamados `screenName` e `screenType`, siga as mesmas etapas usadas ao criar o objeto **[!UICONTROL appInteraction]**.

1. Selecione **[!UICONTROL Salvar]**.

   ![Estado final do tipo de dados](assets/schema-datatype-final.png){zoomable="yes"}

## Adicionar um grupo de campos personalizado

Agora, adicione um grupo de campos personalizados usando seu tipo de dados personalizado:

1. Abra o schema criado anteriormente nesta lição.

1. Selecione ![Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Adicionar]** ao lado de **[!UICONTROL Grupos de campos]**.

   ![Adicionando novo grupo de campos](assets/schema-fieldgroup-add.png){zoomable="yes"}

1. Selecione **[!UICONTROL Criar novo grupo de campos]**.

1. Forneça um **[!UICONTROL Nome de exibição]** e uma **[!UICONTROL Descrição]**, por exemplo, `App Interactions` e `Fields for app interactions`.

1. Selecione **Adicionar grupos de campos**.

   ![Fornecendo nome e descrição](assets/schema-fieldgroup-name.png){zoomable="yes"}

1. Na tela de composição principal, selecione **[!UICONTROL Interações de Aplicativo**].

1. Adicione um campo à raiz do esquema selecionando o botão ![Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) ao lado do nome do esquema.

1. No painel direito, forneça um **[!UICONTROL Nome do campo]** de `appInformation`, um **[!UICONTROL Nome de exibição]** de `App Information` e um **[!UICONTROL Tipo]** de `App Information`.

1. Selecione **[!UICONTROL Interações do aplicativo]** no menu suspenso **[!UICONTROL Grupo de campos]** para atribuir os campos ao novo grupo de campos.

1. Selecione **[!UICONTROL Aplicar]**.

1. Selecione **[!UICONTROL Salvar]**.

   ![Selecionando aplicar](assets/schema-fieldgroup-apply.png){zoomable="yes"}

>[!NOTE]
>
>Os grupos de campos personalizados são sempre posicionados no identificador da organização da Experience Cloud.


>[!SUCCESS]
>
>Agora você tem um esquema para usar no restante do tutorial.
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-os nesta [postagem de discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Próximo: **[Criar uma [!UICONTROL sequência de dados]](create-datastream.md)**
