---
title: Implementar o consentimento com uma plataforma de gerenciamento de consentimento (CMP)
description: Saiba como implementar e ativar dados de consentimento obtidos de uma Plataforma de gerenciamento de consentimento (CMP) usando a extensão Adobe Experience Platform Web SDK na Coleta de dados.
feature: Web SDK, Tags
role: Developer, Data Engineer
doc-type: tutorial
exl-id: bee792c3-17b7-41fb-a422-289ca018097d
source-git-commit: 951987c5c360aca005c78a976a6090d088f36455
workflow-type: tm+mt
source-wordcount: '3323'
ht-degree: 2%

---

# Implementar o consentimento com uma plataforma de gerenciamento de consentimento (CMP) usando a extensão SDK da Web da plataforma

Muitas regulamentações legais de privacidade introduziram requisitos de consentimento ativo e específico quando se trata de coleta de dados, personalização e outros casos de uso de marketing. Para atender a esses requisitos, o Adobe Experience Platform permite capturar informações de consentimento em perfis de clientes individuais e usar essas preferências como um fator determinante na forma como os dados de cada cliente são usados em workflows da plataforma downstream.

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo integrado à Adobe Experience Platform como um conjunto de tecnologias de coleção de dados. Várias alterações de terminologia foram implementadas na interface de que você deve estar ciente ao usar este conteúdo:
>
> * O Platform launch (lado do cliente) agora está **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)**
> * Agora o lado do servidor do Platform launch **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * As configurações de borda agora são **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=pt-BR)**


Este tutorial demonstra como implementar e ativar dados de consentimento obtidos de uma Plataforma de gerenciamento de consentimento (CMP) usando a extensão SDK da Web da plataforma na Coleta de dados. Faremos isso usando os padrões do Adobe e o padrão de consentimento do IAB TCF 2.0, com o OneTrust ou Sourcepoint como CMPs de exemplo.

Este tutorial usa a extensão SDK da Web da plataforma para enviar dados de consentimento para a Plataforma. Para obter uma visão geral do SDK da Web, consulte [esta página](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=pt-BR).

## Pré-requisitos

