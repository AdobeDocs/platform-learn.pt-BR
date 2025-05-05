---
title: Enviar dados para o Experience Platform com o SDK móvel da Platform
description: Saiba como enviar dados para o Experience Platform.
solution: Data Collection,Experience Platform
feature: Mobile SDK,Data Ingestion
jira: KT-14637
exl-id: fdd2c90e-8246-4d75-a6db-df3ef31946c4
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 2%

---

# Enviar dados para o Experience Platform

Saiba como enviar dados do aplicativo móvel para o Adobe Experience Platform.

Esta lição opcional é relevante para todos os clientes do Real-time Customer Data Platform (Real-Time CDP), Journey Optimizer e Customer Journey Analytics. o Experience Platform, a base dos produtos Experience Cloud, é um sistema aberto que transforma todos os seus dados (Adobe e não Adobe) em perfis robustos de clientes. Esses perfis do cliente são atualizados em tempo real e usam insights orientados por IA para ajudar você a fornecer as experiências certas em cada canal.

Os dados de [evento](events.md), [ciclo de vida](lifecycle-data.md) e [identidade](identity.md) que você coletou e enviou para o Platform Edge Network em lições anteriores são encaminhados para os serviços configurados em sua sequência de dados, incluindo o Adobe Experience Platform.

![Arquitetura](assets/architecture-aep.png)


## Pré-requisitos

Sua organização deve ser provisionada e as permissões devem ser concedidas para o Adobe Experience Platform.

Se você não tiver acesso, poderá [ignorar esta lição](install-sdks.md).

## Objetivos de aprendizagem

Nesta lição, você vai:

* Crie um conjunto de dados de Experience Platform.
* Configure seu fluxo de dados para encaminhar dados para o Experience Platform.
* Validar dados no conjunto de dados.
* Ative seu esquema e conjunto de dados para o Perfil de cliente em tempo real.
* Validar dados no Perfil do cliente em tempo real.
* Validar dados no gráfico de identidade.


## Criar um conjunto de dados

Todos os dados assimilados com sucesso na Adobe Experience Platform são mantidos no data lake como conjuntos de dados. Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados (normalmente uma tabela) que contém um esquema (colunas) e campos (linhas). Os conjuntos de dados também contêm metadados que descrevem vários aspectos dos dados armazenados. Consulte a [documentação](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=pt-BR) para obter mais informações.

1. Navegue até a interface do Experience Platform, selecionando-a no menu Aplicativos ![Aplicativos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg), no canto superior direito.


1. Selecione **[!UICONTROL Conjuntos de dados]** no menu de navegação esquerdo.

1. Selecione ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Criar conjunto de dados]**.

1. Selecione **[!UICONTROL Criar conjunto de dados do esquema]**.
   ![início do conjunto de dados](assets/dataset-create.png)

1. Procure pelo esquema. por exemplo, usando `Luma Mobile` no campo de pesquisa.
1. Selecione seu esquema, por exemplo **[!DNL Luma Mobile App Event Schema]**.

1. Selecione **[!UICONTROL Próximo]**.
   ![configuração de conjunto de dados](assets/dataset-configure.png)

1. Forneça um **[!UICONTROL Nome]**, por exemplo `Luma Mobile App Events Dataset` e uma **[!UICONTROL Descrição]**.

1. Selecione **[!UICONTROL Concluir]**.
   ![término do conjunto de dados](assets/dataset-finish.png)


## Adicionar serviço de sequência de dados do Adobe Experience Platform

Para enviar seus dados XDM do Edge Network para o Adobe Experience Platform, adicione o serviço Adobe Experience Platform à sequência de dados configurada como parte de [Criar uma sequência de dados](create-datastream.md).

>[!IMPORTANT]
>
>Você só pode ativar o serviço Adobe Experience Platform ao criar um conjunto de dados de evento.

1. Na interface da Coleção de dados, selecione **[!UICONTROL Sequências de dados]** e a sequência de dados.

1. Em seguida, selecione ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Adicionar Serviço]**.

1. Selecione **[!UICONTROL Adobe Experience Platform]** na lista [!UICONTROL Serviço].

1. Habilite o serviço alternando **[!UICONTROL Habilitado]** em.

1. Selecione o **[!UICONTROL Conjunto de Dados do Evento]** criado anteriormente, por exemplo **[!DNL Luma Mobile App Event Dataset]**.

1. Selecione **[!UICONTROL Salvar]**.

   ![Adicionar o Adobe Experience Platform como um serviço de sequência de dados](assets/datastream-service-aep.png)
1. A configuração final deve ser semelhante a esta.

   ![configurações de sequência de dados](assets/datastream-settings.png)


## Validar dados no conjunto de dados

