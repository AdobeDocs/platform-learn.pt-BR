---
title: Introdução ao Apache Kafka
description: Introdução ao Apache Kafka
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# 2.6.1 Introdução ao Apache Kafka

## 2.6.1.1 Introdução

Cada organização começa de uma maneira muito simples a partir de uma perspectiva de dados. O ecossistema de dados de uma organização começa com um sistema de origem e um destino. O sistema de origem envia dados para o sistema de destino, e é isso. Calma, não é?
Quem me dera que permanecesse assim tão simples. As organizações superam rapidamente essa configuração simples e o número de sistemas de origem e de destino aumenta rapidamente. Todas essas diferentes fontes e destinos precisam trocar dados entre si, e as coisas tornam-se rapidamente muito complexas.
Por exemplo, se uma organização tiver 4 origens e 6 destinos e todos esses aplicativos precisarem falar entre si, será necessário criar 24 integrações... Cada uma dessas integrações vem com suas próprias dificuldades:

- protocolo: como os dados são transportados (TCP, HTTP, REST, FTP ...)
- formato de dados: como os dados são analisados (binário, CSV, JSON, Parquet, ...)
- esquema de dados e evolução: qual é o modelo de dados e como ele evoluirá?

Além disso, cada vez que você conectar um sistema de origem a um sistema de destino, haverá uma carga maior nesses sistemas a partir dessa conexão.

Então, como você resolve isso? É aí que o Apache Kafka entra em cena. O Apache Kafka permite que uma organização dissocie fluxos de dados e sistemas, fornecendo um sistema de mensagens comum, distribuído e de alta taxa de transferência. Os sistemas do Source enviarão seus dados para o Apache Kafka e os sistemas de destino consumirão dados do Apache Kafka.

Pense em todos os tipos de fontes de dados que as empresas precisam gerenciar:

- eventos do site
- eventos de aplicativo móvel
- Eventos de PDV
- Dados de CRM
- dados da central de atendimento
- histórico de transações
- ...

Pense em todos os tipos de destinos que as empresas usam em seus ecossistemas e que todos podem precisar de dados desses sistemas de origem:

- CRM
- data lake
- sistema de email
- auditoria
- analytics
- ...

O Apache Kafka foi criado pela LinkedIn e agora é um projeto de código aberto mantido principalmente pela Confluent.
O Apache Kafka fornece uma arquitetura distribuída e resiliente que é tolerante a falhas. Ele pode ser dimensionado horizontalmente para centenas de corretores e pode ser dimensionado para milhões de mensagens por segundo. Ele oferece alto desempenho com latências inferiores a 10 ms, ideal para casos de uso em tempo real.

Alguns exemplos de casos de uso:

- Sistema de mensagens
- Rastreamento de atividades
- Coletar métricas de vários locais diferentes
- Coleta de logs de aplicativo
- Processamento de fluxo (com a API de fluxos Kafka ou o Spark)
- Dissociação das dependências do sistema
- Integração com Spark, Flink, Storm, Hadoop e muitas outras tecnologias do Big Data.

Por exemplo:

- O Netflix usa o Kafka para aplicar recomendações em tempo real enquanto você assiste programas de TV
- O Uber usa o Kafka para coletar dados de usuários, táxis e viagens em tempo real para calcular e prever a demanda e calcular o aumento de preços em tempo real
- O linkedIn usa o Kafka para evitar spam, coletar interações do usuário para fazer recomendações de conexão melhores em tempo real

Para todos esses casos de uso, o Kafka só é usado como mecanismo de transporte. O Kafka é realmente bom em mover dados entre aplicativos.

## 2.6.1.2 Terminologia de Kafka

### Mensagem

Uma mensagem é uma comunicação enviada por um sistema ao Kafka. Uma mensagem contém uma carga e uma carga contém elementos de dados. Por exemplo, um evento de experiência enviado por um site para o Adobe Experience Platform é considerado uma mensagem.

### Tópico, partições, deslocamentos

Um tópico é um fluxo específico de dados, semelhante a uma tabela em um banco de dados. Você pode ter quantos tópicos desejar e um tópico é identificado por seu nome. Os tópicos são divididos em partições. Cada partição é ordenada e cada mensagem em uma partição recebe uma ID incremental, que é chamada de **offset**. As mensagens são armazenadas em um tópico, em uma partição e são referenciadas usando um deslocamento. As mensagens são mantidas somente por um tempo limitado (o padrão é 1 semana). Depois que uma mensagem é gravada em uma partição, ela não pode mais ser alterada.

### Corretores

Um broker é semelhante a um servidor. Um cluster Kafka é composto por vários corretores (servidores). Cada agente é identificado com uma ID e contém determinadas partições de tópico.

### Replicação

Kafka é um sistema distribuído. Uma das coisas importantes de um sistema distribuído é que os dados são armazenados com segurança e, como tal, a replicação é necessária. Afinal, quando um broker (servidor) fica inativo, outro broker (servidor) ainda deve ser capaz de fornecer acesso a mensagens que foram inicialmente armazenadas no broker que ficou inativo. A replicação criará cópias de mensagens em vários corretores para garantir que nenhum dado seja perdido.

### Produtores

Como os dados são enviados para o Kafka? Esse é o papel de um produtor. Um produtor se conecta a um sistema de origem e pega os dados do sistema de origem e, em seguida, grava esses dados nos tópicos em partições. Com base na configuração do cluster Kafka, os produtores saberão automaticamente em qual agente e partição gravar. Em um sistema distribuído com vários corretores e estratégia de replicação, um produtor armazenará dados aleatoriamente em vários corretores, o que significa que ele fará o balanceamento de carga automaticamente.

### Chaves de mensagem

Os produtores podem optar por enviar uma chave com a mensagem. Uma chave pode ser qualquer sequência, número, etc. Se nenhuma chave for fornecida, uma mensagem será enviada aleatoriamente para os corretores. Se uma chave for enviada, todas as mensagens dessa chave sempre irão para a mesma partição. Uma chave de mensagem como tal é usada para solicitar mensagens com base em um campo específico.

### Consumidores

Os consumidores leem os dados de um tópico do Apache Kafka e, em seguida, compartilham esses dados com os sistemas de destino. Os consumidores sabem de qual corretor ler. Os dados são lidos por um consumidor em ordem, em cada partição. Os consumidores leem os dados em grupos de consumidores.

### Zookeeper

O ZooKeeper é essencialmente um serviço para sistemas distribuídos que oferece um armazenamento hierárquico de valores-chave, que é usado para fornecer um serviço de configuração distribuída, serviço de sincronização e registro de nomes para grandes sistemas distribuídos. O Zookeeper precisa estar em execução antes que você possa usar o Apache Kafka, e o Zookeeper é uma espécie de mestre de cerimônias para o Kafka, gerenciando serviços distribuídos no back-end enquanto o Kafka produz e consome eventos.

Você concluiu este exercício.

Próxima Etapa: [2.6.2 Instale e configure seu cluster Kafka](./ex2.md)

[Voltar ao módulo 2.6](./aep-apache-kafka.md)

[Voltar a todos os módulos](../../../overview.md)
