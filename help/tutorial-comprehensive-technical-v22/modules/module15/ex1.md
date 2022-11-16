---
title: Introdução ao Apache Kafka
description: Introdução ao Apache Kafka
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 7b600c79-03c5-46fc-9ac9-a15599608c35
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# 15.1 Introdução ao Apache Kafka

## 15.1.1 Introdução

Cada organização começa de uma maneira muito simples, a partir de uma perspectiva de dados. O ecossistema de dados de uma organização começa com um sistema de origem e um destino. O sistema de origem envia dados para o sistema de destino, e é isso. Fácil, certo?
Se pelo menos continuasse assim tão simples. As organizações superam rapidamente essa configuração simples e o número de sistemas de origem e de destino aumenta rapidamente. Todas essas diferentes fontes e destinos precisam trocar dados uns com os outros, e as coisas rapidamente se tornam muito complexas.
Por exemplo, se uma organização tiver 4 fontes e 6 destinos e todos esses aplicativos precisarem conversar uns com os outros, será necessário criar 24 integrações... Cada uma dessas integrações vem com suas próprias dificuldades:

- protocolo: como os dados são transportados (TCP, HTTP, REST, FTP, ...)
- formato de dados: como os dados são analisados (binário, CSV, JSON, Parquet, ...)
- schema de dados e evolução: qual é o modelo de dados e como ele evoluirá?

Além disso, sempre que você conectar um sistema de origem a um sistema de destino, haverá um aumento na carga desses sistemas a partir dessa conexão.

Então, como resolver isso? É aí que Apache Kafka entra na cena. O Apache Kafka permite que uma organização dissocie fluxos de dados e sistemas fornecendo um sistema comum de mensagens distribuídas de alta throughput. Os sistemas de origem enviarão seus dados para o Apache Kafka, e os sistemas de destino consumirão dados do Apache Kafka.

Pense em todos os tipos de fontes de dados que as empresas devem gerenciar:

- eventos do site
- eventos de aplicativo móvel
- Eventos POS
- Dados de CRM
- dados do callcenter
- histórico de transações
- ...

E pense em todos os tipos de destinos que as empresas usam em seu ecossistema, o que pode precisar de dados desses sistemas de origem:

- CRM
- lago de dados
- sistema de email
- auditoria
- analytics
- ...

O Apache Kafka foi criado pela LinkedIn e agora é um projeto de código aberto mantido principalmente pela Confluente.
O Apache Kafka oferece uma arquitetura distribuída e resiliente que é tolerante a falhas. Pode ser dimensionado horizontalmente para 100s de corretores e pode ser dimensionado para milhões de mensagens por segundo. Ele fornece alto desempenho com latências inferiores a 10 ms, o que é ideal para casos de uso em tempo real.

Alguns exemplos de caso de uso:

- Sistema de mensagens
- Rastreamento de atividade
- Coletar métricas de vários locais diferentes
- Coleta de registros de aplicativos
- Processamento de fluxo (com API Kafka Streams ou Spark)
- Desvinculação de dependências do sistema
- Integração com Spark, Flink, Storm, Hadoop e muitas outras tecnologias de Big Data.

Por exemplo:

- A Netflix usa o Kafka para aplicar recomendações em tempo real enquanto você assiste programas de TV
- O Uber usa o Kafka para coletar dados de usuários, táxis e viagens em tempo real para calcular e prever a demanda e calcular o aumento de preços em tempo real
- O linkedIn usa o Kafka para evitar spam, coletar interações do usuário para fazer recomendações de melhor conexão em tempo real

Para todos estes casos de uso, Kafka é usado apenas como um mecanismo de transporte. Kafka é realmente bom em mover dados entre aplicativos.

## 15.1.2 Terminologia Kafka

### Mensagem

Uma mensagem é uma comunicação enviada por um sistema para Kafka. Uma mensagem contém um payload e um payload contém elementos de dados. Por exemplo, um evento de experiência enviado por um site para o Adobe Experience Platform é considerado uma mensagem.

### Tópico, partições, deslocamentos

Um tópico é um fluxo específico de dados, semelhante a uma tabela em um banco de dados. Você pode ter quantos tópicos desejar e um tópico é identificado pelo nome. Os tópicos são divididos em partições. Cada partição é solicitada e cada mensagem dentro de uma partição recebe uma id incremental, que é chamada de **offset**. As mensagens são armazenadas em um tópico, em uma partição e são referenciadas usando um deslocamento. As mensagens são mantidas somente por um tempo limitado (o padrão é uma semana). Depois que uma mensagem é gravada em uma partição, ela não pode mais ser alterada.

### Corretores

Um broker é semelhante a um servidor. Um cluster Kafka é composto por vários corretores (servidores). Cada broker é identificado com uma ID e contém determinadas partições de tópico.

### Replicação

Kafka é um sistema distribuído. Uma das coisas importantes de um sistema distribuído é que os dados são armazenados com segurança e, como tal, a replicação é necessária. Afinal, quando um corretor (servidor) fica inativo, outro corretor (servidor) ainda deve ser capaz de fornecer acesso às mensagens que foram inicialmente armazenadas no corretor que ficou inativo. A replicação criará cópias de mensagens em vários corretores para garantir que nenhum dado seja perdido.

### Produtores

Como os dados são enviados para Kafka? Esse é o papel de um produtor. Um produtor se conecta a um sistema de origem, pega os dados do sistema de origem e grava esses dados em tópicos em partições. Com base na configuração do seu cluster Kafka, os produtores saberão automaticamente em qual corretor e partição gravar. Em um sistema distribuído com vários corretores e estratégia de replicação, um produtor armazenará dados aleatoriamente em vários corretores, o que significa que fará o balanceamento de carga automaticamente.

### Chaves de mensagem

Os produtores podem optar por enviar uma chave com a mensagem. Uma chave pode ser qualquer string, número, etc. Se não for fornecida qualquer chave, será enviada aleatoriamente uma mensagem aos corretores. Se uma chave for enviada, todas as mensagens para essa chave sempre serão enviadas para a mesma partição. Uma chave de mensagem, como tal, é usada para ordenar mensagens com base em um campo específico.

### Consumidores

Os consumidores leem dados de um tópico do Apache Kafka e compartilham esses dados com sistemas de destino. Os consumidores sabem de qual mediador ler. Os dados são lidos por um consumidor em ordem, dentro de cada partição. Os consumidores leem dados em grupos de consumidores.

### Guardião

O ZooKeeper é essencialmente um serviço para sistemas distribuídos que oferecem um armazenamento hierárquico de valores-chave, utilizado para fornecer um serviço de configuração distribuído, serviço de sincronização e registro de nomenclatura para grandes sistemas distribuídos. O Zookeeper precisa ser executado antes que você possa usar o Apache Kafka, e o Zookeeper é meio que o principal da cerimônia para Kafka, gerenciando serviços distribuídos no back-end enquanto Kafka produz e consome eventos.

Terminou este exercício.

Próxima etapa: [15.2 Instalar e configurar seu cluster do Kafka](./ex2.md)

[Voltar ao Módulo 15](./aep-apache-kafka.md)

[Voltar para todos os módulos](../../overview.md)