Agora que você criou um conjunto de dados e atualizou seu fluxo de dados para enviar dados para o Experience Platform, todos os dados XDM enviados para o Platform Edge Network são encaminhados para a Platform e chegam ao conjunto de dados.

Abra o aplicativo e navegue até as telas onde você está rastreando eventos. Você também pode acionar medições de ciclo de vida.

Abra o conjunto de dados na interface da Platform. Você deve ver os dados que chegam em lotes ao conjunto de dados. Normalmente, os dados chegam em microlotes a cada 15 minutos, portanto, talvez você não veja os dados imediatamente.

![validar lotes do conjunto de dados da plataforma de aterrissagem de dados](assets/platform-dataset-batches.png)

Você também pode ver registros e campos de exemplo usando o recurso **[!UICONTROL Visualizar conjunto de dados]**:
![validar ciclo de vida enviado ao conjunto de dados da plataforma](assets/lifecycle-platform-dataset.png)

Uma ferramenta mais robusta para validação de dados é o [serviço de consulta](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html?lang=pt-BR) da Platform.

## Ativar o Perfil do cliente em tempo real

O Perfil do cliente em tempo real do Experience Platform permite criar uma visualização integral de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, de CRM e de terceiros. O Perfil permite consolidar dados diferentes do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

### Ativar o esquema

1. Abra seu esquema, por exemplo **[!DNL Luma Mobile App Event Schema]**.
1. Habilitar **[!UICONTROL Perfil]**.
1. Selecione **[!UICONTROL Os dados deste esquema conterão uma identidade principal no campo identityMap.]** no diálogo.
1. **[!UICONTROL Salve]** o esquema.

   ![habilitar o esquema para o perfil](assets/platform-profile-schema.png)

### Ativar o conjunto de dados

1. Abra seu conjunto de dados, por exemplo **[!DNL Luma Mobile App Event Dataset]**.
1. Habilitar **[!UICONTROL Perfil]**.

   ![habilitar o conjunto de dados para o perfil](assets/platform-profile-dataset.png)

### Validar dados no perfil

Abra o aplicativo e navegue até as telas onde você está rastreando eventos, por exemplo: faça logon no aplicativo Luma e faça uma compra.

Use o Assurance para localizar uma das identidades transmitidas no identityMap (Email, lumaCrmId ou ECID), por exemplo, a ID do CRM.

![obter um valor de identidade](assets/platform-identity.png)

Na interface da Platform,

1. Navegue até **[!UICONTROL Perfis]** e selecione **[!UICONTROL Procurar]** na barra superior.
1. Especifique os detalhes de identidade que você acabou de capturar, por exemplo `Luma CRM ID` para **[!UICONTROL Namespace de identidade]** e o valor copiado para **[!UICONTROL Valor de identidade]**. Em seguida, selecione **[!UICONTROL Exibir]**.
1. Para exibir detalhes, selecione o perfil.

![pesquisar um valor de identidade](assets/platform-profile-lookup.png)

Na tela **[!UICONTROL Detalhes]**, você pode ver informações básicas sobre o usuário, incluindo as **[!UICONTROL **&#x200B; identidades vinculadas &#x200B;**]**:
![detalhes do perfil](assets/platform-profile-details.png)

No **[!UICONTROL Eventos]**, você pode ver os eventos coletados da implementação do aplicativo móvel para este usuário:

![eventos de perfil](assets/platform-profile-events.png)


Na tela de detalhes do perfil:

1. Para exibir o gráfico de identidade, clique no link ou navegue até **[!UICONTROL Identidades]** e selecione **[!UICONTROL Gráfico de identidade]** na barra superior.
1. Para pesquisar o valor de identidade, especifique `Luma CRM ID` como o **[!UICONTROL Namespace de identidade]** e o valor copiado como o **[!UICONTROL Valor de identidade]**. Em seguida, selecione **[!UICONTROL Exibir]**.

   Esta visualização mostra todas as identidades que estão vinculadas em um perfil e suas origens. Este é um exemplo de um gráfico de identidade construído com dados coletados ao concluir este tutorial do SDK móvel (Data Source 2) e o [tutorial do SDK da Web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=pt-BR) (Data Source 1):

   ![obter um valor de identidade](assets/platform-profile-identitygraph.png)


## Próximas etapas

Os profissionais de marketing e análise podem fazer muito mais com dados capturados no Experience Platform, inclusive analisá-los no Customer Journey Analytics e criar segmentos no Real-time Customer Data Platform. Você está indo para um bom começo!


>[!SUCCESS]
>
>Agora você configurou o aplicativo para enviar dados não apenas para o Edge Network, mas também para o Adobe Experience Platform.<br>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-os nesta [postagem de Discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Próximo: **[Criar e enviar notificações por push](journey-optimizer-push.md)**
