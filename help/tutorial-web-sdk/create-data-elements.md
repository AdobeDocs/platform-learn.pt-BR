---
title: Criar elementos de dados
description: Saiba como criar um objeto XDM e mapear elementos de dados para ele em tags. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Tags
exl-id: d662ec46-de9b-44ba-974a-f81dfc842e68
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 5%

---

# Criar elementos de dados

Saiba como criar os elementos de dados essenciais necessários para capturar dados com o Experience Platform Web SDK. Capturar dados de conteúdo e identidade na [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Saiba como usar o esquema XDM criado anteriormente para coletar dados usando o SDK da Web da plataforma por meio de um novo tipo de elemento de dados chamado Objeto XDM.

>[!NOTE]
>
> Para fins de demonstração, os exercícios desta lição baseiam-se no exemplo usado durante [Configurar um schema](configure-schemas.md) degrau; criação de objetos XDM de exemplo que capturam o conteúdo exibido e as identidades dos usuários no [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html).

>[!IMPORTANT]
>
>Os dados desta lição vêm do `[!UICONTROL digitalData]` camada de dados no site Luma. Para exibir a camada de dados, abra o console do desenvolvedor e digite `[!UICONTROL digitalData]` para ver a camada de dados completa disponível.![camada de dados digitalData](assets/data-element-data-layer.png)


Independentemente do SDK da Web da plataforma, você deve continuar a criar elementos de dados dentro da propriedade de tag que mapeiam para variáveis de coleta de dados do seu site, como uma camada de dados, um atributo de HTML ou outros. Depois de criar esses elementos de dados, você deve mapeá-los para o esquema XDM criado durante a [configurar schemas](configure-schemas.md) lição. Para fazer isso, a extensão Platform Web SDK disponibiliza um novo tipo de elemento de dados chamado objeto XDM. Portanto, a criação de elementos de dados consiste em duas ações:

1. Mapeamento de variáveis de site a elementos de dados e
1. Mapeamento desses elementos de dados para um objeto XDM

Para a etapa 1, você continua mapeando a camada de dados para elementos de dados da maneira que faz atualmente, usando qualquer um dos tipos de elemento de dados da extensão de tag principal. Para a etapa 2, a extensão Platform Web SDK cria um conjunto de novos tipos de elementos de dados não disponíveis anteriormente:

* ID da mesclagem de eventos
* Mapa de identidade
* Objeto XDM

Essa lição foca no objeto XDM e nos tipos de elementos de dados do mapa de identidade. Você criará objetos XDM para capturar a atividade e o status de autenticação dos visitantes Luma.

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Criar elementos de dados para capturar dados de conteúdo e ID de logon do usuário
* Criar um elemento de dados do mapa de identidade
* Mapear elementos de dados para um elemento de dados de objeto XDM


## Pré-requisitos

Você tem uma compreensão do que é uma camada de dados, familiarizada com a [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html)Camada de dados {target=&quot;_blank&quot;} e saiba como fazer referência aos elementos de dados nas tags . Você deve ter concluído as seguintes etapas anteriores no tutorial

* [Configurar permissões](configure-permissions.md)
* [Configurar um esquema XDM](configure-schemas.md)
* [Configurar um namespace de identidade](configure-identities.md)
* [Configurar um conjunto de dados](configure-datastream.md)
* [Extensão do SDK da Web instalada na propriedade da tag](install-web-sdk.md)

>[!IMPORTANT]
>
>O [Extensão do Experience Cloud ID Service](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) não é necessário ao implementar o SDK da Web da Adobe Experience Platform, pois a funcionalidade do Serviço de ID é incorporada ao SDK da Web da plataforma.

## Criar elementos de dados para capturar a camada de dados

Antes de começar a criar o objeto XDM, crie o seguinte conjunto de elementos de dados mapeando para a [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html)Camada de dados {target=&quot;_blank&quot;}:

1. Ir para **[!UICONTROL Elementos de dados]** e selecione **[!UICONTROL Adicionar elemento de dados]** ou **[!UICONTROL Criar novo elemento de dados]** se não houver elementos de dados existentes na propriedade da tag)

   ![Criar elemento de dados](assets/data-element-create.jpg)

