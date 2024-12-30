---
title: Adobe Journey Optimizer - Aplicar personalização em uma mensagem de email
description: Este exercício explica como usar a personalização de segmentos em um conteúdo de email
kt: 5342
doc-type: tutorial
exl-id: bb5f8130-0237-4381-bc1e-f6b62950b1fc
source-git-commit: c531412a2c0a5c216f49560e01fb26b9b7e71869
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 1%

---

# 3.4.3 Aplicar personalização em uma mensagem de email

Faça login no Adobe Experience Cloud em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Adobe Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepTenantId--``.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acoptriglp.png)

## 3.4.3.1 Personalização baseada em segmentos

Neste exercício, você melhorará a mensagem de email do seu informativo com um texto personalizado com base na associação do segmento.

Vá para **Jornada**. Localize a jornada do informativo criada no exercício anterior. Pesquisar por `--aepUserLdap-- - Newsletter`. Clique na jornada para abri-la.

![Journey Optimizer](./images/sbp1.png)

Você verá isso. Clique em **Duplicate**.

![Journey Optimizer](./images/sbp2.png)

Clique em **Duplicate**.

![Journey Optimizer](./images/sbp3.png)

Selecione sua ação **Email** e clique em **Editar conteúdo**.

![Journey Optimizer](./images/sbp3a.png)

Clique em **Designer de email**.

![Journey Optimizer](./images/sbp4.png)

Você verá isso.

![Journey Optimizer](./images/sbp5.png)

Abra os **Componentes do Conteúdo** e arraste um componente **Texto** abaixo do conteúdo do informativo atual.

![Journey Optimizer](./images/sbp6.png)

Selecione todo o texto padrão e exclua. Em seguida, clique no botão **Adicionar personalização** na barra de ferramentas.

![Journey Optimizer](./images/sbp7.png)

Você verá isto:

![Journey Optimizer](./images/seg1.png)

No menu esquerdo, clique em **Associações de segmento**.

![Journey Optimizer](./images/seg2.png)

>[!NOTE]
>
>Se você não conseguir encontrar o segmento nessa lista, role para baixo um pouco para encontrar instruções sobre como recuperar a ID do segmento manualmente.

Selecione o segmento `Luma - Women's Category Interest` e clique no ícone **+**, que deve ter esta aparência:

![Journey Optimizer](./images/seg3.png)

Em seguida, você deve deixar a primeira linha como está e substituir as linhas 2 e 3 por este código:

``
    Psssst... a private sale in the women category will launch soon, we will keep you posted
{%else%}
    Thanks for taking the time to read our newsletter. Here is a 10% promo code to use on the website: READER10
{%/if%}
``

Você terá isto:

![Journey Optimizer](./images/seg4.png)

Clique em **Validar** para verificar se o código está correto. Clique em **Salvar**.

![Journey Optimizer](./images/sbp8.png)

Agora você pode salvar esta mensagem clicando no botão **Salvar** no canto superior direito. Em seguida, clique em **Simular conteúdo**.

![Journey Optimizer](./images/sbp9.png)

Selecione um dos perfis que você criou como parte deste tutorial e clique em **Visualizar**. Você verá o resultado da sua configuração.

![Journey Optimizer](./images/sbp10.png)

Você verá isso. Em seguida, clique em **Fechar**.

![Journey Optimizer](./images/sbp10fff.png)

Volte para o painel da mensagem clicando na **seta** ao lado do texto da linha de assunto no canto superior esquerdo.

![Journey Optimizer](./images/sbp11.png)

Clique na seta no canto superior esquerdo para voltar à jornada.

![Journey Optimizer](./images/oc79afff.png)

Clique em **Ok** para fechar sua ação de email.

![Journey Optimizer](./images/oc79bfff.png)

Altere seu **Calendário** para **Uma Vez** e defina uma **Data/Hora**. Clique em **Ok**.

>[!NOTE]
>
>A data e a hora de envio da mensagem devem estar dentro de mais de uma hora.

![Journey Optimizer](./images/sbp18.png)

Clique no botão **Publish** na jornada.

![Journey Optimizer](./images/sbp19.png)

Na janela pop-up, clique novamente em **Publish**.

![Journey Optimizer](./images/sbp20.png)

A jornada básica do informativo agora está publicada. A mensagem de email do informativo será enviada de acordo com a sua programação. A jornada será interrompida assim que o último email for enviado.

![Journey Optimizer](./images/sbp20fff.png)

Você concluiu este exercício.

Próxima Etapa: [3.4.4 Configurar e usar notificações por push para iOS](./ex4.md)

[Voltar ao módulo 3.4](./journeyoptimizer.md)

[Voltar a todos os módulos](../../../overview.md)
