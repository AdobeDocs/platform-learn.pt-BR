---
title: Ativar perfis do cliente em tempo real
seo-title: Enable Real-Time Customer Profiles | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Ativar perfis do cliente em tempo real
description: Nesta lição, você ativará seus esquemas e conjuntos de dados para o Perfil do cliente em tempo real.
role: Data Architect
feature: Profiles
kt: 4348
thumbnail: 4348-enable-profiles.jpg
exl-id: b05f1af1-a599-42f2-8546-77453a578b92
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 0%

---

# Ativar perfis do cliente em tempo real

<!-- 15min-->
Nesta lição, você ativará seus esquemas e conjuntos de dados para o Perfil do cliente em tempo real.

Ok, eu menti quando disse que a lição de conjuntos de dados era a lição mais curta neste tutorial — esta deve levar ainda menos tempo! Literalmente, tudo o que você vai fazer é virar um monte de toggles. Mas o que acontece quando você vira essas chaves é _realmente_ importante, então eu queria dedicar uma página inteira a ele.

Com o Perfil do cliente em tempo real, você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. O Perfil permite consolidar seus diferentes dados do cliente em uma visualização unificada que oferece uma conta acionável com carimbo de data e hora de cada interação com o cliente.

Por mais incrível que tudo pareça, você não precisa ativar *todos os seus dados* para perfil. Na verdade, você só deve ativar os dados necessários para casos de uso de ativação. Ative os dados que deseja usar para casos de uso de marketing, integrações da central de atendimento e assim por diante, onde você precisa de acesso rápido a um perfil de cliente robusto. Se você estiver fazendo upload de dados somente para análise, eles provavelmente não deverão ser ativados para o perfil.

Há questões importantes [medidas de proteção para dados de Perfil do cliente em tempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en) que você deve revisar ao decidir quais de seus próprios dados você deve ativar para o perfil.

<!--is this accurate. Are there other considerations to point out? -->

**Arquitetos de dados** O precisará ativar o Perfil do cliente em tempo real fora deste tutorial.

Antes de começar os exercícios, assista a este breve vídeo para saber mais sobre o Perfil do cliente em tempo real:
>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12&learn=on)

## Permissões necessárias

No [Configurar permissões](configure-permissions.md) lição, configure todos os controles de acesso necessários para concluir esta lição.


<!--* Permission items **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## Ativar esquemas para o Perfil do cliente em tempo real usando a interface do usuário da plataforma

Vamos começar com a tarefa simples de habilitar um schema:

1. Na interface do usuário da Plataforma, abra o **Esquema de Fidelidade do Luma**
1. Em **[!UICONTROL Propriedades do esquema]**, alterne a **Perfil** switch
1. No modal de confirmação, pressione a tecla **[!UICONTROL Habilitar]** botão para confirmar
1. Selecione o **[!UICONTROL Salvar]** botão para salvar suas alterações

   >[!IMPORTANT]
   >
   >Depois que um esquema é ativado para o Perfil, ele não pode ser desativado ou excluído. Além disso, os campos não podem ser removidos do schema após esse ponto. Essas implicações são importantes que você deve ter em mente posteriormente ao trabalhar com seus próprios dados no ambiente de produção. Você deve estar usando uma sandbox de desenvolvimento neste tutorial, que pode ser excluída a qualquer momento.
   >
   >No ambiente controlado deste tutorial, você ativará seus esquemas e conjuntos de dados para perfil, _antes de assimilar quaisquer dados_. Ao trabalhar com seus próprios dados, recomendamos que você faça as coisas na seguinte ordem:
   >
   > 1. Primeiro, assimile alguns dados em seus conjuntos de dados.
   > 1. Resolver quaisquer problemas que surjam durante o processo de assimilação de dados (por exemplo, problemas de validação ou mapeamento de dados).
   > 1. Ativar os conjuntos de dados e esquemas para Perfil
   > 1. assimilar os dados



   ![Alternar perfil](assets/profile-loyalty-enableSchema.png)

Fácil, certo? Repita as etapas acima para esses outros esquemas:

1. Esquema do catálogo de produtos Luma
1. Esquema de eventos de compra offline do Luma
1. Luma Web Events Schema (no modal de confirmação, marque a caixa &quot;Data for this schema will contains a primary identity in the identityMap field&quot;.)

## Ativar esquemas para o Perfil do cliente em tempo real usando a API da plataforma

Agora, é hora de habilitar o `Luma CRM Schema` com a API. Se quiser ignorar este exercício e apenas ativá-lo na interface do usuário, siga em frente.

### Obter a meta:altId do esquema

Primeiro vamos pegar o `meta:altId` do `Luma CRM Schema`:

1. Abrir [!DNL Postman]
1. Se você não tiver feito uma solicitação nas últimas 24 horas, seus tokens de autorização provavelmente expiraram. Abrir a solicitação **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]** e selecione **Enviar** para solicitar novos tokens de acesso e JWT, como você fez no [!DNL Postman] lição.
1. Abrir a solicitação **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**
1. Selecione o **Enviar** botão
1. Você deve obter uma resposta 200
1. Procure a resposta para a variável `Luma CRM Schema` e copie o `meta:altId` value
   ![Copie o meta:altIid](assets/profile-crm-getMetaAltId.png)

