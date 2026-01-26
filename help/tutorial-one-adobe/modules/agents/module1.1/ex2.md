---
title: Adobe Marketing Agent para ChatGPT Enterprise
description: Adobe Marketing Agent para ChatGPT Enterprise
kt: 5342
doc-type: tutorial
source-git-commit: 44d0e98ae4c7568411cb0e01ed8eff38b4a34137
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# 1.1.2 Adobe Marketing Agent para ChatGPT Enterprise

>[!IMPORTANT]
>
>Este laboratório usa um recurso que ainda não foi lançado. O recurso ainda está sendo desenvolvido e, portanto, ainda não está disponível para o público geral.

[!BADGE Em Desenvolvimento]

+++Em detalhes de desenvolvimento
Ao usar o Adobe Marketing Agent para ChatGPT Enterprise Beta, você reconhece que a Beta é fornecida &quot;no estado em que se encontra&quot; sem garantias de nenhum tipo. A Adobe não tem nenhuma obrigação de manter, corrigir, atualizar, alterar, modificar ou oferecer suporte à Beta. É recomendável ter cuidado e não depender de forma alguma do funcionamento ou desempenho correto desse Beta e/ou dos materiais que o acompanham. O Beta é considerado Informações confidenciais da Adobe.  Qualquer &quot;Feedback&quot; (informação sobre o Beta incluindo, mas não se limitando a, problemas ou defeitos encontrados durante o uso do Beta, sugestões, melhorias e recomendações) fornecido por Você ao Adobe é atribuído ao Adobe, incluindo todos os direitos, cargos e interesses no e no Feedback.

+++

## Vídeo

Neste vídeo, você receberá uma explicação e uma demonstração de todas as etapas envolvidas neste exercício.

