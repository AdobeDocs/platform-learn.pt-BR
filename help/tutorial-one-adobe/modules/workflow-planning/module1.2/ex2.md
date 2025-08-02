---
title: Prova com o Workfront
description: Prova com o Workfront
kt: 5342
doc-type: tutorial
exl-id: 5feb9486-bdb4-4d59-941c-09fc2e38163b
source-git-commit: 42f6d8a07baa03a9ab31cff0ef518ae2c5ad930e
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---

# 1.2.2 Prova com o Workfront

>[!IMPORTANT]
>
>Se você tiver configurado anteriormente um Programa AEM CS com um ambiente AEM Assets CS, pode ser que sua sandbox AEM CS tenha hibernado. Considerando que a deshibernação de uma sandbox desse tipo leva de 10 a 15 minutos, seria uma boa ideia iniciar o processo de deshibernação agora para que você não precise aguardar mais tarde.

## 1.2.2.1 Criar um Novo Fluxo de Aprovação

Volte para **Adobe Workfront**. Clique no ícone **menu** e selecione **Revisão**.

![WF](./images/wfp1.png)

Vá para **Workflows**, clique em **+ Novo** e selecione **Novo modelo**.

![WF](./images/wfp2.png)

Defina o **Nome do modelo** como `--aepUserLdap-- - Approval Workflow` e defina o **Proprietário do modelo** como você mesmo.

![WF](./images/wfp3.png)

Role para baixo e, em **Estágios** > **Estágio 1**, adicione-se com a **Função** do **Revisor e Aprovador**.

Clique em **Criar**.

![WF](./images/wfp4.png)

O fluxo de trabalho básico de aprovação agora está pronto para ser usado.

![WF](./images/wfp5.png)

## 1.2.2.2 Criar um novo projeto

Abra o **menu** e vá para **Programas**.

![WF](./images/wfp6a.png)

Clique no programa que você criou antes, chamado `--aepUserLdap-- CitiSignal Fiber Launch`.

>[!NOTE]
>
>Você criou um programa como parte do exercício no [Workfront Planning](./../module1.1/ex1.md) com a automação que criou e executou. Se você ainda não tiver feito isso, poderá encontrar as instruções lá.

![WF](./images/wfp6b.png)

No seu programa, vá para **Projetos**. Clique em **+ Novo projeto** e selecione **Novo projeto**.

![WF](./images/wfp6.png)

Você deverá ver isso. Altere o nome para `--aepUserLdap-- - CitiSignal Fiber Launch`.

![WF](./images/wfp6c.png)

Vá para **Detalhes do projeto**. Clique em **+Adicionar** em **Descrição**.

![WF](./images/wfp6d.png)

Defina a descrição como `The CitiSignal Fiber Launch project is used to plan the upcoming launch of CitiSignal Fiber.`

Clique em **Salvar alterações**.

![WF](./images/wfp6e.png)

Seu projeto foi criado.

![WF](./images/wfp7.png)

## 1.2.2.3 Criar uma nova tarefa

Vá para **Tarefas** e clique em **+ Nova Tarefa**.

![WF](./images/wfp7a.png)

Digite este nome para sua tarefa: `Create assets for Fiber campaign`.

Definir o campo **Descrição** como: `This task is used to track the progress of the creation of the assets for the CitiSignal Fiber Launch Campaign.`

Clique em **Criar tarefa**.

![WF](./images/wfp8.png)

Você deverá ver isso.

![WF](./images/wfp9.png)

Na coluna **Atribuição**, adicione seu próprio nome.

![WF](./images/wfp9a.png)

A tarefa será atribuída a você.

![WF](./images/wfp9b.png)

## 1.2.2.4 Adicionar um novo Documento à sua Tarefa passar pelo fluxo de aprovação

Clique no logotipo **Workfront** para voltar à página de visão geral. Você deverá ver o projeto que acabou de criar aparecer na visão geral. Clique no projeto para abri-lo.

![WF](./images/wfp9c.png)

Em **Tarefas**, clique em para abrir a tarefa.

![WF](./images/wfp9d.png)

Ir para **Documentos**. Clique em **+ Adicionar novo** e selecione **Documento**.

![WF](./images/wfp10.png)

Baixe [este arquivo](./images/2048x2048.png) na área de trabalho.

![WF](./images/2048x2048.png){width="50px" align="left"}

Selecione o arquivo **2048x2048.png** e clique em **Abrir**.

![WF](./images/wfp12.png)

Você deveria ficar com isso. Passe o mouse sobre o documento carregado. Clique em **Criar prova** e escolha **Prova avançada**.

![WF](./images/wfp13.png)

Na janela **nova prova**, selecione **Automatizado** e, em seguida, selecione o modelo de fluxo de trabalho criado anteriormente, que deve ser nomeado como `--aepUserLdap-- - Approval Workflow`. Clique em **Criar prova**.

![WF](./images/wfp14.png)

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

Retorne à sua **Tarefa** e ao **Documento**. Agora é necessário carregar uma segunda imagem que considere os comentários fornecidos.

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

Clique no **Nome da Tarefa** para voltar para a visão geral da Tarefa.

![WF](./images/wfp33.png)

Você voltará à exibição Tarefa, com um ativo aprovado. Esse ativo agora precisa ser compartilhado na AEM Assets.

![WF](./images/wfp34.png)

Selecione o documento aprovado. Clique no ícone de **Seta de compartilhamento** e selecione sua integração com o AEM Assets, que deve se chamar `--aepUserLdap-- - CitiSignal AEM`.

![WF](./images/wfp35.png)

Clique duas vezes na pasta criada anteriormente, que deve se chamar `--aepUserLdap-- - CitiSignal Fiber Launch Assets`.

![WF](./images/wfp36.png)

Clique em **Selecionar pasta**.

![WF](./images/wfp37.png)

Após 1-2 minutos, seu documento será publicado no AEM Assets. Você verá um ícone do AEM ao lado do nome do documento.

![WF](./images/wfp37a.png)

Clique em **Marcar como concluído** para concluir esta tarefa.

![WF](./images/wfp37b.png)

Você deverá ver isso.

![WF](./images/wfp37c.png)

## 1.2.2.5 Exibir seu arquivo no AEM Assets

Vá para sua pasta no AEM Assets CS, chamada `--aepUserLdap-- - CitiSignal Fiber Launch Assets`.

![WF](./images/wfppaem1.png)

Selecione a imagem e escolha **Detalhes**.

![WF](./images/wfppaem2.png)

Em seguida, você verá o Formulário de metadados que criou anteriormente, com os valores que foram preenchidos automaticamente pela integração entre o Workfront e o AEM Assets.

![WF](./images/wfppaem3.png)

Voltar para o [Gerenciamento de Fluxo de Trabalho com o Adobe Workfront](./workfront.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