### Ativar o esquema

Agora que temos a meta:altId do schema, podemos habilitá-la para o perfil:

1. Abrir a solicitação **[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]**
1. No **Params** cole seu `meta:altId` como o valor `SCHEMA_ID` valor do parâmetro
1. No **Corpo** , cole o seguinte código

   ```json
   [{
       "op": "add",
       "path": "/meta:immutableTags",
       "value": ["union"]
   }]
   ```

1. Selecione o **Enviar** botão
1. Você deve obter uma resposta 200

   ![Ative o esquema CRM para o perfil com sua meta:altIid personalizada usada como o parâmetro SCHEMA_ID](assets/profile-crm-enableProfile.png)

Você deve conseguir ver na interface do usuário que todos os cinco esquemas estão habilitados para o Perfil (talvez seja necessário fazer o SHIFT-Reload para ver que `Luma CRM Schema` está ativado):
![Todos os esquemas ativados](assets/profile-allSchemasEnabled.png)


## Ativar conjuntos de dados para o Perfil do cliente em tempo real usando a interface do usuário da plataforma

Os conjuntos de dados também devem ser habilitados para o Perfil, e o processo é ainda mais simples:

1. Na interface do usuário da Plataforma, abra o `Luma Loyalty Dataset`
1. Ative o **[!UICONTROL Perfil]** switch
1. No modal de confirmação, pressione a tecla **[!UICONTROL Habilitar]** botão para confirmar

   ![ Alternar perfil](assets/profile-loyalty-enableDataset.png)

Repita as etapas acima para esses outros conjuntos de dados:

1. Conjunto de dados do catálogo de produtos Luma
1. Conjunto de dados de eventos de compra offline Luma
1. Conjunto de dados de eventos da Web Luma

>[!NOTE]
>
>Ao contrário dos esquemas, você pode desativar os conjuntos de dados do Perfil, no entanto, todos os dados assimilados anteriormente permanecerão no Perfil.

## Ativar conjuntos de dados para o Perfil do cliente em tempo real usando a API da plataforma

Agora, você ativará um conjunto de dados para Perfil usando a API. Novamente, se você quiser habilitá-lo por meio da interface do usuário usando o método acima, tudo bem também.

### Obter a id do conjunto de dados

Primeiro precisamos obter o `id` do `Luma CRM Dataset`:

1. Abrir [!DNL Postman]
1. Se você não tiver feito uma solicitação nas últimas 24 horas, seus tokens de autorização provavelmente expiraram. Abrir a solicitação **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]** e selecione **Enviar** para solicitar novos tokens de acesso e JWT, como você fez no [!DNL Postman] lição.
1. Abrir a solicitação **[!DNL Catalog Service API > Datasets > Retrieve a list of datasets.]**
1. Selecione o **Enviar** botão
1. Você deve obter uma resposta 200
1. Procure a resposta para a variável `Luma CRM Dataset` e copie a id:
   ![Copiar a id](assets/profile-crm-copyDatasetId.png)

### Ativar o conjunto de dados

Agora que temos a id do conjunto de dados, podemos habilitá-la para o perfil:

1. Abrir a solicitação **[!DNL Catalog Service API > Datasets > Update one or more attributes of a dataset specified by ID.]**
1. No **Params** atualize o `DATASET_ID` para seu
1. No **Corpo** cole o seguinte código. Observe que os dois primeiros valores são tags pré-existentes visíveis na resposta anterior. Eles precisam ser incluídos no corpo, além das duas novas tags que adicionamos:

   ```json
   {
       "tags":{
           "adobe/pqs/table":["luma_crm_dataset"],
           "adobe/siphon/table/format":["parquet"],
           "unifiedProfile":["enabled:true"],
           "unifiedIdentity":["enabled:true"]
           }
   }
   ```

1. Selecione o **Enviar** botão
1. Você deve obter uma resposta 200

   ![Ative o conjunto de dados do CRM para perfil, certificando-se de usar sua ID de conjunto de dados personalizada como o parâmetro DATASET_ID](assets/profile-crm-enableDataset.png)

Também é possível confirmar se a interface do usuário mostra o conjunto de dados habilitado:
![Confirmar](assets/profile-crm-confirmEnabled.png)

>[!IMPORTANT]
>
> Se assimilar dados antes de habilitar o esquema e o conjunto de dados para o perfil, será necessário assimilar novamente esses dados depois.

## Recursos adicionais

* [Documentação de Perfil do cliente em tempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=pt-BR)
* [Referência da API do perfil do cliente em tempo real](https://www.adobe.io/experience-platform-apis/references/profile/)


**Engenheiros de dados** deve continuar a [Assinar eventos de assimilação de dados](subscribe-to-data-ingestion-events.md) lição.
**Arquitetos de dados** _pode pular com antecedência_ e vá para o [lição de ingestão em lote](ingest-batch-data.md).
