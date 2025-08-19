---
title: Criar experiência de email do GenStudio for Performance Marketing para o AJO
description: Criar experiência de email do GenStudio for Performance Marketing para o AJO
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 9837c076-e6ca-47a0-96b9-5fa5fdba3fd2
source-git-commit: 917ebcd2dd5d8316413a183bd2c1a048c090428c
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---

# 1.3.4 Criar experiência de email para o AJO

>[!IMPORTANT]
>
>Para concluir este exercício, você precisa ter acesso a um ambiente do Adobe Journey Optimizer provisionado para a integração com o GenStudio for Performance Marketing, que atualmente está na versão beta.

>[!IMPORTANT]
>
>Para executar todas as etapas deste exercício, é necessário ter acesso a um ambiente existente do Adobe Workfront e, nesse ambiente, criar um fluxo de trabalho de projeto e aprovação. Se você seguir o exercício [Gerenciamento de Fluxo de Trabalho com o Adobe Workfront](./../../../modules/workflow-planning/module1.2/workfront.md){target="_blank"}, terá a configuração necessária disponível.

## 1.3.4.1 Criar e Aprovar Experiência de Email

No menu esquerdo, vá para **Criar**. Selecione **Email**.

![GSPeM](./images/gsemail1.png)

Selecione o modelo de **Email** que você importou antes, chamado `--aepUserLdap---citisignal-email-template`. Clique em **Usar**.

![GSPeM](./images/gsemail2.png)

Você deverá ver isso. Altere o nome do seu anúncio para `--aepUserLdap-- - Email Online Gamers Fiber Max`.

![GSPeM](./images/gsemail3.png)

Em **Parâmetros**, selecione as seguintes opções:

- **Marca**: `--aepUserLdap-- - CitiSignal`
- **Idioma**: `English (US)`
- **Pessoa**: `--aepUserLdap-- - Online Gamers`
- **Produto**: `--aepUserLdap-- - CitiSignal Fiber Max`

Clique em **Selecionar do conteúdo**.

![GSPeM](./images/gsemail4.png)

Selecione o ativo `--aepUserLdap-- - neon rabbit.png`. Clique em **Usar**.

![GSPeM](./images/gsemail5.png)

Digite o prompt `convince online gamers to start playing online multiplayer games using CitiSignal internet` e clique em **Gerar**.

![GSPeM](./images/gsemail6.png)

Você deve ver algo como isso, com quatro variações de email sendo geradas. O modo de exibição padrão mostra o modo de exibição **dispositivo móvel**. Você pode alternar para o modo de exibição de área de trabalho clicando no ícone **computador**.

![GSPeM](./images/gsemail7.png)

Para cada email, uma pontuação de conformidade é calculada automaticamente. Clique na pontuação para ver mais detalhes.

![GSPeM](./images/gsemail8.png)

Clique em **Exibir e corrigir problemas**.

![GSPeM](./images/gsemail9.png)

Você pode ver mais detalhes sobre o que pode fazer para otimizar a pontuação de conformidade.

![GSPeM](./images/gsemail10.png)

Em seguida, clique em **Solicitar aprovação**, que se conectará ao Adobe Workfront.

![GSPeM](./images/gsemail11.png)

Selecione seu projeto do Adobe Workfront, que deve ser nomeado como `--aepUserLdap-- - CitiSignal Fiber Launch`. Insira seu próprio endereço de email em **Convidar pessoas** e verifique se sua função está definida como **Aprovador**.

![GSPeM](./images/gsemail12.png)

Como alternativa, você também pode usar um fluxo de trabalho de aprovação existente no Adobe Workfront. Para fazer isso, clique em **Usar modelo** e selecione o modelo `--aepuserLdap-- - Approval Workflow`. Clique em **Enviar**.

![GSPeM](./images/gsemail13.png)

Clique em **Exibir comentários no Workfront**. Você será enviado agora para a Interface do Usuário do Adobe Workfront Proof.

![GSPeM](./images/gsemail14.png)

Na interface do Adobe Workfront Proof, clique em **Tomar decisão**.

![GSPeM](./images/gsemail15.png)

Selecione **Aprovado** e clique em **Tomar decisão**.

![GSPeM](./images/gsemail16.png)

Clique em **Publicar**.

![GSPeM](./images/gsemail17.png)

Selecione sua Campanha `--aepUserLdap-- - CitiSignal Fiber Launch Campaign` e clique em **Publicar**.

![GSPeM](./images/gsemail18.png)

Clique em **Abrir no Conteúdo**.

![GSPeM](./images/gsemail19.png)

As 4 experiências de email agora estão disponíveis em **Conteúdo** > **Experiências**.

