---
title: Criar uma regra de tag
description: Saiba como enviar um evento para a Platform Edge Network com seu objeto XDM usando uma regra de tag. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Tags
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 1%

---

# Criar uma regra de tag

Saiba como enviar um evento para a Platform Edge Network com seu objeto XDM usando uma regra de tag. Uma regra de tag é uma combinação de eventos, condições e ações que instrui a propriedade de tag a fazer algo.

>[!NOTE]
>
> Para fins de demonstração, os exercícios desta lição baseiam-se no exemplo usado durante a [Criar identidades](create-identities.md) etapa; enviar uma ação de evento XDM para capturar conteúdo e identidades dos usuários na [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html).


## Objetivos de aprendizagem

No final desta lição, você poderá:

* Usar uma convenção de nomenclatura para gerenciar regras nas tags
* Enviar um evento XDM usando os tipos de ação Atualizar variável e Enviar evento em uma regra de tag
* Publicar uma regra de tag em uma biblioteca de desenvolvimento


## Pré-requisitos

Você está familiarizado com as tags de Coleção de dados e a [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html)e você deve ter concluído as seguintes lições anteriores no tutorial:

* [Configurar um esquema XDM](configure-schemas.md)
* [Configurar um namespace de identidade](configure-identities.md)
* [Configurar uma sequência de dados](configure-datastream.md)
* [Extensão SDK da Web instalada na propriedade da tag](install-web-sdk.md)
* [Criar elementos de dados](create-data-elements.md)
* [Criar identidades](create-identities.md)

## Convenções de nomenclatura

Para gerenciar melhor as regras nas tags, é recomendável seguir uma convenção de nomenclatura padrão. Este tutorial usa uma convenção de nomenclatura de três partes:

* [**localização**] - [**evento**] - [**ferramenta**] (**sequência**)

onde;

1. **localização** é a página ou páginas no site em que a regra é acionada
1. **evento** é o acionador da regra
1. **ferramenta** é o aplicativo ou aplicativos específicos usados na etapa de ação dessa regra
1. **sequência** é a ordem na qual a regra deve ser acionada em relação a outras regras
<!-- minor update -->

## Criar regra de tag

Nas tags, as regras são usadas para executar ações (acionar chamadas) em várias condições. A extensão de tags do SDK da Web da Platform inclui duas ações que serão usadas nesta lição:

* **[!UICONTROL Atualizar variável]** mapeia elementos de dados para campos XDM
* **[!UICONTROL Enviar evento]** envia o objeto XDM para a Rede de borda do Experience Platform

### Atualizar variável

Crie essa primeira regra como uma &quot;configuração global&quot; para definir todas as variáveis de conteúdo essenciais no objeto XDM usando o SDK da Web da plataforma **[!UICONTROL Atualizar variável]** ação. Em seguida, crie uma segunda regra, sequenciada para ser acionada depois da primeira, para enviar o objeto XDM para a Rede de borda da Platform usando o **[!UICONTROL Enviar evento]** ação. Posteriormente neste tutorial, você enviará campos XDM diferentes com base no tipo de página em que o visitante está (por exemplo, SKUs de produto em páginas de produto). Você consegue isso sequenciando as regras que contêm **[!UICONTROL Atualizar variável]** ações antes da regra que usa o **[!UICONTROL Enviar evento]** ação.

Para criar uma regra de tag:

1. Abra a propriedade da tag que você está usando neste tutorial

1. Ir para **[!UICONTROL Regras]** na navegação à esquerda

1. Selecione o **[!UICONTROL Criar nova regra]** botão

   ![Criar uma regra](assets/rules-create.png)

1. Atribua um nome à regra `all pages global content variables - page bottom - AA (order 1)`

1. No **[!UICONTROL Eventos]** , selecione **[!UICONTROL Adicionar]**

   ![Nomear a regra e adicionar um evento](assets/rule-name-new.png)

1. Use o **[!UICONTROL Extensão principal]** e selecione `Page Bottom` como o **[!UICONTROL Tipo de evento]**

1. No **[!UICONTROL Nome]** campo, nomeie-o `Core - Page Bottom - order 1`. Isso ajuda a descrever o acionador com um nome significativo.

1. Selecionar **[!UICONTROL Avançado]** e insira `1` in **[!UICONTROL Pedido]**

   >[!NOTE]
   >
   > Quanto maior o número inserido, mais tarde na ordem geral de operações ele será acionado.

1. Selecionar **[!UICONTROL Manter alterações]** para retornar à tela principal da regra
   ![Selecionar acionador final da página](assets/create-tag-rule-trigger-bottom.png)

1. No **[!UICONTROL Ações]** , selecione **[!UICONTROL Adicionar]**

1. Como a variável **[!UICONTROL Extensão]**, selecione **[!UICONTROL Adobe Experience Platform Web SDK]**

1. Como a variável **[!UICONTROL Tipo de ação]**, selecione **[!UICONTROL Atualizar variável]**

1. Como a variável **[!UICONTROL Elemento de dados]**, selecione o `xdm.variable.content` você criou na [Criar elementos de dados](create-data-elements.md) lição

   ![Atualizar esquema de variável](assets/create-rule-update-variable.png)

Agora mapeie seu [!UICONTROL elementos de dados] para o [!UICONTROL schema] usado pelo seu objeto XDM.

