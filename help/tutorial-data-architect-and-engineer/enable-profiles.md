---
title: Ativar perfis do cliente em tempo real
seo-title: Enable Real-Time Customer Profiles | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Ativar perfis do cliente em tempo real
description: Nesta lição, você ativará seus esquemas e conjuntos de dados para o Perfil do cliente em tempo real.
role: Data Architect
feature: Profiles
jira: KT-4348
thumbnail: 4348-enable-profiles.jpg
exl-id: b05f1af1-a599-42f2-8546-77453a578b92
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 0%

---

# Ativar perfis do cliente em tempo real

<!-- 15min-->
Nesta lição, você ativará seus esquemas e conjuntos de dados para o Perfil do cliente em tempo real.

Ok, menti quando disse que a lição de conjuntos de dados era a lição mais curta deste tutorial — esta deveria levar ainda menos tempo! Literalmente, tudo o que você vai fazer é virar um monte de interruptores. Mas o que acontece quando você inverte esses botões é _realmente_ importante, então eu gostaria de dedicar uma página inteira a ele.

Com o Perfil do cliente em tempo real, você pode ter uma visualização integral de cada cliente individual, combinando dados de vários canais, inclusive dados online, offline, de CRM e de terceiros. O Perfil permite consolidar dados diferentes do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

Por incrível que pareça, você não precisa ativar *todos os seus dados* para o perfil. Na verdade, você só deve ativar os dados necessários para casos de uso de ativação. Ative os dados que você deseja usar para casos de uso de marketing, integrações com a central de atendimento e assim por diante, onde é necessário acesso rápido a um perfil de cliente robusto. Se você estiver carregando dados somente para análise, eles provavelmente não deverão ser ativados para o perfil.

Há [medidas de proteção importantes para os dados de Perfil do cliente em tempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en) que você deve examinar ao decidir quais dos seus próprios dados deve habilitar para o perfil.

<!--is this accurate. Are there other considerations to point out? -->

Os **Arquitetos de dados** precisarão ativar o Perfil do cliente em tempo real fora deste tutorial.

