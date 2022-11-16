---
title: Foundation - Perfil do cliente em tempo real - Criar um segmento - API
description: Foundation - Perfil do cliente em tempo real - Criar um segmento - API
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 3f537efd-7281-4c0c-b809-97f266a2a337
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 3%

---

# 3.5 Criar um segmento - API

Neste exercício, você usará o Postman e o Adobe I/O para criar um segmento e armazenar os resultados desse segmento como um conjunto de dados, usando as APIs do Adobe Experience Platform.

## História

No Perfil do cliente em tempo real, todos os dados do perfil são mostrados junto aos dados do evento e às associações de segmento existentes. Os dados mostrados podem vir de qualquer lugar, de aplicativos Adobe e soluções externas. Essa é a exibição mais poderosa no Adobe Experience Platform, o sistema de experiência de registro.

## Exercício 3.5.1 - Criar um segmento por meio da API da plataforma

Vá para Postman.

Localize a coleção: **_Ativação Adobe Experience Platform**. Nesta coleção, você verá uma pasta **2. Segmentação**. Usaremos essas solicitações neste exercício.

![Segmentação](./images/pmdtl.png)

O que faremos em seguida é seguir todas as etapas necessárias para criar um segmento por meio da API. Vamos criar um segmento simples: &quot;**ldap** - Todas as clientes do sexo feminino&quot;.

### Etapa 1 - Criar uma definição de segmento

Clique na solicitação nomeada **Etapa 1 - Perfil: Criar Uma Definição De Segmento**.

![Segmentação](./images/s1_call.png)

Vá para a **Corpo** seção desta solicitação.

![Segmentação](./images/s1_body.png)

No **Corpo** dessa solicitação, você verá o seguinte:

![Segmentação](./images/s1_bodydtl.png)

O idioma usado para essa solicitação é chamado de Idioma da Consulta de Perfil, ou **PQL**.

Você pode encontrar mais informações e documentação sobre o PQL [here](https://experienceleague.adobe.com/docs/experience-platform/segmentation/pql/overview.html?lang=en).


Atenção: atualize a variável **name** na solicitação abaixo, substituindo **ldap** com seu **ldap**.

```json
{
    "name" : "ldap - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "ldap",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

Depois de adicionar o **ldap** O corpo deve ser semelhante a este:

```json
{
    "name" : "vangeluw - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "vangeluw",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

Você também deve verificar a variável **Cabeçalho** - campos da sua solicitação. Ir para **Cabeçalhos**. Você verá isso:

![Postman](./images/s1_h.png)

| Chave | Valor |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>Você precisa especificar o nome da sandbox do Adobe Experience Platform que está usando. Seu nome x-sandbox deve ser `--aepSandboxId--`.

Agora, clique no azul **Enviar** para criar o segmento e exibir os resultados disso.

![Segmentação](./images/s1_bodydtl_results.png)

Após esta etapa, você pode visualizar sua definição de segmento na interface do usuário da plataforma. Para verificar isso, faça logon no Adobe Experience Platform e acesse **Segmentos**.

![Segmentação](./images/s1_segmentdef.png)

### Etapa 2 - Criar um POST de segmento

No exercício anterior, você criou um _transmissão_ segmento. Um segmento de transmissão avalia continuamente as qualificações em tempo real. O que você está fazendo aqui é criar um _lote_ segmento. O segmento de lote fornece uma pré-visualização de como o segmento pode se parecer em termos de qualificações, mas _isso não significa que o segmento realmente foi executado_. Atualmente, _ninguém está qualificado para este segmento_. Para que as pessoas se qualifiquem, o segmento de lote precisa ser executado, que é exatamente o que faremos aqui.

Agora vamos POST de um trabalho de segmento.

Vá para Postman.

![Segmentação](./images/pmdtl.png)

Na coleção do Postman, clique na solicitação nomeada **Etapa 2 - Tarefa de segmento de POST** para abri-lo.

![Segmentação](./images/s2_call.png)

Você também deve verificar a variável **Cabeçalho** - campos da sua solicitação. Ir para **Cabeçalhos**. Você verá isso:

![Postman](./images/s2headers.png)

| Chave | Valor |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>Você precisa especificar o nome da sandbox do Adobe Experience Platform que está usando. Seu nome x-sandbox deve ser `--aepSandboxId--`.

Clique em azul **Enviar** botão.

Você deve ver um resultado semelhante:

![Segmentação](./images/s2_call_response.png)

Esse trabalho de segmento agora está em execução, e isso pode levar algum tempo. Na Etapa 3, você poderá verificar o status deste trabalho.


### Etapa 3 - Status do trabalho do segmento do GET

Vá para Postman.

![Segmentação](./images/pmdtl.png)

Na coleção do Postman, clique na solicitação nomeada **Etapa 3 - Status do trabalho do segmento do GET**.

![Segmentação](./images/s3_call.png)

Você também deve verificar a variável **Cabeçalho** - campos da sua solicitação. Ir para **Cabeçalhos**. Você verá isso:

![Postman](./images/s3headers.png)

| Chave | Valor |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>Você precisa especificar o nome da sandbox do Adobe Experience Platform que está usando. Seu nome x-sandbox deve ser `--aepSandboxId--`.

Clique em azul **Enviar** botão.

Você deve ver um resultado semelhante:

![Segmentação](./images/s3_status.png)

Neste exemplo, a variável **status** da tarefa estiver definida como **EM FILA**.

Repita essa solicitação clicando no botão azul **Enviar** a cada dois minutos até a **status** está definida como **SUCEDIDO**.

![Segmentação](./images/s3_status_succeeded.png)

Quando o status for **SUCEDIDO**, seu trabalho de segmento foi executado e os clientes agora estão qualificados para o segmento.

Parabéns, você concluiu com sucesso o exercício Segmentação . Agora vamos ver como o Perfil do cliente em tempo real pode ser ativado em toda a empresa.

Próxima etapa: [3.6 Veja você Perfil do cliente em tempo real em ação no Call Center](./ex6.md)

[Voltar ao Módulo 3](./real-time-customer-profile.md)

[Voltar para todos os módulos](../../overview.md)
