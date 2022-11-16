---
title: Foundation - Assimilação de dados - Assimilação de dados de fontes offline
description: Foundation - Assimilação de dados - Assimilação de dados de fontes offline
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 93d9f4ef-9cbd-4310-879e-d69106b70404
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 2%

---

# 2.5 Zona de aterrissagem de dados

Neste exercício, o objetivo é configurar seu conector da Fonte da Zona de Aterrissagem de Dados com o armazenamento do Azure Blob.

A Data Landing Zone é uma interface de armazenamento do Azure Blob provisionada pela Adobe Experience Platform, permitindo acessar um recurso de armazenamento de arquivos seguro e baseado em nuvem para trazer arquivos para a Platform. A Zona de Aterrissagem de Dados oferece suporte à autenticação baseada em SAS e seus dados são protegidos com mecanismos de segurança de armazenamento padrão do Azure Blob em repouso e em trânsito. A autenticação baseada em SAS permite que você acesse com segurança seu contêiner da Zona de aterrissagem de dados por meio de uma conexão pública com a Internet.

>[!NOTE]
>
> Adobe Experience Platform **aplica um TTL (time-to-live, tempo de vida útil) estrito de sete dias** em todos os arquivos carregados em um contêiner de Zona de aterrissagem de dados. Todos os arquivos são excluídos após sete dias.


## Pré-requisitos 2.5.1

