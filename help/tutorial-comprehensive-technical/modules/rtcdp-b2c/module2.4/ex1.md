---
title: Ativação de segmento para o Hub de eventos do Microsoft Azure - Configurar o ambiente do Microsoft Azure
description: Ativação de segmento para o Hub de eventos do Microsoft Azure - Configurar o ambiente do Microsoft Azure
kt: 5342
doc-type: tutorial
exl-id: 772b4d2b-144a-4f29-a855-8fd3493a85d2
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 2.4.1 Configurar o ambiente

## Criar uma assinatura do Azure

>[!NOTE]
>
>Se você já tiver uma Assinatura do Azure, ignore esta etapa. Nesse caso, prossiga com o próximo exercício.

Acesse [https://portal.azure.com](https://portal.azure.com) e faça logon com sua conta do Azure. Se você não tiver um, use seu endereço de email pessoal para criar sua conta do Azure.

![02-azure-portal-email.png](./images/02azureportalemail.png)

Depois de fazer logon, você verá a seguinte tela:

![03-azure-logged-in.png](./images/03azureloggedin.png)

Clique no menu à esquerda e selecione **Todos os recursos**. A tela de assinatura do Azure será exibida se você ainda não tiver assinado. Nesse caso, selecione **Iniciar com uma avaliação gratuita do Azure**.

![04-azure-start-subscribe.png](./images/04azurestartsubscribe.png)

Preencha o formulário de assinatura do Azure, forneça seu celular e cartão de crédito para ativação (você terá uma camada gratuita por 30 dias e não será cobrado, a menos que atualize).

Quando o processo de assinatura for concluído, você poderá prosseguir:

![06-azure-subscription-ok.png](./images/06azuresubscriptionok.png)

## Instalar o Visual Code Studio

Você usará o Microsoft Visual Code Studio para gerenciar seu Projeto do Azure. Você pode baixá-lo via [este link](https://code.visualstudio.com/download). Siga as instruções de instalação do sistema operacional específico no mesmo site.

## Instalar extensões do Visual Code

Instale as Funções do Azure para Visual Studio Code de [https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions). Clique no botão de instalação:

![07-azure-code-extension-install.png](./images/07azurecodeextensioninstall.png)

Instale a Conta do Azure e o Logon para Visual Studio Code de [https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account). Clique no botão de instalação:

![08-azure-account-extension-install.png](./images/08azureaccountextensioninstall.png)

## Instalar node.js

>[!NOTE]
>
>Se você já tiver o node.js instalado, ignore esta etapa. Nesse caso, prossiga com o próximo exercício.

### macOS

Certifique-se de ter o [Homebrew](https://brew.sh/) instalado primeiro. Siga as instruções [aqui](https://brew.sh/).

![Nó](./images/brew.png)

Depois de instalar o Homebrew, execute este comando:

```javascript
brew install node
```

### Windows

Baixe o [Windows Installer](https://nodejs.org/en/#home-downloadhead) diretamente do site [nodejs.org](https://nodejs.org/en/).

## Verificar a versão do node.js

Para este módulo, você precisa ter o node.js versão 18 instalado. Qualquer outra versão do node.js pode causar problemas com este exercício.

Antes de continuar, verifique sua versão do node.js agora.

Execute este comando para verificar a versão do node.js:

```javascript
node -v
```

Se sua versão for inferior ou superior a 18, será necessário atualizar ou fazer downgrade.

### Atualização/downgrade da versão node.js no macOS

Verifique se o pacote **n** está instalado.

Para instalar o pacote **n**, execute este comando:

```javascript
sudo npm install -g n
```

Se sua versão for inferior ou superior à versão 12, execute este comando para atualizar ou fazer downgrade:

```javascript
sudo n 18
```

### Atualização/Rebaixamento da versão do node.js no Windows

Desinstale o node.js do Windows > Painel de controle > Adicionar ou remover programas.

Instalando a versão necessária do site [nodejs.org](https://nodejs.org/en/).

## Instalar pacote NPM: solicitação

Você precisa instalar o pacote **request** como parte da instalação do node.js.

Para instalar o pacote **request**, execute este comando:

```javascript
npm install request
```

## Instalar as Ferramentas principais do Azure Functions:

```
brew tap azure/functions
brew install azure-functions-core-tools@4
```

Próxima etapa: [2.4.2 Configurar o ambiente do EventHub do Microsoft Azure](./ex2.md)

[Voltar ao módulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Voltar a todos os módulos](./../../../overview.md)
