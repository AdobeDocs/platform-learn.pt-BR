---
title: Real-time CDP - SDK de destinos
description: Real-time CDP - SDK de destinos
kt: 5342
doc-type: tutorial
exl-id: 5606ca2f-85ce-41b3-80f9-3c137f66a8c0
source-git-commit: 3a19e88e820c63294eff38bb8f699a9f690afcb9
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 6%

---

# 2.3.7 SDK de destinos

## Configurar o projeto do Adobe I/O

Neste exercício, você usará o Adobe I/O novamente para consultar as APIs da Adobe Experience Platform. Se você ainda não tiver configurado o projeto Adobe I/O, volte para o [Exercício 3 no Módulo 2.1](../module2.1/ex3.md) e siga as instruções lá.

## Autenticação Postman para Adobe I/O

Neste exercício, você usará o Postman novamente para consultar as APIs da Adobe Experience Platform. Se você ainda não tiver configurado seu aplicativo Postman, volte para o [Exercício 3 no Módulo 2.1](../module2.1/ex3.md) e siga as instruções lá.

## Definir ponto de extremidade e formato

Para este exercício, será necessário configurar um endpoint para que, quando um segmento se qualificar, o evento de qualificação possa ser transmitido para esse endpoint. Neste exercício, você usará um terminal de exemplo usando [https://webhook.site/](https://webhook.site/). Vá para [https://webhook.site/](https://webhook.site/), onde você verá algo semelhante a isto. Clique em **Copiar para a área de transferência** para copiar a url. Você precisará especificar esse url no próximo exercício. A URL neste exemplo é `https://webhook.site/e0eb530c-15b4-4a29-8b50-e40877d5490a`.

![Assimilação de dados](./images/webhook1.png)

Quanto ao formato, usaremos um modelo padrão que transmitirá as qualificações ou não qualificações do segmento junto com metadados como identificadores de clientes. Os modelos podem ser personalizados para atender às expectativas de endpoints específicos, mas neste exercício reutilizaremos um modelo padrão, o que resultará em uma carga como essa que será transmitida para o endpoint.

```json
{
  "profiles": [
    {
      "identities": [
        {
          "type": "ecid",
          "id": "64626768309422151580190219823409897678"
        }
      ],
      "AdobeExperiencePlatformSegments": {
        "add": [
          "f58c723c-f1e5-40dd-8c79-7bb4ab47f041"
        ],
        "remove": []
      }
    }
  ]
}
```

## Criar uma configuração de servidor e modelo

A primeira etapa para criar seu próprio Destino no Adobe Experience Platform é criar uma configuração de servidor e modelo.

Para fazer isso, vá para **API de criação de destino**, para **Servidores e modelos de destino** e clique para abrir a solicitação **POST - Criar uma configuração de servidor de destino**. Você verá isso. Em **Cabeçalhos**, é necessário atualizar manualmente o valor da chave **x-sandbox-name** e defini-lo como `--aepSandboxName--`. Selecione o valor **{{SANDBOX_NAME}}**.

![Assimilação de dados](./images/sdkpm1.png)

Substituir por `--aepSandboxName--`.

![Assimilação de dados](./images/sdkpm2.png)

Em seguida, vá para **Corpo**. selecione o espaço reservado **{{body}}**.

![Assimilação de dados](./images/sdkpm3.png)

Agora é necessário substituir o espaço reservado **{{body}}** pelo código abaixo:

```json
{
    "name": "Custom HTTP Destination",
    "destinationServerType": "URL_BASED",
    "urlBasedDestination": {
        "url": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "yourURL"
        }
    },
    "httpTemplate": {
        "httpMethod": "POST",
        "requestBody": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{\n    \"profiles\": [\n    {%- for profile in input.profiles %}\n        {\n            \"identities\": [\n            {%- for idMapEntry in profile.identityMap -%}\n            {%- set namespace = idMapEntry.key -%}\n                {%- for identity in idMapEntry.value %}\n                {\n                    \"type\": \"{{ namespace }}\",\n                    \"id\": \"{{ identity.id }}\"\n                }{%- if not loop.last -%},{%- endif -%}\n                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}\n            {% endfor %}\n            ],\n            \"AdobeExperiencePlatformSegments\": {\n                \"add\": [\n                {%- for segment in profile.segmentMembership.ups | added %}\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\n                {% endfor %}\n                ],\n                \"remove\": [\n                {#- Alternative syntax for filtering segments by status: -#}\n                {% for segment in removedSegments(profile.segmentMembership.ups) %}\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\n                {% endfor %}\n                ]\n            }\n        }{%- if not loop.last -%},{%- endif -%}\n    {% endfor %}\n    ]\n}"
        },
        "contentType": "application/json"
    }
}
```

Depois de colar o código acima, você precisa atualizar manualmente o campo **urlBasedDestination.url.value** e defini-lo para a url do webhook criado na etapa anterior, que era `https://webhook.site/e0eb530c-15b4-4a29-8b50-e40877d5490a` neste exemplo.

![Assimilação de dados](./images/sdkpm4.png)

Depois de atualizar o campo **urlBasedDestination.url.value**, ele deverá ter esta aparência. Clique em **Enviar**.

![Assimilação de dados](./images/sdkpm5.png)

Depois de clicar em **Enviar**, seu modelo de servidor será criado e, como parte da resposta, você verá um campo chamado **instanceId**. Anote-o, como você precisará dele na próxima etapa. Neste exemplo, a **instanceId** é
`eb0f436f-dcf5-4993-a82d-0fcc09a6b36c`.

![Assimilação de dados](./images/sdkpm6.png)

## Criar sua configuração de destino

No Postman, em **API de criação de destino**, vá para **Configurações de destino** e clique para abrir a solicitação **POST - Criar uma configuração de destino**. Você verá isso. Em **Cabeçalhos**, é necessário atualizar manualmente o valor da chave **x-sandbox-name** e defini-lo como `--aepSandboxName--`. Selecione o valor **{{SANDBOX_NAME}}**.

![Assimilação de dados](./images/sdkpm7.png)

Substituir por `--aepSandboxName--`.

![Assimilação de dados](./images/sdkpm8.png)

Em seguida, vá para **Corpo**. selecione o espaço reservado **{{body}}**.

![Assimilação de dados](./images/sdkpm9.png)

Agora é necessário substituir o espaço reservado **{{body}}** pelo código abaixo:

```json
{
    "name": "--aepUserLdap-- - Webhook",
    "description": "Exports segment qualifications and identities to a custom webhook via Destination SDK.",
    "status": "TEST",
    "customerAuthenticationConfigurations": [
        {
            "authType": "BEARER"
        }
    ],
    "customerDataFields": [
        {
            "name": "endpointsInstance",
            "type": "string",
            "title": "Select Endpoint",
            "description": "We could manage several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
            "isRequired": true,
            "enum": [
                "US",
                "EU",
                "APAC",
                "NZ"
            ]
        }
    ],
    "uiAttributes": {
        "documentationLink": "https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en",
        "category": "streaming",
        "connectionType": "Server-to-server",
        "frequency": "Streaming"
    },
    "identityNamespaces": {
        "ecid": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": false
        }
    },
    "segmentMappingConfig": {
        "mapExperiencePlatformSegmentName": true,
        "mapExperiencePlatformSegmentId": true,
        "mapUserInput": false
    },
    "aggregation": {
        "aggregationType": "BEST_EFFORT",
        "bestEffortAggregation": {
            "maxUsersPerRequest": "1000",
            "splitUserById": false
        }
    },
    "schemaConfig": {
        "profileRequired": false,
        "segmentRequired": true,
        "identityRequired": true
    },
    "destinationDelivery": [
        {
            "authenticationRule": "NONE",
            "destinationServerId": "yourTemplateInstanceID"
        }
    ]
}
```

![Assimilação de dados](./images/sdkpm11.png)

Depois de colar o código acima, é necessário atualizar manualmente o campo **destinationDelivery. destinationServerId**, e você precisa defini-lo como **instanceId** do modelo de servidor de destino que você criou na etapa anterior, que era `eb0f436f-dcf5-4993-a82d-0fcc09a6b36c` neste exemplo. Em seguida, clique em **Enviar**.

![Assimilação de dados](./images/sdkpm10.png)

Você verá essa resposta.

![Assimilação de dados](./images/sdkpm12.png)

Seu destino foi criado no Adobe Experience Platform. Vamos lá verificar.

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepSandboxName--``. Você pode fazer isso clicando no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. Depois de selecionar a [!UICONTROL sandbox] apropriada, você verá a alteração da tela e agora estará na [!UICONTROL sandbox] dedicada.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/sb1.png)

