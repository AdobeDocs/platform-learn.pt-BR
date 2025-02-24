---
title: AEM CS - Crie seu site com base em documento
description: AEM CS - Crie seu site com base em documento
kt: 5342
doc-type: tutorial
exl-id: db366111-3873-4504-95f1-b240836c833f
source-git-commit: dd075b0296c6ba06d72b229145635060c2c6abb1
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---

# 1.1.2 Criar o site com base em documento

Enquanto aguarda a criação de seu Programa Cloud Manager, você tem tempo suficiente para configurar seu primeiro site de criação baseado em documento. O exercício abaixo é baseado no [Tutorial do desenvolvedor do aem.live](https://www.aem.live/developer/tutorial){target="_blank"}. Siga as etapas abaixo para começar.

## 1.1.2.1 Configurar o Google Drive

Ir para [https://drive.google.com](https://drive.google.com){target="_blank"}. Clique em **+ Nova** e em **Nova Pasta**.

![AEMCS](./images/googledrive1.png){zoomable="yes"}

Nomeie sua pasta `aemdocb-test`. Clique em **Criar**.

![AEMCS](./images/googledrive2.png){zoomable="yes"}

Baixe o arquivo [aemboilerplate.zip](./../../../assets/aem/aemboilerplate.zip){target="_blank"} e extraia-o no computador.

![AEMCS](./images/googledrive3.png){zoomable="yes"}

Você verá três arquivos nessa pasta. Copie esses arquivos na nova pasta Google Drive.

![AEMCS](./images/googledrive4.png){zoomable="yes"}

Agora é necessário converter esses arquivos em um arquivo Google nativo. Para fazer isso, abra cada arquivo e vá para **Arquivo** > **Salvar como Google Docs**.

![AEMCS](./images/googledrive5.png){zoomable="yes"}

Você deve fazer isso para todos os 3 arquivos e depois verá 6 arquivos na pasta Google Drive.

![AEMCS](./images/googledrive6.png){zoomable="yes"}

Você tem isso na sua pasta.

![AEMCS](./images/googledrive7.png){zoomable="yes"}

Para que a demonstração de criação baseada em documentos funcione, agora você precisa compartilhar sua pasta do Google Drive com o endereço de email **helix@adobe.com**. Clique no nome da sua pasta, clique em **Compartilhar** e em **Compartilhar** novamente.

![AEMCS](./images/googledrive8.png){zoomable="yes"}

Insira o endereço de email **helix@adobe.com** e clique em **Enviar**.

![AEMCS](./images/googledrive9.png){zoomable="yes"}

Em seguida, copie e anote o URL da pasta Google Drive conforme necessário no próximo exercício. Clique no nome da sua pasta, clique em **Compartilhar** e em **Copiar link**.

![AEMCS](./images/googledrive10.png){zoomable="yes"}

`https://drive.google.com/drive/folders/1PNIOFeptIfszSebawT-Y_bwB4_anQWk5?usp=drive_link`

Você deve remover o parâmetro da cadeia de caracteres de consulta `?usp=drive_link` para que a URL fique com esta aparência:

`https://drive.google.com/drive/folders/1PNIOFeptIfszSebawT-Y_bwB4_anQWk5`

## 1.1.2.2 Configurar o repositório GitHub

Ir para [https://github.com](https://github.com){target="_blank"}. Clique em **Fazer logon**.

![AEMCS](./images/aemcssetup1.png){zoomable="yes"}

Insira suas credenciais. Clique em **Fazer logon**.

![AEMCS](./images/aemcssetup2.png){zoomable="yes"}

Depois de fazer logon, você verá seu Painel do GitHub.

![AEMCS](./images/aemcssetup3.png){zoomable="yes"}

Ir para [https://github.com/adobe/aem-boilerplate](https://github.com/adobe/aem-boilerplate){target="_blank"}. Você verá isso. Clique em **Usar este modelo** e em **Criar um novo repositório**.

![AEMCS](./images/aemdocbcssetup4.png){zoomable="yes"}

Para o **Nome do repositório**, use `aemdocb-test`. Defina a visibilidade como **Particular**. Clique em **Criar repositório**.

![AEMCS](./images/aemdocbcssetup5.png){zoomable="yes"}

Após alguns segundos, o repositório será criado.

![AEMCS](./images/aemdocbcssetup6.png){zoomable="yes"}

Em seguida, vá para [https://github.com/apps/aem-code-sync](https://github.com/apps/aem-code-sync){target="_blank"}. Clique em **Configurar**.

![AEMCS](./images/aemcssetup7.png){zoomable="yes"}

Clique em sua conta GitHub.

![AEMCS](./images/aemcssetup8.png){zoomable="yes"}

Clique em **Selecionar apenas repositórios** e, em seguida, adicionar o repositório que você acabou de criar. Em seguida, clique em **Instalar**.

![AEMCS](./images/aemdocbcssetup9.png){zoomable="yes"}

Você receberá essa confirmação.

![AEMCS](./images/aemcssetup10.png){zoomable="yes"}

## 1.1.2.3 Arquivo de atualização fstab.yaml

No repositório do GitHub, clique em para abrir o arquivo `fstab.yaml`.

![AEMCS](./images/aemdocbcssetup11.png){zoomable="yes"}

Clique no ícone **editar**.

![AEMCS](./images/aemdocbcssetup12.png){zoomable="yes"}

Agora é necessário atualizar o valor do campo **url** na linha 2.

![AEMCS](./images/aemdocbcssetup13.png){zoomable="yes"}

É necessário substituir o valor atual pelo URL do seu ambiente específico do AEM CS em combinação com as configurações do seu repositório GitHub.

Este é o valor atual da URL: `https://drive.google.com/drive/u/0/folders/1MGzOt7ubUh3gu7zhZIPb7R7dyRzG371j`.

Substitua esse valor pela URL copiada da pasta Unidade Google, `https://drive.google.com/drive/folders/1PNIOFeptIfszSebawT-Y_bwB4_anQWk5`. Clique em **Confirmar alterações...**.

![AEMCS](./images/aemdocbcssetup14.png){zoomable="yes"}

Clique em **Confirmar alterações**.

![AEMCS](./images/aemdocbcssetup15.png){zoomable="yes"}

## 1.1.2.4 Instalar extensão do AEM Sidekick

Ir para [https://chromewebstore.google.com/detail/aem-sidekick/ccfggkjabjahcjoljmgmklhpaccedipo](https://chromewebstore.google.com/detail/aem-sidekick/ccfggkjabjahcjoljmgmklhpaccedipo){target="_blank"}. Clique em **Adicionar ao Chrome**.

![AEMCS](./images/aemdocbcssetup16.png){zoomable="yes"}

Fixar a extensão **AEM Sidekick**.

![AEMCS](./images/aemdocbcssetup17.png){zoomable="yes"}

## 1.1.2.5 Pré-visualizar e publicar seu site baseado em documento

Volte para a pasta Google Drive. Na barra de tarefas, clique na extensão **AEM Sidekick**. Em seguida, você verá um pop-up, barra de AEM Sidekick, na sua pasta.

![AEMCS](./images/aemdocbcssetup18.png){zoomable="yes"}

Selecione os 3 arquivos na pasta Google Drive. Clique em **Visualizar**.

![AEMCS](./images/aemdocbcssetup19.png){zoomable="yes"}

Clique novamente em **Visualizar**.

![AEMCS](./images/aemdocbcssetup20.png){zoomable="yes"}

Clique para fechar a janela pop-up verde.

![AEMCS](./images/aemdocbcssetup21.png){zoomable="yes"}

Selecione os 3 arquivos na pasta Google Drive novamente. Agora, clique em **Publicar**.

![AEMCS](./images/aemdocbcssetup22.png){zoomable="yes"}

Clique em **Publicar**.

![AEMCS](./images/aemdocbcssetup23.png){zoomable="yes"}

Clique para fechar a caixa de diálogo verde novamente. Agora, selecione o arquivo **índice**, clique em **Copiar URLs** e em **Copiar URLs em tempo real**.

![AEMCS](./images/aemdocbcssetup24.png){zoomable="yes"}

A URL copiada terá esta aparência: `https://main--aemdocb-test--woutervangeluwe.aem.live/`.

No URL acima:

- **principal** refere-se à ramificação no seu repositório GitHub
- **aemdocb-test** refere-se ao nome do repositório GitHub
- **woutervangeluwe** refere-se ao nome da conta de usuário do GitHub
- **.live** refere-se ao ambiente ativo da sua instância do AEM
- Você pode substituir **.live** por **.page** para abrir o ambiente de visualização da sua instância do AEM

Abra uma nova janela do navegador e navegue até o URL.

![AEMCS](./images/aemdocbcssetup25.png){zoomable="yes"}

## 1.1.2.6 Faça uma alteração e publique-a

Volte para a sua Unidade Google e abra o filtro **índice** no Google.

![AEMCS](./images/aemdocbcssetup27.png){zoomable="yes"}

Substitua o texto **Testing** por qualquer outro texto de sua escolha. Clique em **Visualizar**.

![AEMCS](./images/aemdocbcssetup28.png){zoomable="yes"}

A versão de visualização do site será aberta. Revise sua alteração e clique em **Publicar**.

![AEMCS](./images/aemdocbcssetup29.png){zoomable="yes"}

Você verá a versão ao vivo do site.

![AEMCS](./images/aemdocbcssetup30.png){zoomable="yes"}

O exercício acima foi uma boa maneira de começar e experimentar a criação baseada em documentos. Agora você pode continuar com o próximo exercício, onde você configurará seu próprio site de demonstração usando o CitiSignal como uma marca de demonstração.

Próxima Etapa: [1.1.3 Configurar o ambiente do AEM CS](./ex3.md){target="_blank"}

Voltar para o [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./aemcs.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
