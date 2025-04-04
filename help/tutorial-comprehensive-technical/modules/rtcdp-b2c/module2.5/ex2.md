---
title: Coleta de dados da Adobe Experience Platform e encaminhamento pelo lado do servidor em tempo real - atualize a sequência de dados para disponibilizar os dados para a propriedade do Servidor de coleta de dados da Adobe Experience Platform
description: Atualize sua sequência de dados para disponibilizar os dados para sua propriedade do Servidor de coleta de dados da Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: 7b5b598e-e54c-4f0f-b260-d643600ee6ca
source-git-commit: 6485bfa1c75c43bb569f77c478a273ace24a61d4
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 1%

---

# 2.5.2 Atualize sua sequência de dados para disponibilizar os dados para sua propriedade do Servidor de coleta de dados da Adobe Experience Platform

## Atualizar a sequência de dados

Em [Introdução](./../../gettingstarted/gettingstarted/ex2.md), você criou seu próprio **[!UICONTROL Datastream]**. Você usou o nome `--aepUserLdap-- - Demo System Datastream`.

Neste exercício, você precisa configurar o **[!UICONTROL Datastream]** para funcionar com sua **propriedade do Servidor de Coleta de Dados**.

Para fazer isso, vá para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Você verá isso. No menu esquerdo, clique em **[!UICONTROL Datastreams]**.

No canto superior direito da tela, selecione o nome da sandbox, que deve ser `--aepSandboxName--`.

![Clique no ícone Configuração do Edge na navegação à esquerda](./images/edgeconfig1b.png)

Procure pela sua **[!UICONTROL Sequência de dados]**, chamada `--aepUserLdap-- - Demo System Datastream`. Clique na **[!UICONTROL Sequência de dados]** para abri-la.

![SDKdaWeb](./images/websdk0.png)

Você verá isso. Clique em **[!UICONTROL + Adicionar Serviço]**.

![SDKdaWeb](./images/websdk3.png)

Selecione o serviço **Encaminhamento de Eventos**. Isso mostrará duas configurações adicionais. Selecione a propriedade Encaminhamento de eventos, que você criou no exercício anterior e que se chama `--aepUserLdap-- - Demo System (DD/MM/YYYY) (Edge)`. Em seguida, selecione **Desenvolvimento** em **Ambiente**. Clique em **Salvar**.

![SDKdaWeb](./images/websdk4.png)

Sua sequência de dados foi atualizada e está pronta para uso.

![SDKdaWeb](./images/websdk8a.png)

A sequência de dados agora está pronta para funcionar com o **[!DNL Event Forwarding property]**.

Próxima etapa: [2.5.3 Criar e configurar um webhook personalizado](./ex3.md)

[Voltar ao módulo 2.5](./aep-data-collection-ssf.md)

[Voltar a todos os módulos](./../../../overview.md)