Antes de começar os exercícios, assista a este vídeo curto para saber mais sobre o Perfil do cliente em tempo real:
>[!VIDEO](https://video.tv.adobe.com/v/27251?learn=on)

## Permissões necessárias

Na lição [Configurar Permissões](configure-permissions.md), você configura todos os controles de acesso necessários para concluir esta lição.


<!--* Permission items **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## Ativar esquemas para o Perfil de cliente em tempo real usando a interface do usuário da plataforma

Vamos começar com a tarefa simples de ativar um esquema:

1. Na interface do usuário da Platform, abra o **Esquema de fidelidade Luma**
1. Em **[!UICONTROL Propriedades do Esquema]**, alterne a opção **Perfil**
1. No modal de confirmação, pressione o botão **[!UICONTROL Habilitar]** para confirmar
1. Selecione o botão **[!UICONTROL Salvar]** para salvar suas alterações

   >[!IMPORTANT]
   >
   >Depois que um esquema é ativado para o Perfil, ele não pode ser desativado ou excluído. Além disso, os campos não podem ser removidos do esquema após esse ponto. Essas implicações são importantes para ter em mente posteriormente quando você estiver trabalhando com seus próprios dados no ambiente de produção. Você deve usar uma sandbox de desenvolvimento neste tutorial, que pode ser excluída a qualquer momento.
   >
   >No ambiente controlado deste tutorial, você habilitará seus esquemas e conjuntos de dados para o perfil, _antes de assimilar dados_. Ao trabalhar com seus próprios dados, recomendamos que você faça as coisas na seguinte ordem:
   >
   > 1. Primeiro, assimile alguns dados em seus conjuntos de dados.
   > 1. Resolva quaisquer problemas que surjam durante o processo de assimilação de dados (por exemplo, problemas de validação ou mapeamento de dados).
   > 1. Ativar seus conjuntos de dados e esquemas para o Perfil
   > 1. Assimilar os dados


   ![Alternância de perfil](assets/profile-loyalty-enableSchema.png)

Fácil, não é? Repita as etapas acima para esse outro schema:

1. Esquema do catálogo de produtos Luma
1. Esquema de eventos de compra offline da Luma
1. Esquema de eventos da Web da Luma (no modal de confirmação, marque a caixa &quot;Os dados deste esquema conterão uma identidade primária no campo identityMap&quot;).

## Ativar esquemas para o Perfil do cliente em tempo real usando a API da plataforma

Agora, é hora de habilitar o `Luma CRM Schema` com a API. Se você quiser ignorar este exercício e simplesmente ativá-lo na interface do usuário, vá em frente.

### Obtenha o meta:altId do esquema

Primeiro, vamos obter o `meta:altId` de `Luma CRM Schema`:

1. Abrir [!DNL Postman]
1. Se você não tiver um token de acesso, abra a solicitação **[!DNL OAuth: Request Access Token]** e selecione **Enviar** para solicitar um novo token de acesso, exatamente como você fez na lição [!DNL Postman].
1. Abrir a solicitação **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**
1. Selecione o botão **Enviar**
1. Você deve receber uma resposta 200
1. Examine a resposta para o item `Luma CRM Schema` e copie o valor `meta:altId`
   ![Copiar meta:altIid](assets/profile-crm-getMetaAltId.png)

### Ativar o esquema

Agora que temos o meta:altId do esquema, podemos habilitá-lo para o perfil:

1. Abrir a solicitação **[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]**
1. No **Params**, cole seu valor `meta:altId` como o valor do parâmetro `SCHEMA_ID`
1. Na guia **Corpo**, cole o seguinte código

   ```json
   [{
       "op": "add",
       "path": "/meta:immutableTags",
       "value": ["union"]
   }]
   ```

1. Selecione o botão **Enviar**
1. Você deve receber uma resposta 200

   ![Habilite o esquema do CRM para o perfil com seu meta:altIid personalizado usado como o parâmetro SCHEMA_ID](assets/profile-crm-enableProfile.png)

Você poderá ver na interface que todos os cinco esquemas estão habilitados para o Perfil (talvez seja necessário SHIFT-Reload para ver que `Luma CRM Schema` está habilitado):
![Todos os esquemas habilitados](assets/profile-allSchemasEnabled.png)


## Ativar conjuntos de dados para o Perfil do cliente em tempo real usando a interface do usuário da plataforma

Os conjuntos de dados também devem ser ativados para o Perfil e o processo é ainda mais simples:

1. Na interface do usuário da Platform, abra o `Luma Loyalty Dataset`
1. Alternar a opção **[!UICONTROL Perfil]**
1. No modal de confirmação, pressione o botão **[!UICONTROL Habilitar]** para confirmar

   ![ Alternância de perfil](assets/profile-loyalty-enableDataset.png)

Repita as etapas acima para esses outros conjuntos de dados:

1. Conjunto de dados do catálogo de produtos Luma
1. Conjunto de dados de eventos de compra offline da Luma
1. Conjunto de dados de eventos da Web da Luma

>[!NOTE]
>
>Diferentemente dos esquemas, você pode desativar conjuntos de dados do Perfil, no entanto, todos os dados assimilados anteriormente permanecerão no Perfil.

## Ativar conjuntos de dados para o Perfil do cliente em tempo real usando a API da plataforma

Agora você ativará um conjunto de dados para o Perfil usando a API. Novamente, se você quiser ativá-lo pela interface do usuário usando o método acima, tudo bem também.

### Obter a ID do conjunto de dados

Primeiro precisamos obter o `id` do `Luma CRM Dataset`:

1. Abrir [!DNL Postman]
1. Se você não tiver um token de acesso, abra a solicitação **[!DNL OAuth: Request Access Token]** e selecione **Enviar** para solicitar um novo token de acesso, exatamente como você fez na lição [!DNL Postman].
1. Abrir a solicitação **[!DNL Catalog Service API > Datasets > Retrieve a list of datasets.]**
1. Selecione o botão **Enviar**
1. Você deve receber uma resposta 200
1. Examine a resposta para o item `Luma CRM Dataset` e copie a id:
   ![Copiar a ID](assets/profile-crm-copyDatasetId.png)

### Ativar o conjunto de dados

Agora que temos a ID do conjunto de dados, podemos habilitá-la para o perfil:

1. Abrir a solicitação **[!DNL Catalog Service API > Datasets > Update one or more attributes of a dataset specified by ID.]**
1. No **Params**, atualize o valor `DATASET_ID` para o seu próprio
1. Na guia **Corpo**, cole o código a seguir. Observe que os dois primeiros valores são tags pré-existentes que estão visíveis na resposta anterior. Elas precisam ser incluídas no corpo, além das duas novas tags que estamos adicionando:

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

1. Selecione o botão **Enviar**
1. Você deve receber uma resposta 200

   ![Habilite o conjunto de dados do CRM para o perfil, certificando-se de usar sua ID de conjunto de dados personalizada como o parâmetro DATASET_ID](assets/profile-crm-enableDataset.png)

Você também pode confirmar se a interface do usuário mostra o conjunto de dados habilitado:
![Confirmar](assets/profile-crm-confirmEnabled.png)

>[!IMPORTANT]
>
> Se você assimilar dados antes de ativar o esquema e o conjunto de dados para o perfil, será necessário assimilar novamente esses dados depois.

## Recursos adicionais

* [Documentação de Perfil do Cliente em Tempo Real](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=pt-BR)
* [Referência da API do Perfil do cliente em tempo real](https://www.adobe.io/experience-platform-apis/references/profile/)


**Engenheiros de dados** deve continuar para a lição [Assinar eventos de assimilação de dados](subscribe-to-data-ingestion-events.md).
**Os arquitetos de dados** _podem ignorar_ e acessar a [lição de assimilação em lote](ingest-batch-data.md).
