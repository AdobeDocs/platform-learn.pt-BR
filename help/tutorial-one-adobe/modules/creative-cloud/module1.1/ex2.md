---
title: Otimizar seu processo do Firefly usando o Microsoft Azure e URLs pré-assinadas
description: Saiba como otimizar seu processo do Firefly usando o Microsoft Azure e URLs pré-assinadas
role: Developer
level: Beginner
jira: KT-5342
doc-type: tutorial
exl-id: 5f9803a4-135c-4470-bfbb-a298ab1fee33
source-git-commit: c29fb7908ee9a16a265f96d8181dca93fd9256cc
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 1%

---

# 1.1.2 Otimizar o processo do Firefly usando o Microsoft Azure e URLs pré-assinados

Saiba como otimizar seu processo do Firefly usando o Microsoft Azure e URLs pré-assinadas.

## 1.1.2.1 Criar uma assinatura do Azure

>[!NOTE]
>
>Se você já tiver uma Assinatura do Azure existente, ignore esta etapa. Nesse caso, prossiga com o próximo exercício.

1. Acesse [https://portal.azure.com](https://portal.azure.com){target="_blank"} e faça logon com sua conta do Azure. Se você não tiver um, use seu endereço de email pessoal para criar sua conta do Azure.

   ![Armazenamento do Azure](./images/02azureportalemail.png){zoomable="yes"}

   Depois de fazer logon, você verá a seguinte tela:

   ![Armazenamento do Azure](./images/03azureloggedin.png){zoomable="yes"}

1. No menu esquerdo, selecione **Todos os Recursos**. A tela de assinatura do Azure será exibida se você ainda não tiver assinado.

1. Se você não tiver assinado, selecione **Iniciar com uma avaliação gratuita do Azure**.

   ![Armazenamento do Azure](./images/04azurestartsubscribe.png){zoomable="yes"}

1. Preencha o formulário de assinatura do Azure e forneça seu celular e cartão de crédito para ativação (você terá uma camada gratuita por 30 dias e não será cobrado, a menos que atualize).

   Quando o processo de assinatura for concluído, você estará pronto para prosseguir.

   ![Armazenamento do Azure](./images/06azuresubscriptionok.png){zoomable="yes"}

## 1.1.2.2 Criar Conta de Armazenamento do Azure

1. Procure por `storage account` e selecione **Contas de armazenamento**.

   ![Armazenamento do Azure](./images/azs1.png){zoomable="yes"}

1. Selecione **+ Criar**.

   ![Armazenamento do Azure](./images/azs2.png){zoomable="yes"}

1. Selecione sua **Assinatura** e selecione (ou crie) um **Grupo de recursos**.

1. Em **Nome da conta de armazenamento**, use `--aepUserLdap--`.

1. Selecione **Revisar + criar**.

   ![Armazenamento do Azure](./images/azs3.png){zoomable="yes"}

1. Selecione **Criar**.

   ![Armazenamento do Azure](./images/azs4.png){zoomable="yes"}

1. Após a confirmação, selecione **Ir para o recurso**.

   ![Armazenamento do Azure](./images/azs5.png){zoomable="yes"}

   Sua Conta de Armazenamento do Azure está pronta para ser usada.

   ![Armazenamento do Azure](./images/azs6.png){zoomable="yes"}

1. Selecione **Armazenamento de dados** e vá para **Contêineres**. Selecione **+ Contêiner**.

   ![Armazenamento do Azure](./images/azs7.png){zoomable="yes"}

1. Use `--aepUserLdap--` para o nome e selecione **Criar**.

   ![Armazenamento do Azure](./images/azs8.png){zoomable="yes"}

   Seu contêiner agora está pronto para ser usado.

   ![Armazenamento do Azure](./images/azs9.png){zoomable="yes"}

## 1.1.2.3 Instalar o Azure Storage Explorer

1. [Baixe o Microsoft Azure Storage Explorer para gerenciar seus arquivos](https://azure.microsoft.com/en-us/products/storage/storage-explorer#Download-4){target="_blank"}. Selecione a versão correta para seu sistema operacional específico, baixe-a e instale-a.

   ![Armazenamento do Azure](./images/az10.png){zoomable="yes"}

1. Abra o aplicativo e selecione **Fazer logon com o Azure**.

   ![Armazenamento do Azure](./images/az11.png){zoomable="yes"}

1. Selecione **Assinatura**.

   ![Armazenamento do Azure](./images/az12.png){zoomable="yes"}

1. Selecione **Azure** e depois **Próximo**.

   ![Armazenamento do Azure](./images/az13.png){zoomable="yes"}

1. Selecione sua conta do Microsoft Azure e conclua o processo de autenticação.

   ![Armazenamento do Azure](./images/az14.png){zoomable="yes"}

   Após a autenticação, essa mensagem é exibida.

   ![Armazenamento do Azure](./images/az15.png){zoomable="yes"}

1. De volta ao aplicativo Microsoft Azure Storage Explorer, selecione sua assinatura e escolha **Abrir o Explorer**.

   >[!NOTE]
   >
   >Se a sua conta não for exibida, clique no ícone de **engrenagem** ao lado do seu endereço de email e selecione **Desfiltrar**.

   ![Armazenamento do Azure](./images/az16.png){zoomable="yes"}

   Sua conta de armazenamento aparece em **Contas de Armazenamento**.

   ![Armazenamento do Azure](./images/az17.png){zoomable="yes"}

1. Abra **Contêineres de blob** e selecione o contêiner criado no exercício anterior.

   ![Armazenamento do Azure](./images/az18.png){zoomable="yes"}

## 1.1.2.4 Upload manual de arquivo e uso de um arquivo de imagem como referência de estilo

1. Carregue um arquivo de imagem de sua escolha ou [este arquivo](./images/gradient.jpg){target="_blank"} no container.

   ![Armazenamento do Azure](./images/gradient.jpg)

   Depois de carregado, você pode vê-lo no container:

   ![Armazenamento do Azure](./images/az19.png){zoomable="yes"}

1. Clique com o botão direito do mouse em `gradient.jpg` e selecione **Obter Assinatura de Acesso Compartilhado**.

   ![Armazenamento do Azure](./images/az20.png){zoomable="yes"}

1. Em **Permissões**, somente **Leitura** é necessário. Selecione **Criar**.

   ![Armazenamento do Azure](./images/az21.png){zoomable="yes"}

1. Copie o URL pré-assinado para este arquivo de imagem para a próxima solicitação de API para o Firefly.

   ![Armazenamento do Azure](./images/az22.png){zoomable="yes"}

1. De volta ao Postman, abra a solicitação **POST - Firefly - T2I (styleref) V3**.
Isto aparece no **Corpo**.

   ![Armazenamento do Azure](./images/az23.png){zoomable="yes"}

1. Substitua a URL de espaço reservado pela URL pré-assinada para o arquivo de imagem e selecione **Enviar**.

   ![Armazenamento do Azure](./images/az24.png){zoomable="yes"}

1. Abra a nova imagem de resposta dos Serviços da Firefly no navegador.

   ![Armazenamento do Azure](./images/az25.png){zoomable="yes"}

   Outra imagem aparece com `horses in a field`, mas dessa vez o estilo é semelhante ao arquivo de imagem fornecido como referência de estilo.

   ![Armazenamento do Azure](./images/az26.png){zoomable="yes"}

## 1.1.2.5 Upload de arquivo programático

Para usar o carregamento de arquivo programático com as Contas de Armazenamento do Azure, é necessário criar um novo token **SAS (Assinatura de Acesso Compartilhado)** com permissões que permitam gravar um arquivo.

1. No Azure Storage Explorer, clique com o botão direito do mouse em seu contêiner e selecione **Obter Assinatura de Acesso Compartilhado**.

   ![Armazenamento do Azure](./images/az27.png){zoomable="yes"}

1. Em **Permissões**, selecione as seguintes permissões necessárias:

   - **Leitura**
   - **Adicionar**
   - **Create**
   - **Write**
   - **Lista**

1. Selecione **Criar**.

   ![Armazenamento do Azure](./images/az28.png){zoomable="yes"}

1. Depois de receber seu **token SAS**, selecione **Copiar**.

   ![Armazenamento do Azure](./images/az29.png){zoomable="yes"}

   Use o **token SAS** para carregar um arquivo na sua Conta de Armazenamento do Azure.

1. De volta ao Postman, selecione a pasta **FF - Firefly Services Tech Insiders**, em seguida, selecione **...** na pasta **Firefly** e selecione **Adicionar solicitação**.

   ![Armazenamento do Azure](./images/az30.png){zoomable="yes"}

1. Altere o nome da solicitação vazia para **Fazer upload do arquivo para a Conta de Armazenamento do Azure**, altere o **Tipo de Solicitação** para **PUT** e cole a URL do token SAS na seção de URL e selecione **Corpo**.

   ![Armazenamento do Azure](./images/az31.png){zoomable="yes"}

1. Em seguida, selecione um arquivo de seu computador local ou use outro arquivo de imagem localizado [aqui](./images/gradient2-p.jpg){target="_blank"}.

   ![Arquivo de gradação](./images/gradient2-p.jpg)

1. Em **Corpo**, selecione **binário** e **Selecione arquivo** e **+ Novo arquivo da máquina local**.

   ![Armazenamento do Azure](./images/az32.png){zoomable="yes"}

1. Selecione o arquivo de sua escolha e selecione **Abrir**.

   ![Armazenamento do Azure](./images/az33.png){zoomable="yes"}

1. Em seguida, especifique o nome de arquivo a ser usado em sua Conta de Armazenamento do Azure, colocando o cursor na frente do ponto de interrogação **?** no URL desta forma:

   ![Armazenamento do Azure](./images/az34.png){zoomable="yes"}

   A URL atualmente tem esta aparência, mas precisa ser alterada.

   `https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03...`

1. Altere o nome do arquivo para `gradient2-p.jpg` e altere a URL para incluir o nome do arquivo desta forma:

   `https://vangeluw.blob.core.windows.net/vangeluw/gradient2-p.jpg?sv=2023-01-03...`

   ![Armazenamento do Azure](./images/az34a.png){zoomable="yes"}

1. Em seguida, vá para **Cabeçalhos** para adicionar um novo cabeçalho manualmente da seguinte maneira:

   | Chave | Valor |
   |:-------------:| :---------------:| 
   | `x-ms-blob-type` | `BlockBlob` |


   ![Armazenamento do Azure](./images/az35.png){zoomable="yes"}

1. Vá para **Autorização** e defina o **Tipo de Autenticação** como **Sem Autenticação** e selecione **Enviar**.

   ![Armazenamento do Azure](./images/az36.png){zoomable="yes"}

1. Em seguida, essa resposta vazia é exibida no Postman, o que significa que o upload do arquivo está correto.

   ![Armazenamento do Azure](./images/az37.png){zoomable="yes"}

1. De volta ao Azure Storage Explorer, atualize o conteúdo de sua pasta e o arquivo recém-carregado é exibido.

   ![Armazenamento do Azure](./images/az38.png){zoomable="yes"}

## 1.1.2.6 Utilização programática de arquivos

Para ler programaticamente os arquivos das Contas de Armazenamento do Azure a longo prazo, você precisa criar um novo token **SAS (Assinatura de Acesso Compartilhado)**, com permissões que permitam ler um arquivo. Tecnicamente, você pode usar o token SAS criado no exercício anterior, mas é prática recomendada ter um token separado com apenas permissões de **Leitura** e um token separado com apenas permissões de **Gravação**.

### Token SAS de leitura de longo prazo

1. Volte para o Azure Storage Explorer, clique com o botão direito do mouse no seu contêiner e selecione **Obter Assinatura de Acesso Compartilhado**.

   ![Armazenamento do Azure](./images/az27.png){zoomable="yes"}

1. Em **Permissões**, selecione as seguintes permissões necessárias:

   - **Leitura**
   - **Lista**

1. Defina o **Tempo de Expiração** para 1 ano a partir de agora.

1. Selecione **Criar**.

   ![Armazenamento do Azure](./images/az100.png){zoomable="yes"}

1. Copie o URL e anote-o em um arquivo em seu computador para obter seu token SAS de longo prazo com permissões de leitura.

   ![Armazenamento do Azure](./images/az101.png){zoomable="yes"}

   Seu URL deve ter esta aparência:

   `https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

   Você pode derivar alguns valores do URL acima:

   - `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
   - `AZURE_STORAGE_CONTAINER`: `vangeluw`
   - `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

### Token SAS de gravação de longo prazo

1. Volte para o Azure Storage Explorer, clique com o botão direito do mouse no seu contêiner e selecione **Obter Assinatura de Acesso Compartilhado**.

   ![Armazenamento do Azure](./images/az27.png){zoomable="yes"}

1. Em **Permissões**, selecione as seguintes permissões necessárias:

   - **Adicionar**
   - **Create**
   - **Write**

1. Defina o **Tempo de Expiração** para 1 ano a partir de agora.

1. Selecione **Criar**.

   ![Armazenamento do Azure](./images/az102.png){zoomable="yes"}

1. Copie o URL e anote-o em um arquivo em seu computador para obter seu token SAS de longo prazo com permissões de leitura.

   ![Armazenamento do Azure](./images/az103.png){zoomable="yes"}

   Seu URL deve ter esta aparência:

   `https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

   Você pode derivar alguns valores do URL acima:

   - `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
   - `AZURE_STORAGE_CONTAINER`: `vangeluw`
   - `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
   - `AZURE_STORAGE_SAS_WRITE`: `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

### Variáveis no Postman

>[!IMPORTANT]
>
>Se você for um funcionário da Adobe, siga as instruções aqui para usar o [PostBuster](./../../../postbuster.md).

Como você pode ver na seção acima, há algumas variáveis comuns nos tokens Read e Write.

Em seguida, é necessário criar variáveis no Postman que armazenam os vários elementos dos tokens SAS acima. Há alguns valores que são os mesmos em ambos os URLs:

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`: `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

Para interações futuras de API, o principal elemento que muda é o nome do ativo, enquanto as variáveis acima permanecem as mesmas. Nesse caso, faz sentido criar variáveis no Postman para que você não precise especificá-las manualmente sempre.

1. No Postman, selecione **Ambientes**, abra **Todas as variáveis** e selecione **Ambiente**.

   ![Armazenamento do Azure](./images/az104.png){zoomable="yes"}

1. Crie estas 4 variáveis na tabela mostrada e, para as colunas **Valor inicial** e **Valor atual**, insira seus valores pessoais específicos.

   - `AZURE_STORAGE_URL`: sua url
   - `AZURE_STORAGE_CONTAINER`: seu nome de container
   - `AZURE_STORAGE_SAS_READ`: seu token de leitura SAS
   - `AZURE_STORAGE_SAS_WRITE`: seu token de Gravação SAS

1. Selecione **Salvar**.

   ![Armazenamento do Azure](./images/az105.png){zoomable="yes"}

   Em um dos exercícios anteriores, o **Corpo** da solicitação **Firefly - T2I (styleref) V3** ficou assim:

   `"url": "https://vangeluw.blob.core.windows.net/vangeluw/gradient.jpg?sv=2023-01-03&st=2025-01-13T07%3A16%3A52Z&se=2026-01-14T07%3A16%3A00Z&sr=b&sp=r&sig=x4B1XZuAx%2F6yUfhb28hF0wppCOMeH7Ip2iBjNK5A%2BFw%3D"`

   ![Armazenamento do Azure](./images/az24.png){zoomable="yes"}

1. Altere o URL para:

   `"url": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/gradient.jpg{{AZURE_STORAGE_SAS_READ}}"`

1. Selecione **Enviar** para testar as alterações que você fez.

   ![Armazenamento do Azure](./images/az106.png){zoomable="yes"}

   Se as variáveis foram configuradas corretamente, um URL de imagem será retornado.

   ![Armazenamento do Azure](./images/az107.png){zoomable="yes"}

1. Abra o URL da imagem para verificar sua imagem.

   ![Armazenamento do Azure](./images/az108.jpg)

## Próximas etapas

Ir para [Trabalho com APIs do Photoshop](./ex3.md){target="_blank"}

Retorne para [Visão geral dos Serviços da Adobe Firefly](./firefly-services.md){target="_blank"}

Voltar para [Todos os Módulos](./../../../overview.md){target="_blank"}