No menu esquerdo, vá para **Destinos**, clique em **Catálogo** e role para baixo até a categoria **Streaming**. Você verá seu destino disponível lá agora.

![Assimilação de dados](./images/destsdk1.png)

## Vincular o segmento ao destino

Em **Destinos** > **Catálogo**, clique em **Configurar** no seu destino para começar a adicionar segmentos ao seu novo destino.

![Assimilação de dados](./images/destsdk2.png)

Insira um token de portador fictício, como **1234**. Clique em **Conectar ao destino**.

![Assimilação de dados](./images/destsdk3.png)

Você verá isso. Como um nome para o seu destino, use `--aepUserLdap-- - Webhook`. Selecione um endpoint de escolha, neste exemplo **EU**. Clique em **Next**.

![Assimilação de dados](./images/destsdk4.png)

Opcionalmente, é possível selecionar uma política de governança de dados. Clique em **Next**.

![Assimilação de dados](./images/destsdk5.png)

Selecione o segmento criado anteriormente, chamado `--aepUserLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`. Clique em **Next**.

![Assimilação de dados](./images/destsdk6.png)

Você verá isso. Mapeie o **CAMPO DO SOURCE** `--aepTenantId--.identification.core.ecid` para o campo `Identity: ecid`. Clique em **Next**.

