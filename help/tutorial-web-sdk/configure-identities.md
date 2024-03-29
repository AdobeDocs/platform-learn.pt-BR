---
title: Configurar um namespace de identidade
description: Saiba como configurar namespaces de identidade para usar com o Adobe Experience Platform Web SDK. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Web SDK,Tags,Identities
exl-id: 7719dff4-6b30-4fa0-acae-7491c3208f15
source-git-commit: 9f75ef042342e1ff9db6039e722159ad96ce5e5b
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 7%

---

# Configurar um namespace de identidade


>[!CAUTION]
>
>Esperamos publicar alterações importantes neste tutorial na sexta-feira, 15 de março de 2024. Depois desse ponto, muitos exercícios serão alterados e talvez seja necessário reiniciar o tutorial desde o início para concluir todas as lições.

Saiba como configurar namespaces de identidade para usar com o Adobe Experience Platform Web SDK.

A variável [Serviço de identidade da Adobe Experience Platform](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR) O define uma ID de visitante comum em todas as soluções da Adobe para alimentar os recursos da Experience Cloud, como o compartilhamento de público-alvo entre soluções. Você também pode enviar suas próprias IDs do cliente para o Serviço para ativar o direcionamento entre dispositivos e integrações com outros sistemas, como o sistema de CRM (relacionamento com o cliente).

Se o site já estiver usando o Serviço de ID do Experience Cloud no site (por meio da API de visitante ou da extensão de tag do Serviço de ID de Experience Cloud ) e você quiser continuar usando-o ao migrar para o SDK da Web da Adobe Experience Platform, será necessário usar a versão mais recente da API de visitante ou da extensão de tag do Serviço de ID do Experience Cloud. Consulte [Migração de ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en) para obter mais informações.

>[!NOTE]
>
> Para fins de demonstração, os exercícios desta lição permitem capturar os detalhes de identidade de um cliente fictício conectado ao [Site de demonstração da Luma](https://luma.enablementadobe.com/content/luma/us/en.html) usando as credenciais, **user: test@adobe.com / password: test**. Embora você possa usar essas etapas para criar uma identidade diferente para seus próprios fins, para conhecer os recursos do Mapa de identidade na interface da Coleção de dados, recomenda-se seguir primeiro para capturar a identidade de exemplo.

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Entender namespaces de identidade
* Criar um namespace de identidade personalizado para capturar uma ID de CRM interna


## Pré-requisitos

Você já deve ter concluído as lições anteriores:

* [Configurar permissões](configure-permissions.md)
* [Configurar esquemas](configure-schemas.md)

>[!IMPORTANT]
>
>A variável [Extensão do Experience Cloud ID](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) não é necessário ao implementar o Adobe Experience Platform Web SDK, pois a biblioteca JavaScript do SDK da Web contém a funcionalidade do serviço de ID de visitante.

## Criar um namespace de identidade

Neste exercício, você cria um namespace de identidade para o campo de identidade personalizado da Luma, `lumaCrmId`. Os namespaces de identidade desempenham uma função essencial na criação de perfis de clientes em tempo real, pois dois valores correspondentes no mesmo namespace permitem que duas fontes de dados formem um gráfico de identidade.

Antes de começar os exercícios, assista a este vídeo curto para saber mais sobre identidade no Adobe Experience Platform:
>[!VIDEO](https://video.tv.adobe.com/v/27841?learn=on)

Agora, crie um namespace para a ID do CRM da Luma:

1. Abra o [Interface da coleção de dados](https://launch.adobe.com/){target="_blank"}
1. Selecione a sandbox que você está usando para o tutorial

   >[!NOTE]
   >
   >Se você for o cliente de um aplicativo baseado em plataforma como o Real-Time CDP, recomendamos usar uma sandbox de desenvolvimento para este tutorial. Caso não esteja, use o **[!UICONTROL Prod]** sandbox.

1. Selecionar **[!UICONTROL Identidades]** na navegação à esquerda
1. Selecionar **[!UICONTROL Procurar]**

   Uma lista de namespaces de identidade é exibida na interface principal da página, mostrando seus nomes, símbolos de identidade, data da última atualização e se são namespaces padrão ou personalizados. O painel direito contém informações sobre a intensidade do gráfico de identidade.

1. Selecionar **[!UICONTROL Criar namespace de identidade]**

   ![Exibir identidades](assets/configure-identities-screen.png)

1. Forneça os detalhes a seguir e selecione **[!UICONTROL Criar]**.

   | Campo | Valor |
   |---------------|-----------|
   | Nome de exibição | ID do CRM da Luma |
   | Símbolo de identidade | lumaCrmId |
   | Tipo | ID entre dispositivos |


   ![Criar namespaces](assets/identities-create-namespace.png)


   O namespace de identidade é preenchido no campo **[!UICONTROL Identidades]** tela.

   ![Criar namespaces](assets/configure-identities-namespace-lumaCrmId.png)


>[!INFO]
>
> No [Criar elementos de dados](create-data-elements.md) lição, você aprenderá a usar esse namespace ao enviar identidades para a Platform Edge Network.

## Criar o namespace de identidade em sua sandbox de produção

Devido a uma limitação atual na extensão SDK da Web, os namespaces de identidade também devem ser criados na sandbox de produção para usar o namespace para enviar dados a uma sandbox de desenvolvimento. Portanto, se você estiver usando uma sandbox de desenvolvimento para este tutorial, crie também a `Luma CRM ID` namespace na sandbox de produção.

## Recursos adicionais

* [Documentação do Serviço de identidade](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=pt-BR)
* [API do serviço de identidade](https://www.adobe.io/experience-platform-apis/references/identity-service/)

Agora que as identidades estão em vigor, o fluxo de dados pode ser configurado.

[Próximo: ](configure-datastream.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
