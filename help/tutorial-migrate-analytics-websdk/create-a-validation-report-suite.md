---
title: Criar um conjunto de relatórios de validação
description: Crie um conjunto de relatórios no Adobe Analytics que você possa usar para validar dados do Web SDK ao migrar seu(s) site(s) da implementação antiga.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16756
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# Criar um conjunto de relatórios de validação

Crie um conjunto de relatórios no Adobe Analytics que você possa usar para validar dados do Web SDK ao migrar seu(s) site(s) da implementação antiga.

Dependendo do tamanho e da complexidade da implementação do Analytics, a migração para o Web SDK pode demorar um pouco. Durante esse período, você deverá validar seu trabalho, certificando-se de que os dados estejam fluindo corretamente para os relatórios do Adobe Analytics. Em vez de enviar esses dados para um conjunto de relatórios junto com os dados de produção ou até mesmo com quaisquer outros dados de desenvolvimento, é uma prática recomendada criar um novo conjunto de relatórios que possa ser usado para essa migração. Na próxima lição, criaremos e configuraremos novos &quot;fluxos de dados&quot; para desenvolvimento, armazenamento temporário e produção. Quando fizermos isso, precisaremos saber a ID do conjunto de relatórios para a configuração.

## Criar o novo conjunto de relatórios

1. Abra o Adobe Analytics e navegue até as configurações do **conjunto de relatórios** no Admin Console

   ![Admin Console](assets/aa-admin-console.jpg).

1. Selecione **[!UICONTROL Adicionar conjunto de relatórios]**

   ![Adicionar conjunto de relatórios](assets/add-report-suite.jpg)

1. Preencha o formulário para criar um novo conjunto de relatórios. Embora você possa optar por criar o novo conjunto de relatórios a partir de um modelo, e até mesmo um modelo em branco, provavelmente funcionará melhor se você escolher a opção **Duplicar um conjunto de relatórios existente** e escolher o conjunto de relatórios que está migrando para o Web SDK. Dessa forma, você terá os mesmos nomes e configurações que testou os dados migrados recentemente, facilitando a validação à medida que avança. Preencha todos os campos obrigatórios e salve seu novo conjunto de relatórios de desenvolvimento de migração.

   ![Novo conjunto de relatórios de desenvolvimento de migração](assets/new-websdk-validation-report-suite.jpg)

1. Anote a ID do novo conjunto de relatórios, pois ela será necessária na próxima lição, à medida que você configurar fluxos de dados para a implementação do Web SDK. É bom lembrar também do título do site, pois ele pode ser usado no Analysis Workspace para escolher o conjunto de relatórios de desenvolvimento de migração no seu projeto do Analytics.

>[!TIP]
>
>Para assistir a uma apresentação em vídeo sobre como criar conjuntos de relatórios, consulte [Noções básicas e como criar conjuntos de relatórios](https://experienceleague.adobe.com/pt-br/docs/analytics-learn/tutorials/intro-to-analytics/analytics-basics/understanding-and-creating-report-suites){target="_blank"}.

