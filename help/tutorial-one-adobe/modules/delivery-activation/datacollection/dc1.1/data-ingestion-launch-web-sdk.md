---
title: 1.1 Configuração da coleção de dados do Adobe Experience Platform e da extensão do Web SDK
description: Foundation - Configuração da coleta de dados do Adobe Experience Platform e da extensão Web SDK
kt: 5342
doc-type: tutorial
exl-id: 8c613648-9007-49fb-898f-039c366297da
source-git-commit: 23816907de778cbe3b9708f4a7273bdcb8e86d5c
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# 1.1 Configuração da coleção de dados do Adobe Experience Platform e da extensão de tag da Web SDK

Este módulo fundamental apresenta a você a visão de coleção de dados da Adobe e explica como obter dados de um site e aplicativo móvel no Adobe Experience Platform e em outros aplicativos por meio da Coleção de dados da Adobe Experience Platform, dos SDKs da Adobe Experience Platform e do Adobe Experience Platform Edge Network.

Este módulo apresenta alguns conceitos e tecnologias que têm um impacto além do escopo de um tutorial técnico do Adobe Experience Platform. Deve ficar claro quais partes desses exercícios são fundamentais para o restante do tutorial abrangente, que ensina mais sobre a Edge Network e seus recursos e onde obter mais informações e tutoriais.

## Objetivos de aprendizagem

- Saiba como uma marca usa a Coleção de dados da Adobe Experience Platform como seu Sistema Tag Management (TMS).
- Saiba mais sobre os fluxos de dados usados por uma marca para assimilar dados para seus produtos da Adobe.
- Saiba como enviar dados para a Adobe Experience Platform e outros produtos por meio do Adobe Experience Platform Edge Network.
- Saiba como criar Elementos de dados e Regras que coletam dados da Web e de dispositivos móveis.
- Saiba mais sobre os eventos de rastreamento do [Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home) e como depurar seu conteúdo.
- Saiba o que é uma camada de dados e o que a Adobe recomenda ao implementar uma.
- Saiba quais são as etapas para implementar o [Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home) do zero.
- Saiba mais sobre a diferença entre uma implementação da Web e móvel.

## Pré-requisitos

- Acesso ao Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acesso à Coleção de Dados do Adobe Experience Platform: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Acesso ao site de demonstração

>[!NOTE]
>
>Não se esqueça de instalar, configurar e usar a Extensão do Chrome, conforme referenciado em [Instalar a extensão do Chrome para a documentação do Experience League](../../../getting-started/gettingstarted/ex1.md)

## Exercícios

[1.1.1 Noções básicas sobre a coleta de dados do Adobe Experience Platform](./ex1.md)

Neste exercício, explore a interface da Coleção de dados da Adobe Experience Platform e entenda seus recursos.

[1.1.2 Edge Network, fluxos de dados e coleção de dados do lado do servidor](./ex2.md)

Neste exercício, você aprenderá a encaminhar dados para produtos da Adobe na interface da Coleção de dados da Adobe Experience Platform e a investigar os fluxos de dados usados pelo site de demonstração.

[1.1.3 Introdução à coleta de dados do Adobe Experience Platform](./ex3.md)

Neste exercício, você aprenderá a configurar uma extensão, criar elementos de dados e regras e publicá-los na Web.

[1.1.4 Coleta de dados da Web no lado do cliente](./ex4.md)

Neste exercício, depure o Web SDK que foi instalado para entender como ele funciona e quais dados serão usados em exercícios futuros.

[1.1.5 Implementação do Adobe Analytics e do Adobe Audience Manager](./ex5.md)

Neste exercício, consulte e use dados da Web coletados com o Web SDK no Adobe Analytics e no Adobe Audience Manager.

[1.1.6 Implementação do Adobe Target](./ex6.md)

Neste exercício, configure uma atividade no Adobe Target, implementada por meio da Web SDK.

[Requisitos do esquema XDM do 1.1.7 no Adobe Experience Platform](./ex7.md)

Para garantir que o Web SDK possa assimilar dados na Adobe Experience Platform, há um requisito para que um mixin XDM específico faça parte do esquema XDM no Adobe Experience Platform.

![Informantes técnicos](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo tudo o que há para saber sobre o Adobe Experience Platform e seus aplicativos. Em caso de dúvidas, envie um email para **techinsiders@adobe.com** para compartilhar comentários gerais sobre sugestões para conteúdo futuro. Entre em contato diretamente com o Tech Insiders.

[Voltar a todos os módulos](./../../../../overview.md)
