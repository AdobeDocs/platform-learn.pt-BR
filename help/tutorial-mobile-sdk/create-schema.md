---
title: Criar um esquema do XDM
description: Saiba como criar um esquema XDM para eventos de aplicativos móveis.
exl-id: c6b0d030-437a-4afe-b7d5-5a7831877983
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 6%

---

# Criar um esquema do XDM

Saiba como criar um esquema XDM para eventos de aplicativos móveis.

A padronização e a interoperabilidade são conceitos-chave por trás do Adobe Experience Platform. O Experience Data Model (XDM), impulsionado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.

## O que são esquemas XDM?

O XDM é uma especificação publicamente documentada projetada para melhorar o poder das experiências digitais. Ele fornece estruturas e definições comuns que permitem que qualquer aplicativo se comunique com os serviços da plataforma. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum que pode fornecer insights de uma maneira mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e expressar atributos do cliente para fins de personalização.

A Experience Platform utiliza esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, fica mais fácil manter o significado e, portanto, obter valor dos dados.

Para que os dados possam ser assimilados na Platform, um schema deve ser composto para descrever a estrutura dos dados e fornecer restrições ao tipo de dados que pode ser contido em cada campo. Os esquemas consistem em uma classe base e zero ou mais grupos de campos de esquema.

Para obter mais informações sobre o modelo de composição de schema, incluindo princípios de design e práticas recomendadas, consulte o [noções básicas da composição do schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=pt-BR) ou o curso [Modelar seus dados de experiência do cliente com o XDM](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm).

>[!TIP]
>
>Se você estiver familiarizado com a Referência de design da solução (SDRs) do Analytics, poderá pensar em um esquema como um SDR mais robusto.

## Pré-requisitos

Para concluir a lição, você deve ter permissão para criar um esquema de Experience Platform.

## Objetivos de aprendizagem

Nesta lição, você:

* Criar um schema na interface da Coleta de dados
* Adicionar um grupo de campos padrão ao esquema
* Criar e adicionar um grupo de campos personalizado ao esquema

## Navegar para schemas

1. Faça logon na Adobe Experience Cloud.

1. Abra o alternador de aplicativos e selecione **[!UICONTROL Coleta de dados]**

   ![Menu suspenso 3x3](assets/mobile-schema-navigate1.png)

1. Certifique-se de estar na sandbox do Experience Platform que você está usando para este tutorial.

   >[!NOTE]
   >
   > Os clientes de aplicativos baseados em plataforma como o Real-Time CDP devem usar uma sandbox de desenvolvimento para este tutorial. Outros clientes usarão a sandbox de produção padrão.


1. Selecionar **[!UICONTROL Esquemas]** under **[!UICONTROL Gerenciamento de dados]**.

   ![tela inicial das tags](assets/mobile-schema-navigate3.png)

Agora, você está na página dos schemas principais e recebe uma lista de qualquer schema existente. Também é possível ver as guias correspondentes aos blocos fundamentais de um schema:

* **Grupos de campos** são componentes reutilizáveis que definem um ou mais campos para capturar dados específicos, como detalhes pessoais, preferências de hotel ou endereço.
* **Classes** defina os aspectos comportamentais dos dados que o schema contém. Por exemplo: `XDM ExperienceEvent` captura a série de tempo, os dados do evento e `XDM Individual Profile` captura dados do atributo sobre um indivíduo.
* **Tipos de dados** são usados como tipos de campos de referência em classes ou grupos de campos da mesma forma que campos literais básicos.

As descrições acima são uma visão geral de alto nível. Para obter mais detalhes, consulte a [Blocos de construção do schema](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/schema-building-blocks.html?lang=pt-BR) vídeo ou leitura [Noções básicas da composição do schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=pt-BR) na documentação do produto.

Neste tutorial, você usa o grupo de campos Evento de experiência do consumidor e cria um grupo personalizado para demonstrar o processo.

>[!NOTE]
>
>O Adobe continua a adicionar mais grupos de campos padrão e eles devem ser usados sempre que possível, pois esses campos são entendidos implicitamente pelos serviços do Experience Platform e fornecem maior consistência quando usados em componentes da plataforma. O uso de grupos de campos padrão oferece benefícios tangíveis, como o mapeamento automático nos recursos de Analytics e AI da plataforma.

## Arquitetura do esquema de aplicativo Luma

Em um cenário do mundo real, o processo de design do schema pode ter esta aparência:

* Reunir requisitos comerciais.
* Encontre grupos de campos pré-criados para cobrir o máximo possível de requisitos.
* Crie grupos de campos personalizados para qualquer intervalo.

Para fins de aprendizado, você usará grupos de campos pré-criados e personalizados.

* **Evento de experiência do consumidor**: Grupo de campos pré-construído que tem muitos campos comuns.
* **Informações do aplicativo**: Grupo de campos personalizado projetado para mimetizar os conceitos do TrackState/TrackAction Analytics.

<!--Later in the tutorial, you can [update the schema](lifecycle-data.md) to include the **[!UICONTROL AEP Mobile Lifecycle Details]** field group.-->

## Criar um esquema

1. Selecionar **[!UICONTROL Criar esquema]** para trazer o menu suspenso de opções e selecione **[!UICONTROL ExperiênciaEvento XDM]**.

   ![Selecionar ExperienceEvent do menu suspenso](assets/mobile-schema-create.png)

1. Procurar por `Consumer Experience Event`.

1. Você pode visualizar os campos e/ou ler a descrição para obter mais detalhes antes de selecionar.

1. Marque a caixa de seleção e **[!UICONTROL Adicionar grupos de campos]**.

   ![Seleção do grupo de campos](assets/mobile-schema-select-field-groups.png)

   Você é trazido de volta para a tela principal de composição do schema, onde pode ver todos os campos disponíveis.

