---
title: Offer Decisioning - Offer decisioning 101
description: Offer Decisioning - Offer decisioning 101
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: e7cfe551-c8b4-47b0-b048-05e1869da7f9
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 4%

---

# 9.1 Offer decisioning 101

## 9.1.1 Terminologia

Para entender melhor o Offer Decisioning, recomendamos que você leia a [visão geral](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=en) sobre como o Serviço de Aplicativo do Offer Decisioning funciona com o Adobe Experience Platform.

Trabalhando com o Offer Decisioning, é necessário entender os seguintes conceitos:

| Termo | Explicação |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Oferta** | Uma oferta é uma mensagem de marketing que pode ter regras associadas a ela que especificam quem está qualificado para ver a oferta. Uma oferta tem um status: rascunho, aprovado ou arquivado. |
| **Disposição** | A combinação de local (ou Tipo de canal) e contexto (ou Tipo de conteúdo) em que uma oferta é exibida para um usuário final. Efetivamente, é a combinação de Texto, HTML, Imagem, JSON em dispositivos móveis, Web, Social, Mensagens instantâneas e canais não digitais. |
| **Regra** | A lógica que define e controla a qualificação de usuários finais para uma oferta. |
| **Oferta personalizada** | Uma mensagem de marketing personalizável com base em regras e restrições de elegibilidade. |
| **Oferta de fallback** | A oferta padrão exibida quando um usuário final não está qualificado para nenhuma das ofertas na coleção usada. |
| **Limitação** | Usada em uma definição de oferta para definir quantas vezes uma oferta pode ser apresentada no total e a um usuário específico. |
| **Prioridade** | Nível para determinar a classificação de prioridade a partir de um conjunto de resultados de ofertas. |
| **Coleção** | Usado para filtrar um subconjunto de ofertas da lista de ofertas personalizada para acelerar o processo do offer decisioning. |
| **Decisão** | Uma combinação de um conjunto de ofertas, posicionamento e perfil que o profissional de marketing deseja que o mecanismo de decisão forneça a melhor oferta. |
| **AEM Assets Essentials** | Uma experiência universal e centralizada para armazenar, localizar e selecionar ativos nas soluções da Adobe Experience Cloud e na Adobe Experience Platform. |

{style=&quot;table-layout:auto&quot;}

## offer decisioning 9.1.2

Faça logon no Adobe Journey Optimizer acessando [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Você será redirecionado para o **Início**  no Journey Optimizer. Primeiro, certifique-se de usar a sandbox correta. A sandbox a ser usada é chamada de `--aepSandboxId--`. Para alterar de uma sandbox para outra, clique em **Produto de produção (VA7)** e selecione a sandbox na lista. Neste exemplo, a sandbox é chamada de **Ativação AEP FY22**. Você estará no **Início** exibição da sandbox `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

No menu esquerdo, clique em **Ofertas**. Agora você verá o menu Ofertas, que contém itens como Ofertas, Coleções e Decisões.

![Posicionamentos](./images/homedec.png)

Clique em **Componentes**. Agora você verá o menu Ofertas, que contém itens como Disposições, Tags, Regras e Classificações.

![Posicionamentos](./images/components.png)

## 9.1.3 Disposições

Ir para **Posicionamentos**.

![Posicionamentos](./images/placements.png)

No **Posicionamentos** é possível definir suas disposições para as ofertas. Ao definir uma decisão, o posicionamento define onde a oferta resultante será exibida (Tipo de canal) e em que forma ou formulário (Tipo de conteúdo).

Se você não vir nenhuma disposição na sua instância do Adobe Experience Platform, crie-as conforme indicado abaixo e na captura de tela.

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

{style=&quot;table-layout:auto&quot;}

**Observação**: Não altere nada para as disposições já disponíveis.

Clique em qualquer Disposição para visualizar suas configurações.

![Posicionamentos](./images/placement1.png)

Agora você verá todos os campos da Disposição:

- **Nome** da disposição
- **ID de posicionamento**
- **Tipo de canal** para a disposição
- **Tipo de conteúdo** da disposição, que pode ser **Texto**, **HTML**, **Imagem** ou **JSON**
- **Descrição** que permite adicionar uma descrição adicional para a disposição

## 9.1.4 Regras de decisão

Uma Regra (também chamada de regra de elegibilidade) é o equivalente a uma **Segmento**. Uma Regra é, de fato, um Segmento com a única diferença de que uma Regra pode ser usada com uma Oferta para fornecer a melhor oferta a um perfil no Adobe Experience Platform.

Como você já sabe definir segmentos com base nos módulos de ativação anteriores, vamos rapidamente revisitar o Ambiente de segmentação:

Ir para **Regras**. Clique em **+ Criar regra**.

![Regras de decisão](./images/rules.png)

Em seguida, você verá o ambiente Segmentação do Adobe Experience Platform.

![Regras de decisão](./images/createrule1.png)

Agora é possível acessar todos os campos que fazem parte do Esquema da União para o Perfil do cliente em tempo real e criar qualquer regra.

Também é interessante saber que você pode simplesmente reutilizar segmentos já definidos no Adobe Experience Platform, acessando **Públicos-alvo** > ``--aepTenantIdSchema--``.

![Regra de decisão](./images/decisionruleaud.png)

Você verá isso:

![Regra de decisão](./images/decisionruleaud1.png)

Se desejar, agora é possível configurar suas próprias Regras. Para este exercício, você precisará de duas regras:

- all - Clientes masculinos
- all - Clientes do sexo feminino

Se essas regras ainda não existirem, por favor, crie-as. Se já existirem, use essas regras e não crie novas regras.

O atributo a ser usado para criar a regra é **Perfil individual XDM** > **Pessoa** > **Gênero**.

Como exemplo, aqui está a definição de regra para a regra **all - Clientes masculinos**:

![Regra de decisão](./images/allmale.png)

Como exemplo, aqui está a definição de regra para a regra **all - Clientes do sexo feminino**:

![Regra de decisão](./images/allfemale.png)

## 9.1.5 Ofertas

Ir para **Ofertas** e selecione **Ofertas**. Clique em **+ Criar oferta**.

![Regra de decisão](./images/offers1.png)

Você verá esse pop-up.

![Regra de decisão](./images/offers2.png)

Não crie ofertas agora - você fará isso no próximo exercício.

Agora, você verá que há dois tipos de ofertas:

- Ofertas personalizadas
- Ofertas de fallback

Uma Oferta personalizada é um conteúdo específico que deve ser exibido em uma situação específica. Uma Oferta personalizada é criada especificamente para fornecer uma experiência pessoal e contextual se critérios específicos forem atendidos.

Uma Oferta de fallback é uma oferta que é exibida se os critérios para as Ofertas personalizadas não forem atendidos.

## 9.1.6 Decisões

Uma Decisão combina disposições, uma coleção de ofertas personalizadas e uma oferta de fallback a ser usada pelo mecanismo do Offer Decisioning para encontrar a melhor oferta para um perfil específico, com base em cada uma das características de oferta personalizada individual, como prioridade, restrição de elegibilidade e limite total/usuário.

Para configurar o **Decisão**, clique em **Decisões**.

![Regra de decisão](./images/activity.png)

No próximo exercício, você configurará suas próprias ofertas e decisões.

Próxima etapa: [9.2 Configurar suas ofertas e decisão](./ex2.md)

[Voltar ao Módulo 9](./offer-decisioning.md)

[Voltar para todos os módulos](./../../overview.md)
