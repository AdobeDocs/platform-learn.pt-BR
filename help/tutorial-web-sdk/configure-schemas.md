---
title: Criar um esquema XDM para dados da Web
description: Saiba como criar um esquema XDM para dados da Web na interface da Coleção de dados. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Web SDK,Schemas
exl-id: 2858ce03-4f95-43ac-966c-1b647b33ef16
source-git-commit: aeff30f808fd65370b58eba69d24e658474a92d7
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 1%

---

# Criar um esquema XDM para dados da Web

Saiba como criar um esquema XDM para dados da Web na interface da Coleção de dados.

Os esquemas do Experience Data Model (XDM) são os blocos fundamentais, os princípios e as práticas recomendadas para coletar dados no Adobe Experience Platform.

O SDK da Web da Platform usa o esquema para padronizar os dados de eventos da Web, enviá-los para o Edge Network da Platform e, por fim, encaminhar os dados para qualquer aplicativo Experience Cloud configurado no fluxo de dados. Essa etapa é crítica, pois define um modelo de dados padrão necessário para assimilar dados de experiência do cliente no Experience Platform e habilita serviços e aplicativos downstream baseados nesses padrões.

## Por que modelar os dados?

As empresas têm sua própria linguagem para se comunicar sobre seus domínios. As concessionárias de automóveis lidam com marcas, modelos e cilindros. As companhias aéreas lidam com números de voo, classe de serviço e atribuições de assentos. Alguns desses termos são exclusivos de uma empresa específica, alguns são compartilhados entre um setor vertical e alguns são compartilhados por quase todas as empresas. Para termos compartilhados entre um setor vertical ou até mais amplo, você pode começar a fazer coisas poderosas com seus dados ao nomear e estruturar esses termos de uma maneira comum.

Por exemplo, muitas empresas lidam com pedidos. E se, coletivamente, essas empresas decidissem modelar um pedido de maneira semelhante? Por exemplo, e se o modelo de dados consistisse em um objeto com uma `priceTotal` propriedade que representava o preço total do pedido? E se esse objeto também tiver propriedades chamadas? `currencyCode` e `purchaseOrderNumber`? Talvez o objeto da ordem contenha uma propriedade chamada `payments` que seria uma matriz de objetos de pagamento. Cada objeto representaria um pagamento para o pedido. Por exemplo, talvez um cliente tenha pago parte do pedido com um cartão-presente e pago o restante usando um cartão de crédito. Você pode começar a construir um modelo com esta aparência:

```json
{
  "order": {
    "priceTotal": 89.50,
    "currencyCode": "EUR",
    "purchaseOrderNumber": "JWN20192388410012",
    "payments": [
      {
        "paymentType": "gift_card",
        "paymentAmount": 50
      },
      {
        "paymentType": "credit_card",
        "paymentAmount": 39.50
      }
    ]
  }
}
```

Se todas as empresas que lidam com pedidos decidissem modelar seus dados de pedidos de maneira consistente para termos comuns no setor, coisas mágicas poderiam começar a acontecer. As informações poderiam ser trocadas de forma mais fluida dentro e fora da organização, em vez de interpretar e traduzir constantemente os dados (props e evars, alguém?). O aprendizado de máquina poderia entender mais facilmente o que seus dados _significa_ e fornecer insights acionáveis. As interfaces do usuário para encontrar dados relevantes podem se tornar mais intuitivas. Seus dados podem ser perfeitamente integrados a parceiros e fornecedores que estejam seguindo a mesma modelagem.