1. Dê um nome ao esquema selecionando **[!UICONTROL Esquema sem título]** no canto superior esquerdo e, em seguida, fornecer um **[!UICONTROL Nome de exibição]** &amp; **[!UICONTROL Descrição]**, por exemplo `Luma Tutorial Mobile` e `"Luma App" schema for Adobe Tutorial`

1. Selecione **[!UICONTROL Salvar]**.

   ![Seleção de aplicação](assets/mobile-schema-name-save.png)

>[!NOTE]
>
>Lembre-se de que não é necessário usar todos os campos em um grupo. Se for útil, pense em um esquema como uma camada de dados vazia. No seu aplicativo, você preenche os valores relevantes no momento apropriado.
>
>O `Consumer Experience Event` tem um tipo de dados chamado `Web information`, que descreve eventos como exibição de página e cliques em links. No momento da escrita, não há uma paridade de aplicativos móveis para esse recurso, portanto, você criará o seu próprio.

## Criar um tipo de dados personalizado

Você começa criando um tipo de dados personalizado que descreve os dois eventos:

* Exibição da tela
* Interação do aplicativo

1. Selecione o **[!UICONTROL Tipos de dados]** e selecione **[!UICONTROL Criar tipo de dados]**.

   ![Seleção do menu de tipo de dados](assets/mobile-schema-datatype-create.png)

1. Dê um **[!UICONTROL Nome de exibição]** e **[!UICONTROL Descrição]**, por exemplo `App Information` e `Custom data type describing "Screen Views" & "App Actions"`

   ![Fornecimento de nome e descrição](assets/mobile-schema-datatype-name.png)

   >[!TIP]
   >
   > Sempre use legível, descritivo [!UICONTROL nomes para exibição] para seus campos personalizados, já que essa prática os torna mais acessíveis aos profissionais de marketing quando os campos são exibidos em serviços downstream, como o construtor de segmentos.


1. Para adicionar um campo, selecione o botão (+) .

   Este campo é um objeto de contêiner para interação de aplicativo. Dê-lhe um camelo **[!UICONTROL Nome do campo]** `appInteraction`, **[!UICONTROL nome de exibição]** `App Interaction`e **[!UICONTROL type]** `Object`.

1. Selecionar **[!UICONTROL Aplicar]**.

   ![Adicionar novo evento de ação do aplicativo](assets/mobile-schema-datatype-app-action.png)

1. Para medir a frequência de ocorrência de uma ação, adicione um campo selecionando o botão (+) ao lado do `appInteraction` objeto criado.

1. Dê-lhe um camelo **[!UICONTROL Nome do campo]** `appAction`, **[!UICONTROL nome de exibição]** de `App Action` e **[!UICONTROL type]** `Measure`.

   Essa etapa seria equivalente a um evento bem-sucedido no Adobe Analytics.

1. Selecionar **[!UICONTROL Aplicar]**.

   ![Adição de um campo de nome de ação](assets/mobile-schema-datatype-action-name.png)

1. Adicione um campo descrevendo o tipo de interação selecionando o botão (+) ao lado do `appInteraction` objeto.

1. Dê um **[!UICONTROL Nome do campo]** `name`, **[!UICONTROL nome de exibição]** de `Name` e **[!UICONTROL type]** `String`.

   Essa etapa é equivalente a uma dimensão no Adobe Analytics.

   ![Seleção de aplicação](assets/mobile-schema-datatype-apply.png)

1. Role até a parte inferior do painel direito e selecione **[!UICONTROL Aplicar]**.

1. Siga o mesmo padrão para criar um `appStateDetails` objeto contendo um campo Measure chamado `screenView` e duas strings chamadas `screenName` e `screenType`.

1. Selecione **[!UICONTROL Salvar]**.

   ![Estado final do tipo de dados](assets/mobile-schema-datatype-final.png)

## Adicionar um grupo de campos personalizado

Agora, adicione um grupo de campos personalizado usando seu tipo de dados personalizado:

1. Abra o schema criado anteriormente nesta lição.

1. Selecionar **[!UICONTROL Adicionar]** ao lado de **[!UICONTROL Grupos de campos]**.

   ![Adição de novo grupo de campos](assets/mobile-schema-fieldgroup-add.png)

1. Desta vez, você cria um grupo de campos personalizado selecionando o **[!UICONTROL Criar novo grupo de campos]** botão de opção próximo à parte superior e, em seguida, forneça um nome e uma descrição, por exemplo, `App Interactions` e `Fields for app interactions`.

   ![Fornecimento de nome e descrição](assets/mobile-schema-fieldgroup-name.png)

1. Na tela de composição principal, adicione um campo à raiz do schema.

1. Selecione o (+) ao lado do nome do schema.

1. No painel direito, forneça um **[!UICONTROL Nome do campo]** de `appInformation`, um nome de exibição de `App Information`.

1. Selecionar `App Information` do **[!UICONTROL Tipo]** , o tipo de dados criado no exercício anterior.

1. Selecionar **[!UICONTROL Aplicar]**.

   ![Seleção de aplicação](assets/mobile-schema-fieldgroup-apply.png)

>[!NOTE]
>
>Os grupos de campos personalizados são sempre colocados em seu identificador de organização de Experience Cloud.
>
>`_techmarketingdemos` é substituída pelo valor exclusivo de sua organização.

Agora você tem um schema a ser usado para o restante do tutorial.

Próximo: **[Crie um [!UICONTROL datastream]](create-datastream.md)**

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender sobre o Adobe Experience Platform Mobile SDK. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)