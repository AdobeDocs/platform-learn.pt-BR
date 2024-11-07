---
title: Assimilar e analise dados do Google Analytics no Adobe Experience Platform com o Conector de Source do BigQuery - Crie sua conta da Google Cloud Platform
description: Assimilar e analise dados do Google Analytics no Adobe Experience Platform com o Conector de Source do BigQuery - Crie sua conta da Google Cloud Platform
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 1%

---

# 4.2.1 Criar sua conta da Google Cloud Platform

## Objetivos

- Criar sua conta da Google Cloud Platform
- Familiarize-se com o Console da Google Cloud Platform
- Criar e preparar seu projeto do BigQuery

## 4.2.1.1 Por que conectar o Google BigQuery ao Adobe Experience Platform para obter dados do Google Analytics

O Google Cloud Platform (GCP) é um conjunto de serviços de computação em nuvem pública oferecidos pela Google. A Google Cloud Platform inclui uma variedade de serviços hospedados para computação, armazenamento e desenvolvimento de aplicativos que são executados em hardware da Google.

O BigQuery é um desses serviços e está sempre incluído no Google Analytics 360. Os dados do Google Analytics são frequentemente amostrados quando tentamos obter dados diretamente dele (API, por exemplo). É por isso que a Google inclui o BigQuery para obter dados não amostrados, de modo que as marcas podem fazer análise avançada usando SQL e se beneficiar do poder do GCP.

Os dados do Google Analytics são carregados diariamente no BigQuery usando um mecanismo em lote. Dessa forma, não faz sentido usar essa integração GCP/BigQuery para casos de uso de personalização e ativação em tempo real.

Se uma marca quiser fornecer casos de uso de personalização em tempo real com base em dados do Google Analytics, ela poderá coletar esses dados no site com o Google Tag Manager e transmiti-los para a Adobe Experience Platform em tempo real.

O Conector GCP/BigQuery Source deve ser usado para...

- rastreie todo o comportamento do cliente no site e carregue esses dados no Adobe Experience Platform para análise, ciência de dados e casos de uso de personalização que não exigem ativação em tempo real.
- carregar dados históricos do Google Analytics no Adobe Experience Platform, novamente para análise e casos de uso de ciência de dados

## 4.2.1.2 Criar sua conta da Google

Para obter uma conta da Google Cloud Platform, você precisa de uma conta da Google.

## 4.2.1.3 Ativar a conta da Google Cloud Platform

Agora que você tem uma conta do Google, pode criar um ambiente da Google Cloud Platform. Para fazer isso, vá para [https://console.cloud.google.com/](https://console.cloud.google.com/).

Na próxima página, aceite os Termos e condições.

![demonstração](./images/ex1/1.png)

Em seguida, clique em **Selecionar um projeto**.

![demonstração](./images/ex1/2.png)

Clique em **NEW PROJECT**.

![demonstração](./images/ex1/createproject.png)

Nomeie o projeto seguindo esta convenção de nomenclatura:

| Convenção | Exemplo |
| ----------------- |-------------| 
| `--aepUserLdap---googlecloud` | delaigle-googlecloud |

![demonstração](./images/ex1/3.png)

Clique em **Criar**.

![demonstração](./images/ex1/3-1.png)

Aguarde até que a notificação na parte superior direita da tela informe que a criação foi concluída. Clique em **Exibir projeto**.

![demonstração](./images/ex1/4.png)

Em seguida, vá para a barra de pesquisa na parte superior da tela e digite **BigQuery**. Selecione o primeiro resultado.

![demonstração](./images/ex1/7.png)

Você será redirecionado para o Console do BigQuery e verá uma mensagem pop-up.

**Clique em Concluído**.

![demonstração](./images/ex1/5.png)

O objetivo desse módulo é obter dados do Google Analytics no Adobe Experience Platform. Para fazer isso, precisamos de dados fictícios em um conjunto de dados Google Analytics para começar.

Clique em **Adicionar Dados** no menu do lado esquerdo, seguido por um clique em **Explorar conjuntos de dados públicos**.

![demonstração](./images/ex1/18.png)

Você verá esta janela:

![demonstração](./images/ex1/19.png)

Insira o termo de pesquisa **Amostra de Google Analytics** na barra de pesquisa e selecione o primeiro resultado.

![demonstração](./images/ex1/20.png)

Você verá a tela a seguir com uma descrição do conjunto de dados. Clique em **EXIBIR CONJUNTO DE DADOS**.

![demonstração](./images/ex1/21.png)

Você será redirecionado para o BigQuery, onde verá este conjunto de dados **bigquery-public-data** no **Explorer**.

![demonstração](./images/ex1/22a.png)

No **Explorer**, você deve ver várias tabelas. Sinta-se à vontade para explorá-los. Vá para `google_analytics_sample`.

![demonstração](./images/ex1/22.png)

Clique para abrir a tabela `ga_sessions`.

![demonstração](./images/ex1/23.png)

Antes de continuar com o próximo exercício, anote os seguintes itens em um arquivo de texto separado no seu computador:

| Credencial | Nomenclatura | Exemplo |
| ----------------- |-------------| -------------|
| Nome do projeto | `--aepUserLdap---googlecloud` | vangeluw-googlecloud |
| ID do projeto | random | composto-tarefa-306413 |

Você pode encontrar seu Nome do Projeto e ID do Projeto clicando no **Nome do Projeto** na barra de menu superior:

![demonstração](./images/ex1/projectMenu.png)

Em seguida, você verá sua ID do projeto no lado direito:

![demonstração](./images/ex1/projetcselection.png)

Agora você pode migrar para o Exercício 12.2, no qual você suja as mãos consultando dados do Google Analytics.

Próxima etapa: [4.2.2 Crie sua primeira consulta no BigQuery](./ex2.md)

[Voltar ao módulo 4.2](./customer-journey-analytics-bigquery-gcp.md)

[Voltar a todos os módulos](./../../../overview.md)
