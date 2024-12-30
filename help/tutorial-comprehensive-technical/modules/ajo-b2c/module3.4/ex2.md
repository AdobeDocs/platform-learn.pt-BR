---
title: Adobe Journey Optimizer - Configurar uma jornada baseada em lote
description: Nesta seção, você configurará uma jornada de email em lote para enviar um informativo
kt: 5342
doc-type: tutorial
exl-id: 52b2e019-e408-4160-87b7-2aabd0f3c68f
source-git-commit: c531412a2c0a5c216f49560e01fb26b9b7e71869
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 1%

---

# 3.4.2 Configurar uma jornada de boletim informativo baseada em lote

Faça login no Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`. Para alterar a sandbox, clique em **Produção (VA7)** e selecione a sandbox na lista. Neste exemplo, a sandbox é chamada de **AEP Enablement FY22**. Você estará na exibição **Página inicial** da sua sandbox `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acoptriglp.png)

## 3.4.2.1 Criar jornada de informativo

Agora você criará uma jornada baseada em lote. Ao contrário da jornada baseada em eventos do exercício anterior, que depende de eventos de experiência de entrada, entradas de público-alvo ou saídas para acionar uma jornada para um cliente específico, as jornadas baseadas em lote têm como alvo um público-alvo inteiro, uma vez com conteúdo exclusivo, como boletins informativos, promoções únicas ou informações genéricas ou periodicamente com conteúdo semelhante enviado regularmente, como por exemplo campanhas de aniversário e lembretes.

No menu, vá para **Jornadas** e clique em **Criar Jornada**.

![Journey Optimizer](./images/oc43.png)

No lado direito, você verá um formulário em que precisa especificar o nome e a descrição da jornada. Insira os seguintes valores:

- **Nome**: `--aepUserLdap-- - Newsletter Journey`. Por exemplo: **vangeluw - Jornada do informativo**.
- **Descrição**: informativo mensal

Clique em **Ok**.

![Journey Optimizer](./images/batchj2.png)

Em **Orquestração**, arraste e solte **Ler público-alvo** na tela. Isso significa que, uma vez publicada, a jornada começará recuperando todo o público-alvo, que se tornará o público-alvo da jornada e da mensagem. Clique em **Selecionar uma audiência**.

![Journey Optimizer](./images/batchj3.png)

No pop-up **Escolher um público-alvo**, pesquise pelo seu ldap e selecione o público-alvo criado no [Módulo 2.3 - CDP em tempo real - Criar um público-alvo e executar a ação](./../../../modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md) chamada `--aepUserLdap-- - Interest in Galaxy S24`. Clique em **Salvar**.

![Journey Optimizer](./images/batchj5.png)

Clique em **Ok**.

![Journey Optimizer](./images/batchj6.png)

No menu esquerdo, localize a seção **Ações** e arraste e solte na tela uma ação de **Email**.

![Journey Optimizer](./images/batchj7.png)

Defina a **Categoria** como **Marketing** e selecione uma superfície de email que permita o envio de emails. Nesse caso, a superfície de email a ser selecionada é **Email**. Verifique se as caixas de seleção para **Cliques no email** e **aberturas de email** estão habilitadas.

![ACOP](./images/journeyactions1eee.png)

A próxima etapa é criar a mensagem. Para fazer isso, clique em **Editar conteúdo**.

![ACOP](./images/journeyactions2.png)

Agora vocês podem ver isso. Clique no campo de texto **Linha de assunto**.

![Journey Optimizer](./images/batch4.png)

Digite este texto para a linha de assunto: `Luma Newsletter - your monthly update has arrived.`. Clique em **Salvar**.

![Journey Optimizer](./images/batch5.png)

Você estará de volta aqui. Clique em **Enviar Designer por email** para começar a criar o conteúdo do email.

![Journey Optimizer](./images/batch6.png)

Você verá isso. Clique em **Importar HTML**.

![Journey Optimizer](./images/batch7.png)

Na tela pop-up, será necessário arrastar e soltar o arquivo HTML do email. Você pode encontrar o modelo de HTML [aqui](./../../../assets/html/ajo-newsletter.html.zip). Baixe o arquivo zip com o modelo de HTML para o computador local e descompacte em seu desktop.

![Journey Optimizer](./images/html1.png)

Arraste e solte o arquivo **ajo-newsletter.html** para carregá-lo no Journey Optimizer. Clique em **Importar**.

![Journey Optimizer](./images/batch8.png)

Esse conteúdo de email está pronto para ser enviado, pois tem toda a personalização, imagens e texto esperados. Somente o espaço reservado da oferta fica vazio.

Você pode receber uma mensagem de erro: **Erro ao tentar buscar ativos**. Isso é vinculado à imagem no email.

![Journey Optimizer](./images/errorfetch.png)

Se você receber este erro, selecione a imagem e clique no botão **Editar imagem**.

![Journey Optimizer](./images/errorfetch1.png)

Clique em **Assets Essentials** para voltar para a biblioteca do AEM Assets Essentials.

![Journey Optimizer](./images/errorfetch2.png)

Você então verá esse pop-up. Navegue até a pasta **enablement-assets** e selecione a imagem **luma-newsletterContent.png**. Clique em **Selecionar**.

![Journey Optimizer](./images/errorfetch3.png)

O email básico do informativo agora está pronto. Clique em **Salvar**.

![Journey Optimizer](./images/ready.png)

Volte para o painel da mensagem clicando na **seta** ao lado do texto da linha de assunto no canto superior esquerdo.

![Journey Optimizer](./images/batch9.png)

Clique na seta no canto superior esquerdo para voltar à jornada.

![Journey Optimizer](./images/oc79aeee.png)

Clique em **Ok** para fechar sua ação de email.

![Journey Optimizer](./images/oc79beee.png)

A jornada do informativo agora está pronta para ser publicada. Antes de fazer isso, observe a seção **Agenda**, na qual você pode alternar essa jornada de campanha única para recorrente. Clique no botão **Agendar**.

![Journey Optimizer](./images/batchj12.png)

Você verá isso. Selecione **Uma Vez**.

![Journey Optimizer](./images/sch1.png)

Selecione uma data e hora na próxima hora para testar a jornada. Clique em **Ok**.

>[!NOTE]
>
>A data e a hora de envio da mensagem devem estar dentro de mais de uma hora.

Clique em **Publish**.

![Journey Optimizer](./images/batchj13.png)

Clique novamente em **Publish**.

![Journey Optimizer](./images/batchj14.png)

A jornada básica do informativo agora está publicada. A mensagem de email do informativo será enviada conforme você a definiu na programação, e a jornada será interrompida assim que o último email for enviado.

![Journey Optimizer](./images/batchj14eee.png)

Você concluiu este exercício.

Próxima Etapa: [3.4.3 Aplicar personalização em uma mensagem de email](./ex3.md)

[Voltar ao módulo 3.4](./journeyoptimizer.md)

[Voltar a todos os módulos](../../../overview.md)
