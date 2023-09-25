---
title: Criar políticas de mesclagem
seo-title: Create merge policies | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Criar políticas de mesclagem
description: Nesta lição, você criará políticas de mesclagem para determinar como os dados são mesclados em perfis.
role: Data Architect, Data Engineer
feature: Profiles
jira: KT-4348
audience: data architect
doc-type: tutorial
activity: implement
thumbnail: 4348-create-merge-policies.jpg
exl-id: ec862bb2-7aa2-4157-94eb-f5af3a94295f
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 1%

---

# Criar políticas de mesclagem

<!--20 min-->

Nesta lição, você criará políticas de mesclagem para priorizar como várias fontes de dados se mesclam em perfis.

O Adobe Experience Platform permite reunir dados de várias fontes e combiná-los para obter uma visualização completa de cada cliente individual. Ao reunir esses dados, as políticas de mesclagem determinam como os dados são priorizados e quais dados são combinados para criar essa visualização unificada.

Manteremos a interface do usuário para esta lição, mas também existem opções de API para criar políticas de mesclagem.

**Arquitetos de dados** O precisará criar políticas de mesclagem fora deste tutorial.

Antes de começar os exercícios, assista a este vídeo curto para saber mais sobre políticas de mesclagem:
>[!VIDEO](https://video.tv.adobe.com/v/330433?learn=on)

## Permissões necessárias

No [Configurar permissões](configure-permissions.md) você configura todos os controles de acesso necessários para concluir esta lição.

<!--* Permission items **[!UICONTROL Profile Management]** > **[!UICONTROL View Merge Policies]** and **[!UICONTROL Manage Merge Policies]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]** and **[!UICONTROL Manage Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## Sobre políticas de mesclagem e esquema de união

Lembre-se, na lição sobre assimilação em lote, carregamos dois registros com informações um pouco diferentes para o mesmo cliente. No [!DNL Loyalty] dados, o nome do cliente foi `Daniel` e ele morava em `New York City`, mas nos dados do CRM o nome do cliente foi `Danny` e ele morava em `Portland`. Os dados do cliente mudam com o tempo. Talvez ele tenha se mudado de `Portland` para `New York City`. Outras coisas também mudam, como números de telefone e endereços de email. As políticas de mesclagem ajudam você a decidir como lidar com esses tipos de conflitos quando duas fontes de dados fornecem informações diferentes para o mesmo usuário.

Então, por que `Danny` ganha como primeiro nome? Vamos dar uma olhada:

1. Na interface do usuário da Platform, selecione **[!UICONTROL Perfis]** na navegação à esquerda
1. Vá para a **[!UICONTROL Políticas de mesclagem]** guia
1. A Política de mesclagem padrão é carimbo de data e hora ordenado. Como você carregou os dados do CRM após os dados de Fidelidade, `Danny` ganhou como o nome no perfil:

![Tela Política de mesclagem](assets/mergepolicies-default.png)

Quando vários esquemas estiverem ativados para perfil, uma variável [!UICONTROL Esquema de união] é criado automaticamente para todos os esquemas de registro ativados por perfil que compartilham uma classe base. É possível exibir a [!UICONTROL Esquemas de união] acessando o **[!UICONTROL Esquema de união]** guia.

![Tela Política de mesclagem](assets/mergepolicies-unionSchema.png)

Observe que não há um esquema de união para a classe ExperienceEvent. Embora os dados do ExperienceEvent ainda caiam no perfil, como são baseados em séries de tempo, cada evento inclui um carimbo de data e hora e as colisões não são um problema.

E se você não gostar dessa política de mesclagem padrão? E se a Luma decidir que seu sistema de CRM deve ser a fonte da verdade quando há um conflito? Para isso, criaremos uma política de mesclagem.

## Criar uma política de mesclagem na interface

1. Na tela Políticas de mesclagem, selecione a variável **[!UICONTROL Criar política de mesclagem]** botão no canto superior direito
1. Como a variável **[!UICONTROL Nome]**, insira `Loyalty Prioritized`
1. Como a variável **[!UICONTROL Esquema]**, selecione **[!UICONTROL Perfil XDM]** (observe que sua classe personalizada, já que são dados de registro, também está disponível para políticas de mesclagem)
1. Para **[!UICONTROL Compilação De Id]**, selecione **[!UICONTROL Gráfico privado]**
1. Para **[!UICONTROL Mesclagem de atributos]**, selecione **[!UICONTROL Prioridade de conjunto de dados]**
1. Arrastar e soltar `Luma Loyalty Dataset` e `Luma CRM Dataset` para o **[!UICONTROL Conjunto de dados]** painel.
1. Verifique se `Luma Loyalty Dataset` está na parte superior arrastando e soltando acima da `Luma CRM Dataset`
1. Selecione o botão **[!UICONTROL Salvar]**
   <!--do i need to explain Private Graph? Is that GA?-->
   ![Política de mesclagem](assets/mergepolicies-newPolicy.png)

## Validar a política de mesclagem

Vamos ver se a política de mesclagem está fazendo o que esperaríamos:

1. Vá para a **[!UICONTROL Procurar]** guia
1. Altere o **[!UICONTROL Política de mesclagem]** para o novo `Loyalty Prioritized` política
1. Como a variável **[!UICONTROL Namespace de identidade]**, use seu `Luma CRM Id`
1. Como a variável **[!UICONTROL Valor de identidade]** use `112ca06ed53d3db37e4cea49cc45b71e`
1. Selecione o **[!UICONTROL Mostrar perfil]** botão
1. `Daniel` está de volta!

![Exibição de um perfil com uma política de mesclagem diferente](assets/mergepolicies-lookupProfileWithMergePolicy.png)

## Criar uma política de mesclagem com conjuntos de dados limitados

Ao criar políticas de mesclagem usando a precedência do conjunto de dados, somente os conjuntos de dados da mesma classe base que você inclui à direita são incluídos no perfil. Vamos configurar outra política de mesclagem

1. Na tela Políticas de mesclagem, selecione a variável **[!UICONTROL Criar política de mesclagem]** botão no canto superior direito
1. Como a variável **[!UICONTROL Nome]**, insira  `Loyalty Only`
1. Como a variável **[!UICONTROL Esquema]**, selecione **[!UICONTROL Perfil XDM]**
1. Para **[!UICONTROL Compilação De Id]**, selecione **[!UICONTROL Nenhum]**
1. Para **[!UICONTROL Mesclagem de atributos]**, selecione **[!UICONTROL Prioridade de conjunto de dados]**
1. Arraste e solte somente a variável `Luma Loyalty Dataset` para **[!UICONTROL Conjunto de dados selecionado]** painel.
1. Selecione o botão **[!UICONTROL Salvar]**

![Política de mesclagem somente de fidelidade](assets/mergepolicies-loyaltyOnly.png)

## Validar a política de mesclagem

Agora vamos ver o que essa política de mesclagem faz:

1. Vá para a **[!UICONTROL Procurar]** guia
1. Altere o **[!UICONTROL Política de mesclagem]** para o novo `Loyalty Only` política
1. Como a variável **[!UICONTROL Namespace de identidade]**, use seu `Luma CRM Id`
1. Como a variável **[!UICONTROL Valor de identidade]** use `112ca06ed53d3db37e4cea49cc45b71e`
1. Selecione o **[!UICONTROL Mostrar perfil]** botão
1. Confirme se nenhum perfil foi encontrado:
   ![Somente Fidelidade, sem pesquisa de ID do CRM.](assets/mergepolicies-loyaltyOnly-noCrmLookup.png)

ID do CRM é um campo de identidade na `Luma Loyalty Dataset`, mas somente as identidades primárias podem ser usadas para pesquisar perfis. Então, vamos pesquisar o perfil usando a identidade primária, `Luma Loyalty Id`&quot;

1. Altere o **[!UICONTROL Namespace de identidade]** para `Luma Loyalty Id`
1. Como a variável **[!UICONTROL Valor de identidade]** use `5625458`
1. Selecione o **[!UICONTROL Mostrar perfil]** botão
1. Selecione a ID do perfil para abrir o perfil
1. Vá para a **[!UICONTROL Atributos]** guia
1. Observe que outros detalhes do perfil do conjunto de dados do CRM, como o número do telefone celular e o endereço de email, não estão disponíveis porque apenas
   ![Os dados do CRM não podem ser visualizados na política Somente fidelidade](assets/mergepolicies-loyaltyOnly-attributes.png)
1. Vá para a **[!UICONTROL Eventos]** guia
1. Os dados do ExperienceEvent estão disponíveis apesar de não serem explicitamente incluídos nos conjuntos de dados da política de mesclagem:
   ![Os eventos podem ser visualizados na política Somente fidelidade](assets/mergepolicies-loyaltyOnly-events.png)

## Mais informações sobre políticas de mesclagem

Na pesquisa de perfil, altere a política de mesclagem usada de volta para `Default Timebased` e selecione o **[!UICONTROL Mostrar perfil]** botão. Danny está de volta!

![Exibição de um perfil com uma política de mesclagem diferente](assets/mergepolicies-backToDanny.png)

O que está acontecendo aqui? Bem, a fusão de perfis não é uma coisa única. Os perfis do cliente em tempo real são montados dinamicamente, com base em vários fatores, incluindo a política de mesclagem usada. É possível criar várias políticas de mesclagem para usar em contextos diferentes, dependendo da visualização do cliente que você deseja.

Um caso de uso importante para políticas de mesclagem é o para governança de dados. Por exemplo, digamos que você assimile dados de terceiros na Platform, que não podem ser usados para casos de uso de personalização, mas _pode_ para casos de uso de publicidade. Você pode criar uma política de mesclagem que exclua esse conjunto de dados de terceiros e usar essa política de mesclagem para criar segmentos para seus casos de uso de publicidade.

## Recursos adicionais

* [Documentação de políticas de mesclagem](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/overview.html)
* [Referência da API de políticas de mesclagem (parte da API de perfil do cliente em tempo real)](https://www.adobe.io/experience-platform-apis/references/profile/#tag/Merge-policies)

Agora vamos para o [estrutura de governança de dados](apply-data-governance-framework.md).
