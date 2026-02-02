---
title: CJA e ChatGPT com servidor MCP
description: CJA e ChatGPT com servidor MCP
kt: 5342
doc-type: tutorial
source-git-commit: 5eb5432251ee7193909ed4ec7decd0d94d0843a2
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 0%

---

# 1.5.1 CJA e ChatGPT com servidor MCP

[!BADGE Alpha]

+++Detalhes do Alpha
Ao usar o CJA &amp; Claude.ai com o servidor MCP Alpha, você reconhece que a Alpha é fornecida &quot;no estado em que se encontra&quot; sem garantias de nenhum tipo. A Adobe não tem nenhuma obrigação de manter, corrigir, atualizar, alterar, modificar ou oferecer suporte à Alpha. É recomendável ter cuidado e não depender de forma alguma do funcionamento ou desempenho correto desse Alpha e/ou dos materiais que o acompanham. O Alpha é considerado Informações confidenciais da Adobe. Qualquer &quot;Feedback&quot; (informação sobre o Alpha incluindo, mas não se limitando a, problemas ou defeitos encontrados durante o uso do Alpha, sugestões, melhorias e recomendações) fornecido por Você ao Adobe é atribuído ao Adobe, incluindo todos os direitos, cargos e interesses no e no Feedback.

+++

>[!NOTE]
>
>Este exercício sobre como configurar e usar um Servidor MCP com ChatGPT para se conectar ao CJA está relacionado a este exercício [1.1 Customer Journey Analytics: Crie um painel usando o Analysis Workspace sobre o Adobe Experience Platform](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/customer-journey-analytics-build-a-dashboard.md). A visualização de dados e a conexão do CJA que está sendo usada no exercício abaixo são a visualização de dados e a conexão configuradas nesse exercício. Se quiser replicar os resultados abaixo, siga essas instruções primeiro.

## Vídeo

Neste vídeo, você receberá uma explicação e uma demonstração de todas as etapas envolvidas neste exercício.

