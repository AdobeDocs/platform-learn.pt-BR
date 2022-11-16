---
title: Introdução à Adobe Experience Platform para arquitetos e engenheiros de dados
description: Introdução à Adobe Experience Platform para arquitetos de dados e engenheiros de dados.
breadcrumb-title: Visão geral
role: Data Architect, Data Engineer
kt: 4348
thumbnail: 4348-overview.jpg
recommendations: catalog, noDisplay
exl-id: fabbc591-840b-40dc-89af-305626a16338
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 1%

---

# Introdução à Adobe Experience Platform para arquitetos e engenheiros de dados

<!--5min-->

_Introdução à Adobe Experience Platform para arquitetos e engenheiros de dados_ O é o ponto de partida perfeito para pôr mãos à obra com o Experience Platform.


<!--How do we address ETL-->

## Objetivos de aprendizagem

Os arquitetos de dados e os engenheiros de dados devem colaborar estreitamente para uma implantação Experience Platform bem-sucedida. Este tutorial prático ensina as principais tarefas executadas por _ambas as funções_ para que você saiba como começar a implementar a Platform para sua própria empresa. Você será orientado por exercícios que apresentarão a terminologia, os recursos, a interface e a API do Experience Platform. Os clientes de aplicativos Adobe Experience Cloud, como Real-time Customer Data Platform, Customer Journey Analytics e Journey Optimizer, também considerarão esse conteúdo útil, pois os serviços da plataforma são os fundamentos críticos desses aplicativos.

![A arquitetura da Adobe Experience Cloud destaca os serviços da plataforma abordados neste tutorial — identidade, perfil, segmentação, assimilação, consulta e governança](assets/marketecture.png)

Os tópicos incluem:

* Configuração de permissões de usuário
* Criação de sandboxes
* Configurar um projeto do Console do desenvolvedor e usar a API da plataforma
* Gerenciamento de dados — incluindo a criação de esquemas, conjuntos de dados, identidades, políticas de mesclagem e governança de dados
* Assimilação de dados usando modos de lote e fluxo
* Captura de dados da Web com o SDK da Web da Adobe Experience Platform
* Criação de perfis de clientes em tempo real
* Uso do Serviço de query para validar dados e extrair dados
* Criação de segmentos

## Cenário comercial

O Adobe Experience Platform é uma plataforma técnica criada para ajudá-lo a atingir os objetivos de marketing. Os casos de uso comercial devem orientar a criação e implementação da tecnologia. Este tutorial foca em uma marca de varejo ficcional chamada Luma. O Luma opera lojas brick-and-mortar em vários países e também tem uma presença online com um site e aplicativos móveis. Eles estão investindo no Adobe Experience Platform para combinar dados de fidelidade, CRM, Web e compra offline em perfis de clientes em tempo real e ativar esses perfis para elevar seu marketing ao próximo nível. Os objetivos de negócios do Luma podem ou não estar alinhados com os objetivos de sua empresa, mas você deve ser capaz de relacionar as etapas práticas deste tutorial com seus próprios objetivos de negócios.

## Pré-requisitos

* Você concluiu o [Introdução ao curso do Adobe Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2020.1) no Experience League e estão familiarizados com os recursos da plataforma
* Você tem acesso a uma conta provisionada com a Adobe Experience Platform (ou um aplicativo baseado na plataforma, como CDP em tempo real ou Journey Optimizer) e Coleta de dados (antigo Launch).
* Você é um Administrador do Sistema dessa conta ou pode ter uma [configurar permissões de usuário](configure-permissions.md) para você.

## Usar este tutorial

Este tutorial combina tarefas para engenheiros de dados e arquitetos de dados. Como é um tutorial introdutório, você deve ser capaz de concluir as tarefas para ambas as funções. Uma vez que muitas das lições se baseiam no que foi implementado em lições anteriores, é necessário avançar através das lições em ordem. Vou dizer que lições podem ser ignoradas.

Conforme você cria vários elementos da Plataforma durante este tutorial, tente se manter fiel aos nomes que eu recomendar na medida do possível. No entanto, há alguns nomes de elementos de alto nível que você pode querer personalizar caso haja várias pessoas em sua organização assistindo a este tutorial simultaneamente. Por exemplo, você pode querer nomear a sandbox da plataforma como &quot;Plataforma tutorial do Luma - Ignatius J Reilly&quot; em vez de apenas &quot;Plataforma tutorial do Luma&quot;.

Se ficar preso, tente ler novamente as instruções primeiro e use a ![Registrar um problema](https://experienceleague.adobe.com/assets/img/feedback.svg) na barra lateral de cada página para entrar em contato comigo.

## Notas técnicas

### Ambientes do Sandbox

No tutorial, você criará um ambiente de sandbox e o usará para concluir os exercícios. O ambiente sandbox torna seguro você realizar exercícios e experimentar sem se preocupar em comprometer seus dados de produção.

### API

A plataforma é criada com a API primeiro. Embora existam workflows de interface para todos os principais workflows da plataforma e sejam usados principalmente, o tutorial contém alguns exercícios orientados a API. Irei guiá-lo pela configuração básica do projeto no Adobe Developer Console e fornecerei a você [!DNL Postman] ambientes e coleções para começar a usar a API do Platform. Após concluir o tutorial, você pode achar valioso estar familiarizado com a API da plataforma e usá-la em sua própria implantação.

### Tecnologias de terceiros

Embora você use várias tecnologias neste tutorial, você permanecerá quase totalmente dentro do ecossistema do Adobe. Na sua própria implementação da plataforma, você provavelmente integrará a Platform a tecnologias específicas de terceiros. Para manter este tutorial relevante para todos os clientes, usaremos uma implementação mais genérica.

Agora vamos para a primeira lição.[configurar permissões](configure-permissions.md).
