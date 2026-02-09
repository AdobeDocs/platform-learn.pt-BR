---
title: Usar seu modelo de mídia dinâmica com o Adobe Journey Optimizer
description: Usar seu modelo de mídia dinâmica com o Adobe Journey Optimizer
kt: 5342
doc-type: tutorial
source-git-commit: 261475b85bfb15f7e9f630d1c5203732c2d4c254
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# 1.4.2 Usar seu modelo de mídia dinâmica com o Adobe Journey Optimizer

## 1.4.2.1 Crie sua campanha no Adobe Journey Optimizer

Faça login no Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`. Você estará na exibição **Página inicial** da sua sandbox `--aepSandboxName--`.

![ACOP](./images/acoptriglp.png)

Agora você criará uma campanha. Ao contrário da jornada baseada em eventos do exercício anterior, que depende de eventos de experiência de entrada, entradas de público-alvo ou saídas para acionar uma jornada para um cliente específico, as campanhas direcionam todo um público-alvo uma vez com conteúdo exclusivo, como boletins informativos, promoções únicas ou informações genéricas ou periodicamente com conteúdo semelhante enviado regularmente, como por exemplo campanhas de aniversário e lembretes.

No menu, vá para **Campanhas** e clique em **Criar campanha**.

![Journey Optimizer](./images/gsemail21.png)

Selecione **Agendado - Marketing** e clique em **Criar**.

![Journey Optimizer](./images/gsemail22.png)

Na tela de criação da campanha, configure o seguinte:

- **Nome**: `--aepUserLdap-- - CitiSignal Fiber Max DM Email Campaign`.

Clique em **Ações**.

![Journey Optimizer](./images/gsemail23.png)

Clique em **+ Adicionar ação** e selecione **Email**.

![Journey Optimizer](./images/gsemail24.png)

Em seguida, selecione uma **configuração de email** existente e clique em **Editar conteúdo**.

![Journey Optimizer](./images/gsemail25.png)

Você verá isso. Para a **Linha de assunto**, use esta:

```
{{profile.person.name.firstName}}, say hello to CitiSignal Fiber Max!
```

Em seguida, clique em **Editar conteúdo**.

![Journey Optimizer](./images/gsemail26.png)

Selecione **Design do zero**.

![Journey Optimizer](./images/gsemail27.png)

Você deverá ver isso.

![Journey Optimizer](./images/gsemail28.png)

Adicionar 2x **1:1 coluna** à tela.

![Journey Optimizer](./images/gsemail29.png)

Vá para **Fragmentos**, arraste o fragmento **cabeçalho** para a primeira coluna:1 e arraste o fragmento **rodapé** para a segunda coluna:1.

![Journey Optimizer](./images/gsemail30.png)

Adicione uma nova coluna 1:1 entre os 2 fragmentos e adicione uma **Imagem** nessa coluna 1:1. Em seguida, clique em **Procurar**.

![Journey Optimizer](./images/gsemail31.png)

Navegue até a pasta em que você armazenou o modelo do Dynamic Media. Selecione seu modelo do Dynamic Media e clique em **Selecionar**.

![Journey Optimizer](./images/gsemail32.png)

Você deverá ver isso.

![Journey Optimizer](./images/gsemail33.png)

## Próximas etapas

Voltar para [Adobe Experience Manager Assets e Dynamic Media](./aemassetsdm.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