>[!VIDEO](https://video.tv.adobe.com/v/3479159?quality=12&learn=on)

## 1.5.1.1 Criar aplicativo personalizado no ChatGPT para CJA

>[!NOTE]
>
>O uso do CJA no ChatGPT requer o seguinte:
>- uma versão paga do ChatGPT do OpenAI
>- usar o cliente Web ChatGPT

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

- **Nome**: `CJA`
- **URL do Servidor MCP**: verifique com seu representante da Adobe
- **Autenticação**: `OAuth`

Marque a caixa de seleção **Entendo e desejo continuar**.

Clique em **Criar**.

![GPTchat](./images/chatgpt6.png)

Depois de fazer logon com êxito, você deve ver que seu aplicativo CJA agora está conectado com êxito.

![GPTchat](./images/chatgpt8.png)

## 1.5.1.2 Definir contexto no CJA

Feche esta janela.

![ChatGPT e CJA](./images/chatgpt9.png)

Você deverá ver isso. Clique no ícone **+**, vá para **Mais** e selecione **CJA**.

![ChatGPT e CJA](./images/chatgpt10.png)

Antes de interagir mais com o CJA por meio do ChatGPT, o contexto precisa ser definido.

Para este exercício, o contexto precisa ser definido para usar:

- **Dataview**: **—aepUserLdap— - Visualização de Dados Omnichannel**

A configuração Exibição de dados ajuda a identificar a exibição de dados que o ChatGPT deve considerar ao fazer perguntas.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
list dataviews
```

![ChatGPT e CJA](./images/chatgpt11.png)

Você deverá ver uma lista semelhante de exibições de dados disponíveis.

![ChatGPT e CJA](./images/chatgpt11a.png)

Para alterar para a exibição de dados que precisa ser usada, insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
switch to dataview --aepUserLdap-- - Omnichannel Data View
```

![ChatGPT e CJA](./images/chatgpt12.png)

Você deverá ver isso.

![ChatGPT e CJA](./images/chatgpt16.png)

Seu contexto agora está definido corretamente, portanto, você pode começar a enviar prompts específicos em seguida.

## 1.5.1.3 Explorar a exibição de dados

>[!NOTE]
>
>A exibição de dados sendo usada aqui foi configurada como parte do exercício [Criar uma exibição de dados](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md).

Insira o seguinte **Prompt** e clique no botão **enviar** para explorar quais métricas e dimensões estão disponíveis para você.

```javascript
list the available metrics and dimensions
```

![ChatGPT e CJA](./images/chatgpt101.png)

Você deverá ver essa resposta, que inclui as métricas e dimensões configuradas como parte do exercício [Criar uma exibição de dados](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md).

![ChatGPT e CJA](./images/chatgpt102.png)

## Tabela de forma livre 1.5.1.4 - Exibições do produto

Agora você pode começar a explorar os dados. Comece inserindo o prompt abaixo e clique em **enviar** para enviar sua solicitação de relatório.

```javascript
how many product views happened on January 21?
```

![ChatGPT e CJA](./images/chatgpt103.png)

Selecione **RunReport**.

![ChatGPT e CJA](./images/chatgpt104.png)

Você deverá ver uma resposta como essa.

![ChatGPT e CJA](./images/chatgpt105.png)

Agora é possível detalhar a resposta adicionando uma dimensão. Insira o seguinte **prompt** e clique no botão **enviar**.

```javascript
break down product views by product name
```

![ChatGPT e CJA](./images/chatgpt106.png)

Você deverá ver uma resposta como essa.

![ChatGPT e CJA](./images/chatgpt107.png)

Agora você também pode criar uma visualização. Insira o seguinte **prompt** e clique no botão **enviar**.

```javascript
create a line visualization by hour for product views on January 21
```

![ChatGPT e CJA](./images/chatgpt108.png)

Selecione **UpsertProject**.

![ChatGPT e CJA](./images/chatgpt109.png)

Selecione **RunReport**.

![ChatGPT e CJA](./images/chatgpt110.png)

Você deverá ver isso.

![ChatGPT e CJA](./images/chatgpt111.png)

Role para baixo.

![ChatGPT e CJA](./images/chatgpt112.png)

Agora você também pode baixar este gráfico de linhas. Insira o seguinte **prompt** e clique no botão **enviar**.

```javascript
export this chart to PNG
```

![ChatGPT e CJA](./images/chatgpt113.png)

Você deverá ver isso. Clique em **Baixar o PNG**.

![ChatGPT e CJA](./images/chatgpt114.png)

Insira o seguinte **prompt** e clique no botão **enviar**.

```javascript
can you breakdown product views by user agent?
```

![ChatGPT e CJA](./images/chatgpt115.png)

Selecione **RunReport**.

![ChatGPT e CJA](./images/chatgpt116.png)

Você deverá ver isso.

![ChatGPT e CJA](./images/chatgpt117.png)

## Visualização de fallout de 1.5.1.5

Insira o seguinte **prompt** e clique no botão **enviar**.

```javascript
can you create a fallout visualization for the product interaction funnel, starting with all traffic and then in the next steps add Product Views, Add to Cart and purchases?
```

![ChatGPT e CJA](./images/chatgpt118.png)

Selecione **UpsertProject**.

![ChatGPT e CJA](./images/chatgpt119.png)

Selecione **RunReport**.

![ChatGPT e CJA](./images/chatgpt120.png)

Você deveria ver algo assim. Insira o seguinte **prompt** e clique no botão **enviar**.

```javascript
can you show me a visualization of the above fallout analysis?
```

![ChatGPT e CJA](./images/chatgpt120a.png)

Clique em **Baixar o PNG**.

![ChatGPT e CJA](./images/chatgpt121.png)

Agora você verá a visualização da análise de fallout.

![ChatGPT e CJA](./images/chatgpt122.png)

Próxima etapa: [CJA &amp; Claude.ai com servidor MCP](./ex2.md){target="_blank"}

Voltar para [Analytics e Agentes](./analyticsagents.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}