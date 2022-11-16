---
title: Coleta de dados do Adobe Experience Platform e encaminhamento pelo lado do servidor em tempo real - Atualize o conjunto de dados para disponibilizar os dados para a propriedade do Servidor de coleta de dados da Adobe Experience Platform
description: Atualize seu Datastream para disponibilizar os dados para sua propriedade do Adobe Experience Platform Data Collection Server
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 0c42350c-c38a-410e-bdab-41aff6024f81
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# 14.2 Atualize seu conjunto de dados para disponibilizar os dados para sua propriedade do Servidor de coleta de dados da Adobe Experience Platform

## 14.2.1 Atualizar o fluxo de dados

Em [Exercício 0.2](./../../modules/module0/ex2.md), você criou seu próprio **[!UICONTROL Datastream]**. Em seguida, você usou o nome `--demoProfileLdap-- - Demo System Datastream`.

Neste exercício, você precisa configurar **[!UICONTROL Datastream]** para trabalhar com seu **[!DNL Data Collection Server property]**.

Para fazer isso, acesse [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Você verá isso. No menu esquerdo, clique em **[!UICONTROL Datastreams]**.

No canto superior direito da tela, selecione o nome da sandbox, que deve ser `--aepSandboxId--`.

![Clique no ícone Configuração de borda no painel de navegação esquerdo](./images/edgeconfig1b.png)

Procure por seu **[!UICONTROL Datastream]**, que é nomeado como `--demoProfileLdap-- - Demo System Datastream`. Clique no seu **[!UICONTROL Datastream]** para abri-lo.

![WebSDK](./images/websdk0.png)

Você verá isso. Clique em **[!UICONTROL + Adicionar serviço]**.

![WebSDK](./images/websdk3.png)

Selecionar o serviço **Encaminhamento de evento**. Isso mostrará duas configurações adicionais. Selecione a propriedade Encaminhamento de eventos, que você criou no exercício anterior e que é nomeada `--demoProfileLdap-- - Demo System (DD/MM/YYYY) (Edge)`. Em seguida, selecione **Desenvolvimento** under **Ambiente**. Clique em **Salvar**.

![WebSDK](./images/websdk4.png)

Seu armazenamento de dados foi atualizado e está pronto para uso.

![WebSDK](./images/websdk8a.png)

Seu armazenamento de dados agora está pronto para trabalhar com seu **[!DNL Event Forwarding property]**.

Próxima etapa: [14.3 Criar e configurar um webhook personalizado](./ex3.md)

[Voltar ao Módulo 14](./aep-data-collection-ssf.md)

[Voltar para todos os módulos](./../../overview.md)
