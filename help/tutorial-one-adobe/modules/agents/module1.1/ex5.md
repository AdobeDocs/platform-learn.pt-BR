---
title: Adobe Marketing Agent para Claude
description: Adobe Marketing Agent para Claude
kt: 5342
doc-type: tutorial
source-git-commit: e476d5b516dcbe0f094eb2dfc38f4985798ecc3b
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 1%

---

# 1.1.5 Adobe Marketing Agent para Claude

[!BADGE Beta]

+++Detalhes do Beta
Ao usar o Adobe Marketing Agent com Claude Beta, você reconhece que o Beta é fornecido &quot;no estado em que se encontra&quot; sem garantias de nenhum tipo. A Adobe não tem nenhuma obrigação de manter, corrigir, atualizar, alterar, modificar ou oferecer suporte à Beta. É recomendável ter cuidado e não depender de forma alguma do funcionamento ou desempenho correto desse Beta e/ou dos materiais que o acompanham. O Beta é considerado Informações confidenciais da Adobe.  Qualquer &quot;Feedback&quot; (informação sobre o Beta incluindo, mas não se limitando a, problemas ou defeitos encontrados durante o uso do Beta, sugestões, melhorias e recomendações) fornecido por Você ao Adobe é atribuído ao Adobe, incluindo todos os direitos, cargos e interesses no e no Feedback.

+++

## Pré-requisitos

Para seguir as etapas neste laboratório conforme documentado abaixo, o seguinte acesso é necessário:

- Acesso ao Real-Time CDP, Journey Optimizer e Customer Journey Analytics
- Acesso ao Assistente de IA no Adobe Experience Cloud
- Acesso ao AEP Agent Orchestrator
- Acesso a Claude

## Vídeo

Neste vídeo, você receberá uma explicação e uma demonstração de todas as etapas envolvidas neste exercício.

>[!VIDEO](https://video.tv.adobe.com/v/3482212?quality=12&learn=on)

Este laboratório está em desenvolvimento.

## 1.1.5.1 Criar aplicativo personalizado no Claude.ai para o CJA

>[!NOTE]
>
>O uso do Adobe Marketing Agent no Claude.ai exige o seguinte:
>- uma versão paga do Claude.ai

Vá para [https://claude.ai/](https://claude.ai/){target="_blank"} e faça logon usando os detalhes de sua conta. Depois de fazer logon, você deverá ver isso.

![Claude.ai](./images/claude1.png)

Clique para abrir sua conta e selecione **Configurações**.

![Claude.ai](./images/claude2.png)

Vá para **Connectors** e clique em **Ir para Personalizar**.

![Claude.ai](./images/claude2a.png)

Clique em **+** e selecione **Adicionar conector personalizado**.

![Claude.ai](./images/claude3.png)

Preencha os campos desta forma:

- **Nome**: `Adobe Marketing Agent`
- **URL do Servidor MCP**: verifique com seu representante da Adobe

Clique em **Adicionar**.

![Claude.ai](./images/claude4.png)

Você deverá ver isso. Clique em **+** para iniciar um novo chat.

![Claude.ai](./images/claude5.png)

Clique no ícone **+**, vá para **Connectors** e verifique se o **Adobe Marketing Agent** está habilitado**.

![Claude.ai](./images/claude6.png)

## 1.1.5.2 Autenticar e definir contexto

Antes de interagir mais com o Adobe Marketing Agent por meio do Claude.ai, é necessário fazer logon e definir o contexto.

Digite o prompt a seguir e clique em **enviar**.

```
login to Adobe Marketing Agent
```

![Claude.ai](./images/claude7.png)

Selecione **Sempre permitir**.

![Claude.ai](./images/claude8.png)

Clique no link para fazer login no Adobe Marketing Agent**.

![Claude.ai](./images/claude8a.png)

Clique em **Abrir link**.

![Claude.ai](./images/claude8b.png)

Clique em **Permitir acesso**.

![Claude.ai](./images/claude8c.png)

Depois de autenticar com êxito, você deve ver isso. Volte para Claude.

![Claude.ai](./images/claude8d.png)

Digite o seguinte comando e clique em **enviar**.

```javascript
logged in
```

![Claude.ai](./images/claude8e.png)

Agora você está conectado com êxito. A próxima etapa é definir o contexto. Digite o prompt a seguir e clique em **enviar**.


```javascript
change context
```

![Claude.ai e CJA](./images/claude9.png)

Selecione **Organização**. Você também pode repetir esse comando para alterar a sandbox e a visualização de dados posteriormente.

![Claude.ai e CJA](./images/claude10.png)

Insira o nome da sua instância e clique em **enviar**.

![Claude.ai e CJA](./images/claude11.png)

Selecione **Sempre permitir**.

![Claude.ai e CJA](./images/claude12.png)

Você deveria ver algo assim.

![Claude.ai e CJA](./images/claude13.png)

Se a sandbox ainda não estiver definida corretamente, você poderá usar o seguinte comando para alterar para a sandbox que precisa usar. Clique em **enviar**. Como alternativa, você pode usar o comando `change context` acima e selecionar **sandbox**

```javascript
change sandbox to --aepSandboxName--
```

![Claude.ai e CJA](./images/claude14.png)

Se a visualização de dados ainda não estiver definida corretamente, você poderá usar o seguinte comando para alterar para a sandbox que precisa usar (substitua XXX no comando abaixo pelo nome da visualização de dados). Clique em **enviar**. Como alternativa, você pode usar o comando `change context` acima e selecionar **exibição de dados**

```javascript
change dataview to XXX
```

![Claude.ai e CJA](./images/claude15.png)

Depois que a **Organização**, a **Sandbox** e a **Exibição de Dados** estiverem definidas corretamente, você estará pronto para começar a fazer perguntas à Adobe Marketing Agent.

## Próximas etapas

Voltar para [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
