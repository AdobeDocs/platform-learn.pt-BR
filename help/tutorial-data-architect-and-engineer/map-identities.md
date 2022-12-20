---
title: Mapear identidades
seo-title: Map identities | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Mapear identidades
description: Nesta lição, criaremos namespaces de identidade e adicionaremos campos de identidade aos nossos schemas.
role: Data Architect
feature: Profiles
kt: 4348
thumbnail: 4348-map-identities.jpg
exl-id: e17ffabc-049c-42ff-bf0a-8cc31d665dfa
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 4%

---

# Mapear identidades

<!-- 30 min-->

Nesta lição, criaremos namespaces de identidade e adicionaremos campos de identidade aos nossos schemas. Depois de fazer isso, também poderemos concluir os relacionamentos de schema da lição anterior.

O serviço de identidade da Adobe Experience Platform ajuda você a obter uma melhor visão de seus clientes e seus comportamentos ao unir identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real. Campos de identidade e namespaces são a cola que une diferentes fontes de dados para criar o perfil do cliente em tempo real de 360 graus.

**Arquitetos de dados** O precisará mapear identidades fora deste tutorial.

Antes de começar os exercícios, assista a este breve vídeo para saber mais sobre identidade no Adobe Experience Platform:
>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

>[!NOTE]
>
>Os campos de identidade só são necessários se você criar perfis de clientes em tempo real. Eles não são necessários se você estiver apenas assimilando dados no lago de dados.

<!--explain identity maps-->
<!--explain the strategy behind the identity selection, how these identities will join all the data together-->

## Permissões necessárias

No [Configurar permissões](configure-permissions.md) lição, configure todos os controles de acesso necessários para concluir esta lição.

<!--
* Permission items **[!UICONTROL Identity Management]** > **[!UICONTROL View Identity Namespaces]** and **[!UICONTROL Manage Identity Namespaces]**
* Permission item **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## Criar namespace de identidade

Neste exercício, criaremos namespaces de identidade para os campos de identidade personalizados do Luma, `loyaltyId`, `crmId`e `productSku`. Os namespaces de identidade desempenham um papel essencial na criação de perfis de clientes em tempo real, já que dois valores correspondentes no mesmo namespace permitem que duas fontes de dados formem um gráfico de identidade.


### Criar namespaces na interface do usuário

Vamos começar criando um namespace para o Esquema de Fidelidade do Luma:

1. Na interface do usuário da Platform, acesse **[!UICONTROL Identidades]** na navegação à esquerda
1. Você observará que há vários namespaces de identidade prontos para uso disponíveis. Selecione o **[!UICONTROL Criar namespace de identidade]** botão
1. Forneça os detalhes a seguir

   | Campo | Valor |
   |---------------|-----------|
   | Nome de exibição | Id de Fidelidade do Luma |
   | Símbolo de identidade | lumaLoyaltyId |
   | Tipo |  entre dispositivos |

1. Selecione **[!UICONTROL Criar]**

   ![Criar namespaces](assets/identity-createNamespace.png)

Agora, configure outro namespace para o Esquema do catálogo de produtos do Luma com os seguintes detalhes:

| Campo | Valor |
|---------------|-----------|
| Nome de exibição | SKU do produto Luma |
| Símbolo de identidade | lumaProductSKU |
| Tipo | Identificador de não pessoas |



## Criar namespace de identidade usando API

Criaremos nosso namespace do CRM por meio da API.

>[!NOTE]
>
>Se preferir ignorar os exercícios de API, sinta-se à vontade para criar o namespace do CRM por meio do método de interface do usuário usado com os seguintes detalhes:
>
> 1. Como **[!UICONTROL Nome de exibição]**, use `Luma CRM Id`
> 1. Como **[!UICONTROL Símbolo de identidade]**, use `lumaCrmId`
> 1. Como **[!UICONTROL Tipo]**, use Cross-Device


Vamos criar o Namespace de Identidade `Luma CRM Id`:

1. Baixar [Serviço de identidade.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Identity%20Service.postman_collection.json) para `Luma Tutorial Assets` pasta
1. Importe a coleção para [!DNL Postman]
1. Se você não tiver feito uma solicitação nas últimas 24 horas, seus tokens de autorização provavelmente expiraram. Abrir a solicitação **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]** e selecione **Enviar** para solicitar novos tokens de acesso e JWT.
1. Selecionar a solicitação **[!UICONTROL Serviço de identidade] > [!UICONTROL Namespace de identidade] > [!UICONTROL Criar um novo namespace de identidade].**
1. Cole o seguinte como o [!DNL Body] do pedido:

   ```json
   {
       "name": "Luma CRM Id",
       "code": "lumaCrmId",
       "idType": "Cross_device"
   }
   ```

1. Pressione a tecla **Enviar** e você deve obter um **200 OK** resposta:

   ![Namespace de identidade](assets/identity-createUsingApi.png)

Caso volte à interface do usuário, você deverá ver seus três novos namespaces personalizados:
![Namespace de identidade ](assets/identity-newIdentities.png)