Os pré-requisitos para usar o SDK da Web estão listados [here](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/prerequisite.html#fundamentals).

Nessa página, há um requisito para um &quot;Conjunto de dados do evento&quot; e, como parece, esse é um conjunto de dados para manter os dados do evento da experiência. Para enviar informações de consentimento com eventos, a variável [Detalhes do consentimento da TCF do IAB 2.0](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/iab/dataset.html) O grupo de campos precisa ser adicionado ao esquema Evento de experiência:

![](./images/event-schema.png)

Para o padrão de consentimento da plataforma v2.0, também precisaremos acessar o Adobe Experience Platform para criar um esquema de Perfil individual e um conjunto de dados XDM. Para obter um tutorial sobre a criação de schema, consulte [Criar um esquema usando o Editor de esquemas](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html#tutorials) e para o grupo de campos Consentimento e Detalhes de Preferência necessário, consulte [Configurar um conjunto de dados para capturar dados de consentimento e preferência](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/adobe/dataset.html).

Este tutorial pressupõe que você tenha acesso à Coleta de dados e criou uma propriedade de Tags do lado do cliente com a extensão do SDK da Web instalada e uma biblioteca de trabalho criada e criada para desenvolvimento. Estes tópicos são detalhados e demonstrados nestes documentos:

* [Criar ou configurar uma propriedade](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html?lang=en#create-or-configure-a-property)
* [Visão geral das bibliotecas](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/libraries.html)
* [Visão geral da publicação](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html?lang=pt-BR)

Também usaremos o [Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) Extensão do Chrome para inspecionar e validar nossa implementação.

Para implementar o exemplo da TCF do IAB com uma CMP em seu próprio site, você precisará acessar uma CMP como OneTrust ou Sourcepoint para gerar os dados que eles fornecem, ou você pode simplesmente acompanhar aqui e ver os resultados abaixo.

## Uso do SDK da Web com o Adobe Consent Standard (v1.0 ou v2.0)

>[!NOTE]
>
>O padrão 1.0 está sendo distribuído em favor da v2.0. O padrão 2.0 permite adicionar dados de consentimento adicionais que podem ser usados para impor manualmente as preferências de consentimento. As capturas de tela abaixo da extensão do SDK da Web da plataforma são da versão [2.4.0](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html#version-2.4.0) da extensão que é compatível com v1.0 ou v2.0 do Adobe Consent Standard.

Para obter mais informações sobre esses padrões, consulte [Suporte às preferências de consentimento do cliente](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html).

### Etapa 1: Configurar o consentimento na extensão do SDK da Web

Depois de instalar a extensão SDK da Web da plataforma em uma propriedade de Tags, podemos configurar as opções para endereçar dados de consentimento na tela de configuração de extensão:

![](./images/pending.png)

A seção &quot;Privacidade&quot; define o nível de consentimento para o SDK se o usuário não tiver fornecido preferências de consentimento anteriormente. Isso define o estado padrão para a coleta de dados de consentimento e evento no SDK. A configuração escolhida responde à pergunta &quot;o que o SDK deve fazer se o usuário ainda não tiver fornecido preferências de consentimento explícitas?&quot;

* Em - Colete eventos que ocorrem antes que o usuário forneça preferências de consentimento.
* Out - Solte os eventos que ocorrem antes que o usuário forneça as preferências de consentimento.
* Pendente - eventos da fila que ocorrem antes que o usuário forneça as preferências de consentimento.
* Fornecido pelo elemento de dados

Se a configuração de consentimento padrão for &quot;In&quot;, isso informará ao SDK que ele não deve aguardar por consentimento explícito e deverá coletar os eventos que ocorrem antes que o usuário forneça as preferências de consentimento. Normalmente, essas preferências são manipuladas e armazenadas em um CMP.

Se a configuração de consentimento padrão for &quot;Out&quot;, isso informará ao SDK que ele não deve coletar eventos que ocorram antes que as preferências de aceitação do usuário sejam definidas. A atividade do visitante que ocorre antes de definir a preferência de consentimento não será incluída em nenhum dado enviado pelo SDK depois que o consentimento for definido. Por exemplo, se você rolar e exibir uma página da Web antes de selecionar o banner de consentimento, e essa configuração &quot;Fora&quot; for usada, essa atividade de rolagem e o tempo de exibição não serão enviados se o usuário posteriormente fornecer consentimento explícito para a coleta de dados.

Se a configuração de consentimento padrão for &quot;Pendente&quot;, o SDK colocará em fila todos os eventos que ocorrerem antes de o usuário fornecer preferências de consentimento, de modo que os eventos possam ser enviados depois que as preferências de consentimento forem definidas e depois que o SDK for configurado inicialmente durante uma visita.

Com essa configuração &quot;Pendente&quot;, tentar executar qualquer comando que exija preferências de aceitação do usuário (por exemplo, o comando de evento) resultará na fila do comando no SDK. Esses comandos não são processados até que você comunique as preferências de aceitação do usuário ao SDK.

Depois que uma CMP coleta as preferências do usuário, podemos comunicar essas preferências ao SDK. Em uma seção posterior abaixo, veremos como obter esses dados de opt-in e usá-los com a extensão do SDK da Web.

&quot;Fornecido pelo elemento de dados&quot; nos permite acessar um elemento de dados que contém qualquer dado de preferência de consentimento capturado pelo código personalizado ou por uma CMP em seu site ou na camada de dados. Um elemento de dados usado para essa finalidade deve resolver &quot;in&quot;, &quot;out&quot; ou &quot;pending&quot;.

Observe: essa configuração do SDK não é persistente para os perfis dos usuários, é específica para definir o comportamento do SDK antes que as preferências de consentimento explícito sejam fornecidas pelo visitante.

Para saber mais sobre como configurar a extensão SDK da Web, consulte o [Visão geral da extensão do SDK da Web da plataforma](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/web-sdk-extension-configuration.html?lang=en#configure-the-extension) e [Suporte às preferências de consentimento do cliente](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html).

Neste exemplo, vamos escolher a opção para &quot;Pendente&quot; e selecionar **Salvar** para salvar as configurações.

### Etapa 2: Comunicar preferências de consentimento

Agora que definimos o comportamento padrão do SDK, podemos usar tags para enviar preferências de consentimento explícitas de um visitante para a Platform. O envio de dados de consentimento usando o padrão Adobe 1.0 ou 2.0 é facilmente implementado com o uso da variável `setConsent` do SDK da Web nas regras de tags.

#### Configuração do consentimento com o Platform Consent Standard 1.0

Vamos criar uma regra para demonstrar isso. Na propriedade de tag da Plataforma, selecione Regras, em seguida, no botão azul Adicionar regras . Vamos nomear a Regra como &quot;setAdobeConsent&quot; e selecionar para adicionar um Evento. Para o Tipo de evento, escolha &quot;Janela carregada&quot; que acionará essa regra sempre que uma página for carregada em seu site. Em seguida, em &quot;Ações&quot;, selecione &quot;Adicionar&quot; para abrir a tela de configuração de ação. É aqui que definiremos os dados de consentimento. Selecione a lista suspensa &quot;Extensão&quot; e selecione &quot;SDK da Web da plataforma&quot;, selecione o &quot;Tipo de ação&quot; e selecione &quot;Definir consentimento&quot;.

Em &quot;Informações de consentimento&quot;, escolha &quot;Preencha um formulário&quot;. Nesta ação de regra, usaremos o SDK da Web para definir o consentimento para o padrão de consentimento do Adobe 1.0 preenchendo o formulário exibido:

![](./images/1-0-form.png)

Podemos optar por transmitir &quot;Entrada&quot;, &quot;Saída&quot; ou &quot;Fornecida por elemento de dados&quot; com esta ação Definir consentimento. Um elemento de dados aqui deve resolver como &quot;dentro&quot; ou &quot;fora&quot;.

Neste exemplo, vamos selecionar &quot;In&quot; para indicar que o visitante consentiu em permitir que o SDK da Web envie dados para a Platform. Selecione o botão azul &quot;Manter alterações&quot; para salvar esta ação e, em seguida, &quot;Salvar&quot; para salvar esta regra.

Observação: Depois que um visitante do site rejeitar, o SDK não permitirá que você defina o consentimento dos usuários para o no.

As regras de tags podem ser acionadas por uma variedade de [events](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/core/overview.html) que pode ser usada para transmitir esses dados de consentimento no momento apropriado durante uma sessão de visitante. No exemplo acima, usamos o evento de carregamento de janela para acionar a regra. Em uma seção posterior, usaremos um evento de preferência de consentimento de um CMP para acionar uma ação Definir consentimento. Você pode usar uma ação Definir consentimento em uma regra acionada por qualquer evento que você preferir que indique uma configuração de preferência de aceitação.

#### Configuração do consentimento com o Padrão de consentimento da plataforma 2.0

A versão 2.0 do padrão de consentimento da plataforma funciona com o [XDM](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/schemas-and-experience-data-model.html?lang=pt-BR) dados. Também requer adicionar o grupo de campos Consentimento e Detalhes de preferência ao esquema do perfil no Platform. Consulte [Processamento de consentimento na plataforma](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/adobe/overview.html) para obter mais informações sobre o Adobe standard versão 2.0 e este grupo de campos.

Criaremos um elemento de dados de código personalizado para transmitir dados para as propriedades de coleta e metadados do objeto de consentimentos mostrado no esquema abaixo:

![](./images/collect-metadata.png)

Este grupo de campos Consentimento e Detalhes da Preferência contém campos para o [Consentimentos e preferências tipo de dados XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/data-types/consents.html#prerequisites) que conterão os dados de preferência de consentimento que enviamos para a Platform com a extensão SDK da Web da plataforma em nossa ação de regra. Atualmente, as únicas propriedades necessárias para implementar o Platform Consent Standard 2.0 são o valor de coleta (val) e o valor de tempo dos metadados, realçado acima em vermelho.

Vamos criar um elemento de dados para esses dados. Selecione Elementos de dados e o botão azul Adicionar elemento de dados . Chamaremos isso de &quot;xdm-consent 2.0&quot; e, usando a extensão principal, selecionaremos um tipo de código personalizado. Você pode inserir ou copiar e colar os seguintes dados na janela do editor de código personalizado:

```js
var dateString = new Date().toISOString();

return {
  collect: {
    val: "y"
  },
  metadata: {
    time: dateString
  }
}
```

O campo de hora deve especificar quando o usuário atualizou pela última vez suas preferências de consentimento. Estamos criando um carimbo de data e hora aqui como exemplo usando um método padrão no objeto JavaScript Date . Selecione salvar para salvar o código personalizado e selecione salvar novamente para salvar o elemento de dados.

Em seguida, vamos selecionar Regras, depois o botão azul Adicionar Regra e inserir o nome &quot;setConsent onLoad - Consent 2.0&quot;. Vamos escolher o evento Janela carregada como nosso acionador de regra e, em seguida, selecionar Adicionar em Ações. Escolha a Extensão do SDK da Web da plataforma e, para Tipo de ação, escolha Definir consentimento. O Padrão deve ser Adobe e a Versão deve ser 2.0. Para Valor, usaremos o elemento de dados que acabamos de criar que contém os valores de coleta e de tempo que precisamos enviar para a Plataforma:

![](./images/2-0-form.png)

Para revisar esta ação de exemplo, estamos chamando Definir consentimento da extensão SDK da Web da plataforma e transmitindo o Padrão e a Versão do formulário, enquanto passamos os valores para coleta e hora do elemento de dados criado anteriormente.

Selecione o botão azul Salvar e depois para salvar a regra.

Agora temos duas regras, uma para cada padrão de Consentimento de Plataforma. Na prática, você provavelmente escolherá um padrão em todos os sites. Em seguida, criaremos um exemplo usando o padrão de consentimento do IAB TCF 2.0.

## Uso do SDK da Web com o Padrão de consentimento da TCF do IAB 2.0

Saiba mais sobre a versão 2.0 da Estrutura de transparência e consentimento do IAB no [Site da IAB Europe](https://iabeurope.eu/transparency-consent-framework/).

Para definir os dados de preferência de consentimento usando esse padrão, precisamos adicionar o grupo de campos Detalhes do consentimento da TCF do IAB 2.0 ao nosso schema de Eventos de experiência na Plataforma:

![](./images/consentStrings.png)

Este grupo de campos contém os campos de preferência de consentimento exigidos pelo padrão TCF 2.0 do IAB. Para obter mais informações sobre schemas e grupos de campos, consulte o [Visão geral do sistema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=pt-BR).

### Etapa 1: Criar um elemento de dados de consentimento

Para enviar dados do evento de consentimento das tags usando o padrão de consentimento do IAB TCF 2.0, primeiro configuramos um elemento de dados xdm com os campos de consentimento necessários:

![](./images/data-element.png)

Em suas tags, na propriedade do lado do cliente, selecione Elementos de dados e o botão azul &quot;Adicionar elemento de dados&quot;. Vamos nomear esse elemento de dados como &quot;xdm-consentStrings&quot; para este exemplo. Esses campos xdm conterão os dados de consentimento do usuário necessários para o padrão TCF 2.0 do IAB.

No menu suspenso Extensão , escolha &quot;SDK da Web da plataforma&quot; e, para Tipo de elemento de dados, escolha &quot;Objeto XDM&quot;. O mapeador xdm deve aparecer, permitindo que você selecione e expanda o item &quot;consentStrings&quot;, como mostrado na captura de tela acima.

Definiremos cada uma das sequências de consentimento da seguinte maneira:

* **`consentStandard`**:  `IAB TCF`
* **`consentStandardVersion`**:  `2.0`
* **`consentStringValue`**:  `%IAB TCF Consent String%`
* **`containsPersonalData`**:  `False` (escolhido pelo botão Selecionar valor)
* **`gdprApplies`**:  `%IAB TCF Consent GDPR%`

O `consentStandard` e `consentStandardVersion` ambos os campos são apenas sequências de texto para o padrão que estamos usando, que é a versão 2.0 da TCF do IAB. A variável `consentStringValue` faz referência a um elemento de dados chamado &quot;Cadeia de consentimento da TCF do IAB&quot;. Os sinais de porcentagem ao redor do texto indicam o nome de um elemento de dados, e veremos isso em um momento. O `containsPersonalData` indica se a cadeia de consentimento do IAB TCF 2.0 contém quaisquer dados pessoais com &quot;Verdadeiro&quot; ou &quot;Falso&quot;. O `gdprApplies` indica se &quot;true&quot; para o GDPR se aplica, &quot;false&quot; para o GDPR não se aplica ou &quot;undefined&quot; para desconhecido se o GDPR se aplica. Atualmente, o SDK da Web tratará &quot;undefined&quot; como &quot;true&quot;, portanto, os dados de consentimento enviados com &quot;gdprApplies: &quot;indefinido&quot; será tratado como se o visitante estivesse localizado em uma área em que o GDPR não se aplica.

Consulte a [documentação de consentimento](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/iab-tcf/with-launch.html#getting-started) para obter mais informações sobre essas propriedades e sobre o IAB TCF 2.0 nas tags.

### Etapa 2: Criar uma regra para definir o consentimento com o padrão TCF do IAB 2.0

Em seguida, criamos uma regra para definir o consentimento com o SDK da Web quando os dados de consentimento desse padrão forem definidos ou alterados por um visitante do site. Nesta regra, também veremos como capturar esses sinais de alteração de consentimento de uma CMP como [OneTrust](https://www.onetrust.com/products/cookie-consent/) ou [Sourcepoint](https://www.sourcepoint.com/cmp/).

#### Adicionar um evento de regra

Selecione a seção Regras na propriedade de tag da Plataforma e, em seguida, no botão azul Adicionar regra . Vamos nomear a regra setConsent - IAB e selecionar Adicionar em Eventos. Vamos nomear esse evento tcfapi addEventListener e selecionar Abrir editor para abrir o editor de código personalizado.

Copie e cole o seguinte código na janela do editor:

```js
// Wait for window.__tcfapi to be defined, then trigger when the customer has completed their consent and preferences.
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && (tcData.eventStatus === "useractioncomplete" || tcData.eventStatus === "tcloaded")) {
        // save the tcData.tcString properties in data elements
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF Consent GDPR", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn't defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

Esse código simplesmente cria e executa uma função chamada `addEventListener`. A função verifica se a variável `window.__tcfapi` existe e, se existir, adiciona um ouvinte de evento de acordo com as especificações da API. Você pode ler mais sobre essas especificações no [Acordo de recompra IAB](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework) no GitHub. Se esse ouvinte de evento for adicionado com sucesso e o visitante do site tiver concluído suas opções de consentimento e preferências, o código definirá as tags como variáveis personalizadas para a variável `tcData.tcString`e o indicador para as regiões do GDPR. Novamente, para saber mais sobre a TCF do IAB, consulte o IAB [site](https://iabeurope.eu/transparency-consent-framework/) e [GitHub repo](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework) para obter detalhes técnicos. Após definir esses valores, o código executa a função de acionador que aciona essa regra para ser executada.

Se a variável `window.__tcfapi` não existia na primeira vez que essa função foi executada, a função verificará se ela existe novamente a cada 100 milissegundos, para que o ouvinte do evento possa ser adicionado. A última linha do código simplesmente executa o `addEventListener` definida nas linhas do código acima.

Para resumir, criamos uma função para verificar o status de consentimento que um visitante do site define usando um banner de consentimento CMP (ou personalizado). Quando essa preferência de consentimento é definida, esse código cria duas variáveis personalizadas (elementos de dados de código personalizado) que podem ser usadas na ação de regra. Depois de colar o código acima na janela do editor de código personalizado de nosso evento, selecione o botão azul Salvar para salvar o evento da regra.

Agora vamos configurar a ação Definir regra de consentimento para usar esses valores e enviá-los para a Plataforma.

#### Adicionar uma ação de regra

Selecione Adicionar na seção Ações . Em Extensão, escolha Plataforma Web SDK na lista suspensa. Em Tipo de ação, escolha Definir consentimento. Vamos nomear essa ação como setConsent.

Na configuração da ação, em Informações de consentimento, escolha Preencher um formulário. Para o Standard, escolha IAB TCF e, para Versão, insira 2.0. Para o Valor, usaremos a variável personalizada de nosso evento e inseriremos `%IAB TCF Consent String%` que vem do [tcData](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20CMP%20API%20v2.md#tcdata) capturamos a função personalizada de evento de regra acima.

Em GDPR Aplica-se, usaremos a outra variável personalizada de nosso evento e inseriremos `%IAB TCF Consent GDPR%` que também vem do `tcData` capturamos a função personalizada de evento de regra acima. Se você sabe que o GDPR definitivamente se aplicará a visitantes deste site, você pode selecionar Sim ou Não, conforme aplicável, em vez de usar a opção de variável personalizada (elemento de dados). Você também pode usar a lógica condicional em um elemento de dados para verificar se o GDPR se aplica e retornar o valor apropriado.

Em GDPR Contém dados pessoais, selecione a opção para indicar se os dados desse usuário contêm dados pessoais ou não. Um elemento de dados aqui deve resolver como true ou false.

![](./images/data-element-2-0.png)

Selecione o botão azul Salvar para salvar a ação e o botão azul Salvar (ou Salvar na biblioteca) para salvar a regra. Neste ponto, você implementou com êxito o elemento de dados e a regra nas tags para definir o consentimento usando a extensão SDK da Web com o padrão de consentimento IAB TCF 2.0.

### Etapa 3: Salvar na biblioteca e criar

Se estiver usando o [biblioteca de trabalho](https://experienceleague.adobe.com/docs/launch-learn/implement-in-websites-with-launch/configure-tags/launch-data-elements-rules.html?lang=en#use-the-working-library-feature) pré-requisito, você já salvou essas alterações e criou a biblioteca de desenvolvimento:

![](./images/save-library.png)

### Etapa 4: Inspect e validar a coleta de dados

Em nosso site, atualizamos a página e confirmamos a build da biblioteca no [Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) Extensão do Chrome, na seção de menu de tags:

![](./images/build-date.png)

Também podemos inspecionar a chamada setConsent para os padrões do Adobe 1.0 ou 2.0 na seção do depurador do SDK da Web da Plataforma, selecionando na linha Corpo do POST na solicitação de rede onde você vê `{"consent":[{"value":{"general":"in"},"version…`:

![](./images/inspect-consent-call.png)

Para validar a chamada setConsent e nossa regra para o padrão TCF do IAB 2.0, usaremos o banner de consentimento do OneTrust em nosso site de teste para definir nossas preferências de consentimento e criar o tcData descrito anteriormente:

![](./images/banner.png)

Após selecionar &quot;Aceito&quot;, podemos inspecionar a chamada setConsent para o padrão TCF 2.0 do IAB na seção do SDK da Web da plataforma do depurador, selecionando na linha Corpo do POST na solicitação de rede, onde você vê `{"consent":[{"value":"someAlphaNumericCharacters…`.

![](./images/inspect-2-0.png)

Aqui vemos os dados configurados anteriormente em nossos elementos de dados e na regra de tags. A propriedade value contém os dados codificados tcString que vimos anteriormente.

O OneTrust, o Sourcepoint e outras CMPs que implementam o padrão TCF 2.0 do IAB produzirão dados semelhantes em nossas páginas. Podemos capturar esses dados e usá-los com a extensão do SDK da Web em tags usando o evento de código personalizado na regra criada acima. O código personalizado será o mesmo independentemente da CMP usada para gerar os dados da TCF do IAB 2.0. O código personalizado também pode ser usado com qualquer um dos padrões de Consentimento de plataforma (1.0 ou 2.0).

## Envio de dados de consentimento com eventos de experiência

Você pode ter notado que não referenciamos o elemento de dados &quot;xdm-consentStrings&quot; criado anteriormente em um campo de elemento de dados em qualquer uma de nossas regras. Esse elemento de dados deve ser usado quando for necessário enviar dados de consentimento com um Evento de experiência.

![](./images/consentStrings-data-element.png)

Como esse elemento de dados contém todos os campos necessários para o padrão TCF do IAB 2.0, você pode simplesmente fazer referência ao elemento de dados ao enviar esses dados xdm com seus Eventos de experiência:

![](./images/consentStrings-reference.png)

## Conclusão

Agora que inspecionamos e validamos os dados, você deve ver como implementar e ativar os dados de consentimento obtidos de uma CMP usando a extensão SDK da Web da plataforma para a plataforma.
