---
title: Foundation - Perfil do cliente em tempo real - Criar um segmento - API
description: Foundation - Perfil do cliente em tempo real - Criar um segmento - API
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 3%

---

# 2.1.5 Criar um segmento - API

Neste exercício, você usará o Postman e o Adobe I/O para criar um segmento e armazenar os resultados dele como um conjunto de dados, utilizando as APIs da Adobe Experience Platform.

## Story

No Perfil do cliente em tempo real, todos os dados do perfil são mostrados junto com os dados do evento e as associações de segmento existentes. Os dados mostrados podem vir de qualquer lugar, de aplicativos Adobe e de soluções externas. Essa é a visualização mais eficiente no Adobe Experience Platform, o sistema de experiência de registro.

## 2.1.5.1 - Criar um segmento por meio da API da plataforma

Vá para o Postman.

Localize a coleção: **_Habilitação de Adobe Experience Platform**. Nesta coleção, você verá uma pasta **2. Segmentação**. Usaremos essas solicitações neste exercício.

![Segmentação](./images/pmdtl.png)

O que faremos a seguir é seguir todas as etapas necessárias para criar um segmento por meio da API. Vamos criar um segmento simples: &quot;**ldap** - Todas as Clientes do Sexo Feminino&quot;.

### Etapa 1 - Criar uma definição de segmento

Clique na solicitação chamada **Etapa 1 - Perfil: Criar Uma Definição De Segmento**.

![Segmentação](./images/s1_call.png)

Vá para a seção **Corpo** desta solicitação.

![Segmentação](./images/s1_body.png)

No **Corpo** desta solicitação, você verá o seguinte:

![Segmentação](./images/s1_bodydtl.png)

O idioma usado para esta solicitação é chamado Profile Query Language ou **PQL**.

Você pode encontrar mais informações e documentação sobre o PQL [aqui](https://experienceleague.adobe.com/docs/experience-platform/segmentation/pql/overview.html?lang=en).


Atenção: atualize a variável **nome** na solicitação abaixo substituindo o **ldap** pelo seu **ldap** específico.

```json
{
    "name" : "ldap - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "ldap",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

Depois de adicionar o **ldap** específico, o Corpo deve ser semelhante a:

```json
{
    "name" : "vangeluw - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "vangeluw",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

Você também deve verificar os campos **Cabeçalho** - da sua solicitação. Ir para **Cabeçalhos**. Você verá isto:

![Postman](./images/s1_h.png)

| Chave | Valor |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>É necessário especificar o nome da sandbox da Adobe Experience Platform que você está usando. Seu x-sandbox-name deve ser `--aepSandboxName--`.

Agora, clique no botão azul **Enviar** para criar o segmento e exibir os resultados.

![Segmentação](./images/s1_bodydtl_results.png)

Após essa etapa, você pode visualizar a definição do segmento na interface do usuário da Platform. Para verificar isso, faça logon no Adobe Experience Platform e vá para **Segmentos**.

![Segmentação](./images/s1_segmentdef.png)

### Etapa 2 - Criar um trabalho de POST do segmento

No exercício anterior, você criou um segmento _streaming_. Um segmento de transmissão avalia continuamente as qualificações em tempo real. O que você está fazendo aqui é criar um segmento de _lote_. O segmento em lote oferece uma visualização do que o segmento pode parecer em termos de qualificações, mas _isso não significa que o segmento foi realmente executado_. Atualmente, _ninguém se qualifica para este segmento_. Para fazer com que as pessoas se qualifiquem, o segmento em lote precisa ser executado, que é exatamente o que faremos aqui.

Agora vamos POST um Trabalho de segmento.

Vá para o Postman.

![Segmentação](./images/pmdtl.png)

Na sua coleção do Postman, clique na solicitação chamada **Etapa 2 - POST Trabalho de segmento** para abri-la.

![Segmentação](./images/s2_call.png)

Você também deve verificar os campos **Cabeçalho** - da sua solicitação. Ir para **Cabeçalhos**. Você verá isto:

![Postman](./images/s2headers.png)

| Chave | Valor |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>É necessário especificar o nome da sandbox da Adobe Experience Platform que você está usando. Seu x-sandbox-name deve ser `--aepSandboxName--`.

Clique no botão azul **Enviar**.

Você deve ver um resultado semelhante:

![Segmentação](./images/s2_call_response.png)

Este trabalho de segmento agora está em execução e isso pode levar algum tempo. Na Etapa 3, você poderá verificar o status desse trabalho.


### Etapa 3 - Status do trabalho do segmento do GET

Vá para o Postman.

![Segmentação](./images/pmdtl.png)

Na sua coleção do Postman, clique na solicitação chamada **Etapa 3 - Status do trabalho do segmento do GET**.

![Segmentação](./images/s3_call.png)

Você também deve verificar os campos **Cabeçalho** - da sua solicitação. Ir para **Cabeçalhos**. Você verá isto:

![Postman](./images/s3headers.png)

| Chave | Valor |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>É necessário especificar o nome da sandbox da Adobe Experience Platform que você está usando. Seu x-sandbox-name deve ser `--aepSandboxName--`.

Clique no botão azul **Enviar**.

Você deve ver um resultado semelhante:

![Segmentação](./images/s3_status.png)

Neste exemplo, o **status** do trabalho está definido como **EM FILA**.

Repita esta solicitação clicando no botão azul **Enviar** a cada dois minutos até que o **status** seja definido como **COM ÊXITO**.

![Segmentação](./images/s3_status_succeeded.png)

Assim que o status for **SUCCEEDED**, o trabalho do seu segmento será executado e os clientes agora estarão qualificados para o segmento.

Parabéns, você concluiu com êxito o exercício de Segmentação. Agora vamos ver como o Perfil do cliente em tempo real pode ser ativado em toda a empresa.

Próxima Etapa: [2.1.6 Veja você o Perfil de Cliente em Tempo Real em ação na Central de Atendimento](./ex6.md)

[Voltar ao módulo 2.1](./real-time-customer-profile.md)

[Voltar a todos os módulos](../../../overview.md)