>[!VIDEO](https://video.tv.adobe.com/v/3478410?quality=12&learn=on)

## 1.1.2.1 Criar aplicativo personalizado no ChatGPT Enterprise para Adobe Marketing Agent

>[!NOTE]
>
>O uso do Adobe Marketing Agent no ChatGPT requer o seguinte:
>- uma versão paga do ChatGPT Enterprise da OpenAI
>- usar o cliente Web ChatGPT Enterprise

Vá para [https://chatgpt.com/](https://chatgpt.com/){target="_blank"} e faça logon usando os detalhes de sua conta. Depois de fazer logon, você deverá ver isso. Clique no seu nome de usuário.

![GPTchat](./images/chatgpt1.png)

Selecione **Configurações**.

![GPTchat](./images/chatgpt2.png)

Vá para **Aplicativos** e selecione **Configurações avançadas**.

![GPTchat](./images/chatgpt3.png)

Ative o **Modo de desenvolvedor** e clique em **Voltar**.

![GPTchat](./images/chatgpt4.png)

Clique em **Criar aplicativo**.

![GPTchat](./images/chatgpt5.png)

Preencha os campos desta forma:

- **Nome**: `Adobe Marketing Agent`
- **URL do Servidor MCP**: verifique com seu representante da Adobe
- **Autenticação**: `OAuth`

Marque a caixa de seleção **Entendo e desejo continuar**.

Clique em **Criar**.

![GPTchat](./images/chatgpt6.png)

O ChatGPT agora tentará se conectar à sua conta da Adobe. Selecione **Permitir acesso** e você terá que fazer logon com sua conta da Adobe.

![GPTchat](./images/chatgpt7.png)

Depois de fazer logon, você deve ver que seu Adobe Marketing Agent agora está conectado com êxito.

![GPTchat](./images/chatgpt8.png)

## 1.1.2.2 Definir contexto no Adobe Marketing Agent

Feche esta janela.

![Agent Orchestrator](./images/chatgpt9.png)

Você deverá ver isso. Clique no ícone **+**, vá para **Mais** e selecione **Adobe Marketing Agent**.

![Agent Orchestrator](./images/chatgpt10.png)

Antes de interagir mais com o Adobe Marketing Agent por meio do ChatGPT, o contexto precisa ser definido.

Para este exercício, o contexto precisa ser definido para usar:

- **Sandbox**: **Prod - Acelerar (VA7)**

A configuração de sandbox ajuda a identificar qual sandbox o ChatGPT deve observar ao fazer perguntas.

- **Dataview**: **Acelerar B2C 2026**

A configuração Exibição de dados ajuda a identificar a exibição de dados que o ChatGPT deve considerar ao fazer perguntas.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
list sandboxes
```

![Agent Orchestrator](./images/chatgpt11.png)

Você deverá ver uma lista semelhante de sandboxes disponíveis. A sandbox atual neste exemplo está definida como **prod**.

Para alterar para a sandbox que precisa ser usada, insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
switch to sandbox accelerate
```

![Agent Orchestrator](./images/chatgpt12.png)

Você deverá ver isso. Clique em **Definir Contexto**.

![Agent Orchestrator](./images/chatgpt13.png)

Você deverá ver isso. Insira o seguinte **Prompt** e clique no botão **enviar** para definir a exibição de dados a ser usada.

```javascript
list dataviews
```

![Agent Orchestrator](./images/chatgpt14.png)

Você deverá ver uma lista semelhante de exibições de dados disponíveis.

Para definir a exibição de dados que precisa ser usada, insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
switch to Accelerate 2026 B2C
```

![Agent Orchestrator](./images/chatgpt15.png)

Você deverá ver isso. Clique em **Definir Contexto**.

![Agent Orchestrator](./images/chatgpt16.png)

Você deverá ver isso.

![Agent Orchestrator](./images/chatgpt17.png)

Seu contexto agora está definido corretamente, portanto, você pode começar a enviar prompts específicos em seguida.

## 1.1.2.3 Comece com as tendências gerais de compra para ancorar o contexto e ampliar a fibra

**Propósito**

Obtenha pulsos de alto nível conforme a demanda da categoria — móvel, telefone fixo, Internet, TV, fibra — especificamente pelos últimos 60 dias. Isso define linhas de base para sazonalidade, efeitos promocionais e variação regional após a implantação em Nova York.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Show me purchases by mainCategory over the last 2 months.
```

![Agent Orchestrator](./images/chatgpt18.png)

Você deverá ver isso:

![Agent Orchestrator](./images/chatgpt19.png)

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Show me purchases by mainCategory = Fiber over the last 2 months per week
```

![Agent Orchestrator](./images/chatgpt20.png)

Você verá isso, que detalha tendências específicas de fibra.

![Agent Orchestrator](./images/chatgpt21.png)

## 1.1.2.4 Correlacionar pedidos com preferências de conteúdo

**Propósito**

Teste a hipótese de que uma preferência por um gênero específico (por exemplo, ficção científica, esportes, drama) prevê o comportamento de atualização da banda larga, especialmente para necessidades de alta largura de banda.

Primeiro, você precisa descobrir qual campo é usado para armazenar a preferência de gênero.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Which field is used to store the preferred genre in the sandbox accelerate?
```

![Agent Orchestrator](./images/chatgpt22.png)

Você deverá ver isso, que mostra que o campo usado para o gênero é **_experienceplatform.individualCharacteristics.references.preferredGenre**.

![Agent Orchestrator](./images/chatgpt23.png)

Com essas informações, você pode começar a detalhar os dados de compra.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/chatgpt24.png)

Você deverá ver isso. Clique em **Pesquisa**.

![Agent Orchestrator](./images/chatgpt25.png)

Você deverá ver isso.

![Agent Orchestrator](./images/chatgpt26.png)

Role para baixo para ver mais informações.

![Agent Orchestrator](./images/chatgpt27.png)

## 1.1.2.5 Identificar Jornadas de Fibra Existentes

**Propósito**

Descubra quais jornadas ativas ou concluídas recentemente incluem &quot;Fibre&quot; no título, por exemplo, &quot;Fibre Upgrade NYC - Set&quot;, &quot;Fibre Trial - Streaming Bundle&quot;.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/chatgpt28.png)

Você deverá ver isso. Clique em **Pesquisa**.

![Agent Orchestrator](./images/chatgpt29.png)

Você deverá ver uma lista de jornadas.

![Agent Orchestrator](./images/chatgpt30.png)

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/chatgpt31.png)

Você deverá ver isso. Clique em **Pesquisa**.

![Agent Orchestrator](./images/chatgpt32.png)

Você deverá ver isso.

![Agent Orchestrator](./images/chatgpt33.png)

Role para baixo para ver mais detalhes.

![Agent Orchestrator](./images/chatgpt34.png)

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
show me the details of the journey 'CitiSignal - Fiber Max Launch Promotion'
```

![Agent Orchestrator](./images/chatgpt35.png)

Você deverá ver isso.

![Agent Orchestrator](./images/chatgpt36.png)

## 1.1.2.6 Validar o desempenho da jornada através da análise de fallout

**Propósito**

Você deseja entender o fallout de desempenho da jornada para saber se há nós ou condições na jornada que estão enfrentando uma grande porcentagem de perfis que estão sendo descartados. Isso é útil para entender se são necessários ajustes adicionais na jornada.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/chatgpt37.png)

Você deverá ver isso.

![Agent Orchestrator](./images/chatgpt38.png)

Role para baixo um pouco. Agora você pode revisar a tabela inspecionando cada nó e seus respectivos números de entrada, números de fallout e taxa de fallout.

![Agent Orchestrator](./images/chatgpt39.png)

Role para baixo um pouco mais para ver observações e recomendações.

![Agent Orchestrator](./images/chatgpt40.png)

Você concluiu este laboratório.

Voltar para [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}