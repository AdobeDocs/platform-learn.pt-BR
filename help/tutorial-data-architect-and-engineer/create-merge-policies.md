---
title: Criar políticas de mesclagem
seo-title: Create merge policies | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Criar políticas de mesclagem
description: Nesta lição, você criará políticas de mesclagem para determinar como os dados se mesclam em perfis.
role: Data Architect, Data Engineer
feature: Profiles
kt: 4348
audience: data architect
doc-type: tutorial
activity: implement
thumbnail: 4348-create-merge-policies.jpg
exl-id: ec862bb2-7aa2-4157-94eb-f5af3a94295f
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 1%

---

# Criar políticas de mesclagem

<!--20 min-->

Nesta lição, você criará políticas de mesclagem para priorizar como várias fontes de dados se mesclam em perfis.

O Adobe Experience Platform permite reunir os dados de várias fontes e combiná-los para ver uma visualização completa de cada cliente individual. Ao unir esses dados, as políticas de mesclagem determinam como os dados são priorizados e quais dados são combinados para criar essa visualização unificada.

Vamos manter a interface do usuário para esta lição, mas as opções de API também existem para criar políticas de mesclagem.

**Arquitetos de dados** O precisará criar políticas de mesclagem fora deste tutorial.

Antes de começar os exercícios, assista a este breve vídeo para saber mais sobre as políticas de mesclagem:
>[!VIDEO](https://video.tv.adobe.com/v/330433?quality=12&learn=on)

## Permissões necessárias

No [Configurar permissões](configure-permissions.md) lição, configure todos os controles de acesso necessários para concluir esta lição.

<!--* Permission items **[!UICONTROL Profile Management]** > **[!UICONTROL View Merge Policies]** and **[!UICONTROL Manage Merge Policies]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]** and **[!UICONTROL Manage Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## Sobre as políticas de mesclagem e o Esquema da União

Você pode se lembrar, na lição sobre assimilação em lote, fizemos upload de dois registros com informações um pouco diferentes para o mesmo cliente. No [!DNL Loyalty] dados, o nome do cliente foi `Daniel` e ele viveu em `New York City`, mas nos dados do CRM o nome do cliente era `Danny` e ele viveu em `Portland`. Os dados do cliente são alterados ao longo do tempo. Talvez ele tenha se mudado de `Portland` para `New York City`. Outras coisas também mudam, como números de telefone e endereços de email. As políticas de mesclagem ajudam você a decidir como lidar com esses tipos de conflitos quando duas fontes de dados fornecem informações diferentes para o mesmo usuário.

Então, por que `Danny` ganha como nome? Vamos dar uma olhada:

1. Na interface do usuário da Plataforma, selecione **[!UICONTROL Perfis]** na navegação à esquerda
1. Vá para o **[!UICONTROL Mesclar Políticas]** guia
1. A Política de Mesclagem padrão é ordenada por carimbo de data e hora. Como você carregou os dados do CRM após os dados de Fidelidade, `Danny` ganhou como o primeiro nome no perfil:

![Tela de Política de Mesclagem](assets/mergepolicies-default.png)

Quando vários esquemas são ativados para perfil, um [!UICONTROL Esquema de união] O é criado automaticamente para todos os esquemas de registro ativados por perfil que compartilham uma classe base. Você pode visualizar o [!UICONTROL Esquemas de união] ao acessar o **[!UICONTROL Esquema de união]** guia .

![Tela de Política de Mesclagem](assets/mergepolicies-unionSchema.png)

Observe que não há um schema de união para a classe ExperienceEvent. Embora os dados do ExperienceEvent ainda apareçam no perfil, porque são baseados em séries de tempo, cada evento inclui um carimbo de data e hora e as colisões não são um problema.

E se você não gostar dessa política de mesclagem padrão? E se Luma decidir que seu sistema de CRM deve ser a fonte de verdade quando há um conflito? Para isso, criaremos uma política de fusão.

## Criar uma política de mesclagem na interface do usuário

1. Na tela Mesclar políticas , selecione o **[!UICONTROL Criar Política de Mesclagem]** no canto superior direito
1. Como **[!UICONTROL Nome]**, insira `Loyalty Prioritized`
1. Como **[!UICONTROL Esquema]**, selecione **[!UICONTROL Perfil XDM]** (observe que sua classe personalizada — já que são dados de registro — também está disponível para políticas de mesclagem)
1. Para **[!UICONTROL Identificação]**, selecione **[!UICONTROL Gráfico privado]**
1. Para **[!UICONTROL Mesclar atributos]**, selecione **[!UICONTROL Precedência do conjunto de dados]**
1. Arrastar e soltar `Luma Loyalty Dataset` e `Luma CRM Dataset` para **[!UICONTROL Conjunto de dados]** painel.
1. Certifique-se de `Luma Loyalty Dataset` está no topo, arrastando-o e soltando-o acima da `Luma CRM Dataset`
1. Selecione o botão **[!UICONTROL Salvar]**
<!--do i need to explain Private Graph? Is that GA?-->
![Política de Mesclagem](assets/mergepolicies-newPolicy.png)

## Validar a política de mesclagem

Vamos ver se a política de mesclagem está fazendo o que esperaríamos:

1. Vá para o **[!UICONTROL Procurar]** guia
1. Altere o **[!UICONTROL Política de mesclagem]** para o novo `Loyalty Prioritized` política
1. Como **[!UICONTROL Namespace de identidade]**, use o `Luma CRM Id`
1. Como **[!UICONTROL Valor de identidade]** use `112ca06ed53d3db37e4cea49cc45b71e`
1. Selecione o **[!UICONTROL Mostrar perfil]** botão
1. `Daniel` está de volta!

![Exibição de um perfil com uma política de mesclagem diferente](assets/mergepolicies-lookupProfileWithMergePolicy.png)

## Criar uma política de mesclagem com conjuntos de dados limitados

Ao criar políticas de Mesclagem usando a precedência do conjunto de dados, somente os conjuntos de dados da mesma classe base que você inclui à direita são incluídos no perfil. Vamos configurar outra política de mesclagem

1. Na tela Mesclar políticas , selecione o **[!UICONTROL Criar Política de Mesclagem]** no canto superior direito
1. Como **[!UICONTROL Nome]**, insira  `Loyalty Only`
1. Como **[!UICONTROL Esquema]**, selecione **[!UICONTROL Perfil XDM]**
1. Para **[!UICONTROL Identificação]**, selecione **[!UICONTROL Nenhum]**
1. Para **[!UICONTROL Mesclar atributos]**, selecione **[!UICONTROL Precedência do conjunto de dados]**
1. Arrastar e soltar somente o `Luma Loyalty Dataset` para **[!UICONTROL Conjunto de dados selecionado]** painel.
1. Selecione o botão **[!UICONTROL Salvar]**

![Política de Mesclagem Somente Fidelidade](assets/mergepolicies-loyaltyOnly.png)

## Validar a política de mesclagem

Agora vamos ver o que essa política de mesclagem faz:

1. Vá para o **[!UICONTROL Procurar]** guia
1. Altere o **[!UICONTROL Política de mesclagem]** para o novo `Loyalty Only` política
1. Como **[!UICONTROL Namespace de identidade]**, use o `Luma CRM Id`
1. Como **[!UICONTROL Valor de identidade]** use `112ca06ed53d3db37e4cea49cc45b71e`
1. Selecione o **[!UICONTROL Mostrar perfil]** botão
1. Confirme se nenhum perfil foi encontrado:
   ![Fidelidade Somente sem pesquisa de ID de CRM.](assets/mergepolicies-loyaltyOnly-noCrmLookup.png)

A ID do CRM é um campo de identidade na `Luma Loyalty Dataset`, mas somente as identidades primárias podem ser usadas para buscar perfis. Então, vamos procurar o perfil usando a identidade primária. `Luma Loyalty Id`&quot;

1. Altere o **[!UICONTROL Namespace de identidade]** para `Luma Loyalty Id`
1. Como **[!UICONTROL Valor de identidade]** use `5625458`
1. Selecione o **[!UICONTROL Mostrar perfil]** botão
1. Selecione a ID do perfil para abrir o perfil
1. Vá para o **[!UICONTROL Atributos]** guia
1. Observe que outros detalhes de perfil do conjunto de dados do CRM, como o número do telefone celular e o endereço de email, não estão disponíveis porque nós somente estamos
   ![Os dados do CRM não podem ser visualizados na política Somente Fidelidade](assets/mergepolicies-loyaltyOnly-attributes.png)
1. Vá para o **[!UICONTROL Eventos]** guia
1. Os dados do ExperienceEvent estão disponíveis, apesar de não incluí-los explicitamente nos conjuntos de dados da política de mesclagem:
   ![Os eventos podem ser visualizados na política Somente fidelidade](assets/mergepolicies-loyaltyOnly-events.png)

## Mais informações sobre políticas de mesclagem

Na pesquisa de perfil, altere a política de mesclagem usada de volta para `Default Timebased` e selecione o **[!UICONTROL Mostrar perfil]** botão. Danny voltou!

![Exibição de um perfil com uma política de mesclagem diferente](assets/mergepolicies-backToDanny.png)

O que está acontecendo aqui? Bem, a mesclagem de perfis não é uma coisa única. Os perfis de clientes em tempo real são montados em tempo real, com base em vários fatores, incluindo qual política de mesclagem é usada. É possível criar várias políticas de mesclagem para usar em diferentes contextos, dependendo de qual visualização do cliente você deseja.

Um caso de uso importante para as políticas de mesclagem é o controle de dados. Por exemplo, digamos que você assimile dados de terceiros na Platform que não podem ser usados para casos de uso de personalização, mas _can_ ser usado para casos de uso de publicidade. Você pode criar uma política de mesclagem que exclui esse conjunto de dados de terceiros e usar essa política de mesclagem para criar segmentos para seus casos de uso de publicidade.

## Recursos adicionais

* [Documentação das Políticas de Mesclagem](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/overview.html)
* [Referência da API de políticas de mesclagem (parte da API de perfil do cliente em tempo real)](https://www.adobe.io/experience-platform-apis/references/profile/#tag/Merge-policies)

Agora vamos para o [estrutura de governança de dados](apply-data-governance-framework.md).
