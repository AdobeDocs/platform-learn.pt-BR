---
title: Coleta de dados do Adobe Experience Platform e encaminhamento lateral de evento em tempo real - Criar uma propriedade de encaminhamento de evento de coleta de dados do Adobe Experience Platform
description: Criar uma propriedade de encaminhamento de eventos de coleta de dados do Adobe Experience Platform
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 1%

---

# 2.5.1 Criar uma propriedade de encaminhamento de eventos de coleta de dados do Adobe Experience Platform

>[!NOTE]
>
>No momento, a extensão para dispositivos móveis do Adobe Experience Platform Edge está no BETA. O uso desta extensão é somente por convite. Entre em contato com o Gerente de sucesso do cliente do Adobe para obter mais informações e acesso aos materiais deste tutorial.

## 2.5.1.1 O que é uma propriedade de encaminhamento de eventos de coleta de dados do Adobe Experience Platform?

Normalmente, quando os dados são coletados usando a Coleção de dados da Adobe Experience Platform, eles são coletados no **Client Side**. O **Client Side** é um ambiente como um site ou um aplicativo para dispositivos móveis. No Módulo 0 e no Módulo 1, a configuração de uma propriedade do Adobe Experience Platform Data Collection Client foi discutida em profundidade e você implementou essa propriedade do Adobe Experience Platform Data Collection Client em seu site e aplicativo móvel, para que os dados pudessem ser coletados lá quando um cliente estivesse interagindo com o site e o aplicativo móvel.

Quando os dados de interação são coletados pela propriedade do Cliente de coleta de dados da Adobe Experience Platform, uma solicitação é enviada pelo site ou aplicativo móvel para o Adobe Edge. O Edge é um ambiente de coleta de dados de Adobe e é o ponto de entrada para dados de sequência de cliques no ecossistema de Adobe. Na Edge, esses dados coletados são enviados para aplicativos como Adobe Experience Platform, Adobe Analytics, Adobe Audience Manager ou Adobe Target.

Com a adição de uma propriedade de encaminhamento de eventos de coleta de dados do Adobe Experience Platform, agora é possível configurar uma propriedade de coleção de dados do Adobe Experience Platform que ouve dados recebidos na Edge. Quando a propriedade Encaminhamento de eventos de coleta de dados do Adobe Experience Platform que está em execução no Edge vê dados recebidos, ela pode usar esses dados e encaminhá-los para outro lugar. Esse outro lugar agora também pode ser um webhook externo não Adobe, o que torna possível enviar esses dados para, por exemplo, o data lake de escolha, um aplicativo de decisão ou qualquer outro aplicativo que tenha a capacidade de abrir um webhook.

A configuração de uma propriedade de encaminhamento de eventos de coleta de dados do Adobe Experience Platform parece familiar a uma propriedade do cliente, com a capacidade de configurar elementos de dados e regras como no passado com as propriedades do cliente de coleta de dados do Adobe Experience Platform. No entanto, a maneira como os dados serão acessados e usados será um pouco diferente, dependendo do caso de uso.

Vamos começar criando a propriedade de Encaminhamento de eventos da coleção de dados do Adobe Experience Platform.

## 2.5.1.2 Criar uma propriedade de encaminhamento de eventos de coleta de dados do Adobe Experience Platform

Ir para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). No menu esquerdo, clique em **Encaminhamento de Eventos**. Você verá uma visão geral de todas as propriedades disponíveis do Encaminhamento de eventos da coleção de dados da Adobe Experience Platform. Clique no botão **Nova propriedade**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/launchhome.png)

Agora é necessário inserir um nome para a propriedade de encaminhamento de eventos da coleção de dados da Adobe Experience Platform. Como uma convenção de nomenclatura, use `--aepUserLdap-- - Demo System (DD/MM/YYYY) (Edge)`. Por exemplo, neste exemplo, o nome é **vangeluw - Sistema de demonstração (22/02/2022) (Edge)**. Clique em **Salvar**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/ssf1.png)

Você voltará à lista de propriedades de Encaminhamento de eventos de coleta de dados do Adobe Experience Platform. Clique em para abrir a propriedade que você acabou de criar.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/ssf2.png)

## 2.5.1.2 Configurar a extensão do Adobe Cloud Connector

No menu esquerdo, vá para **Extensões**. Você verá que a extensão **Core** já está configurada.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/ssf3.png)

Ir para **Catálogo**. Você verá a extensão **Adobe Cloud Connector**. Clique em **Instalar** para instalá-lo.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/ssf4.png)

A extensão será adicionada. Não há configuração a ser feita nesta etapa. Você será redirecionado para a visão geral das extensões instaladas.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/ssf5.png)

## 2.5.1.3 Implante a propriedade de encaminhamento de eventos da coleta de dados do Adobe Experience Platform

No menu esquerdo, vá para **Fluxo de publicação**. Clique em **Adicionar biblioteca**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/ssf6.png)

Insira o nome **Principal**, selecione o ambiente **Desenvolvimento (desenvolvimento)** e clique em **+ Adicionar todos os recursos alterados**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/ssf7.png)

Você verá isso. Clique em **Salvar e criar para desenvolvimento**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/ssf8.png)

Sua biblioteca será criada, o que pode levar de 1 a 2 minutos.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/ssf9.png)

Por fim, sua biblioteca será criada e estará pronta.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/ssf10.png)

Próxima Etapa: [2.5.2 Atualize sua Sequência de Dados para disponibilizar os dados para sua propriedade de Encaminhamento de Eventos de Coleta de Dados](./ex2.md)

[Voltar ao módulo 2.5](./aep-data-collection-ssf.md)

[Voltar a todos os módulos](./../../../overview.md)
