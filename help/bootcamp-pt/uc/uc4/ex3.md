---
title: Bootcamp - Customer Journey Analytics - Criar uma visualização de dados - Brasil
description: Customer Journey Analytics - Criar uma visualização de dados - Brasil
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Data Views
exl-id: 8cfd4467-167d-4235-a305-4596e3a7d4fb
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 2%

---

# 4.3 Crime uma Visualização de Dados

## Objetivos

- Entenda a UI de Visualização de Dados
- Compreenda como resolver de definição de visita
- Compreenda a interferência e a Persistência em uma visualização de

## 4.3.1 Visualização de dados

Agora, com sua conclusão, é possível progredir para corrigir a. Uma Parte entre o Adobe Analytics e o CJA é que o CJA A precisa de uma conduta de dados para analisar e atualizar os dados antes da garantia.

Uma Visualização de dados é essencial ao desenvolvimento de Suites no Adobe Analytics, no que você encontrar como migrar de volta com o contexto, filtragem e também os eventos são migrados.

Será necessário, no mínimo, uma Visualização de Dados por conexão. Não é possível, para alguns casos de uso, é possível ter Visualizações de dados para a conexão, com o objetivo de melhorar insights diferentes para. Se você quiser que sua empresa é responsável por dados, deve a forma como os dados são colocados em cada equipe. Alguns episódios:

- Métricas de UX apenas para uma equipe de UX Design
- Use os exemplos para KPIs e métricas para o Google Analytics e para o Customer Journey Analytics, para que a equipe de análise digital fale apenas 1 idioma.
- Visualização de dados filtrada para mostrar, por exemplo, dados para apenas um mercado, ou uma marca, ou apenas para Dispositivos móveis.

Na tela de **Conexões** marque a caixa de seleção da conexão que você acabou de criar. Clique em **Criar visualização de dados**.

![demonstração](./images/exta.png)

Você será redirecionado para o fluxo de trabalho **Criar visualização de dados** fluxo de trabalho.

![demonstração](./images/0-v2.png)

## 4.3.2 Definição de visualização de dados

Arquivado do original em 12 de julho de 2012 &quot;Agora você pode mudar como o movimento de transformação para sua visualização dados&quot; .

![demonstração](./images/0-v2.png)

Uma **Conexão** que você criou no exercício anterior já está selecionada. Sua conexão se chama `yourLastName – Omnichannel Data Connection`.

![demonstração](./images/ext5.png)

Em seguida, dê um nome à sua Visualização de Administração este modelo de nomenclatura: `yourLastName – Omnichannel Data View`.

Descrição do jogo: `yourLastName – Omnichannel Data View`.

| Nome | Descrição |
| ----------------- |-------------| 
| `yourLastName – Omnichannel Data View` | `yourLastName – Omnichannel Data View` |

![demonstração](./images/1-v2.png)

Para **Fuso Horário**, fuso horário **Berlim, Estocolmo, Roma, Berna, Bruxelas, Viena, GMT+01:00**. Este é um mundo realmente interessante, pois algumas empresas relacionadas em países e geografias. Alocar o fuso horário para o momento para país evitará os típicos de dados, como, por exemplo, µ a maioria das pessoas compradas camisetas às 4h no Peru.

![demonstração](./images/ext7.png)

Você também pode modificar a classificação das principais (Pessoa, Sessão e Evento). Isso não é obrigatório, mas alguns acompanhantes de usar Pessoas, Visitas e Acesso em vez de Pessoa, Sessão e Eventos (convenções de nomenclatura padrão do Customer Journey Analytics).

Agora você deve ter como modificar:

![demonstração](./images/1-v2.png)

Clique em **Salvar e Continuar**.

![demonstração](./images/12-v2.png)

## 4.3.3 Componentes da Visualização de Dados

Neste exercício, você irá modificar os requisitos para os dados e visualizá-los usando o Analysis Workspace. Nesta IU, há três áreas principais:

- Lado relacionado: Documentação dos conjuntos de dados obtidos
- Meio: Componentes próximos à Visualização de Dados
- Lado escolhas: Configurações do componente

![demonstração](./images/2-v2.png)

>[!IMPORTANT]
>
>Se você não consegue encontrar uma mudança ou mudança, a mudança se o campo foi mudado de sua migrada. `Contains data` Caso contrário, exclua esse campo.
>
>![demonstração](./images/2-v2a.png)

Agora você precisa arrastar e soltar os necessários para a análise nos **Componentes adicionados**. Isso, você deve os componentes no menu à esquerda e arrastá-los e solta-los na tela no meio.

Vamos começar com o primeiro componente: **Nome (web.webPageDetails.name)**. Pesquisa esse componente e garantia-o e solte o tela.

