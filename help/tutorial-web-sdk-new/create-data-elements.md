---
title: Criar elementos de dados
description: Saiba como criar um objeto XDM e mapear elementos de dados para ele em tags. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Tags
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 1%

---

# Criar elementos de dados

Saiba como criar os elementos de dados essenciais necessários para capturar dados com o SDK da Web do Experience Platform. Capturar dados de conteúdo e de identidade no [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Saiba como usar o esquema XDM criado anteriormente para coletar dados usando o tipo de elemento de dados do SDK da Web da plataforma chamado Variável.

>[!NOTE]
>
> Para fins de demonstração, os exercícios desta lição baseiam-se no exemplo usado durante [Configurar um esquema](configure-schemas.md) etapa; criação de objetos XDM de exemplo que capturam o conteúdo visualizado e as identidades dos usuários na [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html).

>[!IMPORTANT]
>
>Os dados para esta lição vêm do `[!UICONTROL digitalData]` camada de dados no site Luma. Para visualizar a camada de dados, abra o console do desenvolvedor e digite `[!UICONTROL digitalData]` para ver a camada de dados completa disponível.![camada de dados digitalData](assets/data-element-data-layer.png)


Independentemente do SDK da Web da Platform, você deve continuar criando elementos de dados dentro da propriedade de tags, que mapeiam para variáveis de coleção de dados do seu site, como uma camada de dados, atributo HTML ou outros. Depois de criar esses elementos de dados, você deve mapeá-los para o esquema XDM criado durante o [configurar schemas](configure-schemas.md) lição. Portanto, a criação de elementos de dados consiste em duas ações:

1. Mapear variáveis de site para elementos de dados e
1. Mapeamento desses elementos de dados para um objeto XDM

Para a etapa 1, você continua a mapear a camada de dados para elementos de dados da maneira que faz no momento, usando qualquer um dos tipos de elementos de dados da extensão de tag principal. Para a etapa 2, a extensão SDK da Web da Platform tem os seguintes tipos de elementos de dados disponíveis:

* ID de mesclagem de eventos
* Mapa de identidade
* Variable
* Objeto XDM

Esta lição se concentra no tipo de elemento de dados Variável. Crie um elemento de dados para capturar a atividade dos visitantes do Luma com base na camada de dados disponível no site Luma. Na próxima lição, você aprenderá sobre o Mapa de identidade.

>[!NOTE]
>
> A ID de mesclagem de eventos e os tipos de elemento de dados de objeto XDM raramente são usados para casos de borda.

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Entender diferentes abordagens para mapear uma camada de dados para o XDM
* Criar elementos de dados para capturar dados de conteúdo
* Mapear elementos de dados para um elemento de dados de objeto XDM


## Pré-requisitos

Você entende o que é uma camada de dados, familiarizado com o [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} camada de dados e saiba como fazer referência a elementos de dados em tags. Você deve ter concluído as seguintes etapas anteriores no tutorial.

* [Configurar um esquema XDM](configure-schemas.md)
* [Configurar um namespace de identidade](configure-identities.md)
* [Configurar uma sequência de dados](configure-datastream.md)
* [Extensão SDK da Web instalada na propriedade da tag](install-web-sdk.md)

>[!IMPORTANT]
>
>A variável [Extensão do Experience Cloud ID Service](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) não é necessário ao implementar o SDK da Web da Adobe Experience Platform, pois a funcionalidade do Serviço de ID é incorporada no SDK da Web da plataforma.

## Abordagens da Camada de dados

Há várias maneiras de mapear dados da camada de dados para o XDM usando a funcionalidade de tags do Adobe Experience Platform. Abaixo estão alguns prós e contras de três abordagens diferentes:

* [Implementar o XDM na camada de dados](create-data-elements.md#implement-xdm-in-the-data-layer)
* [Mapear para XDM no fluxo de dados](create-data-elements.md#map-to-xdm-in-the-datastream)
* [Mapear para XDM em tags](create-data-elements.md#map-data-layer-in-tags)

>[!NOTE]
>
>Os exemplos neste tutorial seguem a abordagem Mapear para XDM em tags.


### Implementar o XDM na camada de dados

Essa abordagem envolve o uso do objeto XDM totalmente definido como a estrutura da camada de dados. Em seguida, mapeie toda a camada de dados para um elemento de dados de objeto XDM nas Tags Adobe. Se sua implementação não estiver usando um gerenciador de tags, essa abordagem poderá ser ideal, pois você pode enviar dados para o XDM diretamente do aplicativo usando o [Comando sendEvent do XDM](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#sending-xdm-data). Se você usar tags Adobe, poderá criar um elemento de dados de código personalizado capturando toda a camada de dados como um objeto JSON de passagem para o XDM. Em seguida, mapeie o JSON de passagem para o campo do objeto XDM na Ação Enviar evento.

Veja abaixo um exemplo de como seria a camada de dados usando o formato da Camada de dados do cliente Adobe:

+++XDM no exemplo de Camada de dados

```JSON
window.adobeDataLayer.push({
"eventType": "web.webPageDetails.pageViews",
"web":{
         "webInteraction":{
            "linkClicks":{
               "id":"",
               "value":""
            },
            "URL":"",
            "name":"",
            "region":"",
            "type":""
         },
         "webPageDetails":{
            "pageViews":{
               "id":"",
               "value":"1"
            },
            "URL":"https://luma.enablementadobe.com/",
            "isErrorPage":"",
            "isHomePage":"",
            "name":"luma:home",
            "server":"enablementadobe.com",
            "siteSection":"home",
            "viewName":""
         },
         "webReferrer":{
            "URL":"",
            "type":""
         }
      }
});
```

+++

Pontos positivos

* Ignora etapas para mapear variáveis de camada de dados individuais para XDM
* Pode ser mais rápido de implantar se a sua equipe de desenvolvimento possuir a tag de comportamento digital

Pontos negativos

* Confiança total na equipe de desenvolvimento e no ciclo de desenvolvimento para atualizar quais dados vão para o XDM
* Flexibilidade limitada, pois o XDM recebe a carga exata da camada de dados
* Não é possível usar recursos integrados de tags, como raspagem, persistência e recursos para implantações rápidas
* Não é possível usar a camada de dados para pixels de terceiros
* Não há capacidade de transformar os dados entre a camada de dados e o XDM

### Mapear para XDM no fluxo de dados

Essa abordagem usa uma funcionalidade integrada à configuração de sequência de dados chamada [Preparação de dados para coleção de dados](https://experienceleague.adobe.com/docs/experience-platform/datastreams/data-prep.html) O e o ignoram o mapeamento de variáveis de camada de dados para o XDM nas tags.

Pontos positivos

* Flexível, pois é possível mapear variáveis individuais para o XDM
* Capacidade para [calcular novos valores](https://experienceleague.adobe.com/docs/experience-platform/data-prep/functions.html?lang=pt-BR) ou [transformar tipos de dados](https://experienceleague.adobe.com/docs/experience-platform/data-prep/data-handling.html) de uma camada de dados antes de ela ir para o XDM
* Aproveitar um [Mapeamento da interface do usuário](https://experienceleague.adobe.com/docs/experience-platform/datastreams/data-prep.html#create-mapping) para mapear campos nos dados de origem para o XDM com uma interface de apontar e clicar

Pontos negativos

* Não é possível usar variáveis de camada de dados como elementos de dados para pixels de terceiros do lado do cliente, mas você pode usá-las com o encaminhamento de eventos de tags Adobe
* Não é possível usar a funcionalidade de reaproveitamento do recurso de tags do Adobe Experience Platform
* A complexidade de manutenção aumenta se o mapeamento da camada de dados for feito em tags e na sequência de dados

### Mapear a camada de dados nas tags

Essa abordagem envolve o mapeamento de variáveis de camada de dados individuais OU objetos de camada de dados para elementos de dados em tags e, por fim, para o XDM. Essa é a abordagem tradicional de implementação usando um sistema de gerenciamento de tags.

Pontos positivos

* A abordagem mais flexível, pois você pode controlar variáveis individuais e transformar dados antes que eles cheguem ao XDM
* Pode usar acionadores de tags Adobe e a funcionalidade de refugo para transmitir dados ao XDM
* Pode mapear elementos de dados para pixels de terceiros no lado do cliente

Pontos negativos

* Pode levar mais tempo para implementar

>[!TIP]
>
> Camada de dados Google
> 
> Se sua organização já usa o Google Analytics e tem o objeto tradicional dataLayer do Google em seu site, você pode usar o [Extensão da camada de dados do Google](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/google-data-layer/overview.html?lang=en) em Tags do Adobe. Isso permite que você implante a tecnologia Adobe mais rapidamente, sem precisar solicitar suporte da sua equipe de TI. O mapeamento da camada de dados do Google para o XDM seguiria as mesmas etapas descritas acima.

>[!IMPORTANT]
>
>Como observado anteriormente, os exemplos neste tutorial seguem a abordagem Mapear para XDM em tags.

## Criar elementos de dados para capturar a camada de dados

Antes de criar o objeto XDM, crie o seguinte conjunto de elementos de dados para o [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} camada de dados:

1. Ir para **[!UICONTROL Elementos de dados]** e selecione **[!UICONTROL Adicionar elemento de dados]** (ou **[!UICONTROL Criar novo elemento de dados]** se não houver elementos de dados existentes na propriedade tag )

   ![Criar elemento de dados](assets/data-element-create.jpg)

1. Nomeie o elemento de dados `page.pageInfo.pageName`
1. Use o **[!UICONTROL Variável JavaScript]** **[!UICONTROL Tipo de elemento de dados]** para apontar para um valor na camada de dados do Luma: `digitalData.page.pageInfo.pageName`

1. Marque as caixas para **[!UICONTROL Forçar valor de minúsculas]** e **[!UICONTROL Texto limpo]** para padronizar o caso e remover espaços irrelevantes

1. Sair `None` como o **[!UICONTROL Duração do armazenamento]** já que esse valor é diferente em cada página

1. Selecionar **[!UICONTROL Salvar]**

   ![Elemento de dados do nome da página](assets/data-element-pageName.jpg)

Crie esses quatro elementos de dados adicionais seguindo as mesmas etapas:

* **`page.pageInfo.server`**  mapeado para
  `digitalData.page.pageInfo.server`

* **`page.pageInfo.hierarchie1`**  mapeado para
  `digitalData.page.pageInfo.hierarchie1`

* **`user.profile.attributes.username`**  mapeado para
  `digitalData.user.0.profile.0.attributes.username`

* **`user.profile.attributes.loggedIn`** mapeado para
  `digitalData.user.0.profile.0.attributes.loggedIn`

* **`cart.orderId`** mapeado para `digitalData.cart.orderId` (você usa isso durante o [Configurar o Analytics](setup-analytics.md) lição)


>[!CAUTION]
>
>A variável [!UICONTROL Variável JavaScript] o tipo de elemento de dados trata as referências de matriz como pontos em vez de colchetes, de modo que fazer referência ao elemento de dados username como `digitalData.user[0].profile[0].attributes.username` **não funcionará**.

## Criar elemento de dados Variable

Depois de criar os elementos de dados, mapeie-os para o XDM usando o **[!UICONTROL Variável]** elemento de dados que define o esquema usado para o objeto XDM. Esse objeto deve estar em conformidade com o esquema XDM criado durante o [Configurar um esquema](configure-schemas.md) lição.

Para criar o elemento de dados Variable:

1. Selecionar **[!UICONTROL Adicionar elemento de dados]**
1. Nomeie seu elemento de dados `xdm.variable.content`. Recomenda-se adicionar um prefixo &quot;xdm&quot; aos Elementos de dados específicos do XDM para organizar melhor a propriedade da tag
1. Selecione o **[!UICONTROL Adobe Experience Platform Web SDK]** como o **[!UICONTROL Extensão]**
1. Selecione o **[!UICONTROL Variável]** como o **[!UICONTROL Tipo de elemento de dados]**
1. Selecione o Experience Platform apropriado **[!UICONTROL Sandbox]**
1. Selecione o apropriado **[!UICONTROL Esquema]**, neste caso `Luma Web Event Data`
1. Selecionar **[!UICONTROL Salvar]**

   ![Elemento de dados variável](assets/analytics-tags-data-element-xdm-variable.png)

<!-- There are different ways to map data elements to XDM object fields. You can map individual data elements to individual XDM fields or map data elements to entire XDM objects as long as your data element matches the exact key-value pair schema present in the XDM object. In this lesson, you will capture content data by mapping to individual fields. You will learn how to [map a data element to an entire XDM object](setup-analytics.md#Map-an-entire-array-to-an-XDM-Object) in the [Setup Analytics](setup-analytics.md) lesson. 

Create an XDM object to capture content data:

1. In the left navigation, select **[!UICONTROL Data Elements]**
1. Select **[!UICONTROL Add Data Element]**
1. **[!UICONTROL Name]** the data element **`xdm.content`**
1. As the **[!UICONTROL Extension]** select `Adobe Experience Platform Web SDK`
1. As the **[!UICONTROL Data Element Type]** select `XDM object`
1. Select the Platform **[!UICONTROL Sandbox]** in which you created the XDM schema in during the [Configure an XDM Schema](configure-schemas.md) lesson, in this example `DEVELOPMENT Mobile and Web SDK Courses`
1. As the **[!UICONTROL Schema]**, select your `Luma Web Event Data` schema:

    ![XDM object](assets/data-element-xdm.content-fields.png)

    >[!NOTE]
    >
    >The sandbox corresponds to the Experience Platform sandbox in which you created the schema. There can be multiple sandboxes available in your Experience Platform instance, so make sure to select the right one. Always work in development first, then production.

1. Scroll down until you reach the **`web`** object
1. Select to open it

    ![Web Object](assets/data-element-pageviews-xdm-object.png)


1. Map the following web XDM variables to data elements

    * **`web.webPageDetials.name`** to `%page.pageInfo.pageName%`
    * **`web.webPageDetials.server`** to `%page.pageInfo.server%`
    * **`web.webPageDetials.siteSection`** to `%page.pageInfo.hierarchie1%`

    ![XDM object](assets/data-element-xdm.content.png)

1. Next, find the `identityMap` object in the schema and select it
 
1. Map to the `identityMap.loginID` data element

1. Select **[!UICONTROL Save]**

   ![Data Collection interface](assets/identity-dataElements-xdmContent-LumaSchema-identityMapSelect3.png)

-->

Ao final dessas etapas, você deve ter os seguintes elementos de dados criados:

| Elementos de dados da extensão CORE | Elementos de dados do SDK da Web da plataforma |
-----------------------------|-------------------------------
| `cart.orderId` | `xdm.variable.content` |
| `page.pageInfo.hierarchie1` | |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |


>[!TIP]
>
>Em um futuro [Criar uma regra de tag](create-tag-rule.md) lição, você aprenderá como a **[!UICONTROL Variável]** O elemento de dados permite empilhar várias regras em tags usando o **[!UICONTROL Atualizar tipo de ação variável]**. Em seguida, é possível enviar independentemente o objeto XDM para a Rede de borda da Adobe Experience Platform usando uma **[!UICONTROL Tipo de ação Enviar Evento]**.

Com esses elementos de dados implementados, você estará pronto para começar a enviar dados para a Rede de borda da Platform com uma regra de tags. Mas, primeiro, saiba mais sobre como coletar identidades com o SDK da Web.

[Próximo: ](create-identities.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar feedback geral ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
