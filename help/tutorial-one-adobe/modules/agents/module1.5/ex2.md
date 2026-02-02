---
title: CJA & Claude.ai com servidor MCP
description: CJA & Claude.ai com servidor MCP
kt: 5342
doc-type: tutorial
source-git-commit: b8906d1995dcb470789be2a1297eb48cb7690a9c
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---

# 1.5.2 CJA &amp; Claude.ai com servidor MCP

[!BADGE Alpha]

+++Detalhes do Alpha
Ao usar o CJA &amp; Claude.ai com o servidor MCP Alpha, você reconhece que a Alpha é fornecida &quot;no estado em que se encontra&quot; sem garantias de nenhum tipo. A Adobe não tem nenhuma obrigação de manter, corrigir, atualizar, alterar, modificar ou oferecer suporte à Alpha. É recomendável ter cuidado e não depender de forma alguma do funcionamento ou desempenho correto desse Alpha e/ou dos materiais que o acompanham. O Alpha é considerado Informações confidenciais da Adobe. Qualquer &quot;Feedback&quot; (informação sobre o Alpha incluindo, mas não se limitando a, problemas ou defeitos encontrados durante o uso do Alpha, sugestões, melhorias e recomendações) fornecido por Você ao Adobe é atribuído ao Adobe, incluindo todos os direitos, cargos e interesses no e no Feedback.

+++


>[!NOTE]
>
>Este exercício sobre a configuração e o uso de um Servidor MCP com o Claude.ai para conexão com o CJA está relacionado a este exercício [1.1 Customer Journey Analytics: Crie um painel usando o Analysis Workspace sobre o Adobe Experience Platform](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/customer-journey-analytics-build-a-dashboard.md). A visualização de dados e a conexão do CJA que está sendo usada no exercício abaixo são a visualização de dados e a conexão configuradas nesse exercício. Se quiser replicar os resultados abaixo, siga essas instruções primeiro.

## Vídeo

Neste vídeo, você receberá uma explicação e uma demonstração de todas as etapas envolvidas neste exercício.

