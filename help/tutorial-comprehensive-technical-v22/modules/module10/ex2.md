---
title: Adobe Journey Optimizer - Configurar uma jornada baseada em lote
description: Nesta seção, você configurará uma jornada de email em lote para enviar um boletim informativo
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 761da5b4-682f-430b-951c-278302fc4c54
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 8%

---

# 10.2 Configurar uma jornada de boletim informativo em lote

Faça logon no Adobe Journey Optimizer acessando [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Você será redirecionado para o **Início**  no Journey Optimizer. Primeiro, certifique-se de usar a sandbox correta. A sandbox a ser usada é chamada de `--aepSandboxId--`. Para alterar de uma sandbox para outra, clique em **Produto de produção (VA7)** e selecione a sandbox na lista. Neste exemplo, a sandbox é chamada de **Ativação AEP FY22**. Você estará no **Início** exibição da sandbox `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

## 10.2.1 Criar jornada de boletim informativo

Agora você criará uma jornada baseada em lote. Ao contrário da jornada baseada em eventos do exercício anterior, que depende de eventos de experiência recebidos ou entradas de segmentos ou saídas para acionar uma jornada para um cliente específico, as jornadas baseadas em lote direcionam um segmento inteiro uma vez com conteúdo exclusivo, como boletins informativos, promoções pontuais ou informações genéricas, ou periodicamente com conteúdo semelhante enviado regularmente, como, por exemplo, campanhas de aniversário e lembretes.

No menu , acesse **Jornada** e clique em **Criar Jornada**.

![Journey Optimizer](./images/oc43.png)

No lado direito, você verá um formulário no qual será necessário especificar o nome e a descrição da jornada. Insira os seguintes valores:

- **Nome**: `--demoProfileLdap-- - Newsletter Journey`. Por exemplo: **vangeluw - Jornada do informativo**.
- **Descrição**: Informativo Mensal

Clique em **Ok**.

![Journey Optimizer](./images/batchj2.png)

Em **Orquestração**, arrastar e soltar **Ler segmento** na tela. Isso significa que, uma vez publicada, a jornada começará recuperando todo o público-alvo do segmento, que se torna o público-alvo da jornada e da mensagem. Clique em **Selecionar um segmento**.

![Journey Optimizer](./images/batchj3.png)

No **Escolher um segmento** pop-up, pesquise pelo ldap e selecione o segmento criado em [Módulo 6 - CDP em tempo real - Crie um segmento e execute ações](../module6/real-time-cdp-build-a-segment-take-action.md) nomeado `--demoProfileLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`. por exemplo: vangeluw - Interesse em TEUS FITNESS JACKSHIRT. Clique em **Salvar**.

![Journey Optimizer](./images/batchj5.png)

Clique em **Ok**.

![Journey Optimizer](./images/batchj6.png)

No menu esquerdo, encontre a variável **Ações** e arrastar e soltar uma **Email** ação na tela.

![Journey Optimizer](./images/batchj7.png)

Defina as **Categoria** para **Marketing** e selecione uma superfície de email que permita enviar emails. Nesse caso, a superfície do email a ser selecionada é **Email**. Certifique-se de que as caixas de seleção de **Cliques no email** e **aberturas de email** estão ativadas.

![ACOP](./images/journeyactions1eee.png)

A próxima etapa é criar a mensagem. Para fazer isso, clique em **Editar conteúdo**.

![ACOP](./images/journeyactions2.png)

Agora você vê isso. Clique no botão **Linha de assunto** campo de texto.

![Journey Optimizer](./images/batch4.png)

Insira este texto para a linha de assunto: `Luma Newsletter - your monthly update has arrived.`. Clique em **Salvar**.

![Journey Optimizer](./images/batch5.png)

Então você estará de volta. Clique em **Email Designer** para começar a criar o conteúdo do email.

![Journey Optimizer](./images/batch6.png)

Você verá isso. Clique em **Importar HTML**.

![Journey Optimizer](./images/batch7.png)

Na tela pop-up, será necessário arrastar e soltar o arquivo HTML do email. Você pode encontrar o template HTML [here](../../assets/html/ajo-newsletter.html.zip). Baixe o arquivo zip com o modelo HTML no computador local e descompacte no desktop.

![Journey Optimizer](./images/html1.png)

Arraste e solte o arquivo **ajo-newsletter.html** para fazer upload no Journey Optimizer. Clique em **Importar**.

![Journey Optimizer](./images/batch8.png)

Esse conteúdo de email está pronto para ser enviado, pois tem toda a personalização, imagem e texto esperados. Somente o espaço reservado da oferta fica vazio.

Você pode receber uma mensagem de erro: **Erro ao tentar buscar ativos**. Isso é vinculado à imagem no email.

![Journey Optimizer](./images/errorfetch.png)

Se você receber esse erro, selecione a imagem e clique no botão **Editar imagem** botão.

![Journey Optimizer](./images/errorfetch1.png)

Clique em **Assets Essentials** para voltar à biblioteca do AEM Assets Essentials.

![Journey Optimizer](./images/errorfetch2.png)

Você verá esse pop-up. Navegue até a pasta **ativos de habilitação** e selecione a imagem **luma-newsletterContent.png**. Clique em **Selecionar**.

![Journey Optimizer](./images/errorfetch3.png)

O email básico do informativo agora está pronto. Clique em **Salvar**.

![Journey Optimizer](./images/ready.png)

Volte para o painel de mensagens clicando no botão **seta** ao lado do texto da linha de assunto no canto superior esquerdo.

![Journey Optimizer](./images/batch9.png)

Clique na seta no canto superior esquerdo para retornar à jornada.

![Journey Optimizer](./images/oc79aeee.png)

Clique em **Ok** para fechar a ação de email.

![Journey Optimizer](./images/oc79beee.png)

A jornada do informativo agora está pronta para ser publicada. Antes de fazer isso, observe o **Agendar** seção na qual você pode deixar essa jornada de ser uma campanha única para uma campanha recorrente. Clique no botão **Agendar** botão.

![Journey Optimizer](./images/batchj12.png)

Você verá isso. Selecionar **Uma vez**.

![Journey Optimizer](./images/sch1.png)

Selecione uma data e hora na próxima hora para testar sua jornada. Clique em **Ok**.

>[!NOTE]
>
>A data e a hora de envio da mensagem devem estar dentro de mais de uma hora.

Clique em **Publicar**.

![Journey Optimizer](./images/batchj13.png)

Clique em **Publicar** novamente.

![Journey Optimizer](./images/batchj14.png)

Sua jornada básica do boletim informativo foi publicada. Sua mensagem de email do informativo será enviada conforme você a definiu em sua programação, e sua jornada parará assim que o último email for enviado.

![Journey Optimizer](./images/batchj14eee.png)

Terminou este exercício.

Próxima etapa: [10.3 Aplicar personalização em uma mensagem de email](./ex3.md)

[Voltar ao Módulo 10](./journeyoptimizer.md)

[Voltar para todos os módulos](../../overview.md)