## Rotular campos de identidade em schemas

Agora que temos nossos namespaces, o próximo passo é atualizar nossos esquemas para rotular nossos campos de identidade.


### Rotular campos XDM para identidade primária

Cada esquema usado com o Perfil do cliente em tempo real deve ter uma identidade primária especificada. E cada registro assimilado deve ter um valor para esse campo.

Vamos adicionar uma identidade primária ao `Luma Loyalty Schema`:

1. Abra o `Luma Loyalty Schema`
1. Selecione o `Luma Identity profile field group`
1. Selecione o `loyaltyId` campo
1. Verifique a **[!UICONTROL Identidade]** caixa
1. Verifique a **[!UICONTROL Identidade principal]** caixa também
1. Selecione o `Luma Loyalty Id` namespace de **[!UICONTROL Namespaces de identidade]** lista suspensa
1. Selecionar **[!UICONTROL Aplicar]**
1. Selecione **[!UICONTROL Salvar]**

   ![Identidade principal ](assets/identity-loyalty-primary.png)

Repita o processo para alguns dos outros esquemas:

1. No `Luma CRM Schema`, rotule o `crmId` como a identidade primária usando o `Luma CRM Id` namespace
1. No `Luma Offline Purchase Events Schema`, rotule o `loyaltyId` como a identidade primária usando o `Luma Loyalty Id` namespace
1. No `Luma Product Catalog Schema`, rotule o `productSku` como a identidade primária usando o `Luma Product SKU` namespace

>[!NOTE]
>
>Os dados coletados com o SDK da Web são uma exceção à prática típica de rotular campos de identidade no esquema. O SDK da Web usa o Mapa de identidade para rotular identidades *do lado da implementação* e, portanto, vamos determinar as identidades para a `Luma Web Events Schema` quando implementamos o SDK da Web no site Luma. Nessa lição posterior, coletaremos a Experience Cloud Visitor ID (ECID) como a id primária e o crmId como uma id secundária.

Com nossa seleção de identidades primárias, é claro ver como `Luma CRM Schema` pode se conectar ao `Luma Offline Purchase Events Schema` já que ambos usam `loyaltyId` como um identificador. Mas como conectar nossas compras offline ao comportamento online? Como podemos classificar os produtos comprados com nosso catálogo de produtos? Usaremos campos de identidade adicionais e relações de esquema.

<!--use a visual-->

### Rotular campos XDM para a identidade secundária

Vários campos de identidade podem ser adicionados a um esquema. Identidades não primárias são frequentemente referidas como identidades secundárias. Para conectar compras offline ao comportamento online, adicionaremos o crmId como identificador secundário ao nosso `Luma Loyalty Schema` e posteriormente nos dados de eventos da Web. Vamos atualizar o `Luma Loyalty Schema`:

1. Abra o `Luma Loyalty Schema`
1. Selecione `Luma Identity Profile Field group`
1. Selecionar `crmId` campo
1. Verifique a **[!UICONTROL Identidade]** caixa
1. Selecione o `Luma CRM Id` namespace de **[!UICONTROL Namespaces de identidade]** lista suspensa
1. Selecionar **[!UICONTROL Aplicar]** e selecione o **[!UICONTROL Salvar]** botão para salvar suas alterações

   ![Identidade secundária](assets/identity-loyalty-secondaryId.png)

## Concluir as relações do schema

Agora que temos nossos campos de identidade rotulados, podemos concluir a configuração dos relacionamentos de esquema entre o catálogo de produtos do Luma e os esquemas de evento:

1. Abra o `Luma Offline Purchase Events Schema`
1. Selecionar **[!UICONTROL Detalhes de comércio]** grupo de campos
1. Selecionar **[!UICONTROL productListItems]** > **[!UICONTROL SKU]** campo
1. Verifique a **[!UICONTROL Relação]** caixa
1. Selecionar `Luma Product Catalog Schema` como **[!UICONTROL Esquema de referência]**
1. `Luma Product SKU` deve preencher automaticamente como o **[!UICONTROL Namespace de identidade de referência]**
1. Selecionar **[!UICONTROL Aplicar]**
1. Selecione **[!UICONTROL Salvar]**

   ![Campo de referência](assets/identity-offlinePurchase-relationship.png)

Repita esse processo para criar uma relação entre a `Luma Web Events Schema` e `Luma Product Catalog Schema`.

Observe que, após definir a relação, ela é indicada em **[!UICONTROL Composição]** e **[!UICONTROL Estrutura]** do editor de esquema.

![Visualização do relacionamento no editor de esquema](assets/identity-webEvents-relationship.png)

<!--need to verify that the relationship schema works-->

## Recursos adicionais

* Documentação do [Serviço de identidade](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=pt-BR)
* [API do serviço de identidade](https://www.adobe.io/experience-platform-apis/references/identity-service/)

Agora que as nossas identidades estão reunidas, podemos [criar nossos conjuntos de dados](create-datasets.md)!
