---
title: Configurar o Gerenciamento de decisões da Journey Optimizer com o SDK da Web da plataforma
description: Saiba como implementar a Gestão de decisões usando o SDK da Web da plataforma. Esta lição é parte do tutorial Implementar a Adobe Experience Cloud com o SDK da web.
solution: Data Collection,Experience Platform,Journey Optimizer
feature-set: Journey Optimizer
feature: Decision Management,Offers
jira: KT-15412
exl-id: f7852ef4-44b0-49df-aec8-cb211726247d
source-git-commit: 901b90ca165a74bbc4f871469222064b70d0a20a
workflow-type: tm+mt
source-wordcount: '2513'
ht-degree: 1%

---

# Configurar o Gerenciamento de decisões com o SDK da Web da plataforma

Saiba como implementar o recurso de Gestão de decisões da Adobe Journey Optimizer usando o SDK da Web da plataforma. Este guia aborda os pré-requisitos básicos da Gestão de decisões, as etapas detalhadas de configuração e um aprofundamento em um caso de uso centrado no status de fidelidade.

Ao seguir este tutorial, os usuários do Journey Optimizer estão equipados para usar os recursos de Gestão de decisões, aprimorando a personalização e a relevância das interações com os clientes.


![SDK da Web e diagrama do Adobe Analytics](assets/dc-websdk-ajo.png)

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Entenda os conceitos principais da Gestão de decisões na Adobe Journey Optimizer e sua integração com o SDK da Web da Adobe Experience Platform.

* Saiba mais sobre o processo passo a passo de configuração do SDK da Web para o Offer Decisioning, garantindo uma integração perfeita com o Journey Optimizer.

* Explore um caso de uso detalhado centrado em ofertas de status de fidelidade, obtendo insights sobre como criar e gerenciar ofertas, decisões e disposições de maneira eficaz.

* Conheça os termos essenciais e suas implicações na estrutura da Gestão de decisões.

* Entenda o significado das regras de decisão, dos qualificadores de coleção e das ofertas substitutas no delivery da oferta certa ao usuário certo.

* Analise tópicos avançados, como simulações e coleta de dados de eventos personalizados, permitindo testar, validar e aprimorar seus mecanismos de delivery de ofertas.

## Pré-requisitos

Para concluir as lições desta seção, primeiro você deve:

* Certifique-se de que sua organização tenha acesso ao Adobe Journey Optimizer Ultimate (Journey Optimizer e Offer Decisioning) ou Adobe Experience Platform e ao complemento Offer Decisioning.

* Concluir todas as lições para a configuração inicial do SDK da Web da Platform.

* Ative a organização para o Edge Decisioning.

* Entenda como configurar um posicionamento e instanciar IDs de posicionamento e atividade no Escopo de decisão JSON.

## Limitações

No momento, as ofertas baseadas em eventos não são compatíveis com o Adobe Journey Optimizer. Se você criar uma regra de decisão com base em um evento, não poderá aplicá-la em uma oferta.

## Conceder acesso à Gestão de decisões

