---
title: Offer Decisioning - Teste sua decisão usando a API
description: Teste sua decisão usando a API
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 0091c31f-0b54-4d40-a82b-3bf688db8a1f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---

# 9.6 Teste sua decisão usando a API

## 9.6.1 Trabalhar com a API do Offer Decisioning usando o Postman

Baixar [esta coleção Postman para Offer Decisioning](./../../assets/postman/postman_offer-decisioning.zip) na área de trabalho e descompacte-a. Você terá isso:

![API OD](./images/unzip.png)

Agora você tem este arquivo na área de trabalho:

- [!UICONTROL _Módulo 14 - Decisioning Service.postman_collection.json]

Em [Exercício 3.3.3 - Autenticação Postman para o Adobe I/O](./../../modules/module3/ex3.md) você instalou o Postman. Você precisará usar o Postman novamente para este exercício.

Abra o Postman. Clique em **[!UICONTROL Importar]**.

![Nova integração do Adobe I/O](./images/postmanui.png)

Clique em **[!UICONTROL Upload de arquivos]**.

![Nova integração do Adobe I/O](./images/pm1.png)

Selecione o arquivo **[!UICONTROL _Módulo 14 - Decisioning Service.postman_collection.json]** e clique em **[!UICONTROL Abrir]**.

![Nova integração do Adobe I/O](./images/pm2.png)

Em seguida, você terá essa coleção disponível no Postman.

![Nova integração do Adobe I/O](./images/pm3.png)

Agora você tem tudo o que precisa no Postman para começar a interagir com o Adobe Experience Platform por meio das APIs.

### 9.6.1.1 Contêineres de lista

Clique em para abrir a solicitação **[!UICONTROL GET - Contêineres de lista]**.

Em **[!UICONTROL Params]**, você verá o seguinte:

- propriedade: `_instance.parentName==aepenablementfy22`

Nesse parâmetro, **[!UICONTROL aepenablementfy22]** é o nome da sandbox usada no Adobe Experience Platform. A sandbox que você deve usar é `--aepSandboxId--`. Substituir o texto **[!UICONTROL aepenablementfy22]** por `--aepSandboxId--`.

Depois de substituir o nome da sandbox, clique em **[!UICONTROL Enviar]**.

![API OD](./images/api2.png)

Esta é a resposta, que mostra o contêiner de oferta para a sandbox que você especificou. Copie o **[!UICONTROL instanceId do container]** conforme indicado abaixo e anote-o em um arquivo de texto no seu computador. Você precisará usar isso **[!UICONTROL instanceId do container]** para o próximo exercício!

![API OD](./images/api3.png)

### 9.6.1.2 Listar disposições

Clique em para abrir a solicitação **[!UICONTROL GET - Listar disposições]**. Clique em **[!UICONTROL Enviar]**.

![API OD](./images/api4.png)

Agora você está vendo todas as disposições disponíveis no contêiner de oferta. As disposições que você está vendo foram definidas na interface do usuário do Adobe Experience Platform, como você pode ver em [Exercício 9.1.3](./ex1.md).

![API OD](./images/api5.png)

### 9.6.1.3 Lista de regras de decisão

Clique em para abrir a solicitação **[!UICONTROL GET - Lista de regras de decisão]**. Clique em **[!UICONTROL Enviar]**.

![API OD](./images/api6.png)

Na resposta, você verá as Regras de decisão definidas na interface do usuário do Adobe Experience Platform, como pode ver em [Exercício 9.1.4](./ex1.md).

![API OD](./images/api7.png)

### 9.6.1.4 Lista de ofertas personalizadas

Clique em para abrir a solicitação **[!UICONTROL GET - Listar ofertas personalizadas]**. Clique em **[!UICONTROL Enviar]**.

![API OD](./images/api8.png)

Na resposta, você verá as Ofertas personalizadas definidas na interface do usuário do Adobe Experience Platform em [Exercício 9.2.1](./ex2.md).

![API OD](./images/api9.png)

### 9.6.1.5 Lista de ofertas de fallback

Clique em para abrir a solicitação **[!UICONTROL GET - Listar ofertas de fallback]**. Clique em **[!UICONTROL Enviar]**.

![API OD](./images/api10.png)

Na resposta, você verá a Oferta de fallback que você definiu na interface do usuário do Adobe Experience Platform em [Exercício 9.2.2](./ex2.md).

![API OD](./images/api11.png)

### 9.6.1.6 Listar coleções

Clique em para abrir a solicitação **[!UICONTROL GET - Listar coleções]**.

![API OD](./images/api12.png)

Na resposta, você verá a coleção que você definiu na interface do usuário do Adobe Experience Platform em [Exercício 9.2.3](./ex2.md).

![API OD](./images/api13.png)

### 9.6.1.7 Obter ofertas detalhadas para o perfil do cliente

Clique em para abrir a solicitação **[!UICONTROL POST - Obtenha ofertas detalhadas para o perfil do cliente]**. Essa solicitação é semelhante à anterior, mas retorna detalhes como URLs de imagem, texto etc.

![API OD](./images/api23.png)

Para essa solicitação, semelhante ao exercício anterior que tem requisitos semelhantes, é necessário fornecer os valores para **[!UICONTROL xdm:placementId]** e **[!UICONTROL xdm:activityId]** para recuperar os detalhes específicos da oferta para um cliente.

O campo **[!UICONTROL xdm:activityId]** precisa ser preenchida. Você pode recuperar isso na interface do usuário do Adobe Experience Platform, conforme indicado abaixo.

![API OD](./images/activityid.png)

O campo **[!UICONTROL xdm:placementId]** precisa ser preenchida. Você pode recuperar isso na interface do usuário do Adobe Experience Platform, conforme indicado abaixo. No exemplo abaixo, você pode ver o placementId da disposição **[!UICONTROL Web - Imagem]**.

![API OD](./images/placementid.png)

Ir para **[!UICONTROL Corpo]** e insira o endereço de email do cliente para o qual você deseja solicitar uma oferta. Clique em **[!UICONTROL Enviar]**.

![API OD](./images/api24.png)

Por fim, você verá o resultado de que tipo de oferta personalizada e quais ativos precisam ser exibidos para esse cliente.

![API OD](./images/api25.png)

Você concluiu este exercício.

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao Módulo 9](./offer-decisioning.md)

[Voltar para todos os módulos](./../../overview.md)
