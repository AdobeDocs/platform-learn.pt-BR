---
title: Adobe Analytics & Claude.ai com servidor MCP
description: Adobe Analytics & Claude.ai com servidor MCP
kt: 5342
doc-type: tutorial
source-git-commit: 44559d6278da4bed8a864d0faf092352b8370398
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# 1.5.3 Adobe Analytics &amp; Claude.ai com servidor MCP

[!BADGE Alpha]

+++Detalhes do Alpha
Ao usar o CJA &amp; Claude.ai com o servidor MCP Alpha, você reconhece que a Alpha é fornecida &quot;no estado em que se encontra&quot; sem garantias de nenhum tipo. A Adobe não tem nenhuma obrigação de manter, corrigir, atualizar, alterar, modificar ou oferecer suporte à Alpha. É recomendável ter cuidado e não depender de forma alguma do funcionamento ou desempenho correto desse Alpha e/ou dos materiais que o acompanham. O Alpha é considerado Informações confidenciais da Adobe. Qualquer &quot;Feedback&quot; (informação sobre o Alpha incluindo, mas não se limitando a, problemas ou defeitos encontrados durante o uso do Alpha, sugestões, melhorias e recomendações) fornecido por Você ao Adobe é atribuído ao Adobe, incluindo todos os direitos, cargos e interesses no e no Feedback.

+++

## Vídeo

Neste vídeo, você receberá uma explicação e uma demonstração de todas as etapas envolvidas neste exercício.

>[!VIDEO](https://video.tv.adobe.com/v/3479562?quality=12&learn=on)

## 1.5.3.1 Criar aplicativo personalizado no Claude.ai para o Adobe Analytics

>[!NOTE]
>
>O uso do Adobe Analytics no Claude.ai exige o seguinte:
>- uma versão paga do Claude.ai
>- usar o cliente da Web Claude.ai

Vá para [https://claude.ai/](https://claude.ai/){target="_blank"} e faça logon usando os detalhes de sua conta. Depois de fazer logon, você deverá ver isso. Clique no ícone **+**.

![Claude.ai](./images/claudeaa1.png)

Selecione **Adicionar conectores**.

![Claude.ai](./images/claudeaa2.png)

Clique em **adicionar um personalizado**.

![Claude.ai](./images/claudeaa3.png)

Preencha os campos desta forma:

- **Nome**: `CJA`
- **URL do Servidor MCP**: verifique com seu representante da Adobe

Clique em **Adicionar**.

![Claude.ai](./images/claudeaa4.png)

Você deverá ver isso. Clique em **Conectar**.

![Claude.ai](./images/claudeaa5.png)

Depois de autenticado com êxito, você deve ver isso. Clique no ícone **+** para iniciar um novo chat.

![Claude.ai](./images/claudeaa6.png)

Vá para **+**, para **Conectores** e você deve ver que o conector **Adobe Analytics** agora está habilitado.

![Claude.ai](./images/claudeaa7.png)

Agora você está pronto para iniciar sua análise de dados.

![Claude.ai](./images/claudeaa8.png)

## 1.5.3.2 Definir contexto no Adobe Analytics

Antes de interagir mais com o CJA por meio do Claude.ai, o contexto precisa ser definido.

Para este exercício, o contexto precisa ser definido para usar:

- **Conjunto de relatórios**: **CID - Dados de demonstração**

A configuração do Conjunto de relatórios ajuda a identificar quais dados o Claude.ai deve examinar ao fazer perguntas.

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
list report suites
```

![Claude.ai](./images/claudeaa9.png)

Selecione **Sempre permitir**.

![Claude.ai](./images/claudeaa10.png)

Selecione **Sempre permitir**.

![Claude.ai](./images/claudeaa11.png)

Você deveria ver algo assim.

![Claude.ai](./images/claudeaa12.png)

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
use report suite CID Demo Data
```

![Claude.ai](./images/claudeaa13.png)

Selecione **Sempre permitir**.

![Claude.ai](./images/claudeaa14.png)

O conjunto de relatórios foi selecionado.

![Claude.ai](./images/claudeaa15.png)

## 1.5.2.3 Explorar o conjunto de relatórios

Insira o seguinte **Prompt** e clique no botão **enviar** para explorar quais métricas e dimensões estão disponíveis para você.

```javascript
list the available metrics and dimensions
```

![Claude.ai e CJA](./images/claudeaa101.png)

Selecione **Sempre permitir**.

![Claude.ai e CJA](./images/claudeaa102.png)

Selecione **Sempre permitir** novamente.

![Claude.ai e CJA](./images/claudeaa103.png)

Você deve ver essa resposta, que inclui as métricas e dimensões configuradas nesse conjunto de relatórios.

![Claude.ai e CJA](./images/claudeaa104.png)

## 1.5.2.4 Relatórios

Agora você pode começar a explorar os dados. Comece inserindo o prompt abaixo e clique em **enviar** para enviar sua solicitação de relatório.

```javascript
show me pageviews for Feb 2?
```

![Claude.ai e CJA](./images/claudeaa105.png)

Você deveria ver algo assim.

![Claude.ai e CJA](./images/claudeaa106.png)

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
break down pageviews by page name
```

![Claude.ai e CJA](./images/claudeaa107.png)

Você deverá ver isso.

![Claude.ai e CJA](./images/claudeaa108.png)

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
give me an overview of page names, page views by marketing channel
```

![Claude.ai e CJA](./images/claudeaa109.png)

Você deveria ver algo assim.

![Claude.ai e CJA](./images/claudeaa110.png)

Role para baixo um pouco para ver a análise.

![Claude.ai e CJA](./images/claudeaa111.png)

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
Analyze different metrics by marketing channel
```

![Claude.ai e CJA](./images/claudeaa112.png)

Você deveria ver algo assim.

![Claude.ai e CJA](./images/claudeaa113.png)

Insira o seguinte **Prompt** e clique no botão **enviar**.

```javascript
which tracking codes drove the most visits and purchases?
```

![Claude.ai e CJA](./images/claudeaa114.png)

Você verá algo assim, primeiro mostrando **Principais Códigos de Rastreamento por Visitas**.

![Claude.ai e CJA](./images/claudeaa115.png)

Você pode ver os códigos de rastreamento que geraram mais compras no relatório **Principais códigos de rastreamento por pedidos (compras)**.

![Claude.ai e CJA](./images/claudeaa116.png)

E você encontrará insights adicionais fornecidos pelo Claude.ai com base nos dados provenientes do Adobe Analytics.

![Claude.ai e CJA](./images/claudeaa117.png)

Você terminou este exercício agora.

Voltar para [Analytics e Agentes](./analyticsagents.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}