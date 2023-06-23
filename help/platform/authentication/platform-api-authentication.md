---
title: Autenticar e acessar APIs da Experience Platform
description: Saiba como acessar APIs da Adobe Experience Platform.
role: Developer
feature: API
jira: KT-3688
thumbnail: 28832.jpeg
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 13%

---

# Autenticar e acessar [!DNL Experience Platform] APIs

Saiba como começar a usar APIs do Adobe Experience Platform. Este tutorial o orienta pelo processo de criação de credenciais de autenticação e começa a fazer solicitações de API do Experience Platform.

## Criar um projeto no Console do Adobe Developer e exportar um ambiente do Postman{#export-integration-details-to-postman}

[[!DNL Postman]](https://www.postman.com/) O é um aplicativo de terceiros que ajuda os desenvolvedores a interagir de forma rápida e fácil com as APIs do Adobe Experience Platform.

[do console Adobe Developer](https://developer.adobe.com/console/home) **Detalhes de exportação do Postman** O recurso oferece uma maneira fácil de exportar os detalhes da conta necessários para acessar e interagir com APIs de Experience Platform em um único arquivo de ambiente do Postman, removendo a necessidade de copiar e colar valores do console do Adobe Developer no Postman.

>[!IMPORTANT]
>
>Para acessar o [Console do Adobe Developer](https://developer.adobe.com/console/home), você deve ser um [Administrador do sistema](https://helpx.adobe.com/enterprise/using/admin-roles.html) ou um [Desenvolvedor](https://helpx.adobe.com/enterprise/using/manage-developers.html#:~:text=Add%20developers%20to%20a%20single%20product%20profile&amp;text=In%20the%20Admin%20Console%2C%20navigate,in%20the%20upper%2Dright%20corner.) no [Adobe Admin Console](https://adminconsole.adobe.com).
>
> Depois de criar a credencial da API, um Administrador do sistema deve associá-la a uma função no Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?quality=12&learn=on)




## Gerar um token de acesso com o Postman{#generate-an-access-token-with-postman}

Use o [APIs de serviço do Adobe Identity Management](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) para obter um token de acesso para acessar as APIs do Adobe Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)


## Interagir com APIs Experience Platform usando o Postman

Explore a interação com as APIs do Adobe Experience Platform usando o [Coleções de Postman da API de Experience Platform fornecida por Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform), com base no [Variáveis de ambiente do console do Adobe Developer](#export-integration-details-to-postman) e [token de acesso gerado](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?quality=12&learn=on)


## Recursos referenciados nestes vídeos

* [Console do desenvolvedor da Adobe](https://developer.adobe.com/console/home)
* [Exemplos do Adobe Experience Platform Postman](https://github.com/adobe/experience-platform-postman-samples)
   * [Identity Management System Postman Collection para gerar tokens de acesso](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Coleções Postman da API do Adobe Experience Platform](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Baixar o Postman](https://www.postman.com/)
