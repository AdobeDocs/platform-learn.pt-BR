---
title: Prova com o Workfront
description: Prova com o Workfront
kt: 5342
doc-type: tutorial
exl-id: 5feb9486-bdb4-4d59-941c-09fc2e38163b
source-git-commit: da966703aed5342000c19732b6b48682c3958c7f
workflow-type: tm+mt
source-wordcount: '1279'
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

Role para baixo e, em **Estágios** > **Estágio 1**, altere a função de **Criador de provas** para **Revisor e Aprovador**. Você também pode adicionar qualquer outra pessoa, por exemplo, adicionar a si mesmo selecionando seu usuário e definindo a **Função** de **Revisor e Aprovador**.

Clique em **Criar**.

![WF](./images/wfp4.png)

O fluxo de trabalho básico de aprovação agora está pronto para ser usado.

![WF](./images/wfp5.png)

## 1.2.2.2 Habilitar o Workfront Blueprint

Na próxima etapa, você criará um novo projeto usando um modelo. A Adobe Workfront fornece vários blueprints disponíveis que precisam ser ativados.

Para o caso de uso do CitiSignal, o blueprint **Integrated Campaign Execution** é o que você precisa usar.

Para instalar esse blueprint, abra o menu e selecione **Blueprints**.

![WF](./images/blueprint1.png)

Selecione o filtro **Marketing** e role para baixo para encontrar o blueprint **Execução de campanha integrada**. Clique em **Instalar**.

![WF](./images/blueprint2.png)

Clique em **Continuar**.

![WF](./images/blueprint3.png)

Clique em **Instalar como está...**.

![WF](./images/blueprint4.png)

Você deverá ver isso. A instalação pode levar alguns minutos.

![WF](./images/blueprint5.png)

Após alguns minutos, o blueprint será instalado.

![WF](./images/blueprint6.png)

## 1.2.2.3 Criar um novo projeto

Abra o **menu** e vá para **Programas**.

![WF](./images/wfp6a.png)

Clique no programa que você criou antes, chamado `--aepUserLdap-- CitiSignal Fiber Launch`.

>[!NOTE]
>
>Você criou um programa como parte do exercício no [Workfront Planning](./../module1.1/ex1.md) com a automação que criou e executou. Se você ainda não tiver feito isso, poderá encontrar as instruções lá.

![WF](./images/wfp6b.png)

No seu programa, vá para **Projetos**. Clique em **+ Novo projeto** e selecione **Novo projeto do modelo**.

![WF](./images/wfp6.png)

Selecione o modelo **Integrated Campaign Execution** e clique em **Usar modelo**.

![WF](./images/wfp6g.png)

Você deverá ver isso. Altere o nome para `--aepUserLdap-- - CitiSignal Fiber Launch Winter 2026` e clique em **Criar projeto**.

![WF](./images/wfp6c.png)

Seu projeto foi criado. Vá para **Detalhes do projeto**.

![WF](./images/wfp6h.png)

Vá para **Detalhes do projeto**. Clique para selecionar o texto atual em **Descrição**.

![WF](./images/wfp6d.png)

Defina a descrição como `The CitiSignal Fiber Launch project is used to plan the upcoming launch of CitiSignal Fiber.`

Clique em **Salvar alterações**.

![WF](./images/wfp6e.png)

Seu projeto está pronto para ser usado.

![WF](./images/wfp7.png)

As tarefas e dependências no projeto foram criadas com base no modelo escolhido e definido como. proprietário do projeto. O status do projeto foi definido como **Planning**. Você pode alterar o status do projeto selecionando outro valor na lista.

![WF](./images/wfp7z.png)

## 1.2.2.4 Criar uma nova tarefa

Passe o mouse sobre a tarefa **Começar a Criar Modelos de Design** e clique nos 3 pontos **...**.

![WF](./images/wfp7a.png)

Selecione a opção **Inserir tarefa abaixo**.