1. Nomeie o elemento de dados `page.pageInfo.pageName`
1. Use o **[!UICONTROL Variável JavaScript]** **[!UICONTROL Tipo de elemento de dados]** para apontar para um valor na camada de dados do Luma: `digitalData.page.pageInfo.pageName`

1. Marque as caixas **[!UICONTROL Forçar valor minúsculo]** e **[!UICONTROL Texto limpo]** para padronizar o caso e remover espaços irrelevantes

1. Sair `None` como **[!UICONTROL Duração do armazenamento]** configuração , pois esse valor é diferente em cada página

1. Selecione **[!UICONTROL Salvar]**

   ![Elemento de dados do nome da página](assets/data-element-pageName.jpg)

Siga as mesmas etapas para criar esses quatro elementos de dados adicionais:

* **`page.pageInfo.server`**  mapeado para
   `digitalData.page.pageInfo.server`

* **`page.pageInfo.hierarchie1`**  mapeado para
   `digitalData.page.pageInfo.hierarchie1`

* **`user.profile.attributes.username`**  mapeado para
   `digitalData.user.0.profile.0.attributes.username`

* **`user.profile.attributes.loggedIn`** mapeado para
   `digitalData.user.0.profile.0.attributes.loggedIn`

* **`cart.orderId`** mapeado para `digitalData.cart.orderId` (você usará durante a [Configurar Analytics](setup-analytics.md) lição)


>[!CAUTION]
>
>O [!UICONTROL Variável JavaScript] o tipo de elemento de dados trata as referências da matriz como pontos em vez de colchetes, portanto, referenciar o elemento de dados de nome de usuário como `digitalData.user[0].profile[0].attributes.username` **não funcionará**.

## Criar elemento de dados do Mapa de identidade

Em seguida, você pode criar o elemento de dados do Mapa de identidade:

1. Ir para **[!UICONTROL Elementos de dados]** e selecione **[!UICONTROL Adicionar elemento de dados]**

1. **[!UICONTROL Nome]** o elemento de dados `identityMap.loginID`

1. Como **[!UICONTROL Extensão]**, selecione `Adobe Experience Platform Web SDK`

1. Como **[!UICONTROL Tipo de elemento de dados]**, selecione `Identity map`

1. Isso solicitará uma área da tela à direita na **[!UICONTROL Interface da Coleta de dados]** para você configurar a identidade:

   ![Interface da Coleta de dados](assets/identity-identityMap-setup.png)

1. Como  **[!UICONTROL Namespace]**, selecione o `Luma CRM Id` namespace criado anteriormente na [Configurar identidades](configure-identities.md) lição.

   >[!NOTE]
   >
   >    Se você não vir seu `Luma CRM Id` namespace, verifique se você também o criou na sandbox de produção padrão. Somente os namespaces criados na sandbox de produção padrão são exibidos atualmente na lista suspensa namespace .

1. Depois que a variável **[!UICONTROL Namespace]** for selecionada, uma ID deverá ser definida. Selecione o `user.profile.attributes.username` elemento de dados criado anteriormente nesta lição, que captura uma ID quando os usuários estão conectados ao site Luma.

