---
title: Assimilar e analise dados do Google Analytics no Adobe Experience Platform com o Conector de Source do BigQuery - Crie sua conta da Google Cloud Platform
description: Assimilar e analise dados do Google Analytics no Adobe Experience Platform com o Conector de Source do BigQuery - Crie sua conta da Google Cloud Platform
kt: 5342
doc-type: tutorial
exl-id: 6dbfb5a3-adc2-4818-8f79-bbb00e56fbdf
source-git-commit: d6f6423adbc8f0ce8e20e686ea9ffd9e80ebb147
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---

# 4.2.1 Comece a usar a Google Cloud Platform

>[!NOTE]
>
>Para este exercício, você precisa acessar um ambiente da Google Cloud Platform. Se você ainda não tiver acesso ao GCP, crie uma nova conta usando seu endereço de email pessoal.

## 4.2.1.1 Por que conectar o Google BigQuery ao Adobe Experience Platform para obter dados do Google Analytics

O Google Cloud Platform (GCP) é um conjunto de serviços de computação em nuvem pública oferecidos pela Google. A Google Cloud Platform inclui uma variedade de serviços hospedados para computação, armazenamento e desenvolvimento de aplicativos que são executados em hardware da Google.

O BigQuery é um desses serviços e está sempre incluído no Google Analytics 360. Os dados do Google Analytics são frequentemente amostrados quando tentamos obter dados diretamente dele (API, por exemplo). É por isso que a Google inclui o BigQuery para obter dados não amostrados, de modo que as marcas podem fazer análise avançada usando SQL e se beneficiar do poder do GCP.

Os dados do Google Analytics são carregados diariamente no BigQuery usando um mecanismo em lote. Dessa forma, não faz sentido usar essa integração GCP/BigQuery para casos de uso de personalização e ativação em tempo real.

Se uma marca quiser fornecer casos de uso de personalização em tempo real com base em dados do Google Analytics, ela poderá coletar esses dados no site com o Google Tag Manager e transmiti-los para a Adobe Experience Platform em tempo real.

O Conector GCP/BigQuery Source deve ser usado para...

- rastreie todo o comportamento do cliente no site e carregue esses dados no Adobe Experience Platform para análise, ciência de dados e casos de uso de personalização que não exigem ativação em tempo real.
- carregar dados históricos do Google Analytics no Adobe Experience Platform, novamente para análise e casos de uso de ciência de dados

## 4.2.1.2 Sua conta da Google

>[!NOTE]
>
>Para este exercício, você precisa acessar um ambiente da Google Cloud Platform. Se você ainda não tiver acesso ao GCP, crie uma nova conta usando seu endereço de email pessoal.

## 4.2.1.3 Selecionar ou criar um projeto

Ir para [https://console.cloud.google.com/](https://console.cloud.google.com/).

Em seguida, clique em **Selecionar um projeto** ou clique em um projeto existente.

![demonstração](./images/ex12.png)

Se você ainda não tiver um projeto, clique em **NOVO PROJETO**. Se você já tiver um projeto, poderá optar por selecionar esse projeto e prosseguir para a próxima etapa.

![demonstração](./images/ex1createproject.png)

Nomeie o projeto seguindo esta convenção de nomenclatura. Clique em **CRIAR**.

| Convenção |
| ----------------- |
| `--aepUserLdap---googlecloud` |

![demonstração](./images/ex13.png)

Aguarde até que a notificação na parte superior direita da tela informe que a criação foi concluída. Em seguida, clique em **SELECIONAR PROJETO**.

![demonstração](./images/ex14.png)

Em seguida, vá para a barra de pesquisa na parte superior da tela e digite **BigQuery**. Selecione o primeiro resultado.

![demonstração](./images/ex17.png)

O objetivo desse módulo é obter dados do Google Analytics no Adobe Experience Platform. Para fazer isso, você precisa começar com dados fictícios em um conjunto de dados Google Analytics.

Clique em **+ Adicionar** e, em seguida, clique em **Conjuntos de dados públicos** no menu direito.

![demonstração](./images/ex118.png)

Você verá esta janela:

![demonstração](./images/ex119.png)

Insira o termo de pesquisa **Amostra de Google Analytics** na barra de pesquisa e clique no primeiro resultado da pesquisa.

![demonstração](./images/ex120.png)

Você verá a tela a seguir com uma descrição do conjunto de dados. Clique em **EXIBIR CONJUNTO DE DADOS**.

![demonstração](./images/ex121.png)

Você será redirecionado para o BigQuery, onde verá este conjunto de dados **bigquery-public-data** no **Explorer**.

![demonstração](./images/ex122a.png)

No **Explorer**, você deve ver várias tabelas. Sinta-se à vontade para explorá-los. Vá para `google_analytics_sample`.

![demonstração](./images/ex122.png)

Clique para abrir a tabela `ga_sessions`.

![demonstração](./images/ex123.png)

Antes de continuar com o próximo exercício, anote os seguintes itens em um arquivo de texto separado no seu computador:

| Credencial | Nomenclatura | Exemplo |
| ----------------- |-------------| -------------|
| Nome do projeto | `--aepUserLdap---googlecloud` | vangeluw-googlecloud |
| ID do projeto | random | possible-bee-447102-h3 |

Você pode encontrar seu Nome do Projeto e ID do Projeto clicando no **Nome do Projeto** na barra de menu superior:

![demonstração](./images/ex1projectMenu.png)

Em seguida, você verá sua ID do projeto no lado direito:

![demonstração](./images/ex1projetcselection.png)

Agora você pode ir para o próximo exercício onde você sujará as mãos consultando dados do Google Analytics.

Próxima etapa: [4.2.2 Crie sua primeira consulta no BigQuery](./ex2.md)

[Voltar ao módulo 4.2](./customer-journey-analytics-bigquery-gcp.md)

[Voltar a todos os módulos](./../../../overview.md)
