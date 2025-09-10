---
title: Configurar uma propriedade de tag para implementações do Platform Mobile SDK
description: Aprenda a configurar uma propriedade de tag na interface da [!UICONTROL Coleção de dados].
feature: Mobile SDK,Tags
jira: KT-14626
exl-id: 0c4b00cc-34e3-4d08-945e-3fd2bc1b6ccf
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '1131'
ht-degree: 4%

---

# Configurar uma propriedade de tag

Aprenda a configurar uma propriedade de tag na interface da [!UICONTROL Coleção de dados].

As tags no Adobe Experience Platform são a última palavra em gerenciamento de tags da Adobe. As tags oferecem aos clientes uma forma simples de implantar e gerenciar tags de análise, marketing e anúncios necessárias para potencializar experiências de cliente relevantes. Saiba mais sobre [Marcas](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home) na documentação do produto.

## Pré-requisitos

Para concluir a lição, você deve ter permissão para criar uma propriedade de tag. Também é útil ter uma compreensão básica das tags.

>[!NOTE]
>
> O Platform Launch (lado do cliente) agora é [Tags](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)

## Objetivos de aprendizagem

Nesta lição, você vai:

* Instale e configure as extensões de tag para dispositivos móveis.
* Gere as instruções de instalação do SDK.

## Configuração inicial