>[!NOTE]
> 
> Você pode mapear para propriedades individuais ou objetos inteiros. Neste exemplo, você mapeia para propriedades individuais.


1. Role para baixo até alcançar a **`web`** objeto

1. Selecione para abri-lo

1. Mapeie os seguintes elementos de dados para o correspondente `web` Variáveis XDM

   * **`web.webPageDetials.name`** para `%page.pageInfo.pageName%`
   * **`web.webPageDetials.server`** para `%page.pageInfo.server%`
   * **`web.webPageDetials.siteSection`** para `%page.pageInfo.hierarchie1%`

   ![Atualizar conteúdo variável](assets/create-rule-xdm-variable-content.png)

1. Em seguida, localize o `identityMap` no esquema e selecione-o

1. Mapear para o `identityMap.loginID` elemento de dados

   ![Atualizar mapa de identidade da variável](assets/create-rule-variable-identityMap.png)

1. Em seguida, localize o campo eventType e selecione-o

1. Insira o valor `web.webpagedetails.pageViews`

   >[!WARNING]
   >
   > Essa lista suspensa preenche o **`xdm.eventType`** no objeto XDM. Embora também seja possível digitar rótulos de forma livre neste campo, é altamente recomendável **não** pois tem efeitos adversos com a Platform.

   >[!TIP]
   >
   > Para entender quais valores devem ser preenchidos na variável `eventType` , você deve ir para a página do esquema e selecionar a `eventType` para exibir os valores sugeridos no painel direito.

   ![Atualizar mapa de identidade da variável](assets/create-tag-rule-eventType.png)


1. Selecionar **[!UICONTROL Manter alterações]** e depois **[!UICONTROL Salvar]** na próxima tela para concluir a criação da regra

### Enviar evento

Agora que você definiu as variáveis, é possível criar a segunda regra para enviar o objeto XDM para a Rede de borda da Platform com o **[!UICONTROL Enviar evento]** tipo de ação.

1. À direita, selecione para **[!UICONTROL Adicionar regra]** para criar outra regra

1. Atribua um nome à regra `all pages send event - page bottom - AA (order 50)`

1. No **[!UICONTROL Eventos]** , selecione **[!UICONTROL Adicionar]**

1. Use o **[!UICONTROL Extensão principal]** e selecione `Page Bottom` como o **[!UICONTROL Tipo de evento]**

1. No **[!UICONTROL Nome]** campo, nomeie-o `Core - Page Bottom - order 50`. Isso ajuda a descrever o acionador com um nome significativo.

1. Selecionar **[!UICONTROL Avançado]** e insira `50` in **[!UICONTROL Pedido]**. Isso garantirá que a segunda regra seja acionada depois da primeira regra definida para acionar como `1`.

1. Selecionar **[!UICONTROL Manter alterações]** para retornar à tela principal da regra
   ![Selecionar acionador final da página](assets/create-tag-rule-trigger-bottom-send.png)

1. No **[!UICONTROL Ações]** , selecione **[!UICONTROL Adicionar]**

1. Como a variável **[!UICONTROL Extensão]**, selecione  **[!UICONTROL Adobe Experience Platform Web SDK]**

1. Como a variável  **[!UICONTROL Tipo de ação]**, selecione  **[!UICONTROL Enviar evento]**

1. Como a variável **[!UICONTROL XDM]**, selecione o `xdm.variable.content` elemento de dados criado na lição anterior

1. Selecionar **[!UICONTROL Manter alterações]** para retornar à tela principal da regra

   ![Adicionar a ação Enviar evento](assets/create-rule-send-event-action.png)
1. Selecionar **[!UICONTROL Salvar]** para salvar a regra

   ![Salvar a regra](assets/create-rule-save-rule.png)

## Publicar a regra em uma biblioteca

Em seguida, publique a regra no ambiente de desenvolvimento para que você possa verificar se funciona.

Para criar uma biblioteca:

1. Ir para **[!UICONTROL Fluxo de publicação]** na navegação à esquerda

1. Selecionar **[!UICONTROL Adicionar biblioteca]**

   ![Selecione Adicionar biblioteca](assets/rule-publish-library.png)
1. Para o **[!UICONTROL Nome]**, insira `Luma Web SDK Tutorial`
1. Para o **[!UICONTROL Ambiente]**, selecione `Development`
1. Selecionar  **[!UICONTROL Adicionar todos os recursos alterados]**

   >[!NOTE]
   >
   >    Além da extensão do SDK da Web da Adobe Experience Platform e da `all pages global content variables - page bottom - AA (order 50)` regra, você verá os componentes de tag criados nas lições anteriores. A extensão principal contém o JavaScript básico exigido por todas as propriedades de tag da Web.

1. Selecionar **[!UICONTROL Salvar e criar para desenvolvimento]**

   ![Criar a biblioteca](assets/create-tag-rule-library-changes.png)

A biblioteca pode levar alguns minutos para ser criada e, quando estiver concluída, exibirá um ponto verde à esquerda do nome da biblioteca:

![Compilação concluída](assets/create-rule-development-success.png)

Como você pode ver no [!UICONTROL Fluxo de publicação] há muito mais no processo de publicação, que está além do escopo deste tutorial. Este tutorial usa apenas uma única biblioteca no ambiente de desenvolvimento do.

Agora você está pronto para validar os dados na solicitação usando o Adobe Experience Platform Debugger.

[Próxima ](validate-with-debugger.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar feedback geral ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
