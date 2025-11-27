---
title: Introdução ao Agent Orchestrator
description: Introdução ao Agent Orchestrator
kt: 5342
doc-type: tutorial
source-git-commit: bb31fe8a36f1c9ee9d212500e2e58e01be1129b8
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 0%

---

# 1.1.1 Introdução ao Agent Orchestrator

## 1.1.1.1 Definir contexto no Agent Orchestrator

Ir para [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Você deverá ver isso. Verifique se você está na organização **Experience Platform International**.

![Agent Orchestrator](./images/ao1.png)

Clique na janela **contexto**.

![Agent Orchestrator](./images/ao2.png)

Defina o contexto como:

- **Source de Documentação**: **Journey Optimizer**

A configuração Source de documentação ajuda a dar preferência a qual conjunto de documentos da liga de experiência verificar se há perguntas relacionadas ao conhecimento do produto/Experience League.

- **Sandbox**: **Prod - Acelerar (VA7)**

A configuração de Sandbox ajuda a identificar o que o Assistente de IA de sandbox deve considerar ao fazer perguntas.

- **Dataview**: **Acelerar B2C 2026**

A configuração Exibição de dados ajuda a identificar qual Assistente de IA de exibições de dados deve considerar ao fazer perguntas.

Clique em **Definir contexto**.

![Agent Orchestrator](./images/ao3.png)

## 1.1.1.2 Comece com as tendências gerais de compra para ancorar o contexto e ampliar a fibra

**Propósito**

Obtenha pulsos de alto nível conforme a demanda da categoria — móvel, telefone fixo, Internet, TV, fibra — especificamente pelos últimos 60 dias. Isso define linhas de base para sazonalidade, efeitos promocionais e variação regional após a implantação em Nova York.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Show me purchases by mainCategory over the last 2 months.
```

![Agent Orchestrator](./images/ao4.png)

Você deverá ver isso:

![Agent Orchestrator](./images/ao5.png)

Insira o seguinte **Prompt** e clique no botão **enviar**.

`Show me purchases by mainCategory = Fiber over the last 2 months per week`

![Agent Orchestrator](./images/ao6.png)

Você verá isso, que detalha tendências específicas de fibra.

![Agent Orchestrator](./images/ao7.png)

## 1.1.1.3 Correlacionar pedidos com preferências de conteúdo

**Propósito**

Teste a hipótese de que uma preferência por um gênero específico (por exemplo, ficção científica, esportes, drama) prevê o comportamento de atualização da banda larga, especialmente para necessidades de alta largura de banda.

Primeiro, você precisa descobrir qual campo é usado para armazenar a preferência de gênero.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Which field is used to store the preferred genre?
```

![Agent Orchestrator](./images/ao7a.png)

Você deverá ver isso, que mostra que o campo usado para o gênero é **_experienceplatform.individualCharacteristics.references.preferredGenre**.

![Agent Orchestrator](./images/ao7b.png)

Com essas informações, você pode começar a detalhar os dados de compra.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/ao8.png)

Você deverá ver isso. Clique no ícone no bloco **Raciocínio concluído** para entender o que está acontecendo nos bastidores do Agent Orchestrator.

![Agent Orchestrator](./images/ao9.png)

Você deverá ver uma explicação semelhante.

![Agent Orchestrator](./images/ao10.png)

## 1.1.1.4 Identificar Jornadas de Fibra Existentes

**Propósito**

Descubra quais jornadas ativas ou concluídas recentemente incluem &quot;Fibre&quot; no título, por exemplo, &quot;Fibre Upgrade NYC - Set&quot;, &quot;Fibre Trial - Streaming Bundle&quot;.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/ao12.png)

Você deverá ver isso. Clique em **Mostrar mais**.

![Agent Orchestrator](./images/ao13.png)

Você deverá ver uma lista maior de jornadas ativas ou passadas. Clique no ícone **baixar** para baixar uma lista dessas jornadas.

![Agent Orchestrator](./images/ao13a.png)

Isso gerará um arquivo CSV que contém toda a saída do Assistente de IA.

![Agent Orchestrator](./images/ao13b.png)

Clique em para fechar o painel direito. Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/ao14.png)

Você deverá ver isso. Clique no link de uma das jornadas e selecione **Detalhes da Jornada**.

