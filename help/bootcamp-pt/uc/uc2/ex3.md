---
title: Bootcamp - Journey Optimizer Crie sua jornada e mensagem de email - Brasil
description: Bootcamp - Journey Optimizer Crie sua jornada e mensagem de email - Brasil
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: d486d1aa-7b8e-4301-91e6-4c84fba0c72a
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 3%

---

# 2.3 Criar sua jornada e mensagem de e-mail

Neste exercício, você adota a jornada que precisa ser acionada quando criar uma conta no site de.

Faça logon no Adobe Journey Optimizer acessando a [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a da **Início**  sem Journey Optimizer. Primeiro, usar você está usando o sandbox correto. O nome do sandbox que deve ser usado é `Bootcamp`. Para alternar de um sandbox para outro, clique em **Prod** e o sandbox na lista. Exemplo, o nome do sandbox é **Bootcamp**. Você está na da **Início** fazer seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 2.3.1 Criar a sua jornada

Sem menu à esquerda, clique em **Jornadas**. Em seguida, clique em **Criar Jornada** para criar uma nova jornada.

![ACOP](./images/createjourney.png)

Você verá uma tela de vazia.

![ACOP](./images/journeyempty.png)

Não exercício anterior, você criou um novo **Evento**. Você consegue o evento `seuSobrenomeAccountCreationEvent` e substituiu `seuSobrenome` pelo seu sobrenome. Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

Agora você deve este evento como o início desta Jornada. Você pode fazer o lado evento da tela e tendências pelo seu lista de eventos.

![ACOP](./images/eventlist.png)

é possível encontrar seu evento, e solte o evento na tela da Jornada. Sua Jornada agora deve ser analisada a seguir:

![ACOP](./images/journeyevent.png)

Como segunda etapa da jornada, você deve acompanhar uma aula curta de **Aguardar**. Vá para o lado esquerdo da tela até a migração **Orquestração** para encontrar isso. Você usará a capacidade de perfil e ➡ garantir que eles gravam os tempos no Perfil do cliente em real.

![ACOP](./images/journeywait.png)

Sua jornada deve ser seguido. Não há lado direito da tela que você modificar o tempo de espera. Defina como 1 minuto. Isso dará tempo suficiente para o que os jogadores do anúncio exibido para o disparo do evento.

![ACOP](./images/journeywait1.png)

Clique em **Ok** para proteger o cliente.

Como etapa da jornada, você deve mudar uma ação **E-mail**. Vá para o lado esquerdo da tela para **Ações**, uma ação **E-mail** e ➡ e nó solte a ação no segundo da jornada. Agora o seguinte será exibido.

![ACOP](./images/journeyactions.png)

Definir um **Categoria** como **Marketing** e ➡ uma **superfície de email** que envio o envio de e-mail. Nesse caso, a **superfície de email** Selecione um e-mail de seleção. das caixas de seleção **Cliques no email** e **aberturas de email** marcadas.

![ACOP](./images/journeyactions1.png)

A próxima etapa é a sua mensagem. Para, clique em San José **Editar conteúdo**.

![ACOP](./images/journeyactions2.png)

## 2.3.2 Criar a sua mensagem

Para criar sua mensagem, clique em **Editar conteúdo**.

![ACOP](./images/journeyactions2.png)

O seguinte será exibido.

![ACOP](./images/journeyactions3.png)

Clique no campo de texto **Linha de assunto**.

![Journey Optimizer](./images/msg5.png)

Na área de texto, início **Olá**

![Journey Optimizer](./images/msg6.png)

A linha de conduta ainda não está pronta. Em seguida, você cresce o token de personalização para o **Nome** que está presente em `profile.person.name.firstName`. No menu à esquerda, papel para baixo para encontrar o elemento **Person** e clique na seta para visualizar mais campos

![Journey Optimizer](./images/msg7.png)

Agora encontra o elemento **Nome completo** e clique na seta para visualizar mais campos.

![Journey Optimizer](./images/msg8.png)

Por fim, localize o campo **Nome** e clique no ➡ **+**  ao lado dele. Você verá o token de personalização aparece no campo de texto.

![Journey Optimizer](./images/msg9.png)

Em mudança, o texto, **agradecemos a sua inscrição!**. Clique em **Salvar**.

![Journey Optimizer](./images/msg10.png)

Então, você muda para esta tela. Clique em **Email Designer**  para criar o conteúdo do email.

![Journey Optimizer](./images/msg11.png)

Na próxima tela, será melhor que você não insira conteúdo do e-mail através de 3 métodos diferentes:

- **Criar do zero**: Comece com uma tela em branco e use o editor WYSIWYG para arrastar e soltar a estrutura e os componentes de conteúdo para criar visualmente o conteúdo do e-mail.
- **Desenvolva o seu**: Criar seu próprio modelo de e-mail utilizando o HTML
- **Importar HTML**: Importe modelo HTML existente, que você pode mudar.

Clique em **Importar HTML**.

![Journey Optimizer](./images/msg12.png)

Arraste e solte o arquivo **mailtemplatebootcamp.html**, que você pode baixa [aqui](../../assets/html/mailtemplatebootcamp.html.zip). Clique em Importar.

![Journey Optimizer](./images/msg13.png)

Você verá este modelo de e-mail padrão:

![Journey Optimizer](./images/msg14.png)

Vamos mudar o e-mail. Clique ao lado do texto **Olá** e, em seguida, clique no monitoramento **Adicionar personalização**.

![Journey Optimizer](./images/msg35.png)

Em seguida, você cresce o token de personalização **Nome** que está presente em `profile.person.name.firstName`. Nenhum menu, localizar o elemento **Person**, exercícios uma vez visto não há elemento **Nome completo** e clique no ➡ **+** para ➡ o campo **Nome** ao editor.

Clique em **Salvar**.

![Journey Optimizer](./images/msg36.png)

Agora verá como o campo de personalização foi ao seu texto.

![Journey Optimizer](./images/msg37.png)

Clique em **Salvar** para salvar sua mensagem.

![Journey Optimizer](./images/msg55.png)

Retornado para o painel de veículos movidos na coluna visível ao lado do lado do tópico de tópico no canto superior.

![Journey Optimizer](./images/msg56.png)

Agora reconhecida a criação do seu e-mail de cadastro. Clique na seta no canto superior para acompanhar a sua jornada.

![Journey Optimizer](./images/msg57.png)

Clique em **Ok**.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3 Publicação da sua jornada

Você ainda precisa um Nome à sua jornada. Você pode fazer isso, não tem nada a ver **Propriedades** nenhum canto superior direito da tela.

![ACOP](./images/journeyname.png)

Você pode fazer isso no item não identificado e inserindo o seguinte nome `yourLastName - Account Creation Journey`. Clique em **OK** para aplicar as alterações.

![ACOP](./images/journeyname1.png)

Agora você pode publicar sua rotina em **Publish**.

![ACOP](./images/publishjourney.png)

Clique em **Publish**  novamente.

![ACOP](./images/publish1.png)

Você verá uma barra de verde informa que sua agora está Publicada.

![ACOP](./images/published.png)

Você terminou este exercício.

Próxima etapa: [2.4 Testa sua jornada](./ex4.md)

[Retorno para Fluxo de monitoramento 2](./uc2.md)

[Retorno para Todos os compartilhados](../../overview.md)
