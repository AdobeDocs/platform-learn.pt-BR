---
title: Foundation - Assimilação de dados - Assimilação de dados de fontes offline
description: Foundation - Assimilação de dados - Assimilação de dados de fontes offline
kt: 5342
doc-type: tutorial
exl-id: 21b84a77-4115-4ba7-b847-b236aa14bbdd
source-git-commit: 8bdcd03bd38a6da98b82439ad86482cad5f4e684
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 2%

---

# 1.2.5 Zona de aterrissagem de dados

Neste exercício, o objetivo é configurar seu conector de Source da Data Landing Zone com o armazenamento de blobs do Azure.

A Zona de aterrissagem de dados é uma interface de armazenamento de blobs do Azure fornecida pela Adobe Experience Platform, que concede acesso a um recurso de armazenamento de arquivos seguro e baseado em nuvem para trazer arquivos para a plataforma. A Zona de aterrissagem de dados é compatível com a autenticação baseada em SAS e seus dados são protegidos com mecanismos de segurança de armazenamento de blobs do Azure padrão em repouso e em trânsito. A autenticação baseada em SAS permite acessar com segurança o contêiner da Data Landing Zone por meio de uma conexão pública com a Internet.

>[!NOTE]
>
> O Adobe Experience Platform **impõe um TTL (time-to-live)** rigoroso de sete dias em todos os arquivos carregados em um contêiner de Zona de Aterrissagem de Dados. Todos os arquivos são excluídos após sete dias.


## Pré-requisitos

Para copiar blobs ou arquivos para a sua Zona de aterrissagem de dados da Adobe Experience Platform, você usará o AzCopy, um utilitário de linha de comando. Você pode baixar uma versão para seu sistema operacional via [https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10), rolar para baixo nessa página para **Baixar o binário portátil do AzCopy** e selecionar a versão apropriada para seu sistema operacional.

![dlz-install-az-copy.png](./images/dlzinstallazcopy.png)

- Descompacte o arquivo baixado

![dlz-install-az-copy.png](./images/dlz1.png)

- Baixe o arquivo de dados de amostra global-context-websiteinteractions.csv, que contém interações de site de exemplo e salve-o na pasta em que você descompactou o **azcopy**.

![dlz-install-az-copy.png](./images/dlz2.png)

- Abra uma janela de terminal e navegue até a pasta na área de trabalho. Você deve ver o seguinte conteúdo (azcopy e global-context-websiteinteractions.csv), por exemplo, no OSX:

![dlz-unzip-azcopy.png](./images/dlzunzipazcopy.png)

## 1.2.5.2 Conectar a zona de aterrissagem de dados à Adobe Experience Platform

Faça logon no Adobe Experience Platform acessando esta URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepSandboxName--``.  Depois de selecionar a sandbox apropriada, você verá a alteração da tela e agora estará em sua sandbox dedicada.

![Assimilação de dados](./images/sb1.png)

No menu esquerdo, vá para **Fontes**. No catálogo Fontes, pesquise por **aterrissagem de dados**.

![Assimilação de dados](./images/sourcesdlz.png)

Clique no cartão **Data Landing Zone** e você verá as credenciais na guia direita.

![dlz-view-credentials.png](./images/dlzviewcredentials.png)

Clique no ícone conforme indicado para copiar o **SASUri**.

![dlz-copy-sas-uri.png](./images/dlzcopysasuri.png)

## Copie o arquivo csv para a zona de aterrissagem de dados da AEP

Agora você assimilará dados na Adobe Experience Platform usando as ferramentas de linha de comando do Azure com o AZCopy.

Abra um terminal no local de instalação do Azcopy e execute o seguinte comando para copiar um arquivo para a zona de aterrissagem de dados da AEP:

``./azcopy copy <your-local-file> <your SASUri>``

Certifique-se de cercar seu SASUri com aspas duplas. Substitua `<your-local-file>` pelo caminho da sua cópia local do arquivo **global-context-websiteinteractions.csv** no diretório azcopy e substitua `<your SASUri>` pelo valor **SASUri** copiado da interface do usuário do Adobe Experience Platform. O comando deve ter esta aparência:

```command
./azcopy copy global-context-websiteinteractions.csv "https://sndbxdtlnd2bimpjpzo14hp6.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-xxxxxxx-9843-4973-ae52-xxxxxxxx&sr=c&sp=racwdlm&sig=DN3kdhKzard%2BQwKASKg67Zxxxxxxxxxxxxxxxx"
```

Depois de executar o comando acima em seu terminal, você verá o seguinte:

![dlz-exec-copy-command.png](./images/dlzexeccopycommand.png)

## Pesquisar o arquivo na Data Landing Zone

Vá para a Data Landing Zone no Adobe Experience Platform.

Selecione **Fontes**, procure **aterrissagem de dados** e clique no botão **Instalação**.

![dlz-inspect-datalanding-zone.png](./images/dlzinspectdatalandingzone.png)

Isso abrirá a Data Landing Zone. Você verá o arquivo que acabou de carregar no painel **Selecionar dados** da zona de aterrissagem de dados.

![dlz-datalanding-zone-open.png](./images/dlzdatalandingzoneopen.png)

## Processar o arquivo

Selecione o arquivo e selecione **Delimitado** como formato de dados. Você verá uma pré-visualização dos dados. Clique em **Next**.

![dlz-datalanding-select-file.png](./images/dlzdatalandingselectfile.png)

Agora é possível começar a mapear os dados carregados para corresponder ao esquema XDM do seu conjunto de dados.

Selecione **Conjunto de dados existente** e selecione o conjunto de dados **Sistema de demonstração - Conjunto de dados de eventos para o site (Global v1.1)**. Clique em **Next**.

![dlz-target-dataset.png](./images/dlztargetdataset.png)

Agora você está pronto para mapear os dados de origem recebidos do arquivo csv para os campos de destino do esquema XDM do conjunto de dados.

![dlz-start-mapping.png](./images/dlzstartmapping.png)

>[!NOTE]
>
> Não se importa com os possíveis erros do mapeamento. Você corrigirá o mapeamento na próxima etapa.

## Mapear campos

Primeiro, clique no botão **Limpar todos os mapeamentos**. Em seguida, você pode começar com um mapeamento limpo.

![dlz-clear-mappings.png](./images/mappings1.png)

Em seguida, clique em **Novo tipo de campo** e selecione **Adicionar novo campo**.

![dlz-clear-mappings.png](./images/dlzclearmappings.png)

Para mapear o campo de origem **ecid**, selecione o campo **identities.ecid** e clique em **Selecionar**.

![dlz-map-identity.png](./images/dlzmapidentity.png)

Em seguida, clique em **Mapear campo de destino**.

![dlz-map-select-target-field.png](./images/dlzmapselecttargetfield.png)

Selecione o campo ``--aepTenantId--``.identification.core.ecid na estrutura do esquema.

![dlz-map-target-field.png](./images/dlzmaptargetfield.png)

Você precisa mapear alguns outros campos, clique em **+ Novo tipo de campo** seguido de **Adicionar novo campo** e adicionar campos para este mapeamento

| origem | público-alvo |
|---|---|
| resource.info.pagename | web.webPageDetails.name |
| carimbo de data e hora | carimbo de data e hora |
| carimbo de data e hora | _id |

![dlz-add-other-mapping.png](./images/dlzaddothermapping.png)

Quando terminar, sua tela deverá ficar parecida com a tela abaixo. Clique em **Next**.

![dlz-mapping-result.png](./images/dlzmappingresult.png)

Clique em **Next**.

![dlz-default-scheduling.png](./images/dlzdefaultscheduling.png)

Clique em **Concluir**.

![dlz-import-finish.png](./images/dlzimportfinish.png)

## Monitorar fluxo de dados

Para monitorar seu fluxo de dados, vá para **Fontes**, **Fluxos de Dados** e clique em seu fluxo de dados:

![dlz-monitor-dataflow.png](./images/dlzmonitordataflow.png)

O carregamento dos dados pode levar alguns minutos. Quando for bem-sucedido, você verá um status de **Sucesso**:

![dlz-monitor-dataflow-result.png](./images/dlzmonitordataflowresult.png)

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao módulo 1.2](./data-ingestion.md)

[Voltar a todos os módulos](../../../overview.md)
