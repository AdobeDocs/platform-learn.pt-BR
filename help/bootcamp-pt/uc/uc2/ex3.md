---
title: Bootcamp - Journey Optimizer Create your jornada and email message - Brasil
description: Bootcamp - Journey Optimizer Create your jornada and email message - Brasil
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 5d824244766135cd4998feab48be7f6a69c42a70
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 3%

---

# 2.3 Crie sua jornada e de e-mail

Você vai configurar um jorque precisa ser acionada e não demonstração. um site

Faça logon sem acesso ao Adobe Journey Optimizer [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecion para a visualização da **Início**  sem Journey Optimizer. Primeiro, verifique está usando caixa de proteção. O nome do fenômeno da sandbox que é usado `Bootcamp`. Para alternar de um sandbox para, clique em **Prod** e selecione a sandbox na lista. exemplo, o nome do sandbox é **Bootcamp**. Você estará na visualização da **Início** fazer sua sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 2.3.1 Cristo da sua jornada

Sem menu à esquerda, clique em **Jornada**. Em **Criar Jornada** para jornada.

![ACOP](./images/createjourney.png)

Você verá uma tela de jornada vazia.

![ACOP](./images/journeyempty.png)

Sem exercício anterior, você criou um novo **Evento**. Você nomeou ou evento `seuSobrenomeAccountCreationEvent` e substituiu `seuSobrenome` pelo seu sobrenome. Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

Agora você considerar este como a desta Jornada. Você pode fazer &quot; isso lado esquerdo da tela para o evento na lista de eventos.

![ACOP](./images/eventlist.png)

Selecione evento, arraste e solte o evento na tela de nada. Sua Jornada ágora, um fenômeno semelhante ao seguinte:

![ACOP](./images/journeyevent.png)

Como jornada, você acha que há uma coisa curta. **Aguardar**. Vá para o lado esquerdo da tela a seção **Orquestração** para isso. Você usará atributos de está precisa, ará garantir que eles não sejam Perfil do tempo real.

![ACOP](./images/journeywait.png)

Sua jornada agora é um fenômeno semelhante ao seguinte. Não há calendário de você configurar. Defina como 1. Isso dará bastante para o que os atributos do estejam do disponíveis dísmo do evento.

![ACOP](./images/journeywait1.png)

Clique em **Ok** para salvar suas alterações.

Como é a jornada, você é uma obra. **Email**. Vá para o lado esquerdo da tela **Ações** selecione uma ação **Email** e arraste e solte a ação no segundo nó da jornada. Agora o seguinte será exibido.

![ACOP](./images/journeyactions.png)

Defina a **Categoria** como **Marketing** e selecione uma **superfície de email** permita para envio de e-mail. Caso, a **superfície de email** um usuário selecionada é E-mail. Certifique-se de que as caixas de seleção **Cliques no email** e **aberturas de email** estejam marcadas.

![ACOP](./images/journeyactions1.png)

Um próximo é . Para isso, clique em **Editar conteúdo**.

![ACOP](./images/journeyactions2.png)

## 2.3.2 Crie um vídeo

Para sua família **Editar conteúdo**.

![ACOP](./images/journeyactions2.png)

O seguinte será exibido.

![ACOP](./images/journeyactions3.png)

Clique sem campo de texto **Linha de assunto**.

![Journey Optimizer](./images/msg5.png)

Na cor da texto, comece **Hello**

![Journey Optimizer](./images/msg6.png)

A linha de não está agora. Em, você trazer o token personalization para o **Nome** que está armazenado `profile.person.name.firstName`. Não há menu à esquerda, função para parágrafo elemento **Pessoa** e panelinha na posição para visualizar mais campos

![Journey Optimizer](./images/msg7.png)

Agora elemento **Nome completo** e panelinha em lugar visualizar mais campos.

![Journey Optimizer](./images/msg8.png)

Por fim, localize o campo **Nome** e panelhe no símbolo **+**  ao lado dele. Você verá o token de personalização aparecer no campo de texto.

![Journey Optimizer](./images/msg9.png)

Em, texto **agrecemos a sua inscrição!**. Clique em **Salvar**.

![Journey Optimizer](./images/msg10.png)

Então, você vai retornar para esta tela. Clique em **Email Designer**  para o conteúdo do e-mail

![Journey Optimizer](./images/msg11.png)

Na tela, será solicitado que você forneça fazer e-mail através de 3 métodos diferentes:

- **Design do zero**: Comece com tela em branco e uso do editor WYSIWYG para arrastar e soltar a estrutura e os de conteúdo para visita o conteúdo do e-mail.
- **Codifique seu próprio**: Codificação da Correio Eletrônico usando HTML
- **Importar HTML**: Importe um HTML existente, que poderá editar.

Clique em **Importar HTML**.

![Journey Optimizer](./images/msg12.png)

Arraste e solte o in **mailtemplatebootcamp.html**, que você pode [aqui](../../assets/html/mailtemplatebootcamp.html.zip). Clique em Importar.

![Journey Optimizer](./images/msg13.png)

Você verá  de correio eletrônico:

![Journey Optimizer](./images/msg14.png)

Continuar a enviar correio eletrônico personalizado. Clique ao lado do texto **Hello** e, em, não ícone **Adicionar personalização**.

![Journey Optimizer](./images/msg35.png)

Em, você trazer o token personalization **Nome** que está armazenado `profile.person.name.firstName`. Nenhum menu, localize ou elemento **Pessoa** faça uma busca detalhada não elemento **Nome completo** e panelhe no ícone **+** para **Nome** ao editor.

Clique em **Salvar**.

![Journey Optimizer](./images/msg36.png)

Agora você verá como o campo de personalização é adicionado ao seu texto.

![Journey Optimizer](./images/msg37.png)

Clique em **Salvar** para salvar sua mensagem.

![Journey Optimizer](./images/msg55.png)

Retorne para painel de mensagens clicando na linha da linha do sentido do lado esquerdo.

![Journey Optimizer](./images/msg56.png)

Agora você concluiu criação do seu e-mail de cadastro. Clique na seta no canto superior esquerdo para retornar à sua jornada.

![Journey Optimizer](./images/msg57.png)

Clique em **Ok**.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3 Publicar a sua jornada

Você precisa de um nome à sua jornada. Você pode fazer isso clicando no ícone **Propriedades** não canto superior da tela.

![ACOP](./images/journeyname.png)

Você pode fazer isso clicando nenhum item clicar nenhum item &quot;Nome&quot; e inserindo seguinte nome `yourLastName - Account Creation Journey`. Clique em **OK** para salvar como mudanças.

![ACOP](./images/journeyname1.png)

Agora você publicar sua jornada clicando **Publicar**.

![ACOP](./images/publishjourney.png)

Clique em **Publicar**  Data

![ACOP](./images/publish1.png)

Você verá uma barra de confirmação verde informando que sua jornada agora está publicada.

![ACOP](./images/published.png)

Você terminou este.

Proxima. [2.4 Teste da sua jornada](./ex4.md)

[Retornar para Fluxo 2](./uc2.md)

[Retornar para Todos os Módulos](../../overview.md)