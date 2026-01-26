---
title: Adobe Marketing Agent com o Microsoft Copilot
description: Adobe Marketing Agent com o Microsoft Copilot
kt: 5342
doc-type: tutorial
source-git-commit: 1eafbf27de93b45288bec8cb3cd70f04e8cc715e
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 0%

---

# 1.1.3 Adobe Marketing Agent com Microsoft Copilot

[!BADGE Beta]

+++Ver detalhes
Ao usar o Adobe Marketing Agent com o Microsoft Copilot Beta, você reconhece que o Beta é fornecido &quot;no estado em que se encontra&quot; sem garantias de nenhum tipo. A Adobe não tem nenhuma obrigação de manter, corrigir, atualizar, alterar, modificar ou oferecer suporte à Beta. É recomendável ter cuidado e não depender de forma alguma do funcionamento ou desempenho correto desse Beta e/ou dos materiais que o acompanham. O Beta é considerado Informações confidenciais da Adobe.  Qualquer &quot;Feedback&quot; (informação sobre o Beta incluindo, mas não se limitando a, problemas ou defeitos encontrados durante o uso do Beta, sugestões, melhorias e recomendações) fornecido por Você ao Adobe é atribuído ao Adobe, incluindo todos os direitos, cargos e interesses no e no Feedback.

+++

>[!IMPORTANT]
>
>Este laboratório usa um recurso que ainda não foi lançado. O recurso ainda está sendo desenvolvido e, portanto, ainda não está disponível para o público geral.

## Pré-requisitos

Para seguir as etapas neste laboratório conforme documentado abaixo, o seguinte acesso é necessário:

- Acesso ao Real-Time CDP, Journey Optimizer e Customer Journey Analytics
- Acesso ao Assistente de IA no Adobe Experience Cloud
- Acesso ao AEP Agent Orchestrator
- Acesso ao Microsoft Copilot

## Vídeo

Neste vídeo, você receberá uma explicação e uma demonstração de todas as etapas envolvidas neste exercício.

>[!VIDEO](https://video.tv.adobe.com/v/3479158?quality=12&learn=on)

## 1.1.3.1 Adicionar o Adobe Marketing Agent ao Microsoft Teams e Copilot

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

Após a autenticação bem-sucedida, talvez seja necessário selecionar a instância específica que deseja usar. Se você vir essa tela, selecione a instância —aepImsOrgName—.

![GPTchat](./images/copilotlogin4.png)

Você verá um código semelhante sendo gerado. Clique em **Copiar** para copiar o código.

![GPTchat](./images/copilotlogin5.png)

Cole o código na janela do Adobe Marketing Agent no Copilot e clique no botão **enviar**.

![GPTchat](./images/copilotlogin6.png)

Você verá algo semelhante a isso. Agora você está conectado com sucesso ao Adobe Marketing Agent no Microsoft Copilot.

![GPTchat](./images/copilotlogin7.png)

## 1.1.3.2 Definir contexto no Adobe Marketing Agent

Antes de interagir mais com o Adobe Marketing Agent por meio do Copilot, o contexto precisa ser definido.

Para este exercício, o contexto precisa ser definido para usar:

- **Sandbox**: **Prod - Acelerar (VA7)**

  A configuração de sandbox ajuda a identificar qual assistente de IA de sandbox deve observar ao fazer perguntas.

- **Dataview**: **Acelerar B2C 2026**

  A configuração da visualização de dados ajuda a identificar qual assistente da IA de visualização de dados deve considerar ao fazer perguntas.

![Agent Orchestrator](./images/copilotlogin7.png)

Para alterar a sandbox, digite o seguinte comando e clique no botão **enviar**.

```javascript
change sandbox
```

![Agent Orchestrator](./images/copilot9.png)

Você verá algo semelhante a isso. Selecione a sandbox que você precisa usar e clique em **selecionar**.

![Agent Orchestrator](./images/copilot10.png)

Você deverá ver isso. Para alterar a exibição de dados, digite o seguinte comando e clique no botão **enviar**.

```javascript
change dataview
```

![Agent Orchestrator](./images/copilot11.png)

Você verá algo semelhante a isso. Selecione a exibição de dados que você precisa usar e clique em **selecionar**.

![Agent Orchestrator](./images/copilot12.png)

Você deverá ver isso. O contexto agora está definido corretamente para que você possa começar a enviar prompts específicos em seguida.

![Agent Orchestrator](./images/copilot13.png)

## 1.1.3.3 Comece com as tendências gerais de compra para ancorar o contexto e ampliar a fibra

**Propósito**

Obtenha pulsos de alto nível conforme a demanda da categoria — móvel, telefone fixo, Internet, TV, fibra — especificamente pelos últimos 60 dias. Isso define linhas de base para sazonalidade, efeitos promocionais e variação regional após a implantação em Nova York.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Show me purchases by mainCategory over the last 4 months.
```

![Agent Orchestrator](./images/copilot18.png)

Você deverá ver isso:

![Agent Orchestrator](./images/copilot19.png)

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Show me purchases by mainCategory = Fiber over the last 4 months broken down by week
```

![Agent Orchestrator](./images/copilot20.png)

Você verá isso, que detalha tendências específicas de fibra.

![Agent Orchestrator](./images/copilot21.png)

## 1.1.3.4 Correlacionar pedidos com preferências de conteúdo

**Propósito**

Teste a hipótese de que uma preferência por um gênero específico (por exemplo, ficção científica, esportes, drama) prevê o comportamento de atualização da banda larga, especialmente para necessidades de alta largura de banda.

Primeiro, você precisa descobrir qual campo é usado para armazenar a preferência de gênero.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Which field is used to store the preferred genre
```

![Agent Orchestrator](./images/copilot22.png)

Você deverá ver isso, que mostra que o campo usado para o gênero é **_experienceplatform.individualCharacteristics.references.preferredGenre**.

![Agent Orchestrator](./images/copilot23.png)

Com essas informações, você pode começar a detalhar os dados de compra.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Show me ordersYTD by preferredGenre for the last 4 months
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

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/copilot28.png)

Você deverá ver uma lista de jornadas.

![Agent Orchestrator](./images/copilot29.png)

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/copilot31.png)

Você deverá ver isso.

![Agent Orchestrator](./images/copilot33.png)

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Show me the details of the journey 'CitiSignal - Fiber Max Launch Promotion'
```

![Agent Orchestrator](./images/copilot35.png)

Você deverá ver isso.

![Agent Orchestrator](./images/copilot36.png)

## 1.1.3.6 Validar o desempenho da jornada através da análise de fallout

**Propósito**

Você deseja entender o fallout de desempenho da jornada para saber se há nós ou condições na jornada que estão enfrentando uma grande porcentagem de perfis que estão sendo descartados. Isso é útil para entender se são necessários ajustes adicionais na jornada.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/copilot37.png)

Você deverá ver isso.

![Agent Orchestrator](./images/copilot38.png)

Role para baixo um pouco mais para ver observações e recomendações. Clique nos 3 pontos **...** e selecione **Detalhes da Jornada** para abrir a jornada específica no Adobe Journey Optimizer.

![Agent Orchestrator](./images/copilot40.png)

Você deverá ver isso.

![Agent Orchestrator](./images/copilot41.png)

Você concluiu este laboratório.

Voltar para [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}