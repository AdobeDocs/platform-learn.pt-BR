---
title: Assimilar dados em lote
seo-title: Ingest batch data | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Assimilar dados em lote
description: Nesta lição, você assimilará dados em lote na Experience Platform usando vários métodos.
role: Data Engineer
feature: Data Ingestion
jira: KT-4348
thumbnail: 4348-ingest-batch-data.jpg
exl-id: fc7db637-e191-4cc7-9eec-29f4922ae127
source-git-commit: e0359d1bade01f79d0f7aff6a6e69f3e4d0c3b62
workflow-type: tm+mt
source-wordcount: '2446'
ht-degree: 0%

---

# Assimilar dados em lote

<!-- 1hr-->
Nesta lição, você assimilará dados em lote na Experience Platform usando vários métodos.

A assimilação de dados em lote permite assimilar uma grande quantidade de dados na Adobe Experience Platform de uma só vez. Você pode assimilar dados em lote em um upload único na interface da Platform ou usando a API. Você também pode configurar carregamentos em lote regularmente agendados de serviços de terceiros, como serviços de armazenamento na nuvem usando conectores do Source.

**Os engenheiros de dados** precisarão assimilar dados em lote fora deste tutorial.

Antes de começar os exercícios, assista a este vídeo curto para saber mais sobre a assimilação de dados:

>[!VIDEO](https://video.tv.adobe.com/v/346835?learn=on&enablevpops&captions=por_br)


## Permissões necessárias

Na lição [Configurar Permissões](configure-permissions.md), você configura todos os controles de acesso necessários para concluir esta lição.

<!--
* Permission item **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]**, **[!UICONTROL Manage Datasets]** and **[!UICONTROL Data Monitoring]**
* Permission items **[!UICONTROL Data Ingestion]** > **[!UICONTROL View Sources]** and **[!UICONTROL Manage Sources]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

Você precisará acessar um servidor (S)FTP ou uma solução de armazenamento na nuvem para o exercício Origens. Há uma solução alternativa se você não tiver uma.

## Assimilar dados em lotes com a interface do usuário da Platform

Os dados podem ser carregados diretamente em um conjunto de dados na tela de conjuntos de dados nos formatos JSON e parquet. Essa é uma ótima maneira de testar a assimilação de alguns de seus dados após criar uma

### Baixar e preparar os dados

Primeiro, obtenha os dados de amostra e personalize-os para seu locatário:

>[!NOTE]
>
>Os dados contidos no arquivo [luma-data.zip](assets/luma-data.zip) são fictícios e devem ser usados apenas para fins de demonstração.

1. Baixe o [luma-data.zip](assets/luma-data.zip) na sua pasta **Tutorial Assets** do Luma.
1. Descompacte o arquivo, criando uma pasta chamada `luma-data` que contém os quatro arquivos de dados que usaremos nesta lição
1. Abra o `luma-loyalty.json` em um editor de texto e substitua todas as instâncias do `_techmarketingdemos` pela sua própria id de locatário com sublinhado, como vista em seus próprios esquemas:
   ![Sublinhar ID do locatário](assets/ingestion-underscoreTenant.png)

1. Salve o arquivo atualizado

### Assimilar os dados

1. Na interface da Platform, selecione **[!UICONTROL Conjuntos de dados]** na navegação à esquerda
1. Abra seu `Luma Loyalty Dataset`
1. Role para baixo até ver a seção **[!UICONTROL Adicionar dados]** na coluna direita
1. Carregar o arquivo `luma-loyalty.json`.
1. Depois que o arquivo for carregado, uma linha do lote será exibida
1. Se você recarregar a página após alguns minutos, verá que o lote foi carregado com êxito com 1000 registros e 1000 fragmentos de perfil.

   ![Assimilação](assets/ingestion-loyalty-uploadJson.png)
   <!--do i need to explain error diagnostics and partial ingestion-->

