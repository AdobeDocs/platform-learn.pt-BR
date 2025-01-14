---
title: Criar as alterações de implementação na biblioteca de desenvolvimento
description: Saiba como criar alterações feitas na biblioteca de desenvolvimento na propriedade de tags para testar os resultados no site de desenvolvimento.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16762
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---


# Criar as alterações de implementação na biblioteca de desenvolvimento

Saiba como criar alterações feitas na biblioteca de desenvolvimento na propriedade de tags para testar os resultados no site de desenvolvimento.

Conforme você avança neste tutorial, ou sempre que faz alterações na implementação, será necessário criar/publicar essas alterações para vê-las nos sites de desenvolvimento, preparo ou produção. Tenho certeza de que você já fez isso antes, pois este é um documento de migração e não um documento de primeira implementação. Na realidade, você desejará fazer isso com frequência, à medida que executa cada função e deseja testá-la e garantir que esteja funcionando corretamente, enviando os dados corretos para o Analytics.

Portanto, haverá alguns lembretes neste tutorial para criar ou publicar suas alterações. Se necessário, coloque um marcador nesta página e não tenha receio de criar em sua biblioteca de desenvolvimento. Você pode fazer isso a qualquer momento.

Então, vamos construir o que fizemos até agora. A propósito, às vezes podemos trocar &quot;criar&quot; e &quot;publicar&quot; neste tutorial. O mais importante é saber se você está &quot;criando&quot; para uma biblioteca de desenvolvimento ou de preparo, ou se está &quot;publicando&quot; para a biblioteca e o ambiente de produção, independentemente da palavra usada.

## Criar alterações de migração para desenvolvimento em tags Experience Platform

1. Enquanto estiver na propriedade nas tags Experience Platform, selecione **Fluxo de publicação** na navegação à esquerda e adicione uma nova biblioteca.

   ![Fluxo de publicação](assets/publishing-flow-new-library.jpg)

1. Nomeie a biblioteca como desejar, por exemplo **Migração inicial do Web SDK**.
1. Selecione o ambiente **Desenvolvimento**.
1. Selecione **Adicionar todos os recursos alterados** para adicionar todos os itens nos quais você está trabalhando.

   ![Nova biblioteca](assets/new-library-websdk-migration.jpg)

1. Salvar e criar no desenvolvimento

   ![Salvar e criar no desenvolvimento](assets/save-and-build-to-dev.jpg)

1. Quando a build for concluída, você poderá ver se a build foi bem-sucedida. Passe o mouse sobre o ponto verde à esquerda da nova biblioteca no fluxo de publicação e, na verdade, se estiver verde, a conclusão será bem-sucedida e isso será informado.

   ![Publicação bem-sucedida](assets/successful-publish.jpg)

### Selecionar uma biblioteca de trabalho

Este é um bom atalho ao realizar edições em tags. Em vez de percorrer todo o fluxo de publicação sempre que fizer uma alteração, você pode escolher uma biblioteca de trabalho e salvar e criar com apenas um clique. Faça isso. Você me agradecerá mais tarde.

1. Em qualquer lugar na interface do usuário de tags, clique em Selecionar uma biblioteca de trabalho na parte superior direita da interface e escolha a que deseja. Para este tutorial, escolha Migração inicial do Web SDK.

   ![Selecionar biblioteca de trabalho](assets/select-working-library.jpg)

