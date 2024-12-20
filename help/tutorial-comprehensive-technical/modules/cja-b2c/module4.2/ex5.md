---
title: Assimilar e analisar dados do Google Analytics no Adobe Experience Platform com o Conector de Source do BigQuery - Analisar dados do Google Analytics usando o Customer Journey Analytics
description: Assimilar e analisar dados do Google Analytics no Adobe Experience Platform com o Conector de Source do BigQuery - Analisar dados do Google Analytics usando o Customer Journey Analytics
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '3338'
ht-degree: 2%

---

# 4.2.5 Analisar dados do Google Analytics usando o Customer Journey Analytics

## Objetivos

- Conecte nosso conjunto de dados do BigQuery ao Customer Journey Analytics (CJA)
- Conecte-se e associe-se a Google Analytics com dados de fidelidade.
- Familiarizar-se com a interface do CJA

## 4.2.5.1 Criar uma conexão

Acesse [analytics.adobe.com](https://analytics.adobe.com) para acessar o Customer Journey Analytics.

![demonstração](./images/1a.png)

Na página inicial do Customer Journey Analytics, vá para **Conexões**.

![demonstração](./images/conn1.png)

Aqui você pode ver todas as diferentes conexões feitas entre o CJA e a Platform. Essas conexões têm o mesmo objetivo que os conjuntos de relatórios no Adobe Analytics. Mas a coleta de dados é totalmente diferente. Todos os dados vêm dos conjuntos de dados da Adobe Experience Platform.

![demonstração](./images/2.png)

Clique em **Criar nova conexão**.

![demonstração](./images/conn3.png)

Você verá a interface do usuário **Criar conexão**.

![demonstração](./images/5.png)

Primeiro, é necessário selecionar a sandbox correta para usar. No menu da sandbox, selecione sua sandbox, que deve ser `--aepSandboxName--`. Neste exemplo, a sandbox a ser usada é **AEP Enablement FY21**.

![demonstração](./images/cjasb.png)

Após selecionar sua sandbox, os conjuntos de dados disponíveis serão atualizados.

![demonstração](./images/cjasb1.png)

No menu esquerdo, é possível ver todos os conjuntos de dados do Adobe Experience Platform disponíveis. Pesquisar o conjunto de dados `Demo System - Event Dataset for BigQuery (Global v1.1)`. Clique em **+** para adicionar o conjunto de dados a esta conexão.

![demonstração](./images/6.png)

Depois de adicioná-lo, você verá o conjunto de dados dentro da conexão.

Agora é necessário selecionar a **ID de pessoa**. Certifique-se de que o **fidelidId** esteja selecionado como ID de pessoa.

![demonstração](./images/8.png)

Agora você enriquecerá os dados de Interação do site do Google Analytics com outro conjunto de dados do Adobe Experience Platform.

Procure o conjunto de dados `Demo System - Profile Dataset for Loyalty (Global v1.1)` e adicione-o a essa conexão.

![demonstração](./images/10.png)

Você verá isto:

![demonstração](./images/10a.png)

Para mesclar ambos os conjuntos de dados, é necessário selecionar uma **ID de pessoa** que contenha o mesmo tipo de IDs. O conjunto de dados `Demo System - Profile Dataset for Loyalty (Global v1.1)` usa o **fidelidId** como ID de pessoa, que contém o mesmo tipo de IDs que o `Demo System - Event Dataset for BigQuery (Global v1.1)`, que também usa o **fidelisidId** como uma ID de pessoa.

![demonstração](./images/12.png)

Clique em **Next**.

![demonstração](./images/14.png)

Você verá isto:

![demonstração](./images/15.png)

Aqui você precisa dar um nome à sua conexão.

Use esta convenção de nomenclatura: `ldap - GA + Loyalty Data Connection`.

Exemplo: `vangeluw - GA + Loyalty Data Connection`

Antes de concluir, ative o **Importar automaticamente todos os novos dados de todos os conjuntos de dados nesta conexão, a partir de hoje.** como na imagem abaixo.

![demonstração](./images/16.png)

Isso iniciará um fluxo de dados do Adobe Experience Platform para o CJA a cada 60 minutos. No entanto, com grandes volumes de dados, pode levar até 24 horas.

Você também precisa preencher dados históricos. Marque a caixa de seleção **Importar todos os dados existentes** e selecione **menos de 1 milhão** em **Número médio de eventos diários**.

![demonstração](./images/17.png)

Após criar sua **Conexão**, pode levar algumas horas até que seus dados estejam disponíveis no CJA.

Clique em **Salvar** e vá para o próximo exercício.

![demonstração](./images/cjasave.png)

Em seguida, você verá sua conexão na lista de conexões disponíveis.

![demonstração](./images/18.png)

## 4.2.5.2 Criar uma visualização de dados

Com a conexão concluída, agora é possível avançar para a visualização de influência. Uma diferença entre o Adobe Analytics e o CJA é que o CJA precisa de uma visualização de dados para limpar e preparar os dados antes da visualização.

Uma visualização de dados é semelhante ao conceito de conjuntos de relatórios virtuais no Adobe Analytics, onde você define definições de visita com reconhecimento de contexto, filtragem e também como os componentes são chamados.

Você precisará de, no mínimo, uma visualização de dados por conexão. No entanto, para alguns casos de uso, é ótimo ter várias visualizações de dados para a mesma conexão, com o objetivo de fornecer diferentes insights para equipes diferentes.

Se quiser que sua empresa se torne orientada por dados, você deve adaptar como os dados são visualizados em cada equipe. Alguns exemplos:

- Métricas de UX somente para a equipe de design de UX
- Use os mesmos nomes para KPIs e Métricas para Google Analytics e para Customer Journey Analytics, de modo que a equipe de análise digital possa falar apenas 1 idioma.
- visualização de dados filtrada para mostrar, por exemplo, dados de apenas um mercado ou uma marca ou apenas para Dispositivos móveis.

Na tela **Conexões**, marque a caixa de seleção na frente da conexão que você acabou de criar.

![demonstração](./images/exta.png)

Agora clique em **Criar visualização de dados**.

![demonstração](./images/extb.png)

Você será redirecionado para o fluxo de trabalho **Criar Exibição de Dados**.

![demonstração](./images/extc.png)

Agora você pode configurar as definições básicas para a visualização de dados. Coisas como Fuso horário, Tempo limite da sessão ou a filtragem de visualização de dados (a parte de segmentação é semelhante aos Conjuntos de relatórios virtuais no Adobe Analytics).

A **Conexão** criada no exercício anterior já está selecionada. Sua conexão é nomeada `ldap - GA + Loyalty Data Connection`.

![demonstração](./images/ext5.png)

Em seguida, dê um nome à sua visualização de dados seguindo esta convenção de nomenclatura: `ldap - GA + Loyalty Data View`.

Insira o mesmo valor para a descrição: `ldap - GA + Loyalty Data View`.

Antes de fazer qualquer análise ou visualização, precisamos criar uma visualização de dados com todos os campos, dimensões e métricas e suas configurações de atribuição.

| Campo | Convenção de nomeação | Exemplo |
| ----------------- |-------------|-------------|  
| Nomear conexão | ldap - GA + Visualização de dados de fidelidade | vangeluw - GA + Visualização de dados de fidelidade |
| Descrição | ldap - GA + Visualização de dados de fidelidade | vangeluw - GA + Visualização de dados de fidelidade |

![demonstração](./images/22.png)

Clique em **Salvar e continuar**.

![demonstração](./images/23.png)

Agora é possível adicionar componentes à visualização de dados. Como você pode ver, algumas métricas e dimensões são adicionadas automaticamente.

![demonstração](./images/24.png)

Adicione os seguintes componentes à visualização de dados:

| Nome do componente | Tipo de componente | Caminho do componente |
| -----------------|-----------------|-----------------|
| nível | Dimensão | _experienceplatform.altyDetails.level |
| pontos | Métrica | _experienceplatform.fidelisationDetails.points |
| commerce.checkouts.value | Métrica | commerce.checkouts.value |
| commerce.productListRemovals.value | Métrica | commerce.productListRemovals.value |
| commerce.productListAdds | Métrica | commerce.productListAdds |
| commerce.productViews.value | Métrica | commerce.productViews.value |
| commerce.purchases.value | Métrica | commerce.purchases.value |
| web.webPageDetails.pageViews | Métrica | web.webPageDetails.pageViews |
| ID da transação | Dimensão | commerce.order.payments.transactionID |
| channel.mediaType | Dimensão | channel.mediaType |
| channel.typeAtSource | Dimensão | channel.typeAtSource |
| Código de rastreamento | Dimensão | marketing.trackingCode |
| gaid | Dimensão | _experienceplatform.identification.core.gaid |
| web.webPageDetails.name | Dimensão | web.webPageDetails.name |
| Tipo de evento | Dimensão | eventType |
| Fornecedor | Dimensão | environment.browserDetails.vendor |
| Identificador | Dimensão | _id |
| Carimbo de data e hora | Dimensão | carimbo de data e hora |
| Tipo | Dimensão | device.type |
| fidelisd | Dimensão | _experienceplatform.identification.core.fidelizaçãoId |

Você terá isto:

![demonstração](./images/25.png)

Em seguida, é necessário alterar o nome amigável de algumas das métricas e dimensões acima para que você possa usá-las facilmente ao criar a análise. Para fazer isso, selecione a métrica ou a dimensão e atualize o campo **Nome** conforme indicado na imagem abaixo.

![demonstração](./images/25a.png)

| Nome original do componente | Nome de exibição |
| -----------------|-----------------|
| nível | Nível de fidelidade |
| pontos | Pontos de fidelidade |
| commerce.checkouts.value | Check-outs |
| commerce.productListRemovals.value | Remoções do carrinho |
| commerce.productListAdds | Adições ao carrinho |
| commerce.productViews.value | Visualizações de produto |
| commerce.purchases.value | Compras |
| web.webPageDetails.pageViews | Page Views |
| channel.mediaType | Tráfego Medium |
| channel.typeAtSource | Traffic Source |
| Código de rastreamento | Canal de marketing |
| gaid | ID do Google Analytics |
| Nome | Título da página |
| Fornecedor | Navegador |
| Tipo | Device Type |
| fidelisd | ID de fidelidade |

Você terá algo assim:

![demonstração](./images/25b.png)

Em seguida, você precisa fazer algumas alterações no contexto de Pessoa e Sessão para alguns desses componentes alterando as **Configurações de Atribuição**.

![demonstração](./images/25c.png)

Altere as **Configurações de atribuição** dos componentes abaixo:

| Componente |
| -----------------|
| Traffic Source |
| Canal de marketing |
| Navegador |
| Tráfego Medium |
| Device Type |
| ID do Google Analytics |
| ID de fidelidade |
| Nível de fidelidade |
| Pontos de fidelidade |

Para fazer isso, selecione o componente, clique em **Usar modelo de atribuição personalizado** e defina o **Modelo** como **Último contato** e a **Expiração** como **Pessoa (Janela de relatórios)**. Repita isso para todos os componentes mencionados acima.

![demonstração](./images/27a.png)

Depois de fazer as alterações nas configurações de atribuição para todos os componentes mencionados acima, você deve ter esta visualização:

![demonstração](./images/27.png)

A visualização de dados agora está configurada. Clique em **Salvar**.

![demonstração](./images/30.png)

Agora você está pronto para analisar dados do Google Analytics no Adobe Analytics Analysis Workspace. Vamos passar para o próximo exercício.

## 4.2.5.3 Criar o projeto

No Customer Journey Analytics, vá para **Projetos**.

![demonstração](./images/pro1.png)

Você verá isto:

![demonstração](./images/pro2.png)

Crie um Projeto clicando em **Criar Novo Projeto**.

![demonstração](./images/pro3.png)

Agora você tem um Projeto em branco:

![demonstração](./images/pro4.png)

Primeiro, salve o projeto e dê um nome a ele. Você pode usar o seguinte comando para salvar:

| Sistema operacional | Atalho |
| ----------------- |-------------| 
| Windows | Ctrl+S |
| Mac | Command+S |

Você verá este pop-up:

![demonstração](./images/prsave.png)

Use esta convenção de nomenclatura:

| Nome | Descrição |
| ----------------- |-------------| 
| ldap - GA + Loyalty Workspace | ldap - GA + Loyalty Workspace |

Em seguida, clique em **Salvar projeto**.

![demonstração](./images/prsave2.png)

Em seguida, selecione a visualização de dados correta no canto superior direito da tela. Esta é a visualização de dados criada no exercício anterior, com a convenção de nomenclatura `ldap - GA + Loyalty Data View`. Neste exemplo, a Visualização de Dados a ser selecionada é `ldap - GA + Loyalty Data View`.

![demonstração](./images/prdvlist.png)

![demonstração](./images/prdv.png)

### 12.5.3.1 Tabelas de forma livre

As tabelas de forma livre funcionam, mais ou menos, como tabelas dinâmicas no Excel. Você escolhe algo na barra esquerda, arrasta e solta na Forma livre e obtém um relatório de tabela.

As tabelas de forma livre são quase ilimitadas. Você pode fazer (quase) qualquer coisa e isso traz tanto valor quando comparado a Google Analytics (já que essa ferramenta tem algumas limitações de análise). Esse é um dos motivos para carregar dados do Google Analytics em outra ferramenta de análise.

Veja dois exemplos em que você precisa usar o SQL, o BigQuery e algum tempo para responder a perguntas simples que não são possíveis de fazer na interface do Google Analytics ou no Google Data Studio:

- Quantas pessoas chegam ao checkout do Navegador Safari dividido por canal de marketing? Verifique se a métrica de check-out está sendo filtrada pelo Navegador Safari. Acabamos de arrastar e soltar a variável Navegador = Safari na parte superior da coluna de check-out.

- Como analista, posso ver que o Canal de marketing social tem baixas conversões. Estou usando a atribuição Último contato como padrão, mas e quanto ao Primeiro contato? Ao passar o mouse sobre qualquer métrica, as configurações da métrica são exibidas. Posso selecionar o modelo de atribuição que desejo. Você pode fazer a Atribuição no GA (não no Data Studio) como uma atividade independente, mas não pode ter outras métricas ou dimensões não relacionadas à análise de atribuição na mesma tabela.

Vamos responder a essas perguntas e a outras mais com o Analysis Workspace no CJA.

Primeiro, selecione o intervalo de datas correto (**Últimas 53 semanas completas**) no lado direito do painel.

![demonstração](./images/pro11.png)

Em seguida, clique em **Aplicar** para aplicar o intervalo de datas. Lembre-se desta etapa para os próximos exercícios.

![demonstração](./images/apply.png)

>[!NOTE]
>
>Se você acabou de criar a **Conexão de dados** e a **Visualização de dados**, talvez precise aguardar algumas horas. O CJA precisa de algum tempo para preencher retroativamente dados históricos quando há uma enorme quantidade de registros de dados.

Vamos arrastar e soltar algumas dimensões e métricas para analisar os canais de marketing. Primeiro use a dimensão **Canal de marketing** e arraste e solte-a na tela da **Tabela de forma livre**. (Clique em **Mostrar tudo** caso não veja a métrica imediatamente no menu Métricas)

![demonstração](./images/pro14.png)

Você verá isto:

![demonstração](./images/pro14a.png)

Em seguida, é necessário adicionar as Métricas à Tabela de forma livre. Você deve adicionar estas Métricas: **Pessoas**, **Sessões**, **Exibições de Produtos**, **Check-outs**, **Compras**, **Taxa de Conversão** (Métrica Calculada).

Antes de fazer isso, é necessário criar a Métrica calculada **Taxa de conversão**. Para fazer isso, clique no ícone **+** ao lado de Métricas:

![demonstração](./images/procalc1.png)

Como nome da Métrica Calculada, use **Taxa de Conversão**. Em seguida, arraste as Métricas **compra** e **Sessões** para a tela. Definir **Formato** a **Percentual** e **Casas Decimais** a **2**. Finalmente, clique em **Salvar**.

![demonstração](./images/procalc2.png)

Em seguida, para usar todas essas Métricas na **Tabela de forma livre**, arraste e solte-as uma por uma na **Tabela de forma livre**. Veja o exemplo abaixo.

![demonstração](./images/pro16.png)

Você terminará com uma tabela como esta:

![demonstração](./images/pro16a.png)

Como mencionado acima, as **Tabelas de forma livre** oferecem a liberdade necessária para executar uma análise detalhada. Por exemplo, você pode escolher qualquer outro Dimension para analisar uma métrica específica dentro da tabela.

Como exemplo, vá para dimensões e pesquisa e selecione a variável **Navegador**.

![demonstração](./images/new1.png)

Você verá uma visão geral dos valores disponíveis para esse Dimension.

![demonstração](./images/new2.png)

Escolha o Dimension **Safari** e arraste-o e solte-o sobre uma Métrica, por exemplo **Check-outs**. Você verá isto:

![demonstração](./images/new3.png)

Ao fazer isso, você acabou de responder a uma possível pergunta que tinha: Quantas pessoas chegam à página de check-out usando o Safari, divididas pelo Canal de marketing?

Agora vamos responder à pergunta sobre Atribuição.

Localize a métrica **Compra** na tabela.

![demonstração](./images/pro20.png)

Passe o mouse sobre a métrica e um ícone de **Configurações** será exibido. Clique nele.

![demonstração](./images/pro21.png)

Um menu contextual será exibido. Marque a caixa de seleção para **modelo de atribuição não padrão**.

![demonstração](./images/pro22.png)

No pop-up que você verá, é possível alterar facilmente os modelos de atribuição e a janela de pesquisa (o que é bastante complexo de se obter com o SQL).

![demonstração](./images/pro23.png)

Selecione **Primeiro contato** como seu modelo de atribuição.

![demonstração](./images/pro24.png)

Escolha **Pessoa** para a Janela de Pesquisa.

![demonstração](./images/pro25.png)

Agora clique em **Aplicar**.

![demonstração](./images/pro26.png)

Agora é possível ver que o modelo de atribuição para essa métrica específica agora é Primeiro contato.

![demonstração](./images/pro27.png)

Você pode fazer o detalhamento que quiser, sem limites de tipos de variável, segmentos, dimensão ou intervalos de datas.

Algo ainda mais especial é a capacidade de unir qualquer conjunto de dados do Adobe Experience Platform para enriquecer os dados de comportamento digital do Google Analytics. Por exemplo, offline, call center, fidelidade ou dados de CRM.

Para mostrar essa funcionalidade, vamos configurar seu primeiro detalhamento que combina dados offline com dados online. Escolha o **Nível de Fidelidade** da dimensão e arraste-o e solte-o em qualquer **Canal de Marketing**, por exemplo, **Pesquisa Orgânica**:

![demonstração](./images/pro28.png)

Em seguida, vamos analisar qual **Tipo de Dispositivo** é usado pelos clientes que vieram ao site usando a **Pesquisa Orgânica** com um **Nível de Fidelidade** que é **Bronze**. Pegue o Dimension **Tipo de dispositivo** e arraste e solte-o no **Bronze**. Você verá isto:

![demonstração](./images/pro29.png)

Você pode ver que, para o primeiro detalhamento, é usado o Nível de fidelidade. Essa dimensão vem de um conjunto de dados e de um esquema diferentes do que você usou para o conector do BigQuery. A ID de pessoa **fidelidID** (Sistema de demonstração - Esquema de evento para BigQuery (Global v1.1)) e **fidelidID** (Sistema de demonstração - Esquema de perfil para fidelização (Global v1.1)) correspondem entre si. Portanto, você pode combinar eventos de experiência de Google Analytics com dados de perfil do esquema de fidelidade.

Podemos continuar dividindo as linhas com segmentos ou intervalos de datas específicos (talvez para refletir campanhas de TV específicas) para fazer perguntas ao Customer Journey Analytics e obter as respostas em movimento.

Alcançar o mesmo resultado final com SQL e, em seguida, uma ferramenta de visualização de terceiros é um grande desafio. Especialmente quando você faz perguntas e tenta obter as respostas em tempo real. O Customer Journey Analytics não tem esse desafio e permite que os analistas de dados consultem os dados de forma flexível e em tempo real.

## 4.2.5.3.2 Análise de funil ou fallout

Os funis são um ótimo mecanismo para entender as principais etapas em uma jornada do cliente. Essas etapas também podem vir de interações offline (por exemplo, da central de atendimento) e, em seguida, você pode combiná-las com pontos de contato digitais no mesmo funil.

O Customer Journey Analytics permite fazer isso e muito mais. Se você se lembrar do Módulo 13, nós conseguimos clicar com o botão direito do mouse e fazer coisas como:

- Analisar para onde os usuários estão indo após uma etapa de fallout
- Criar um segmento a partir de qualquer ponto do funil
- Ver a tendência em qualquer estágio em uma visualização de Gráfico de linha


Vamos ver outra coisa que você pode fazer: como está o funil de Jornada para clientes este mês em relação ao mês anterior? E quanto a mobilidade vs desktop?

Abaixo, você criará dois painéis:

- Análise de funil (janeiro)
- Análise de funil (fevereiro)

Você verá que estamos comparando um funil em diferentes períodos de tempo (janeiro e fevereiro) divididos por Tipo de dispositivo.

Esse tipo de análise não é possível na interface do usuário do Google Analytics ou é muito limitado. Assim, o CJA novamente adiciona muito valor aos dados capturados pelo Google Analytics.

Para criar sua primeira visualização de fallout. Feche o painel atual para começar com um novo.

Observe o lado direito do painel e clique na seta para fechá-lo.

![demonstração](./images/pro33.png)

Em seguida, clique em **+** para criar um novo painel.

![demonstração](./images/pro35.png)

Agora selecione a Visualização **Fallout**.

![demonstração](./images/pro36.png)

Como um analista, imagine que deseja entender o que está acontecendo com seu funil principal de comércio eletrônico: Página inicial > Pesquisa interna > Detalhes do produto > Check-out > Compra.

Vamos começar adicionando algumas novas etapas ao funil. Para fazer isso, abra a dimensão **Nome da página**.

![demonstração](./images/pro37.png)

Em seguida, você verá todas as páginas disponíveis que foram visitadas.

![demonstração](./images/pro38.png)

Arraste e solte a **Página inicial** na primeira etapa.

![demonstração](./images/pro39.png)

Como segunda etapa, use os **Armazenar resultados de pesquisa**

![demonstração](./images/pro40.png)

Agora é necessário adicionar algumas ações de comércio eletrônico. Nos Dimension, pesquise a dimensão Dimension **Tipo de evento**. Clique em para abrir a dimensão.

![demonstração](./images/pro41.png)

Selecione **Product_Detail_Views** e arraste-o e solte-o na próxima etapa.

![demonstração](./images/pro43.png)

Selecione **Product_Checkouts** e arraste-o e solte-o na próxima etapa.

![demonstração](./images/pro44.png)

Redimensionar a visualização de Fallout.

![demonstração](./images/pro45.png)

A visualização de fallout agora está pronta.

Para começar a analisar e documentar os insights, é sempre uma boa ideia usar uma visualização de **Texto**. Para adicionar uma visualização de **Texto**, clique no ícone **Gráfico** no menu esquerdo para ver todas as visualizações disponíveis. Em seguida, arraste e solte a visualização **Texto** na tela. Redimensione e mova-a para que fique parecida com a imagem abaixo.

![demonstração](./images/pro48.png)

E, novamente, redimensione-o para caber no painel:

![demonstração](./images/pro49.png)

As visualizações de Fallouts também permitem detalhamentos. Use a dimensão **Tipo de dispositivo** abrindo-a e arraste e solte alguns dos valores em por um na visualização:

![demonstração](./images/pro50.png)

Você terá uma visualização mais avançada:

![demonstração](./images/pro51.png)

O Customer Journey Analytics permite fazer isso e muito mais. Ao clicar com o botão direito do mouse em qualquer lugar do fallout, você pode...

- Analisar para onde os usuários vão em uma etapa de fallout
- Criar um segmento a partir de qualquer ponto do funil
- Colocar em tendência qualquer etapa em uma visualização de Linha
- Compare qualquer funil a diferentes períodos de tempo visualmente.

Como exemplo, clique com o botão direito do mouse em qualquer etapa do fallout para ver algumas dessas opções de análise.

![demonstração](./images/pro52.png)

## 4.2.5.3.3 Análise e visualização de fluxo

Se você quiser fazer análise de fluxo avançada usando o Google Analytics, será necessário usar SQL para extrair os dados e usar uma solução de terceiros para a parte de visualização. O Customer Journey Analytics vai ajudar nisso.

Nesta etapa, você configurará uma análise de fluxo para responder esta pergunta: Quais são os principais canais de contribuição antes de uma Landing Page específica.  Com dois arrastar e soltar e um clique, como analista, você pode descobrir o fluxo do usuário em direção à Landing page com os dois últimos toques de canais de marketing.

Outras perguntas que o Customer Journey Analytics pode ajudar a responder:

- Qual é a principal combinação de canais antes de uma landing page específica?
- O que faz com que um usuário saia da sessão quando chega ao Product_Checkout? Quais são as etapas anteriores?

Vamos começar com um painel em branco novamente para responder a essas perguntas. Feche o painel atual e clique em **+**.

![demonstração](./images/pro53.png)

Agora selecione a visualização **Fluxo**.

![demonstração](./images/pro54.png)

Agora vamos configurar uma Análise de fluxo de canal de marketing de vários caminhos. Arraste e solte a dimensão **Canal de marketing** na área **Dimension** de entrada.

![demonstração](./images/pro55.png)

Agora você pode ver os primeiros caminhos de entrada:

![demonstração](./images/pro56.png)

Clique no primeiro caminho para detalhá-lo.

![demonstração](./images/pro58.png)

Agora você pode ver o próximo caminho (Canal de marketing).

![demonstração](./images/pro59.png)

Vamos fazer um terceiro detalhamento. Clique na primeira opção dentro do novo caminho, **Referência**.

![demonstração](./images/pro60.png)

Agora você deve ver a visualização assim:

![demonstração](./images/pro61.png)

Vamos complicar as coisas. Imagine que você queira analisar o que era a landing page após dois caminhos de marketing? Para fazer isso, é possível usar uma dimensão secundária para alterar o último caminho. Localize a dimensão **Nome da Página** e arraste-a e solte-a assim:

![demonstração](./images/pro62n.png)

Agora você verá isto:

![demonstração](./images/pro63n.png)

Vamos fazer outra análise de fluxo. Desta vez, você analisará o que aconteceu após um ponto de saída específico. Outras soluções do Analytics exigem o uso do SQL/ETL e, novamente, uma ferramenta de visualização de terceiros para alcançar a mesma coisa.

Traga uma nova **Visualização de Fluxo** para o painel.

![demonstração](./images/pro64.png)

Você terá isto:

![demonstração](./images/pro64a.png)

Localize o Dimension **Tipo de Evento** e arraste-o e solte-o na área **Dimensão de saída**.

![demonstração](./images/pro65.png)

Agora você pode ver quais caminhos de **Tipo de evento** levaram os clientes para a saída.

![demonstração](./images/pro66.png)

Vamos investigar o que aconteceu antes da saída da ação de check-out. Clique no caminho **Product_Checkouts**:

![demonstração](./images/pro67.png)

Um novo caminho de ação será exibido com alguns dados que não são reveladores.

![demonstração](./images/pro68.png)

Vamos analisar mais detalhadamente! Pesquise o Dimension **Nome da página** e arraste-o e solte-o no novo caminho gerado.

![demonstração](./images/pro69.png)

Agora você tem uma análise avançada de fluxo feita em minutos. Você pode clicar nos diferentes caminhos para ver como eles se conectam da saída para as etapas anteriores.

![demonstração](./images/pro70.png)

Agora você tem um kit eficiente para analisar funis e explorar caminhos do comportamento do cliente em pontos de contato digitais, mas também offline.

Não se esqueça de salvar suas alterações!

## 4.2.5.4 Compartilhamento do projeto

>[!IMPORTANT]
>
>O conteúdo abaixo é destinado a informação pessoal - Você **NÃO** precisa compartilhar seu projeto com outra pessoa.

INFO - Você pode compartilhar este projeto com colegas para colaborar ou analisar perguntas comerciais juntos.

![demonstração](./images/pro99.png)

![demonstração](./images/pro100.png)

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao módulo 4.2](./customer-journey-analytics-bigquery-gcp.md)

[Voltar a todos os módulos](./../../../overview.md)
