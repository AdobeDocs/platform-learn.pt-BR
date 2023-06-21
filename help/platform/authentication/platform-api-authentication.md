---
title: Autenticar e acessar APIs da Experience Platform
description: Saiba como acessar APIs da Adobe Experience Platform.
role: Developer
feature: API
kt: 3688
thumbnail: 28832.jpeg
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: 60f509ef55ce121f572466a8f13953dba982a0ce
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 15%

---

# Autenticar e acessar [!DNL Experience Platform] APIs

Para fazer solicitações às APIs do Adobe Experience Platform, você deve ter uma conta de desenvolvedor de Experience Platform.

## Criar um projeto no Console do Adobe Developer e exportar um ambiente do Postman

[[!DNL Postman]](https://www.postman.com/) O é uma ferramenta que permite aos desenvolvedores interagir rápida e facilmente com as APIs do Adobe Experience Platform.

do console Adobe Developer **Detalhes de exportação do Postman** O recurso oferece uma maneira fácil de exportar todos os detalhes da conta necessários para acessar e interagir com uma API Experience Platform em um único arquivo de ambiente do Postman, removendo a necessidade de copiar e colar valores do Adobe Developer Console no Postman.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?quality=12&learn=on)

>[!IMPORTANT]
>
>Depois de criar a credencial da API, um Administrador do sistema na empresa deve associar a credencial a uma função Experience Platform.


## Gerar um token de acesso com o Postman

Use o [APIs de serviço do Adobe Identity Management](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) para obter um token de acesso para acessar as APIs do Adobe Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)


## Interagir com APIs Experience Platform usando o Postman

Explore a interação com as APIs do Adobe Experience Platform usando o [Coleções de Postman da API de Experience Platform fornecida por Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform), com base no [Variáveis de ambiente do console do Adobe Developer](#export-adobe-io-integration-details-to-postman) e [token de acesso gerado](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?quality=12&learn=on)


## Recursos adicionais

* [Console do desenvolvedor da Adobe](https://developer.adobe.com/console/home)
* [Exemplos do Adobe Experience Platform Postman](https://github.com/adobe/experience-platform-postman-samples)
   * [Identity Management System Postman Collection para gerar tokens de acesso](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Coleções Postman da API do Adobe Experience Platform](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Baixar o Postman](https://www.postman.com/)