Para copiar blobs ou arquivos para sua zona de aterrissagem de dados do Adobe Experience Platform, você usará o AzCopy, um utilitário de linha de comando. Você pode baixar uma versão para seu sistema operacional via [https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

![dlz-install-az-copy.png](./images/dlz-install-az-copy.png)

- Descompacte o arquivo de download

![dlz-install-az-copy.png](./images/dlz1.png)

- Baixe o arquivo de dados de amostra [global-context-websiteinteractions.csv](../../assets/csv/data-ingestion/global-context-websiteinteractions.csv), que contém amostras de interações do site e as salva na pasta em que você descompactou **azcopia**.

![dlz-install-az-copy.png](./images/dlz2.png)

- Abra uma janela de terminal e navegue até a pasta na área de trabalho. Você deverá ver o seguinte conteúdo (azcopy e global-context-websiteinteractions.csv), por exemplo, no OSX:

![dlz-unzip-azcopy.png](./images/dlz-unzip-azcopy.png)

## 2.5.2 Conectar a zona de aterrissagem de dados ao Adobe Experience Platform

Faça logon no Adobe Experience Platform acessando este URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer logon, você será direcionado para a página inicial do Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, é necessário selecionar um **sandbox**. A sandbox a ser selecionada é chamada de ``--module2sandbox--``. Você pode fazer isso clicando no texto **[!UICONTROL Produto de produção]** na linha azul na parte superior da tela. Depois de selecionar a sandbox apropriada, você verá a tela mudar e agora estará na sandbox dedicada.

![Assimilação de dados](./images/sb1.png)

No menu esquerdo, acesse **Fontes**. No catálogo Fontes, procure por **aterrissagem de dados**. No **Zona de aterrissagem de dados** cartão, clique em **...** e selecione **Exibir credenciais**.

![dlz-view-credentials.png](./images/dlz-view-credentials.png)

Clique na cópia para cima **SASUri**.

![dlz-copy-sas-uri.png](./images/dlz-copy-sas-uri.png)

## 2.5.3 Copie o arquivo csv para a zona de aterrissagem de dados da AEP

Agora você assimilará dados no Adobe Experience Platform usando as ferramentas de linha de comando do Azure usando o AZCopy.

Abra um terminal no local de instalação do azcopy e execute o seguinte comando para copiar um arquivo para a zona de aterrissagem de dados do AEP:

``./azcopy copy <your-local-file> <your SASUri>``

Certifique-se de rodar o SASUri com aspas duplas. Substituir `<your-local-file>` pelo caminho para a cópia local do arquivo **global-context-websiteinteractions.csv** no diretório azcopy e substitua `<your SASUri>` pela **SASUri** valor que você copiou da interface do usuário do Adobe Experience Platform. Seu comando deve ser semelhante a:

```command
./azcopy copy global-context-websiteinteractions.csv "https://sndbxdtlnd2bimpjpzo14hp6.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-xxxxxxx-9843-4973-ae52-xxxxxxxx&sr=c&sp=racwdlm&sig=DN3kdhKzard%2BQwKASKg67Zxxxxxxxxxxxxxxxx"
```

Depois de executar o comando acima em seu terminal, você verá o seguinte:

![dlz-exec-copy-command.png](./images/dlz-exec-copy-command.png)

## 2.5.4 Pesquisar seu arquivo na sua Zona de aterrissagem de dados

Vá para a sua Zona de aterrissagem de dados no Adobe Experience Platform.

Selecionar **Fontes**, pesquisar por **aterrissagem de dados** e clique no botão **Configuração** botão.

![dlz-inspecit-datalanding-zone.png](./images/dlz-inspect-datalanding-zone.png)

Isso abrirá a Zona de aterrissagem de dados. Você verá o arquivo que acabou de carregar no da zona de aterrissagem de dados **selecionar dados** painel.

![dlz-datalanding-zone-open.png](./images/dlz-datalanding-zone-open.png)

## 2.5.5 Processar o arquivo

Selecione o arquivo e selecione **Delimitado** como formato de dados. Em seguida, você visualizará seus dados. Clique em **Próximo**.

![dlz-datalanding-select-file.png](./images/dlz-datalanding-select-file.png)

Agora é possível começar a mapear os dados carregados para corresponder ao esquema XDM do conjunto de dados.

Selecionar **Conjunto de dados existente** e selecione o conjunto de dados **Sistema de demonstração - Conjunto de dados do evento para site (Global v1.1)**. Clique em **Próximo**.

![dlz-target-dataset.png](./images/dlz-target-dataset.png)

Agora você está pronto para mapear os dados de origem recebidos do arquivo csv para os campos de destino do esquema XDM do conjunto de dados.

![dlz-start-mapping.png](./images/dlz-start-mapping.png)

>[!NOTE]
>
> Não se preocupe com os possíveis erros no mapeamento. Você corrigirá o mapeamento na próxima etapa.

## 2.5.6 Campos de mapa

Em primeiro lugar, clique no botão **Limpar todos os mapeamentos** botão. Você pode começar com um mapeamento limpo.

![dlz-clear-mappings.png](./images/mappings1.png)

Em seguida, clique em **Novo tipo de campo** e depois selecione **Adicionar novo campo**.

![dlz-clear-mappings.png](./images/dlz-clear-mappings.png)

Para mapear a variável **ecid** campo de origem, selecione o campo **identities.ecid** e clique em **Selecionar**.

![dlz-map-identity.png](./images/dlz-map-identity.png)

Em seguida, clique em **Mapear campo de destino**.

![dlz-map-select-target-field.png](./images/dlz-map-select-target-field.png)

Selecione o campo ``--aepTenantId--``.identification.core.ecid na estrutura do schema.

![dlz-map-target-field.png](./images/dlz-map-target-field.png)

Você precisa mapear alguns outros campos, clique em **+ Novo tipo de campo** seguida de **Adicionar novo campo** e adicionar campos para este mapeamento

| source | target |
|---|---|
| resource.info.pagename | web.webPageDetails.name |
| carimbo de data e hora | carimbo de data e hora |
| carimbo de data e hora | _id |

![dlz-add-other-mapping.png](./images/dlz-add-other-mapping.png)

Quando terminar, a tela ficará parecida com a tela abaixo. Clique em **Próximo**.

![dlz-mapping-result.png](./images/dlz-mapping-result.png)

Clique em **Próximo**.

![dlz-default-scheduling.png](./images/dlz-default-scheduling.png)

Clique em **Concluir**.

![dlz-import-end.png](./images/dlz-import-finish.png)

## 2.5.7 Monitorar fluxo de dados

Para monitorar o fluxo de dados, acesse **Fontes**, **Fluxos de dados** e clique no seu fluxo de dados:

![dlz-monitor-dataflow.png](./images/dlz-monitor-dataflow.png)

O carregamento dos dados pode demorar alguns minutos, quando for bem-sucedido, você verá um status de **Sucesso**:

![dlz-monitor-dataflow-result.png](./images/dlz-monitor-dataflow-result.png)

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao Módulo 2](./data-ingestion.md)

[Voltar para todos os módulos](../../overview.md)
