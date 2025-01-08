---
title: Introdução aos serviços do Firefly
description: Introdução aos serviços do Firefly
kt: 5342
doc-type: tutorial
exl-id: 5f9803a4-135c-4470-bfbb-a298ab1fee33
source-git-commit: ea06ca2d05195efa57643d45d7e50d3d914081d3
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 1%

---

# 1.1.2 Otimizar o processo de Firefly usando o Microsoft Azure e URLs pré-assinados

## 1.1.2.1 Criar uma assinatura do Azure

>[!NOTE]
>
>Se você já tiver uma Assinatura do Azure existente, ignore esta etapa. Nesse caso, prossiga com o próximo exercício.

Acesse [https://portal.azure.com](https://portal.azure.com) e faça logon com sua conta do Azure. Se você não tiver um, use seu endereço de email pessoal para criar sua conta do Azure.

![Armazenamento do Azure](./images/02azureportalemail.png)

Depois de fazer logon, você verá a seguinte tela:

![Armazenamento do Azure](./images/03azureloggedin.png)

Clique no menu à esquerda e selecione **Todos os recursos**. A tela de assinatura do Azure será exibida se você ainda não tiver assinado. Nesse caso, selecione **Iniciar com uma avaliação gratuita do Azure**.

![Armazenamento do Azure](./images/04azurestartsubscribe.png)

Preencha o formulário de assinatura do Azure, forneça seu celular e cartão de crédito para ativação (você terá uma camada gratuita por 30 dias e não será cobrado, a menos que atualize).

Quando o processo de assinatura for concluído, você poderá prosseguir:

![Armazenamento do Azure](./images/06azuresubscriptionok.png)

## 1.1.2.2 Criar Conta de Armazenamento do Azure

Pesquise por `storage account` e clique em **Contas de armazenamento**.

![Armazenamento do Azure](./images/azs1.png)

Clique em **+ Criar**.

![Armazenamento do Azure](./images/azs2.png)

Preencha os seguintes detalhes:

- Selecione sua **Assinatura**
- Selecione (ou crie) um **Grupo de recursos**
- **Nome da conta de armazenamento**: use `--aepUserLdap--`

Clique em **Revisar + criar**.

![Armazenamento do Azure](./images/azs3.png)

Clique em **Criar**.

![Armazenamento do Azure](./images/azs4.png)

Você receberá uma confirmação semelhante. Clique em **Ir para o recurso**.

![Armazenamento do Azure](./images/azs5.png)

Sua Conta de Armazenamento do Azure está pronta para ser usada.

![Armazenamento do Azure](./images/azs6.png)

Clique em **Armazenamento de dados** e vá para **Contêineres**. Clique em **+ Contêiner**.

![Armazenamento do Azure](./images/azs7.png)

Para o nome, use `--aepUserLdap--`. Clique em **Criar**.

![Armazenamento do Azure](./images/azs8.png)

Seu contêiner agora está pronto para ser usado.

![Armazenamento do Azure](./images/azs9.png)

## 1.1.2.3 Instalar o Azure Storage Explorer

Você usará o Microsoft Azure Storage Explorer para gerenciar seus arquivos. Você pode baixá-lo via [este link](https://azure.microsoft.com/en-us/products/storage/storage-explorer#Download-4). Selecione a versão correta para seu sistema operacional específico, baixe-a e instale-a.

![Armazenamento do Azure](./images/az10.png)

Depois que o aplicativo estiver instalado, abra-o. Você verá algo semelhante a isso. Clique em **Fazer logon com o Azure**.

![Armazenamento do Azure](./images/az11.png)

Clique em **Assinatura**.

![Armazenamento do Azure](./images/az12.png)

Selecione **Azure** e clique em **Avançar**.

![Armazenamento do Azure](./images/az13.png)

Selecione sua conta do Microsoft Azure e conclua o processo de autenticação.

![Armazenamento do Azure](./images/az14.png)

Depois de autenticado, você verá uma mensagem como esta.

![Armazenamento do Azure](./images/az15.png)

Retorne ao aplicativo Microsoft Azure Storage Explorer. Selecione sua assinatura e clique em **Abrir o Explorer**.

![Armazenamento do Azure](./images/az16.png)

Você encontrará sua conta de armazenamento em **Contas de Armazenamento**.

![Armazenamento do Azure](./images/az17.png)

Abra **Contêineres de Blob** e clique no contêiner criado no exercício anterior.

![Armazenamento do Azure](./images/az18.png)

## 1.1.2.4 Upload manual do arquivo e uso de um arquivo de gradiente como referência de estilo

Agora você deve carregar um arquivo de gradiente de sua escolha no seu container. Você pode usar qualquer arquivo de gradiente de sua escolha ou pode usar [este arquivo](./images/gradient.jpg) baixando-o em seu computador.

![Armazenamento do Azure](./images/gradient.jpg)

Solte o arquivo de gradiente em seu container no Azure Storage Explorer.

Depois de carregado, você verá em seu container:

![Armazenamento do Azure](./images/az19.png)

Clique com o botão direito do mouse no arquivo `gradient.jpg` e clique em **Obter Assinatura de Acesso Compartilhado**.

![Armazenamento do Azure](./images/az20.png)

Em **Permissões**, somente **Leitura** é necessário. Clique em **Criar**.

![Armazenamento do Azure](./images/az21.png)

Em seguida, você verá o URL pré-assinado para esse arquivo de imagem. Copie-o conforme necessário para a próxima solicitação de API para o Firefly.

![Armazenamento do Azure](./images/az22.png)

Volte para o Postman. Abra a solicitação **POST - Firefly - T2I (styleref) V3**. Você verá isso no **Corpo**.

![Armazenamento do Azure](./images/az23.png)

Substitua a URL do espaço reservado pela URL pré-assinada do arquivo de gradiente que você copiou do Azure Storage Explorer. Então você terá isto. Clique em **Enviar**.

![Armazenamento do Azure](./images/az24.png)

Em seguida, você obterá uma resposta do Firefly Services novamente, com uma nova imagem. Abra o arquivo de imagem em seu navegador.

![Armazenamento do Azure](./images/az25.png)

Você verá outra imagem com `horses in a field`, mas dessa vez o estilo será semelhante ao arquivo de gradiente fornecido como referência de estilo.

![Armazenamento do Azure](./images/az26.png)

## 1.1.2.5 Upload de arquivo programático

Para usar o carregamento de arquivo programático com as Contas de Armazenamento do Azure, será necessário criar um novo token **SAS (Assinatura de Acesso Compartilhado)**, com permissões que permitam gravar um arquivo.

Para fazer isso, volte para o Azure Storage Explorer. Clique com o botão direito do mouse no contêiner e clique em **Obter Assinatura de Acesso Compartilhado**.

![Armazenamento do Azure](./images/az27.png)

Em **Permissões**, as seguintes permissões são necessárias:

- **Leitura**
- **Adicionar**
- **Create**
- **Write**
- **Lista**

Clique em **Criar**.

![Armazenamento do Azure](./images/az28.png)

Você obterá seu **token SAS**. Clique em **Copiar**.

![Armazenamento do Azure](./images/az29.png)

Agora você pode usar este **token SAS** para carregar um arquivo na sua Conta de Armazenamento do Azure. Volte para o Postman para fazer isso.

Clique para selecionar a pasta **FF - Firefly Services Tech Insiders**, em seguida, clique nos 3 pontos **...** na pasta **Firefly** e em **Adicionar solicitação**.

![Armazenamento do Azure](./images/az30.png)

Você terá uma solicitação vazia. Altere o nome da solicitação para **Carregar arquivo para a Conta de Armazenamento do Azure**, altere o **Tipo de Solicitação** para **PUT** e cole a URL do token SAS na seção de URL.

Em seguida, clique em **Corpo**.

![Armazenamento do Azure](./images/az31.png)

Agora, será necessário selecionar um arquivo do computador local. Você pode usar um novo arquivo de imagem de sua escolha ou pode usar outro arquivo de gradiente que você pode encontrar [aqui](./images/gradient2-p.jpg).

![Arquivo de gradação](./images/gradient2-p.jpg)

Em **Corpo**, selecione **binário** e clique em **Selecionar arquivo** e em **+ Novo arquivo do computador local**.

![Armazenamento do Azure](./images/az32.png)

Selecione o arquivo de sua escolha e clique em **Abrir**.

![Armazenamento do Azure](./images/az33.png)

Você verá isso. A próxima ação é especificar o nome do arquivo que será usado em sua Conta de Armazenamento do Azure. Para fazer isso, você precisa colocar seus cursos na frente do ponto de interrogação **?** na URL. Atualmente, você pode ver isso aqui:

![Armazenamento do Azure](./images/az34.png)

No momento, o URL tem esta aparência, mas precisará ser alterado.

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03...`

O nome de arquivo a ser usado é `gradient2-p.jpg`, o que significa que a URL precisa ser alterada para incluir o nome do arquivo, desta forma:

`https://vangeluw.blob.core.windows.net/vangeluw/gradient2-p.jpg?sv=2023-01-03...`

![Armazenamento do Azure](./images/az34a.png)

Em seguida, vá para **Cabeçalhos**, onde você precisa adicionar um novo cabeçalho manualmente. Use isto:

Blob de tipo x-ms-blob

![Armazenamento do Azure](./images/az35.png)

Vá para **Autorização** e defina o **Tipo de Autenticação** como **Sem Autenticação**. Clique em **Enviar**.

![Armazenamento do Azure](./images/az36.png)

Você verá essa resposta vazia no Postman, o que significa que o upload do arquivo foi concluído.

![Armazenamento do Azure](./images/az37.png)

Se você voltar para o Azure Storage Explorer e atualizar o conteúdo de sua pasta, agora encontrará o arquivo recém-carregado lá.

![Armazenamento do Azure](./images/az38.png)

Próxima Etapa: [1.1.3 ...](./ex3.md)

[Voltar ao módulo 1.1](./firefly-services.md)

[Voltar a todos os módulos](./../../../overview.md)