Esse é o objetivo do Adobe [Experience Data Model](https://business.adobe.com/products/experience-platform/experience-data-model.html). O XDM fornece modelagem prescritiva para dados comuns no setor, além de permitir estender o modelo para suas necessidades específicas. O Adobe Experience Platform é construído com base no XDM e, como tal, os dados enviados para o Experience Platform precisam estar no XDM. Em vez de pensar em onde e como você pode transformar seus modelos de dados atuais em XDM antes de enviar os dados para o Experience Platform, considere adotar o XDM de forma mais abrangente em toda a organização para que a tradução raramente precise ocorrer.


>[!NOTE]
>
> Para fins de demonstração, os exercícios nesta lição criam um schema de exemplo para capturar o conteúdo visualizado e os produtos comprados pelos clientes no [Site de demonstração da Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Embora você possa usar essas etapas para criar um esquema diferente para suas próprias finalidades, recomenda-se seguir primeiro juntamente com a criação do esquema de exemplo para saber mais sobre os recursos do editor de esquema.

Para saber mais sobre esquemas XDM, faça o curso [Modelar seus dados de experiência do cliente com o XDM](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=pt-BR) ou consulte a [Visão geral do sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home).

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Criar um esquema XDM na interface da Coleção de dados
* Adicionar grupos de campos ao esquema XDM
* Criar esquemas XDM para dados de evento da Web usando práticas recomendadas

## Pré-requisitos

Todas as permissões de usuário e provisionamento necessárias para a Coleção de dados e o Adobe Experience Platform descritas na [visão geral](overview.md) página.

## Criar um esquema do XDM

Os esquemas XDM são a maneira padrão de descrever dados no Experience Platform, permitindo que todos os dados em conformidade com os esquemas sejam reutilizados em uma organização sem conflitos ou até mesmo compartilhados entre várias organizações. Para saber mais, consulte a [noções básicas da composição Esquema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition).

Neste exercício, você criará um esquema XDM usando os grupos de campos de linha de base recomendados para capturar dados de eventos da Web no [Site de demonstração da Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}:

1. Abra o [Interface da coleção de dados](https://launch.adobe.com/){target="_blank"}
1. Verifique se você está na sandbox correta. Localize a sandbox no canto superior direito

   >[!NOTE]
   >
   >Se você for o cliente de um aplicativo baseado em plataforma, como o Real-Time CDP ou o Journey Optimizer, recomendamos usar uma sandbox de desenvolvimento para este tutorial. Caso não esteja, use o **[!UICONTROL Prod]** sandbox.

1. Ir para **[!UICONTROL Esquemas]** na navegação à esquerda
1. Selecione o **[!UICONTROL Criar esquema]** botão na parte superior direita

   ![Criar esquema](assets/schema-xdm-create-schema.png)
1. Selecionar **[!UICONTROL Evento de experiência]** na tela a seguir
1. Selecionar **[!UICONTROL Próxima]**

   ![Evento de experiência de esquema](assets/schema-experience-event.png)

1. Insira o nome do esquema em **[!UICONTROL Nome de exibição do esquema]** neste caso, `Luma Web Event Data`

   >[!TIP]
   >
   >Uma convenção de nomenclatura comum para esquemas XDM é nomear o esquema após a origem dos dados.


1. Selecione Concluir

   ![Término do Evento de Experiência de Esquema](assets/schema-name-schema.png)

## Adicionar grupos de campos

Como observado anteriormente, o XDM é a estrutura principal que padroniza os dados de experiência do cliente, fornecendo estruturas e definições comuns para uso nos serviços downstream da Adobe Experience Platform. Ao aderir aos padrões XDM, _todos os dados de experiência do cliente_ podem ser incorporados numa representação comum. Essa abordagem permite obter insights valiosos das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e expressar atributos do cliente para fins de personalização usando dados de várias fontes. Consulte [Práticas recomendadas para modelagem de dados](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/best-practices) para obter mais informações.

Quando possível, é recomendável usar grupos de campo existentes e aderir a um modelo independente de produto e convenções de nomenclatura. Para quaisquer dados específicos da sua organização que não se encaixem nos grupos de campos predefinidos acima, você pode criar um grupo de campos personalizado. Consulte [Criação de um esquema usando o Editor de esquemas](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/create-schema-ui#create) para obter etapas mais detalhadas sobre esquemas personalizados.

>[!TIP]
> 
>Neste exercício, você adiciona os grupos de campos predefinidos recomendados para a coleta de dados da Web: _**[!UICONTROL ExperienceEvent do SDK da Web da AEP]**_ e _**[!UICONTROL Evento de experiência do consumidor]**_.
>
>
> Se você estiver apenas implementando **Adobe Analytics** com o SDK da Web e não enviando dados para o **Experience Platform**, use o [!UICONTROL Modelo de evento de experiência do Adobe Analytics] grupo de campos para definir o esquema XDM. Isso será usado no [Configurar o Analytics](setup-analytics.md) lição.

1. No **[!UICONTROL Grupos de campos]** , selecione **[!UICONTROL Adicionar]**

   ![Novo grupo de campos](assets/schema-new-field-group.png)

1. Pesquisar por [!UICONTROL `AEP Web SDK ExperienceEvent`]
1. Marque a caixa
1. Pesquisar por [!UICONTROL `Consumer Experience Event`]
1. Marque a caixa
1. Selecionar **[!UICONTROL Adicionar grupos de campos]**

   ![Adicionar grupo de campos](assets/schema-add-field-group.png)

Com ambos os grupos de campos, observe que você tem acesso aos pares de valores chave mais usados, necessários para a coleta de dados na Web. A variável [!UICONTROL nome de exibição] de cada campo aparece para os profissionais de marketing na interface do construtor de segmentos dos aplicativos baseados em plataforma e você pode alterar o nome de exibição dos campos padrão para atender às suas necessidades. Também é possível remover campos indesejados. Ao clicar em qualquer nome de grupo de campos, a interface destaca quais agrupamentos de pares de valores chave pertencem a ele. No exemplo abaixo, você pode ver a quais grupos pertencem **[!UICONTROL Evento de experiência do consumidor]**.

![Grupos de campos de esquema](assets/schema-consumer-experience-event.png)

Esta lição é apenas um ponto de partida. Ao criar seu próprio schema de eventos da Web, você deve explorar e documentar seus requisitos de negócios. Esse processo é semelhante à criação de um [Documento de requisitos comerciais](https://experienceleague.adobe.com/en/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-a-business-requirements-document) e [Referência de design da solução](https://experienceleague.adobe.com/en/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr) para uma implementação do Adobe Analytics, mas deve incluir requisitos para _todos os destinatários de dados downstream_ como Destinos de encaminhamento de eventos, Platform e Target.


### O objeto identityMap

Há um campo especial usado para identificar usuários da Web chamado `[!UICONTROL identityMap]`.

![Dados de evento da Web da Luma](assets/schema-identityMap.png)

É um objeto obrigatório para qualquer coleta de dados relacionada à Web, pois abriga a ID de Experience Cloud necessária para identificar usuários na Web. Também é fundamental para definir IDs internas do cliente para usuários autenticados. `[!UICONTROL identityMap]` é discutido mais na seção [Configurar identidades](configure-identities.md) lição. Ele é incluído automaticamente em todos os esquemas que usam a variável **[!UICONTROL XDM ExperienceEvent]** classe.


>[!IMPORTANT]
>
> É possível habilitar **[!UICONTROL Perfil]** para um esquema antes de salvá-lo. **Não** ative-o neste ponto. Depois que um esquema é ativado para o Perfil, ele não pode ser desativado ou excluído. Os campos também não podem ser removidos de esquemas neste ponto, embora seja possível [Substituir campos na interface do usuário](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/field-deprecation-ui#deprecate). Essas implicações são importantes para ter em mente posteriormente quando você estiver trabalhando com seus próprios dados no ambiente de produção.
>
>
>Essa configuração é discutida mais durante o [Configurar Experience Platform](setup-experience-platform.md) lição.
>![Esquema de perfil](assets/schema-profile.png)

Para concluir esta lição, selecione **[!UICONTROL Salvar]** no canto superior direito.

![Salvar esquema](assets/schema-select-save.png)


Agora é possível fazer referência a esse esquema ao adicionar a extensão SDK da Web à propriedade da tag.


[Próximo: ](configure-identities.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar feedback geral ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
