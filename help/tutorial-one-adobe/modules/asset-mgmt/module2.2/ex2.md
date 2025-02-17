---
title: Prova com o Workfront
description: Prova com o Workfront
kt: 5342
doc-type: tutorial
exl-id: 1b5ca13b-2a32-44a1-a3ae-342bccc6baeb
source-git-commit: dd075b0296c6ba06d72b229145635060c2c6abb1
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# 1.2.2 Prova com o Workfront

## 1.2.2.1 Criar um novo fluxo de aprovação

Ir para [https://experienceplatform.my.workfront.com/](https://experienceplatform.my.workfront.com/){target="_blank"}.

Clique no ícone de 9 pontos **hambúrguer** e selecione **Revisão**.

![WF](./images/wfp1.png)

Vá para **Workflows**, clique em **+ Novo** e selecione **Novo modelo**.

![WF](./images/wfp2.png)

Defina o **Nome do modelo** como `--aepUserLdap-- - Approval Workflow` e defina o **Proprietário do modelo** como você mesmo.

![WF](./images/wfp3.png)

Role para baixo e, em **Estágios** > **Estágio 1**, adicione **Wouter Van Geluwe** com a **Função** de **Revisor e Aprovador**.

Clique em **Criar**.

![WF](./images/wfp4.png)

O fluxo de trabalho básico de aprovação agora está pronto para ser usado.

![WF](./images/wfp5.png)

## 1.2.2.2 Criar um novo projeto

Na página inicial do Workfront, clique em **Novo** na guia **Meus Projetos**. Selecione **Projeto Em Branco**.

![WF](./images/wfp6.png)

Você deverá ver isso. Altere o nome para `--aepUserLdap-- - CitiSignal Fiber Launch`.

![WF](./images/wfp6a.png)

Seu projeto foi criado.

![WF](./images/wfp7.png)

## 1.2.2.3 Criar uma nova tarefa

Digite este nome para sua tarefa: **Criar ativos para a campanha de Fibra**. Clique em **Criar tarefa**.

![WF](./images/wfp8.png)

Você deverá ver isso.

![WF](./images/wfp9.png)

## 1.2.2.4 Adicionar um novo Documento à Tarefa passar pelo fluxo de aprovação

Clique em **+ Adicionar novo** e selecione **Documento**.

![WF](./images/wfp10.png)

Baixe [este arquivo](./images/2048x2048.png) na área de trabalho.

![WF](./images/2048x2048.png){width="50px" align="left"}

Selecione o arquivo **2048x2048.png** e clique em **Abrir**.

![WF](./images/wfp12.png)

Você deveria ficar com isso. Clique em **Criar prova** e escolha **Prova avançada**.

![WF](./images/wfp13.png)

Na janela **nova prova**, selecione o modelo de fluxo de trabalho criado anteriormente, que deve ser nomeado como `--aepuserLdap-- - Approval Workflow`. Clique em **Criar prova**.

![WF](./images/wfp14.png)

Você estará de volta à sua tarefa. Clique no botão **Atribuir a** e selecione **Atribuir a mim**.

![WF](./images/wfp15.png)

Clique em **Salvar**.

![WF](./images/wfp16.png)

Clique em **Trabalhar nisto**.

![WF](./images/wfp17.png)

Clique em **Abrir prova**

![WF](./images/wfp18.png)

Agora você pode revisar a prova. Selecione **Adicionar comentário** para adicionar um comentário que exija que o documento seja alterado.

![WF](./images/wfp19.png)

Insira seu comentário e clique em **Postar**. Clique em **Fechar**.

![WF](./images/wfp20.png)

Em seguida, você precisa alterar sua função de **Revisor** para **Revisor e Aprovador**. Para fazer isso, volte para a sua Tarefa e clique em **Fluxo de trabalho de revisão**.

![WF](./images/wfp21.png)

Altere sua função de **Revisor** para **Revisor e Aprovador**.

![WF](./images/wfp22.png)

Volte para Tarefa e abra a prova novamente. Agora você vê um novo botão, **Tomar decisão**. Clique nele.

![WF](./images/wfp23.png)

Selecione **Alterações necessárias** e clique em **tomar uma decisão**.

![WF](./images/wfp24.png)

Você deveria voltar aqui. Agora é necessário carregar uma segunda imagem que considere os comentários fornecidos.

![WF](./images/wfp25.png)

Baixe [este arquivo](./images/2048x2048_buynow.png) na área de trabalho.

![este arquivo](./images/2048x2048_buynow.png){width="50px" align="left"}

Na exibição Tarefa, selecione o arquivo de imagem antigo que não foi aprovado. Em seguida, clique em **+ Adicionar novo**, selecione **Versão** e selecione **Documento**.

![WF](./images/wfp26.png)

Selecione o arquivo **2048x2048_buynow.png** e clique em **Abrir**.

![WF](./images/wfp27.png)

Você deveria ficar com isso. Clique em **Criar prova** e selecione novamente **Prova avançada**.

![WF](./images/wfp28.png)

Você verá isso. O **modelo de fluxo de trabalho** agora está pré-selecionado, pois a Workfront presume que o fluxo de trabalho de aprovação anterior ainda é válido. Clique em **Criar prova**.

![WF](./images/wfp29.png)

Selecione **Abrir Prova**.

![WF](./images/wfp30.png)

Agora você pode ver duas versões do arquivo próximas uma da outra.

![WF](./images/wfp31.png)

Clique em **Tomar decisão**, selecione **Aprovado** e clique novamente em **Tomar decisão**.

![WF](./images/wfp32.png)

Feche a pré-visualização da prova.

![WF](./images/wfp33.png)

Você voltará à exibição Tarefa, com um ativo aprovado. Esse ativo agora precisa ser compartilhado na AEM Assets.

![WF](./images/wfp34.png)

Clique no ícone de **Seta de compartilhamento** e selecione sua integração com o AEM Assets, que deve se chamar `--aepUserLdap-- - Citi Signal AEM`.

![WF](./images/wfp35.png)

Clique duas vezes na pasta criada anteriormente, que deve se chamar `--aepUserLdap-- - Workfront Assets`.

![WF](./images/wfp36.png)

Clique em **Selecionar pasta**.

![WF](./images/wfp37.png)

Após 1-2 minutos, seu documento será publicado no AEM Assets. Você verá um ícone do AEM ao lado do nome do documento.

![WF](./images/wfp37a.png)

Clique em **Abrir resumo**.

![WF](./images/wfp38.png)

Vá para **Metadados**, você deve ver isto:

![WF](./images/wfp39.png)

Vá para **Visão geral** e clique em **+ Adicionar** para adicionar uma descrição.

![WF](./images/wfp40.png)

Insira sua descrição. As configurações de prova e documento foram concluídas.

![WF](./images/wfp41.png)

## 1.2.2.5 Exibir o arquivo no AEM Assets

Vá para sua pasta no AEM Assets, chamada `--aepUserLdap-- - Workfront Assets`.

![WF](./images/wfppaem1.png)

Clique nos 3 pontos abaixo da imagem e selecione **Detalhes**.

![WF](./images/wfppaem2.png)

Em seguida, você verá o Formulário de metadados que criou anteriormente, com os valores que foram preenchidos automaticamente pela integração entre o Workfront e o AEM Assets.

![WF](./images/wfppaem3.png)

Voltar para o [Gerenciamento de Fluxo de Trabalho com o Adobe Workfront](./workfront.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
