---
title: Introdução ao Agent Orchestrator
description: Introdução ao Agent Orchestrator
kt: 5342
doc-type: tutorial
source-git-commit: dee5b0855eeeb455bf22f511d11cd13f7e904889
workflow-type: tm+mt
source-wordcount: '1112'
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

- **Source de Documentação**: **Customer Journey Analytics**
- **Sandbox**: **Acelerar**
- **Dataview**: **Acelerar B2C 2026**

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

**Ação**: observe a curva de crescimento e os picos regionais.

![Agent Orchestrator](./images/ao7.png)

## 1.1.1.3 Correlacionar pedidos com preferências de conteúdo

**Propósito**

Teste a hipótese de que a preferência de conteúdo (por exemplo, ficção científica, esportes, drama) prevê o comportamento de atualização da banda larga, especialmente para as necessidades de banda larga.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/ao8.png)

Você deverá ver isso:

![Agent Orchestrator](./images/ao9.png)

## 1.1.1.4 Identificar Jornadas de Fibra Existentes

**Propósito**

Descubra quais jornadas ativas ou concluídas recentemente incluem &quot;Fibre&quot; no título, por exemplo, &quot;Fibre Upgrade NYC - Set&quot;, &quot;Fibre Trial - Streaming Bundle&quot;.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/ao12.png)

Você deverá ver isso:

![Agent Orchestrator](./images/ao13.png)

Listar jornadas ativas ou passadas com mensagens por fibra.

Ação: selecione jornadas de alto desempenho para clonagem.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/ao14.png)

Você deverá ver isso:

![Agent Orchestrator](./images/ao15.png)

## 1.1.1.5 Verifique a propagação

**Intenção**:

Entenda a definição inicial da jornada &quot;CitiSignal - Promoção de inicialização máxima de fibra&quot; — quais características impulsionaram o direcionamento (por exemplo, &quot;Preferência de gênero SciFi&quot;, &quot;4+ dispositivos&quot;, &quot;fluxo ≥ 300 GB/mês&quot;).

Insira o seguinte **Prompt** e digite **+CitiSignal fib** para habilitar o preenchimento automático. Selecione a jornada **CitiSignal - Fibre Max Launch Promotion**.

```javascript
What was the initial audience in the journey named 
```

![Agent Orchestrator](./images/ao16.png)

Você deverá ver isso. Clique no botão **enviar**.

![Agent Orchestrator](./images/ao17.png)

Você deverá ver isso.

![Agent Orchestrator](./images/ao18.png)

## 1.1.1.6 Validar o desempenho da jornada através da análise de fallout

**Propósito**

Criar uma funnel em etapas no Customer Journey Analytics

Entregue → Aberto → Clicado → Desembarcado → Exibição do produto → Adicionar ao carrinho → Check-out → Pedido concluído

Inclua exibições de SKU relacionadas a fibra como uma ramificação.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/ao19.png)

## 1.1.1.7 Criar um novo público

**Propósito**

Com base nas descobertas acima, há uma correlação entre clientes que consomem muitos dados e que têm um gênero preferido de ficção científica ou fantasia. Agora você combinará esses atributos em um público-alvo.

