---
title: Configurar consentimento com o SDK da Web da plataforma
description: Saiba como definir as configurações de privacidade da extensão de tag do SDK da Web do Experience Platform. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Web SDK,Tags,Consent
exl-id: 502a7467-3699-4b2b-93bf-6b6069ea2090
source-git-commit: aeff30f808fd65370b58eba69d24e658474a92d7
workflow-type: tm+mt
source-wordcount: '1602'
ht-degree: 0%

---

# Configurar consentimento com o SDK da Web da plataforma

Saiba como definir as configurações de privacidade da extensão de tag do SDK da Web do Experience Platform. Defina o consentimento com base na interação do visitante com um banner de uma Plataforma de gerenciamento de consentimento (CMP).

>[!NOTE]
> 
>Para fins de demonstração, este tutorial usa [Klaro](https://heyklaro.com/) como um CMP. Você pode seguir o Klaro ou o CMP usado com seu site.


## Objetivos de aprendizagem

No final desta lição, você poderá:

* Carregar uma CMP usando tags
* Definição das configurações de privacidade na extensão de tag do SDK da Web do Experience Platform
* Definir consentimento para o SDK da Web do Experience Platform com base na ação do visitante

## Pré-requisitos

Você deve estar familiarizado com as tags e as etapas para criar regras, elementos de dados, criar bibliotecas de tags para ambientes e alternar bibliotecas de tags usando o Depurador Experience Platform.

Antes de começar a definir as configurações de privacidade e criar as regras para definir o consentimento, insira o script da plataforma de gerenciamento de consentimento no site e esteja funcionando corretamente. Uma CMP pode ser carregada diretamente no código-fonte com a ajuda de desenvolvedores de site ou carregada por meio de tags. Esta lição demonstra a última abordagem.
>[!NOTE]
> 
>1. Uma Plataforma de gerenciamento de consentimento (ou CMP) é usada pelas organizações para documentar e gerenciar legalmente as opções de consentimento de um visitante antes de coletar, compartilhar ou vender dados do visitante de fontes online, como sites e aplicativos.
>
>2. A abordagem recomendada para inserir um CMP é diretamente por meio do código-fonte, antes do script do gerenciador de tags.

### Configurar o Klaro

Antes de entrar nas configurações de tag, saiba mais sobre a plataforma de gerenciamento de consentimento usada neste tutorial do Klaro.

1. Visita [Klaro](https://heyklaro.com/) e configurar uma conta.
1. Ir para **Gerenciador de privacidade** e crie uma instância de acordo com as instruções.
1. Use o **Código de integração** para injetar Klaro na propriedade da tag (as instruções estão no próximo exercício).
1. Ignorar o **Digitalizando** seção, pois detectará a propriedade da tag, que está codificada no site de demonstração Luma e não aquela que você criou para este tutorial.
1. Adicione um serviço chamado `aep web sdk` e alterne no **Estado padrão do serviço**. Quando ativado, o valor de consentimento padrão é `true`, caso contrário, será `false`. Essa configuração é útil para decidir qual será o estado de consentimento padrão (antes do consentimento do visitante) para o seu aplicativo web. Por exemplo:
   * Para a CCPA, o consentimento padrão geralmente é definido como `true`. Você referenciará esse cenário como **Aceitação implícita** neste tutorial
   * Para o GDPR, o consentimento padrão geralmente é definido como `false`. Você referenciará esse cenário como **Recusa implícita** neste tutorial.

<!--
    This consent value can be verified by returning the JavaScript object ```klaro.getManager().consents``` in the browser's developer console.
-->
    >[!NOTE]
    >
    >Geralmente, as etapas acima mencionadas são realizadas e tratadas pela equipe ou indivíduo responsável por lidar com a CMP, como o OneTrust ou TrustArc.

## Injetar um CMP

>[!WARNING]
>
>A prática recomendada para implementar uma Plataforma de gerenciamento de consentimento é normalmente carregar a CMP _antes_ carregando o gerenciador de tags. Para facilitar este tutorial, você carregará a CMP _com_ o gerenciador de tags. Esta lição foi projetada para mostrar como usar os recursos de consentimento no SDK da Web da Platform e não deve ser usada como guia para configurar corretamente o Klaro ou qualquer outro CMP.


Agora, depois de concluir as configurações do Klaro, crie regras de tag com as seguintes configurações:

* [!UICONTROL Nome]: `all pages - library load - Klaro`
* [!UICONTROL Evento]: [!UICONTROL Biblioteca carregada (início da página)] com [!UICONTROL Opções avançadas] > [!UICONTROL Pedido] defina como 1
* [!UICONTROL Ação]: [!UICONTROL Custom Code], [!UICONTROL Idioma]: HTML para carregar o script CMP.

![Inserir regra CMP](assets/consent-cmp-inject-rule-1.png)

O bloco de código personalizado deve ser semelhante ao seguinte:

![Inserir regra CMP](assets/consent-cmp-inject-rule-2.png)

Agora, salve e crie essa regra na biblioteca de desenvolvimento, valide se o banner de consentimento está sendo exibido ao alternar a biblioteca de tags do site Luma para o seu próprio site. Você deve ver um banner CMP no site, conforme abaixo. E para verificar a permissão de consentimento do visitante atual, você pode usar o seguinte trecho no console do navegador.

```javascript
    klaro.getManager().consents 
```

![Banner de consentimento](assets/consent-cmp-banner.png)

Para entrar no modo de depuração, use a seguinte caixa de seleção no Adobe Experience Platform Debugger.

![Modo de depuração da tag](assets/consent-rule-debugging.png)

Além disso, talvez seja necessário limpar os cookies e o armazenamento local várias vezes ao percorrer este tutorial, pois o valor de consentimento do visitante é armazenado lá. Você pode simplesmente fazer isso conforme abaixo:

![Limpando Armazenamento](assets/consent-clearning-cookies.png)

## Cenários de consentimento

Atos de privacidade como GDPR, CCPA e outros desempenham um papel vital na forma como você arquitetar a implementação do consentimento. Nesta lição, você explora como um visitante pode interagir com o banner de consentimento em dois atos de privacidade mais proeminentes.
![Cenários de consentimento](assets/consent-scenarios.jpeg)


### Cenário 1: aceitação implícita

A aceitação implícita significa que a empresa não precisa obter o consentimento do visitante (ou a &quot;aceitação&quot;) antes de coletar seus dados e, portanto, todos os visitantes do site são tratados como aceitos por padrão. No entanto, o visitante pode recusar rejeitando os cookies por meio do banner de consentimento. Esse caso de uso é semelhante à CCPA.

Agora, você configurará e implementará o consentimento para este cenário:

1. No **[!UICONTROL Privacidade]** da extensão de tag do SDK da Web do Experience Platform, verifique se  **[!UICONTROL Consentimento padrão]** está definida como **[!UICONTROL Entrada]** :


   ![Configuração de privacidade da extensão do AEP de consentimento](assets/consent-web-sdk-privacy-in.png)

   >[!NOTE]
   > 
   >Para uma solução dinâmica, selecione a opção &quot;Fornecer um elemento de dados&quot; e passe um elemento de dados que retorne o valor de ```klaro.getManager().consents```
   >
   >Essa opção é usada se a CMP for injetada no código-fonte *antes* o código incorporado da tag para que o consentimento padrão fique disponível antes que a extensão SDK da Web do Experience Platform comece a ser carregada. No nosso exemplo, não podemos usar essa opção, pois a CMP é carregada com tags e não antes das tags.



2. Salvar e criar essa alteração na biblioteca de tags
3. Carregue sua biblioteca de tags no site de demonstração Luma
4. Ative a depuração de tags no site Luma e recarregue a página. No console do desenvolvedor do seu navegador, você deve ver que defaultConsent é igual a **[!UICONTROL Entrada]**
5. Com essa configuração, a extensão SDK da Web do Experience Platform continua a fazer solicitações de rede, a menos que um visitante decida rejeitar os cookies e recusar:

   ![Consentimento implicado na aceitação](assets/consent-Implied-optin-default.png)



Se um visitante decidir recusar (rejeitar os cookies de rastreamento), você deverá alterar o consentimento para **[!UICONTROL Saída]**. Altere a configuração de consentimento seguindo estas etapas:

<!--
1. Create a data element to store the consent value of the visitor. Let's call it `klaro consent value`. Use the code snippet to create a custom code type data element:
    
    ```javascript
    return klaro.getManager().consents["aep web sdk"]
    ```

    ![Data Element consent value](assets/consent-data-element-value.png)


1. Create another custom code data element, `consent confirmed`, with the following snippet which returns ```true``` only after a visitor confirms consent:

    
    ```javascript
    return klaro.getManager().confirmed
    ```

    ![Data Element consent confirmed](assets/consent-data-element-confirmed.png)
-->

1. Crie uma regra que é acionada quando o visitante clica em **Não aceito**.  Nomear esta regra como: `all pages - click consent banner - set consent "out"`

1. Como a variável **[!UICONTROL Evento]**, use **[!UICONTROL Clique em]** em **[!UICONTROL Elementos que correspondem ao seletor de CSS]** `#klaro .cn-decline`

   ![Condição de regra em que o usuário clica &quot;Não aceito&quot;](assets/consent-optOut-clickEvent.png)

1. Agora, use o SDK da Web do Experience Platform, [!UICONTROL Definir consentimento] [!UICONTROL tipo de ação] para definir o consentimento como &quot;out&quot;:

   ![Ação de recusa da regra de consentimento](assets/consent-rule-optout-action.png)

1. Selecionar **[!UICONTROL Salvar na biblioteca e criar]**:

   ![Salve e crie sua biblioteca](assets/consent-rule-optout-saveAndBuild.png)

Agora, quando um visitante recusa, a regra configurada da maneira acima é acionada e define o consentimento do SDK da Web como **[!UICONTROL Saída]**.

Valide acessando o site de demonstração Luma, rejeite os cookies e confirme se nenhuma solicitação do SDK da Web é acionada após a recusa.

### Cenário 2: recusa implícita


A recusa implícita significa que os visitantes devem ser tratados como recusa por padrão e os cookies não devem ser definidos. As solicitações do SDK da Web não devem ser acionadas, a menos que os visitantes decidam aceitar manualmente aceitando os cookies por meio do banner de consentimento. Talvez seja necessário lidar com esse caso de uso na região da União Europeia onde o GDPR se aplica.

Veja como definir a configuração de um cenário de recusa implícita:

1. Em Klaro, desative a opção **Estado padrão do serviço** no seu `aep web sdk` e salve a configuração atualizada.

1. Entrada **[!UICONTROL Privacidade]** seção da extensão SDK da Web do Experience Platform, defina o consentimento padrão como **[!UICONTROL Saída]** ou **[!UICONTROL Pending]** conforme necessário.

   ![Configuração de privacidade da extensão do AEP de consentimento](assets/consent-implied-opt-out.png)

1. **Salvar** a configuração atualizada na biblioteca de tags e recrie-a.

   Com essa configuração, o SDK da Web do Experience Platform garante que nenhuma solicitação seja acionada, a menos que a permissão de consentimento mude para **[!UICONTROL Entrada]**. Isso pode acontecer como resultado de um visitante aceitar manualmente os cookies ao aceitar.

1. No Debugger, verifique se o site Luma está mapeado para a propriedade da tag e se o registro do console de tags está ativado.
1. Use o console do desenvolvedor do seu navegador para **Limpar dados do site** in **Aplicativo** > **Armazenamento**

1. Recarregue o site Luma e você verá isso `defaultConsent` está definida como **[!UICONTROL Saída]** e nenhuma solicitação do SDK da Web foi feita

   ![Consentimento implicado na recusa](assets/consent-implied-out-cmp.png)

Caso um visitante decida aceitar (aceitar os cookies de rastreamento), você deve alterar o consentimento e defini-lo como **[!UICONTROL Entrada]**. Veja como fazer isso com uma regra:

1. Crie uma regra que é acionada quando o visitante clica em **Tudo bem**.  Nomear esta regra como: `all pages - click consent banner - set consent "in"`

1. Como a variável **[!UICONTROL Evento]**, use **[!UICONTROL Clique em]** em **[!UICONTROL Elementos que correspondem ao seletor de CSS]** `#klaro .cm-btn-success`

   ![O usuário clica em Condição de regra &quot;Tudo bem&quot;](assets/consent-optIn-clickEvent.png)

1. Adicionar uma ação usando o Experience Platform Web SDK [!UICONTROL Extensão], **[!UICONTROL Tipo de ação]** de **[!UICONTROL Definir consentimento]**, **[!UICONTROL Consentimento geral]** as **[!UICONTROL Entrada]**.

   ![Ação de aceitação da regra de consentimento](assets/consent-rule-optin-action.png)

   Uma coisa a observar aqui é que isso [!UICONTROL Definir consentimento] a ação será a primeira solicitação que sai e estabelece a identidade. Por causa disso, pode ser importante sincronizar identidades na própria primeira solicitação. O mapa de identidade pode ser adicionado a [!UICONTROL Definir consentimento] ação transmitindo um elemento de dados do tipo identidade.

1. Selecionar **[!UICONTROL Salvar na biblioteca e criar]**:

   ![Recusa da regra de consentimento](assets/consent-rule-optin-saveAndBuild.png)

1. **[!UICONTROL Salvar]** para a biblioteca e recrie-a.

Depois que essa regra estiver em vigor, a coleção de eventos deverá começar quando um visitante optar por entrar.

![Opção de pós-visitante de consentimento](assets/consent-post-user-optin.png)


Para obter mais informações sobre consentimento no SDK da Web, consulte [Suporte às preferências de consentimento do cliente](https://experienceleague.adobe.com/en/docs/experience-platform/edge/consent/supporting-consent).


Para obter mais informações sobre o [!UICONTROL Definir consentimento] ação, consulte [Definir consentimento](https://experienceleague.adobe.com/en/docs/experience-platform/edge/extension/action-types#set-consent).

[Próximo: ](setup-event-forwarding.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar feedback geral ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
