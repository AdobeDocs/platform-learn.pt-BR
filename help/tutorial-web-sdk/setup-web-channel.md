---
title: Configurar o canal da Web do Journey Optimizer com o SDK da Web da plataforma
description: Saiba como implementar o canal da Web da Journey Optimizer usando o SDK da Web da plataforma. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
solution: Data Collection,Experience Platform,Journey Optimizer
feature-set: Journey Optimizer
feature: Web Channel,Web SDK
exl-id: ab83ce56-7f54-4341-8750-b458d0db0239
source-git-commit: aeff30f808fd65370b58eba69d24e658474a92d7
workflow-type: tm+mt
source-wordcount: '2885'
ht-degree: 0%

---


# Configurar canal da Web do Journey Optimizer

Saiba como implementar o Journey Optimizer [canal da web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/web/get-started-web) usando o SDK da Web da plataforma. Esta lição aborda os pré-requisitos básicos do canal da Web, as etapas detalhadas de configuração e um aprofundamento sobre um caso de uso centrado no status de fidelidade.

Ao seguir esta lição, os usuários do Journey Optimizer estão equipados para aplicar efetivamente o canal da Web para personalização online avançada usando o web designer do Journey Optimizer.

![Diagrama do SDK da Web e Adobe Analytics](assets/dc-websdk-ajo.png)

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Entenda a função e o significado do SDK da Web no fornecimento da experiência de canal da Web.
* Entenda o processo de criação de uma campanha de canal da Web do início ao fim utilizando o caso de uso de amostra do Luma Loyalty Rewards.
* Configure propriedades, ações e agendamentos da campanha na interface.
* Entenda a funcionalidade e os benefícios da extensão Auxiliar de edição visual do Adobe Experience Cloud.
* Saiba como editar o conteúdo da página da Web, incluindo imagens, cabeçalhos e outros elementos, usando o web designer.
* Saiba como inserir ofertas em uma página da Web usando o componente Offer decision.
* Familiarize-se com as práticas recomendadas para garantir a qualidade e o sucesso de uma campanha de canal da Web.

## Pré-requisitos

Para concluir as lições desta seção, primeiro você deve:

* Completar todas as lições para a configuração inicial do SDK da Web da Platform, incluindo a configuração de elementos de dados e regras.
* Verifique se a versão da extensão de tags do SDK da Web da Adobe Experience Platform é 2.16 ou superior.
* Se você estiver usando o web designer da Journey Optimizer para criar sua experiência de canal na Web, verifique se está usando os navegadores Google Chrome ou Microsoft® Edge.
* Verifique também se você baixou e ativou o [Extensão de navegador da Adobe Experience Cloud Visual Editing Helper](https://chromewebstore.google.com/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca).
* Verifique se os cookies de terceiros são permitidos em seu navegador. Talvez seja necessário desativar os bloqueadores de anúncios no navegador também.

  >[!CAUTION]
  >
  > No web designer do Journey Optimizer, alguns sites podem não ser abertos de forma confiável devido a um dos seguintes motivos:
  > 
  > 1. O site tem políticas de segurança rigorosas.
  > 1. O site é incorporado em um iframe.
  > 1. O site de controle de qualidade ou preparo do cliente não está acessível externamente (é um site interno).

* Ao criar experiências da Web e incluir conteúdo da biblioteca do Adobe Experience Manager Assets Essentials, é necessário [configurar o subdomínio para publicar este conteúdo](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/web/web-delegated-subdomains).
* Se estiver usando o recurso de experimentação de conteúdo, verifique se o conjunto de dados da Web também está incluído na configuração de relatórios.
* Atualmente, há suporte para dois tipos de implementações para habilitar a criação e o delivery de campanhas de canal da Web nas propriedades da Web:
   * Somente no lado do cliente: para modificar seu site, você deve implementar o SDK da Web da Adobe Experience Platform.
   * Modo híbrido: você pode utilizar a API do servidor do Platform Edge Network para solicitar personalização no lado do servidor. A resposta da API é então fornecida ao SDK da Web da Adobe Experience Platform para renderizar modificações no lado do cliente. Para obter mais informações, consulte a documentação da API do Adobe Experience Platform Edge Network Server. Detalhes adicionais e amostras de implementação para o modo híbrido podem ser encontrados nesta publicação do blog.

  >[!NOTE]
  >
  >A implementação somente do lado do servidor não é compatível no momento.




## Terminologia

Primeiro, você deve entender a terminologia usada nas campanhas de canal da Web.

* **Canal da Web**: um meio de comunicação ou entrega de conteúdo pela Web. No contexto deste guia, ele se refere ao mecanismo pelo qual o conteúdo personalizado é entregue aos visitantes do site usando o SDK da Web da plataforma no Adobe Journey Optimizer.
* **Superfície da Web**: refere-se a uma propriedade da Web identificada por um URL em que o conteúdo é entregue. Pode abranger uma ou várias páginas da Web.
* **web designer do Journey Optimizer**: uma ferramenta ou interface específica na Journey Optimizer em que os usuários podem criar suas experiências de canal da Web.
* **Adobe Experience Cloud Visual Editing Helper**: uma extensão do navegador que ajuda a editar visualmente e criar experiências de canal da Web.
* **Sequência de dados**: uma configuração no serviço Adobe Experience Platform que garante que as experiências de canal da Web possam ser fornecidas.
* **Política de mesclagem**: uma configuração que garante a ativação e a publicação precisas de campanhas de entrada.
* **Público**: um segmento específico de usuários ou visitantes do site que atendem a determinados critérios.
* **Designer da Web**: uma interface ou ferramenta que ajuda a editar visualmente e criar experiências na Web sem mergulhar no código.
* **Editor de expressão**: uma ferramenta no web designer que permite aos usuários adicionar personalização ao conteúdo da Web, possivelmente com base em atributos de dados ou outros critérios.
* **Componente da Offer Decision**: um componente no web designer que ajuda a decidir qual oferta é mais adequada para ser exibida a um visitante específico com base na gestão de decisões.
* **Experimento de conteúdo**: um método para testar diferentes variações de conteúdo e descobrir qual delas tem o melhor desempenho em termos da métrica desejada, como cliques de entrada.
* **Tratamento**: No contexto de experimentos de conteúdo, um tratamento se refere a uma variação específica de conteúdo que está sendo testado em relação a outra.
* **Simulação**: um mecanismo de visualização para visualizar a experiência de canal da Web antes de ativá-la para públicos-alvo ao vivo.

## Configurar o fluxo de dados

Você já adicionou o serviço Adobe Experience Platform ao seu fluxo de dados. Agora é necessário habilitar a opção Adobe Journey Optimizer para fornecer experiências de canal da Web.

Para configurar o Adobe Journey Optimizer na sequência de dados:

1. Vá para a [Coleta de dados](https://experience.adobe.com/#/data-collection){target="blank"} interface.
1. Na navegação à esquerda, selecione **[!UICONTROL Datastreams]**.
1. Selecione a sequência de dados do SDK da Web Luma criada anteriormente.

   ![Selecionar sequência de dados](assets/web-channel-select-datastream.png)

1. Selecionar **[!UICONTROL Editar]** no serviço Adobe Experience Platform.

   ![Editar sequência de dados](assets/web-channel-edit-datastream.png)

1. Verifique a **[!UICONTROL Adobe Journey Optimizer]** caixa.

   ![Caixa Verificar AJO](assets/web-channel-check-ajo-box.png)

1. Selecione **[!UICONTROL Salvar]**.

Isso garante que os eventos de entrada do Journey Optimizer sejam manipulados corretamente pelo Edge Network Adobe Experience Platform.

## Configurar a política de mesclagem

Verifique se uma política de mesclagem está definida com o **[!UICONTROL Política de mesclagem ativa na borda]** opção ativada. Essa opção de política de mesclagem é empregada pelos canais de entrada do Journey Optimizer para garantir a ativação e a publicação precisas de campanhas de entrada na borda.

Para configurar a opção na política de mesclagem:

1. Vá para a **[!UICONTROL Cliente]** > **[!UICONTROL Perfis]** página na interface do Experience Platform ou Journey Optimizer.
1. Selecione o **[!UICONTROL Políticas de mesclagem]** guia.
1. Selecione sua política (geralmente é melhor usar a variável [!UICONTROL Timebased Padrão] política) e alterne a variável **[!UICONTROL Política de mesclagem ativa na borda]** opção no campo **[!UICONTROL Configurar]** etapa.

   ![Alternar política de mesclagem](assets/web-channel-active-on-edge-merge-policy.png)

## Configurar o conjunto de dados da Web para experimentação de conteúdo

Para usar experimentos de conteúdo em campanhas de canal da Web, você deve garantir que o conjunto de dados da Web usado também seja incluído na configuração dos relatórios. O sistema de relatórios do Journey Optimizer usa o conjunto de dados somente leitura para preencher relatórios de experimentação de conteúdo prontos para uso.

[A adição de conjuntos de dados para os relatórios de experimento de conteúdo é detalhada nesta seção](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/content-experiment/reporting-configuration#add-datasets).

## Visão geral do caso de uso - Recompensas de fidelidade

Nesta lição, um exemplo de caso de uso de Recompensas de fidelidade é usado para detalhar a implementação de uma experiência de canal da Web usando o SDK da Web.

Esse caso de uso permite entender melhor como o Journey Optimizer pode ajudar a fornecer as melhores experiências de entrada aos seus clientes, utilizando campanhas do Journey Optimizer e o web designer.

Como este tutorial é destinado aos implementadores, vale a pena observar que esta lição envolve um trabalho de interface substancial no Journey Optimizer. Embora essas tarefas de interface sejam normalmente tratadas por profissionais de marketing, pode ser benéfico para os implementadores obterem insights sobre o processo, mesmo que eles não sejam normalmente responsáveis pela criação de campanhas de canais da Web.

### Criar um esquema de fidelidade e assimilar dados de amostra

Quando os dados do SDK da Web são assimilados na Adobe Experience Platform, eles podem ser enriquecidos por outras fontes de dados assimiladas na Platform. Por exemplo, quando um usuário faz logon no site Luma, um gráfico de identidade é construído no Experience Platform e todos os outros conjuntos de dados habilitados para perfis podem ser unidos para criar Perfis de clientes em tempo real. Para ver isso em ação, crie rapidamente outro conjunto de dados no Adobe Experience Platform com alguns dados de fidelidade de exemplo, para que você possa usar Perfis de clientes em tempo real em campanhas da Web do Journey Optimizer. Como você já fez exercícios semelhantes, as instruções serão breves.

Crie o esquema de fidelidade:

1. Criar um novo esquema
1. Escolher **[!UICONTROL Perfil individual]** como o [!UICONTROL classe base]
1. Nomeie o esquema `Luma Loyalty Schema`
1. Adicione o [!UICONTROL Detalhes de fidelidade] grupo de campos
1. Adicione o [!UICONTROL Detalhes demográficos] grupo de campos
1. Selecione o `Person ID` e marque-o como um [!UICONTROL Identidade] e [!UICONTROL Identidade principal] usando o `Luma CRM Id` [!UICONTROL Namespace de identidade].
1. Ativar o esquema para [!UICONTROL Perfil]

   ![Esquema de fidelidade](assets/web-channel-loyalty-schema.png)

Para criar o conjunto de dados e assimilar os dados de amostra:

1. Crie um novo conjunto de dados pela `Luma Loyalty Schema`
1. Nomeie o conjunto de dados `Luma Loyalty Dataset`
1. Ativar o conjunto de dados para [!UICONTROL Perfil]
1. Baixe o arquivo de amostra [luma-fidelization-forWeb.json](assets/luma-loyalty-forWeb.json)
1. Arraste e solte o arquivo no seu conjunto de dados
1. Confirme se os dados foram assimilados com êxito

   ![Esquema de fidelidade](assets/web-channel-loyalty-dataset.png)

### Criar um público-alvo

Os públicos-alvo agrupam perfis em torno de características comuns. Crie um público-alvo rápido que você pode usar em sua campanha da Web:

1. Na interface do Experience Platform, vá para **[!UICONTROL Públicos-alvo]** na navegação à esquerda
1. Selecionar **[!UICONTROL Criar público]**
1. Selecionar **[!UICONTROL Criar regra]**
1. Selecionar **[!UICONTROL Criar]**

   ![Criar um público-alvo](assets/web-campaign-create-audience.png)

1. Selecionar **[!UICONTROL Atributos]**
1. Localize o **[!UICONTROL Fidelidade]** > **[!UICONTROL Nível]** e arraste-o para a **[!UICONTROL Atributos]** seção
1. Definir o público-alvo como usuários cujos `tier` é `gold`
1. Nomear o público `Luma Loyalty Rewards – Gold Status`
1. Selecionar **[!UICONTROL Edge]** como o **[!UICONTROL Método de avaliação]**
1. Selecionar **[!UICONTROL Salvar]**

   ![Definir o público-alvo](assets/web-campaign-define-audience.png)

Como esse é um público-alvo muito simples, podemos usar o método de avaliação Edge. Os públicos-alvo da borda avaliam a borda, portanto, na mesma solicitação feita pelo SDK da Web para o Platform Edge Network, podemos avaliar a definição do público-alvo e confirmar imediatamente se o usuário se qualificará.

### Criar campanha de recompensas de fidelidade

Agora que você assimilou nossos dados de fidelidade de amostra e criou nosso segmento, crie a campanha do canal da Web Loyalty Rewards no Adobe Journey Optimizer.

Para criar a campanha de amostra:

1. Abra o [Journey Optimizer](https://experience.adobe.com/journey-optimizer/home){target="_blank"} interface

   >[!NOTE]
   >
   > Esquema, conjuntos de dados e públicos também podem ser criados na interface do Journey Optimizer, pois são construções de Experience Platform comuns.

1. Navegue até **[!UICONTROL Gerenciamento de jornadas]** > **[!UICONTROL Campanhas]** na navegação à esquerda
1. Clique em **[!UICONTROL Criar campanha]** no canto superior direito.
1. No **[!UICONTROL Propriedades]** especifique como deseja executar a campanha. Para o caso de uso do Loyalty Rewards, escolha **Agendado**.

   ![Campanha programada](assets/web-channel-campaign-properties-scheduled.png)

1. No **[!UICONTROL Ações]** escolha a opção **[!UICONTROL Canal da Web]**. Como a variável  **[!UICONTROL Superfície da Web]**, selecione **[!UICONTROL URL da página]**.

   >[!NOTE]
   >
   >Uma superfície da Web se refere a uma propriedade da Web identificada por um URL em que o conteúdo é entregue. Ele pode corresponder a um único URL de página ou abranger várias páginas, permitindo aplicar modificações em uma ou várias páginas da Web.

1. Escolha o **[!UICONTROL URL da página]** opção de superfície da web para implantar a experiência em uma página para esta campanha. Insira o URL da página Luma, `https://luma.enablementadobe.com/content/luma/us/en.html`

1. Depois que a superfície da web for definida, selecione **[!UICONTROL Criar]**.

   ![Selecionar superfície da Web](assets/web-channel-web-surface.png)

1. Agora, adicione alguns detalhes adicionais à nova campanha de canal da Web. Primeiro, nomeie a campanha. Chame `Luma Loyalty Rewards – Gold Status`. Opcionalmente, é possível adicionar uma descrição à campanha. Também adicionar **[!UICONTROL Tags]** para melhorar a taxonomia geral da campanha.

   ![Nomeie a campanha](assets/web-channel-campaign-name.png)

1. Por padrão, a campanha está ativa para todos os visitantes do site. Para os fins deste caso de uso, somente os membros do prêmio gold status devem ver a experiência. Para habilitar isso, clique em **[!UICONTROL Selecionar público]** e escolha o `Luma Loyalty Rewards – Gold Status` público-alvo.

1. No **[!UICONTROL Namespace de identidade]** selecione o namespace para identificar indivíduos dentro do segmento escolhido. Como você está implantando a campanha no site Luma, é possível escolher o namespace da ECID. Perfis dentro do `Luma Loyalty Rewards – Gold Status` O público-alvo que não tem o namespace ECID entre suas várias identidades não é direcionado pela campanha do canal da Web.

   ![Escolher tipo de identidade](assets/web-channel-indentity-type.png)

1. Programe a campanha para começar na data de hoje usando o **[!UICONTROL Início da campanha]** e terminará em uma semana usando a opção **[!UICONTROL Fim da campanha]** opção.

   ![Programação de campanha](assets/web-channel-campaign-schedule.png)

>[!NOTE]
>
>Lembre-se de que, para campanhas de canal da Web, a experiência da Web é mostrada quando o visitante abre a página. Portanto, ao contrário de outros tipos de campanhas no Adobe Journey Optimizer, a **[!UICONTROL Acionadores de ação]** seção não configurável.

### Experimento com conteúdo de recompensas de fidelidade

Se você rolar a tela de volta para cima, na janela **[!UICONTROL Ação]** é possível criar um experimento para testar qual conteúdo funciona melhor para a `Luma Loyalty Rewards – Gold Status` público-alvo. Vamos criar e testar dois tratamentos como um componente da configuração da campanha.

Para criar o experimento de conteúdo:

1. Clique em **[!UICONTROL Criar experimento]**.

   ![Criar experimento](assets/web-channel-create-content-experiment.png)

1. Primeiro escolha um **[!UICONTROL Métrica de sucesso]**. Essa é a métrica para determinar a eficácia do conteúdo. Escolher **[!UICONTROL Cliques de entrada únicos]**, para ver qual tratamento de conteúdo gera mais cliques no CTA de experiência da Web.

   ![Escolher métrica de sucesso](assets/web-channel-content-experiment-metric.png)

1. Ao configurar um experimento usando um canal da Web e escolhendo o **[!UICONTROL Cliques de entrada]**, **[!UICONTROL Cliques de entrada únicos]**, **[!UICONTROL Exibições de página]** ou **[!UICONTROL Visualizações únicas de página]** métricas, a variável **[!UICONTROL Ação do clique]** permite rastrear e monitorar com precisão os cliques e as exibições em páginas específicas.

1. Opcionalmente, você pode designar um **[!UICONTROL Retenção]** que não recebe nenhum dos dois tratamentos. Deixe essa opção desmarcada por enquanto.

1. Além disso, opcionalmente, escolha **[!UICONTROL Distribuir uniformemente]**. Marque esta opção para garantir que as divisões de tratamento sejam sempre divididas uniformemente.

[Saiba mais sobre experimentos de conteúdo no canal da Web do Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/content-experiment/get-started-experiment).

### Editar conteúdo usando o Auxiliar visual

Agora vamos criar a experiência de canal da Web. Para fazer isso, use o Adobe Experience Cloud **[!UICONTROL Auxiliar visual]**. Esta ferramenta é uma extensão de navegador compatível com o Google Chrome e Microsoft® Edge. Verifique se você baixou a extensão antes de tentar criar suas experiências. Além disso, verifique se a página da Web inclui o SDK da Web.

1. No prazo de **[!UICONTROL Ação]** da campanha, clique em **[!UICONTROL Editar conteúdo]**. Como você inseriu uma URL de página única como superfície, você deve estar pronto para começar a trabalhar no compositor.

   ![Editar conteúdo](assets/web-channel-edit-content.png)

1. Agora clique em **[!UICONTROL Editar página da Web]** para começar a criar.

   ![Editar página da Web](assets/web-channel-edit-web-page.png)

1. Comece editando alguns elementos com o web composer. Use o menu contextual para editar o cabeçalho de imagem herói Luma. Ajuste o estilo do painel contextual à direita.

   ![Adicionar edições contextuais](assets/web-channel-some-contextual-edit.png)

1. Além disso, adicione personalização ao contêiner usando o **[!UICONTROL Editor de expressão]**.

   ![Adicionar personalização](assets/web-channel-add-basic-personalization.png)

1. Verifique se a experiência está sendo rastreada adequadamente para cliques. Escolher **[!UICONTROL Clicar no elemento de rastreamento]** no menu contextual.

   ![Rastrear cliques](assets/web-channel-click-tracking.png)

1. Use o **[!UICONTROL Componente da Offer Decision]** para inserir ofertas na página da Web. Este componente usa **[!UICONTROL Gerenciamento de decisão]** para escolher a melhor oferta para entregar aos visitantes da Luma.


### Alterações no design do HTML

Há alguns métodos disponíveis caso você queira fazer alterações mais avançadas ou personalizadas no site como um componente da campanha de Recompensas de Fidelidade.

Use o **[!UICONTROL Componentes]** painel para adicionar HTML ou outro conteúdo diretamente ao site Luma.

![Explorar o painel de componentes](assets/web-channel-components-pane.png)

Adicione um novo componente HTML na parte superior da página. Edite o HTML dentro do componente na interface de design ou **[!UICONTROL Contextual]** painel.

![Adicionar HTML personalizado](assets/web-channel-add-html-component.png)

Como alternativa, adicione edições de HTML do **[!UICONTROL Modificações]** painel. Esse painel permite selecionar um componente na página e editá-lo na interface do designer.

No editor, adicione o HTML para a variável `Luma Loyalty Rewards – Gold Status` público-alvo. Selecionar **[!UICONTROL Validar]**.

![Validar HTML](assets/web-channel-add-custom-html-validate.png)

Agora, revise o novo componente de HTML personalizado para adequação e funcionalidade.

![Revisar HTML personalizado](assets/web-channel-review-custom-html.png)

Editar um componente específico usando o **[!UICONTROL Tipo de seletor de CSS]** modificação.

![Modificar CSS](assets/web-channel-css-selector.png)

Adicionar código personalizado usando o **Página `<head>` type** modificação.

![Modificar cabeçalho](assets/web-channel-page-head-modification.png)

As possibilidades são infinitas usando o **[!UICONTROL Auxiliar visual]**.

### Simular conteúdo de prêmios de fidelidade

Visualize a página da Web modificada antes de ativar a campanha. Lembre-se de que você deve ter perfis de teste configurados para simular experiências de canal da Web.

Para simular a experiência:

1. Selecionar **[!UICONTROL Simular conteúdo]** dentro da campanha.

   ![Simular conteúdo](assets/web-channel-simulate-content.png)

1. Escolha um perfil de teste para receber a simulação. Lembre-se de que o perfil de teste deve estar no estado `Luma Loyalty Rewards – Gold Status` público-alvo para receber o tratamento adequado.

1. A visualização é exibida para o perfil de teste.

### Ativação da campanha de prêmios de fidelidade

Por fim, ative a campanha do canal Web.

1. Selecionar **Revisar para ativar**.

1. Você será solicitado a confirmar os detalhes da campanha uma última vez. Selecionar **[!UICONTROL Ativar]**. Pode levar até 15 minutos para que a campanha seja ativada no site.

### Garantia de qualidade das recompensas de fidelidade

Você pode usar alguns logons para simular usuários com o &quot;status gold&quot; e se qualificar para a sua campanha:

1. `cleavlandeuler@emailsim.io`/`test`
1. `leftybeagen@emailsim.io`/`test`
1. `jenimartinho@emailsim.io`/`test`

Como prática recomendada, monitore o **[!UICONTROL Web]** dos relatórios campaign live e global para os KPIs específicos da campanha. Para esta campanha, monitore as impressões da experiência e a taxa de cliques.

![Exibir relatório da Web](assets/web-channel-web-report.png)

### Validação de canal da Web usando Adobe Experience Platform Debugger

A extensão Adobe Experience Platform Debugger, disponível para Chrome e Firefox, analisa suas páginas da Web para identificar problemas na implementação das soluções da Adobe Experience Cloud.

Você pode usar o depurador no site Luma para validar a experiência do canal da Web em produção. Esta é uma prática recomendada quando o caso de uso de Recompensas de fidelidade está em execução, para garantir que tudo seja configurado corretamente.

[Saiba como configurar o depurador em seu navegador usando o guia aqui](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/debugger/overview).

Para iniciar a validação usando o depurador:

1. Navegue até a página da Web do Luma com a experiência do canal da Web.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Na página da Web, abra **[!UICONTROL Adobe Experience Platform Debugger]**.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Navegue até **Resumo**. Verifique se **[!UICONTROL ID da sequência de dados]** corresponde ao **[!UICONTROL sequência de dados]** in **[!UICONTROL Coleta de dados Adobe]** para o qual você ativou o Adobe Journey Optimizer.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Em seguida, você pode fazer logon no site com várias contas de fidelidade Luma e usar o depurador da para validar as solicitações enviadas para o Edge Network do Adobe Experience Platform.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Em **[!UICONTROL Soluções]** navegue até o **[!UICONTROL Experience Platform Web SDK]**.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. No prazo de **Configuração** guia, alternar em **[!UICONTROL Habilitar Depuração]**. Isso permite o registro da sessão em um **[!UICONTROL Adobe Experience Platform Assurance]** sessão.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Faça logon no site com várias contas de fidelidade Luma e use o depurador para validar as solicitações enviadas para o **[!UICONTROL Rede de borda Adobe Experience Platform]**. Todas essas solicitações devem ser capturadas no **[!UICONTROL Assurance]** para rastreamento de log.
<!--
   ![ADD SCREENSHOT](#)
-->

[Próximo: ](setup-decision-management.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar feedback geral ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