![Agent Orchestrator](./images/ao15.png)

Uma nova janela será aberta e você será direcionado para a visão geral de Detalhes da Jornada imediatamente.

![Agent Orchestrator](./images/ao15a.png)

## 1.1.1.5 Verifique qual público-alvo é usado

**Intenção**:

Entenda a definição inicial da jornada &quot;CitiSignal - Promoção de inicialização máxima de fibra&quot; — quais características impulsionaram o direcionamento (por exemplo, &quot;Preferência de gênero SciFi&quot;, &quot;4+ dispositivos&quot;, &quot;fluxo ≥ 300 GB/mês&quot;).

Digite o seguinte **Prompt**:

```javascript
What was the initial audience in the journey named 
```

Em seguida, digite manualmente `+CitiSignal fib` para habilitar o preenchimento automático. Selecione a jornada **CitiSignal - Fibre Max Launch Promotion**.

![Agent Orchestrator](./images/ao16.png)

Você deverá ver isso. Clique no botão **enviar**.

![Agent Orchestrator](./images/ao17.png)

Você deverá ver isso.

![Agent Orchestrator](./images/ao18.png)

## 1.1.1.6 Validar o desempenho da jornada através da análise de fallout

**Propósito**

Você deseja entender o fallout de desempenho da jornada para saber se há nós ou condições na jornada que estão enfrentando uma grande porcentagem de perfis que estão sendo descartados. Isso é útil para entender se são necessários ajustes adicionais na jornada.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/ao19.png)

Você deverá ver isso.

![Agent Orchestrator](./images/ao20.png)

Role para baixo um pouco. Agora você pode revisar a tabela inspecionando cada nó e seus respectivos números de entrada, números de fallout e taxa de fallout.

O Assistente de IA fornece observações e recomendações.

Clique na frase **Veja aqui como obtive os resultados**.

![Agent Orchestrator](./images/ao21.png)

Você pode ver as etapas seguidas pelo Assistente de IA para chegar aos resultados.

![Agent Orchestrator](./images/ao22.png)

## 1.1.1.7 Criar um novo público

**Propósito**

Com base nas descobertas e pesquisas acima, há uma correlação entre clientes que consomem muitos dados e que têm um gênero preferido de ficção científica ou fantasia. Agora você combinará esses atributos em um público-alvo.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Create an audience that combines people with an average download per month of over 2000 GB and a preferred genre of sci-fi or fantasy.
```

![Agent Orchestrator](./images/ao32.png)

Revise o plano. Insira `yes` e clique em **enviar**.

>[!NOTE]
>
>Este plano é gerado com base em um guia de referência no sistema. Os clientes poderão personalizar planos e adicionar seus próprios planos, mas, por enquanto, eles são estáticos.

![Agent Orchestrator](./images/ao33.png)

Revise a expressão de consulta do segmento. Digite `yes` e clique no botão **enviar**.

![Agent Orchestrator](./images/ao34.png)

Revise a estimativa de tamanho do segmento. Digite `yes` e clique no botão **enviar**.

![Agent Orchestrator](./images/ao35.png)

Clique em **Revisão**.

![Agent Orchestrator](./images/ao36.png)

Revise a definição do segmento. Clique em **Criar**.

![Agent Orchestrator](./images/ao37.png)

Seu público-alvo foi criado.

![Agent Orchestrator](./images/ao38.png)

>[!NOTE]
>
>Ao criar um novo público-alvo, levará 24 horas até que ele esteja disponível para o Assistente de IA para uso adicional.

## 1.1.1.8 Encontre públicos-alvo existentes alinhados a alto uso e verifique se eles estão em uso

**Intenção**:

Localize qualquer público-alvo chamado de &quot;downloaders pesados&quot;, definido pelos limites mensais de uso de dados.

>[!NOTE]
>
>Na etapa anterior, você criou um novo público-alvo. Lembre-se de que levará 24 horas até que o público-alvo esteja disponível para o Assistente de IA para uso adicional. Em vez disso, você deve usar outro público já existente.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

![Agent Orchestrator](./images/ao30.png)

Você deverá ver isso. Agora você deseja ver todos os seus públicos-alvo e o quanto eles mudaram nos últimos dias.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
List how much these audiences changed over the last few days.
```

