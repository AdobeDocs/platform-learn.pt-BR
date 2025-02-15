---
title: Introdução - Adobe I/O
description: Introdução - Adobe I/O
kt: 5342
doc-type: tutorial
source-git-commit: 431f7696df12c8c133aced57c0f639c682304dee
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# Configurar o projeto do Adobe I/O

## Criar seu projeto do Adobe I/O

Neste exercício, o Adobe I/O é usado para consultar vários endpoints do Adobe. Siga estas etapas para configurar o Adobe I/O.

Ir para [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}.

![Nova integração do Adobe I/O](./images/iohome.png){zoomable="yes"}

Selecione a instância correta no canto superior direito da tela. Sua instância é `--aepImsOrgName--`.
Em seguida, selecione **Criar novo projeto**.

![Nova integração do Adobe I/O](./images/iocomp.png){zoomable="yes"}

### API de serviços da Firefly

Você deverá ver isso. Selecione **+ Adicionar ao Projeto** e escolha **API**.

![Nova integração do Adobe I/O](./images/adobe_io_access_api.png){zoomable="yes"}

Sua tela deve ter esta aparência.

![Nova integração do Adobe I/O](./images/api1.png){zoomable="yes"}

Selecione **Creative Cloud** e escolha **Firefly - Firefly Services**, depois selecione **Próximo**.

![Nova integração do Adobe I/O](./images/api3.png){zoomable="yes"}

Forneça um nome para a credencial: `--aepUserLdap-- - One Adobe OAuth credential`e selecione **Avançar**.

![Nova integração do Adobe I/O](./images/api4.png){zoomable="yes"}

Selecione o perfil padrão **Configuração Padrão de Serviços da Firefly** e selecione **Salvar API Configurada**.

![Nova integração do Adobe I/O](./images/api9.png){zoomable="yes"}

Você deverá ver isso.

![Nova integração do Adobe I/O](./images/api10.png){zoomable="yes"}

### API do Photoshop Services

Selecione **+ Adicionar ao Projeto** e **API**.

![Armazenamento do Azure](./images/ps2.png){zoomable="yes"}

Selecione **Creative Cloud** e escolha **Photoshop - Firefly Services**. Selecione **Próximo**.

![Armazenamento do Azure](./images/ps3.png){zoomable="yes"}

Selecione **Próximo**.

![Armazenamento do Azure](./images/ps4.png){zoomable="yes"}

Em seguida, é necessário selecionar um perfil de produto que defina quais permissões estão disponíveis para essa integração.

Selecione **Configuração Padrão dos Serviços Firefly** e **Configuração Padrão dos Serviços Creative Cloud Automation**.

Selecione **Salvar API configurada**.

![Armazenamento do Azure](./images/ps5.png){zoomable="yes"}

Você deverá ver isso.

![Nova integração do Adobe I/O](./images/ps7.png){zoomable="yes"}

### API do Adobe Experience Platform

Selecione **+ Adicionar ao Projeto** e **API**.

![Armazenamento do Azure](./images/aep1.png){zoomable="yes"}

Selecione **Adobe Experience Platform** e escolha **API Experience Platform**. Selecione **Próximo**.

![Armazenamento do Azure](./images/aep2.png){zoomable="yes"}

Selecione **Próximo**.

![Armazenamento do Azure](./images/aep3.png){zoomable="yes"}

Em seguida, é necessário selecionar um perfil de produto que defina quais permissões estão disponíveis para essa integração.

Selecione **Adobe Experience Platform - Todos os usuários - PROD**.

Selecione **Salvar API configurada**.

![Armazenamento do Azure](./images/aep4.png){zoomable="yes"}

Você deverá ver isso.

![Nova integração do Adobe I/O](./images/aep5.png){zoomable="yes"}

### Nome do projeto

Clique no nome do projeto.

![Nova integração do Adobe I/O](./images/api13.png){zoomable="yes"}

Selecione **Editar Projeto**.

![Nova integração do Adobe I/O](./images/api14.png){zoomable="yes"}

Digite um nome amigável para a integração: `--aepUserLdap-- One Adobe tutorial`e selecione **Salvar**.

![Nova integração do Adobe I/O](./images/api15.png){zoomable="yes"}

A configuração do projeto do Adobe I/O foi concluída.

![Nova integração do Adobe I/O](./images/api16.png){zoomable="yes"}

## Próximas etapas

Ir para [Opção 1: configuração do Postman](./ex7.md){target="_blank"}

Ir para [Opção 2: configuração PostBuster](./ex8.md){target="_blank"}

Volte para [Introdução](./getting-started.md){target="_blank"}

Voltar para [Todos os módulos](./../../../overview.md){target="_blank"}