![WF](./images/wfp7x.png)

Digite este nome para sua tarefa: `Create layout using approved assets and copy`.

Defina o campo **Atribuições** para a função **Designer**.
Defina o campo **Duração** para **5 dias**.
Definir a predecessora do campo como **9**.
Insira uma data para os campos **Início em** e **Conclusão em**.

Clique em outro lugar na tela para salvar a nova tarefa.

![WF](./images/wfp8.png)

Você deverá ver isso. Clique na tarefa para abri-la.

![WF](./images/wfp9.png)

Vá para **Detalhes da tarefa** e defina o campo **Descrição** como: `This task is used to track the progress of the creation of the assets for the CitiSignal Fiber Launch Campaign.`

Clique em **Salvar alterações**.

![WF](./images/wfp9a.png)

Você deverá ver isso. Clique no campo **Projeto** para voltar ao seu projeto.

![WF](./images/wfp9b.png)

No modo de exibição **Projeto**, vá para **Balanceador de Carga de Trabalho**.

![WF](./images/wfpwlb1.png)

Clique em **Atribuições em massa**.

![WF](./images/wfpwlb2.png)

Selecione a **Atribuição de função** do **Designer** e clique no campo **Usuário a ser atribuído**. Isso mostrará todos os usuários que têm uma função do **Designer** na sua instância do Workfront. Nesse caso, selecione o usuário fictício **Melissa Jenkins**.

![WF](./images/wfpwlb3.png)

Clique em **Atribuir**. O usuário que você selecionou será atribuído agora às tarefas do projeto que estão vinculadas à função **Designer**.

![WF](./images/wfpwlb4.png)

As tarefas agora estão atribuídas. Clique em **Tarefas** para voltar para a página de visão geral de **Tarefas**.

![WF](./images/wfpwlb5.png)

Clique na tarefa que você criou, chamada
**Criar layout usando ativos aprovados e copiar**.

![WF](./images/wfpwlb6.png)

Agora você começará a trabalhar nessa tarefa como parte desse exercício. Você pode ver que Melissa Jenkins está atribuída a esta tarefa no momento. Para alterar isso para você mesmo, clique no campo **Atribuições** e selecione **Atribuir a mim**.

![WF](./images/wfpwlb7.png)

Clique em **Salvar**.

![WF](./images/wfpwlb8.png)

Clique em **Trabalhar nisto**.

![WF](./images/wfpwlb9.png)

Você deverá ver isso.

![WF](./images/wfpwlb10.png)

Como parte dessa tarefa, você precisa criar uma nova imagem e carregá-la como um documento no Workfront. Agora você mesmo criará esse ativo usando o Adobe Express.

## 1.2.2.5 Adicione um novo Documento ao seu Projeto e inicie o fluxo de aprovação

Para este exercício, você precisa baixar e usar este ativo: [timetravelnow.png](./images/timetravelnow.png)

![WF](./images/timetravelnow.png)

Vá para **Documentos** da sua Tarefa. Clique em **+ Adicionar novo** e selecione **Documento**.

![WF](./images/wfp10.png)

Clique para selecionar o arquivo `timetravelnow.png`. Clique em **Abrir**.

![WF](./images/wfp10a.png)

Você deveria ficar com isso.

![WF](./images/wfp10b.png)

Passe o mouse sobre o documento carregado. Clique em **Criar prova** e escolha **Prova avançada**.

![WF](./images/wfp13.png)

Na janela **nova prova**, selecione **Automatizado** e, em seguida, selecione o modelo de fluxo de trabalho criado anteriormente, que deve ser nomeado como `--aepUserLdap-- - Approval Workflow`. Clique em **Criar prova**.

![WF](./images/wfp14.png)

Clique em **Abrir prova**

![WF](./images/wfp18.png)

Agora você pode revisar a prova. Selecione **Adicionar comentário** para adicionar um comentário que exija que o documento seja alterado.