![Agent Orchestrator](./images/ao31.png)

Você deverá ver isso. Clique em **Mostrar mais**.

![Agent Orchestrator](./images/ao31a.png)

Você deverá ver isso. Clique em para fechar o painel direito.

![Agent Orchestrator](./images/ao31b.png)

Role para baixo um pouco para analisar as etapas executadas pelo Assistente de IA.

![Agent Orchestrator](./images/ao31c.png)

Já existem alguns públicos-alvo para &quot;downloads pesados&quot;. Vamos ver se elas já estão em uso.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Which of the above are used in a journey? 
```

![Agent Orchestrator](./images/ao50.png)

Você verá algo semelhante a isso.

![Agent Orchestrator](./images/ao51.png)

Agora você deve verificar se essa jornada está ativa. Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Are these journeys active? 
```

![Agent Orchestrator](./images/ao52.png)

Você verá algo semelhante a isso. Nenhuma dessas jornadas está em execução no momento.

![Agent Orchestrator](./images/ao53.png)

Para o próximo lançamento do Fiber Max, você deve criar uma nova jornada.

## 1.1.1.9 Criar nova Jornada para lançamento de máximo de fibra

**Intenção**:

Criar uma nova jornada direcionada ao público-alvo composto:

Preferência de SciFi para baixadores pesados.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

![Agent Orchestrator](./images/aocj1.png)

Você deverá ver isso. Insira `yes` e clique em gerar.

![Agent Orchestrator](./images/aocj2.png)

Você deverá ver isso. Insira `yes` e clique em gerar.

![Agent Orchestrator](./images/aocj3.png)

Você deverá ver isso. Digite `The first one` e clique em enviar.

![Agent Orchestrator](./images/aocj4.png)

Você deverá ver isso. Digite `yes` e clique em enviar.

![Agent Orchestrator](./images/aocj5.png)

Revise a resposta. Digite `yes` e clique em enviar.

![Agent Orchestrator](./images/aocj6.png)

Clique em **Revisão**.

![Agent Orchestrator](./images/aocj7.png)

Atualize o nome da jornada com seu LDAP para torná-lo exclusivo. Clique em **Salvar**.

![Agent Orchestrator](./images/aocj8.png)

Sua jornada foi criada no modo de rascunho.

![Agent Orchestrator](./images/aocj9.png)

## 1.1.1.10 Gerenciamento de Conflitos de Jornada

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
How can I manage journey conflicts?
```

![Agent Orchestrator](./images/aocj80.png)

Revise as informações.

![Agent Orchestrator](./images/aocj81.png)

Role para baixo e selecione as **Fontes** para descobrir que as informações são provenientes da Experience League.

![Agent Orchestrator](./images/aocj82.png)

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
List any conflicts for the journey +CitiSignal Fiber Max
```

Em seguida, selecione manualmente a jornada **CitiSignal - Fibre Max Launch Promotion** na lista.

![Agent Orchestrator](./images/aocj70.png)

Você deverá ver isso. Clique em **enviar**.

![Agent Orchestrator](./images/aocj70a.png)

Revise as informações de conflito da jornada.

![Agent Orchestrator](./images/aocj71.png)

Role para baixo para encontrar mais detalhes sobre conflitos de jornada.

![Agent Orchestrator](./images/aocj72.png)

## 1.1.1.11 Experimentos

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
How are the experiments performing for the journey named 'CitiSignal - Fiber Max Launch Promotion'?
```

![Agent Orchestrator](./images/aoea0.png)

Você deverá ver isso:

![Agent Orchestrator](./images/aoea1.png)

Role para baixo e clique em uma das sugestões. Clique em **enviar**.

>[!NOTE]
>
>As sugestões são dinâmicas, portanto, você deve esperar ver sugestões diferentes sempre que uma resposta for gerada. Suas sugestões provavelmente serão diferentes das sugestões mostradas nesta captura de tela.

![Agent Orchestrator](./images/aoea2.png)

Você deverá ver uma resposta detalhada relacionada à sugestão que foi escolhida.

![Agent Orchestrator](./images/aoea4.png)

Você concluiu este laboratório.

Voltar para [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}