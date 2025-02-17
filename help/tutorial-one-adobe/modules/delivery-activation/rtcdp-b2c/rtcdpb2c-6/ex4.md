---
title: Instale e configure o Kafka Connect e o Adobe Experience Platform Sink Connector
description: Instale e configure o Kafka Connect e o Adobe Experience Platform Sink Connector
kt: 5342
doc-type: tutorial
exl-id: 51ddfdfc-fa5c-4bf4-bfc2-b4a88b0b8a4d
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 0%

---

# 2.6.4 Instale e configure o Kafka Connect e o Conector do dissipador do Adobe Experience Platform

## Baixar o Conector do coletor Adobe Experience Platform

Acesse [https://github.com/adobe/experience-platform-streaming-connect/releases](https://github.com/adobe/experience-platform-streaming-connect/releases) e baixe a versão oficial mais recente do Adobe Experience Platform Sink Connector.

![Kafka](./images/kc1.png)

Baixe o arquivo **streaming-connect-sink-0.0.27-java-11.jar**.

![Kafka](./images/kc1a.png)

Coloque o arquivo de download, **streaming-connect-sink-0.0.27-java-11.jar**, no desktop.

![Kafka](./images/kc2.png)

## Configurar o Kafka Connect

Vá para a pasta na sua área de trabalho chamada **Kafka_AEP** e navegue até a pasta `kafka_2.13-3.9.0/config`.
Nessa pasta, abra o arquivo **connect-distribut.properties** usando qualquer Editor de Texto.

![Kafka](./images/kc3a.png)

No Editor de Texto, vá para as linhas 34 e 35 e certifique-se de definir os campos `key.converter.schemas.enable` e `value.converter.schemas.enable` como `false`

```json
key.converter.schemas.enable=false
value.converter.schemas.enable=false
```

Salve as alterações neste arquivo.

![Kafka](./images/kc3.png)

Em seguida, volte para a pasta `kafka_2.13-3.1.0` e crie manualmente uma nova pasta e a nomeie como `connectors`.

![Kafka](./images/kc4.png)

Clique com o botão direito na nova pasta e clique em **Novo terminal na Pasta**.

![Kafka](./images/kc5.png)

Você verá isso. Digite o comando `pwd` para recuperar o caminho completo dessa pasta. Selecione o caminho completo e copie-o para a área de transferência.

![Kafka](./images/kc6.png)

Volte para o Editor de Texto, para o arquivo **connect-distribution.properties** e role para baixo até a última linha (linha 89 na captura de tela). Você deve remover o comentário da linha (remover `#`) que começa com `# plugin.path=` e colar o caminho completo na pasta chamada `connectors`. O resultado deve ser semelhante a este:

`plugin.path=/Users/woutervangeluwe/Desktop/Kafka_AEP/kafka_2.13-3.9.0/connectors`

Salve as alterações no arquivo **connect-distribut.properties** e feche o Editor de Texto.

![Kafka](./images/kc7.png)

Em seguida, copie a versão oficial mais recente do Adobe Experience Platform Sink Connector que você baixou para a pasta chamada `connectors`. O arquivo que você baixou antes se chama **streaming-connect-sink-0.0.27-java-11.jar**. Basta movê-lo para a pasta `connectors`.

![Kafka](./images/kc8.png)

Em seguida, abra uma nova janela Terminal no nível da pasta **kafka_2.13-3.9.0**. Clique com o botão direito nessa pasta e clique em **Novo Terminal na Pasta**.

Na janela Terminal, cole este comando: `bin/connect-distributed.sh config/connect-distributed.properties` e clique em **Enter**. Este comando iniciará o Kafka Connect e carregará a biblioteca do Adobe Experience Platform Sink Connector.

![Kafka](./images/kc9.png)

Após alguns segundos, você verá algo assim:

![Kafka](./images/kc10.png)

## Criar seu Conector do Adobe Experience Platform Sink usando o Postman

Agora você pode interagir com o Kafka Connect usando o Postman. Para fazer isso, baixe [esta coleção do Postman](./../../../../assets/postman/postman_kafka.zip) e descompacte-a no computador local na área de trabalho. Você terá um arquivo chamado `Kafka_AEP.postman_collection.json`.

![Kafka](./images/kc11a.png)

Você precisa importar esse arquivo no Postman. Para fazer isso, abra o Postman, clique em **Importar**, arraste e solte o arquivo `Kafka_AEP.postman_collection.json` no pop-up e clique em **Importar**.

![Kafka](./images/kc11b.png)

Você encontrará essa coleção no menu esquerdo do Postman. Clique na primeira solicitação, **Conectores do GET Available Kafka Connect**, para abri-la.

![Kafka](./images/kc11c.png)

Você verá isso. Clique no botão azul **Enviar**, após o qual você deverá ver uma resposta vazia `[]`. A resposta vazia se deve ao fato de que nenhum conector Kafka Connect está definido no momento.

![Kafka](./images/kc11.png)

Para criar um conector, clique para abrir a segunda solicitação na coleção Kafka, **PÓS Criar Conector de Coletor AEP** e vá para **Corpo**. Você verá isso. Na linha 11, onde diz **&quot;aep.endpoint&quot;: &quot;&quot;**, é necessário colar na URL do ponto de extremidade de transmissão da API HTTP recebida ao final de um dos exercícios anteriores. A URL do ponto de extremidade de Streaming da API HTTP tem esta aparência: `https://dcs.adobedc.net/collection/63751d0f299eeb7aa48a2f22acb284ed64de575f8640986d8e5a935741be9067`.

![Kafka](./images/kc12a.png)

Depois de colá-lo, o corpo da solicitação deve ter esta aparência. Clique no botão azul **Enviar** para criar seu conector. Você receberá uma resposta imediata da criação do conector.

![Kafka](./images/kc12.png)

Clique na primeira solicitação, **Conectores do GET Available Kafka Connect**, para abri-lo novamente e clique novamente no botão azul **Enviar**. agora você verá que existe um conector Kafka Connect.

![Kafka](./images/kc13.png)

Em seguida, abra a terceira solicitação da coleção Kafka, **GET Check Kafka Connect Connector Status**. Clique no botão azul **Enviar** para obter uma resposta como a abaixo, informando que o conector está em execução.

![Kafka](./images/kc14.png)

## Produzir um evento de experiência

Abra uma nova janela do **Terminal** clicando com o botão direito do mouse na sua pasta **kafka_2.13-3.9.0** e clicando em **Novo Terminal na Pasta**.

![Kafka](./images/kafka11.png)

Digite o seguinte comando:

`bin/kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic aep`

Você verá isso. Cada nova linha seguida do pressionamento do botão Enter resultará no envio de uma nova mensagem para o tópico **aep**.

![Kafka](./images/kc16.png)

Agora você pode enviar uma mensagem, que resultará no consumo pelo Adobe Experience Platform Sink Connector e que será assimilada no Adobe Experience Platform em tempo real.

Pegue a carga útil do evento de experiência de amostra abaixo e copie-a em um Editor de texto.

```json
{
  "header": {
    "datasetId": "61fe23fd242870194a6d779c",
    "imsOrgId": "--aepImsOrgID--",
    "source": {
      "name": "Launch"
    },
    "schemaRef": {
      "id": "https://ns.adobe.com/experienceplatform/schemas/b0190276c6e1e1e99cf56c99f4c07a6e517bf02091dcec90",
      "contentType": "application/vnd.adobe.xed-full+json;version=1"
    }
  },
  "body": {
    "xdmMeta": {
      "schemaRef": {
        "id": "https://ns.adobe.com/experienceplatform/schemas/b0190276c6e1e1e99cf56c99f4c07a6e517bf02091dcec90",
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
      }
    },
    "xdmEntity": {
      "eventType": "callCenterInteractionKafka",
      "_id": "",
      "timestamp": "2024-11-25T09:54:12.232Z",
      "_experienceplatform": {
        "identification": {
          "core": {
            "phoneNumber": ""
          }
        },
        "interactionDetails": {
          "core": {
            "callCenterAgent": {
              "callID": "Support Contact - 3767767",
              "callTopic": "contract",
              "callFeeling": "negative"
            }
          }
        }
      }
    }
  }
}
```

Você verá isso. É necessário atualizar manualmente dois campos:

- **_id**: defina-a como uma ID aleatória, algo como `--aepUserLdap--1234`
- **carimbo de data/hora**: atualize o carimbo de data/hora para a data e hora atuais
- **phoneNumber**: digite o phoneNumber da conta criada anteriormente no site de demonstração. Você pode encontrá-lo no painel Visualizador de perfis em **Identidades**.

Também é necessário verificar e talvez atualizar estes campos:

- **datasetId**: é necessário copiar a ID do conjunto de dados para o Sistema de demonstração do conjunto de dados - Conjunto de dados de evento para a Central de atendimento (Global v1.1)

![Kafka](./images/kc20ds.png)

- **imsOrgID**: sua ID de Organização IMS é `--aepImsOrgId--`

>[!NOTE]
>
>O campo **_id** precisa ser exclusivo para cada assimilação de dados. Se você produzir vários eventos, atualize o campo **_id** sempre para um valor novo e exclusivo.

Você deve ter algo assim:

![Kafka](./images/kc21.png)

Em seguida, copie o evento de experiência completa para a área de transferência. O espaço em branco da carga JSON precisa ser removido e uma ferramenta online será usada para fazer isso. Vá para [http://jsonviewer.stack.hu/](http://jsonviewer.stack.hu/) para fazer isso.

Cole o evento de experiência no editor e clique em **Remover espaço em branco**.

![Kafka](./images/kc22a.png)

Em seguida, selecione todo o texto de saída e copie-o para a área de transferência.

![Kafka](./images/kc23.png)

Volte para a janela do Terminal.

![Kafka](./images/kc16.png)

Cole o novo conteúdo sem espaços em branco na janela do Terminal e clique em **Enter**.

![Kafka](./images/kc23a.png)

Em seguida, volte para o site de demonstração e atualize a página. Agora você deve ver um evento de experiência no seu perfil, em **Eventos de Experiência**, exatamente como o abaixo:

![Kafka](./images/kc24.png)

>[!NOTE]
>
>Se você quiser que as interações da central de atendimento apareçam no painel Visualizador de Perfis, adicione o rótulo e o filtro abaixo em seu projeto em [https://dsn.adobe.com](https://dsn.adobe.com), acessando a guia **Visualizador de Perfis** e adicionando uma nova linha em **Eventos**, com estas variáveis:
>- **Rótulo de Tipo de Evento**: Interações da Central de Atendimento
>- **Filtro de Tipo de Evento**: callCenterInteractionKafka
>- **Título**: `--aepTenantId--.interactionDetails.core.callCenterAgent.callID`

![Kafka](./images/kc25.png)

Você concluiu este exercício.

## Próximas etapas

Ir para [Resumo e benefícios](./summary.md){target="_blank"}

Voltar para [Transmitir dados do Apache Kafka para o Adobe Experience Platform](./aep-apache-kafka.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
