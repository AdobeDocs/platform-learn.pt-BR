---
title: Bootcamp - Journey Optimizer Crie sua jornada e mensagem de email
description: Bootcamp - Journey Optimizer Crie sua jornada e mensagem de email
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Journeys
exl-id: 138a70fa-fe50-4585-b47f-150db4770c3d
source-git-commit: cd59a41f4533f18a54d80298ee9faf3a8ba3c6e7
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# 2.3 Criar a jornada e a mensagem de email

Neste exercício, você configurará a jornada que precisa ser acionada quando alguém criar uma conta no site de demonstração.

Faça login no Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `Bootcamp`. Para alterar a sandbox, clique em **Prod** e selecione a sandbox na lista. Neste exemplo, a sandbox é chamada **Bootcamp**. Você estará na exibição **Página inicial** da sua sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 2.3.1 Criar a jornada

No menu esquerdo, clique em **Jornadas**. Em seguida, clique em **Criar Jornada** para criar uma nova jornada.

![ACOP](./images/createjourney.png)

Você verá uma tela de jornada vazia.

![ACOP](./images/journeyempty.png)

No exercício anterior, você criou um novo **Evento**. Você o nomeou desta forma `yourLastNameAccountCreationEvent` e substituiu `yourLastName` pelo seu sobrenome. Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

Agora, é necessário tomar este evento como o início desta Jornada. Você pode fazer isso indo para o lado esquerdo da tela e procurando seu evento na lista de eventos.

![ACOP](./images/eventlist.png)

Selecione o evento, arraste e solte-o na tela de Jornada. Agora a Jornada tem esta aparência:

![ACOP](./images/journeyevent.png)

Como a segunda etapa da jornada, você precisa adicionar uma pequena etapa **Aguardar**. Vá para o lado esquerdo da tela para a seção **Orquestração** para encontrar isso. Você estará usando atributos de perfil e precisa verificar se eles estão preenchidos no Perfil do cliente em tempo real.

![ACOP](./images/journeywait.png)

Sua jornada agora está assim. No lado direito da tela, é necessário configurar o tempo de espera. Defina-o como 1 minuto. Isso dará bastante tempo para que os atributos de perfil estejam disponíveis após o acionamento do evento.

![ACOP](./images/journeywait1.png)

Clique em **Ok** para salvar suas alterações.

Como terceira etapa da jornada, você precisa adicionar uma ação **Email**. Vá para o lado esquerdo da tela para **Ações**, selecione a ação **Email** e arraste-a e solte-a no segundo nó da jornada. Agora vocês podem ver isso.

![ACOP](./images/journeyactions.png)

Defina a **Categoria** como **Marketing** e selecione uma superfície de email que permita o envio de emails. Nesse caso, a superfície de email a ser selecionada é **Email**. Verifique se as caixas de seleção para **Cliques no email** e **aberturas de email** estão habilitadas.

![ACOP](./images/journeyactions1.png)

A próxima etapa é criar a mensagem. Para fazer isso, clique em **Editar conteúdo**.

![ACOP](./images/journeyactions2.png)

## 2.3.2 Criar a mensagem

Para criar sua mensagem, clique em **Editar conteúdo**.

![ACOP](./images/journeyactions2.png)

Agora vocês podem ver isso.

![ACOP](./images/journeyactions3.png)

Clique no campo de texto **Linha de assunto**.

![Journey Optimizer](./images/msg5.png)

Na área de texto comece a gravar **Olá**

![Journey Optimizer](./images/msg6.png)

A linha de assunto ainda não foi terminada. Em seguida, você precisa trazer o token de personalização para o campo **Nome**, que é armazenado em `profile.person.name.firstName`. No menu esquerdo, role para baixo para encontrar o elemento **Person** e clique na seta para ir um nível mais fundo.

![Journey Optimizer](./images/msg7.png)

Agora, encontre o elemento **Nome completo** e clique na seta para ir um nível mais fundo.

![Journey Optimizer](./images/msg8.png)

Finalmente, encontre o campo **Nome** e clique no sinal **+** ao lado dele. Você verá o token de personalização aparecer no campo de texto.

![Journey Optimizer](./images/msg9.png)

Em seguida, adicione o texto **, obrigado por se inscrever!**. Clique em **Salvar**.

![Journey Optimizer](./images/msg10.png)

Você estará de volta aqui. Clique em **Email do Designer** para criar o conteúdo do email.

![Journey Optimizer](./images/msg11.png)

Na próxima tela, 3 métodos diferentes serão exibidos para fornecer o conteúdo do email:

- **Criar do zero**: comece com uma tela em branco e use o editor WYSIWYG para arrastar e soltar componentes de estrutura e conteúdo para criar visualmente o conteúdo do email.
- **Codifique o seu próprio**: crie seu próprio modelo de email codificando-o usando o HTML
- **Importar HTML**: importe um modelo de HTML existente, que poderá ser editado.

Clique em **Importar HTML**. Como alternativa, você pode clicar em **Modelos salvos** e selecionar o modelo **Bootcamp - Modelo de email**.

![Journey Optimizer](./images/msg12.png)

Se você selecionou **Importar HTML**, agora é possível arrastar e soltar o arquivo **mailtemplatebootcamp.html**, que você pode baixar [aqui](../../assets/html/mailtemplatebootcamp.html.zip). Clique em Importar.

![Journey Optimizer](./images/msg13.png)

Em seguida, você verá este template de email padrão:

![Journey Optimizer](./images/msg14.png)

Vamos personalizar o email. Clique em próximo ao texto **Olá** e clique no ícone **Adicionar Personalization**.

![Journey Optimizer](./images/msg35.png)

Em seguida, você precisa trazer o token de personalização de **Nome**, que é armazenado em `profile.person.name.firstName`. No menu, localize o elemento **Pessoa**, vá para o elemento **Nome Completo** e clique no ícone **+** para adicionar o campo Nome ao editor de expressão.

Clique em **Salvar**.

![Journey Optimizer](./images/msg36.png)

Agora você observará como o campo de personalização foi adicionado ao seu texto.

![Journey Optimizer](./images/msg37.png)

Clique em **Salvar** para salvar sua mensagem.

![Journey Optimizer](./images/msg55.png)

Volte para o painel da mensagem clicando na **seta** ao lado do texto da linha de assunto no canto superior esquerdo.

![Journey Optimizer](./images/msg56.png)

Você concluiu a criação do email de registro. Clique na seta no canto superior esquerdo para voltar à jornada.

![Journey Optimizer](./images/msg57.png)

Clique em **Ok**.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3 Publish com sua jornada

Você ainda precisa dar um Nome à sua jornada. Você pode fazer isso clicando no ícone **Lápis** na parte superior esquerda da tela.

![ACOP](./images/journeyname.png)

Em seguida, você pode inserir o nome da jornada aqui. Use `yourLastName - Account Creation Journey`. Clique em **OK** para salvar suas alterações.

![ACOP](./images/journeyname1.png)

Agora você pode publicar sua jornada clicando em **Publish**.

![ACOP](./images/publishjourney.png)

Clique novamente em **Publish**.

![ACOP](./images/publish1.png)

Você verá uma barra de confirmação verde informando que a jornada foi publicada.

![ACOP](./images/published.png)

Você terminou este exercício agora.

Próxima etapa: [2.4 Testar sua jornada](./ex4.md)

[Voltar para Fluxo de Usuário 2](./uc2.md)

[Voltar a todos os módulos](../../overview.md)