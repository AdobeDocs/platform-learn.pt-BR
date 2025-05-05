---
title: Adicionar e configurar a extensão do Web SDK
description: Saiba como adicionar e configurar a extensão Web SDK à sua propriedade de tags para fornecer a funcionalidade necessária em lições adicionais para concluir a migração.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16758
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---


# Adicionar e configurar a extensão do Web SDK

Saiba como adicionar e configurar a extensão Web SDK na propriedade Tags para fornecer a funcionalidade necessária em lições adicionais para concluir a migração.
Siga estas etapas para adicionar e configurar a extensão:

1. Navegue até Coleta de dados do Experience Platform. Isso pode ser feito de uma das duas formas a seguir:
   1. Vá para a [interface do Adobe Experience Platform](https://platform.adobe.com/) e selecione **[!UICONTROL Tags]** próximo à parte inferior da navegação à esquerda.

      ![Acessar marcas 1](assets/access-tags-1.jpg)
   1. Se você não tiver acesso à Platform, poderá usar o alternador de aplicativos (9 pontos) na parte superior direita da janela e selecionar Coleção de dados (depois de fazer logon em Experience.Adobe.com).

      ![Acessar marcas 2](assets/access-tags-2.jpg)
1. Localize e selecione a propriedade da tag que você está migrando para o Web SDK.
1. Na navegação à esquerda da propriedade da marca, selecione **[!UICONTROL Extensões]**.
1. Selecione **[!UICONTROL Catálogo]** próximo à parte superior para ver uma lista de todas as extensões disponíveis.
1. Procure e selecione a extensão **[!UICONTROL Adobe Experience Platform Web SDK]** e clique em **[!UICONTROL Instalar]** à direita.

   ![Localizar a Extensão Web SDK](assets/find-the-websdk-extension.jpg){style="border:1px solid lightslategray"}

1. As definições de configuração de extensão são exibidas. Localize a seção Datastreams e defina a sandbox Experience Platform que deseja usar para essa migração (menus suspensos em &quot;Ambiente&quot; para todos os três ambientes). Se você estiver apenas migrando o Adobe Analytics e não enviará dados para o Adobe Experience Platform, escolha a sandbox **Produção**. Se você enviar esses dados de análise comportamental para o Experience Platform para uso nos aplicativos localizados nesse local, escolha a sandbox que deseja usar para isso. No início, você provavelmente desejará selecionar uma sandbox de desenvolvimento até concluir a migração e adicionar/testar o serviço da Platform.
1. É muito importante conectar o código e as configurações aqui, em Tags, à Edge, selecionando os fluxos de dados criados na etapa anterior para ambientes de Produção, Preparo e Desenvolvimento.

   ![Seleção de sequência de dados](assets/choose-datastreams.jpg){style="border:1px solid lightslategray"}

1. Role para baixo e observe que as configurações de **Identidade** estão selecionadas por padrão. Deixe essas caixas de seleção marcadas para ajudar a identificar os visitantes do site corretamente ao migrar para o Web SDK. Mais informações estão disponíveis na documentação, vinculada abaixo.

1. Selecione **[!UICONTROL Salvar]**.

>[!NOTE]
>
>A propriedade Tags agora tem uma instalação e configuração básicas da extensão Web SDK. Usaremos partes da extensão do Web SDK à medida que criamos ou modificamos elementos e regras de dados durante este tutorial de migração, mas não alteraremos mais os itens de configuração de extensão no tutorial. Itens de configuração adicionais podem e devem ser usados para casos de uso adicionais. Para obter a documentação detalhada sobre essas configurações, consulte [Configurar a extensão de tag do Web SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/tags/extensions/client/web-sdk/web-sdk-extension-configuration).
