---
title: Configurar um conjunto de dados
description: Saiba como habilitar um conjunto de dados e configurar soluções do Experience Cloud. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Datastreams
exl-id: ca28374a-9fe0-44de-a7ac-0aa046712515
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 6%

---

# Configurar um conjunto de dados

Saiba como habilitar um conjunto de dados e configurar soluções do Experience Cloud.

Os conjuntos de dados informam a Rede de borda da Adobe Experience Platform onde enviar dados coletados pelo SDK da Web da plataforma. Na configuração dos conjuntos de dados, você habilita seus aplicativos Experience Cloud, sua conta Experience Platform e o encaminhamento do evento. Consulte a [Fundamentos da configuração de um fluxo de dados](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en) para obter informações mais detalhadas.

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Criar um fluxo de dados
* Ativar os aplicativos do Experience Cloud
* Ativar o Experience Platform

## Pré-requisitos

Antes de configurar o armazenamento de dados, você já deve ter concluído as seguintes lições:

* [Configurar permissões](configure-permissions.md)
* [Configurar um schema](configure-schemas.md)
* [Configurar um namespace de identidade](configure-identities.md)

## Criar um fluxo de dados

Agora é possível criar um armazenamento de dados para informar à Rede de borda da plataforma onde enviar dados coletados pelo SDK da Web.

**Para criar um armazenamento de dados:**

1. Abra o [Interface da Coleta de dados](https://launch.adobe.com/){target=&quot;_blank&quot;}
1. Certifique-se de que você está na sandbox correta

   >[!NOTE]
   >
   >Se você for o cliente de um aplicativo baseado em plataforma como o Real-Time CDP, recomendamos usar uma sandbox de desenvolvimento para este tutorial. Caso contrário, use a variável **[!UICONTROL Prod]** sandbox.

1. Ir para **[!UICONTROL Datastreams]** na navegação à esquerda
1. Selecionar **[!UICONTROL Novo fluxo de dados]** no lado direito do ecrã.
1. Digite `Luma Web SDK` como o **[!UICONTROL nome]**. Esse nome é referenciado posteriormente quando você configura a extensão SDK da Web na propriedade da tag.
1. Selecione seu `Luma Web Event Data` como **[!UICONTROL Esquema do evento]**
1. Selecione **[!UICONTROL Salvar]**

   ![Criar o armazenamento de dados](assets/datastream-create-datastream.png)

   >[!AVAILABILITY]
   >
   >O recurso de mapeamento será incorporado a este tutorial em uma data posterior.




Na próxima tela, é possível adicionar serviços, como aplicativos Adobe, ao conjunto de dados, no entanto, você não adicionará serviços neste ponto do tutorial. Fá-lo-á mais tarde nas lições [Configurar Experience Platform](setup-experience-platform.md), [Configurar Analytics](setup-analytics.md), [Configurar Audience Manager](setup-audience-manager.md), [Configurar Target](setup-target.md)ou [Encaminhamento de evento](setup-event-forwarding.md).

>[!NOTE]
>
>Ao implementar o SDK da Web da plataforma em seu próprio site, você deve criar três conjuntos de dados para mapear para seus três ambientes de tags (desenvolvimento, estágio e produção). Se você estiver usando o SDK da Web da plataforma com aplicativos baseados em plataforma, como o Adobe Real-time Customer Data Platform ou o Adobe Journey Optimizer, certifique-se de criar esses conjuntos de dados nas sandboxes apropriadas da Platform.

Agora você está pronto para instalar a extensão SDK da Web da plataforma na propriedade da tag!

[Próximo: ](install-web-sdk.md)

>[!NOTE]
>
>Obrigado por investir seu tempo para aprender sobre o SDK da Web da Adobe Experience Platform. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
