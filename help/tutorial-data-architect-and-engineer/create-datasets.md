---
title: Criar conjuntos de dados
seo-title: Create datasets | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Criar conjuntos de dados
description: Nesta lição, você criará conjuntos de dados para receber seus dados.
role: Data Architect, Data Engineer
feature: Data Management
jira: KT-4348
thumbnail: 4348-create-datasets.jpg
exl-id: 80227af7-4976-4fd2-b1d4-b26bc4626fa0
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 6%

---

# Criar conjuntos de dados

<!--15min-->

Nesta lição, você criará conjuntos de dados para receber seus dados. Você ficará animado em saber que esta é a lição mais curta do tutorial!

Todos os dados assimilados com sucesso na Adobe Experience Platform são mantidos no data lake como conjuntos de dados. Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela, que contém um esquema (colunas) e campos (linhas). Os conjuntos de dados também contêm metadados que descrevem vários aspectos dos dados armazenados.

**Os Arquitetos de Dados** precisarão criar conjuntos de dados fora deste tutorial.

Antes de começar os exercícios, assista a este vídeo curto para saber mais sobre conjuntos de dados:
>[!VIDEO](https://video.tv.adobe.com/v/34332?learn=on&enablevpops&captions=por_br)

## Permissões necessárias

Na lição [Configurar Permissões](configure-permissions.md), você configura todos os controles de acesso necessários para concluir esta lição.

<!--
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## Criar conjuntos de dados na interface do

Neste exercício, criaremos conjuntos de dados na interface do usuário. Vamos começar com os dados de fidelidade:

1. Vá para **[!UICONTROL Conjuntos de dados]** na navegação à esquerda da interface de usuário da plataforma
1. Selecione o botão **[!UICONTROL Criar conjunto de dados]**
   ![Criar um conjunto de dados](assets/datasets-createDataset.png)

1. Na próxima tela, selecione **Criar conjunto de dados do esquema**
1. Na próxima tela, selecione o `Luma Loyalty Schema` e o botão **[!UICONTROL Avançar]**
   ![Selecionar o conjunto de dados](assets/datasets-selectSchema.png)

1. Nomeie o conjunto de dados `Luma Loyalty Dataset` e selecione o botão **[!UICONTROL Concluir]**
   ![Nomear o conjunto de dados](assets/datasets-nameDataset.png)
1. Quando o conjunto de dados for salvo, você será direcionado a uma tela como esta:
   ![Conjunto de dados criado](assets/datasets-created.png)

Pronto! Eu te disse que isso seria rápido. Crie esses outros conjuntos de dados usando as mesmas etapas:

1. `Luma Offline Purchase Events Dataset` para o seu `Luma Offline Purchase Events Schema`
1. `Luma Web Events Dataset` para o seu `Luma Web Events Schema`
1. `Luma Product Catalog Dataset` para o seu `Luma Product Catalog Schema`


## Criar um conjunto de dados usando a API

Agora crie o `Luma CRM Dataset` usando a API.

>[!NOTE]
>
>Se quiser ignorar o exercício de API e criar o `Luma CRM Dataset` na interface do usuário, tudo bem. Nomeie `Luma CRM Dataset` e use o `Luma CRM Schema`.

### Obter a ID do esquema a ser usado no conjunto de dados

Primeiro precisamos obter o `$id` do `Luma CRM Schema`:

1. Abrir [!DNL Postman]
1. Se você não tiver um token de acesso, abra a solicitação **[!DNL OAuth: Request Access Token]** e selecione **Enviar** para solicitar um novo token de acesso, exatamente como você fez na lição [!DNL Postman].
1. Abrir a solicitação **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**
1. Selecione o botão **Enviar**
1. Você deve receber uma resposta 200
1. Examine a resposta para o item `Luma CRM Schema` e copie o valor `$id`
   ![Copiar a $id](assets/dataset-crm-getSchemaId.png)

### Criar o conjunto de dados

Agora é possível criar o conjunto de dados:

1. Baixe o [Serviço de Catálogo API.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Catalog%20Service%20API.postman_collection.json) na pasta `Luma Tutorial Assets`.
1. Importar a coleção para [!DNL Postman]
1. Selecionar a solicitação **[!DNL Catalog Service API > Datasets > Create a new dataset.]**
1. Cole o seguinte como o **Corpo** da solicitação, ***substituindo o valor de id pelo seu próprio***:

   ```json
   {
       "name": "Luma CRM Dataset",
   
       "schemaRef": {
           "id": "REPLACE_WITH_YOUR_OWN_ID",
           "contentType": "application/vnd.adobe.xed-full+json;version=1"
       },
       "fileDescription": {
           "persisted": true,
           "containerFormat": "parquet",
           "format": "parquet"
       }
   }
   ```

1. Selecione o botão **Enviar**
1. Você deve receber uma resposta criada em 201 contendo a ID do novo conjunto de dados!
   ![Conjunto de dados criado com a API, sua $id personalizada usada no corpo](assets/datasets-crm-created.png)

>[!TIP]
>
> Problemas comuns que fazem essa solicitação e prováveis correções:
>
> * `400: There was a problem retrieving xdm schema`. Verifique se você substituiu a ID na amostra acima pela ID do seu próprio `Luma CRM Schema`
> * Nenhum token de autenticação: execute a solicitação **OAuth: Request Access Token** para gerar um novo token
> * `401: Not Authorized to PUT/POST/PATCH/DELETE for this path : /global/schemas/`: Atualizar a variável de ambiente **CONTAINER_ID** de `global` para `tenant`
> * `403: PALM Access Denied. POST access is denied for this resource from access control`: Verifique suas permissões de usuário no Admin Console


Você pode voltar para a tela **[!UICONTROL Conjuntos de dados]** na interface do usuário da Platform e verificar se a criação dos cinco conjuntos de dados foi bem-sucedida.
![Cinco conjuntos de dados concluídos](assets/datasets-allComplete.png)


## Recursos adicionais

* [Documentação de conjuntos de dados](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=pt-BR)
* [Referência da API dos conjuntos de dados (parte do Serviço de Catálogo)](https://www.adobe.io/experience-platform-apis/references/catalog/#tag/Datasets)

Agora que todos os nossos esquemas, identidades e conjuntos de dados estão em vigor, podemos [habilitá-los para o Perfil de cliente em tempo real](enable-profiles.md).