Ir para [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Insira o seguinte **Prompt** e clique no botão **enviar**.

>[!NOTE]
>
>Verifique se o contexto do assistente aponta para a sandbox **Accelerate** e a exibição de dados **Accelerate 2026 B2C**

```javascript
Create an audience that combines people with an average download per month of over 2000 GB and a preferred genre of sci-fi or fantasy.
```

![Agent Orchestrator](./images/ao32.png)

Revise o plano. Insira `yes` e clique em **enviar**.

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
>Ao criar um novo público-alvo, levará 24 horas até que ele esteja disponível para o assistente para uso adicional.

## 1.1.1.8 Encontre públicos-alvo existentes alinhados a alto uso e verifique se eles estão em uso

**Intenção**:

Localize qualquer público-alvo chamado de &quot;downloaders pesados&quot;, definido pelos limites mensais de uso de dados.

>[!NOTE]
>
>Na guia anterior, você criou um novo público-alvo. Lembre-se de que levará 24 horas até que o público-alvo esteja disponível para o assistente para uso adicional. Em vez disso, você deve usar outro público já existente.

Ir para [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Você deverá ver isso. Verifique se você está na organização **Experience Platform International**.

Insira o seguinte **Prompt** e clique no botão **enviar**.

>[!NOTE]
>
>Verifique se o contexto do assistente aponta para a sandbox **Accelerate** e a exibição de dados **Accelerate 2026 B2C**

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

![Agent Orchestrator](./images/ao30.png)

Você deverá ver isso.

![Agent Orchestrator](./images/ao31.png)

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
Which of the above are used in a journey? 
```

![Agent Orchestrator](./images/ao52.png)

Você verá algo semelhante a isso. Essa jornada não está sendo executada no momento.

![Agent Orchestrator](./images/ao53.png)

Para o próximo lançamento do Fiber Max, você deve criar uma nova jornada.

## 1.1.1.9 Criar nova Jornada para lançamento de máximo de fibra

**Intenção**:

Criar uma nova jornada direcionada ao público-alvo composto:

Preferência de SciFi de Heavy Downloaders ∩ (chave de público kbaa_5207bf).

Ir para [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Você deverá ver isso. Verifique se você está na organização **Experience Platform International**.

Insira o seguinte **Prompt** e clique no botão **enviar**.

>[!NOTE]
>
>Verifique se o contexto do assistente aponta para a sandbox **Accelerate** e a exibição de dados **Accelerate 2026 B2C**

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

![Agent Orchestrator](./images/aocj1.png)

Você deverá ver isso. Insira `yes` e clique em gerar.

![Agent Orchestrator](./images/aocj2.png)

Você deverá ver isso. Insira `yes` e clique em gerar.

![Agent Orchestrator](./images/aocj3.png)

Você deverá ver isso. Insira `The first one` e clique em gerar.

![Agent Orchestrator](./images/aocj4.png)

Você deverá ver isso. Insira `yes` e clique em gerar.

![Agent Orchestrator](./images/aocj5.png)

Revise a resposta. Insira `yes` e clique em gerar.

![Agent Orchestrator](./images/aocj6.png)

Clique em **Revisão**.

![Agent Orchestrator](./images/aocj7.png)

Atualize o nome da jornada com seu LDAP para torná-lo exclusivo. Clique em **Salvar**.

![Agent Orchestrator](./images/aocj8.png)

Sua jornada foi criada no modo de rascunho.

![Agent Orchestrator](./images/aocj9.png)

## 1.1.1.10 Gerenciamento de Conflitos de Jornada

Ir para [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Você deverá ver isso. Verifique se você está na organização **Experience Platform International**.

Insira o seguinte **Prompt** e clique no botão **enviar**.

>[!NOTE]
>
>Verifique se o contexto do assistente aponta para a origem da documentação **Journey Optimizer**, a sandbox **Accelerate** e a exibição de dados **Accelerate 2026 B2C**

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
List any conflicts for "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/aocj70.png)

Revise as informações de conflito da jornada.

![Agent Orchestrator](./images/aocj71.png)

Role para baixo para encontrar mais detalhes sobre conflitos de jornada.

![Agent Orchestrator](./images/aocj72.png)

## 1.1.1.11 Experimentos

Ir para [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Você deverá ver isso. Verifique se você está na organização **Experience Platform International**.

Insira o seguinte **Prompt** e clique no botão **enviar**.

>[!NOTE]
>
>Verifique se o contexto do assistente aponta para a sandbox **Accelerate** e a exibição de dados **Accelerate 2026 B2C**

```javascript
How are the experiments performing for the journey named 'CitiSignal - Fiber Max Launch Promotion'?
```

![Agent Orchestrator](./images/aoea0.png)

Você deverá ver isso:

![Agent Orchestrator](./images/aoea1.png)

Clique na sugestão para comparar as taxas de conversão de cada tratamento e, em seguida, clique em **enviar**.

![Agent Orchestrator](./images/aoea2.png)

Você deverá ver uma comparação detalhada como esta:

![Agent Orchestrator](./images/aoea4.png)

Voltar para [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}