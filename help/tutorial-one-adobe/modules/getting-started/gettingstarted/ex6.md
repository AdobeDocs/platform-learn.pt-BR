---
title: Introdução - Adobe I/O
description: Introdução - Adobe I/O
kt: 5342
doc-type: tutorial
exl-id: 00f17d4f-a2c8-4e8e-a1ff-556037a60629
source-git-commit: a45283bf5263a6de5c2f83f5be35b7d03ce04d7d
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# Configurar o projeto do Adobe I/O

## Criar seu projeto do Adobe I/O

Neste exercício, o Adobe I/O é usado para consultar vários endpoints do Adobe. Siga estas etapas para configurar o Adobe I/O.

Ir para [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}.

![Nova integração do Adobe I/O](./images/iohome.png){zoomable="yes"}

Selecione a instância correta no canto superior direito da tela. Sua instância é `--aepImsOrgName--`.

>[!NOTE]
>
> A captura de tela abaixo mostra uma organização específica sendo selecionada. Quando você estiver assistindo a este tutorial, é muito provável que sua organização tenha um nome diferente. Quando se inscreveu neste tutorial, você recebeu os detalhes do ambiente que devem ser usados. Siga estas instruções.

Em seguida, selecione **Criar novo projeto**.

![Nova integração do Adobe I/O](./images/iocomp.png){zoomable="yes"}

### API do Firefly Services

>[!IMPORTANT]
>
>Dependendo do caminho de aprendizado selecionado, talvez você não tenha acesso à API do Firefly Services. Você só terá acesso à API do Firefly Services se estiver no Caminho de Aprendizado **Firefly**, **Workfront Fusion**, **ALL** ou quando estiver participando de um **workshop presencial**. Você pode pular esta etapa se não estiver em um desses caminhos de aprendizagem.

Você deverá ver isso. Selecione **+ Adicionar ao Projeto** e escolha **API**.

![Nova integração do Adobe I/O](./images/adobe_io_access_api.png){zoomable="yes"}

Sua tela deve ter esta aparência.

![Nova integração do Adobe I/O](./images/api1.png){zoomable="yes"}

Selecione **Creative Cloud** e escolha **Firefly - Firefly Services**, depois selecione **Próximo**.

![Nova integração do Adobe I/O](./images/api3.png){zoomable="yes"}

Forneça um nome para a credencial: `--aepUserLdap-- - One Adobe OAuth credential` e selecione **Avançar**.

![Nova integração do Adobe I/O](./images/api4.png){zoomable="yes"}

Selecione o perfil padrão **Configuração padrão do Firefly Services** e selecione **Salvar API configurada**.

![Nova integração do Adobe I/O](./images/api9.png){zoomable="yes"}

Você deverá ver isso.

![Nova integração do Adobe I/O](./images/api10.png){zoomable="yes"}

### API do Photoshop Services

>[!IMPORTANT]
>
>Dependendo do caminho de aprendizado selecionado, talvez você não tenha acesso à API do Photoshop Services. Você só terá acesso à API do Photoshop Services se estiver no Caminho de Aprendizado **Firefly**, **Workfront Fusion**, **ALL** ou quando estiver participando de um **workshop presencial**. Você pode pular esta etapa se não estiver em um desses caminhos de aprendizagem.

Selecione **+ Adicionar ao Projeto** e **API**.

![Armazenamento do Azure](./images/ps2.png){zoomable="yes"}

Selecione **Creative Cloud** e escolha **Photoshop - Firefly Services**. Selecione **Próximo**.

![Armazenamento do Azure](./images/ps3.png){zoomable="yes"}

Selecione **Próximo**.

![Armazenamento do Azure](./images/ps4.png){zoomable="yes"}

Em seguida, é necessário selecionar um perfil de produto que defina quais permissões estão disponíveis para essa integração.

Selecione **Configuração padrão do Firefly Services** e **Configuração padrão dos Serviços de Automação da Creative Cloud**.

Selecione **Salvar API configurada**.

![Armazenamento do Azure](./images/ps5.png){zoomable="yes"}

Você deverá ver isso.

![Nova integração do Adobe I/O](./images/ps7.png){zoomable="yes"}

### API do Adobe Experience Platform

>[!IMPORTANT]
>
>Dependendo do caminho de aprendizado selecionado, talvez você não tenha acesso à API do Adobe Experience Platform. Você só terá acesso à API do Adobe Experience Platform se estiver no caminho de aprendizado **AEP + Aplicativos**, **TODOS** ou quando estiver participando de um **workshop presencial**. Você pode pular esta etapa se não estiver em um desses caminhos de aprendizagem.

Selecione **+ Adicionar ao Projeto** e **API**.

![Armazenamento do Azure](./images/aep1.png){zoomable="yes"}

Selecione **Adobe Experience Platform** e escolha **API Experience Platform**. Selecione **Próximo**.

![Armazenamento do Azure](./images/aep2.png){zoomable="yes"}

Selecione **Próximo**.

![Armazenamento do Azure](./images/aep3.png){zoomable="yes"}

Em seguida, é necessário selecionar um perfil de produto que defina quais permissões estão disponíveis para essa integração.

Selecione **Adobe Experience Platform - Todos os usuários - PROD**.

>[!NOTE]
>
>O nome do Perfil de produto do AEP depende de como o ambiente foi configurado. Se você não vir o perfil de produto mencionado acima, talvez tenha um perfil de produto chamado **Acesso total à produção padrão**. Caso não tenha certeza de qual escolher, pergunte ao administrador do sistema da AEP.

Selecione **Salvar API configurada**.

![Armazenamento do Azure](./images/aep4.png){zoomable="yes"}

Você deverá ver isso.

![Nova integração do Adobe I/O](./images/aep5.png){zoomable="yes"}

### Nome do projeto

Clique no nome do projeto.

![Nova integração do Adobe I/O](./images/api13.png){zoomable="yes"}

Selecione **Editar Projeto**.

![Nova integração do Adobe I/O](./images/api14.png){zoomable="yes"}

Digite um nome amigável para a integração: `--aepUserLdap-- One Adobe tutorial` e selecione **Salvar**.

![Nova integração do Adobe I/O](./images/api15.png){zoomable="yes"}

A configuração do projeto do Adobe I/O foi concluída.

![Nova integração do Adobe I/O](./images/api16.png){zoomable="yes"}

## Próximas etapas

Ir para [Opção 1: configuração do Postman](./ex7.md){target="_blank"}

Ir para [Opção 2: configuração PostBuster](./ex8.md){target="_blank"}

Volte para [Introdução](./getting-started.md){target="_blank"}

Voltar para [Todos os módulos](./../../../overview.md){target="_blank"}
