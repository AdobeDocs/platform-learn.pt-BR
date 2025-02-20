---
title: Autenticar e acessar APIs da Experience Platform
description: Saiba como acessar APIs da Adobe Experience Platform.
feature: API
role: Developer
level: Beginner
jira: KT-3688
thumbnail: 28832.jpeg
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 10%

---

# Autenticar e acessar [!DNL Experience Platform] APIs

Saiba como começar a usar APIs do Adobe Experience Platform. Este tutorial o orienta pelo processo de criação de credenciais de autenticação e pelo início da criação de solicitações de API do Experience Platform.

## Criar um projeto no Adobe Developer Console e exportar um ambiente do Postman{#export-integration-details-to-postman}

[[!DNL Postman]](https://www.postman.com/) é um aplicativo de terceiros que ajuda desenvolvedores a interagir rápida e facilmente com APIs do Adobe Experience Platform.

O recurso [Exportar Detalhes para Postman **do ](https://developer.adobe.com/console/home)** do Adobe Developer Console fornece uma maneira fácil de exportar os detalhes da conta necessários para acessar e interagir com uma APIs do Experience Platform em um único arquivo de Ambiente do Postman, eliminando a necessidade de copiar e colar valores do Adobe Developer Console no Postman.

>[!IMPORTANT]
>
>Para acessar o [Adobe Developer Console](https://developer.adobe.com/console/home), você deve ser um [Administrador do Sistema](https://helpx.adobe.com/br/enterprise/using/admin-roles.html) ou um [Desenvolvedor](https://helpx.adobe.com/enterprise/using/manage-developers.html#:~:text=Add%20developers%20to%20a%20single%20product%20profile&amp;text=In%20the%20Admin%20Console%2C%20navigate,in%20the%20upper%2Dright%20corner.) no [Adobe Admin Console](https://adminconsole.adobe.com).
>
> Depois de criar a credencial da API, um Administrador do sistema deve associá-la a uma função no Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on&enablevpops)

## Gerar um token de acesso com o Postman{#generate-an-access-token-with-postman}

Use as [APIs de serviço do Adobe Identity Management](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) para obter um token de acesso para acessar as APIs do Adobe Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?learn=on&enablevpops)


## Interagir com APIs do Experience Platform usando o Postman

Explore a interação com as APIs do Adobe Experience Platform usando as [coleções do Postman da API do Experience Platform fornecidas pela Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform), com base nas [Variáveis de ambiente do Adobe Developer Console](#export-integration-details-to-postman) e no [token de acesso gerado](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?learn=on&enablevpops)


## Recursos referenciados nestes vídeos

* [Console do desenvolvedor da Adobe](https://developer.adobe.com/console/home)
* [Exemplos do Adobe Experience Platform Postman](https://github.com/adobe/experience-platform-postman-samples)
   * [Coleção do Identity Management System Postman para geração de tokens de acesso](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Coleções de API Postman do Adobe Experience Platform](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Baixar Postman](https://www.postman.com/)
