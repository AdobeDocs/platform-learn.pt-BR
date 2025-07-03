---
title: Experience Decisioning - Experience Decisioning 101
description: Experience Decisioning - Experience Decisioning 101
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
source-git-commit: 13d790855601fa6f36c1afa0f2d5faad5fc07eb0
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 1%

---

# 3.7.1 Decisão da experiência 101

## Terminologia de 3.7.1.1

Para entender melhor o Experience Decisioning, recomendamos que você leia a [visão geral](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=en) sobre como o Serviço de Aplicativos Offer Decisioning funciona com o Adobe Experience Platform.

Ao trabalhar com o Offer Decisioning, é necessário compreender os seguintes conceitos:

| Termo | Explicação |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Oferta** | Uma oferta é uma mensagem de marketing que pode ter regras associadas que especificam quem está qualificado para ver a oferta. Uma oferta tem um status: rascunho, aprovado ou arquivado. |
| **Posicionamento** | A combinação de local (ou Tipo de canal) e contexto (ou Tipo de conteúdo) em que uma oferta é exibida para um usuário final. Efetivamente, é a combinação de Texto, HTML, Imagem, JSON em canais móveis, da Web, sociais, de Mensagens instantâneas e não digitais. |
| **Regra** | A lógica que define e controla a qualificação dos usuários finais para uma oferta. |
| **Oferta personalizada** | Uma mensagem de marketing personalizável com base em regras de elegibilidade e restrições. |
| **Oferta substituta** | A oferta padrão exibida quando um usuário final não está qualificado para nenhuma das ofertas na coleção usada. |
| **Limite** | Usado em uma definição de oferta para definir quantas vezes uma oferta pode ser apresentada no total e para um usuário específico. |
| **Prioridade** | Nível para determinar a classificação de prioridade de um conjunto de resultados de ofertas. |
| **Coleção** | Usado para filtrar um subconjunto de ofertas da lista de ofertas personalizadas para acelerar o processo de decisão de oferta. |
| **Decisão** | Uma combinação de um conjunto de ofertas, disposição e perfil para os quais o profissional de marketing deseja que o mecanismo de decisão forneça a melhor oferta. |
| **AEM Assets Essentials** | Uma experiência universal e centralizada para armazenar, localizar e selecionar ativos nas soluções da Adobe Experience Cloud e da Adobe Experience Platform. |

{style="table-layout:auto"}

## 3.7.1.2 Decisão da experiência

Faça login no Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ExD](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`. Você estará na exibição **Página inicial** da sua sandbox `--aepSandboxName--`.

![ExD](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

No próximo exercício, você configurará suas próprias ofertas e decisões.

## Próximas etapas

Ir para [3.7.2 Configurar suas Ofertas e Decisão](./ex2.md){target="_blank"}

Voltar para [Experience Decisioning](ajo-decisioning.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
