---
title: Adobe Journey Optimizer - Aplicar personalização em uma mensagem de email
description: Este exercício explica como usar a personalização de segmentos em um conteúdo de email
kt: 5342
doc-type: tutorial
exl-id: a1ad649e-d0c4-4e87-b784-1e2d99f34a2e
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 1%

---

# 3.4.3 Aplicar personalização baseada em segmentos em uma mensagem de email

Faça login no Adobe Experience Cloud em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Adobe Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepTenantId--``.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## 3.4.3.1 Personalização baseada em segmentos

Neste exercício, você melhorará a mensagem de email do informativo criada no exercício anterior com um texto personalizado com base na associação do segmento.

Vá para **Campanhas**. Localize a jornada do informativo criada no exercício anterior. Pesquisar por `--aepUserLdap-- - CitiSignal Newsletter`. Clique com o botão direito do mouse nos 3 pontos **...** e clique em **Duplicar**.

![Journey Optimizer](./images/sbp1.png)

Você verá isso. Use isso para o **Título**: `--aepUserLdap-- - CitiSignal Newsletter (SBP)`. Clique em **Duplicate**.

![Journey Optimizer](./images/sbp2.png)

Clique na campanha duplicada para abri-la.

![Journey Optimizer](./images/sbp3.png)

Clique em **Editar** para alterar o conteúdo.

![Journey Optimizer](./images/sbp3a.png)

Clique em **Editar corpo do email**.

![Journey Optimizer](./images/sbp4.png)

Você verá isso.

![Journey Optimizer](./images/sbp5.png)

Abra o **Content Components** e arraste uma **coluna 1:1** acima da oferta do AirPods.

![Journey Optimizer](./images/sbp6.png)

Arraste e solte um componente **Texto** nessa coluna 1:1.

![Journey Optimizer](./images/sbp6a.png)

Selecione todo o texto padrão e exclua. Em seguida, clique no botão **Adicionar personalização** na barra de ferramentas.

![Journey Optimizer](./images/sbp7.png)

Você verá isso. No menu esquerdo, clique em **Públicos-alvo**.

![Journey Optimizer](./images/seg1.png)

Selecione o segmento `--aepUserLdap-- - Interest in Plans` e clique no ícone **+** para adicioná-lo à tela.

![Journey Optimizer](./images/seg3.png)

Em seguida, você deve deixar a primeira linha como está e substituir as linhas 2 e 3 por este código:

&grave;&grave;
    PS: It may be a good idea to check if your plan still meets your needs! Click here to be contacted by one of our experts!
{%else%}
    PS: Thanks for taking the time to read our newsletter. Here is a 10% promo code to use on the website: NEWSLETTER10
{%/if%}
&grave;&grave;

Então você terá isto. Clique em **Salvar**.

![Journey Optimizer](./images/seg4.png)

Altere o alinhamento do texto para **Alinhamento central**.

![Journey Optimizer](./images/sbp9.png)

Agora você pode salvar esta mensagem clicando no botão **Salvar** no canto superior direito. Em seguida, clique em **seta** ao lado do texto da linha de assunto no canto superior esquerdo.

![Journey Optimizer](./images/sbp9a.png)

Clique em **Revisar para ativar**.

![Journey Optimizer](./images/oc79afff.png)

Clique em **Ativar**.

![Journey Optimizer](./images/oc79bfff.png)

Seu informativo com personalização baseada em segmentos foi publicado. A mensagem de email do informativo será enviada de acordo com a sua programação. A jornada será interrompida assim que o último email for enviado.

Se você se qualificar para o segmento que foi usado, verá isso no email que receberá:

![Journey Optimizer](./images/sbp20fff.png)

Você concluiu este exercício.

## Próximas etapas

Ir para [3.4.4 Instalação e usar notificações por push para iOS](./ex4.md){target="_blank"}

Voltar para [Adobe Journey Optimizer](journeyoptimizer.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