<!--  >[!TIP]
   >
   >You can verify the **[!UICONTROL Luma CRM ID]** is collected in a data element on the web property by going to the [Luma Demo site](https://luma.enablementadobe.com/content/luma/us/en.html), logging in, [switching the tag environment](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) to your own, and typing `_satellite.getVar("user.profile.attributes.username")` in the web browser developer console.
   >
   >   ![Data Element  ID ](assets/identity-data-element-customer-id.png)
-->

1. Como **[!UICONTROL Estado autenticado]**, selecione **[!UICONTROL Autenticado]**

1. Selecione **[!UICONTROL Salvar]**

   ![Interface da Coleta de dados](assets/identity-id-namespace.png)

>[!WARNING]
>
>A identidade primária é necessária em todos os registros enviados para a Adobe Experience Platform. Por padrão, a ID do Experience Cloud (ECID) é usada como a identidade primária do SDK da Web da plataforma. Você nunca gostaria de usar algo como o `Luma CRM ID` como uma identidade primária com o SDK da Web, uma vez que só existe depois que o usuário se autentica e, portanto, não estaria disponível em todos os registros.

<!--
1. Once the data element is configured in **[!UICONTROL Data Collection interface]**, it can be tested on the Luma web property like any other Data Element. Enter the following script in the browser developer console
   
   
   ```
   _satellite.getVar('identityMap.loginID')
   ```  

   ![Data Collection interface](assets/identity-consoleIdentityDataElement.png)
   
   >[!NOTE]
   >
   >ECID identifier will NOT populate in the Data Element, as this is configured already with Platform Web SDK.   
-->

## Mapear elementos de dados para objetos XDM

Todos os elementos de dados criados devem ser mapeados para um objeto XDM. Esse objeto deve estar em conformidade com o esquema XDM criado durante a [Configurar um schema](configure-schemas.md) lição.

Há diferentes maneiras de mapear elementos de dados para campos de objeto XDM. Você pode mapear elementos de dados individuais para campos XDM individuais ou mapear elementos de dados para objetos XDM inteiros, desde que o elemento de dados corresponda ao schema exato do par de valores-chave presente no objeto XDM. Nesta lição, você capturará dados de conteúdo por mapeamento para campos individuais. Você aprenderá como [mapear um elemento de dados para um objeto XDM inteiro](setup-analytics.md#Map-an-entire-array-to-an-XDM-Object) no [Configurar Analytics](setup-analytics.md) lição.

Crie um objeto XDM para capturar dados de conteúdo:

1. Na navegação à esquerda, selecione **[!UICONTROL Elementos de dados]**
1. Selecione **[!UICONTROL Adicionar elemento de dados]**
1. **** Nomeie o elemento de dados **`xdm.content`**
1. Como **[!UICONTROL Extensão]** select `Adobe Experience Platform Web SDK`
1. Como **[!UICONTROL Tipo de elemento de dados]** select `XDM object`
1. Selecione a plataforma **[!UICONTROL Sandbox]** no qual você criou o esquema XDM durante a [Configurar um esquema XDM](configure-schemas.md) lição, neste exemplo `DEVELOPMENT Mobile and Web SDK Courses`
1. Como **[!UICONTROL Esquema]**, selecione o `Luma Web Event Data` schema:

   ![Objeto XDM](assets/data-element-xdm.content-fields.png)

   >[!NOTE]
   >
   >A sandbox corresponde à sandbox do Experience Platform na qual o esquema foi criado. Pode haver várias sandboxes disponíveis na instância do Experience Platform, portanto, selecione a correta. Sempre trabalhe em desenvolvimento primeiro, depois em produção.

1. Role para baixo até acessar o **`web`** objeto
1. Selecione para abri-la

   ![Objeto da Web](assets/data-element-pageviews-xdm-object.png)


1. Mapeie as seguintes variáveis XDM da Web para elementos de dados

   * **`web.webPageDetials.name`** para `%page.pageInfo.pageName%`
   * **`web.webPageDetials.server`** para `%page.pageInfo.server%`
   * **`web.webPageDetials.siteSection`** para `%page.pageInfo.hierarchie1%`

   ![Objeto XDM](assets/data-element-xdm.content.png)

1. Em seguida, encontre a `identityMap` no esquema e selecione-o

1. Mapear para a `identityMap.loginID` elemento de dados

1. Selecione **[!UICONTROL Salvar]**

   ![Interface da Coleta de dados](assets/identity-dataElements-xdmContent-LumaSchema-identityMapSelect3.png)




No final dessas etapas, você deve criar os seguintes elementos de dados:

| Elementos de dados da extensão CORE | Elementos de dados do SDK da Web da plataforma |
-----------------------------|-------------------------------
| `cart.orderId` | `identityMap.loginID` |
| `page.pageInfo.hierarchie1` | `xdm.content` |
| `page.pageInfo.pageName` |  |
| `page.pageInfo.server` |  |
| `user.profile.attributes.loggedIn` |  |
| `user.profile.attributes.username` |  |

Com esses elementos de dados em vigor, você está pronto para começar a enviar dados para a Rede de Borda da Plataforma por meio do objeto XDM criando uma regra nas tags .

[Próximo: ](create-tag-rule.md)

>[!NOTE]
>
>Obrigado por investir seu tempo para aprender sobre o SDK da Web da Adobe Experience Platform. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