![demonstração](./images/3-v2.png)

Esse componente é o nome da página, como você pode derivar da leitura do campo do esquema `(web.webPageDetails.name)`.

Não, usar **Nome** como o nome não é a melhor combinação de notificação para um cliente ➡ essa dimensão.

Vamos mudar o nome para **Nome da página**. Clique em no componente o renomeie na área **Configurações de componente**.

![demonstração](./images/3-0-v2.png)

As Configurações de persistência são **configurações de persistência**. Os conceitos de eVars e prop não tem nenhum CJA, mas as configurações de Persistência possibilitam um comportamento compartilhado.

![demonstração](./images/3-0-v21.png)

Se você não quer as configurações, o CJA irá interpretar a transformação como um **Prop** (nível de manipulação). Além disso, podemos escolher uma Persistência para tornar a realidade a uma dimensão **eVar** (persistir o valor ao longo da jornada).

Se você não está familiarizado com eVars e Props, [leia mais sobre isso na verdade](https://experienceleague.adobe.com/docs/analytics/landing/an-key-concepts.html).

Vamos deixar o Nome da Página como Prop. Dessa forma, você não precisa realizar nenhuma **Configurações de persistência**.

| Component Name to Search | Novo nome | Configurações de persistência |
| ----------------- |-------------| --------------------| 
| Nome (web.webPageDetails.name) | Nome da página |          |

Em seguida, a opção a opção **phoneNumber** e solte-a na tela. O novo nome deve ser **Número de Telefone**.

![demonstração](./images/3-1-v2.png)

Por fim, vamos alterar as Configurações de persistência, pois o Número do Celular deve persistir no nível do usuário.

Para mudar a Persistência, role para baixo no menu à direita e abra a aba **Persistência**:

![demonstração](./images/5-v2.png)

Marque a caixa de seleção para modificar as configurações de persistência. **Mais recente** e o escopo **Pessoa (Janela de relatórios)**, pois nos preocupamos apenas com o último número de celular da pessoa. Se o cliente não deve o cliente em acompanhante, você ainda verá esse valor exibido.

![demonstração](./images/6-v2.png)

| Nome do componente a ser pesquisado | Novo nome | Configurações de persistência |
| ----------------- |-------------| --------------------| 
| phoneNumber | Número de telefone | Mais recente, Pessoa (janela de relatórios) |

O componente é `web.webPageDetails.pageViews.value`.

Nenhum menu à esquerda, pesquise `web.webPageDetails.pageViews.value`. Arraste e solte a essa na tela.

Alterar o nome para **Exibições de página** em **Configurações de componente**.

| Nome do componente a ser pesquisado | Novo nome | Configurações de atribuição |
| ----------------- |-------------| --------------------| 
| web.webPageDetails.pageViews.value | Page Views |         |

![demonstração](./images/7-v2.png)

Para como as regras de conduta, deixaremos em branco.

Observação: As configurações de persistência nas métricas também podem ser analisadas no Analysis Workspace. Em alguns casos, você pode filtrar por configurá-las aqui para evitar que os usuários de negócios que pensar é o melhor modelo de persistência.

Em seguida, você tem que mudar as dimensões dimensões e tricas, na tabela abaixo.

### DIMENSÕES

| Nome do componente a ser pesquisado | Novo nome | Configurações de persistência |
| ----------------- |-------------| --------------------| 
| brandName | Nome da marca | Mais recente, Sessão |
| callfeel | Sensação de chamada |          |
| ID de chamada | Tipo de Interação com Chamada |          |
| callTopic | Chamar tópico | Mais recente, Sessão |
| ecid | ECID | Mais recente, Pessoa (janela de relatórios) |
| email | ID de e-mail | Mais recente, Pessoa (janela de relatórios) |
| Tipo de pagamento | Tipo de pagamento |          |
| Método de adição de produto | Método de adição de produto | Mais recente, Sessão |
| Tipo de evento | Tipo de evento |         |
| Name (productListItems.name) | Nome do produto |         |
| SKU | SKU (Sessão) | Mais recente, Sessão |
| ID da transação | ID da transação |         |
| URL (web.webPageDetails.URL) | URL |         |
| Agente do usuário | Agente do usuário | Mais recente, Sessão |

### MÉTRICA

| Nome do componente a ser pesquisado | Novo nome | Configurações de atribuição |
| ----------------- |-------------| --------------------| 
| Quantidade | Quantidade |          |
| commerce.order.priceTotal | Receita |         |

Sua configuração deve ser feita a seguir:

![demonstração](./images/11-v2.png)

Não se Salvar de Salvar sua Visualização de Dados Então clique em **Salvar**.

![demonstração](./images/12-v2s.png)

## 4.3.4 Métricas calculadas

consultado em 28 de novembro de 2012 &quot;µ todos os componentes na Visualização de dados, ainda há dois anos atrás para que os usuários dos testes para analisar seus dados&quot; .

Se você tiver encontrado, não demonstrações disponibilizadas Métricas como Adicionar ao Carinho, Visualização do produto ou Compras para a Visualização de dados. Não há nenhum processo, é preciso uma dimensão musical: **Tipo de evento**. Então, vamos derivar esses eventos de manipulação 3 métricas calculadas.

Vamos começar com a primeira Métrica: **Visualizações do produto**.

Sem lado esquerdo, pesquise **Tipo de evento** e ➡ a dimensão. Em combinação, componente-o-solte na tela **Incluído**.

![demonstração](./images/calcmetr1.png)

Clique para consolidar uma nova ➡ **Tipo de evento**.

![demonstração](./images/calcmetr2.png)

Agora altere o nome e a descrição do componente para os domínios valores:

| Nome do componente | Descrição do componente |
| ----------------- |-------------| 
| Visualizações de produto | Visualizações de produto |

![demonstração](./images/calcmetr3.png)

Agora vamos contar apenas eventos de **Exibições do produto**. Para fazer isso, role para baixo em **Configurações de componente** até ver Valores de **Incluir valores de exclusão**. µ-se de habilitar a opção **Definir valores de inclusão/exclusão**.

![demonstração](./images/calcmetr4.png)

Como visualizações somente **Exibições do produto**, **commerce.productViews** nos.

![demonstração](./images/calcmetr5.png)

Agora a sua mudança está pronta!

Em seguida, repita o mesmo processador para os eventos **Adicionar ao carrinho** e **Comprar**.

### Adicionar ao carrinho

Primeiro, participantes e solte a ➡ **Tipo de evento**.

![demonstração](./images/calcmetr1.png)

Você verá um alerta pop-up de um Campo Duplicado, pois usando um equipamento de processamento. Clique em **Adicionar mesmo assim**:

![demonstração](./images/calcmetr6.png)

Agora, siga o mesmo processo que muda para a visualização da produção:
- Primeiro altere o nome e a descrição.
- Por fim, **commerce.productListAdds** como exibido para contar apenas Adicionar ao carrinho

| Nome | Descrição | Critérios |
| ----------------- |-------------| -------------|
| Adicionar ao carrinho | Adicionar ao carrinho | commerce.productListAdds |

![demonstração](./images/calcmetr6a.png)

### Compras

Primeiro, competie e solte a ➡ **Tipo de evento** como exibido para as duas métricas anteriores.

![demonstração](./images/calcmetr1.png)

Você verá um alerta pop-up de um Campo Duplicado, pois usando um equipamento de processamento. Clique em **Adicionar mesmo assim**:

![demonstração](./images/calcmetr7.png)

Agora, siga o mesmo processo que fizemos para as métricas Product Views e Add to cart:
- Primeiro altere o nome e a descrição.
- Por fim, **compras** como compras para contas apenas como Compras

| Nome | Descrição | Critérios |
| ----------------- |-------------| -------------|
| Compras | Compras | commerce.purchases |

![demonstração](./images/calcmetr7a.png)

Sua configuração final deve ser seguido. Clique em **Salvar e continuar**.

![demonstração](./images/calcmetr8.png)

## 4.3.5 Componente da análise de dados

Você deve ser redirecionado para esta tela:

![demonstração](./images/8-v2.png)

Nesta aba, você pode modificar como as alterações para a forma processados. Vamos começar definindo o **Tempo limite da sessão** como 30 min. Graças ao registro de dados e hora de cada evento de experiência, você pode estender o desenvolvimento de uma sessão em todos os canais. Por exemplo, o que acontece se um cliente para o call center Depois de visitar o site? Tempos Limite de Sessão expandida, você tem capacidade para movimentar o que é uma sessão e como essa sessão mesclar os dados.

![demonstração](./images/ext8.png)

Nesta aba você pode as coisas como filtrar os dados usando um segmento/filtro. Você não é capaz de fazer isso neste exercício.

![demonstração](./images/10-v2.png)

Quando, clique em **Salvar e finalizar**.

![demonstração](./images/13-v2.png)

>[!NOTE]
>
>Você pode vir a esta Visualização de dados e mudar como configurações e os componentes a qualquer momento. As PERGUNTAS SÃO MOSTRADAS.

Agora você pode continuar com a parte de mudança e análise!

Próxima etapa: [4.4 Preparação de dados em Customer Journey Analytics](./ex4.md)

[Retorno para Fluxo de monitoramento 4](./uc4.md)

[Retorno para Todos os compartilhados](./../../overview.md)
