---
title: Criar um elemento de dados Variable
description: Adicione um elemento de dados que será criado sobre várias regras e enviado para o Edge Network e encaminhado para o Adobe Analytics
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16759
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# Criar um elemento de dados Variable

Adicione um elemento de dados que será construído sobre várias regras e, em seguida, enviado para o Edge Network e encaminhado para o Adobe Analytics.

Esse elemento de dados criará o objeto &quot;Dados&quot;, que será usado para transmitir as variáveis do Adobe Analytics (props, eVars, eventos etc.) de volta para o Adobe Analytics e o Adobe Target. Assim, da mesma forma que a criação do &quot;objeto s&quot; em uma implementação de AppMeasurement no Analytics, criaremos esse tipo: objeto de variável a ser acessado e atualizado nas regras, e que pode ser usado para preencher props e eVars no Analytics.

1. Na interface da coleção de dados, clique em **Elementos de Dados** na navegação à esquerda.

   Você será direcionado para a página de aterrissagem dos elementos de dados, onde verá todos os elementos de dados pré-existentes. Precisamos criar um novo elemento de dados para facilitar a migração. Clique em **Adicionar elemento de dados**.

   ![Adicionar elemento de dados](assets/add-new-data-alement.jpg)

1. Configure o elemento de dados.
   1. Dê um nome ao elemento de dados, algo que o ajude a lembrar que ele está criando os dados na sua página e que esse será o tipo &quot;Variável&quot;. Neste tutorial, vamos chamá-lo de **Variável de dados de exibição de página**.
   1. Selecione **Adobe Experience Platform Web SDK** no menu suspenso Extensão.
   1. Selecione **Variável** no menu suspenso **Tipo de Elemento de Dados**.
   1. No painel direito, selecione o botão de opção **Dados**.
   1. Verifique a solução **Adobe Analytics** e qualquer outra solução que você também está migrando. Por exemplo, **Adobe Target** aparecendo nesta captura de tela.
1. Clique em **Salvar**.

   ![Configurar elemento de dados de variável](assets/configure-variable-data-element.jpg)
