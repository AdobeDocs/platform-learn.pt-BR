---
title: Autenticar e acessar APIs da Experience Platform
description: Saiba como acessar APIs da Adobe Experience Platform.
role: Developer
feature: API
kt: 3688
thumbnail: 28832.jpeg
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 10%

---

# Autenticar e acessar [!DNL Experience Platform] APIs

Para fazer chamadas para APIs do Adobe Experience Platform, primeiro você deve obter acesso a uma conta de desenvolvedor do Experience Platform.

Para obter instruções passo a passo sobre como obter acesso a uma conta de desenvolvedor, visite o [Tutorial de autenticação da API do Experience Platform](https://www.adobe.com/go/platform-api-authentication-en).

## Criar e exportar a API do Experience Platform para o Postman

[Postman](https://www.getpostman.com/) O é uma ferramenta que permite aos desenvolvedores interagir rápida e facilmente com as APIs do Adobe Experience Platform.

do console do Adobe Developer **Exportar detalhes do Postman** O recurso fornece uma maneira fácil de exportar todos os detalhes da conta necessários para acessar e interagir com uma API do Experience Platform em um único arquivo do Ambiente Postman, removendo a necessidade de copiar e colar valores do Console do Adobe Developer no Postman.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?quality=12&learn=on)

## Gerar um token de acesso com o Postman

Use o [APIs do serviço Adobe Identity Management](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) para obter um token de acesso para acessar as APIs do Adobe Experience Platform para uso não relacionado à produção

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

>[!WARNING]
>
> Conforme observado na coleção Adobe I/O Access Token Generation Postman , os métodos de geração indicados são adequados para uso não relacionado à produção. A assinatura local carrega uma biblioteca do JavaScript de um host de terceiros e a assinatura remota envia a chave privada para um serviço da Web de propriedade e operado pelo Adobe. Embora o Adobe não armazene essa chave privada, as chaves de produção nunca devem ser compartilhadas com ninguém.

## Interação com APIs do Adobe I/O usando Postman

Explore a interação com APIs do Adobe I/O usando o [Coleções de Postman da API do Experience Platform fornecidas pelo Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform), com base no [Variáveis de ambiente do Adobe I/O](#export-adobe-io-integration-details-to-postman) e [token de acesso gerado](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?quality=12&learn=on)

Observe que as coleções de Postman fornecidas pelo Adobe podem não existir para cada API do Adobe I/O, no entanto, as [Coleções Experience Platform API Postman](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform) O pode ser usado como um guia sobre como definir suas próprias coleções do Postman para esses casos de uso.

## Recursos adicionais

* [Console Adobe I/O](https://console.adobe.io)
* [Exemplos de Postman do Adobe Experience Platform](https://github.com/adobe/experience-platform-postman-samples)
   * [Coleção Postman de geração de token de acesso ao Adobe I/O](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [APIs do Adobe Experience Platform Coleções de Postman](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Baixar o Postman](https://www.getpostman.com/)
