---
title: Criar o primeiro formulário
description: Criar o primeiro formulário
kt: 5342
doc-type: tutorial
source-git-commit: 8f59b9fdadc9c5aeadb1d4ecccd75090c339b43e
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 10%

---

# 1.3.1 Criar o primeiro formulário

>[!IMPORTANT]
>
>Para concluir este exercício, você precisa ter acesso a um ambiente de trabalho do AEM Assets CS Author com o AEM Assets Dynamic Media habilitado.
>
>Se você não tiver um ambiente como esse, acesse [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Siga as instruções aqui e você terá acesso a esse ambiente.

>[!IMPORTANT]
>
>Se você tiver configurado anteriormente um Programa AEM CS com um ambiente AEM Assets CS, pode ser que sua sandbox AEM CS tenha hibernado. Considerando que a deshibernação de uma sandbox desse tipo leva de 10 a 15 minutos, seria uma boa ideia iniciar o processo de deshibernação agora para que você não precise aguardar mais tarde.

## 1.3.1.1 -

Ir para [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. A organização que você deve selecionar é `--aepImsOrgName--`. Abra o ambiente.

![AEM Forms](./images/aemforms1.png)

Ir para **Forms**.

![AEM Forms](./images/aemforms2.png)

Vá para **Forms e Documentos**.

![AEM Forms](./images/aemforms3.png)

Clique em **Criar** e selecione **Formulário adaptável**.

![AEM Forms](./images/aemforms4.png)

Selecione **Edge Delivery Services** e **Página em branco**. Clique em **Criar**.

![AEM Forms](./images/aemforms5.png)

Você deverá ver isso. Preencha os seguintes campos:

- **Título**: `Fiber Max Interest Form`
- **Nome**: deve ser preenchido automaticamente com base no campo **Título**.
- **URL do Github**: forneça o caminho para o repositório Github que está vinculado ao seu site

Clique em **Criar**.

![AEM Forms](./images/aemforms6.png)

Depois de clicar em **Criar**, o **Editor Universal** deverá abrir automaticamente e você deverá ver algo parecido com isso. Clique no ícone para abrir a **Árvore de conteúdo**.

![AEM Forms](./images/aemforms7.png)

Na **Árvore de conteúdo**, selecione o objeto **Formulário adaptável**.

![AEM Forms](./images/aemforms8.png)

Em seguida, clique no ícone **+** para adicionar um novo elemento e selecione **Entrada de texto**.

![AEM Forms](./images/aemforms9.png)

Na **Árvore de conteúdo**, selecione o campo **Entrada de texto**.

![AEM Forms](./images/aemforms10.png)

Vá para a exibição **Básico**. Você deveria ver isto.

Preencha os seguintes campos:

- **Nome**: `first-name`
- **Título**: `First Name`

Em seguida, vá para **Validação**.

![AEM Forms](./images/aemforms11.png)

Inverta a chave para tornar este campo obrigatório. Preencha os seguintes campos:

- **Mensagem de erro**: `Enter your first name`
- **Padrão**: `[A-Za-z][A-Za-z ]+`
- **Mensagem de erro de padrão**: `Letters only!`

![AEM Forms](./images/aemforms12.png)

Na **Árvore de conteúdo**, selecione o campo **Formulário adaptável**. Clique no ícone **+** e selecione **Entrada de texto**.

![AEM Forms](./images/aemforms13.png)

Na **Árvore de conteúdo**, selecione o campo recém-criado **Entrada de texto**. Ir para **Propriedades**.

![AEM Forms](./images/aemforms14.png)

Vá para a exibição **Básico**. Você deveria ver isto.

Preencha os seguintes campos:

- **Nome**: `last-name`
- **Título**: `Last Name`

Em seguida, vá para **Validação**.

![AEM Forms](./images/aemforms15.png)

Inverta a chave para tornar este campo obrigatório. Preencha os seguintes campos:

- **Mensagem de erro**: `Enter your last name`
- **Padrão**: `[A-Za-z][A-Za-z ]+`
- **Mensagem de erro de padrão**: `Letters only!`

![AEM Forms](./images/aemforms16.png)

Na **Árvore de conteúdo**, selecione o campo **Formulário adaptável**. Clique no ícone **+** e selecione **Entrada de texto**.

![AEM Forms](./images/aemforms17.png)

Na **Árvore de conteúdo**, selecione o campo recém-criado **Entrada de texto**. Ir para **Propriedades**.

![AEM Forms](./images/aemforms18.png)

Vá para a exibição **Básico**. Você deveria ver isto.

Preencha os seguintes campos:

- **Nome**: `email`
- **Título**: `Email`

Em seguida, vá para **Validação**.

![AEM Forms](./images/aemforms19.png)

Inverta a chave para tornar este campo obrigatório. Preencha os seguintes campos:

- **Mensagem de erro**: `Enter your email address`
- **Padrão**: `^[^@]+@[^@]+\.[^@]+$`
- **Mensagem de erro de padrão**: `Please verify your email address!`

![AEM Forms](./images/aemforms20.png)

Na **Árvore de conteúdo**, selecione o campo **Formulário adaptável**. Clique no ícone **+** e selecione **Entrada de texto**.

![AEM Forms](./images/aemforms21.png)

Na **Árvore de conteúdo**, selecione o campo recém-criado **Entrada de texto**.

![AEM Forms](./images/aemforms22.png)

Vá para a exibição **Básico**. Você deveria ver isto.

Preencha os seguintes campos:

- **Nome**: `city`
- **Título**: `city`

Em seguida, vá para **Validação**.

![AEM Forms](./images/aemforms23.png)

Inverta a chave para tornar este campo obrigatório. Preencha os seguintes campos:

- **Mensagem de erro**: `Enter your city`
- **Padrão**: `[A-Za-z][A-Za-z ]+`
- **Mensagem de erro de padrão**: `Letters only!`

![AEM Forms](./images/aemforms24.png)

Clique em **Publicar**.

![AEM Forms](./images/aemforms25.png)

Clique novamente em **Publicar**.

![AEM Forms](./images/aemforms26.png)

Clique em para abrir o formulário.

![AEM Forms](./images/aemforms27.png)

Você pode então preencher o formulário, mas ainda não pode enviá-lo.

![AEM Forms](./images/aemforms28.png)

## Próximas etapas

Próxima Etapa: [-](./ex1.md){target="_blank"}

Voltar para [Adobe Experience Manager Forms com Edge Delivery Services](./aemforms.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
