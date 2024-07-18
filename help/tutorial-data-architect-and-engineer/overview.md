---
title: Introdução à Adobe Experience Platform para arquitetos e engenheiros de dados
description: Introdução à Adobe Experience Platform para arquitetos e engenheiros de dados.
breadcrumb-title: Visão geral
role: Data Architect, Data Engineer
jira: KT-4348
thumbnail: 4348-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: fabbc591-840b-40dc-89af-305626a16338
source-git-commit: efef0389cedfec7dfa19d876df96c58b7463ee12
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# Introdução à Adobe Experience Platform para arquitetos e engenheiros de dados

<!--5min-->

_A Introdução à Adobe Experience Platform para Arquitetos de dados e Engenheiros de dados_ é o ponto de partida perfeito para se familiarizar com o Experience Platform.


<!--How do we address ETL-->

## Objetivos de aprendizagem

Os arquitetos de dados e os engenheiros de dados devem colaborar estreitamente para uma implantação bem-sucedida do Experience Platform. Este tutorial prático ensina as principais tarefas executadas por _ambas as funções_, para que você saiba como começar a implementar a Platform para sua própria empresa. Você será orientado por exercícios que apresentarão a terminologia, os recursos, a interface e as APIs principais do Experience Platform. Os clientes de aplicativos da Adobe Experience Cloud, como Real-time Customer Data Platform, Customer Journey Analytics e Journey Optimizer, também considerarão esse conteúdo útil, pois os serviços da plataforma são a base essencial desses aplicativos.

![Adobe Experience Cloud marketecture destacando os serviços da Platform abordados neste tutorial — identidade, perfil, segmentação, assimilação, consulta e governança](assets/marketecture.png)

Os tópicos incluem:

* Configuração de permissões de usuário
* Criação de sandboxes
* Configuração de um projeto do Developer Console e uso da API da plataforma
* Gerenciamento de dados — incluindo a criação de esquemas, conjuntos de dados, identidades, políticas de mesclagem e governança de dados
* Assimilação de dados usando modos de lote e fluxo
* Captura de dados da Web com o SDK da Web da Adobe Experience Platform
* Criação de perfis de clientes em tempo real
* Utilização do Serviço de consulta para validar dados e extrair dados
* Construção de segmentos

## Cenário de negócios

O Adobe Experience Platform é uma plataforma técnica projetada para ajudar você a atingir os objetivos de marketing. Os casos de uso de negócios devem orientar a maneira como você projeta e implementa a tecnologia. Este tutorial se concentra em uma marca fictícia de varejo chamada Luma. A Luma opera lojas tradicionais em vários países e também tem presença online com um site e aplicativos móveis. Eles estão investindo no Adobe Experience Platform para combinar dados de fidelidade, CRM, Web e compra offline em perfis de clientes em tempo real e ativar esses perfis para elevar o nível do marketing. Os objetivos de negócios da Luma podem ou não estar alinhados aos objetivos de sua empresa, mas você deve ser capaz de relacionar as etapas práticas deste tutorial a seus próprios objetivos de negócios.

## Pré-requisitos

* Você concluiu o curso [Introdução ao Adobe Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2020.1&amp;lang=pt-BR) no Experience League e está familiarizado com os recursos da plataforma
* Você tem acesso a uma conta provisionada com a Adobe Experience Platform (ou um aplicativo baseado na plataforma, como o Real-Time CDP ou o Journey Optimizer) e a Coleção de dados (antigo Launch).
* Você é um Administrador do Sistema dessa conta ou pode ter uma [configurar permissões de usuário](configure-permissions.md) para você.

## Usando este tutorial

Este tutorial combina tarefas para engenheiros de dados e arquitetos de dados. Como é um tutorial de nível introdutório, você deve ser capaz de concluir as tarefas para ambas as funções. Como muitas das lições se baseiam no que foi implementado nas lições anteriores, você deve percorrer as lições em ordem. Vou dizer quais lições podem ser ignoradas.

À medida que você cria vários elementos da Platform durante este tutorial, tente manter os nomes que eu recomendo o máximo possível. No entanto, há alguns nomes de elementos de alto nível que você pode querer personalizar, caso haja várias pessoas em sua organização fazendo este tutorial simultaneamente. Por exemplo, talvez você queira nomear a sandbox da Platform como &quot;Plataforma do tutorial do Luma - Ignatius J Reilly&quot; em vez de apenas &quot;Plataforma do tutorial do Luma&quot;.

Se você ficar preso, tente reler as instruções primeiro e depois use o link ![Registrar um problema](https://experienceleague.adobe.com/assets/img/feedback.svg) na barra lateral de cada página para entrar em contato comigo.

## Notas técnicas

### Ambientes de sandbox

No tutorial, você criará um ambiente de sandbox e o usará para concluir os exercícios. O ambiente de sandbox garante a segurança para que você conclua os exercícios e experimente sem se preocupar em comprometer seus dados de produção.

### API

A Platform é criada como API. Embora existam workflows de interface para todos os principais workflows da Platform e sejam usados principalmente, o tutorial contém alguns exercícios orientados por API. Eu guiarei você pela configuração básica do projeto no Adobe Developer Console e fornecerei [!DNL Postman] ambientes e coleções para começar a usar a API da plataforma. Após concluir o tutorial, talvez você considere importante se familiarizar com a API da plataforma e usá-la na sua própria implantação.

### Tecnologias de terceiros

Embora você use várias tecnologias neste tutorial, você permanecerá quase totalmente no ecossistema de Adobe. Em sua própria implementação da Platform, você provavelmente integrará a Platform a tecnologias específicas de terceiros. Para manter este tutorial relevante para todos os clientes, usaremos uma implementação mais genérica.

## Atualizações do tutorial

* Junho de 2023: atualizado para incluir novo fluxo de trabalho de permissão e usar a credencial da API de servidor para servidor do OAuth


Agora, vamos para a primeira lição—[configurar permissões](configure-permissions.md).
