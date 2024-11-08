---
title: Foundation - Assimilação de dados - Assimilação de dados de fontes offline
description: Foundation - Assimilação de dados - Assimilação de dados de fontes offline
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 2%

---

# 1.2.5 Zona de aterrissagem de dados

Neste exercício, o objetivo é configurar seu conector de Source da Data Landing Zone com o armazenamento de blobs do Azure.

A Zona de aterrissagem de dados é uma interface de armazenamento de blobs do Azure fornecida pela Adobe Experience Platform, que concede acesso a um recurso de armazenamento de arquivos seguro e baseado em nuvem para trazer arquivos para a plataforma. A Zona de aterrissagem de dados é compatível com a autenticação baseada em SAS e seus dados são protegidos com mecanismos de segurança de armazenamento de blobs do Azure padrão em repouso e em trânsito. A autenticação baseada em SAS permite acessar com segurança o contêiner da Data Landing Zone por meio de uma conexão pública com a Internet.

>[!NOTE]
>
> O Adobe Experience Platform **impõe um TTL (time-to-live)** rigoroso de sete dias em todos os arquivos carregados em um contêiner de Zona de Aterrissagem de Dados. Todos os arquivos são excluídos após sete dias.


## 1.2.5.1 Pré-requisitos

Para copiar blobs ou arquivos para a sua Zona de aterrissagem de dados da Adobe Experience Platform, você usará o AzCopy, um utilitário de linha de comando. Você pode baixar uma versão para o seu sistema operacional via [https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

![dlz-install-az-copy.png](./images/dlz-install-az-copy.png)

- Descompacte o arquivo baixado

![dlz-install-az-copy.png](./images/dlz1.png)

- Baixe o arquivo de dados de amostra global-context-websiteinteractions.csv, que contém interações de site de exemplo e salve-o na pasta em que você descompactou o **azcopy**.

![dlz-install-az-copy.png](./images/dlz2.png)

- Abra uma janela de terminal e navegue até a pasta na área de trabalho. Você deve ver o seguinte conteúdo (azcopy e global-context-websiteinteractions.csv), por exemplo, no OSX:

![dlz-unzip-azcopy.png](./images/dlz-unzip-azcopy.png)

## 1.2.5.2 Conectar a zona de aterrissagem de dados à Adobe Experience Platform

Faça logon no Adobe Experience Platform acessando esta URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--module2sandbox--``. Você pode fazer isso clicando no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. Depois de selecionar a sandbox apropriada, você verá a alteração da tela e agora estará em sua sandbox dedicada.

![Assimilação de dados](./images/sb1.png)

No menu esquerdo, vá para **Fontes**. No catálogo Fontes, pesquise por **aterrissagem de dados**. No cartão **Data Landing Zone**, clique em **...** e selecione **Exibir Credenciais**.

![dlz-view-credentials.png](./images/dlz-view-credentials.png)

Clique na cópia de entrada **SASUri**.

![dlz-copy-sas-uri.png](./images/dlz-copy-sas-uri.png)

## 1.2.5.3 Copie o arquivo csv na zona de aterrissagem de dados da AEP

Agora você assimilará dados na Adobe Experience Platform usando as ferramentas de linha de comando do Azure com o AZCopy.

Abra um terminal no local de instalação do Azcopy e execute o seguinte comando para copiar um arquivo para a zona de aterrissagem de dados da AEP:

``./azcopy copy <your-local-file> <your SASUri>``

Certifique-se de cercar seu SASUri com aspas duplas. Substitua `<your-local-file>` pelo caminho da sua cópia local do arquivo **global-context-websiteinteractions.csv** no diretório azcopy e substitua `<your SASUri>` pelo valor **SASUri** copiado da interface do usuário do Adobe Experience Platform. O comando deve ter esta aparência:

```command
./azcopy copy global-context-websiteinteractions.csv "https://sndbxdtlnd2bimpjpzo14hp6.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-xxxxxxx-9843-4973-ae52-xxxxxxxx&sr=c&sp=racwdlm&sig=DN3kdhKzard%2BQwKASKg67Zxxxxxxxxxxxxxxxx"
```

Depois de executar o comando acima em seu terminal, você verá o seguinte:

![dlz-exec-copy-command.png](./images/dlz-exec-copy-command.png)

## 1.2.5.4 Pesquisar o arquivo na Data Landing Zone

Vá para a Data Landing Zone no Adobe Experience Platform.

Selecione **Fontes**, procure **aterrissagem de dados** e clique no botão **Instalação**.

![dlz-inspect-datalanding-zone.png](./images/dlz-inspect-datalanding-zone.png)

Isso abrirá a Data Landing Zone. Você verá o arquivo que acabou de carregar no painel **Selecionar dados** da zona de aterrissagem de dados.

![dlz-datalanding-zone-open.png](./images/dlz-datalanding-zone-open.png)

## 1.2.5.5 Processar o arquivo

Selecione o arquivo e selecione **Delimitado** como formato de dados. Você verá uma pré-visualização dos dados. Clique em **Next**.

![dlz-datalanding-select-file.png](./images/dlz-datalanding-select-file.png)

Agora é possível começar a mapear os dados carregados para corresponder ao esquema XDM do seu conjunto de dados.

Selecione **Conjunto de dados existente** e selecione o conjunto de dados **Sistema de demonstração - Conjunto de dados de eventos para o site (Global v1.1)**. Clique em **Next**.

![dlz-target-dataset.png](./images/dlz-target-dataset.png)

Agora você está pronto para mapear os dados de origem recebidos do arquivo csv para os campos de destino do esquema XDM do conjunto de dados.

![dlz-start-mapping.png](./images/dlz-start-mapping.png)

>[!NOTE]
>
> Não se importa com os possíveis erros do mapeamento. Você corrigirá o mapeamento na próxima etapa.

## 1.2.5.6 Mapear campos

Primeiro, clique no botão **Limpar todos os mapeamentos**. Em seguida, você pode começar com um mapeamento limpo.

![dlz-clear-mappings.png](./images/mappings1.png)

Em seguida, clique em **Novo tipo de campo** e selecione **Adicionar novo campo**.

![dlz-clear-mappings.png](./images/dlz-clear-mappings.png)

Para mapear o campo de origem **ecid**, selecione o campo **identities.ecid** e clique em **Selecionar**.

![dlz-map-identity.png](./images/dlz-map-identity.png)

Em seguida, clique em **Mapear campo de destino**.

![dlz-map-select-target-field.png](./images/dlz-map-select-target-field.png)

Selecione o campo ``--aepTenantId--``.identification.core.ecid na estrutura do esquema.

![dlz-map-target-field.png](./images/dlz-map-target-field.png)

Você precisa mapear alguns outros campos, clique em **+ Novo tipo de campo** seguido de **Adicionar novo campo** e adicionar campos para este mapeamento

| origem | público-alvo |
|---|---|
| resource.info.pagename | web.webPageDetails.name |
| carimbo de data e hora | carimbo de data e hora |
| carimbo de data e hora | _id |

![dlz-add-other-mapping.png](./images/dlz-add-other-mapping.png)

Quando terminar, sua tela deverá ficar parecida com a tela abaixo. Clique em **Next**.

![dlz-mapping-result.png](./images/dlz-mapping-result.png)

Clique em **Next**.

![dlz-default-scheduling.png](./images/dlz-default-scheduling.png)

Clique em **Concluir**.

![dlz-import-finish.png](./images/dlz-import-finish.png)

## 1.2.5.7 Monitorar fluxo de dados

Para monitorar seu fluxo de dados, vá para **Fontes**, **Fluxos de Dados** e clique em seu fluxo de dados:

![dlz-monitor-dataflow.png](./images/dlz-monitor-dataflow.png)

O carregamento dos dados pode levar alguns minutos. Quando for bem-sucedido, você verá um status de **Sucesso**:

![dlz-monitor-dataflow-result.png](./images/dlz-monitor-dataflow-result.png)

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao módulo 1.2](./data-ingestion.md)

[Voltar a todos os módulos](../../../overview.md)
