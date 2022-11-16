---
title: Assimilar dados em lote
seo-title: Ingest batch data | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Assimilar dados em lote
description: Nesta lição, você assimilará dados em lote no Experience Platform usando vários métodos.
role: Data Engineer
feature: Data Ingestion
kt: 4348
thumbnail: 4348-ingest-batch-data.jpg
exl-id: fc7db637-e191-4cc7-9eec-29f4922ae127
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '2529'
ht-degree: 0%

---

# Assimilar dados em lote

<!-- 1hr-->
Nesta lição, você assimilará dados em lote no Experience Platform usando vários métodos.

A assimilação de dados em lote permite assimilar uma grande quantidade de dados no Adobe Experience Platform de uma só vez. Você pode assimilar dados em lote de uma vez por upload na interface do Platform ou usando a API. Você também pode configurar carregamentos em lote regularmente agendados de serviços de terceiros, como serviços de armazenamento em nuvem, usando conectores de origem.

**Engenheiros de dados** O precisará assimilar dados de lote fora deste tutorial.

Antes de começar os exercícios, assista a este breve vídeo para saber mais sobre a assimilação de dados:
>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)


## Permissões necessárias

No [Configurar permissões](configure-permissions.md) lição, configure todos os controles de acesso necessários para concluir esta lição.

<!--
* Permission item **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]**, **[!UICONTROL Manage Datasets]** and **[!UICONTROL Data Monitoring]**
* Permission items **[!UICONTROL Data Ingestion]** > **[!UICONTROL View Sources]** and **[!UICONTROL Manage Sources]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

Você precisará acessar um servidor (S)FTP ou uma solução de armazenamento em nuvem para o exercício Fontes . Há uma solução alternativa se você não tiver uma.

## Assimilar dados em lotes com a interface do usuário da Platform

Os dados podem ser carregados diretamente em um conjunto de dados na tela de conjuntos de dados em formatos JSON e parquet. Essa é uma ótima maneira de testar a assimilação de alguns de seus dados após criar um

### Baixar e preparar os dados

Primeiro, obtenha os dados de amostra e personalize-os para seu locatário:

>[!NOTE]
>
>Os dados contidos na variável [luma-data.zip](assets/luma-data.zip) O ficheiro é fictício e deve ser utilizado apenas para fins de demonstração.

1. Baixar [luma-data.zip](assets/luma-data.zip) para **Ativos do tutorial do Luma** pasta.
1. Descompacte o arquivo, criando uma pasta chamada `luma-data` que contém os quatro arquivos de dados que usaremos nesta lição
1. Abrir `luma-loyalty.json` em um editor de texto e substitua todas as instâncias de `_techmarketingdemos` com sua própria id de locatário do underscore, conforme visto em seus próprios schemas:
   ![Sublinhado da ID do locatário](assets/ingestion-underscoreTenant.png)

1. Salve o arquivo atualizado

### Assimilar os dados

1. Na interface do usuário da Plataforma, selecione **[!UICONTROL Conjuntos de dados]** na navegação à esquerda
1. Abra seu `Luma Loyalty Dataset`
1. Role para baixo até ver a variável **[!UICONTROL Adicionar dados]** na coluna direita
1. Faça upload do `luma-loyalty.json` arquivo.
1. Depois que o arquivo for carregado, uma linha para o lote será exibida
1. Se você recarregar a página após alguns minutos, verá que o lote foi carregado com êxito com 1000 registros e 1000 fragmentos de perfil.

   ![Assimilação](assets/ingestion-loyalty-uploadJson.png)
<!--do i need to explain error diagnostics and partial ingestion-->

