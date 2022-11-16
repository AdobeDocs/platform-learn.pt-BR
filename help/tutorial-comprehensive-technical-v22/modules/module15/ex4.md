---
title: Instale e configure o Kafka Connect e o Adobe Experience Platform Sink Connector
description: Instale e configure o Kafka Connect e o Adobe Experience Platform Sink Connector
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 6a7c91c2-bc92-4b9b-bd11-18cef86294d3
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 0%

---

# 15.4 Instale e configure o Kafka Connect e o conector do dissipador de tinta Adobe Experience Platform

## 15.4.1 Baixe o conector do dissipador de tinta Adobe Experience Platform

Ir para [https://github.com/adobe/experience-platform-streaming-connect/releases](https://github.com/adobe/experience-platform-streaming-connect/releases) e baixe a versão oficial mais recente do Adobe Experience Platform Sink Connector.

![Kafka](./images/kc1.png)

Coloque o arquivo de download, **streaming-connect-sink-0.0.14-java-11.jar** na área de trabalho.

![Kafka](./images/kc2.png)

## 15.4.2 Configurar o Kafka Connect

Vá para a pasta do seu desktop com o nome **Kafka_AEP** e navegue até a pasta `kafka_2.13-3.1.0/config`.
Nessa pasta, abra o arquivo **connect-distribution.properties** usando qualquer Editor de texto.

![Kafka](./images/kc3a.png)

No Editor de texto, vá para as linhas 34 e 35 e certifique-se de definir os campos `key.converter.schemas.enable` e `value.converter.schemas.enable` para `false`

```json
key.converter.schemas.enable=false
value.converter.schemas.enable=false
```

Salve as alterações neste arquivo.

![Kafka](./images/kc3.png)

Em seguida, volte para a pasta `kafka_2.13-3.1.0` e criar manualmente uma nova pasta e nomeá-la `connectors`.

![Kafka](./images/kc4.png)

Clique com o botão direito do mouse na pasta e clique em **Novo terminal na Pasta**.

![Kafka](./images/kc5.png)

Você verá isso. Digite o comando `pwd` para recuperar o caminho completo para essa pasta. Selecione o caminho completo e copie-o para a área de transferência.

![Kafka](./images/kc6.png)

Volte para o Editor de texto, para o arquivo **connect-distribution.properties** e role para baixo até a última linha (linha 86 na captura de tela). Você deve remover o comentário da linha que começa com `# plugin.path=` e você deve colar o caminho completo para a pasta nomeada `connectors`. O resultado deve ser semelhante a este:

`plugin.path=/Users/woutervangeluwe/Desktop/Kafka_AEP/kafka_2.13-3.1.0/connectors`

Salve as alterações no arquivo **connect-distribution.properties** e feche o Editor de texto.

![Kafka](./images/kc7.png)

Em seguida, copie a versão oficial mais recente do Adobe Experience Platform Sink Connector que você baixou na pasta de nome `connectors`. O arquivo que você baixou antes é nomeado como **streaming-connect-sink-0.0.14-java-11.jar**, basta movê-lo para o `connectors` pasta.

![Kafka](./images/kc8.png)

Em seguida, abra uma nova janela do Terminal no nível da **kafka_2.13-3.1.0** pasta. Clique com o botão direito do mouse nessa pasta e clique em **Novo terminal na pasta**.

Na janela Terminal, cole este comando: `bin/connect-distributed.sh config/connect-distributed.properties` e clique em **Enter**. Este comando iniciará o Kafka Connect e carregará a biblioteca do Adobe Experience Platform Sink Connector.

![Kafka](./images/kc9.png)

Após alguns segundos, você verá algo como isto:

![Kafka](./images/kc10.png)

## 15.4.3 Criar o conector do link do Adobe Experience Platform usando o Postman

Agora você pode interagir com o Kafka Connect usando o Postman. Para fazer isso, baixe [esta coleção da Postman](../../assets/postman/postman_kafka.zip) e descompacte-o no computador local na área de trabalho. Em seguida, você terá um arquivo chamado `Kafka_AEP.postman_collection.json`.

![Kafka](./images/kc11a.png)

É necessário importar esse arquivo no Postman. Para fazer isso, abra o Postman, clique em **Importar**, arraste e solte o arquivo `Kafka_AEP.postman_collection.json` na janela pop-up e clique em **Importar**.

![Kafka](./images/kc11b.png)

Em seguida, você encontrará essa coleção no menu esquerdo do Postman. Clique na primeira solicitação, **Conectores Kafka disponíveis para o GET** para abri-lo.

![Kafka](./images/kc11c.png)

Você verá isso. Clique no azul **Enviar** , após o que você deve ver uma resposta vazia `[]`. A resposta vazia é devido ao fato de que nenhum conector Kafka Connect está definido no momento.

![Kafka](./images/kc11.png)

Para criar um conector, clique em para abrir a segunda solicitação na coleção Kafka, **POST - Criar conector de link AEP**. Você verá isso. Na linha 11, onde diz **&quot;aep.endpoint&quot;: &quot;&quot;**, é necessário colar no URL do endpoint de Streaming da API HTTP que você recebeu no final do exercício [15,3](./ex3.md). O URL do ponto de extremidade de Transmissão da API HTTP tem esta aparência: `https://dcs.adobedc.net/collection/d282bbfc8a540321341576275a8d052e9dc4ea80625dd9a5fe5b02397cfd80dc`.

![Kafka](./images/kc12a.png)

Depois de colá-la, o corpo da solicitação deve ficar assim. Clique no azul **Enviar** para criar o conector. Você obterá uma resposta imediata da criação do seu conector.

![Kafka](./images/kc12.png)

Clique na primeira solicitação, **Conectores Kafka disponíveis para o GET** para abri-la novamente e clicar no botão azul **Enviar** novamente. agora você verá que um conector Kafka Connect foi criado.

![Kafka](./images/kc13.png)

Em seguida, abra a terceira solicitação na coleção Kafka, **GET Verificar Status do Conector Kafka Connect**. Clique no azul **Enviar** , você receberá uma resposta como a abaixo, informando que o conector está funcionando.

![Kafka](./images/kc14.png)

## 15.4.4 Produzir um evento de experiência

Abra um novo **Terminal** clicando com o botão direito do mouse em sua pasta **kafka_2.13-3.1.0** e clicando em **Novo terminal na pasta**.

![Kafka](./images/kafka11.png)

Digite o seguinte comando:

`bin/kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic aep`

![Kafka](./images/kc15.png)

Você verá isso. Cada nova linha seguida do botão Inserir resultará no envio de uma nova mensagem para o tópico **aep**.

![Kafka](./images/kc16.png)

Agora você pode enviar uma mensagem que resultará no consumo do Adobe Experience Platform Sink Connector e que será assimilada no Adobe Experience Platform em tempo real.

Vamos fazer uma pequena demonstração para testar isto.

Ir para [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Depois de fazer logon com sua Adobe ID, você verá isso. Clique no projeto do seu site para abri-lo.

![DSN](../module0/images/web8.png)

No **Telas** página, clique em **Executar**.

![DSN](../module1/images/web2.png)

Você verá seu site de demonstração aberto. Selecione o URL e copie-o para a área de transferência.

![DSN](../module0/images/web3.png)

Abra uma nova janela incógnita do navegador.

![DSN](../module0/images/web4.png)

Cole o URL do site de demonstração, que você copiou na etapa anterior. Em seguida, você será solicitado a fazer logon usando sua Adobe ID.

![DSN](../module0/images/web5.png)

Selecione o tipo de conta e conclua o processo de logon.

![DSN](../module0/images/web6.png)

Você verá seu site carregado em uma janela incógnita do navegador. Para cada demonstração, você precisará usar uma nova janela incógnita do navegador para carregar o URL do site de demonstração.

![DSN](../module0/images/web7.png)

Clique no ícone do logotipo do Adobe no canto superior esquerdo da tela para abrir o Visualizador de perfil.

![Demonstração](../module2/images/pv1.png)

Consulte o painel Visualizador de perfil e o Perfil do cliente em tempo real com a **Experience Cloud ID** como o identificador principal para este cliente atualmente desconhecido.

![Demonstração](../module2/images/pv2.png)

Vá para a página Registrar/fazer logon . Clique em **CRIAR UMA CONTA**.

![Demonstração](../module2/images/pv9.png)

Preencha os detalhes e clique em **Registrar** depois disso, você será redirecionado para a página anterior.

![Demonstração](../module2/images/pv10.png)

Abra o painel Visualizador de perfil e acesse Perfil do cliente em tempo real. No painel Visualizador de perfil, você deve ver todos os seus dados pessoais exibidos, como o email e os identificadores de telefone adicionados recentemente.

![Demonstração](../module2/images/pv11.png)

Você pode ver alguns eventos de experiência com base na atividade anterior.

![Kafka](./images/kc19.png)

Vamos mudar isso e enviar um evento de experiência do Callcenter de Kafka para o Adobe Experience Platform.

Pegue a carga do evento de experiência de amostra abaixo e copie-a em um Editor de texto.

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
      "timestamp": "2022-02-23T09:54:12.232Z",
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

Você verá isso. Você precisa atualizar manualmente dois campos:

- **_id**: por favor, defina-o para uma id aleatória, algo como `--demoProfileLdap--1234`
- **timestamp**: atualizar o carimbo de data e hora para a data e hora atuais
- **phoneNumber**: digite phoneNumber da conta que acabou de ser criada no site de demonstração. Você pode encontrá-lo no painel Visualizador de perfil em **Identidades**.

Também é necessário verificar e atualizar esses campos:
- **datasetId**: é necessário copiar a ID do conjunto de dados para o sistema de demonstração do conjunto de dados - conjunto de dados do evento para o Call Center (Global v1.1)
- **imsOrgID**: sua ID organizacional IMS é `--aepImsOrgId--`

>[!NOTE]
>
>O campo **_id** precisa ser exclusiva para cada assimilação de dados. Se você gerar vários eventos, atualize o campo **_id** sempre para um novo valor exclusivo.

![Kafka](./images/kc20.png)

Você deve ter algo como isto:

![Kafka](./images/kc21.png)

Em seguida, copie o evento de experiência completa para a área de transferência. O espaço em branco de sua carga JSON precisa ser removido e usaremos uma ferramenta online para fazer isso. Ir para [http://jsonviewer.stack.hu/](http://jsonviewer.stack.hu/) para fazer isso.

![Kafka](./images/kc22.png)

Cole o evento de experiência no editor e clique em **Remover espaço em branco**.

![Kafka](./images/kc22a.png)

Em seguida, selecione todo o texto de saída e copie-o para a área de transferência.

![Kafka](./images/kc23.png)

Volte para a janela Terminal.

![Kafka](./images/kc16.png)

Cole o novo payload sem espaços em branco na janela Terminal e clique em **Enter**.

![Kafka](./images/kc23a.png)

Em seguida, retorne ao site de demonstração e atualize a página. Agora você deve ver um evento de experiência no seu perfil, em **Outros eventos**, como o abaixo:

![Kafka](./images/kc24.png)

>[!NOTE]
>
>Se desejar que as interações da central de atendimento apareçam no painel Visualizador de perfil , é necessário adicionar o rótulo abaixo e filtrar o projeto em [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects), acessando a guia **Visualizador de perfil**.

![Kafka](./images/kc25.png)

Terminou este exercício.

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao Módulo 15](./aep-apache-kafka.md)

[Voltar para todos os módulos](../../overview.md)
