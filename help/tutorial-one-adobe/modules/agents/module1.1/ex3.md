---
title: Adobe Marketing Agent for Microsoft 365 Copilot
description: Adobe Marketing Agent para Microsoft 365 CopilotCopilot
kt: 5342
doc-type: tutorial
exl-id: 9cab0e72-4d46-46ee-8dee-e5ca83889523
source-git-commit: 312af1518edd28b4eee577e4ab6b97943a56538d
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 0%

---

# 1.1.3 Adobe Marketing Agent for Microsoft 365 Copilot

## Pré-requisitos

Para seguir as etapas neste laboratório conforme documentado abaixo, o seguinte acesso é necessário:

- Acesso ao Real-Time CDP, Journey Optimizer e Customer Journey Analytics
- Acesso ao Assistente de IA no Adobe Experience Cloud
- Acesso ao AEP Agent Orchestrator
- Acesso ao Microsoft 365 Copilot

## Vídeo

Neste vídeo, você receberá uma explicação e uma demonstração de todas as etapas envolvidas neste exercício.

>[!VIDEO](https://video.tv.adobe.com/v/3479158?quality=12&learn=on)

## 1.1.3.1 Adicionar o Adobe Marketing Agent ao Microsoft 365 Teams &amp; Copilot

Abra o Microsoft Teams e faça logon usando os detalhes da sua conta. Depois de fazer logon, você deverá ver isso.

Clique em **Aplicativos**.

![GPTchat](./images/copilot1.png)

Selecione **Gerenciar seus aplicativos**.

![GPTchat](./images/copilot2.png)

Selecione **Carregar um aplicativo**.

![GPTchat](./images/copilot3.png)

Selecione **Carregar um aplicativo personalizado**.

![GPTchat](./images/copilot4.png)

Selecione o arquivo de manifesto fornecido a você pelo seu instrutor e clique em **Abrir**.

![GPTchat](./images/copilot5.png)

Clique em **Adicionar**.

![GPTchat](./images/copilot6.png)

Clique em **Abrir com Copilot**.

![GPTchat](./images/copilot7.png)

O Adobe Marketing Agent foi carregado com êxito.

![GPTchat](./images/copilot8.png)

Digite o prompt `login` e clique no botão **enviar**.

![GPTchat](./images/copilotlogin1.png)

Clique em **Fazer logon no Adobe Marketing Agent**.

![GPTchat](./images/copilotlogin2.png)

Uma nova janela será aberta, solicitando que você faça logon usando as credenciais da sua conta da Adobe.

![GPTchat](./images/copilotlogin3.png)

Você verá um código semelhante sendo gerado. Clique em **Copiar** para copiar o código.

![GPTchat](./images/copilotlogin5.png)

Cole o código na janela do Adobe Marketing Agent no Copilot e clique no botão **enviar**.

![GPTchat](./images/copilotlogin6.png)

Você verá algo semelhante a isso. Agora você está conectado com êxito ao Adobe Marketing Agent no Microsoft 365 Copilot.

![GPTchat](./images/copilotlogin7.png)

## 1.1.3.2 Definir contexto no Adobe Marketing Agent

Antes de interagir mais com o Adobe Marketing Agent por meio do Copilot, o contexto precisa ser definido.

Para este exercício, o contexto precisa ser definido para usar:

- **Sandbox**: **Prod - One Adobe (VA7)**

  A configuração de sandbox ajuda a identificar qual assistente de IA de sandbox deve observar ao fazer perguntas.

- **Dataview**: **AdobeOne - Visualização unificada de dados do cliente**

  A configuração da visualização de dados ajuda a identificar qual assistente da IA de visualização de dados deve considerar ao fazer perguntas.

Primeiro, altere a sandbox para a sandbox correta e clique em **Atualizar exibições de dados**.

![Agent Orchestrator](./images/copilotlogin7a.png)

Em seguida, selecione a exibição de dados correta e clique em **Atualizar**.

![Agent Orchestrator](./images/copilot9.png)

Você deverá ver isso. O contexto agora está definido corretamente para que você possa começar a enviar prompts específicos em seguida.

![Agent Orchestrator](./images/copilot13.png)

## 1.1.3.3 Comece com as tendências gerais de compra para ancorar o contexto e ampliar a fibra

**Propósito**

Obtenha pulsos de alto nível conforme a demanda da categoria — móvel, telefone fixo, Internet, TV, fibra — especificamente pelos últimos 60 dias. Isso define linhas de base para sazonalidade, efeitos promocionais e variação regional após a implantação em Nova York.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```
Show me purchases by mainCategory over the last 2 months.
```

![Agent Orchestrator](./images/copilot18.png)

Você deverá ver isso:

![Agent Orchestrator](./images/copilot19.png)

Insira o seguinte **Prompt** e clique no botão **enviar**.

```
Show me purchases by mainCategory = Fiber over the last 2 months broken down by week
```

![Agent Orchestrator](./images/copilot20.png)

Você verá isso, que detalha tendências específicas de fibra.

![Agent Orchestrator](./images/copilot21.png)

## 1.1.3.4 Correlacionar pedidos com preferências de conteúdo

**Propósito**

Teste a hipótese de que uma preferência por um gênero específico (por exemplo, ficção científica, esportes, drama) prevê o comportamento de atualização da banda larga, especialmente para necessidades de alta largura de banda.

Primeiro, você precisa descobrir qual campo é usado para armazenar a preferência de gênero.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```
Which field is used to store the preferred genre
```

![Agent Orchestrator](./images/copilot22.png)

Você verá isto, que mostra que o campo usado para o gênero é **`--aepTenantId--.individualCharacteristics.telco.mediaPreferences.favouriteGenre`**.

![Agent Orchestrator](./images/copilot23.png)

Com essas informações, você pode começar a detalhar os dados de compra.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```
Show me purchases by preferred genre for the last 2 months until today
```

![Agent Orchestrator](./images/copilot24.png)

Você deverá ver isso. Clique em **Exibir Dados**.

![Agent Orchestrator](./images/copilot25.png)

Você deverá ver isso.

![Agent Orchestrator](./images/copilot26.png)

## 1.1.3.5 Identificar Jornadas de Fibra Existentes

**Propósito**

Descubra quais jornadas ativas ou concluídas recentemente incluem &quot;Fibre&quot; no título, por exemplo, &quot;Fibre Upgrade NYC - Set&quot;, &quot;Fibre Trial - Streaming Bundle&quot;.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```
What journeys exist? 
```

![Agent Orchestrator](./images/copilot28.png)

Você deverá ver uma lista de jornadas.

![Agent Orchestrator](./images/copilot29.png)

Insira o seguinte **Prompt** e clique no botão **enviar**.

```
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/copilot31.png)

Você deverá ver isso.

![Agent Orchestrator](./images/copilot33.png)

Insira o seguinte **Prompt** e clique no botão **enviar**.

```
Show me the details of the journey 'CitiSignal - Fiber Max Launch Promotion'
```

![Agent Orchestrator](./images/copilot35.png)

Você deverá ver isso.

![Agent Orchestrator](./images/copilot36.png)

## 1.1.3.6 Validar o desempenho da jornada através da análise de fallout

**Propósito**

Você deseja entender o fallout de desempenho da jornada para saber se há nós ou condições na jornada que estão enfrentando uma grande porcentagem de perfis que estão sendo descartados. Isso é útil para entender se são necessários ajustes adicionais na jornada.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/copilot37.png)

Você deverá ver isso.

![Agent Orchestrator](./images/copilot38.png)

Role para baixo um pouco mais para ver observações e recomendações.

![Agent Orchestrator](./images/copilot40.png)

Você concluiu este laboratório.

## Próximas etapas

Ir para [Adobe Marketing Agent para Google Gemini Enterprise](./ex4.md){target="_blank"}

Voltar para [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
