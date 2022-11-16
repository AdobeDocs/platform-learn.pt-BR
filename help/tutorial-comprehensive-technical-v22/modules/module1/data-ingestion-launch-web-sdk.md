---
title: 1. Configuração da coleta de dados do Adobe Experience Platform e da extensão do SDK da Web
description: Foundation - Configuração da coleta de dados do Adobe Experience Platform e da extensão do SDK da Web
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 86da7132-cb06-4be3-b6b8-ea3ab937e6dc
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 1%

---

# 1. Foundation - Configuração da coleta de dados do Adobe Experience Platform e da extensão do SDK da Web

**Autor: [Matthew Joseph Woolley](https://www.linkedin.com/in/matthewjwoolley/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Esse módulo fundamental apresenta a visão de coleta de dados do Adobe Edge e explica como obter dados de um site e aplicativo móvel para o Adobe Experience Platform e outros aplicativos por meio da Coleta de dados da Adobe Experience Platform, dos SDKs e da Rede Adobe Experience Platform. Este módulo apresenta alguns conceitos e tecnologias que têm impacto além do escopo de um tutorial técnico do Adobe Experience Platform. Deve ficar claro quais partes desses exercícios são fundamentais para o resto do tutorial abrangente, que o ensina mais sobre o Experience Edge e seus recursos, e onde procurar mais informações e tutoriais.

## Objetivos de aprendizagem

- Saiba como uma marca usa a Coleta de dados da Adobe Experience Platform como seu Sistema Tag Management (TMS).
- Saiba mais sobre os fluxos de dados usados por uma marca para assimilar dados em seus produtos de Adobe.
- Saiba como enviar dados para a Adobe Experience Platform e outros produtos por meio da Rede de borda da Adobe Experience Platform.
- Saiba como criar Elementos de dados e Regras que coletam dados da Web e do Mobile.
- Saiba mais sobre os eventos de rastreamento do SDK da Web e como depurar seu conteúdo.
- Saiba o que é uma camada de dados e o que o Adobe recomenda ao implementar uma.
- Saiba quais são as etapas para implementar o SDK da Web do zero.
- Saiba mais sobre a diferença entre uma implementação da Web e móvel.

## Pré-requisitos

- Acesso ao Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acesso à coleta de dados do Adobe Experience Platform: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Acesso ao site de demonstração

>[!IMPORTANT]
>
>Este tutorial foi criado para facilitar um formato específico de workshop. Ele usa sistemas e contas específicos aos quais você pode não ter acesso. Mesmo sem acesso, achamos que você ainda pode aprender muito lendo esse conteúdo muito detalhado. Se você participar de um dos workshops e precisar de suas credenciais de acesso, entre em contato com o representante do Adobe, que fornecerá as informações necessárias.

## Visão geral da arquitetura

Consulte a arquitetura abaixo, que destaca os componentes que serão discutidos e usados neste módulo.

![Visão geral da arquitetura](../../assets/images/architecturem1.png)

## Sandbox para usar

Para este módulo, use esta sandbox: `--aepSandboxId--`.

>[!NOTE]
>
>Não se esqueça de instalar, configurar e usar a Extensão do Chrome, conforme referenciado em [0.1 - Instalar a extensão do Chrome para a documentação do Experience League](../module0/ex1.md)

## Exercícios

[1.1 Noções básicas sobre a coleta de dados do Adobe Experience Platform](./ex1.md)

Neste exercício, explore a interface do usuário da Coleta de dados da Adobe Experience Platform e entenda seus recursos.

[1.2 Rede de borda, conjuntos de dados e coleta de dados do lado do servidor](./ex2.md)

Neste exercício, você aprenderá a encaminhar dados para produtos do Adobe na interface da Coleta de dados da Adobe Experience Platform e investigar os fluxos de dados usados pelo site de demonstração.

[1.3 Introdução à coleta de dados do Adobe Experience Platform](./ex3.md)

Neste exercício, você aprenderá a configurar uma Extensão, criar Elementos de dados e Regras e publicá-los na Web.

[1.4 Coleta de dados da Web do lado do cliente](./ex4.md)

Neste exercício, depure o SDK da Web que foi instalado para entender como ele funciona e quais dados serão usados em exercícios futuros.

[1.5 Implementar o Adobe Analytics e o Adobe Audience Manager](./ex5.md)

Neste exercício, consulte e use dados da Web coletados com o SDK da Web no Adobe Analytics e no Adobe Audience Manager.

[1.6 Implementar o Adobe Target](./ex6.md)

Neste exercício, configure uma atividade no Adobe Target, implementada por meio do SDK da Web.

[Requisitos do esquema XDM 1.7 no Adobe Experience Platform](./ex7.md)

Para garantir que o SDK da Web e o alloy.js sejam capazes de assimilar dados no Adobe Experience Platform, há um requisito para que uma Mistura XDM específica faça parte do Esquema XDM no Adobe Experience Platform.

[Resumo e benefícios](./summary.md)

Resumo deste módulo e visão geral dos benefícios.

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender tudo o que há para saber sobre a Adobe Experience Platform. Se você tiver dúvidas, queira compartilhar comentários gerais de suas sugestões sobre conteúdo futuro, entre em contato diretamente com Wouter Van Geluwe, enviando um email para **vangeluw@adobe.com**.

[Voltar para todos os módulos](../../overview.md)
