---
title: Criar um conjunto de dados
description: Criar um conjunto de dados
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 7705d292-a29c-4977-bcc6-f088a51713ea
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 4%

---

# Criar um conjunto de dados

Além de descrever os dados que você enviará para o Adobe Experience Platform, você precisa de um local para manter os dados. No Adobe Experience Platform, esses buckets onde você pode colocar dados são chamados de conjuntos de dados.

Para criar um conjunto de dados, navegue até o [!UICONTROL Conjuntos de dados] exibir dentro do Adobe Experience Platform.

![Exibição de conjuntos de dados](../../../assets/implementation-strategy/datasets-view.png)

Clique em [!UICONTROL Criar conjunto de dados] no canto superior direito.

Durante o processo de criação do conjunto de dados, selecione [!UICONTROL Criar conjunto de dados a partir do esquema] e selecione [o schema criado anteriormente](create-a-schema.md).

![Seleção de esquema](../../../assets/implementation-strategy/schema-selection.png)

Clique em [!UICONTROL Próxima] e forneça um nome e uma descrição.

![Nome e descrição do conjunto de dados](../../../assets/implementation-strategy/dataset-name-description.png)

Clique em [!UICONTROL Concluir]. Seu conjunto de dados foi criado e está pronto para receber dados.

À medida que você começa a enviar dados para um conjunto de dados, o Adobe Experience Platform validará se os dados que você está tentando colocar no conjunto de dados estão em conformidade com o esquema aplicado. Se os dados não estiverem em conformidade com o esquema, serão rejeitados e não serão colocados no conjunto de dados. Como resultado dessa etapa de validação, os consumidores do conjunto de dados (produtos Adobe, terceiros ou sua própria empresa) podem ter algum nível de certeza em relação à estrutura e à limpeza dos dados do conjunto de dados.

Para obter mais informações sobre como criar conjuntos de dados, consulte [Guia da interface do usuário de conjuntos de dados](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=pt-BR).
