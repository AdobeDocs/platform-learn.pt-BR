---
title: Criar um esquema XDM para dados da Web
description: Saiba como criar um esquema XDM para dados da Web na interface da Coleta de dados. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Schemas
exl-id: 2858ce03-4f95-43ac-966c-1b647b33ef16
source-git-commit: fc0567823039f8a2005aa64a3f10c5a2564cbf64
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 5%

---

# Criar um esquema XDM para dados da Web

Saiba como criar um esquema XDM para dados da Web na interface da Coleta de dados.

Os esquemas do Experience Data Model (XDM) são os blocos fundamentais, os princípios e as práticas recomendadas para a composição de schemas no Adobe Experience Platform.

O SDK da Web da plataforma usa seu esquema para padronizar os dados de eventos da Web, enviá-los para a Rede de borda da plataforma e, em última análise, encaminhar os dados para qualquer aplicativo Experience Cloud configurado no armazenamento de dados. Essa etapa é essencial, pois define um modelo de dados padrão necessário para assimilar dados de experiência do cliente no Experience Platform e permite serviços e aplicativos de downstream baseados nesses padrões.

>[!NOTE]
>
> Para fins de demonstração, os exercícios nesta lição criam um schema de exemplo para capturar o conteúdo exibido e os produtos comprados pelos clientes na [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Embora você possa usar essas etapas para criar um schema diferente para seus próprios propósitos, é recomendável seguir para criar o schema de exemplo e aprender os recursos do editor de esquema.

Para saber mais sobre esquemas XDM, faça o curso &quot;[Modelar seus dados de experiência do cliente com o XDM](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)&quot; ou veja o [Visão geral do sistema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=pt-BR).

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Criar um esquema XDM na interface da Coleta de dados
* Adicionar grupos de campos ao esquema XDM
* Criar esquemas XDM para dados de eventos da Web usando práticas recomendadas

## Pré-requisitos

Todo o provisionamento e permissões de usuário necessários para a Coleta de dados e a Adobe Experience Platform, descritos na seção [Configurar permissões](configure-permissions.md) lição.

## Criar um esquema do XDM

Os esquemas XDM são a maneira padrão de descrever dados no Experience Platform, permitindo que todos os dados que estão em conformidade com os esquemas sejam reutilizados em uma organização sem conflitos ou até mesmo compartilhados entre várias organizações. Para saber mais, consulte a [noções básicas da composição do Schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=pt-BR).

Neste exercício, você criará um esquema XDM usando os grupos de campos de linha de base recomendados para capturar dados de eventos da Web no [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target=&quot;_blank&quot;}:

1. Abra o [Interface da Coleta de dados](https://launch.adobe.com/){target=&quot;_blank&quot;}
1. Certifique-se de que você está na sandbox correta

   >[!NOTE]
   >
   >Se você for o cliente de um aplicativo baseado em plataforma, como a CDP em tempo real, recomendamos usar uma sandbox de desenvolvimento para este tutorial. Caso contrário, use a variável **[!UICONTROL Prod]** sandbox.

1. Ir para **[!UICONTROL Esquemas]** na navegação à esquerda
1. Selecione o **[!UICONTROL Criar esquema]** no canto superior direito
1. No menu suspenso , selecione **[!UICONTROL ExperiênciaEvento XDM]**

![Evento de experiência de esquema](assets/schema-XDM-experience-event.jpg)

## Adicionar grupos de campos

Como mencionado anteriormente, o XDM é a estrutura principal que padroniza os dados de experiência do cliente fornecendo estruturas e definições comuns para uso nos serviços downstream da Adobe Experience Platform. Ao seguir os padrões XDM, _todos os dados de experiência do cliente_ podem ser incorporadas em uma representação comum. Essa abordagem permite obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e expressar atributos do cliente para fins de personalização usando dados de várias fontes. Consulte [Práticas recomendadas para modelagem de dados](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/best-practices.html?lang=en) para obter mais informações.

Quando possível, é recomendável usar grupos de campo existentes e seguir um modelo agnóstico de produto e convenções de nomenclatura. Para quaisquer dados específicos da sua organização que não se encaixem nos grupos de campos predefinidos acima, é possível criar um grupo de campos personalizado. Consulte [Criação de um esquema usando o Editor de esquemas](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en#create) para obter etapas mais detalhadas sobre schemas personalizados.

>[!TIP]
> 
>Neste exercício, você adiciona os grupos de campos predefinidos recomendados para a coleta de dados da Web: _**[!UICONTROL AEP Web SDK ExperienceEvent]**_ e _**[!UICONTROL Evento de experiência do consumidor]**_.

1. No **[!UICONTROL Grupos de campos]** seção , selecione **[!UICONTROL Adicionar]**
1. Procurar por [!UICONTROL `AEP Web SDK ExperienceEvent`]
1. Marque a caixa
1. Procurar por [!UICONTROL `Consumer Experience Event`]
1. Marque a caixa
1. Selecionar **[!UICONTROL Adicionar grupos de campos]**

   ![Adicionar grupo de campos](assets/schema-add-field-group.jpg)

Com os grupos de campos selecionados, você está pronto para nomear o esquema. Uma convenção de nomenclatura comum para esquemas XDM é nomear o esquema após a fonte de dados:

1. No **[!UICONTROL Composição**] selecione o `Untitled schema name`
1. No **[!UICONTROL Propriedades do schema]** , digite o **[!UICONTROL Nome de exibição]** `Luma Web Event Data`
1. Selecione qualquer coisa fora do **[!UICONTROL Nome de exibição]** para ativar o **[!UICONTROL Salvar]** opção
1. Selecione **[!UICONTROL Salvar]**

![Dados de evento da Web Luma](assets/schema-luma-web-event-data.png)

Com ambos os grupos de campos, observe que você tem acesso aos pares de valores chave mais usados e necessários para a coleta de dados na Web. O [!UICONTROL nome de exibição] de cada campo é exibido aos profissionais de marketing na interface do construtor de segmentos de aplicativos baseados em plataforma e você pode alterar o nome de exibição dos campos padrão para atender às suas necessidades. Também é possível remover campos que não deseja. Quando você clica em um dos nomes de grupo de campos, a interface destaca quais agrupamentos de pares de valor chave pertencem a ele. No exemplo abaixo, você vê a quais grupos pertencem **[!UICONTROL Evento de experiência do consumidor]**.

![Grupos de campos de esquema](assets/schema-consumer-experience-event.jpg)

Esta lição é apenas um ponto de partida. Ao criar seu próprio esquema de eventos da Web, você deve explorar e documentar seus requisitos comerciais. Esse processo é semelhante à criação de um [Documento de requisitos comerciais](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-a-business-requirements-document.html?lang=pt-BR) e [Referência de design da solução](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr.html) para uma implementação do Adobe Analytics, mas deve incluir requisitos para _todos os destinatários de dados de downstream_ como destinos de encaminhamento de plataforma, Target e evento.


### O objeto identityMap

Há um conjunto especial de dados necessários para identificar usuários da Web chamados de `[!UICONTROL identityMap]`.

![Dados de evento da Web Luma](assets/schema-identityMap.png)

É um objeto obrigatório para qualquer coleta de dados relacionada à Web, pois hospeda a ID de Experience Cloud necessária para identificar usuários na Web. Também é a chave para definir IDs internas do cliente para usuários autenticados. `[!UICONTROL identityMap]` O é discutido mais na seção [Configurar identidades](configure-identities.md) lição. Ele é incluído automaticamente em todos os schemas usando o **[!UICONTROL ExperiênciaEvento XDM]** classe .


>[!IMPORTANT]
>
> É possível ativar **[!UICONTROL Perfil]** para um esquema antes de salvar o esquema. **Não** ative-a neste ponto. Depois que um esquema é ativado para o Perfil, ele não pode ser desativado ou excluído. Além disso, os campos não podem ser removidos do schema após esse ponto. Essas implicações são importantes que você deve ter em mente posteriormente ao trabalhar com seus próprios dados no ambiente de produção.
>
>Essa configuração é discutida mais durante o [Experience Platform de configuração](setup-experience-platform.md) lição.
>![Esquema de perfil](assets/schema-profile.png)

Agora é possível fazer referência a esse esquema ao adicionar a extensão do SDK da Web à propriedade da tag .


[Próximo: ](configure-identities.md)

>[!NOTE]
>
>Obrigado por investir seu tempo para aprender sobre o SDK da Web da Adobe Experience Platform. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
