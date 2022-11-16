---
title: Configurar um namespace de identidade
description: Saiba como configurar namespaces de identidade para usar com o SDK da Web da Adobe Experience Platform. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Identities
exl-id: 7719dff4-6b30-4fa0-acae-7491c3208f15
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 7%

---

# Configurar um namespace de identidade

Saiba como configurar namespaces de identidade para usar com o SDK da Web da Adobe Experience Platform.

O [Serviço de identidade da Adobe Experience Platform](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR) define uma ID de visitante comum em todas as soluções do Adobe para alimentar os recursos do Experience Cloud, como o compartilhamento de público-alvo entre soluções. Você também pode enviar suas próprias IDs do cliente para o Serviço para ativar o direcionamento entre dispositivos e integrações com outros sistemas, como o sistema de CRM (relacionamento com o cliente).

Se o seu site já estiver usando o Serviço de ID do Experience Cloud em seu site, por meio da API de Visitante ou da extensão de tag do Serviço de ID do Experience Cloud, e você quiser continuar usando o serviço ao migrar para o SDK da Web da Adobe Experience Platform, deverá usar a versão mais recente da API de Visitante ou a extensão de tag do Serviço de ID do Experience Cloud. Consulte [Migração de ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en) para obter mais informações.

>[!NOTE]
>
> Para fins de demonstração, os exercícios nesta lição fazem com que você capture os detalhes de identidade de um cliente ficcional conectado ao [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html) usando as credenciais, **usuário: test@adobe.com / senha: teste**. Embora você possa usar essas etapas para criar uma identidade diferente para seus propósitos, para aprender os recursos do Mapa de identidade na interface da Coleta de dados, é recomendável seguir em frente para capturar a identidade de exemplo.

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Entenda os namespaces de identidade
* Crie um namespace de identidade personalizado para capturar uma ID de CRM interna


## Pré-requisitos

Você deve ter completado as lições anteriores:

* [Configurar permissões](configure-permissions.md)
* [Configurar esquemas](configure-schemas.md)

>[!IMPORTANT]
>
>O [Extensão Experience Cloud ID](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) não é necessário ao implementar o SDK da Web da Adobe Experience Platform, pois a biblioteca JavaScript do SDK da Web contém a funcionalidade do serviço de ID de visitante.

## Criar um namespace de identidade

Neste exercício, você cria um namespace de identidade para o campo de identidade personalizado do Luma, `lumaCrmId`. Os namespaces de identidade desempenham um papel essencial na criação de perfis de clientes em tempo real, já que dois valores correspondentes no mesmo namespace permitem que duas fontes de dados formem um gráfico de identidade.

Antes de começar os exercícios, assista a este breve vídeo para saber mais sobre identidade no Adobe Experience Platform:
>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

Agora, crie um namespace para a ID do CRM Luma:

1. Abra o [Interface da Coleta de dados](https://launch.adobe.com/){target=&quot;_blank&quot;}
1. Selecione a sandbox que você está usando para o tutorial
1. Selecionar **[!UICONTROL Identidades]** na navegação à esquerda
1. Selecionar **[!UICONTROL Procurar]**

   Uma lista de namespaces de identidade aparece na interface principal da página, mostrando seus nomes, símbolos de identidade, data da última atualização e se eles são namespaces padrão ou personalizados. O painel direito contém informações sobre a força do gráfico de identidade.

1. Selecionar **[!UICONTROL Criar namespace de identidade]**

   ![Exibir identidades](assets/configure-identities-screen.png)

1. Forneça os detalhes a seguir e selecione **[!UICONTROL Criar]**.

   | Campo | Valor |
   |---------------|-----------|
   | Nome de exibição | ID do CRM Luma |
   | Símbolo de identidade | lumaCrmId |
   | Tipo | ID entre dispositivos |


   ![Criar namespaces](assets/identities-create-namespace.png)


   O namespace de identidade é preenchido na variável **[!UICONTROL Identidades]** tela.

   ![Criar namespaces](assets/configure-identities-namespace-lumaCrmId.png)


>[!INFO]
>
> No [Criar elementos de dados](create-data-elements.md) lição: você aprenderá a usar esse namespace ao enviar identidades à Platform Edge Network.

## Crie o namespace de identidade na sandbox de produção

Devido a uma limitação atual na extensão do SDK da Web, os namespaces de identidade também devem ser criados na sandbox de produção para usar o namespace para enviar dados a uma sandbox de desenvolvimento. Portanto, se você tem usado uma sandbox de desenvolvimento para este tutorial, crie também a variável `Luma CRM ID` namespace na sandbox de produção.

## Recursos adicionais

* Documentação do [Serviço de identidade](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=pt-BR)
* [API do serviço de identidade](https://www.adobe.io/experience-platform-apis/references/identity-service/)

Agora que as identidades estão em vigor, o armazenamento de dados pode ser configurado.

[Próximo: ](configure-datastream.md)

>[!NOTE]
>
>Obrigado por investir seu tempo para aprender sobre o SDK da Web da Adobe Experience Platform. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