>[!NOTE]
>
>Há algumas opções, **[!UICONTROL Diagnóstico de erros]** e **[!UICONTROL Assimilação parcial]**, que você verá em várias telas nesta lição. Essas opções não são abordadas no tutorial. Algumas informações rápidas:
>
>* Habilitar o diagnóstico de erro gera dados sobre a assimilação dos dados, que podem ser revisados usando a API de acesso a dados. Saiba mais sobre isso em [a documentação](https://experienceleague.adobe.com/docs/experience-platform/data-access/home.html?lang=pt-BR).
>* A assimilação parcial permite assimilar dados que contêm erros até um determinado limite que você pode especificar. Saiba mais sobre isso em [a documentação](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/partial.html?lang=pt-BR)

### Validar os dados

Há algumas maneiras de confirmar se os dados foram assimilados com êxito.

#### Validar na interface do usuário da Platform

Para confirmar se os dados foram assimilados no conjunto de dados:

1. Na mesma página em que você assimilou os dados, selecione o botão **[!UICONTROL Visualizar conjunto de dados]** no canto superior direito
1. Selecione o botão **Visualizar** e você poderá ver alguns dos dados assimilados.

   ![Visualizar o conjunto de dados bem-sucedido](assets/ingestion-loyalty-preview.png)


Para confirmar se os dados chegaram ao Perfil (pode levar alguns minutos para que sejam enviados):

1. Vá para **[!UICONTROL Perfis]** na navegação à esquerda
1. Selecione o ícone ao lado do campo **[!UICONTROL Selecionar namespace de identidade]** para abrir a modal
1. Selecione seu namespace `Luma Loyalty Id`
1. Em seguida, insira um dos valores `loyaltyId` do seu conjunto de dados, `5625458`
1. Selecionar **[!UICONTROL Exibição]**
   ![Confirmar um perfil do conjunto de dados](assets/ingestion-loyalty-profile.png)

#### Validar com eventos de assimilação de dados

Se você se inscreveu em eventos de assimilação de dados na lição anterior, verifique o URL exclusivo do webhook.site. Você deve ver três solicitações exibidas na seguinte ordem, com algum tempo entre elas, com os seguintes valores `eventCode`:

1. `ing_load_success`—o lote foi assimilado
1. `ig_load_success`—o lote foi assimilado no gráfico de identidade
1. `ps_load_success`—o lote foi assimilado no serviço de perfil

![Webhook de assimilação de dados](assets/ingestion-loyalty-webhook.png)

Consulte a [documentação](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html?lang=pt-BR#available-status-notification-events) para obter mais detalhes sobre as notificações.

## Assimilar dados em lotes com a API da plataforma

Agora vamos carregar dados usando a API.

>[!NOTE]
>
>Arquitetos de dados, sintam-se à vontade para fazer upload dos dados do CRM pelo método da interface do usuário.

### Baixar e preparar os dados

1. Você já deve ter baixado e descompactado o [luma-data.zip](assets/luma-data.zip) na pasta `Luma Tutorial Assets`.
2. Abra o `luma-crm.json` em um editor de texto e substitua todas as instâncias do `_techmarketingdemos` pela sua própria id de locatário com sublinhado, como vista em seus esquemas
3. Salve o arquivo atualizado

### Obter a ID do conjunto de dados

Primeiro, vamos obter a ID da ID do conjunto de dados no qual queremos assimilar dados:

1. Abrir [!DNL Postman]
1. Se você não tiver um token de acesso, abra a solicitação **[!DNL OAuth: Request Access Token]** e selecione **Enviar** para solicitar um novo token de acesso, exatamente como você fez na lição [!DNL Postman].
1. Abra as variáveis de ambiente e verifique se o valor de **CONTAINER_ID** ainda é `tenant`
1. Abra a solicitação **[!DNL Catalog Service API > Datasets > Retrieve a list of datasets.]** e selecione **Enviar**
1. Você deve receber uma resposta de `200 OK`
1. Copiar a ID de `Luma CRM Dataset` do corpo da Resposta
   ![Obter a ID do conjunto de dados](assets/ingestion-crm-getDatasetId.png)

### Criar o lote

Agora podemos criar um lote no conjunto de dados:

1. Baixe a [API de assimilação de dados.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Data%20Ingestion%20API.postman_collection.json) para a pasta `Luma Tutorial Assets`
1. Importar a coleção para [!DNL Postman]
1. Selecionar a solicitação **[!DNL Data Ingestion API > Batch Ingestion > Create a new batch in Catalog Service.]**
1. Cole o seguinte como o **Corpo** da solicitação, ***substituindo o valor datasetId pelo seu próprio***:

   ```json
   {
       "datasetId":"REPLACE_WITH_YOUR_OWN_DATASETID",
       "inputFormat": {
           "format": "json"
       }
   }
   ```

1. Selecione o botão **Enviar**
1. Você deve receber uma resposta 201 Criada contendo a ID do novo lote!
1. Copiar o `id` do novo lote
   ![Lote criado](assets/ingestion-crm-createBatch.png)

### Assimilar os dados

Agora podemos fazer upload dos dados no lote:

1. Selecionar a solicitação **[!DNL Data Ingestion API > Batch Ingestion > Upload a file to a dataset in a batch.]**
1. Na guia **Params**, insira a ID do conjunto de dados e a ID do lote em seus respectivos campos
1. Na guia **Params**, digite `luma-crm.json` como o **filePath**
1. Na guia **Corpo**, selecione a opção **binário**
1. Selecione o `luma-crm.json` baixado da sua pasta `Luma Tutorial Assets` local
1. Selecione **Enviar** e você deverá receber uma resposta 200 OK com &#39;1&#39; no corpo da resposta

   ![Dados carregados](assets/ingestion-crm-uploadFile.png)

Neste ponto, se você observar o lote na interface do usuário da Platform, verá que ele está no status &quot;[!UICONTROL Carregando]&quot;:
![Carregamento em lote](assets/ingestion-crm-loading.png)

Como a API de lote é frequentemente usada para fazer upload de vários arquivos, é necessário informar à Platform quando um lote é concluído, o que faremos na próxima etapa.

### Concluir o lote

Para concluir o lote:

1. Selecionar a solicitação **[!DNL Data Ingestion API > Batch Ingestion > Finish uploading a file to a dataset in a batch.]**
1. Na guia **Params**, digite `COMPLETE` como a **ação**
1. Na guia **Params**, insira a ID do lote. Não se preocupe com a id do conjunto de dados ou filePath, se eles estiverem presentes.
1. Verifique se a URL da PUBLICAÇÃO é `https://platform.adobe.io/data/foundation/import/batches/:batchId?action=COMPLETE` e se não há referências desnecessárias para `datasetId` ou `filePath`
1. Selecione **Enviar** e você deverá receber uma resposta 200 OK com &#39;1&#39; no corpo da resposta

   ![Lote concluído](assets/ingestion-crm-complete.png)

### Validar os dados

#### Validar na interface do usuário da Platform

Validar se os dados chegaram à interface do usuário da Platform da mesma forma que você fez para o conjunto de dados de Fidelidade.

Primeiro, confirme se o lote mostra que 1000 registros foram assimilados:

![Êxito do lote](assets/ingestion-crm-success.png)

Em seguida, confirme o lote usando Visualizar conjunto de dados:

![Visualização em lote](assets/ingestion-crm-preview.png)

Finalmente, confirme se um dos perfis foi criado procurando um dos perfis pelo namespace `Luma CRM Id`, por exemplo `112ca06ed53d3db37e4cea49cc45b71e`

![Perfil assimilado](assets/ingestion-crm-profile.png)

Há uma coisa interessante que aconteceu e que eu quero destacar. Abra esse perfil `Danny Wright`. O perfil tem um `Lumacrmid` e um `Lumaloyaltyid`. Lembre-se de que `Luma Loyalty Schema` continha dois campos de identidade, ID de Fidelidade da Luma e ID do CRM. Agora que carregamos ambos os conjuntos de dados, eles foram mesclados em um único perfil. Os dados de Fidelidade tinham `Daniel` como nome e &quot;Cidade de Nova York&quot; como endereço residencial, enquanto os dados do CRM tinham `Danny` como nome e `Portland` como endereço residencial para o cliente com a mesma ID de Fidelidade. Voltaremos para o motivo pelo qual o nome exibe `Danny` na lição sobre políticas de mesclagem.

Parabéns, você acabou de mesclar perfis!

![Perfil mesclado ](assets/ingestion-crm-profileLinkedIdentities.png)

#### Validar com eventos de assimilação de dados

Se você se inscreveu em eventos de assimilação de dados na lição anterior, verifique o URL exclusivo do webhook.site. Você deve ver três solicitações recebidas, assim como com os dados de fidelidade:

![Webhook de assimilação de dados](assets/ingestion-crm-webhook.png)

Consulte a [documentação](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html?lang=pt-BR#available-status-notification-events) para obter mais detalhes sobre as notificações.

## Assimilar dados com Workflows

Vamos ver outra maneira de fazer upload de dados. O recurso de fluxos de trabalho permite assimilar dados CSV que ainda não estão modelados no XDM.

### Baixar e preparar os dados

1. Você já deve ter baixado e descompactado o [luma-data.zip](assets/luma-data.zip) na pasta `Luma Tutorial Assets`.
1. Confirme que você`luma-products.csv`

### Criar um fluxo de trabalho

Agora vamos configurar o fluxo de trabalho:

1. Vá para **[!UICONTROL Workflows]** na navegação à esquerda
1. Selecione **[!UICONTROL Mapear CSV para esquema XDM]** e selecione o botão **[!UICONTROL Iniciar]**
   ![Iniciar o fluxo de trabalho](assets/ingestion-products-launchWorkflow.png)
1. Selecione o `Luma Product Catalog Dataset` e o botão **[!UICONTROL Avançar]**
   ![Selecione seu conjunto de dados](assets/ingestion-products-selectDataset.png)
1. Adicione o arquivo `luma-products.csv` que você baixou e selecione o botão **[!UICONTROL Avançar]**
   ![Selecione seu conjunto de dados](assets/ingestion-products-selectData.png)
1. Agora você está na interface do mapeador, na qual é possível mapear um campo dos dados de origem (um dos nomes de coluna no arquivo `luma-products.csv`) para campos XDM no esquema de destino. Em nosso exemplo, os nomes das colunas estão próximos o suficiente dos nomes dos campos de esquema que o mapeador pode detectar automaticamente o mapeamento correto! Se o mapeador não puder detectar automaticamente o campo direito, você selecionaria o ícone à direita do campo de destino para selecionar o campo XDM correto. Além disso, se você não quiser assimilar uma das colunas do CSV, poderá excluir a linha do mapeador. Fique à vontade para brincar e alterar os títulos das colunas no `luma-products.csv` para se familiarizar com o funcionamento do mapeador.
1. Selecione o botão **[!UICONTROL Concluir]**
   ![Selecione seu conjunto de dados](assets/ingestion-products-mapper.png)

### Validar os dados

Quando o lote tiver sido carregado, verifique o upload visualizando o conjunto de dados.

Como o `Luma Product SKU` é um namespace que não é de pessoas, não veremos nenhum perfil para as SKUs do produto.

Você deve ver as três ocorrências do seu webhook.

## Assimilar dados com Origens

Ok, você fez as coisas do jeito difícil. Agora vamos para a terra prometida de assimilação em lote _automatizada_! Quando eu disser: &quot;AJUSTE!&quot; você diz: &quot;ESQUEÇA!&quot; &quot;DEFINA!&quot; &quot;ESQUEÇA!&quot; &quot;DEFINA!&quot; &quot;ESQUEÇA!&quot; Brincadeira, você nunca faria uma coisa dessas! Ok, de volta ao trabalho. Você está quase pronto.

Vá para **[!UICONTROL Fontes]** na navegação à esquerda para abrir o catálogo Fontes. Aqui você verá várias integrações prontas para uso com os principais provedores de armazenamento e dados do setor.

![Catálogo do Source](assets/ingestion-offline-sourceCatalog.png)

Ok, vamos assimilar dados usando um conector de origem.

Este exercício será um estilo de escolha-sua-própria-aventura. Vou mostrar o fluxo de trabalho usando o conector de origem FTP. Você pode usar um conector de origem do Cloud Storage diferente que usa em sua empresa ou fazer upload do arquivo json usando a interface do usuário do conjunto de dados, como fizemos com os dados de fidelidade.

Muitas das Fontes têm um fluxo de trabalho de configuração semelhante, no qual você:

1. Insira seus detalhes de autenticação
1. Selecione os dados que deseja assimilar
1. Selecione o conjunto de dados da plataforma no qual você deseja assimilá-lo
1. Mapear os campos para o esquema XDM
1. Escolha a frequência com que deseja assimilar dados desse local

>[!NOTE]
>
>Os dados de compras offline que usaremos neste exercício contêm dados de data e hora. Os dados de Datetime devem estar em [cadeias de caracteres formatadas em ISO 8061](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15:05:59.000-08:00&quot;) ou em Tempo Unix formatadas em milissegundos (1531263959000) e são convertidos no tempo de assimilação para o tipo XDM de destino. Para obter mais informações sobre conversão de dados e outras restrições, consulte [a documentação da API de assimilação em lote](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/api-overview.html?lang=pt-BR#types).

### Baixe, prepare e faça upload dos dados para seu fornecedor de armazenamento na nuvem preferido

1. Você já deve ter baixado e descompactado o [luma-data.zip](assets/luma-data.zip) na pasta `Luma Tutorial Assets`.
1. Abra o `luma-offline-purchases.json` em um editor de texto e substitua todas as instâncias do `_techmarketingdemos` pela sua própria id de locatário com sublinhado, como vista em seus esquemas
1. Atualizar todos os carimbos de data e hora para que os eventos ocorram no último mês (por exemplo, pesquisar `"timestamp":"2022-06` e substituir ano e mês)
1. Escolha seu provedor de armazenamento na nuvem preferido, certificando-se de que ele esteja disponível no catálogo [!UICONTROL Fontes]
1. Carregue `luma-offline-purchases.json` para um local no seu provedor de armazenamento na nuvem preferido

### Assimilar os dados no local de armazenamento na nuvem de sua preferência

1. Na interface do usuário da Platform, filtre o catálogo [!UICONTROL Fontes] para **[!UICONTROL Armazenamento na nuvem]**
1. Observe que há links convenientes para a documentação do `...`
1. Na caixa do fornecedor de armazenamento na nuvem de sua preferência, selecione o botão **[!UICONTROL Configurar]**
   ![Selecionar configurar](assets/ingestion-offline-selectFTP.png)
1. **[!UICONTROL Autenticação]** é a primeira etapa. Digite o nome da sua conta, por exemplo `Luma's FTP Account` e seus detalhes de autenticação. Essa etapa deve ser bastante semelhante para todas as fontes de armazenamento na nuvem, embora os campos possam variar um pouco. Depois de inserir os detalhes de autenticação de uma conta, você pode reutilizá-los para outras conexões de origem que podem estar enviando dados diferentes em agendamentos diferentes de outros arquivos na mesma conta
1. Selecione o **[!UICONTROL botão Conectar à origem]**
1. Quando a Platform tiver se conectado com êxito à Source, selecione o botão **[!UICONTROL Avançar]**
   ![Autenticar na origem](assets/ingestion-offline-authentication.png)

1. Na etapa **[!UICONTROL Selecionar dados]**, a interface usará suas credenciais para abrir a pasta na solução de armazenamento na nuvem
1. Selecione os arquivos que você deseja assimilar, por exemplo `luma-offline-purchases.json`
1. Como o **[!UICONTROL Formato de dados]**, selecione `XDM JSON`
1. Em seguida, é possível visualizar a estrutura json e os dados de amostra no arquivo
1. Selecione o botão **[!UICONTROL Avançar]**
   ![Selecione seu(s) arquivo(s) de dados](assets/ingestion-offline-selectData.png)

1. Na etapa **[!UICONTROL Mapeamento]**, selecione o `Luma Offline Purchase Events Dataset` e o botão **[!UICONTROL Avançar]**. Observe na mensagem que, como os dados que estamos assimilando são um arquivo JSON, não há etapa de mapeamento em que mapeamos o campo de origem para o campo de destino. Os dados JSON já devem estar no XDM. Se você estivesse assimilando um CSV, veria a interface do usuário de mapeamento completa nesta etapa:
   ![Selecione seu conjunto de dados](assets/ingestion-offline-mapping.png)
1. Na etapa **[!UICONTROL Agendando]**, escolha a frequência com que deseja assimilar dados da Source. Reserve um momento para ver as opções. Vamos fazer uma assimilação única, portanto, deixe a **[!UICONTROL Frequência]** em **[!UICONTROL Uma vez]** e selecione o botão **[!UICONTROL Próximo]**:
   ![Agendar seu fluxo de dados](assets/ingestion-offline-scheduling.png)
1. Na etapa **[!UICONTROL detalhes do fluxo de dados]**, você pode escolher um nome para o fluxo de dados, inserir uma descrição opcional, ativar o diagnóstico de erros e assimilação parcial. Deixe as configurações como estão e selecione o botão **[!UICONTROL Avançar]**:
   ![Editar detalhes do seu fluxo de dados](assets/ingestion-offline-detail.png)
1. Na etapa **[!UICONTROL Revisão]**, você pode revisar todas as suas configurações em conjunto e editá-las ou selecionar o botão **[!UICONTROL Concluir]**
1. Depois de salvar, você será direcionado para uma tela como esta:
   ![Concluído](assets/ingestion-offline-complete.png)

### Validar os dados

Quando o lote tiver sido carregado, verifique o upload visualizando o conjunto de dados.

Você deve ver as três ocorrências do seu webhook.

Pesquise o perfil com valor `5625458` no namespace `loyaltyId` novamente para ver se há eventos de compra em seu perfil. Você deve ver uma compra. Para se aprofundar nos detalhes da compra, selecione **[!UICONTROL Exibir JSON]**:

![Evento de compra no perfil](assets/ingestion-offline-eventInProfile.png)

## Ferramentas de ETL

A Adobe tem parcerias com vários fornecedores de ETL para oferecer suporte à assimilação de dados na Experience Platform. Devido à variedade de fornecedores de terceiros, o ETL não é abordado neste tutorial, embora você seja bem-vindo para analisar alguns destes recursos:

* [Desenvolvendo integrações ETL para o Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/etl/home.html?lang=pt-BR)
* [[!DNL Snaplogic] Adobe Experience Platform Snap Pack](https://www.snaplogic.com/resources/videos/august-2020-aep)

## Recursos adicionais

* [Documentação de assimilação em lote](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=pt-BR)
* [Referência da API de assimilação em lote](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)

Agora vamos [transmitir dados usando o Web SDK](ingest-streaming-data.md)
