---
title: Introdução ao Workfront
description: Introdução ao Workfront
kt: 5342
doc-type: tutorial
exl-id: 0867d7fd-4d12-46d8-a5ae-bb8db1575635
source-git-commit: a63c01ebe81df39569981d62b85d0461119ecf66
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 1%

---

# 1.2.1 Integração de metadados do Workfront + AEM Assets CS

>[!IMPORTANT]
>
>Para concluir este exercício, você precisa ter acesso a um ambiente de trabalho do AEM Assets CS Author.
>
>Há duas opções a serem consideradas:
>
>- Se você estiver participando do workshop de Ativação técnica da GenStudio para CSC, seus instrutores criaram um ambiente de autor do AEM Assets CS para você. Verifique com eles qual é o nome e como proceder.
>
>- Se você estiver seguindo o caminho completo do tutorial do One Adobe, vá para o exercício [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Siga as instruções aqui e você terá acesso a esse ambiente.

>[!IMPORTANT]
>
>Se você tiver configurado anteriormente um Programa AEM CS com um ambiente AEM Assets CS, pode ser que sua sandbox AEM CS tenha hibernado. Considerando que a deshibernação de uma sandbox desse tipo leva de 10 a 15 minutos, seria uma boa ideia iniciar o processo de deshibernação agora para que você não precise aguardar mais tarde.

## Terminologia de fluxo de trabalho do Workfront 1.2.1.1

A seguir estão os principais objetos e conceitos do Workfront:

| Nome | Última atualização |
| ---------------------- | ------------ | 
| Portfólio | Uma coleção de projetos com características unificadoras. Esses projetos geralmente competem pelos mesmos recursos, orçamento ou período. |
| Programa | Um subconjunto em um portfólio, em que projetos semelhantes podem ser agrupados para alcançar um benefício bem definido. |
| Projeto | Uma grande quantidade de trabalho que deve ser concluída dentro de um período específico e deve usar um orçamento e número de recursos específicos. Para torná-lo gerenciável, divida o projeto em uma série de tarefas. Concluir todas as tarefas resulta na conclusão do projeto. |
| Modelo de projeto | Você pode usar modelos de projeto para capturar a maioria dos processos, informações e configurações repetíveis associados aos projetos em sua organização. Depois de criar modelos, você pode anexá-los a projetos existentes ou usá-los para criar novos projetos. |
| Tarefa | Uma atividade que deve ser executada como uma etapa para atingir uma meta final (concluir o projeto). Tarefas nunca podem existir independentemente. Eles sempre fazem parte de um projeto. |
| Atribuição | Um usuário, função de trabalho ou equipe atribuída a um problema ou tarefa. Projetos, portfólios ou programas não podem ter atribuições. |
| Documento/Versão | Qualquer arquivo anexado a um objeto no Workfront. Sempre que o mesmo documento for carregado no mesmo objeto, um número de versão será atribuído a ele. Os usuários podem exibir e alterar várias opções de uma versão anterior de um documento. |
| Aprovação | Um determinado item de trabalho, como uma tarefa, um documento ou uma folha de horas, pode exigir que um supervisor ou outro usuário faça logoff no item de trabalho. Esse processo de aprovação é chamado de aprovação. |


Ir para [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Clique para abrir o **Workfront**.

![Planejamento Workfront](./../module1.1/images/wfpl1.png)

Você verá isso.

![WF](./images/wfb1.png)

## 1.2.1.1 Configurar a integração do AEM Assets

Clique no ícone **menu** e selecione **Instalação**.

![WF](./images/wfb2.png)

No menu esquerdo, role até **Documentos** e clique em **Experience Manager Assets**. Clique em **+ Adicionar integração com o Experience Manager**.

![WF](./images/wfb3.png)

Para o nome da sua integração, use `--aepUserLdap-- - CitiSignal AEM`.

Abra a lista suspensa **repositório do Experience Manager** e selecione sua instância do AEM CS, que deve ser chamada `--aepUserLdap-- - CitiSignal`.

![WF](./images/wfb5.png)

Em **Metadados**, configure o seguinte mapeamento:

| Campo do Workfront | Campo do Experience Manager Assets |
| --------------- | ------------------------------ | 
| **Documento** > **Nome** | **wm:documentName** |
| **Projeto** > **Nome** | **wm:projectName** |
| **Projeto** > **Descrição** | **wm:projectDescription** |
| **Solicitação de documentos** > **Status** | **wm:wm:documentStatus** |
| **Tarefa** > **Nome** | **wm:taskName** |
| **Tarefa** > **Descrição** | **wm:taskDescription** |
| **Projeto** > **ID** | **wm:projectId** |

Habilite o comutador para **Sincronizar metadados do objeto**.

Clique em **Salvar**.

![WF](./images/wfb6.png)

Sua integração do Workfront com o AEM Assets CS está configurada.

![WF](./images/wfb7.png)

## 1.2.1.2 Configurar a integração de metadados com o AEM Assets

Em seguida, é necessário configurar o AEM Assets CS para que os campos de metadados do ativo no Workfront sejam compartilhados com o AEM Assets CS.

Para fazer isso, vá para [https://experience.adobe.com/](https://experience.adobe.com/). Clique em **Experience Manager Assets**.

![WF](./images/wfbaem1.png)

Clique para selecionar seu ambiente AEM Assets, que deve ser nomeado como `--aepUserLdap-- - CitiSignal dev`.

![WF](./images/wfbaem2.png)

Você deverá ver isso. No menu esquerdo, vá para **Assets**.

![WF](./images/wfbaem3.png)

Em seguida, clique em **Criar pasta**.

![WF](./images/wfbaem3a.png)

Nomeie sua pasta `--aepUserLdap-- - CitiSignal Fiber Launch Assets` e clique em **Criar**.

![WF](./images/wfbaem4.png)

Em seguida, vá para **Metadata Forms** no menu esquerdo e clique em **Criar**.

![WF](./images/wfbaem5.png)

Use o nome `--aepUserLdap-- - Metadata Form` e clique em **Criar**.

![WF](./images/wfbaem6.png)

Adicione 7 novos campos **Texto de linha única** ao formulário e selecione o primeiro campo. Em seguida, clique no ícone **Esquema** ao lado do campo **Propriedade de metadados** para o primeiro campo.

![WF](./images/wfbaem7.png)

Você então verá esse pop-up. No campo de pesquisa, digite `wm:project` e selecione o campo **Nome do Projeto**. Clique em **Selecionar**.

![WF](./images/wfbaem11.png)

Altere o rótulo do campo para `Project Name`. Clique em **Salvar**.

![WF](./images/wfbaem12.png)

Vá para o segundo campo e clique no ícone **Esquema** ao lado do campo **Propriedade de metadados**.

![WF](./images/wfbaem12a.png)

No campo de pesquisa, insira `wm:project` e selecione o campo **Descrição do Projeto**. Clique em **Selecionar**.

![WF](./images/wfbaem8.png)

Altere o rótulo do campo para `Project Description`.

![WF](./images/wfbaem9.png)

Em seguida, selecione o terceiro campo e clique novamente no ícone **Esquema** ao lado do campo **Propriedade de metadados**.

![WF](./images/wfbaem10b.png)

Você verá esse pop-up novamente. No campo de pesquisa, digite `wm:project` e selecione o campo **ID do Projeto**. Clique em **Selecionar**.

![WF](./images/wfbaem10.png)

Altere o rótulo do campo para `Project ID`.

![WF](./images/wfbaem10a.png)

Em seguida, selecione o quarto campo e clique novamente no ícone **Esquema** ao lado do campo **Propriedade de metadados**.

![WF](./images/wfbaem11a.png)

Você verá esse pop-up novamente. No campo de pesquisa, digite `wm:document` e selecione o campo **ID do Projeto**. Clique em **Selecionar**.

![WF](./images/wfbaem101.png)

Altere o rótulo do campo para `Document Status`.

![WF](./images/wfbaem102.png)

Em seguida, selecione o quinto campo e clique no ícone **Esquema** ao lado do campo **Propriedade de metadados** novamente.

![WF](./images/wfbaem103.png)

Você verá esse pop-up novamente. No campo de pesquisa, digite `wm:document` e selecione o campo **ID do Projeto**. Clique em **Selecionar**.

![WF](./images/wfbaem104.png)

Altere o rótulo do campo para `Document Name`.

![WF](./images/wfbaem105.png)

Em seguida, selecione o sexto campo e clique novamente no ícone **Esquema** ao lado do campo **Propriedade de metadados**.

![WF](./images/wfbaem106.png)

Você verá esse pop-up novamente. No campo de pesquisa, digite `wm:task` e selecione o campo **Nome da Tarefa**. Clique em **Selecionar**.

![WF](./images/wfbaem107.png)

Altere o rótulo do campo para `Task Name`.

![WF](./images/wfbaem108.png)

Em seguida, selecione o sétimo campo e clique no ícone **Esquema** ao lado do campo **Propriedade de metadados** novamente.

![WF](./images/wfbaem109.png)

Você verá esse pop-up novamente. No campo de pesquisa, digite `wm:task` e selecione o campo **Descrição da Tarefa**. Clique em **Selecionar**.

![WF](./images/wfbaem110.png)

Altere o rótulo do campo para `Task Description`.

![WF](./images/wfbaem111.png)

Altere o **Nome da guia** no formulário para `--aepUserLdap-- - Workfront Metadata`.

![WF](./images/wfbaem13.png)

Clique em **Salvar** e **Fechar**.

![WF](./images/wfbaem13a.png)

Seu **Formulário de Metadados** está configurado.

![WF](./images/wfbaem14.png)

Em seguida, é necessário atribuir o Formulário de metadados à pasta criada anteriormente. Marque a caixa de seleção do formulário de metadados e clique em **Atribuir às pastas**.

![WF](./images/wfbaem15.png)

Selecione sua pasta, que deve se chamar `--aepUserLdap-- - CitiSignal Fiber Launch Assets`. Clique em **Atribuir**.

![WF](./images/wfbaem16.png)

O formulário de metadados agora está atribuído à sua pasta com sucesso.

![WF](./images/wfbaem17.png)

Próxima Etapa: [1.2.2 Revisão com o Workfront](./ex2.md){target="_blank"}

Voltar para o [Gerenciamento de Fluxo de Trabalho com o Adobe Workfront](./workfront.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