>[!NOTE]
>
>Há algumas opções, **[!UICONTROL Diagnóstico de erros]** e **[!UICONTROL Ingestão parcial]**, que você verá em várias telas nesta lição. Essas opções não são abordadas no tutorial. Algumas informações rápidas:
>
>* Habilitar o diagnóstico de erro gera dados sobre a assimilação de seus dados, que podem ser revisados usando a API de acesso a dados. Saiba mais sobre isso em [a documentação](https://experienceleague.adobe.com/docs/experience-platform/data-access/home.html).
>* A assimilação parcial permite assimilar dados contendo erros, até um determinado limite que você pode especificar. Saiba mais sobre isso em [a documentação](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/partial.html)


### Validar os dados

Há algumas maneiras de confirmar se os dados foram assimilados com êxito.

#### Validar na interface do usuário da plataforma

Para confirmar que os dados foram assimilados no conjunto de dados:

1. Na mesma página em que os dados foram assimilados, selecione o **[!UICONTROL Visualizar conjunto de dados]** botão no canto superior direito
1. Selecione o **Visualizar** e você poderá ver alguns dos dados assimilados.

   ![Visualizar o conjunto de dados bem-sucedido](assets/ingestion-loyalty-preview.png)


Para confirmar que os dados chegaram ao Perfil (pode levar alguns minutos para que os dados sejam encaminhados):

1. Ir para **[!UICONTROL Perfis]** na navegação à esquerda
1. Selecione o ícone ao lado do **[!UICONTROL Selecionar namespace de identidade]** campo para abrir o modal
1. Selecione seu `Luma Loyalty Id` namespace
1. Em seguida, insira um dos `loyaltyId` valores do seu conjunto de dados,  `5625458`
1. Selecionar **[!UICONTROL Exibir]**

   ![Confirmar um perfil no conjunto de dados](assets/ingestion-loyalty-profile.png)

#### Validar com eventos de assimilação de dados

Se você se inscreveu em eventos de assimilação de dados na lição anterior, verifique o URL exclusivo do webhook.site. Você deve ver três solicitações exibidas na seguinte ordem, com algum tempo entre elas, com o seguinte `eventCode` valores:

1. `ing_load_success`—lote ingerido
1. `ig_load_success`—o lote foi assimilado no gráfico de identidade
1. `ps_load_success`—o lote foi assimilado no serviço de perfil

![Webhook da assimilação de dados](assets/ingestion-loyalty-webhook.png)

Consulte a [documentação](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html#available-status-notification-events) para obter mais detalhes sobre as notificações.

## Assimilar dados em lotes com a API da plataforma

Agora vamos fazer upload de dados usando a API.

>[!NOTE]
>
>Os arquitetos de dados podem fazer upload dos dados do CRM por meio do método da interface do usuário.

### Baixar e preparar os dados

1. Você já deve ter baixado e descompactado [luma-data.zip](assets/luma-data.zip) em seu `Luma Tutorial Assets` pasta.
2. Abrir `luma-crm.json` em um editor de texto e substitua todas as instâncias de `_techmarketingdemos` com sua própria id de locatário do underscore, como visualizado em seus esquemas
3. Salve o arquivo atualizado

### Obter a ID do conjunto de dados

Primeiro, obtemos a id do conjunto de dados no qual queremos assimilar dados:

1. Abrir [!DNL Postman]
1. Se você não tiver feito uma solicitação nas últimas 24 horas, seus tokens de autorização provavelmente expiraram. Abrir a solicitação **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]** e selecione **Enviar** para solicitar novos tokens de acesso e JWT, como você fez no [!DNL Postman] lição.
1. Abra as variáveis de ambiente e verifique se o valor de **CONTAINER_ID** ainda está `tenant`
1. Abrir a solicitação **[!DNL Catalog Service API > Datasets > Retrieve a list of datasets.]** e selecione **Enviar**
1. Você deveria pegar um `200 OK` response
1. Copie a ID do `Luma CRM Dataset` do corpo de resposta
   ![Obter a ID do conjunto de dados](assets/ingestion-crm-getDatasetId.png)

### Criar o lote

Agora podemos criar um lote no conjunto de dados:

1. Baixar [API de assimilação de dados.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Data%20Ingestion%20API.postman_collection.json) para `Luma Tutorial Assets` pasta
1. Importe a coleção para [!DNL Postman]
1. Selecionar a solicitação **[!DNL Data Ingestion API > Batch Ingestion > Create a new batch in Catalog Service.]**
1. Cole o seguinte como o **Corpo** do pedido, ***substituição do valor do conjunto de dadosId por seu próprio***:

   ```json
   {
       "datasetId":"REPLACE_WITH_YOUR_OWN_DATASETID",
       "inputFormat": {
           "format": "json"
       }
   }
   ```

1. Selecione o **Enviar** botão
1. Você deve obter uma resposta 201 Created contendo a id do novo lote!
1. Copie o `id` do novo lote
   ![Lote criado](assets/ingestion-crm-createBatch.png)

### Assimilar os dados

Agora podemos fazer upload dos dados no lote:

1. Selecionar a solicitação **[!DNL Data Ingestion API > Batch Ingestion > Upload a file to a dataset in a batch.]**
1. No **Params** , insira a id do conjunto de dados e a id do lote em seus respectivos campos
1. No **Params** guia , digite `luma-crm.json` como **filePath**
1. No **Corpo** selecione a guia **binário** opção
1. Selecione o download `luma-crm.json` do local `Luma Tutorial Assets` pasta
1. Selecionar **Enviar** e você deve obter uma resposta 200 OK com &#39;1&#39; no corpo da resposta

   ![Dados carregados](assets/ingestion-crm-uploadFile.png)

Neste ponto, se você observar seu lote na interface do usuário da plataforma, verá que ele está em um &quot;[!UICONTROL Carregamento]&quot; status:
![Carregamento em lote](assets/ingestion-crm-loading.png)

Como a API em lote é frequentemente usada para carregar vários arquivos, é necessário informar à Platform quando um lote é concluído, o que faremos na próxima etapa.

### Complete o lote

Para concluir o lote:

1. Selecionar a solicitação **[!DNL Data Ingestion API > Batch Ingestion > Finish uploading a file to a dataset in a batch.]**
1. No **Params** guia , digite `COMPLETE` como **ação**
1. No **Params** , insira a id do lote. Não se preocupe com a ID do conjunto de dados ou com o filePath, se estiverem presentes.
1. Certifique-se de que o URL do POST seja `https://platform.adobe.io/data/foundation/import/batches/:batchId?action=COMPLETE` e que não há referências desnecessárias ao `datasetId` ou `filePath`
1. Selecionar **Enviar** e você deve obter uma resposta 200 OK com &#39;1&#39; no corpo da resposta

   ![Lote concluído](assets/ingestion-crm-complete.png)

### Validar os dados

#### Validar na interface do usuário da plataforma

Valide se os dados chegaram na interface do usuário da Plataforma da mesma forma que aconteceu com o conjunto de dados de Fidelidade.

Primeiro, confirme se o lote mostra que 1000 registros assimilaram:

![Êxito em lote](assets/ingestion-crm-success.png)

Em seguida, confirme o lote usando o conjunto de dados de Visualização:

![Visualização em lote](assets/ingestion-crm-preview.png)

Por fim, confirme se um de seus perfis foi criado pesquisando um dos perfis pelo `Luma CRM Id` namespace, por exemplo `112ca06ed53d3db37e4cea49cc45b71e`

![Perfil assimilado](assets/ingestion-crm-profile.png)

Há uma coisa interessante que aconteceu e que eu quero destacar. Abra o `Danny Wright` perfil. O perfil tem uma `Lumacrmid` e `Lumaloyaltyid`. Lembre-se do `Luma Loyalty Schema` continha dois campos de identidade, ID da Fidelidade do Luma e ID do CRM. Agora que carregamos ambos os conjuntos de dados, eles foram mesclados em um único perfil. Os dados de fidelidade tinham `Daniel` como o nome e &quot;Nova York&quot; como endereço residencial, enquanto os dados do CRM tinham `Danny` como nome e `Portland` como o endereço residencial do cliente com a mesma ID de fidelidade. Voltaremos ao motivo pelo qual o nome é exibido `Danny` na lição sobre políticas de mesclagem.

Parabéns, você acabou de unir perfis!

![Perfil mesclado ](assets/ingestion-crm-profileLinkedIdentities.png)

#### Validar com eventos de assimilação de dados

Se você se inscreveu em eventos de assimilação de dados na lição anterior, verifique o URL exclusivo do webhook.site. Você deve ver três solicitações entrando, assim como com os dados de fidelidade:

![Webhook da assimilação de dados](assets/ingestion-crm-webhook.png)

Consulte a [documentação](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html#available-status-notification-events) para obter mais detalhes sobre as notificações.

## Assimilar dados com fluxos de trabalho

Vamos analisar outra maneira de fazer upload de dados. O recurso de fluxos de trabalho permite assimilar dados CSV que ainda não foram modelados no XDM.

### Baixar e preparar os dados

1. Você já deve ter baixado e descompactado [luma-data.zip](assets/luma-data.zip) em seu `Luma Tutorial Assets` pasta.
1. Confirme que você`luma-products.csv`

### Criar um fluxo de trabalho

Agora vamos configurar o workflow:

1. Ir para **[!UICONTROL Fluxos de trabalho]** na navegação à esquerda
1. Selecionar **[!UICONTROL Mapear CSV para esquema XDM]** e selecione o **[!UICONTROL Launch]** botão
   ![Iniciar o workflow](assets/ingestion-products-launchWorkflow.png)
1. Selecione seu `Luma Product Catalog Dataset` e selecione o **[!UICONTROL Próximo]** botão
   ![Selecionar seu conjunto de dados](assets/ingestion-products-selectDataset.png)
1. Adicione o `luma-products.csv` e selecione o **[!UICONTROL Próximo]** botão
   ![Selecionar seu conjunto de dados](assets/ingestion-products-selectData.png)
1. Agora você está na interface do mapeador, na qual pode mapear um campo a partir dos dados de origem (um dos nomes da coluna na `luma-products.csv` para campos XDM no esquema de destino. No nosso exemplo, os nomes das colunas estão próximos o suficiente dos nomes dos campos do esquema que o mapeador pode detectar automaticamente o mapeamento correto! Se o mapeador não conseguisse detectar automaticamente o campo direito, você selecionaria o ícone à direita do campo de destino para selecionar o campo XDM correto. Além disso, se você não quiser assimilar uma das colunas do CSV, poderá excluir a linha do mapeador. Sinta-se à vontade para reproduzir e alterar cabeçalhos de coluna na `luma-products.csv` para se familiarizar com o funcionamento do mapeador.
1. Selecione o **[!UICONTROL Concluir]** botão
   ![Selecionar seu conjunto de dados](assets/ingestion-products-mapper.png)

### Validar os dados

Quando o lote tiver carregado, verifique o upload visualizando o conjunto de dados.

Como a variável `Luma Product SKU` for um namespace que não seja de pessoas, não veremos nenhum perfil para as SKUs do produto.

Você deve ver as três ocorrências no seu webhook.

## Assimilar dados com Fontes

Ok, você fez as coisas da maneira mais difícil. Agora vamos nos mudar para a terra prometida de _automatizado_ ingestão em lote! Quando eu digo, &quot;DEFINA!&quot; você diz: &quot;ESQUEÇA!&quot; &quot;DEFINA!&quot; &quot;ESQUEÇA!&quot; &quot;DEFINA!&quot; &quot;ESQUEÇA!&quot; Só brincando, você nunca faria tal coisa! Ok, de volta ao trabalho. Você está quase pronto.

Ir para **[!UICONTROL Fontes]** no painel de navegação esquerdo para abrir o catálogo de Fontes. Aqui você verá várias integrações prontas para uso com os provedores líderes do setor de dados e armazenamento.

![Catálogo de origem](assets/ingestion-offline-sourceCatalog.png)

Ok, vamos assimilar dados usando um conector de origem.

Esse exercício será um estilo de aventura. Vou mostrar o workflow usando o conector de origem FTP. Você pode usar um conector de origem do Armazenamento na nuvem diferente usado em sua empresa ou fazer upload do arquivo json usando a interface do usuário do conjunto de dados, como fizemos com os dados de fidelidade.

Muitas das Fontes têm um fluxo de trabalho de configuração semelhante, no qual você:

1. Insira os detalhes de autenticação
1. Selecione os dados que deseja assimilar
1. Selecione o conjunto de dados da plataforma no qual deseja assimilá-lo
1. Mapeie os campos para o esquema XDM
1. Escolha a frequência com que deseja assimilar dados desse local

>[!NOTE]
>
>Os dados de Compra offline que usaremos neste exercício contêm dados de data e hora. Os dados de data e hora devem estar em [Strings formatadas ISO 8061](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15:05:59.000-08:00&quot;) ou Tempo Unix formatado em milissegundos (1531263959000) e são convertidos no momento da assimilação para o tipo XDM de destino. Para obter mais informações sobre conversão de dados e outras restrições, consulte [a documentação da API de assimilação em lote](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/api-overview.html#types).

### Baixe, prepare e faça upload dos dados para seu fornecedor preferido de armazenamento em nuvem

1. Você já deve ter baixado e descompactado [luma-data.zip](assets/luma-data.zip) em seu `Luma Tutorial Assets` pasta.
1. Abrir `luma-offline-purchases.json` em um editor de texto e substitua todas as instâncias de `_techmarketingdemos` com sua própria id de locatário do underscore, como visualizado em seus esquemas
1. Escolha seu provedor de armazenamento em nuvem preferido, certificando-se de que ele esteja disponível na [!UICONTROL Fontes] catálogo
1. Upload `luma-offline-purchases.json` para um local no seu provedor de armazenamento em nuvem preferido

### Assimilar os dados ao local de armazenamento em nuvem de sua preferência

1. Na interface do usuário da Platform, filtre o [!UICONTROL Fontes] catálogo para **[!UICONTROL armazenamento na nuvem]**
1. Observe que há links convenientes para a documentação na seção `...`
1. Na caixa de seu fornecedor preferencial de armazenamento em nuvem, selecione o **[!UICONTROL Configurar]** botão
   ![Selecionar configurar](assets/ingestion-offline-selectFTP.png)
1. **[!UICONTROL Autenticação]** é o primeiro passo. Insira o nome da sua conta, por exemplo `Luma's FTP Account` e seus detalhes de autenticação. Essa etapa deve ser bastante semelhante para todas as fontes de armazenamento em nuvem, embora os campos possam variar um pouco. Depois de ter inserido os detalhes de autenticação de uma conta, você pode reutilizá-los em outras conexões de origem que podem estar enviando dados diferentes em agendamentos diferentes de outros arquivos na mesma conta
1. Selecione o **[!UICONTROL Botão Conectar-se à origem]**
1. Quando a Plataforma tiver se conectado com êxito à Origem, selecione a variável **[!UICONTROL Próximo]** botão
   ![Autenticar para a origem](assets/ingestion-offline-authentication.png)

1. No **[!UICONTROL Selecionar dados]** , a interface do usuário usará suas credenciais para abrir a pasta na solução de armazenamento da nuvem
1. Selecione os arquivos que deseja assimilar, por exemplo `luma-offline-purchases.json`
1. Como **[!UICONTROL Formato dos dados]**, selecione `XDM JSON`
1. Em seguida, você pode visualizar a estrutura json e os dados de amostra no arquivo
1. Selecione o **[!UICONTROL Próximo]** botão
   ![Selecione os arquivos de dados](assets/ingestion-offline-selectData.png)

1. No **[!UICONTROL Mapeamento]** selecione seu `Luma Offline Purchase Events Dataset` e selecione o **[!UICONTROL Próximo]** botão. Observe na mensagem que, como os dados que estamos assimilando são um arquivo JSON, não há uma etapa de mapeamento em que mapeamos o campo de origem para o campo de destino. Os dados JSON já devem estar no XDM. Se você estivesse assimilando um CSV, veria a interface completa do usuário de mapeamento nesta etapa:
   ![Selecionar seu conjunto de dados](assets/ingestion-offline-mapping.png)
1. No **[!UICONTROL Agendamento]** , escolha a frequência com que deseja assimilar dados da Fonte. Reserve um momento para ver as opções. Vamos apenas fazer uma ingestão única, então deixe o **[!UICONTROL Frequência]** on **[!UICONTROL Uma vez]** e selecione o **[!UICONTROL Próximo]** botão:
   ![Programar o fluxo de dados](assets/ingestion-offline-scheduling.png)
1. No **[!UICONTROL Detalhes do fluxo de dados]** , você pode escolher um nome para o fluxo de dados, inserir uma descrição opcional, ativar o diagnóstico de erros e a assimilação parcial. Deixe as configurações como estão e selecione o **[!UICONTROL Próximo]** botão:
   ![Editar detalhes do fluxo de dados](assets/ingestion-offline-detail.png)
1. No **[!UICONTROL Revisão]** , é possível revisar todas as configurações e editá-las ou selecionar a **[!UICONTROL Concluir]** botão
1. Depois de salvar, você será direcionado para uma tela como esta:
   ![Concluir](assets/ingestion-offline-complete.png)

### Validar os dados

Quando o lote tiver carregado, verifique o upload visualizando o conjunto de dados.

Você deve ver as três ocorrências no seu webhook.

Procure o perfil com valor `5625458` no `loyaltyId` namespace novamente para ver se há eventos de compra em seu perfil. Você deve ver uma compra. Você pode acessar os detalhes da compra selecionando **[!UICONTROL Exibir JSON]**:

![Evento de compra no perfil](assets/ingestion-offline-eventInProfile.png)

## Ferramentas ETL

A Adobe faz parceria com vários fornecedores de ETL para dar suporte à assimilação de dados no Experience Platform. Devido à variedade de fornecedores de terceiros, o ETL não é abordado neste tutorial, embora você seja bem-vindo a revisar alguns desses recursos:

* [Desenvolvimento de integrações de ETL para o Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/etl/home.html)
* [Página Informatica Adobe Experience Platform Connector no Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101570.informatica-adobe-experience-cloud-connector.html)
* [Documentação informativa do Adobe Experience Platform Connector ](https://docs.informatica.com/integration-cloud/cloud-data-integration-connectors/current-version/adobe-experience-platform-connector/preface.html)
* [Experiências de público-alvo exclusivas derivadas dos dados: Unifi e Adobe Experience Platform](https://unifisoftware.com/solutions/adobe-experience-platform/)
* [[!DNL Snaplogic] Pacote do Adobe Experience Platform Snap](https://www.snaplogic.com/resources/videos/august-2020-aep)

## Recursos adicionais

* [Documentação de assimilação em lote](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html)
* [Referência da API de assimilação em lote](https://www.adobe.io/experience-platform-apis/references/data-ingestion/#tag/Batch-Ingestion)

Agora vamos [dados de fluxo usando o SDK da Web](ingest-streaming-data.md)