Para conceder acesso à funcionalidade de Gestão de decisões, você deve criar um **Perfil de produto** e atribuir as permissões correspondentes aos usuários. [Saiba mais sobre como gerenciar usuários e permissões do Journey Optimizer nesta seção](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/access-control/privacy/high-low-permissions#decisions-permissions).

## Configurar o fluxo de dados

O Offer Decisioning deve ser habilitado na configuração **datastream** para que qualquer atividade de Gestão de decisões possa ser entregue pelo SDK da Web da plataforma.

Para configurar o Offer Decisioning no fluxo de dados:

1. Vá para a interface [Coleção de Dados](https://experience.adobe.com/#/data-collection).

1. Na navegação à esquerda, selecione **Datastreams**.

1. Selecione a sequência de dados do SDK da Web Luma criada anteriormente.

   ![Selecionar sequência de dados](assets/decisioning-datastream-select.png)

1. Selecione **Editar** no **Adobe Experience Platform Service**.

   ![Editar serviço](assets/decisioning-edit-datastream.png)

1. Marque a caixa **Offer decisioning**.

   ![ADICIONAR CAPTURA DE TELA](assets/decisioning-check-offer-box.png)

1. Selecione **Salvar**.

Isso garante que os eventos de entrada do Journey Optimizer sejam manipulados corretamente pela **Adobe Experience Platform Edge**.

## Configurar o SDK para a Gestão de decisões

A Gestão de decisões requer etapas adicionais do SDK, dependendo do tipo de implementação do SDK da Web. Há duas opções disponíveis para configurar o SDK para a Gestão de decisões.

* Instalação independente do SDK
   1. Configure a ação `sendEvent` com seu `decisionScopes`.

      ```javascript
      alloy("sendEvent", {
         ...
         "decisionScopes": [
            "[DECISION SCOPE 1]",
            "[DECISION SCOPE 2]"
         ]
      })
      ```

* Instalação de tags do SDK
   1. Vá para a interface da Coleção de dados.

   1. Na navegação à esquerda, selecione **Tags**.

      ![Selecionar Marcas](assets/decisioning-data-collection-tags.png)

   1. Selecione a **Propriedade da Marca**.

   1. Crie suas **Regras**.
      * Adicione um SDK da Web da plataforma **Enviar ação de evento** e adicione o `decisionScopes` relevante à configuração dessa ação.

   1. Crie e publique uma **Biblioteca** contendo todas as **Regras**, **Elementos de Dados** e **Extensões** relevantes que você configurou.

## Terminologia

Primeiro, você deve entender a terminologia usada na interface da Gestão de decisões.

* **Limite**: uma restrição que determina com que frequência uma oferta é exibida. Dois tipos:
   * Total de limites: número máximo de vezes que uma oferta pode ser mostrada no público-alvo.
   * Limite de perfil: vezes que uma oferta pode ser mostrada a um usuário específico.
* **Coleções**: subconjuntos de ofertas agrupados por condições específicas definidas por um profissional de marketing, por exemplo, categoria de oferta.
* **Decisão**: lógica que determina a escolha de uma oferta.
* **Regra de decisão**: restrições nas ofertas para descobrir a qualificação de um usuário.
* **Oferta Qualificada**: uma oferta que corresponde às restrições predefinidas e pode ser mostrada a um usuário.
* **Gerenciamento de decisão**: o sistema de criação e distribuição de ofertas personalizadas usando lógica de negócios e regras de decisão.
* **Ofertas substitutas**: a oferta padrão exibida quando um usuário não se qualifica para nenhuma oferta em uma coleção.
* **Oferta**: uma mensagem de marketing com regras de elegibilidade em potencial que determinam seus visualizadores.
* **Biblioteca de ofertas**: um repositório central que gerencia ofertas, decisões e regras associadas.
* **Ofertas personalizadas**: mensagens de marketing personalizadas adaptadas com base em restrições de qualificação.
* **Posicionamentos**: a configuração ou cenário em que uma oferta é exibida a um usuário.
* **Prioridade**: métrica de classificação para ofertas considerando várias restrições, como qualificação e limite.
* **Representações**: informações específicas do canal, por exemplo, localização ou idioma, que orientam a exibição de uma oferta.

## Visão geral do caso de uso - Recompensas de fidelidade

Nesta lição, você implementa um exemplo de caso de uso do Loyalty Rewards para entender a Gestão de decisões usando o SDK da Web.

Esse caso de uso permite entender melhor como a Journey Optimizer pode ajudar a fornecer a melhor oferta aos seus clientes, utilizando a biblioteca de ofertas centralizada e o mecanismo de decisão da Gestão de decisões.

>[!NOTE]
>
> Como este tutorial é destinado aos implementadores, vale a pena observar que esta lição envolve um trabalho de interface substancial no Journey Optimizer. Embora essas tarefas de interface sejam normalmente tratadas por profissionais de marketing, pode ser benéfico para os implementadores obterem insights sobre o processo, mesmo que não sejam responsáveis pela criação de campanhas de gestão de decisões a longo prazo.

## Componentes

Antes de começar a criar as ofertas, você deve definir vários componentes de pré-requisito.

### Criar um posicionamento para ofertas de fidelidade

**Posicionamentos** são contêineres usados para exibir as ofertas. Neste exemplo, você cria um posicionamento na parte superior do site Luma.

A lista de posicionamentos está acessível no menu **Componentes**. Os filtros estão disponíveis para ajudá-lo a recuperar inserções de acordo com um canal ou conteúdo específico.

![Exibir posicionamentos](assets/decisioning-placements-list.png)

Para criar a disposição, siga estas etapas:

1. Clique em **Criar posicionamento**.

   ![Criar posicionamento](assets/decisioning-create-placement.png)

1. Defina as propriedades da disposição:
   * **Nome**: o nome do posicionamento. Vamos chamar o exemplo de posicionamento *&#39;Banner da Página Inicial&#39;*.
   * **Tipo de canal**: o canal para o qual o posicionamento é usado. Vamos usar *&#39;Web&#39;*, pois as ofertas são exibidas no site da Luma.
   * **Tipo de conteúdo**: o tipo de conteúdo que o posicionamento tem permissão para exibir: Texto, HTML, Link de Imagem ou JSON. Você pode usar *&#39;HTML&#39;* para a oferta.
   * **Descrição**: uma descrição do posicionamento (opcional).

   ![Adicionar detalhes](assets/decisioning-placement-details.png)

1. Clique em **Salvar**.
1. Depois que a disposição é criada, ela é exibida na lista de disposições.
1. Selecione a linha que contém a nova disposição e anote a ID de disposição, pois isso pode ser necessário para configuração dentro do Escopo da decisão.

   ![Consulte a ID de Posicionamento ](assets/decisioning-placement-id.png)

### Regras de decisão para status de fidelidade

**As regras de decisão** especificam as condições em que as ofertas são apresentadas. Neste exemplo, você cria regras de decisão para atender ofertas diferentes dependendo do status de Fidelidade de um usuário.

A lista de regras de decisão está acessível no menu **Componentes**.

Para criar as regras de decisão, siga estas etapas:

1. Navegue até a guia **Regras** e clique em **Criar regra**.

   ![Criar a regra](assets/decisioning-create-rule.png)

1. Vamos nomear a primeira regra &#39;*Regra de status de fidelidade ouro*&#39;. Você pode usar campos XDM para definir a regra. O **Construtor de segmentos** da Adobe Experience Platform é uma interface intuitiva que pode ser usada para criar as condições da regra.

   ![Definir a regra](assets/decisioning-define-rule.png)

1. Clique em **Salvar** para confirmar a condição da regra.
1. A recém-salva &#39;*Regra de Status de Fidelidade Ouro*&#39; será exibida na **lista de Regras**. Selecione-a para exibir suas propriedades.

   ![Exibir regra criada](assets/decisioning-view-rules.png)

1. Agora crie as condições restantes da regra de oferta de fidelidade para o caso de uso.


### Qualificadores de Coleção

Os **qualificadores de coleção** permitem organizar e pesquisar facilmente por ofertas na biblioteca de ofertas. Neste exemplo, você adiciona qualificadores de coleção às ofertas do Loyalty Rewards para melhorar a organização da oferta.

A lista de qualificadores da coleção pode ser acessada no menu **Componentes**.

Para criar o qualificador de coleta do Loyalty Rewards, siga estas etapas:

1. Navegue até a guia **Qualificadores da coleção** e clique em **Criar qualificador da coleção**.

   ![Criar qualificador de coleção](assets/decisioning-create-collection-qualifier.png)

1. Vamos nomear o qualificador da coleção &#39;*Loyalty Rewards*&#39;

   ![Nomeie a coleção](assets/decisioning-name-collection.png)

1. O novo qualificador de coleção agora deve ser exibido na guia **Qualificador de coleção**

## Ofertas

Agora é hora de criar as ofertas do Loyalty Rewards.

A lista de ofertas está acessível no menu **Ofertas**.

![Exibir menu de ofertas](assets/decisioning-offers-menu.png)


### Criação de ofertas para diferentes níveis de fidelidade

Comece criando ofertas personalizadas para as diferentes Camadas de fidelidade Luma.

Para criar a primeira **oferta**, siga estas etapas:

1. Clique em **Criar oferta** e selecione **Oferta personalizada**.

1. Vamos nomear a primeira oferta &#39;*Camada de Fidelidade Luma - Gold*&#39;. Você deve especificar uma data e hora de início/término para esta oferta. Você também deve associar o **qualificador de coleção** &#39;*Recompensas de Fidelidade*&#39; à oferta, permitindo que você organize melhor dentro da **Biblioteca de Ofertas**. Depois, clique em **Avançar**.

   ![Adicionar detalhes da oferta](assets/decisioning-add-offer-details.png)

1. Agora você deve adicionar **representações** para definir onde a oferta é exibida. Vamos escolher o **canal da Web**. Também vamos escolher o **posicionamento** do *do &lbrace;Banner* Homepage configurado anteriormente. O **posicionamento** selecionado é do tipo HTML, portanto, você pode adicionar conteúdo de HTML, JSON ou TEXT diretamente ao editor para criar a oferta usando o botão de opção **Personalizado**.

   ![Adicionar detalhes da representação](assets/decisioning-add-representation-details.png)

1. Edite o conteúdo da oferta diretamente com o **Editor de Expressão**. Lembre-se de que você pode adicionar conteúdo HTML, JSON ou TEXT a essa disposição. Selecione o **modo** correto na parte inferior do editor, dependendo do seu tipo de conteúdo. Você também pode pressionar **validar** para garantir que não haja erros.

   ![Adicionar HTML de oferta](assets/decisioning-add-offer-html.png)

1. Além disso, você pode usar o Editor de expressão para recuperar atributos armazenados no Adobe Experience Platform. Vamos adicionar o nome de um perfil ao conteúdo da oferta para personalizar melhor os membros de fidelidade em um nível 1:1.

   ![Adicionar personalização da oferta](assets/decisioning-add-offer-personalization.png)

1. Adicione restrições para mostrar apenas a oferta a perfis qualificados para a &#39;*Regra de Status de Fidelidade Ouro*&#39;.

   ![Adicionar restrição de regra](assets/decisioning-add-rule-constraint.png)

1. Depois de concluir a revisão da oferta, clique em **Concluir**. Selecione **Salvar e aprovar**.

Agora crie o restante das ofertas para os vários níveis de fidelidade da Luma

### Ofertas substitutas

Você ainda deseja disponibilizar uma oferta para visitantes que não sejam da Fidelidade Luma no site Luma. Para fazer isso, você pode configurar uma **oferta substituta** para a campanha.

Para criar a oferta substituta, siga estas etapas:

1. Clique em **Criar oferta** e selecione **Oferta substituta**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Vamos nomear a oferta substituta &#39;*Fidelidade Não-Luma*&#39;. Você também pode associar o **qualificador de coleção**, &#39;*Recompensas de Fidelidade*&#39; criado anteriormente à oferta substituta para facilitar a organização da oferta.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Adicione o conteúdo da oferta substituta ao **Editor de Expressão**. Lembre-se de que você pode adicionar conteúdo HTML, JSON ou TEXT a esse posicionamento. Selecione o **modo** correto na parte inferior do editor, dependendo do seu tipo de conteúdo. Você também pode pressionar **validar** para garantir que não haja erros.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Se tudo estiver configurado corretamente, clique em **Concluir** e em **Salvar e aprovar**.
<!--
   ![ADD SCREENSHOT](#)
-->

## Decisões

**As decisões** são containers para ofertas que escolhem a melhor oferta disponível para um cliente, dependendo do público-alvo.

A lista de decisões está disponível na guia **Decisões** do menu **Ofertas**.
<!--
   ![ADD SCREENSHOT](#)
-->

### Criação de uma decisão para ofertas de fidelidade

Vamos criar uma decisão para o caso de uso de Recompensas de fidelidade Luma.

Para criar a decisão, siga estas etapas:

1. Clique em **Criar decisão**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Vamos chamar a decisão de &quot;*Ofertas de fidelidade da Luma de dezembro*&quot;. As ofertas devem ser executadas por 1 mês, então, vamos especificar isso aqui.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Agora você deve definir os **escopos de decisão**. Selecione primeiro uma disposição. Você pode usar o &#39;*Banner de Página Inicial*&#39; criado anteriormente.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Em seguida, você deve adicionar **critérios de avaliação** para o escopo da decisão. Clique em **Adicionar** e escolha a coleção &#39;*Recompensas de Fidelidade*&#39; criada anteriormente **que contém todas as ofertas de fidelidade a serem consideradas.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Dentro da coleção &#39;*Loyalty Rewards*&#39;, você pode usar o campo de qualificação para restringir a entrega de oferta a um subconjunto de visitantes da Luma. No entanto, nesse caso de uso, é desejável que cada visitante receba uma das ofertas. Lembre-se, você configurou uma **oferta substituta** para todos os visitantes que não são de fidelidade. Defina a qualificação como &quot;None&quot;.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Além disso, você pode usar o campo **método de classificação** para selecionar a melhor oferta para cada visitante do Luma, se várias ofertas estiverem qualificadas para a combinação de usuário/posicionamento. Neste caso de uso, você pode usar o método **Prioridade de oferta**, que usa os valores definidos nas ofertas para fornecer a melhor oferta.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Agora adicione a **oferta substituta** à decisão. Lembre-se de que a oferta substituta é a oferta padrão exibida para visitantes da Luma se eles não se enquadrarem em nenhum dos públicos-alvo da Fidelidade Luma. Selecione &#39;*Fidelidade Não-Luma*&#39; na lista de ofertas substitutas disponíveis para o posicionamento &#39;*Banner de Página Inicial*&#39;.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Antes de ativar a decisão, vamos analisar o escopo da decisão, a oferta substituta, visualizar as ofertas disponíveis e estimar os perfis qualificados. Depois que tudo estiver bem, você pode clicar em **Concluir** e **Salvar e ativar**.
<!--
   ![ADD SCREENSHOT](#)
-->

## Simulações

Como prática recomendada, você deve validar a lógica de decisão da Fidelidade Luma para garantir que as ofertas corretas sejam entregues aos públicos-alvo de fidelidade corretos. Você pode fazer essa validação usando **perfis de teste**. Também é uma boa ideia testar as alterações nas ofertas por meio de perfis de teste antes de enviar novas versões de oferta para produção.

Para iniciar o teste, selecione a guia **Simulações** no menu **Ofertas**.

### Teste de ofertas de fidelidade

1. Selecione um perfil de teste para usar na simulação. Clique em **Gerenciar perfil**. [Para criar ou designar um novo perfil de teste para teste de oferta, siga este guia](https://experienceleague.adobe.com/en/docs/journeys/using/building-journeys/about-journey-building/creating-test-profiles#create-test-profiles-csv).
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Adicione um ou mais perfis de teste à simulação e salve a seleção. Para o teste de caso de uso, verifique se você tem perfis de teste configurados para cada público-alvo de recompensas de fidelidade do Luma.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Selecione o escopo de decisão a ser testado. Selecione **Adicionar escopo da decisão**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Selecione o posicionamento &#39;*Banner de Página Inicial*&#39; criado anteriormente.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. As decisões disponíveis são exibidas, selecione a decisão &#39;*Ofertas de fidelidade de dezembro da Luma*&#39; criada anteriormente e clique em **Adicionar**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Depois de selecionar um perfil de teste, clique em **Exibir resultados**. A melhor oferta disponível é exibida no perfil de teste selecionado para a decisão &#39;*Ofertas de fidelidade da Luma de dezembro*&#39;.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Selecione um perfil de teste diferente e clique em **Exibir resultados**. Idealmente, você deve ver uma oferta simulada diferente, correspondente ao nível de fidelidade do perfil de teste.

## Validação do Gerenciamento de decisão usando o Adobe Experience Platform Debugger

A extensão **Adobe Experience Platform Debugger**, disponível para Chrome e Firefox, analisa suas páginas da Web para identificar problemas na implementação de soluções da Adobe Experience Cloud.

Você pode usar o depurador no site Luma para validar a lógica de decisão na produção. Essa validação é uma boa prática depois que o caso de uso de Fidelidade de recompensas está em execução, para garantir que tudo seja configurado corretamente.

[Saiba como configurar o depurador em seu navegador usando o guia aqui](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/debugger/overview).

Para iniciar a validação usando o depurador:

1. Navegue até a página da Web do Luma com o posicionamento da oferta.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Na página da Web, abra o **Adobe Experience Platform debugger**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Navegue até **Resumo**. Verifique se a **ID da sequência de dados** corresponde à **sequência de dados** da **Coleção de dados do Adobe** para a qual você habilitou o Offer decisioning.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Em **Soluções**, navegue até o **Experience Platform Web SDK**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Na guia **Configuração**, ative **Habilitar Depuração**. Isso habilita o registro para a sessão em uma sessão do **Adobe Experience Platform Assurance**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Você pode fazer logon no site com várias contas de fidelidade Luma e usar o depurador para validar as solicitações enviadas à **rede Edge do Adobe Experience Platform**. Todas essas solicitações devem ser capturadas em **Assurance** para rastreamento de log.
<!--
   ![ADD SCREENSHOT](#)
-->

[Próximo: ](setup-consent.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [postagem de Discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