>[!VIDEO](https://video.tv.adobe.com/v/3479159?quality=12&learn=on)

## 1.5.1.1 Criar aplicativo personalizado no Claude.ai para o CJA

>[!NOTE]
>
>O uso do CJA no Claude.ai exige o seguinte:
>- uma versão paga do Claude.ai
>- usar o cliente da Web Claude.ai

Vá para [https://claude.ai/](https://claude.ai/){target="_blank"} e faça logon usando os detalhes de sua conta. Depois de fazer logon, você deverá ver isso. Clique no ícone **+**.

![Claude.ai](./images/claude1.png)

Selecione **Adicionar conectores**.

![Claude.ai](./images/claude2.png)

Clique em **adicionar um personalizado**.

![Claude.ai](./images/claude3.png)

Preencha os campos desta forma:

- **Nome**: `CJA`
- **URL do Servidor MCP**: verifique com seu representante da Adobe

Clique em **Adicionar**.

![Claude.ai](./images/claude4.png)

Você deverá ver isso. Clique em **Adicionar**.

![Claude.ai](./images/claude5.png)

Depois de autenticado com êxito, você deve ver isso. Clique no ícone **+** para iniciar um novo chat.

![Claude.ai](./images/claude6.png)

Vá para **+**, para **Conectores** e você deve ver que o conector **CJA** agora está habilitado.

![Claude.ai](./images/claude8.png)

Agora você está pronto para iniciar sua análise de dados.

![Claude.ai](./images/claude7.png)


## 1.5.1.2 Definir contexto no CJA

Antes de interagir mais com o CJA por meio do Claude.ai, o contexto precisa ser definido.

Para este exercício, o contexto precisa ser definido para usar:

- **Dataview**: **—aepUserLdap— - Visualização de Dados Omnichannel**

A configuração Exibição de dados ajuda a identificar a exibição de dados que o Claude.ai deve examinar ao fazer perguntas.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
list dataviews
```

![Claude.ai e CJA](./images/claude9.png)

Selecione **Sempre permitir**.

![Claude.ai e CJA](./images/claude10.png)

Você deverá ver uma lista semelhante de exibições de dados disponíveis.

![Claude.ai e CJA](./images/claude11.png)

Para alterar para a exibição de dados que precisa ser usada, insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
switch to dataview --aepUserLdap-- - Omnichannel Data View
```

![Claude.ai e CJA](./images/claude11a.png)

Selecione **Sempre permitir**.

![Claude.ai e CJA](./images/claude12.png)

Você deverá ver isso.

![Claude.ai e CJA](./images/claude16.png)

Seu contexto agora está definido corretamente, portanto, você pode começar a enviar prompts específicos em seguida.

## 1.5.1.3 Explorar a exibição de dados

>[!NOTE]
>
>A exibição de dados sendo usada aqui foi configurada como parte do exercício [Criar uma exibição de dados](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md).

Insira o seguinte **Prompt** e clique no botão **enviar** para explorar quais métricas e dimensões estão disponíveis para você.

```javascript
list the available metrics and dimensions
```

![Claude.ai e CJA](./images/claude101.png)

Selecione **Sempre permitir** duas vezes, uma vez para recuperar **métricas** e outra vez para recuperar **dimensões**.

![Claude.ai e CJA](./images/claude101a.png)

Você deverá ver essa resposta, que inclui as métricas e dimensões configuradas como parte do exercício [Criar uma exibição de dados](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md).

![Claude.ai e CJA](./images/claude102.png)

## Tabela de forma livre 1.5.1.4 - Exibições do produto

Agora você pode começar a explorar os dados. Comece inserindo o prompt abaixo e clique em **enviar** para enviar sua solicitação de relatório.

```javascript
how many product views happened on January 21, 2026?
```

![Claude.ai e CJA](./images/claude103.png)

Selecione **Sempre permitir**.

![Claude.ai e CJA](./images/claude104.png)

Você deverá ver uma resposta como essa.

![Claude.ai e CJA](./images/claude105.png)

Agora é possível detalhar a resposta adicionando uma dimensão. Insira o seguinte **prompt** e clique no botão **enviar**.

```javascript
break down product views by product name
```

![Claude.ai e CJA](./images/claude106.png)

Você deverá ver uma resposta como essa.

![Claude.ai e CJA](./images/claude107.png)

Agora você também pode criar uma visualização. Insira o seguinte **prompt** e clique no botão **enviar**.

```javascript
create a line visualization by hour for product views on January 21
```

![Claude.ai e CJA](./images/claude108.png)

Você deverá ver isso.

![Claude.ai e CJA](./images/claude109.png)

Agora você também pode baixar este gráfico de linhas. Insira o seguinte **prompt** e clique no botão **enviar**.

```javascript
export this chart to PNG
```

![Claude.ai e CJA](./images/claude113.png)

Você deverá ver isso. Clique em **Baixar**.

![Claude.ai e CJA](./images/claude114.png)

Em seguida, você pode abrir o PNG baixado e usá-lo em outros documentos.

![Claude.ai e CJA](./images/claude114a.png)

Insira o seguinte **prompt** e clique no botão **enviar**.

```javascript
can you breakdown product views by user agent?
```

![Claude.ai e CJA](./images/claude115.png)

Você deverá ver isso.

![Claude.ai e CJA](./images/claude117.png)

## Visualização de fallout de 1.5.1.5

Insira o seguinte **prompt** e clique no botão **enviar**.

```javascript
can you create a fallout visualization for the product interaction funnel, starting with all traffic and then in the next steps add Product Views, Add to Cart and purchases?
```

![Claude.ai e CJA](./images/claude118.png)

Você deve ver algo como isso, que inclui uma visualização gerada por Claude.ai com base nos dados fornecidos pelo Customer Journey Analytics.

![Claude.ai e CJA](./images/claude119.png)

Voltar para [Analytics e Agentes](./analyticsagents.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}