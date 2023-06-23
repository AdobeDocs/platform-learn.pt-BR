---
title: Aplicar a estrutura de governança de dados
seo-title: Apply the data governance framework | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Aplicar a estrutura de governança de dados
description: Nesta lição, você aplicará a estrutura de governança de dados aos dados assimilados na sandbox.
role: Data Architect
feature: Data Governance
jira: KT-4348
thumbnail: 4348-apply-data-governance-framework.jpg
exl-id: 3cc3c794-5ffd-41bf-95d8-be5bca2e3a0f
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 2%

---

# Aplicar a estrutura de governança de dados

<!--15min-->

Nesta lição, você aplicará a estrutura de governança de dados aos dados assimilados na sandbox.

O Adobe Experience Platform Data Governance permite gerenciar dados de clientes e garantir conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha um papel fundamental no Experience Platform em vários níveis, incluindo o controle do uso de dados.

Antes de começar os exercícios, assista a estes pequenos vídeos sobre governança de dados:
>[!VIDEO](https://video.tv.adobe.com/v/36653?quality=12&learn=on)

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&learn=on)

<!--
## Permissions required

In the [Configure Permissions](configure-permissions.md) lesson, you set up all the access controls required to complete this lesson, specifically:

* Permission items **[!UICONTROL Data Governance]** > **[!UICONTROL Manage Usage Labels]**, **[!UICONTROL Manage Data Usage Policies]** and **[!UICONTROL View Data Usage Policies]**
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` Product Profile
-->

## Cenário de negócios

A Luma faz uma promessa aos membros de seu programa de Fidelidade, de que os dados de Fidelidade não serão compartilhados com terceiros. Implementaremos esse cenário no restante da lição.

## Aplicar rótulos de governança de dados

A primeira etapa do processo de governança de dados é aplicar rótulos de governança aos seus dados. Antes de fazer isso, vejamos rapidamente quais rótulos estão disponíveis:

1. Na interface do usuário da Platform, selecione **[!UICONTROL Políticas]** na navegação à esquerda
1. Vá para a **[!UICONTROL Rótulos]** para ver todos os rótulos na conta.

Há muitos rótulos prontos para uso, além de você poder criar os seus próprios por meio da [!UICONTROL Criar rótulo] botão. Há três tipos principais: [!UICONTROL Rótulos de contrato], [!UICONTROL Rótulos de identidade], e [!UICONTROL Rótulos sensíveis] que correspondem a motivos comuns para a restrição dos dados. Cada um dos rótulos tem um [!UICONTROL Nome amigável] e uma curta [!UICONTROL Nome] que é apenas uma abreviação do tipo e um número. Por exemplo, a variável [!DNL C1] O rótulo é para &quot;Nenhuma exportação de terceiros&quot;, que é o que precisamos para nossa política de fidelidade.

![Rótulo de governança de dados](assets/governance-policies.png)

Agora é hora de rotular os dados cujo uso queremos restringir:

1. Na interface do usuário da Platform, selecione **[!UICONTROL Conjuntos de dados]** na navegação à esquerda
1. Abra o `Luma Loyalty Dataset`
1. Vá para a **[!UICONTROL Governança de dados]** guia
1. Você pode aplicar rótulos a campos individuais ou aplicá-los ao conjunto de dados inteiro. Aplicaremos o rótulo a todo o conjunto de dados. Clique no ícone de lápis. Se você não vir o ícone, tente aumentar o tamanho do navegador ou rolar o painel do meio para a direita.
   ![Governança de dados](assets/governance-dataset.png)
1. No modal, expanda a variável **[!UICONTROL Rótulos do contrato]** e verifique a **[!UICONTROL C2]** rótulo
1. Selecione o **[!UICONTROL Salvar alterações]** botão
   ![Governança de dados](assets/governance-applyLabel.png)
1. Retornar ao principal [!UICONTROL Governança de dados] tela, com a tag **[!UICONTROL Mostrar rótulos herdados]** você pode ver como o rótulo foi aplicado a todos os campos no conjunto de dados.
   ![Governança de dados](assets/governance-labelsAdded.png)


<!--adding extra, unnecessary fields from field groups makes it harder to see which fields really need labels-->
<!--Are there any best practices for applying governance labels-->

## Criar políticas de governança de dados

Agora que nossos dados estão rotulados, podemos criar uma política.

1. Na interface do usuário da Platform, selecione **[!UICONTROL Políticas]** na navegação à esquerda
1. Na guia Navegar, já existe uma política pronta para uso chamada &quot;Restrição de exportação de terceiros&quot; que associa o rótulo C2 à ação de marketing [!UICONTROL Exportar para terceiros]- exatamente o que precisamos!
1. Selecione a política e ative-a por meio da **[!UICONTROL Status da política]** alternar
   ![Governança de dados](assets/governance-enablePolicy.png)

Você pode criar suas próprias políticas selecionando o **[!UICONTROL Criar política]** botão. Isso abre um assistente que permite combinar vários rótulos e restrições de ação de marketing.

## Aplicar políticas de governança

A aplicação das políticas de governação é, obviamente, uma componente essencial do quadro. A imposição ocorre downstream quando os dados são ativados e enviados da Platform, especialmente com a Real-time Customer Data Platform, que você pode ou não estar licenciando. De qualquer forma, está fora do escopo deste tutorial. Mas você não é deixado na fila, você pode saber mais sobre como as políticas são aplicadas neste vídeo, que eu enfileirei para a parte relevante. Ele também mostrará o que acontece quando uma política é violada.

>[!VIDEO](https://video.tv.adobe.com/v/33631/?t=151&quality=12&learn=on)


## Recursos adicionais

* [Documentação de governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=pt-BR)
* [Referência da API do serviço de conjunto de dados](https://www.adobe.io/experience-platform-apis/references/dataset-service/)
* [Referência da API do serviço de política de governança](https://www.adobe.io/experience-platform-apis/references/policy-service/)

Agora vamos prosseguir para [serviço de consulta](run-queries.md).
