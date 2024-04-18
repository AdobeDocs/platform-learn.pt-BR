---
title: Configurar uma sequência de dados
description: Saiba como habilitar um fluxo de dados e configurar soluções de Experience Cloud. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Web SDK,Tags,Datastreams
exl-id: ca28374a-9fe0-44de-a7ac-0aa046712515
source-git-commit: 15bc08bdbdcb19f5b086267a6d94615cbfe1bac7
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 5%

---

# Configurar uma sequência de dados


>[!CAUTION]
>
>Esperamos publicar grandes alterações neste tutorial na terça-feira, 23 de abril de 2024. Depois desse ponto, muitos exercícios serão alterados e talvez seja necessário reiniciar o tutorial desde o início para concluir todas as lições.

Saiba como habilitar um fluxo de dados e configurar soluções de Experience Cloud.

As sequências de dados informam ao Adobe Experience Platform Edge Network para onde enviar os dados coletados pelo SDK da Web da plataforma. Na configuração dos datastreams, você habilita os aplicativos Experience Cloud, a conta Experience Platform e o encaminhamento de eventos. Consulte a [Princípios básicos da configuração de um fluxo de dados](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=br) para obter informações mais detalhadas.

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Criar um fluxo de dados
* Habilitar os aplicativos Experience Cloud
* Habilitar Experience Platform

## Pré-requisitos

Antes de configurar o fluxo de dados, você já deve ter concluído as seguintes lições:

* [Configurar permissões](configure-permissions.md)
* [Configurar um esquema](configure-schemas.md)
* [Configurar um namespace de identidade](configure-identities.md)

## Criar um fluxo de dados

Agora é possível criar um fluxo de dados para informar ao Platform Edge Network para onde enviar os dados coletados pelo SDK da Web.

**Para criar um fluxo de dados:**

1. Abra o [Interface da coleção de dados](https://launch.adobe.com/){target="_blank"}
1. Verifique se você está na sandbox correta

   >[!NOTE]
   >
   >Se você for o cliente de um aplicativo baseado em plataforma como o Real-Time CDP, recomendamos usar uma sandbox de desenvolvimento para este tutorial. Caso não esteja, use o **[!UICONTROL Prod]** sandbox.

1. Ir para **[!UICONTROL Datastreams]** na navegação à esquerda
1. Selecionar **[!UICONTROL Nova sequência de dados]** no lado direito da tela.
1. Enter `Luma Web SDK` como o **[!UICONTROL Nome]**. Esse nome é referenciado posteriormente ao configurar a extensão do SDK da Web na propriedade da tag.
1. Selecione o `Luma Web Event Data` como o **[!UICONTROL Esquema de evento]**
1. Selecionar **[!UICONTROL Salvar]**

   ![Criar a sequência de dados](assets/datastream-create-datastream.png)

   >[!AVAILABILITY]
   >
   >O recurso de mapeamento será incorporado a este tutorial posteriormente.




Na próxima tela, você poderá adicionar serviços, como aplicativos Adobe, ao fluxo de dados. No entanto, você não adicionará serviços neste ponto do tutorial. Você fará isso mais tarde nas lições [Configurar Experience Platform](setup-experience-platform.md), [Configurar o Analytics](setup-analytics.md), [Configurar Audience Manager](setup-audience-manager.md), [Configurar o Target](setup-target.md)ou [Encaminhamento de evento](setup-event-forwarding.md).

>[!NOTE]
>
>Ao implementar o SDK da Web da Platform em seu próprio site, você deve criar três fluxos de dados para mapear para seus três ambientes de tag (desenvolvimento, preparo e produção). Se estiver usando o SDK da Web da Platform com aplicativos baseados na plataforma, como Adobe Real-time Customer Data Platform ou Adobe Journey Optimizer, certifique-se de criar esses fluxos de dados nas sandboxes da Platform apropriadas.

Agora você está pronto para instalar a extensão SDK da Web da Platform na sua propriedade de tag!

[Próximo: ](install-web-sdk.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
