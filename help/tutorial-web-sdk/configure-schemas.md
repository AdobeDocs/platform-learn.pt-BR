---
title: Criar um esquema XDM para dados da Web
description: Saiba como criar um esquema XDM para dados da Web na interface da Coleção de dados. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Web SDK,Tags,Schemas
exl-id: 2858ce03-4f95-43ac-966c-1b647b33ef16
source-git-commit: adbe8f4476340abddebbf9231e3dde44ba328063
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 6%

---

# Criar um esquema XDM para dados da Web

Saiba como criar um esquema XDM para dados da Web na interface da Coleção de dados.

Os esquemas do Experience Data Model (XDM) são os blocos fundamentais, os princípios e as práticas recomendadas para a composição de esquemas no Adobe Experience Platform.

O SDK da Web da Platform usa o esquema para padronizar os dados de eventos da Web, enviá-los para a Rede de borda da Platform e, por fim, encaminhar os dados para qualquer aplicativo Experience Cloud configurado no fluxo de dados. Essa etapa é crítica, pois define um modelo de dados padrão necessário para assimilar dados de experiência do cliente no Experience Platform e habilita serviços e aplicativos downstream baseados nesses padrões.

>[!NOTE]
>
> Para fins de demonstração, os exercícios nesta lição criam um schema de exemplo para capturar o conteúdo visualizado e os produtos comprados pelos clientes no [Site de demonstração da Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Embora você possa usar essas etapas para criar um esquema diferente para suas próprias finalidades, recomenda-se seguir primeiro juntamente com a criação do esquema de exemplo para saber mais sobre os recursos do editor de esquema.

Para saber mais sobre esquemas XDM, faça o curso &quot;[Modelar seus dados de experiência do cliente com o XDM](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=pt-BR)&quot; ou consulte a [Visão geral do sistema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=pt-BR).

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Criar um esquema XDM na interface da Coleção de dados
* Adicionar grupos de campos ao esquema XDM
* Criar esquemas XDM para dados de evento da Web usando práticas recomendadas

## Pré-requisitos

Todas as permissões de usuário e provisionamento necessárias para a Coleção de dados e o Adobe Experience Platform descritas na [Configurar permissões](configure-permissions.md) lição.

## Criar um esquema do XDM

Os esquemas XDM são a maneira padrão de descrever dados no Experience Platform, permitindo que todos os dados em conformidade com os esquemas sejam reutilizados em uma organização sem conflitos ou até mesmo compartilhados entre várias organizações. Para saber mais, consulte a [noções básicas da composição Esquema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=pt-BR).

Neste exercício, você criará um esquema XDM usando os grupos de campos de linha de base recomendados para capturar dados de eventos da Web no [Site de demonstração da Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}:

1. Abra o [Interface da coleção de dados](https://launch.adobe.com/){target="_blank"}
1. Verifique se você está na sandbox correta

   >[!NOTE]
   >
   >Se você for o cliente de um aplicativo baseado em plataforma como o Real-Time CDP, recomendamos usar uma sandbox de desenvolvimento para este tutorial. Caso não esteja, use o **[!UICONTROL Prod]** sandbox.

1. Ir para **[!UICONTROL Esquemas]** na navegação à esquerda
1. Clique no botão **[!UICONTROL Criar esquema]** no canto superior direito
1. No menu suspenso, selecione **[!UICONTROL XDM ExperienceEvent]**

![Evento de experiência de esquema](assets/schema-XDM-experience-event.jpg)

## Adicionar grupos de campos

Como observado anteriormente, o XDM é a estrutura principal que padroniza os dados de experiência do cliente, fornecendo estruturas e definições comuns para uso nos serviços downstream da Adobe Experience Platform. Ao aderir aos padrões XDM, _todos os dados de experiência do cliente_ podem ser incorporados numa representação comum. Essa abordagem permite obter insights valiosos das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e expressar atributos do cliente para fins de personalização usando dados de várias fontes. Consulte [Práticas recomendadas para modelagem de dados](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/best-practices.html?lang=en) para obter mais informações.

Quando possível, é recomendável usar grupos de campo existentes e aderir a um modelo independente de produto e convenções de nomenclatura. Para quaisquer dados específicos da sua organização que não se encaixem nos grupos de campos predefinidos acima, você pode criar um grupo de campos personalizado. Consulte [Criação de um esquema usando o Editor de esquemas](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en#create) para obter etapas mais detalhadas sobre esquemas personalizados.

>[!TIP]
> 
>Neste exercício, você adiciona os grupos de campos predefinidos recomendados para a coleta de dados da Web: _**[!UICONTROL ExperienceEvent do SDK da Web da AEP]**_, e _**[!UICONTROL Evento de experiência do consumidor]**_.

1. No **[!UICONTROL Grupos de campos]** , selecione **[!UICONTROL Adicionar]**
1. Pesquisar por [!UICONTROL `AEP Web SDK ExperienceEvent`]
1. Marque a caixa
1. Pesquisar por [!UICONTROL `Consumer Experience Event`]
1. Marque a caixa
1. Selecione **[!UICONTROL Adicionar grupos de campos]**

   ![Adicionar grupo de campos](assets/schema-add-field-group.jpg)

Com os grupos de campos selecionados, você está pronto para nomear seu esquema. Uma convenção de nomenclatura comum para esquemas XDM é nomear o esquema após a origem dos dados:

1. Na caixa de diálogo **[!UICONTROL Composição**] , selecione a `Untitled schema name`
1. No **[!UICONTROL Propriedades do esquema]** , insira o **[!UICONTROL Nome de exibição]** `Luma Web Event Data`
1. Selecione qualquer coisa fora do **[!UICONTROL Nome de exibição]** campo para ativar o **[!UICONTROL Salvar]** opção
1. Selecione **[!UICONTROL Salvar]**

![Dados de evento da Web da Luma](assets/schema-luma-web-event-data.png)

Com ambos os grupos de campos, observe que você tem acesso aos pares de valores chave mais usados, necessários para a coleta de dados na Web. A variável [!UICONTROL nome de exibição] de cada campo aparece para os profissionais de marketing na interface do construtor de segmentos dos aplicativos baseados em plataforma e você pode alterar o nome de exibição dos campos padrão para atender às suas necessidades. Também é possível remover campos indesejados. Ao clicar em qualquer nome de grupo de campos, a interface destaca quais agrupamentos de pares de valores chave pertencem a ele. No exemplo abaixo, você pode ver a quais grupos pertencem **[!UICONTROL Evento de experiência do consumidor]**.

![Grupos de campos de esquema](assets/schema-consumer-experience-event.jpg)

Esta lição é apenas um ponto de partida. Ao criar seu próprio schema de eventos da Web, você deve explorar e documentar seus requisitos de negócios. Esse processo é semelhante à criação de um [Documento de requisitos comerciais](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-a-business-requirements-document.html?lang=pt-BR) e [Referência de design da solução](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr.html) para uma implementação do Adobe Analytics, mas deve incluir requisitos para _todos os destinatários de dados downstream_ como Destinos de encaminhamento de eventos, Platform e Target.


### O objeto identityMap

Há um conjunto especial de dados necessários para identificar usuários da Web chamados `[!UICONTROL identityMap]`.

![Dados de evento da Web da Luma](assets/schema-identityMap.png)

É um objeto obrigatório para qualquer coleta de dados relacionada à Web, pois abriga a ID de Experience Cloud necessária para identificar usuários na Web. Também é fundamental para definir IDs internas do cliente para usuários autenticados. `[!UICONTROL identityMap]` é discutido mais na seção [Configurar identidades](configure-identities.md) lição. Ele é incluído automaticamente em todos os esquemas que usam a variável **[!UICONTROL XDM ExperienceEvent]** classe.


>[!IMPORTANT]
>
> É possível habilitar **[!UICONTROL Perfil]** para um esquema antes de salvá-lo. **Não** ative-o neste ponto. Depois que um esquema é ativado para o Perfil, ele não pode ser desativado ou excluído. Além disso, os campos não podem ser removidos do esquema após esse ponto. Essas implicações são importantes para ter em mente posteriormente quando você estiver trabalhando com seus próprios dados no ambiente de produção.
>
>Essa configuração é discutida mais durante o [Configurar Experience Platform](setup-experience-platform.md) lição.
>![Esquema de perfil](assets/schema-profile.png)

Agora é possível fazer referência a esse esquema ao adicionar a extensão SDK da Web à propriedade da tag.


[Próximo: ](configure-identities.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar feedback geral ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
