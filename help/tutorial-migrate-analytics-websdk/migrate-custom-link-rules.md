---
title: Migrar regras de links personalizados
description: Saiba como migrar regras que enviam ocorrências de link personalizado (em vez de exibições de página).
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16765
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 0%

---


# Migrar regras de links personalizados

Neste exercício, você aprenderá a migrar regras que enviam ocorrências de link personalizadas (em vez de exibições de página).

## Visão geral

Ao enviar uma ocorrência de link personalizado por meio da extensão do Analytics, ou código de AppMeasurement, ao configurar a ação **Enviar beacon**, você também escolherá se enviará uma ocorrência de exibição de página ou uma ocorrência de link personalizado e, se escolher uma ocorrência de link personalizado, ela solicitará o **Nome do link** e o **Tipo de link** para essa ocorrência. Se você não estiver enviando outros dados variáveis além do nome e do tipo do link, não será necessário ter uma ação adicional que defina variáveis (props, eVars e eventos).
Por isso, ao migrar regras que são de links personalizados, você terá **um dos dois** cenários a seguir nas regras:

1. A regra existente conterá uma ação **Adobe Analytics - Definir variáveis** que define props, eVars, eventos etc., e conterá uma ação **Adobe Analytics - Enviar beacon** que define a ocorrência para uma ocorrência de link personalizado (OU seja, uma ocorrência s.tl()), define o nome e o tipo do link e envia os dados.
   1. Nesse caso, ele provavelmente também conterá uma ação final chamada **Adobe Analytics - Limpar Variáveis**, para &quot;zerar&quot; o valor das variáveis depois que os dados forem enviados aos servidores Adobe.
1. A regra existente conterá apenas a ação **Adobe Analytics - Enviar Beacon** que define a ocorrência para uma ocorrência de link personalizado, define o nome e o tipo do link e envia os dados.

### Uma mudança importante

À medida que você migra sua implementação do Adobe Analytics para a Web SDK, isso é importante:
A configuração do nome e do tipo do link, que é necessária para que a ocorrência seja uma ocorrência de link personalizado, NÃO está na ação &quot;Enviar equivalente a beacon&quot; (Enviar evento). Em vez disso, essa configuração do nome e do tipo do link estão na ação &quot;Definir equivalente a variáveis&quot; (Atualizar variável).
O resultado disso é que, independentemente de você ter o cenário 1 ou o cenário 2 acima, será necessário ter uma ação Atualizar variável e também uma ação Enviar evento.

Veja a seguir uma representação visual dessa diferença em implementações.

![Migrar regras de links personalizados](assets/migrate-custom-link-rule-2.jpg)

## Etapas de migração

Abra a regra de link personalizado da regra e identifique se ela se parece com o cenário 1 ou o cenário 2 exibido acima.
**Se sua regra assemelha-se ao cenário 1:**

1. Abra a ação Definir variáveis e anote todas as variáveis (props, eVars, eventos etc.) que estão sendo definidas nessa ação (por exemplo, na imagem acima, event10 está sendo definido).
1. Abra a ação Enviar beacon, verifique se ela está definida para enviar uma ocorrência s.tl(). Anote os valores de Tipo de link e Nome do link.
1. Na seção Ações da regra de link personalizado, clique no ícone de adição para adicionar outra regra.

   ![Adicionar uma nova ação](assets/add-new-action-3.jpg)

1. Configurar a ação
   1. Definir a **Extensão** para o Adobe Experience Platform Web SDK
   1. Defina o **Tipo de ação** para Atualizar variável
   1. Selecione o objeto **Analytics**
   1. Defina props, eVars e eventos da ação Definir variáveis do Analytics (neste exemplo, event10)

      ![Definir variáveis a serem migradas](assets/set-variables-to-migrate.jpg)

   1. Na mesma regra, role para baixo até o campo suspenso **Propriedade adicional** e adicione o campo **Nome do link**, definindo-o com o valor extraído da regra Enviar sinal. Na imagem abaixo, o exemplo é definir o nome como o valor da string &quot;clique de menu&quot;.
   1. Adicione também o campo **Tipo de link** do mesmo menu suspenso, adicionando &quot;o&quot; como o valor (considerando que o tipo de link na ação Enviar beacon era &quot;Link personalizado&quot;). Isso enviará o tipo de link &quot;outro&quot;, que equivale a um link personalizado. Se o tipo de link for um link de download, escolha &quot;d&quot; para o valor no campo deste novo tipo de link e, se o tipo de link for um link de saída, escolha &quot;e&quot; para o valor no campo deste novo tipo de link.

      ![Nome e tipo do link](assets/link-name-and-type.jpg)

1. Abaixo das Propriedades adicionais, você verá uma caixa de seleção rotulada **Limpar valor existente**. Se sua regra existente tiver uma **ação Adobe Analytics - Limpar variáveis** (como mostrado acima na etapa 3), basta marcar essa caixa e não será necessário adicionar uma ação de limpeza de variáveis para o Web SDK.

   ![limpar vars](assets/clear-existing-value.jpg)

1. Adicione outra ação clicando no ícone de adição.
1. Configurar a ação Enviar evento
   1. Definir a **Extensão** para o Adobe Experience Platform Web SDK
   1. Definir o **Tipo de ação** para o evento Enviado
   1. Clique no ícone do elemento de dados e escolha o elemento de dados **Variável de dados de exibição de página**

   ![Configurar o evento de envio](assets/configure-send-event.jpg)

1. **Manter alterações**, **Salvar na Biblioteca** e você pode **Criar** a biblioteca da mesma página, pois já definimos uma biblioteca de trabalho.

## Tirar uma importante conclusão sobre a migração

* Nesta lição, você aprendeu a migrar regras de links personalizados.
* No exercício [Migrar a regra de carregamento de página padrão](migrate-your-default-page-load-rule.md), você aprendeu a migrar regras que definem variáveis e também enviam um beacon do Analytics.
* Na lição [Migrar regras de página adicionais](migrate-additional-page-rules.md), você aprendeu a migrar suas regras que definem variáveis, mas não enviam um beacon para o Adobe Analytics.

Como você pode imaginar, os mesmos métodos podem ser usados em várias regras diferentes para migrar sua extensão do Analytics para o Web SDK.
Na maioria dos casos, você está simplesmente **atualizando as ações** nas regras. Você não está alterando o evento nem as condições em que ele é acionado. Você só está alterando o que está acontecendo na seção ações quando as regras são acionadas.
A maioria das regras se enquadra nessas categorias, se não todas. Se você tiver uma regra que não tenha, considere o mesmo paradigma de migração da ação e não o que acionou a regra.
