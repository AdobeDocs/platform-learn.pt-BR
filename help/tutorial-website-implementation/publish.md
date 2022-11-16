---
title: Publicar sua propriedade de tag
description: Saiba como publicar sua propriedade de tag do ambiente de desenvolvimento para os ambientes de preparo e produção . Esta lição é parte do tutorial Implementar o Experience Cloud em sites da Web.
exl-id: dec70472-cecc-4630-b68e-723798f17a56
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 72%

---

# Publicar sua propriedade de tag

Depois de implementar algumas das soluções principais da Adobe Experience Cloud no ambiente de desenvolvimento, é hora de aprender o fluxo de trabalho de publicação.

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo integrado à Adobe Experience Platform como um conjunto de tecnologias de coleção de dados. Várias alterações de terminologia foram implementadas na interface de que você deve estar ciente ao usar este conteúdo:
>
> * O Platform launch (lado do cliente) agora está **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)**
> * Agora o lado do servidor do Platform launch **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * As configurações de borda agora são **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=pt-BR)**


## Objetivos de aprendizagem

No final desta lição, você poderá:

1. Publicar uma biblioteca de desenvolvimento no ambiente de preparo
1. Mapear uma biblioteca de preparo para seu site de produção usando o Depurador
1. Publicar uma biblioteca de preparo para o ambiente de produção

## Publicar no ambiente de preparo

Agora que você criou e validou sua biblioteca no ambiente de desenvolvimento, é hora de publicá-la no ambiente de preparo.

1. Vá para o **[!UICONTROL Fluxo de publicação]** página

1. Abra a lista suspensa ao lado da biblioteca e selecione **[!UICONTROL Enviar para aprovação]**

   ![Enviar para aprovação](images/publishing-submitForApproval.png)

1. Clique no botão **[!UICONTROL Enviar]** na caixa de diálogo:

   ![Clique em Enviar no modal](images/publishing-submit.png)

1. Sua biblioteca agora aparecerá na coluna [!UICONTROL Enviado] em um estado não construído:

1. Abra a lista suspensa e selecione **[!UICONTROL Criar para Preparo]**:

   ![Criar para preparo](images/publishing-buildForStaging.png)

1. Quando o ícone de ponto verde é exibido, a biblioteca pode ser visualizada no ambiente de preparo.

Em um cenário da vida real, a próxima etapa do processo normalmente deve ser a validação das alterações por parte da sua equipe de controle de qualidade na biblioteca de Preparo. Eles podem fazer isso usando o Debugger.

**Para validar as alterações na biblioteca de Preparo**

1. Na propriedade da tag , abra o [!UICONTROL Ambientes] página

1. Na linha [!UICONTROL Armazenamento], clique no ![ícone Instalar](images/launch-installIcon.png) para abrir o modal

   ![Vá para a página Ambientes e clique para abrir o modal](images/publishing-getStagingCode.png)

1. Clique no ![ícone Copiar](images/launch-copyIcon.png) para copiar o código incorporado na área de transferência

1. Clique em **[!UICONTROL Fechar]** para fechar a modal

   ![Ícone Instalar](images/publishing-copyStagingCode.png)

1. Abra o [site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html) no navegador Chrome

1. Abra a [extensão Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) clicando no ![ícone Depurador](images/icon-debugger.png)

   ![Clique no ícone Depurador](images/switchEnvironments-openDebugger.png)

1. Acesse a guia Ferramentas

1. No **[!UICONTROL Adobe Launch > Substituir código incorporado do Launch]** cole o código incorporado de preparo que está na área de transferência
1. Ative o **[!UICONTROL Aplicar em luma.enablementadobe.com]** switch

1. Clique no ícone do disco para salvar

   ![ambiente de tags mostrado no Debugger](images/switchEnvironments-debugger-save.png)

1. Recarregue e verifique a guia Resumo do Debugger. Na seção Launch, você deve ver que sua propriedade de armazenamento temporário está implementada, mostrando o nome da propriedade (ou seja, &quot;Tags Tutorial&quot; ou o nome que você tenha dado à sua propriedade)!

   ![ambiente de tags mostrado no Debugger](images/publishing-debugger-staging.png)

Na vida real, uma vez que a sua equipe de controle de qualidade tenha se desconectado após analisar as alterações no ambiente de preparo, é hora de publicar na produção.

## Publicar na produção

1. Vá para a página [!UICONTROL Publicação]

1. Na lista suspensa, clique em **[!UICONTROL Aprovar para publicação]**:

   ![Aprovar para publicação](images/publishing-approveForPublishing.png)

1. Clique no botão **[!UICONTROL Aprovar]** na caixa de diálogo:

   ![Clique em Aprovar](images/publishing-approve.png)

1. A biblioteca agora aparecerá na coluna [!UICONTROL Aprovado] no estado não criado (ponto amarelo):

1. Abra a lista suspensa e selecione **[!UICONTROL Criar e publicar na produção]**:

   ![Clique em Criar e publicar na produção](images/publishing-buildAndPublishToProduction.png)

1. Clique em **[!UICONTROL Publicar]** na caixa de diálogo:

   ![Clique em Publicar](images/publishing-publish.png)

1. A biblioteca será exibida na coluna [!UICONTROL Publicado]:

   ![Publicado](images/publishing-published.png)

Pronto! Você concluiu o tutorial e publicou sua primeira propriedade nas tags!
