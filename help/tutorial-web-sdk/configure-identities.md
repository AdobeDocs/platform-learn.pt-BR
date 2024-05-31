---
title: Configurar um namespace de identidade
description: Saiba como configurar namespaces de identidade para usar com o Adobe Experience Platform Web SDK. Esta lição é parte do tutorial Implementar a Adobe Experience Cloud com o SDK da web.
feature: Web SDK,Identities
jira: KT-15400
exl-id: 7719dff4-6b30-4fa0-acae-7491c3208f15
source-git-commit: 1a4f2e3813a6db4bef77753525c8a7d40692a4b2
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 12%

---

# Configurar um namespace de identidade

Saiba como configurar namespaces de identidade para usar com o SDK da web da Adobe Experience Platform.

A variável [Serviço de identidade da Adobe Experience Cloud](https://experienceleague.adobe.com/en/docs/id-service/using/home) define uma ID de visitante comum (a ECID) em aplicativos de Adobe baseados em SDK para potencializar recursos de Experience Cloud, como o compartilhamento de público-alvo entre aplicativos. Você também pode enviar suas próprias IDs do cliente para o Serviço para ativar o direcionamento entre dispositivos e integrações com outros sistemas, como o sistema de CRM (relacionamento com o cliente).

A variável [Serviço de identidade da Adobe Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home) (sim, há dois!) O usa as ECIDs e as IDs do cliente para gerar gráficos de identidade, permitindo mesclar atributos e comportamentos em Perfis de clientes em tempo real.

>[!NOTE]
>
>Um namespace de identidade personalizado é _não obrigatório_ para implementar o Adobe Analytics, Adobe Target ou Adobe Audience Manager com o SDK da Web (identidades autenticadas podem ser passadas no `data` em vez do `xdm` como você verá mais tarde). Os namespaces de identidade são necessários para aplicativos nativos da plataforma, como Journey Optimizer, Real-time Customer Data Platform e Customer Journey Analytics. Embora você possa decidir não usar um namespace de identidade em sua própria implementação, espera-se que faça isso como parte deste tutorial.

>[!NOTE]
>
> Para fins de demonstração, os exercícios desta lição permitem capturar os detalhes de identidade de um cliente fictício conectado ao [Site de demonstração da Luma](https://luma.enablementadobe.com/content/luma/us/en.html) usando as credenciais, **usuário: `test@adobe.com` / password: test**.

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Entender namespaces de identidade
* Criar um namespace de identidade personalizado para capturar uma ID de CRM interna


## Pré-requisitos

Você já deve ter concluído as lições anteriores:

* [Configurar esquemas](configure-schemas.md)

>[!IMPORTANT]
>
>A variável [Extensão do Experience Cloud ID](https://exchange.adobe.com/apps/ec/100160/adobe-experience-cloud-id-launch-extension) não é necessário ao implementar o Adobe Experience Platform Web SDK, pois a biblioteca JavaScript do SDK da Web contém a funcionalidade do serviço de ID de visitante.
>
> Se o site já estiver usando o Serviço de ID de Experience Cloud em seu site (por meio da API de visitante ou da extensão de tag do Serviço de ID de Experience Cloud ) e você quiser continuar usando-o ao migrar para o SDK da Web da Adobe Experience Platform, será necessário usar a versão mais recente da API de visitante ou a extensão de tag do Serviço de ID de Experience Cloud. Consulte [Migração de ID](https://experienceleague.adobe.com/en/docs/experience-platform/edge/identity/overview) para obter mais informações.

## Criar um namespace de identidade

Neste exercício, você cria um namespace de identidade para o campo de identidade personalizado da Luma, `lumaCrmId`. Os namespaces de identidade desempenham uma função essencial na criação de perfis de clientes em tempo real, pois dois valores correspondentes no mesmo namespace permitem que duas fontes de dados formem um gráfico de identidade.

Antes de começar os exercícios, assista a este vídeo curto para saber mais sobre identidade no Adobe Experience Platform:

>[!VIDEO](https://video.tv.adobe.com/v/27841?learn=on)

Agora, crie um namespace para a ID do CRM da Luma:

1. Abra o [Interface da coleção de dados](https://launch.adobe.com/){target="_blank"}
1. Selecione a sandbox que você está usando para o tutorial

   >[!NOTE]
   >
   >Se você for o cliente de um aplicativo baseado em plataforma, como o Real-Time CDP ou o Journey Optimizer, recomendamos usar uma sandbox de desenvolvimento para este tutorial. Caso não esteja, use o **[!UICONTROL Prod]** sandbox.

1. Selecionar **[!UICONTROL Identidades]** na navegação à esquerda
1. Selecionar **[!UICONTROL Procurar]**

   Uma lista de namespaces de identidade é exibida na interface principal da página, mostrando seus nomes, símbolos de identidade, data da última atualização e se são namespaces padrão ou personalizados. O painel direito contém informações sobre [!UICONTROL Fortaleza do gráfico de identidade].

1. Selecionar **[!UICONTROL Criar namespace de identidade]**

   ![Exibir identidades](assets/configure-identities-screen.png)

1. Forneça os detalhes a seguir e selecione **[!UICONTROL Criar]**.

   | Campo | Valor |
   |---------------|-----------|
   | Nome de exibição | ID do CRM da Luma |
   | Símbolo de identidade | lumaCrmId |
   | Tipo | ID individual entre dispositivos |


   ![Criar namespaces](assets/identities-create-namespace.png)


   O namespace de identidade é preenchido no campo **[!UICONTROL Identidades]** tela.

   ![Criar namespaces](assets/configure-identities-namespace-lumaCrmId.png)


>[!NOTE]
>
> No [Criar identidades](create-identities.md) lição, você aprenderá a usar esse namespace ao enviar identidades para o Platform Edge Network.

Agora que as identidades estão em vigor, o fluxo de dados pode ser configurado.

[Próximo: ](configure-datastream.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar feedback geral ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