![Assimilação de dados](./images/destsdk7.png)

Clique em **Concluir**.

![Assimilação de dados](./images/destsdk8.png)

Seu destino agora está ativo, as novas qualificações de segmento serão transmitidas para seu webhook personalizado agora.

![Assimilação de dados](./images/destsdk9.png)

## Testar a ativação do segmento

Ir para [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Depois de fazer logon com sua Adobe ID, você verá isso. Clique no projeto do site para abri-lo.

![DSN](../../gettingstarted/gettingstarted/images/web8.png)

Agora você pode seguir o fluxo abaixo para acessar o site. Clique em **Integrações**.

![DSN](../../gettingstarted/gettingstarted/images/web1.png)

Na página **Integrações**, é necessário selecionar a propriedade Coleção de dados criada no exercício 0.1.

![DSN](../../gettingstarted/gettingstarted/images/web2.png)

Você verá seu site de demonstração aberto. Selecione o URL e copie-o para a área de transferência.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Abra uma nova janela incógnita do navegador.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Cole o URL do site de demonstração que você copiou na etapa anterior. Você será solicitado a fazer logon usando sua Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Selecione o tipo de conta e conclua o processo de logon.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Em seguida, você verá seu site carregado em uma janela incógnita do navegador. Para cada demonstração, será necessário usar uma janela do navegador nova e incógnita para carregar o URL do site de demonstração.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

Na página inicial do **Luma**, vá para **Men** e clique no produto **PROTEUS FITNESS JACKSHIRT**.

![Assimilação de dados](./images/homenadia.png)

Você agora visitou a página de produto do **PROTEUS FITNESS JACKSHIRT**, o que significa que agora você se qualificará para o segmento criado anteriormente neste exercício.

![Assimilação de dados](./images/homenadiapp.png)

Ao abrir o Visualizador de perfis e acessar **Segmentos**, você verá o segmento se qualificar.

![Assimilação de dados](./images/homenadiapppb.png)

Agora volte para o webhook aberto em [https://webhook.site/](https://webhook.site/), em que você deve ver uma nova solicitação de entrada, originada no Adobe Experience Platform e que contém o evento de qualificação de segmento.

![Assimilação de dados](./images/destsdk10.png)

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao módulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Voltar a todos os módulos](../../../overview.md)
