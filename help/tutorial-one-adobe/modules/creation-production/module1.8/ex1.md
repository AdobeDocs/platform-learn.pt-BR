---
title: Introdução ao Workfront, Frame.io e ESM
description: Introdução ao Workfront, Frame.io e ESM
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 2f9a3eef-16ef-497c-97f7-377ff9ed2f82
source-git-commit: 8f746831d4a1481f8ccc14539273c4b16ca5170b
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 1%

---

# 1.8.1 Introdução ao Workfront, Frame.io e ESM

## Terminologia de fluxo de trabalho do Workfront 1.8.1.1

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

![Planejamento Workfront](./images/wfpl1.png)

Você verá isso.

![WF](./images/wfb1.png)

## 1.8.1.2 Habilitar o Workfront Blueprint

Na próxima etapa, você criará um novo projeto usando um modelo. A Adobe Workfront fornece vários blueprints disponíveis que precisam ser ativados.

Para o caso de uso do CitiSignal, o blueprint **Integrated Campaign Execution** é o que você precisa usar.

Para instalar esse blueprint, abra o menu e selecione **Blueprints**.

![WF](./images/blueprint1.png)

Selecione o filtro **Marketing** e role para baixo para encontrar o blueprint **Execução de campanha integrada**. Clique em **Instalar**.

![WF](./images/blueprint2.png)

Clique em **Continuar**.

![WF](./images/blueprint3.png)

Altere o **Nome do Modelo de Projeto** para `--aepUserLdap-- - Integrated Campaign Execution`.

Clique em **Instalar blueprint**.

![WF](./images/blueprint4.png)

Após alguns minutos, o blueprint será instalado.

![WF](./images/blueprint6.png)

## 1.8.1.3 Criar um novo projeto

Abra o **menu** e vá para **Portfólios**.

![WF](./images/wfp6a.png)

Clique em **+ Novo Portfolio**.

![WF](./images/wfpfolio1.png)

Insira o nome do portfólio `--aepUserLdap-- - CitiSignal`.

![WF](./images/wfpfolio2.png)

Vá para **Programas** e clique em **+ Novo Programa**. Selecione **Novo Programa**.

![WF](./images/wfnp1.png)

Digite o nome do programa: `--aepUserLdap-- - CitiSignal Fiber Launch`.

![WF](./images/wfp6b.png)

No seu programa, vá para **Projetos**. Clique em **+ Novo projeto** e selecione **Novo projeto do modelo**.

![WF](./images/wfp6.png)

Selecione o modelo `--aepUserLdap-- - Integrated Campaign Execution` e clique em **Usar modelo**.

![WF](./images/wfp6g.png)

Você deverá ver isso. Altere o nome para `--aepUserLdap-- - CitiSignal Fiber Launch Winter 2026` e clique em **Criar projeto**.

![WF](./images/wfp6c.png)

Seu projeto foi criado. Vá para **Detalhes do projeto**.

![WF](./images/wfp6h.png)

Vá para **Detalhes do projeto**. Clique para selecionar o texto atual em **Descrição**.

Defina a descrição como `The CitiSignal Fiber Launch project is used to plan the upcoming launch of CitiSignal Fiber.`

Clique em **Salvar alterações**.

![WF](./images/wfp6e.png)

Seu projeto está pronto para ser usado.

![WF](./images/wfp7.png)

As tarefas e dependências no projeto foram criadas com base no modelo escolhido e definido como. proprietário do projeto. O status do projeto foi definido como **Planning**. Você pode alterar o status do projeto selecionando outro valor na lista.

![WF](./images/wfp7z.png)

## Exibição de projeto 1.8.1.4 no Frame.io

Ir para [https://next.frame.io/](https://next.frame.io/){target="_blank"}. Faça logon e selecione a instância a ser usada, neste exemplo **Experience Platform International ESM**. Você observará que já existe uma pasta no Frame.io para o projeto que acabou de criar. A pasta é nomeada com base no nome do projeto inserido anteriormente.

Esse é um recurso do Enterprise Storage Management, uma solução de armazenamento baseada em nuvem que serve como repositório central para ativos em produtos corporativos da Adobe, incluindo Workfront e Frame.io.

Os principais benefícios do armazenamento corporativo da Adobe incluem:

- Camada de armazenamento unificado para ativos criativos e de gerenciamento de trabalho
- Permissões centralizadas via Adobe Identity Management system (IMS) para controle de acesso seguro
- Visibilidade completa de ativos no Workfront e Frame.io
- Gerenciamento dimensionável de armazenamento e cotas para as necessidades corporativas

![WF](./images/fio1.png)

## 1.8.1.5 Criar uma nova tarefa

Volte para o Workfront. Vá para **Tarefas**, passe o mouse sobre a tarefa **Começar a Criar Modelos de Design** e clique nos três pontos **...**.

![WF](./images/wfp7a.png)

Selecione a opção **Inserir tarefa abaixo**.

![WF](./images/wfp7x.png)

Digite este nome para sua tarefa: `Create layout using approved assets and copy`.

Defina o campo **Atribuições** para a função **Designer**.
Defina o campo **Duração** para **5 dias**.
Definir a predecessora do campo como **9**.
Insira uma data para os campos **Início em** e **Conclusão em** (a data de início desta tarefa deve ser agendada após a data de término da tarefa anterior).

Clique em outro lugar na tela para salvar a nova tarefa.

![WF](./images/wfp8.png)

Você deverá ver isso. Clique na tarefa para abri-la.

![WF](./images/wfp9.png)

Vá para **Detalhes da tarefa** e defina o campo **Descrição** como: `This task is used to track the progress of the creation of the assets for the CitiSignal Fiber Launch Campaign.`

Clique em **Salvar alterações**.

![WF](./images/wfp9a.png)

Você deverá ver isso. Clique no campo **Atribuições** e selecione **Atribuir a mim**.

![WF](./images/wfpwlb7.png)

Clique em **Salvar**.

![WF](./images/wfpwlb8.png)

Clique em **Trabalhar nisto**.

![WF](./images/wfpwlb9.png)

Você deverá ver isso.

![WF](./images/wfpwlb10.png)

Como parte dessa tarefa, um novo ativo precisa ser criado. Na próxima etapa, primeiro você fornecerá imagens de referência no Workfront para que o designer saiba o que é esperado. Em seguida, você mudará para a função do Designer e criará esse ativo sozinho usando o Adobe Express.

## 1.8.1.6 Carregar imagens de referência

Baixe as imagens de referência [aqui](./assets/reference_images.zip) no seu desktop e descompacte-as.

![WF](./images/wfrefimg1.png)

No Workfront, navegue até o nível **Projeto**.

![WF](./images/wfrefimg2.png)

Vá para **Documentos**, clique em **+ Adicionar novo** e selecione **Documento**.

![WF](./images/wfrefimg3.png)

Navegue até a pasta que você baixou que contém as imagens de referência. Selecione todas as imagens e clique em **Abrir**.

![WF](./images/wfrefimg4.png)

Após alguns minutos, todas as imagens serão carregadas e anexadas ao projeto.

![WF](./images/wfrefimg5.png)

Com as imagens de referência instaladas, o designer agora pode criar o novo ativo para essa campanha.

## Próximas etapas

Próxima etapa: [Criar um novo ativo, revisá-lo e aprová-lo](./ex2.md){target="_blank"}

Retorne para [Revisão e aprovação unificadas com Workfront, Frame.io e Enterprise Storage Management](./esm.md){target="_blank"}

Voltar para [Todos os Módulos](./../../../overview.md){target="_blank"}
