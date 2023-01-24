---
title: Bootcamp - Journey Optimizer Create your jornada and email message - Brasil
description: Bootcamp - Journey Optimizer Create your jornada and email message - Brasil
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 4%

---

# 2.3 Criar sua jornada e mensagem de email

Neste exercício, você configurará a jornada que precisa ser acionada quando alguém criar uma conta no site de demonstração.

Faça logon no Adobe Journey Optimizer acessando [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para o **Início**  no Journey Optimizer. Primeiro, certifique-se de usar a sandbox correta. A sandbox a ser usada é chamada de `Bootcamp`. Para alterar de uma sandbox para outra, clique em **Prod** e selecione a sandbox na lista. Neste exemplo, a sandbox é chamada de **Bootcamp**. Você estará no **Início** exibição da sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 2.3.1 Criar a jornada

No menu esquerdo, clique em **Jornada**. Em seguida, clique em **Criar Jornada** para criar uma nova jornada.

![ACOP](./images/createjourney.png)

Você verá uma tela de jornada vazia.

![ACOP](./images/journeyempty.png)

No exercício anterior, você criou um novo **Evento**. Você o nomeou assim `yourLastNameAccountCreationEvent` e substituído `yourLastName` com seu sobrenome. Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

Agora é necessário tomar esse evento como o início desta Jornada. Você pode fazer isso indo para o lado esquerdo da tela e procurando pelo evento na lista de eventos.

![ACOP](./images/eventlist.png)

Selecione seu evento, arraste-o e solte-o na tela de Jornada. A Jornada agora tem esta aparência:

![ACOP](./images/journeyevent.png)

Como a segunda etapa da jornada, é necessário adicionar um curto **Aguardar** etapa. Vá para o lado esquerdo da tela para **Orquestração** para encontrar isso. Você estará usando os atributos do perfil e precisará verificar se eles estão preenchidos no Perfil do cliente em tempo real.

![ACOP](./images/journeywait.png)

Sua jornada agora fica assim. No lado direito da tela, é necessário configurar o tempo de espera. Defina para 1 minuto. Isso dará tempo suficiente para que os atributos do perfil estejam disponíveis após o acionamento do evento.

![ACOP](./images/journeywait1.png)

Clique em **Ok** para salvar as alterações.

Como a terceira etapa da jornada, é necessário adicionar um **Email** ação. Vá para o lado esquerdo da tela para **Ações**, selecione o **Email** , em seguida, arraste e solte no segundo nó da jornada. Agora você vê isso.

![ACOP](./images/journeyactions.png)

Defina as **Categoria** para **Marketing** e selecione uma superfície de email que permita enviar emails. Nesse caso, a superfície do email a ser selecionada é **Email**. Certifique-se de que as caixas de seleção de **Cliques no email** e **aberturas de email** estão ativadas.

![ACOP](./images/journeyactions1.png)

A próxima etapa é criar a mensagem. Para fazer isso, clique em **Editar conteúdo**.

![ACOP](./images/journeyactions2.png)

## 2.3.2 Criar sua mensagem

Para criar sua mensagem, clique em **Editar conteúdo**.

![ACOP](./images/journeyactions2.png)

Agora você vê isso.

![ACOP](./images/journeyactions3.png)

Clique no botão **Linha de assunto** campo de texto.

![Journey Optimizer](./images/msg5.png)

Na área de texto, comece a escrever **Oi**

![Journey Optimizer](./images/msg6.png)

A linha de assunto ainda não foi feita. Em seguida, é necessário trazer o token de personalização para o campo **Nome** armazenado em `profile.person.name.firstName`. No menu esquerdo, role para baixo até encontrar a variável **Pessoa** e clique na seta para ir um nível mais fundo.

![Journey Optimizer](./images/msg7.png)

Agora encontre a variável **Nome completo** e clique na seta para ir um nível mais fundo.

![Journey Optimizer](./images/msg8.png)

Finalmente, encontre a **Nome** e clique no botão **+** sinal ao lado. Em seguida, você verá o token de personalização aparecer no campo de texto.

![Journey Optimizer](./images/msg9.png)

Em seguida, adicione o texto **, obrigado por se inscrever!**. Clique em **Salvar**.

![Journey Optimizer](./images/msg10.png)

Então você estará de volta. Clique em **Email Designer** para criar o conteúdo do email.

![Journey Optimizer](./images/msg11.png)

Na próxima tela, você receberá 3 métodos diferentes para fornecer o conteúdo do email:

- **Design do zero**: Comece com uma tela em branco e use o editor WYSIWYG para arrastar e soltar a estrutura e os componentes de conteúdo para criar visualmente o conteúdo do email.
- **Codifique seu próprio**: Crie seu próprio modelo de email codificando-o usando o HTML
- **Importar HTML**: Importe um template HTML existente, que poderá editar.

Clique em **Importar HTML**.

![Journey Optimizer](./images/msg12.png)

Arraste e solte o arquivo **mailtemplatebootcamp.html**, que você pode baixar [here](../../assets/html/mailtemplatebootcamp.html.zip). Clique em Importar.

![Journey Optimizer](./images/msg13.png)

Você verá este template de email padrão:

![Journey Optimizer](./images/msg14.png)

Vamos personalizar o email. Clique ao lado do texto **Oi** e clique no botão **Adicionar personalização** ícone .

![Journey Optimizer](./images/msg35.png)

Em seguida, você precisa trazer o **Nome** token de personalização armazenado em `profile.person.name.firstName`. No menu, encontre a variável **Pessoa** elemento, navegue até o **Nome completo** e clique no botão **+** ícone para adicionar o campo Nome no editor de expressão.

Clique em **Salvar**.

![Journey Optimizer](./images/msg36.png)

Agora você perceberá como o campo de personalização foi adicionado ao texto.

![Journey Optimizer](./images/msg37.png)

Clique em **Salvar** para salvar sua mensagem.

![Journey Optimizer](./images/msg55.png)

Volte para o painel de mensagens clicando no botão **seta** ao lado do texto da linha de assunto no canto superior esquerdo.

![Journey Optimizer](./images/msg56.png)

Você concluiu a criação do email de registro. Clique na seta no canto superior esquerdo para retornar à jornada.

![Journey Optimizer](./images/msg57.png)

Clique em **Ok**.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3 Publicar a jornada

Você ainda precisa dar um Nome à sua jornada. Você pode fazer isso clicando no botão **Propriedades** no lado superior direito da tela.

![ACOP](./images/journeyname.png)

Você pode então inserir o nome da jornada aqui. Use `yourLastName - Account Creation Journey`. Clique em **OK** para salvar as alterações.

![ACOP](./images/journeyname1.png)

Agora você pode publicar sua jornada clicando em **Publicar**.

![ACOP](./images/publishjourney.png)

Clique em **Publicar** novamente.

![ACOP](./images/publish1.png)

Em seguida, você verá uma barra de confirmação verde informando que sua jornada foi publicada.

![ACOP](./images/published.png)

Você já terminou este exercício.

Próxima etapa: [2.4 Teste sua jornada](./ex4.md)

[Voltar para Fluxo de Usuário 2](./uc2.md)

[Voltar para todos os módulos](../../overview.md)