![GSPeM](./images/gsemail20.png)

## 1.3.4.2 Criar uma campanha no AJO

Faça login no Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`. Você estará na exibição **Página inicial** da sua sandbox `--aepSandboxName--`.

![ACOP](./../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

Agora você criará uma campanha. Ao contrário da jornada baseada em eventos do exercício anterior, que depende de eventos de experiência de entrada, entradas de público-alvo ou saídas para acionar uma jornada para um cliente específico, as campanhas direcionam todo um público-alvo uma vez com conteúdo exclusivo, como boletins informativos, promoções únicas ou informações genéricas ou periodicamente com conteúdo semelhante enviado regularmente, como por exemplo campanhas de aniversário e lembretes.

No menu, vá para **Campanhas** e clique em **Criar campanha**.

![Journey Optimizer](./images/gsemail21.png)

Selecione **Agendado - Marketing** e clique em **Criar**.

![Journey Optimizer](./images/gsemail22.png)

Na tela de criação da campanha, configure o seguinte:

- **Nome**: `--aepUserLdap--  - Online Gamers CitiSignal Fiber Max`.
- **Descrição**: campanha de fibra para Jogadores Online

Clique em **Ações**.

![Journey Optimizer](./images/gsemail23.png)

Clique em **+ Adicionar ação** e selecione **Email**.

![Journey Optimizer](./images/gsemail24.png)

Em seguida, selecione uma **configuração de email** existente e clique em **Editar conteúdo**.

![Journey Optimizer](./images/gsemail25.png)

Você verá isso. Para a **Linha de assunto**, use esta:

```
{{profile.person.name.firstName}}, say goodbye to delays!
```

Em seguida, clique em **Editar conteúdo**.

![Journey Optimizer](./images/gsemail26.png)

Clique em **Importar HTML**.

![Journey Optimizer](./images/gsemail27.png)

Em seguida, clique no botão para **Adobe GenStudio for Performance Marketing**.

![Journey Optimizer](./images/gsemail28.png)

Você deverá ver uma janela pop-up que mostra todas as experiências de email publicadas no GenStudio for Performance Marketing. Selecione uma das experiências de email disponíveis e clique em **Usar**.

![Journey Optimizer](./images/gsemail29.png)

Selecione seu próprio repositório do AEM Assets CS, que deve se chamar `--aepUserLdap-- - CitiSignal dev`, e clique em **Importar**.

![Journey Optimizer](./images/gsemail30.png)

Você deverá ver isso. Selecione o botão de imagem ausente e clique em **Selecionar um ativo**.

![Journey Optimizer](./images/gsemail31.png)

Vá para a pasta semelhante a esta, começando com **GenStudio.zip....** e selecione a imagem `--aepUserLdap-- - neon rabbit.png`. Clique em **Selecionar**

![Journey Optimizer](./images/gsemail32.png)

Você deverá ver isso.

![Journey Optimizer](./images/gsemail33.png)

Role para baixo até o rodapé, selecione a palavra **Cancelar inscrição** e clique no ícone **link**.

![Journey Optimizer](./images/gsemail38.png)

Defina o **Type** como **Opção de não participação/Cancelamento de assinatura externo** e defina a URL como `https://techinsiders.org/unsubscribe.html` (não é permitido ter uma URL em branco para o link de cancelamento de assinatura).

Clique em **Salvar** e na **seta** no canto superior esquerdo da tela para voltar para a configuração da campanha.

![Journey Optimizer](./images/gsemail39.png)

Ir para **Público**.

![Journey Optimizer](./images/gsemail34.png)

Clique em **Selecionar audiência**.

![Journey Optimizer](./images/gsemail35.png)

Selecione a audiência da lista de assinaturas dos Jogadores Online, que deve se chamar `--aepUserLdap--_SL_Interest_Online_Gaming`. Clique em **Salvar**.

![Journey Optimizer](./images/gsemail36.png)

Clique em **Revisar para ativar**.

![Journey Optimizer](./images/gsemail37.png)

Se a configuração da sua campanha não tiver problemas, você poderá clicar em **Ativar**.

![Journey Optimizer](./images/gsemail40.png)

Sua campanha será ativada, o que leva alguns minutos.

![Journey Optimizer](./images/gsemail41.png)

Após alguns minutos, a campanha é ativada e o email será enviado para a lista de assinaturas selecionada.

![Journey Optimizer](./images/gsemail42.png)

Você concluiu este exercício agora.

## Próximas etapas

Ir para [Resumo e benefícios](./summary.md){target="_blank"}

Voltar para [GenStudio for Performance Marketing](./genstudio.md){target="_blank"}

Voltar para [Todos os Módulos](./../../../overview.md){target="_blank"}
