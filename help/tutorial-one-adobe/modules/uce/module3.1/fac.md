---
title: Coleção de dados - Composição de público-alvo federado
description: Coleção de dados - Composição de público-alvo federado
kt: 5342
doc-type: tutorial
exl-id: cc2ac85e-e902-4bb7-ab54-aa39980f97aa
source-git-commit: 71fe7b82e09aa9bc26b03dd2358d008265f54629
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# 3.1 Composição de público-alvo federado

Neste módulo, o objetivo é saber tudo sobre como criar públicos-alvo usando a Composição de público-alvo federado.

A Federated Audience Composition (FAC) no Experience Platform permite acessar e criar públicos com atributos de alto valor correspondentes de data warehouses empresariais, que enriquecem e complementam o perfil do cliente em tempo real e públicos no Experience Platform para melhorar a segmentação, o direcionamento, a ativação e o delivery de experiências de cliente impactantes. Usando a Federated Audience Composition, um banco de dados virtual é criado vinculando bancos de dados remotos por meio de metadados. Essa abordagem simplifica o acesso, reduz a duplicação e melhora a experiência do usuário final. As equipes recebem a flexibilidade de assimilar conjuntos de dados diretamente no Experience Platform ou acessar conjuntos de dados residentes em data warehouses ao montar públicos para workflows de envolvimento. Essa abordagem aproveita os investimentos e os ativos do data warehouse para complementar a Real-Time CDP e a Journey Optimizer. A Federated Audience Composition permite que os clientes utilizem e combinem funcionalidades em lote e em tempo real em novos padrões críticos de caso de uso:

- Segmentação de público federado: uma equipe pode criar um público usando a interface de composição de público de arrastar e soltar compatível com o profissional de marketing no Real-Time CDP e no Journey Optimizer, mas com uma consulta enviada para o data warehouse, deixando dados subjacentes confidenciais no warehouse sem duplicação e fornecendo acesso flexível a conjuntos de dados essenciais.
- Enriquecimento de público: os públicos-alvo integrados ao Real-Time CDP e ao Journey Optimizer podem ser enriquecidos com dados corporativos adicionais para melhorar o direcionamento e a personalização com conjuntos de dados adicionais baseados e não baseados em perfil que não persistem no Adobe Experience Platform. Por exemplo, uma marca de varejo pode complementar um público de compradores online recentes com uma lista dos principais locais tradicionais para criar um público-alvo para uma promoção online e na loja entre canais.
- Enriquecimento de perfil: as equipes podem selecionar atributos de perfil do data warehouse que são essenciais para as experiências do momento serem retidas em perfis de clientes acionáveis que residem no Real-Time CDP e são acessadas pelo Journey Optimizer. Esses pontos de dados adicionais estão disponíveis para segmentação downstream e personalização acionadas por comportamentos de evento, dependendo da ação do usuário e do caso de uso do cliente. Isso permitirá que os atributos trazidos junto com os públicos-alvo federados estejam disponíveis para segmentação e personalização no momento, junto com outros atributos e sinais comportamentais retidos em um perfil do cliente.

A Federated Audience Composition oferece aos clientes da Real-Time CDP e da Journey Optimizer a flexibilidade para decidir quais dados desejam usar quando e ajuda a evitar conjuntos de dados ou padrões de integração desnecessariamente duplicados. Isso representa uma combinação única de uma abordagem federada ao uso de dados corporativos para preparar públicos-alvo e atributos de alto valor, combinada com um sistema otimizado para o engajamento entre canais no momento. Isso resulta em menos movimentação de dados, mas também em novas oportunidades de utilizar públicos-alvo e atributos de alto valor para uma ativação consistente de baixa latência em todos os canais.

## Objetivos de aprendizagem

- Saiba como conectar o Snowflake ao Adobe Experience Platform
- Saiba como criar um modelo de dados para seus dados federados no Adobe Experience Platform
- Saiba como criar composições de público federado no Adobe Experience Platform

## Pré-requisitos

- Acesso ao Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acesso a um data warehouse do Snowflake

## Exercícios

[3.1.1 Configurar o ambiente Snowflake](./ex1.md)

Neste exercício, você configurará sua conta de avaliação do Snowflake e a conectará ao Adobe Experience Platform

[3.1.2 Criar esquemas, modelo de dados e links](./ex2.md)

Neste exercício, você configurará seu modelo de dados na AEP para os dados federados.

[3.1.3 Criar uma composição federada](./ex3.md)

Neste exercício, você configurará seu modelo de dados na AEP para os dados federados.

[Resumo e benefícios](./summary.md)

Resumo desse módulo e visão geral dos benefícios.

>[!NOTE]
>
>![Informantes técnicos](./../../../assets/images/techinsiders.png){width="50px" align="left"}
>
>Em caso de dúvidas, envie um email para **techinsiders@adobe.com** para compartilhar comentários gerais sobre sugestões para conteúdo futuro. Entre em contato diretamente com o Tech Insiders.

[Voltar a todos os módulos](../../../overview.md)
