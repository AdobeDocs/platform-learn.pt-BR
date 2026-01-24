---
title: Configurar o Adobe Target com o Platform Web SDK
description: Saiba como implementar o Adobe Target usando o Platform Web SDK. Esta lição é parte do tutorial Implementar a Adobe Experience Cloud com o SDK da web.
solution: Data Collection, Target
jira: KT-15410
exl-id: 9084f572-5fec-4a26-8906-6d6dd1106d36
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '4362'
ht-degree: 1%

---

# Configurar o Adobe Target com o Platform Web SDK

Saiba como implementar o Adobe Target usando o SDK da web da Adobe Experience Platform. Saiba como fornecer experiências e transmitir parâmetros adicionais para o Target.

O [Adobe Target](https://experienceleague.adobe.com/pt-br/docs/target/using/target-home) é o aplicativo da Adobe Experience Cloud que oferece tudo o que você precisa para ajustar e personalizar a experiência do cliente e maximizar a receita em sites da Web e móveis, aplicativos e outros canais digitais.

![Diagrama do Web SDK e Adobe Target](assets/dc-websdk-at.png)

## Objetivos de aprendizagem

No final desta lição, você poderá fazer o seguinte com uma implementação do Web SDK do Target:

* Adicionar o trecho pré-ocultação para evitar cintilação
* Configurar um fluxo de dados para habilitar a funcionalidade do Target
* Renderizar atividades do visual experience composer
* Renderizar atividades do compositor de formulários
* Envio de dados XDM para o Target e compreensão do mapeamento para parâmetros do Target
* Enviar dados personalizados para o Target, como parâmetros de perfil e entidade
* Validar uma implementação do Target
* Separar solicitações de personalização de solicitações de análise

>[!TIP]
>
>Consulte nosso tutorial [Migrar o Target da at.js 2.x para o Platform Web SDK](/help/tutorial-migrate-target-websdk/introduction.md) para obter um guia passo a passo para migrar sua implementação at.js existente.


## Pré-requisitos

Para concluir as lições desta seção, primeiro você deve:

* Conclua todas as lições para a configuração inicial do Platform Web SDK, incluindo a configuração de elementos de dados e regras.
* Verifique se você tem uma [função de Editor ou Aprovador](https://experienceleague.adobe.com/pt-br/docs/target/using/administer/manage-users/enterprise/properties-overview#section_8C425E43E5DD4111BBFC734A2B7ABC80) no Adobe Target.
* Instale a [extensão auxiliar do Visual Experience Composer](https://experienceleague.adobe.com/pt-br/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension) se estiver usando o navegador Google Chrome.
* Saber como configurar atividades no Target. Se você precisar de uma atualização, os seguintes tutoriais e guias serão úteis para esta lição:
   * [Usar a Extensão Auxiliar do Visual Experience Composer (VEC)](https://experienceleague.adobe.com/pt-br/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension)
   * [Usar o Visual Experience Composer](https://experienceleague.adobe.com/pt-br/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer)
   * [Usar o Experience Composer baseado em formulário](https://experienceleague.adobe.com/pt-br/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer)
   * [Criar atividades de direcionamento de experiência](https://experienceleague.adobe.com/pt-br/docs/target-learn/tutorials/activities/create-experience-targeting-activities)

## Adicionar tratamento de cintilação

Antes de iniciar, determine se é necessária uma solução extra de tratamento de cintilação, dependendo de como a biblioteca de tags é carregada.

>[!NOTE]
>
>Este tutorial usa o [site da Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target=_blank}, que tem uma implementação assíncrona de tags e mitigação de cintilação em vigor. Esta seção é para referência para entender como a mitigação de cintilação funciona com o Platform Web SDK.


### Implementação assíncrona

Quando uma biblioteca de tags é carregada de forma assíncrona, a página pode terminar a renderização antes que o Target substitua o conteúdo padrão pelo conteúdo personalizado. Esse comportamento pode levar ao que é conhecido como &quot;oscilação&quot;, onde o conteúdo padrão é exibido brevemente antes de ser substituído pelo conteúdo personalizado. Caso deseje evitar essa oscilação, a Adobe recomenda adicionar um trecho especial de pré-ocultação imediatamente antes do código incorporado da tag assíncrona.

Este trecho já está presente no site Luma, mas vamos examinar mais de perto para entender o que esse código faz:

```html
<script>
  !function(e,a,n,t){var i=e.head;if(i){
  if (a) return;
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, ".personalization-container { opacity: 0 !important }", 3000);
</script>
```

O trecho pré-ocultação cria uma tag de estilo no cabeçalho da página com a definição CSS de sua escolha. Essa tag de estilo é removida quando uma resposta do Target é recebida ou o tempo limite é atingido.

O comportamento de pré-ocultação é controlado por duas configurações no final do trecho.

* `body { opacity: 0 !important }` especifica a definição de CSS a ser usada para a pré-ocultação até o Target ser carregado. Por padrão, a página inteira fica oculta. É possível atualizar essa definição para os seletores que deseja pré-ocultar junto com a forma como deseja ocultá-los. Você pode incluir várias definições, pois esse valor é simplesmente o que está inserido na tag de estilo de pré-ocultação. Se você tiver um elemento de contêiner de fácil identificação que abranja o conteúdo abaixo de sua navegação, poderá usar essa configuração para limitar a pré-ocultação a esse elemento do contêiner.
* `3000` especifica o tempo limite em milissegundos para a pré-ocultação. Se uma resposta do Target não for recebida antes do tempo limite, a tag de estilo de pré-ocultação será removida. Atingir esse tempo limite deve ser raro.

>[!NOTE]
>
>O trecho pré-ocultação do Platform Web SDK é um pouco diferente daquele usado com a biblioteca at.js do Target. Certifique-se de usar o trecho correto para o Platform Web SDK, pois ele usa uma ID de estilo diferente de `alloy-prehiding`. Se o trecho de pré-ocultação da at.js for usado, talvez ele não funcione corretamente.

O trecho de pré-ocultação também está disponível nas tags:

1. Vá para a seção **[!UICONTROL Extensões]** das tags
1. Selecione **[!UICONTROL Configurar]** para a extensão do Adobe Experience Platform Web SDK
1. Selecione o botão **[!UICONTROL Copiar trecho oculto previamente na área de transferência]**

   ![Trecho de pré-ocultação do Target para implementações assíncronas](assets/target-flicker-async.png)

   >[!NOTE]
   >
   >O trecho pré-ocultação padrão copiado da extensão do Platform Web SDK pode incluir uma definição CSS que não existe no site, como `.personalization-container { opacity: 0 !important }`. Verifique e modifique o trecho pré-ocultação apropriadamente para o seu site.

### Implementação síncrona

A Adobe recomenda implementar tags de forma assíncrona, conforme demonstrado no site Luma. No entanto, se a biblioteca de tags for carregada de forma síncrona, o trecho pré-ocultação não será necessário. Em vez disso, o estilo de pré-ocultação é especificado nas configurações da extensão do Platform Web SDK.

O estilo de pré-ocultação para implementações síncronas pode ser configurado da seguinte maneira:

1. Vá para a seção **[!UICONTROL Extensões]** das tags
1. Selecione o botão **[!UICONTROL Configurar]** para a extensão do Platform Web SDK
1. Selecione o botão **[!UICONTROL Editar estilo pré-ocultado]**

   ![Trecho de pré-ocultação do Target para implementações assíncronas](assets/target-flicker-sync.png)

1. Modifique o CSS para incluir os seletores e ocultar os métodos que gostaria de usar, por exemplo: `body { opacity: 0 !important }` se quiser pré-ocultar todo o corpo da página.
1. Salvar as alterações e criar em uma biblioteca

>[!NOTE]
>
>A configuração de estilo de pré-ocultação deve ser usada somente para implementações síncronas. Esse estilo deve estar em branco ou ser comentado se estiver usando uma implementação assíncrona de tags.

Para saber mais sobre como o Platform Web SDK pode gerenciar a cintilação, consulte a seção do guia: [gerenciamento da cintilação para experiências personalizadas](https://experienceleague.adobe.com/pt-br/docs/experience-platform/edge/personalization/manage-flicker).


## Configurar o fluxo de dados

O Target deve ser ativado na configuração da sequência de dados antes que qualquer atividade do Target possa ser entregue pelo Platform Web SDK.

Para configurar o Target na sequência de dados:

1. Vá para a interface [Coleção de dados](https://experience.adobe.com/#/data-collection){target="blank"}
1. Na navegação à esquerda, selecione **[!UICONTROL Datastreams]**
1. Selecionar a sequência de dados `Luma Web SDK: Development Environment` criada anteriormente

   ![Selecione a sequência de dados do Luma Web SDK](assets/datastream-luma-web-sdk-development.png)

1. Selecione **[!UICONTROL Adicionar Serviço]**
   ![Adicionar um serviço à sequência de dados](assets/target-datastream-addService.png)
1. Selecione **[!UICONTROL Adobe Target]** como o **[!UICONTROL Serviço]**
1. Insira os detalhes opcionais sobre a implementação do Target, se desejado, seguindo as orientações abaixo.
1. Selecione **[!UICONTROL Salvar]**

   ![Configuração da sequência de dados de destino](assets/target-datastream.png)

### Token de propriedade

Os clientes do Target Premium têm a opção de gerenciar permissões de usuário com propriedades. As propriedades do Target permitem que você estabeleça limites em torno de onde os usuários podem executar atividades do Target. Consulte a seção [Permissões empresariais](https://experienceleague.adobe.com/pt-br/docs/target/using/administer/manage-users/enterprise/properties-overview) da documentação do Target para obter detalhes.

Para configurar ou localizar tokens de propriedade, navegue até **Adobe Target** > **[!UICONTROL Administração]** > **[!UICONTROL Propriedades]**. O ícone `</>` exibe o código de implementação. O valor `at_property` é o token de propriedade que você usaria na sequência de dados.

![Token de propriedade de destino](assets/target-admin-properties.png)

<a id="advanced-pto"></a>

Somente um token de propriedade pode ser especificado por sequência de dados, mas as substituições de token de propriedade permitem que você especifique tokens de propriedade alternativos para substituir o token de propriedade primária definido na sequência de dados. Uma atualização para a ação `sendEvent` também é necessária para substituir a sequência de dados.

![Lista de identidades](assets/advanced-property-token.png)

### ID do ambiente de destino

[Ambientes](https://experienceleague.adobe.com/pt-br/docs/target/using/administer/environments) no Target ajudam a gerenciar a implementação em todos os estágios de desenvolvimento. Essa configuração opcional especifica qual ambiente do Target você usará com cada fluxo de dados.

A Adobe recomenda definir a ID de ambiente do Target de forma diferente para cada um dos fluxos de dados de desenvolvimento, preparo e produção para simplificar as coisas. Como alternativa, você pode organizar seus ambientes na interface do Target usando o recurso [hosts](https://experienceleague.adobe.com/pt-br/docs/target/using/administer/hosts).

Para configurar ou localizar IDs de Ambiente, navegue até **Adobe Target** > **[!UICONTROL Administração]** > **[!UICONTROL Ambientes]**.

![Ambientes de destino](assets/target-admin-environments.png)

>[!NOTE]
>
>Se nenhuma ID de ambiente de destino for especificada, o ambiente de produção do Target será considerado.

### Namespace de ID de terceiros do Target

Essa configuração opcional permite especificar qual símbolo de identidade usar para a ID de terceiros do Target. O Target só oferece suporte à sincronização de perfis em um único símbolo de identidade ou namespace. Para obter mais informações, consulte a seção [Sincronização de perfil em tempo real para mbox3rdPartyId](https://experienceleague.adobe.com/pt-br/docs/target/using/audiences/visitor-profiles/3rd-party-id) do guia do Target.

Os Símbolos de Identidade foram encontrados na lista de identidades em **Coleção de Dados** > **[!UICONTROL Cliente]** > **[!UICONTROL Identidades]**.

![Lista de identidades](assets/target-identities.png)

Para os propósitos deste tutorial usando o site Luma, use o Símbolo de Identidade `lumaCrmId` configurado durante a lição sobre [Identidades](configure-identities.md).




## Renderizar decisões de personalização visual

As decisões de personalização visual se referem às experiências criadas no Visual Experience Composer do Adobe Target. Primeiro, você deve entender a terminologia usada nas interfaces do Target e das tags:

* **Atividade**: um conjunto de experiências direcionadas a um ou mais públicos-alvo. Por exemplo, um teste A/B simples pode ser uma atividade com duas experiências.
* **Experiência**: um conjunto de ações direcionadas a um ou mais locais ou escopos de decisão.
* **Escopo de decisão**: um local onde uma experiência do Target é entregue. Os escopos de decisão são equivalentes às &quot;mboxes&quot; se você estiver familiarizado com o uso de versões mais antigas do Target.
* **Decisão do Personalization**: uma ação que o servidor determina que deve ser aplicada. Essas decisões podem ser baseadas nos critérios de público-alvo e na priorização de atividades do Target.
* **Proposta**: o resultado das decisões tomadas pelo servidor, que são entregues na resposta do Platform Web SDK. Por exemplo, trocar uma imagem de banner seria uma proposta.

### Atualizar a ação [!UICONTROL Enviar evento]

As decisões de personalização visual do Target são entregues pela Platform Web SDK, se o Target estiver ativado na sequência de dados. No entanto, _eles não são renderizados automaticamente_. Você deve atualizar a ação [!UICONTROL Enviar evento] para habilitar a renderização automática.

1. Na interface da [Coleção de dados](https://experience.adobe.com/#/data-collection){target="blank"}, abra a propriedade de marca que você está usando para este tutorial
1. Abrir a regra `all pages - library loaded - send event - 50`
1. Selecionar a ação `Adobe Experience Platform Web SDK - Send event`
1. Habilitar **[!UICONTROL Renderizar decisões de personalização visual]** com a caixa de seleção

   ![Habilitar renderização de decisões de personalização visual](assets/target-rule-enable-visual-decisions.png)

<!--
1. In the **[!UICONTROL Datastream configuration overrides**] the **[!UICONTROL Target Property Token]** can be overridden either as a static value or with a data element. Only property tokens defined in the [**Advanced Property Token Overrides**](#advanced-pto) section in **Datastream Configuration** will return results.
   
   ![Override the Property Token](assets/target-property-token-ovrrides.png)
   -->

1. Salve as alterações e crie na biblioteca

A configuração de renderizar decisões de personalização visual faz com que o Platform Web SDK aplique automaticamente quaisquer modificações que tenham sido especificadas usando o Visual Experience Composer do Target ou &quot;mbox global&quot;.

>[!NOTE]
>
>Normalmente, a configuração [!UICONTROL Renderizar decisões de personalização visual] só deve ser habilitada para uma única ação Enviar Evento por carregamento de página completo. Se várias ações Enviar evento tiverem essa configuração ativada, as solicitações de renderização subsequentes serão ignoradas.

Se preferir renderizar ou executar ações nessas decisões usando o código personalizado, você pode deixar a configuração [!UICONTROL Renderizar decisões de personalização visual] desabilitada. O Platform Web SDK é flexível e oferece esse recurso para fornecer controle total. Consulte o manual para obter mais informações sobre [renderização manual de conteúdo personalizado](https://experienceleague.adobe.com/pt-br/docs/experience-platform/edge/personalization/rendering-personalization-content).


### Configurar uma atividade do Target com o Visual Experience Composer

Agora que a parte de implementação básica foi concluída, crie uma atividade de Direcionamento de experiência (XT) no Target para validar se tudo está funcionando corretamente. Você pode consultar o tutorial do Target para [criação de atividades de Direcionamento de experiência](https://experienceleague.adobe.com/pt-br/docs/target-learn/tutorials/activities/create-experience-targeting-activities) se precisar de ajuda.

>[!NOTE]
>
>Se você estiver usando o Google Chrome como navegador, a [extensão de ajuda do Visual Experience Composer (VEC)](https://experienceleague.adobe.com/pt-br/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension) será necessária para carregar o site corretamente para edição no VEC.

1. Navegar até a interface do Adobe Target
1. Crie uma atividade de Direcionamento de experiência (XT) usando a página inicial do Luma para o URL da atividade

   ![Criar uma nova atividade de XT](assets/target-xt-create-activity.png)

1. Modifique a página, por exemplo, altere o texto no banner principal da página inicial.  Quando terminar, selecione **[!UICONTROL Salvar]** e depois **[!UICONTROL Avançar]**.

   ![Modificação do VEC do Target](assets/target-xt-vec-modification.png)

1. Atualize o nome do evento e selecione **[!UICONTROL Próximo]**.

   ![Evento de atualização do VEC do Target](assets/target-xt-vec-updateevent.png)

1. Escolha Adobe Analytics como fonte de relatórios com o conjunto de relatórios apropriado e a métrica Pedidos como meta

   ![Fonte de relatórios do VEC do Target](assets/target-xt-vec-reportingsource.png)

   >[!NOTE]
   >
   >Se você não usar o Adobe Analytics, selecione Target como fonte de relatórios e escolha uma métrica diferente como **Envolvimento > Exibições de página**. Uma métrica de meta é necessária para salvar e visualizar a atividade.

1. Salvar a atividade
1. Se você estiver confortável com as alterações, será possível ativar a atividade. Caso contrário, se você quiser visualizar a experiência sem ativá-la, poderá copiar a [URL de Visualização do Controle de Qualidade](https://experienceleague.adobe.com/pt-br/docs/target/using/activities/activity-qa/activity-qa).
1. Carregue a página inicial do Luma e você deverá ver suas alterações aplicadas
1. Após algumas horas, você poderá ver os dados e as conversões da atividade do Target no Adobe Analytics. Consulte o Guia do Target para obter informações detalhadas sobre os [relatórios do Analytics for Target (A4T)](https://experienceleague.adobe.com/pt-br/docs/target/using/integrate/a4t/reporting).



### Validar com o Debugger

Se você configurar uma atividade, verá seu conteúdo renderizado na página. No entanto, mesmo se nenhuma atividade estiver ativa, você também pode examinar a chamada de rede Enviar evento para confirmar se o Target está configurado corretamente.

>[!CAUTION]
>
>Se você estiver usando o Google Chrome e tiver a [extensão de ajuda do Visual Experience Composer (VEC)](https://experienceleague.adobe.com/pt-br/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension) instalada, verifique se a configuração **Inserir bibliotecas do Target** está desativada. Ativar essa configuração resultará em solicitações adicionais do Target.

1. Abra a extensão do navegador Adobe Experience Platform Debugger
1. Vá para o [site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html) e use o depurador para [alternar a propriedade da marca no site para sua própria propriedade de desenvolvimento](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. Recarregar a página
1. Selecione a ferramenta **[!UICONTROL Rede]** no depurador
1. Filtrar por **[!UICONTROL Experience Platform Web SDK]**
1. Selecionar o valor na linha de eventos para a primeira chamada

   ![Chamada de rede no Adobe Experience Platform Debugger](assets/target-debugger-network.png)

1. Observe que há chaves em `query` > `personalization` e `decisionScopes` tem um valor de `__view__`. Este escopo é equivalente ao `target-global-mbox`. Esta chamada do Platform Web SDK solicitou decisões do Target.

   ![`__view__` solicitação de decisionScope](assets/target-debugger-view-scope.png)

1. Feche a sobreposição e selecione os detalhes do evento para a segunda chamada de rede. Esta chamada só estará presente se o Target retornar uma atividade.
1. Observe que há detalhes sobre a atividade e a experiência retornadas do Target. Essa chamada do Platform Web SDK envia uma notificação de que uma atividade do Target foi renderizada para o usuário e aumenta uma impressão.

   ![Impressão da atividade do público alvo](assets/target-debugger-activity-impression.png)

## Configurar e renderizar um escopo de decisão personalizado

Escopos de decisão personalizados (conhecidos formalmente como &quot;mboxes&quot;) podem ser usados para fornecer conteúdo HTML ou JSON de maneira estruturada usando o Experience Composer baseado em formulário do Target. O conteúdo entregue a um desses escopos personalizados não é renderizado automaticamente pelo Platform Web SDK. Ele pode ser renderizado usando uma ação em Tags.

### Adicionar um escopo à [!UICONTROL ação Enviar evento]

Modifique sua regra de carregamento de página para adicionar um escopo de decisão personalizado:

1. Abrir a regra `all pages - library loaded - send event - 50`
1. Selecionar a ação `Adobe Experience Platform Web SDK - Send Event`
1. Adicione um ou mais escopos que deseja usar. Neste exemplo, use `homepage-hero`.

   ![Escopo personalizado](assets/target-rule-custom-scope.png)

1. Salve as alterações e crie na biblioteca

>[!TIP]
>
>Neste tutorial, você usará um único escopo definido manualmente para fins de demonstração. Se você decidir usar vários escopos de decisão destinados a páginas específicas, considere usar um elemento de dados que retorne uma matriz de escopos condicionalmente, dependendo do caminho da página. Essa abordagem ajuda a manter sua implementação simples e escalável.

### Processar a resposta do Target

Agora que você configurou o Platform Web SDK para solicitar conteúdo para o escopo `homepage-hero`, você deve fazer algo com a resposta. A extensão de marca do Platform Web SDK fornece um evento [!UICONTROL Enviar evento concluído], que pode ser usado para acionar imediatamente uma nova regra quando uma resposta de uma ação [!UICONTROL Enviar evento] for recebida.

1. Crie uma regra chamada `homepage - send event complete - render homepage-hero`.
1. Adicione um evento à regra. Use a extensão **Adobe Experience Platform Web SDK** e o tipo de evento **[!UICONTROL Enviar evento concluído]**.
1. Adicione uma condição para restringir a regra à página inicial do Luma (caminho sem cadeia de caracteres de consulta igual a `/content/luma/us/en.html`).
1. Adicione uma ação à regra. Use a extensão **Adobe Experience Platform Web SDK** e o tipo de ação **Aplicar propostas**.

   ![Renderizar regra herói da página inicial](assets/target-rule-render-hero.png)

   >[!TIP]
   >
   >Dê nomes descritivos aos eventos, condições e ações da regra em vez de usar os nomes padrão. Nomes robustos de componentes de regras tornam os resultados da pesquisa muito mais úteis.

1. Insira `%event.propositions%` no campo Propostas, pois estamos usando o evento &quot;Enviar evento concluído&quot; como acionador para esta regra.
1. Na seção &quot;proposition metadata&quot;, selecione **[!UICONTROL Usar um formulário]**
1. Para a entrada de campo **[!UICONTROL do]** Escopo`homepage-hero`
1. Para a entrada de campo **[!UICONTROL do]** Seletor`div.heroimage`
1. Em **[!UICONTROL Tipo de Ação]**, selecione **[!UICONTROL Definir HTML]**
1. Selecione **[!UICONTROL Manter alterações]**

   ![Renderizar ação de herói da página inicial](assets/target-action-render-hero.png)

   Além de renderizar a atividade, você deve fazer uma chamada adicional para o Target para indicar que a atividade baseada em formulário foi renderizada:

1. Adicione outra ação à regra. Usar a extensão **Core** e o tipo de ação **[!UICONTROL Código personalizado]**:
1. Cole o seguinte código JavaScript:

   ```javascript
   var propositions = event.propositions;
   var heroProposition;
   if (propositions) {
      // Find the hero proposition, if it exists.
      for (var i = 0; i < propositions.length; i++) {
         var proposition = propositions[i];
         if (proposition.scope === "homepage-hero") {
            heroProposition = proposition;
            break;
         }
      }
   }
   // Send a "display" event
   if (heroProposition !== undefined){
      alloy("sendEvent", {
         xdm: {
            eventType: "display",
            _experience: {
               decisioning: {
                  propositions: [{
                     id: heroProposition.id,
                     scope: heroProposition.scope,
                     scopeDetails: heroProposition.scopeDetails
                  }]
               }
            }
         }
      });
   }
   ```

   ![Renderizar ação de herói da página inicial](assets/target-action-fire-display.png)

1. Selecione **[!UICONTROL Manter alterações]**

1. Salve as alterações e crie na biblioteca
1. Carregue a página inicial do Luma algumas vezes, o que deve ser suficiente para fazer o novo registro de escopo de decisão `homepage-hero` na interface do Target.





### Configurar uma atividade do Target com o Experience Composer baseado em formulário

Agora que você tem uma regra para renderizar manualmente um escopo de decisão personalizado, pode criar outra atividade de Direcionamento de experiência (XT) no Target. Desta vez, use o Experience Composer baseado em formulário.

1. Abrir [Adobe Target](https://experience.adobe.com/target)
1. Desativar a atividade usada para a lição anterior
1. Crie uma atividade de Direcionamento de experiência (XT) usando a opção Experience Composer baseado em formulário

   ![Criar uma nova atividade de XT](assets/target-xt-create-form-activity.png)

1. Selecione o local **`homepage-hero`** na lista suspensa de locais e **[!UICONTROL Criar oferta do HTML]** na lista suspensa de conteúdo. Se a localização não estiver disponível, você poderá digitá-la. O Target preenche periodicamente novos nomes de locais depois de receber solicitações para esse local ou escopo.

   ![Criar uma nova atividade de XT](assets/target-xt-form-activity.png)

1. Cole o código a seguir na caixa de conteúdo. Este código é um banner principal básico com uma imagem de fundo diferente:

   ```html
   <div class="we-HeroImage jumbotron" style="background-image: url('/content/luma/us/en/women/_jcr_content/root/hero_image.coreimg.jpeg');">
      <div class="container cq-dd-image">
         <div class="we-HeroImage-wrapper">
            <p class="h3">New Luma Yoga Collection</p>
            <strong class="we-HeroImage-title h1">Be active with style&nbsp;</strong>
            <p>
               <a class="btn btn-primary btn-action" href="/content/luma/us/en/products.html" role="button">Shop Now</a>
            </p>
         </div>
      </div>
   </div>
   ```

1. Na etapa [!UICONTROL Metas e configurações], escolha Adobe Target como fonte de relatórios e [!UICONTROL Envolvimento] > [!UICONTROL Exibições de página] como meta
1. Salvar a atividade
1. Se você estiver confortável com as alterações, será possível ativar a atividade. Caso contrário, se você quiser visualizar a experiência sem ativá-la, poderá copiar a [URL de Visualização do Controle de Qualidade](https://experienceleague.adobe.com/pt-br/docs/target/using/activities/activity-qa/activity-qa).
1. Carregue a página inicial do Luma e você deverá ver suas alterações aplicadas

>[!NOTE]
>
>A meta de conversão &quot;Clicou na mbox&quot; não funciona automaticamente. Como o Platform Web SDK não renderiza automaticamente escopos personalizados, ele não rastreia cliques em locais escolhidos para aplicar o conteúdo. Você pode criar seu próprio rastreamento de cliques para cada escopo usando o `eventType` de &quot;clique&quot; com os detalhes do `_experience` aplicáveis usando a ação `sendEvent`.

### Validar com o Debugger

Se você ativou sua atividade, deve ver a renderização do conteúdo na página. No entanto, mesmo se nenhuma atividade estiver ativa, você também pode consultar a chamada de rede [!UICONTROL Enviar Evento] para confirmar se o Target está solicitando conteúdo para seus escopos personalizados.

1. Abra a extensão do navegador do Adobe Experience Platform Debugger
1. Vá para o [site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html) e use o depurador para [alternar a propriedade da marca no site para sua própria propriedade de desenvolvimento](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. Recarregar a página
1. Selecione a ferramenta **[!UICONTROL Rede]** no Depurador
1. Filtrar por **[!UICONTROL Adobe Experience Platform Web SDK]**
1. Selecionar o valor na linha de eventos para a primeira chamada

   ![Chamada de rede no Adobe Experience Platform Debugger](assets/target-debugger-network.png)

1. Observe que há chaves em `query` > `personalization` e `decisionScopes` tem um valor de `__view__` como antes, mas agora também há um escopo `homepage-hero` incluído. Esta chamada do Platform Web SDK solicitou decisões do Target para alterações feitas usando o VEC e o local `homepage-hero` específico.

   ![`__view__` solicitação de decisionScope](assets/target-debugger-view-custom-scope.png)

1. Feche a sobreposição e selecione os detalhes do evento para a segunda chamada de rede. Esta chamada só estará presente se o Target retornar uma atividade.
1. Observe que há detalhes sobre a atividade e a experiência retornadas do Target. Essa chamada do Platform Web SDK envia uma notificação de que uma atividade do Target foi renderizada para o usuário e aumenta uma impressão. Ela foi iniciada pela ação de código personalizado que você adicionou anteriormente.

   ![Impressão da atividade do público alvo](assets/target-debugger-activity-impression.png)

## Enviar parâmetros para o Target

Nesta seção, você passará dados específicos do Target e examinará em mais detalhes como os dados XDM são mapeados para parâmetros do Target.

### Parâmetros de página (mbox) e XDM

Todos os campos XDM são automaticamente passados para o Target como [parâmetros de página](https://experienceleague.adobe.com/pt-br/docs/target-dev/developer/implementation/methods/page-parameters) ou parâmetros de mbox.

Alguns desses campos XDM serão mapeados para objetos especiais no back-end do Target. Por exemplo, o `web.webPageDetails.URL` estará automaticamente disponível para criar condições de direcionamento baseadas em URL ou como o objeto `page.url` ao criar scripts de perfil.

Você também pode adicionar parâmetros de página usando o objeto de dados.

### Parâmetros especiais e o objeto de dados

Há alguns pontos de dados que podem ser úteis para o Target que não são mapeados a partir do objeto XDM. Estes parâmetros especiais do Target incluem:

* [Atributos do perfil](https://experienceleague.adobe.com/pt-br/docs/target-dev/developer/implementation/methods/in-page-profile-attributes)
* [Atributos de entidade do Recommendations](https://experienceleague.adobe.com/pt-br/docs/target/using/recommendations/entities/entity-attributes)
* [Parâmetros reservados do Recommendations](https://experienceleague.adobe.com/pt-br/docs/target/using/recommendations/plan-implement#pass-behavioral)
* Valores de categoria para [afinidade de categorias](https://experienceleague.adobe.com/pt-br/docs/target/using/audiences/visitor-profiles/category-affinity)

Esses parâmetros devem ser enviados no objeto `data` em vez de no objeto `xdm`. Além disso, os parâmetros de página (ou mbox) também podem ser incluídos no objeto `data`.

Para preencher o objeto de dados, crie o seguinte elemento de dados, reutilizando elementos de dados criados na lição [Criar elementos de dados](create-data-elements.md):

* **`data.content`** usando o seguinte código personalizado:

  ```javascript
  var data = {
     __adobe: {
        target: {
           "entity.id": _satellite.getVar("product.productInfo.sku"),
           "entity.name": _satellite.getVar("product.productInfo.title"),
           "profile.loggedIn": _satellite.getVar("user.profile.attributes.loggedIn"),
           "user.categoryId": _satellite.getVar("product.category")
        }
     }
  }
  return data;
  ```



### Atualizar a regra de carregamento da página

Transmitir dados adicionais para o Target fora do objeto XDM requer a atualização de todas as regras aplicáveis. Para este exemplo, a única modificação que você deve fazer é incluir o novo elemento de dados **data.content** na regra de carregamento de página genérica e na regra de exibição de página do produto.

1. Abrir a regra `all pages - library loaded - send event - 50`
1. Selecionar a ação `Adobe Experience Platform Web SDK - Send event`
1. Adicionar o elemento de dados `data.content` ao campo de dados

   ![Adicionar dados de destino à regra](assets/target-rule-data.png)

1. Salve as alterações e crie na biblioteca

>[!NOTE]
>
>O exemplo acima usa um objeto `data` que não está completamente preenchido em todos os tipos de página. As tags lidam adequadamente com essa situação e omitem chaves com valor indefinido. Por exemplo, `entity.id` e `entity.name` não seriam passados em nenhuma página além dos detalhes do produto.


## Divisão de solicitações do Personalization e do Analytics

A camada de dados no site Luma é completamente definida antes do código incorporado das tags. Isso nos permite usar uma única chamada para buscar conteúdo personalizado (por exemplo, do Adobe Target) e enviar dados de análise (por exemplo, para o Adobe Analytics).

No entanto, em muitos sites, a camada de dados não pode ser carregada com antecedência suficiente ou rapidez suficiente para usar uma única chamada para ambos os aplicativos. Nessas situações, você pode usar duas ações [!UICONTROL Enviar evento] em um único carregamento de página e usar a primeira para personalização e a segunda para análise. Separar os eventos dessa maneira permite que o evento de personalização seja acionado o mais rápido possível, enquanto aguarda que a camada de dados seja carregada completamente antes de enviar o evento do Analytics. Isso é semelhante a muitas implementações pré-Web do SDK, onde o Adobe Target acionaria o `target-global-mbox` na parte superior da página e o Adobe Analytics acionaria a chamada `s.t()` na parte inferior da página

Para criar a solicitação de personalização integrada:

1. Abrir a regra `all pages - library loaded - send event - 50`
1. Abrir a ação **Enviar evento**
1. Selecione **[!UICONTROL Usar eventos guiados]** e **[!UICONTROL Solicitar personalização]**
1. Isso bloqueia o **Tipo** como **[!UICONTROL Busca de apresentação de decisão]**

   ![send_decision_request_alone](assets/target-decision-request.png)

Para criar a solicitação do Analytics na parte inferior:

1. Crie uma nova regra chamada `all pages - page bottom - send event - 50`
1. Adicione um evento à regra. Usar a extensão **Core** e o tipo de evento **[!UICONTROL Page Bottom]**
1. Adicione uma ação à regra. Usar a extensão **Adobe Experience Platform Web SDK** e o tipo de ação **Enviar evento**
1. Selecione **[!UICONTROL Usar eventos guiados]** e **[!UICONTROL Coletar análises]**
1. Isso bloqueia a caixa de seleção **[!UICONTROL Incluir notificações de exibição pendentes]** selecionada para que a notificação de exibição em fila da solicitação de decisão seja enviada.

![send_decision_request_alone](assets/target-aa-request-guided.png)

>[!TIP]
>
>Se o evento para o qual você está buscando uma Proposta de decisão não tiver um evento do Adobe Analytics seguindo-o, use o **Estilo de evento guiado** **[!UICONTROL Não guiado - mostrar todos os campos]**. Você precisará selecionar todas as opções manualmente, mas isso desbloqueia a opção de **[!UICONTROL enviar automaticamente uma notificação de exibição]** junto com a solicitação de busca.


### Validar com o Debugger

Agora que as regras foram atualizadas, você pode validar se os dados estão sendo passados corretamente usando o Adobe Debugger.

1. Navegue até o [site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html) e faça logon com o email `test@test.com` e a senha `test`
1. Navegar até a página de detalhes do produto
1. Abra a extensão de navegador do Adobe Experience Platform Debugger e [alterne a propriedade da marca para sua própria propriedade de desenvolvimento](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. Recarregar a página
1. Selecione a ferramenta **Rede** no Depurador e filtre pela **Adobe Experience Platform Web SDK**
1. Selecionar o valor na linha de eventos para a primeira chamada
1. Observe que há chaves em `data` > `__adobe` > `target` e elas são preenchidas com informações sobre o produto, a categoria e o estado de logon.

   ![`__view__` solicitação de decisionScope](assets/target-debugger-data.png)

### Validar na interface do Target

Em seguida, examine a interface do Target para confirmar se os dados foram recebidos e estão disponíveis para uso em públicos-alvo e atividades. Os dados do XDM são mapeados automaticamente para parâmetros do Target personalizados. Você pode validar se os dados XDM foram recebidos pelo Target e estão disponíveis ao criar um público-alvo.

1. Abrir [Adobe Target](https://experience.adobe.com/target)
1. Navegue até a seção **[!UICONTROL Públicos-alvo]**
1. Crie um público e escolha o tipo de atributo **[!UICONTROL Personalizado]**
1. Pesquisar o campo **[!UICONTROL Parâmetro]** para `web`. O menu suspenso deve ser preenchido com todos os campos XDM relacionados aos detalhes da página da Web.

   ![Validar no atributo personalizado de Destino](assets/validate-in-target-customattribute.png)

Em seguida, valide se o atributo de perfil de estado de logon foi passado com êxito.

1. Escolha o tipo de atributo **[!UICONTROL Perfil do visitante]**
2. Pesquisar por `loggedIn`. Se o atributo estiver disponível no menu suspenso, o atributo foi passado corretamente para o Target. Novos atributos podem levar vários minutos para serem disponibilizados na interface do usuário do Target.

   ![Validar no perfil de Destino](assets/validate-in-target-profile.png)

Se você tiver o Target Premium, também poderá validar se os dados da entidade foram passados corretamente e se os dados do produto foram gravados no catálogo de produtos do Recommendations.

1. Navegue até a seção **[!UICONTROL Recommendations]**
1. Selecione **[!UICONTROL Pesquisa no catálogo]** na navegação à esquerda
1. Procure o SKU do produto ou o nome do produto que você visitou anteriormente no site Luma. O produto deve ser exibido no catálogo de produtos. Os novos produtos podem levar vários minutos para se tornarem pesquisáveis no catálogo de produtos do Recommendations.

   ![Validar na pesquisa do catálogo de destino](assets/validate-in-target-catalogsearch.png)

### Validar com o Assurance

Além disso, você pode usar o Assurance quando apropriado para confirmar que as solicitações de decisão do Target estão obtendo os dados corretos e que qualquer transformação do lado do servidor está ocorrendo corretamente. Você também pode confirmar se as informações de campanha e experiência estão contidas nas chamadas do Adobe Analytics, mesmo quando as chamadas de decisão e do Adobe Analytics do Target são enviadas separadamente.

1. Abrir [Assurance](https://experience.adobe.com/assurance)
1. Inicie uma nova sessão do assurance, insira o **[!UICONTROL nome da sessão]** e insira a **[!UICONTROL url base]** para o site ou qualquer outra página que você esteja testando
1. Clique em **[!UICONTROL Avançar]**

   ![Validar na nova sessão de garantia](assets/validate-in-assurance-newsession.png)

1. Selecione o método de conexão. Nesse caso, usaremos **[!UICONTROL copiar link]**
1. Copiar o link e colá-lo em uma nova guia do navegador
1. Clique em **[!UICONTROL Concluído]**

   ![Validar na conexão de garantia por link de cópia](assets/validate-in-assurance-copylink.png)

1. Depois que a sessão do Assurance for iniciada, você verá os eventos serem preenchidos na guia Eventos
1. Filtrar por &quot;tnta&quot;
1. Selecione a chamada mais recente e expanda as mensagens para garantir que esteja preenchendo corretamente e observe os valores de &quot;tnta&quot;

   ![Validar em Ocorrência de Destino de garantia](assets/validate-in-assurance-targetevent.png)

1. Em seguida, mantenha o filtro &quot;tnta&quot; e selecione o evento analytics.mapping que ocorre após o evento de destino que acabamos de visualizar.
1. Examine o &quot;context.mappedQueryParams.Valor \&lt;yourSchemaName\>&quot; para confirmar que contém um atributo &quot;tnta&quot; com uma string concatenada que corresponde aos valores &quot;tnta&quot; encontrados no evento de destino anterior.

   ![Validar com garantia na ocorrência do Analytics](assets/validate-in-assurance-analyticsevent.png)

Isso confirma que as informações do A4T que estavam na fila para transmissão posterior quando fizemos a chamada do Target Decisioning foram enviadas corretamente quando a chamada de rastreamento do Analytics foi acionada posteriormente na página.

Agora que concluiu esta lição, você deve ter uma implementação funcional do Adobe Target usando a Platform Web SDK.

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [postagem de discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=pt)
