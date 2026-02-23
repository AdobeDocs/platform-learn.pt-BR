---
title: Criar o primeiro formulário
description: Criar o primeiro formulário
kt: 5342
doc-type: tutorial
exl-id: 288e113f-2e9e-4352-8ddd-ca231b552b70
source-git-commit: d2b746d50ec559e0b29a7adb27c3521b0e00d386
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 9%

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

## 1.3.1.1 Requisitos de ambiente para usar o AEM Forms com o Edge Delivery Services

Antes de configurar seu primeiro formulário, há vários requisitos que precisam ser atendidos antes de você poder seguir as etapas abaixo.

### Configuração do programa

Nos **Complementos e Soluções** do seu Programa Cloud Manager, o **Forms** precisa ser habilitado.

![AEM Forms](./images/program.png)

### blocos

No repositório do GitHub, é necessário ter os seguintes blocos disponíveis:

- **formulário**
- **formulário-incorporado-adaptável**

![AEM Forms](./images/block.png)

### scripts

No repositório do GitHub, é necessário ter os seguintes scripts disponíveis:

- **editor-formulário-support.css**
- **editor de formulários-support.js**

![AEM Forms](./images/scripts1.png)

Além disso, no arquivo **editor-support.js**, as seguintes alterações precisam ser feitas para habilitar a edição de formulários no Editor Universal.

- altere a declaração da função de **function attachEventListners(main)** para **função assíncrona attachEventListners(main)**
- aditar as linhas 152 e 153:

```
const module = await import('./form-editor-support.js');
module.attachEventListners(main);
```

![AEM Forms](./images/scripts2.png)

Além disso, no arquivo **editor-support.js**, altere as linhas 90-92 desta forma:

```
if (block.dataset.aueModel === 'form') {
        return true;
      } else if (newBlock) {
```

![AEM Forms](./images/scripts3.png)

### paths.json

Verifique a configuração do repositório Github, especificamente no arquivo **paths.json**. Estas linhas precisam estar presentes no arquivo:

- Em mapeamentos: **&quot;/content/forms/af/:/forms/&quot;**
- Inclusões em: **&quot;/content/forms/af/&quot;**

```json
{
  "mappings": [
    "/content/CitiSignal/:/",
    "/content/CitiSignal/configuration:/.helix/config.json",
    "/content/CitiSignal/headers:/.helix/headers.json",
    "/content/CitiSignal/metadata:/metadata.json",
    "/content/CitiSignal.resource/enrichment/enrichment.json:/enrichment/enrichment.json",
    "/content/forms/af/:/forms/"
  ],
  "includes": [
    "/content/CitiSignal/",
    "/content/forms/af/"
  ]
}
```

![AEM Forms](./images/paths.png)

Com esses requisitos em vigor, você pode criar seu primeiro formulário.

## 1.3.1.2 Criar formulário

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

Depois de publicar o formulário, ele também estará disponível no domínio do Edge Delivery Services, que se parece com o seguinte:

`https://main--techinsidersXX-citisignal-aem-accs--woutervangeluwe.aem.page/forms/fiber-max-interest-form`

![AEM Forms](./images/aemforms29.png)

## 1.3.1.3 Enviar formulário

Para enviar seu formulário, são necessários dois itens:

- um botão **Enviar**
- uma ação **Enviar**

Além disso, neste exercício, você deve usar uma planilha do Google para registrar os envios deste formulário.

### Planilha do Google

Vá para [https://drive.google.com](https://drive.google.com) e crie uma nova planilha em branco.

![AEM Forms](./images/sheet1.png)

Nomeie seu arquivo `citisignal-fiber-max-interest`.

Na linha 1, nas células A-B-C-D, insira os seguintes nomes de campo:

- nome
- sobrenome
- email
- city

Em seguida, clique em **Compartilhar**.

![AEM Forms](./images/sheet2.png)

Compartilhe o arquivo com **forms@adobe.com** com direitos de acesso de nível **Editor**.

Em seguida, clique em **Copiar link**.

Clique em **Enviar**.

![AEM Forms](./images/sheet3.png)

Você precisará usar o link copiado na próxima etapa.

### Botão Enviar

Para configurar o botão **Enviar**, vá para a **árvore de conteúdo**, selecione o **Formulário adaptável**, clique no ícone **+** e selecione **Enviar**.

![AEM Forms](./images/aemforms30.png)

Você deverá ver isso.

![AEM Forms](./images/aemforms31.png)

### Enviar ação

As ações enviar fazem parte de uma extensão do Universal Editor.

>[!NOTE]
>
>Se você não vir o ícone **Editar propriedades do formulário**, significa que essa extensão ainda não está habilitada para o seu ambiente. Para habilitar esta extensão, vá para [https://experience.adobe.com/#/aem/extension-manager](https://experience.adobe.com/#/aem/extension-manager) e habilite a extensão **Editar Propriedades do Formulário**.
>
>![AEM Forms](./images/extmgr.png)

Clique no ícone **Editar propriedades do formulário**.

![AEM Forms](./images/aemforms32.png)

Selecione **Enviar para Planilha**. Cole o URL da Planilha do Google que você criou anteriormente.

Clique em **Salvar e fechar**.

![AEM Forms](./images/aemforms33.png)

>[!NOTE]
>
>Se você receber um erro 401 - Não autorizado, pode ser. porque seu ambiente não foi habilitado para funcionar com o Google Sheets. Entre em contato com seu representante da Adobe para ativar seu ambiente.

Clique em **Publicar**.

![AEM Forms](./images/aemforms34.png)

Clique novamente em **Publicar**.

![AEM Forms](./images/aemforms35.png)

Você pode atualizar seu site, preencher os formulários e clicar em **Enviar**.

![AEM Forms](./images/aemforms36.png)

O envio deve ser bem-sucedido.

![AEM Forms](./images/aemforms37.png)

Se você observar sua planilha do Google, verá o envio bem-sucedido lá também.

![AEM Forms](./images/aemforms38.png)

Você concluiu este exercício com êxito.

## Próximas etapas

Voltar para [Adobe Experience Manager Forms com Edge Delivery Services](./aemforms.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
