---
title: Offer Decisioning - Offer Decisioning 101
description: Offer Decisioning - Offer Decisioning 101
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
exl-id: b46e0205-b0a1-4a14-95f6-9afe21cd2b5e
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 3%

---

# 3.3.1 Offer Decisioning 101

## 3.3.1.1 Terminologia

Para entender melhor o Offer Decisioning, recomendamos que você leia a [visão geral](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=pt-BR) sobre como o Serviço de Aplicativos Offer Decisioning funciona com o Adobe Experience Platform.

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

## 3.3.1.2 Offer Decisioning

Faça login no Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`. Você estará na exibição **Página inicial** da sua sandbox `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

No menu esquerdo, clique em **Ofertas**. Agora você verá o menu Ofertas, que contém itens como Ofertas, Coleções e Decisões.

![Posicionamentos](./images/homedec.png)

Clique em **Componentes**. Agora você verá coisas como Disposições, Qualificador de coleção, Regras e Classificações.

![Posicionamentos](./images/components.png)

## 3.3.1.3 Posicionamentos

Vá para **Posicionamentos**.

![Posicionamentos](./images/placements.png)

Na guia **Posicionamentos**, é possível definir seus posicionamentos para as ofertas. Ao definir uma decisão, o posicionamento define onde a oferta resultante será exibida (Tipo de canal) e em que forma ou formulário (Tipo de conteúdo).

Se você não vir nenhuma disposição em seu ambiente, crie-as conforme indicado abaixo e na captura de tela.

| Nome | Tipo de canal | Tipo de conteúdo |
| ---------------------- | ------------ | ------------ |
| **Não digital - Texto** | Não digital | Texto |
| **Web - JSON** | Web | JSON |
| **Web - HTML** | Web | HTML |
| **Web - Texto** | Web | Texto |
| **Web - Imagem** | Web | Imagem |
| **Email - JSON** | Email | JSON |
| **Email - HTML** | Email | HTML |
| **Email - Texto** | Email | Texto |
| **Email - Imagem** | Email | Imagem |

{style="table-layout:auto"}

**Observação**: não altere nada para os posicionamentos já disponíveis.

Clique em qualquer posicionamento para visualizar suas configurações.

![Posicionamentos](./images/placement1.png)

Agora você verá todos os campos do Posicionamento:

- **Nome** do posicionamento
- **ID de posicionamento**
- **Tipo de canal** para o Posicionamento
- **Tipo de conteúdo** do Posicionamento, que pode ser **Texto**, **HTML**, **Imagem** ou **JSON**
- Campo **Descrição** permitindo adicionar descrição adicional ao Posicionamento

## 3.3.1.4 Regras de decisão

Uma Regra (também chamada de regra de elegibilidade) é equivalente a um **público-alvo**. Uma regra é, na verdade, um público-alvo com a única diferença de que uma regra pode ser usada com uma oferta para fornecer a melhor oferta a um perfil no Adobe Experience Platform.

Como você já sabe definir públicos-alvo com base nos módulos de ativação anteriores, vamos rever rapidamente o Ambiente de segmentação:

Vá para **Regras**. Clique em **+ Criar regra**.

![Regras de decisão](./images/rules.png)

Em seguida, você verá a interface de Criação de público-alvo do Adobe Experience Platform.

![Regras de decisão](./images/createrule1.png)

Agora é possível acessar todos os campos que fazem parte do Esquema de união para o Perfil do cliente em tempo real e criar qualquer regra.

Também é bom saber que você pode simplesmente reutilizar públicos já definidos no Adobe Experience Platform acessando **Públicos-alvo** > ``--aepTenantId--``.

Você verá isto:

![Regra de decisão](./images/decisionruleaud.png)

Se desejar, agora é possível configurar suas próprias Regras. Para este exercício, você precisará de duas regras:

- todos - Clientes do sexo masculino
- all - Clientes do sexo feminino

Se essas regras ainda não existirem, crie-as. Se já existirem, use essas regras e não crie novas.

O atributo a ser usado para criar a regra é **Perfil Individual XDM** > **Pessoa** > **Sexo**.

Como exemplo, aqui está a definição de regra para a regra **todos - Clientes do sexo masculino**:

![Regra de decisão](./images/allmale.png)

Como exemplo, aqui está a definição de regra para a regra **todas - Clientes do sexo feminino**:

![Regra de decisão](./images/allfemale.png)

## 3.3.1.5 Ofertas

Vá para **Ofertas** e selecione **Ofertas**. Clique em **+ Criar oferta**.

![Regra de decisão](./images/offers1.png)

Você então verá esse pop-up.

![Regra de decisão](./images/offers2.png)

Não criar nenhuma oferta agora. Você fará isso no próximo exercício.

Agora você verá que há dois tipos de ofertas:

- Ofertas personalizadas
- Ofertas substitutas

Uma Oferta personalizada é um conteúdo específico que deve ser mostrado em uma situação específica. Uma Oferta personalizada é criada especificamente para fornecer uma experiência pessoal e contextual se critérios específicos forem atendidos.

Uma Oferta substituta é uma oferta exibida se os critérios para Ofertas personalizadas não forem atendidos.

## 3.3.1.6 Decisões

Uma decisão combina posicionamentos, uma coleção de ofertas personalizadas e uma oferta de fallback a ser usada pelo mecanismo do Offer Decisioning para encontrar a melhor oferta para um perfil específico, com base em cada uma das características de oferta personalizadas individuais, como prioridade, restrição de elegibilidade e limite total / usuário.

Para configurar sua **Decisão**, clique em **Decisões**.

![Regra de decisão](./images/activity.png)

No próximo exercício, você configurará suas próprias ofertas e decisões.

## Próximas etapas

Ir para [3.3.2 Configurar as Ofertas e a Decisão](./ex2.md){target="_blank"}

Voltar para [Offer Decisioning](offer-decisioning.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