![WF](./images/wfp19.png)

Insira seu comentário e clique em **Postar**. Em seguida, clique em **Tomar uma decisão**.

![WF](./images/wfp20.png)

Selecione **Alterações necessárias** e clique em **tomar uma decisão**.

![WF](./images/wfp24.png)

Retorne à sua **Tarefa** e ao **Documento**. Você verá que o texto **Alterações necessárias** também aparece lá.

![WF](./images/wfp25.png)

Agora é necessário fazer alterações de design e fazer upload de uma nova versão da imagem.

## 1.2.2.6 Adicione uma nova versão do documento à sua tarefa

Para este exercício, você precisa baixar e usar este ativo: [getonboard.png](./images/getonboard.png)

![WF](./images/getonboard.png)

Na Visualização de tarefa no Adobe Workfront, selecione o arquivo de imagem antigo que não foi aprovado. Em seguida, clique em **+ Adicionar novo**, selecione **Versão** e escolha **Documento**.

![WF](./images/wfp26.png)

Clique para selecionar o arquivo `getonboardnow.png`. Clique em **Abrir**.

![WF](./images/wfp26a.png)

Você deveria ficar com isso. Clique em **Criar prova** e selecione novamente **Prova avançada**.

![WF](./images/wfp28.png)

Você verá isso. O **modelo de fluxo de trabalho** agora está pré-selecionado, pois a Workfront presume que o fluxo de trabalho de aprovação anterior ainda é válido. Clique em **Criar prova**.

![WF](./images/wfp29.png)

Selecione **Abrir Prova**.

![WF](./images/wfp30.png)

Agora você pode ver duas versões do arquivo próximas uma da outra. Clique no botão **Comparar provas**.

![WF](./images/wfp31.png)

Você deverá ver ambas as versões da imagem próximas uma da outra. Clique em **Tomar decisão**.

![WF](./images/wfp32.png)

Selecione **Aprovado** e clique em **Tomar decisão** novamente.

![WF](./images/wfp32a.png)

Feche a exibição **Comparar provas** fechando a versão esquerda da imagem. Clique no **Nome da Tarefa** para voltar para a visão geral da Tarefa.

![WF](./images/wfp33.png)

Você voltará à exibição Tarefa, com um ativo aprovado. Esse ativo agora precisa ser compartilhado na AEM Assets.

![WF](./images/wfp34.png)

Selecione o documento aprovado. Clique no ícone de **Seta de compartilhamento** e selecione sua integração com o AEM Assets, que deve se chamar `--aepUserLdap-- - CitiSignal AEM+ACCS`.

![WF](./images/wfp35.png)

Clique duas vezes na pasta criada anteriormente, que deve se chamar `--aepUserLdap-- - CitiSignal Fiber Campaign`.

![WF](./images/wfp36.png)

Clique em **Selecionar pasta**.

![WF](./images/wfp37.png)

Após 1-2 minutos, seu documento será publicado no AEM Assets. Você verá um ícone do AEM ao lado do nome do documento.

![WF](./images/wfp37a.png)

Clique em **Marcar como concluído** para concluir esta tarefa.

![WF](./images/wfp37b.png)

Você deverá ver isso.

![WF](./images/wfp37c.png)

## 1.2.2.7 Exibir seu arquivo no AEM Assets

Vá para sua pasta no AEM Assets CS, chamada `--aepUserLdap-- - CitiSignal Fiber Campaign`.

![WF](./images/wfppaem1.png)

Selecione a imagem e escolha **Detalhes**.

![WF](./images/wfppaem2.png)

Em seguida, você verá o Formulário de metadados que criou anteriormente, com os valores que foram preenchidos automaticamente pela integração entre o Workfront e o AEM Assets.

![WF](./images/wfppaem3.png)

Voltar para o [Gerenciamento de Fluxo de Trabalho com o Adobe Workfront](./workfront.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