1. Crie uma nova propriedade de tag móvel na Interface da coleção de dados:
   1. Selecione **[!UICONTROL Tags]** na navegação à esquerda.
   1. Selecionar **[!UICONTROL Nova Propriedade]**
      ![criar uma propriedade de marca](assets/tags-new-property.png){zoomable="yes"}.
   1. Para o **[!UICONTROL Nome]**, digite `Luma Mobile App Tutorial`.
   1. Para a **[!UICONTROL Plataforma]**, selecione **[!UICONTROL Dispositivo móvel]**.
   1. Selecione **[!UICONTROL Salvar]**.

      ![configurar a propriedade da marca](assets/tags-property-config.png){zoomable="yes"}

      >[!NOTE]
      >
      > As configurações padrão de consentimento para as implementações do Mobile SDK baseadas em borda, como a que você está fazendo nesta lição, vêm da [!UICONTROL Extensão de consentimento] e não da configuração de [!UICONTROL Privacidade] na configuração da propriedade da tag. Você adiciona e configura a Extensão de consentimento posteriormente nesta lição. Para obter mais informações, consulte [a documentação](https://developer.adobe.com/client-sdks/edge/consent-for-edge-network/).


1. Abra a nova propriedade.
1. Criar uma biblioteca:

   1. Vá para **[!UICONTROL Fluxo de Publicação]** na navegação à esquerda.
   1. Selecione **[!UICONTROL Adicionar Biblioteca]**.

      ![Selecione Adicionar Biblioteca](assets/tags-create-library.png){zoomable="yes"}

   1. Para o **[!UICONTROL Nome]**, digite `Initial Build`.
   1. Para o **[!UICONTROL Ambiente]**, selecione **[!UICONTROL Desenvolvimento (desenvolvimento)]**.
   1. Selecione o ![Botão Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Adicionar todos os Recursos Alterados]**.
   1. Selecione **[!UICONTROL Salvar e criar no desenvolvimento]**.

      ![Criar a Biblioteca](assets/tags-save-library.png){zoomable="yes"}

   1. Finalmente, selecione **[!UICONTROL Build inicial]** como sua biblioteca de trabalho no menu **[!UICONTROL Selecionar uma biblioteca de trabalho]**.
      ![Selecionar como a biblioteca de trabalho](assets/tags-working-library.png){zoomable="yes"}
1. Verificar extensões:

   1. Verifique se **[!UICONTROL Build inicial]** está selecionada como a biblioteca padrão.

   1. Selecione **[!UICONTROL Extensões]** no painel esquerdo.

   1. Selecione a guia **[!UICONTROL Instalado]**.

      As extensões do [!UICONTROL Mobile Core] e do [!UICONTROL Profile] devem ser pré-instaladas.

      ![Marcas instaladas](assets/tags-installed.png){zoomable="yes"}

## Configuração de extensão

1. Verifique se você está em **[!UICONTROL Extensões]** na propriedade do aplicativo móvel.

1. Selecione **[!UICONTROL Catálogo]**.

   ![configuração inicial](assets/tags-starting.png){zoomable="yes"}

1. Use o campo ![Pesquisa](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) **[!UICONTROL Pesquisa]** para localizar a extensão **Identidade**.

   1. Pesquisar por `Identity`.

   2. Selecione a extensão **[!UICONTROL Identidade]**.

   3. Selecione **[!UICONTROL Instalar]**.

      ![Instalação de identidade](assets/tags-identity-install.png){zoomable="yes"}

   Essa extensão não requer nenhuma configuração adicional.

1. Use o campo ![Pesquisa](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) **[!UICONTROL Pesquisa]** para localizar e instalar a extensão **AEP Assurance**.

   Essa extensão não requer nenhuma configuração adicional.

1. Use o campo ![Pesquisa](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) **[!UICONTROL Pesquisa]** para localizar e instalar a extensão **Consentimento**. Na tela de configuração:

   1. Selecione **[!UICONTROL Pendente]**. Neste tutorial, você gerencia o consentimento ainda mais no aplicativo. Saiba mais sobre a Extensão de consentimento em [a documentação](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/).
   1. Selecione **[!UICONTROL Salvar na biblioteca]**.

      ![configurações de consentimento](assets/tags-extension-consent.png){zoomable="yes"}

1. Use o campo ![Pesquisa](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) **[!UICONTROL Pesquisa]** para localizar e instalar a extensão **Adobe Experience Platform Edge Network**.

   1. Em **[!UICONTROL Datastreams]**, selecione o **[!UICONTROL Datastream]** criado na [etapa anterior](create-datastream.md) para cada um dos ambientes, por exemplo **[!DNL Luma Mobile App]**.

   1. Se ainda não estiver preenchido, especifique o **[!UICONTROL domínio Edge Network]** em **[!UICONTROL Configuração de Domínio]**. O domínio do Edge Network é o nome da sua organização, seguido por `data.adobedc.net`, por exemplo `techmarketingdemos.data.adobedc.net`.

   1. No menu **[!UICONTROL Salvar na biblioteca]**, selecione **[!UICONTROL Salvar na biblioteca e criar]**.

      ![configurações de rede de borda](assets/tags-extension-edge.png){zoomable="yes"}

Sua biblioteca foi criada para as novas extensões e configurações. Um <span style="color:green">●</span> no botão **[!UICONTROL Compilação Inicial]** indicou uma compilação bem-sucedida.


## Gerar instruções de instalação do SDK

As tags fornecem instruções e trechos de código para instalar o Adobe Experience Platform Mobile SDK em seu aplicativo.

>[!BEGINTABS]

>[!TAB iOS]

1. Selecione **[!UICONTROL Ambientes]** no painel esquerdo.

1. Selecione o ícone de instalação **[!UICONTROL Desenvolvimento]** ![Caixa](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Box_18_N.svg).

   ![tela inicial dos ambientes](assets/tags-environments.png){zoomable="yes"}

1. Na caixa de diálogo **[!UICONTROL Instruções de Instalação Móvel]**, selecione a guia **[!UICONTROL iOS]**.

1. Você pode copiar ![Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) as instruções para configurar seu projeto usando o CocoaPods. Os CocoaPods são usados para gerenciar versões e downloads do SDK. Para saber mais, consulte a [documentação do CocoaPods](https://cocoapods.org/).

   As [instruções de instalação](https://developer.adobe.com/client-sdks/documentation/getting-started/get-the-sdk/) fornecem um bom ponto de partida para a implementação.

   No restante deste tutorial, você está **não** usando as instruções do CocoaPods. Em vez disso, use a configuração nativa baseada no Swift Package Manager (SPM).

1. Selecione a guia **[!UICONTROL Swift]** abaixo de **[!UICONTROL Adicionar código de inicialização]**. Este bloco de código mostra como importar os SDKs necessários e registrar as extensões no lançamento. Esta importação e registro são abordados com mais detalhes em [Instalar SDKs](install-sdks.md).

1. Copie ![Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) a **[!UICONTROL ID do Arquivo de Ambiente]** e armazene-a no local necessário posteriormente. Essa ID exclusiva aponta para o ambiente de desenvolvimento. Cada ambiente (Produção, Armazenamento temporário, Desenvolvimento) tem seu próprio valor de ID exclusivo.

   ![instruções de instalação](assets/tags-install-instructions.png){zoomable="yes"}

>[!TAB Android]

1. Selecione **[!UICONTROL Ambientes]** no painel esquerdo.
1. Selecione o ícone de instalação **[!UICONTROL Desenvolvimento]** ![Caixa](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Box_18_N.svg).

   ![tela inicial dos ambientes](assets/tags-environments.png){zoomable="yes"}

1. Na caixa de diálogo **[!UICONTROL Instruções de Instalação Móvel]**, selecione a guia **[!UICONTROL Android]**.
1. Você pode copiar ![Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) as instruções para configurar seu projeto usando Gradle. Gradle é usado para gerenciar versões e downloads do SDK. Para saber mais, reveja a [documentação do Gradle](https://gradle.org/)

   As [instruções de instalação](https://developer.adobe.com/client-sdks/documentation/getting-started/get-the-sdk/) fornecem um bom ponto de partida para a implementação.

1. Este bloco de código mostra como importar os SDKs necessários e registrar as extensões no lançamento. Esta importação e registro são abordados com mais detalhes em [Instalar SDKs](install-sdks.md).

1. Copie ![Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) a **[!UICONTROL ID do Arquivo de Ambiente]** e armazene-a no local necessário posteriormente. Essa ID exclusiva aponta para o ambiente de desenvolvimento. Cada ambiente (Produção, Armazenamento temporário, Desenvolvimento) tem seu próprio valor de ID exclusivo.

   ![instruções de instalação](assets/tags-install-instructions-android.png){zoomable="yes"}

>[!ENDTABS]

>[!NOTE]
>
>As instruções de instalação devem ser consideradas um ponto de partida e não uma documentação definitiva. As versões mais recentes do SDK e amostras de código podem ser encontradas na [documentação](https://developer.adobe.com/client-sdks/home/) oficial.

## Arquitetura de tags móveis

Se você estiver familiarizado com a versão da Web de Tags, antes chamada de Launch, é importante entender as diferenças nos dispositivos móveis.

* Na Web, uma propriedade de tag é renderizada na JavaScript, que é então (geralmente) hospedada na nuvem. Esse arquivo do JavaScript é referenciado diretamente no site.

* Em uma propriedade de tag móvel, as regras e configurações são renderizadas em arquivos JSON que são hospedados na nuvem. Os arquivos JSON são baixados e lidos pela extensão Mobile Core no aplicativo móvel. As extensões são SDKs separados que funcionam juntos. Se você adicionar uma extensão à propriedade da tag, também deverá atualizar o aplicativo. Se você alterar uma configuração de extensão ou criar uma regra, essas alterações serão refletidas no aplicativo depois de publicar a biblioteca de tags atualizada. Essa flexibilidade permite modificar configurações (como a id do conjunto de relatórios do Adobe Analytics). Ou até mesmo alterar o comportamento do aplicativo (usando elementos de dados e regras, como você vê nas lições posteriores) sem precisar alterar o código no aplicativo e reenviar para a loja de aplicativos.

>[!SUCCESS]
>
>Agora você tem uma propriedade de tag móvel para usar no restante deste tutorial.
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-os nesta [postagem de discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Próximo: **[Instalar SDKs](install-sdks.md)**
