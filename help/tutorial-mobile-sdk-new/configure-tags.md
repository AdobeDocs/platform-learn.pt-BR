---
title: Configurar uma propriedade de tag
description: Saiba como configurar uma propriedade de tag no [!UICONTROL Coleta de dados] interface.
feature: Mobile SDK,Tags
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 9%

---

# Configurar uma propriedade de tag

Saiba como configurar uma propriedade de tag no [!UICONTROL Coleta de dados] interface.

As tags no Adobe Experience Platform são a última palavra em gerenciamento de tags da Adobe. As tags oferecem aos clientes uma forma simples de implantar e gerenciar tags de análise, marketing e anúncios necessárias para potencializar experiências de cliente relevantes. Saiba mais sobre [Tags](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR) na documentação do produto.

## Pré-requisitos

Para concluir a lição, você deve ter permissão para criar uma propriedade de tag. Também é útil ter uma compreensão básica das tags.

>[!NOTE]
>
> O Platform launch (lado do cliente) agora é [tags](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)

## Objetivos de aprendizagem

Nesta lição, você vai:

* Instale e configure as extensões de tag para dispositivos móveis.
* Gere as instruções de instalação do SDK.

## Configuração inicial

1. Crie uma nova propriedade de tag móvel na Interface da coleção de dados:
   1. Selecionar **[!UICONTROL Tags]** no painel de navegação esquerdo.
   1. Selecione **[!UICONTROL Nova propriedade]**
      ![criar uma propriedade de tag](assets/tags-new-property.png).
   1. Para o **[!UICONTROL Nome]**, insira `Luma Mobile App Tutorial`.
   1. Para o **[!UICONTROL Platform]**, selecione **[!UICONTROL Dispositivo móvel]**.
   1. Selecione **[!UICONTROL Salvar]**.

      ![configurar a propriedade da tag](assets/tags-property-config.png)

      >[!NOTE]
      >
      > As configurações de consentimento padrão para as implementações do sdk móvel baseado em borda, como a que você está fazendo neste tutorial, vêm do [!UICONTROL Extensão de consentimento] e não o [!UICONTROL Privacidade] na configuração da propriedade tag. Você adiciona e configura a Extensão de consentimento posteriormente nesta lição. Para obter mais informações, consulte [a documentação](https://developer.adobe.com/client-sdks/documentation/privacy-and-gdpr/).


1. Abra a nova propriedade.
1. Criar uma biblioteca:

   1. Ir para **[!UICONTROL Fluxo de publicação]** no painel de navegação esquerdo.
   1. Selecionar **[!UICONTROL Adicionar biblioteca]**.

      ![Selecione Adicionar biblioteca](assets/tags-create-library.png)

   1. Para o **[!UICONTROL Nome]**, insira `Initial Build`.
   1. Para o **[!UICONTROL Ambiente]**, selecione **[!UICONTROL Desenvolvimento (desenvolvimento)]**.
   1. Selecionar  ![Botão Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Adicionar todos os recursos alterados]**.
   1. Selecionar **[!UICONTROL Salvar e criar no desenvolvimento]**.

      ![Criar a biblioteca](assets/tags-save-library.png)

   1. Finalmente, selecione **[!UICONTROL Build inicial]** como sua biblioteca de trabalho no **[!UICONTROL Selecionar uma biblioteca de trabalho]** menu.
      ![Selecionar como a biblioteca de trabalho](assets/tags-working-library.png)
1. Verificar extensões:

   1. Assegure que **[!UICONTROL Build inicial]** está selecionada como biblioteca padrão.

   1. Selecione **[!UICONTROL Extensões]** no painel esquerdo.

   1. Selecione o **[!UICONTROL Instalado]** guia.

      A variável [!UICONTROL Núcleo móvel] e [!UICONTROL Perfil] As extensões do devem ser pré-instaladas.

      ![Tags instaladas](assets/tags-installed.png)

## Configuração de extensão

1. Verifique se você está em **[!UICONTROL Extensões]** na propriedade do aplicativo móvel.

1. Selecionar **[!UICONTROL Catálogo]**.

   ![configuração inicial](assets/tags-starting.png)

1. Use o ![Pesquisar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) **[!UICONTROL Pesquisar]** o campo localizar o **Identidade** extensão.

   1. Pesquisar por `Identity`.

   2. Selecione o **[!UICONTROL Identidade]** extensão.

   3. Selecionar **[!UICONTROL Instalar]**.

      ![Instalação de identidade](assets/tags-identity-install.png)

   Essa extensão não requer nenhuma configuração adicional.

1. Use o ![Pesquisar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) **[!UICONTROL Pesquisar]** para localizar e instalar o **AEP Assurance** extensão.

   Essa extensão não requer nenhuma configuração adicional.

1. Use o ![Pesquisar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) **[!UICONTROL Pesquisar]** para localizar e instalar o **Consentimento** extensão. Na tela de configuração:

   1. Selecionar **[!UICONTROL Pending]**. Neste tutorial, você gerencia o consentimento ainda mais no aplicativo. Saiba mais sobre a Extensão de consentimento em [a documentação](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/).
   1. Selecionar **[!UICONTROL Salvar na biblioteca]**.

      ![configurações de consentimento](assets/tags-extension-consent.png)

1. Use o ![Pesquisar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) **[!UICONTROL Pesquisar]** para localizar e instalar o **Rede de borda Adobe Experience Platform** extensão.

   1. Entrada **[!UICONTROL Datastreams]** selecione o **[!UICONTROL Sequência de dados]** que você criou na [etapa anterior](create-datastream.md) para cada ambiente, por exemplo **[!UICONTROL Aplicativo móvel Luma]**.

   1. Especifique a **[!UICONTROL Domínio da rede de borda]** no prazo de **[!UICONTROL Configuração de domínio]**. O domínio Edge Network é o nome da sua sandbox, seguido por `data.adobedc.net`, por exemplo `techmarketingdemos.data.adobedc.net`.

   1. No **[!UICONTROL Salvar na biblioteca]** selecione **[!UICONTROL Salvar na biblioteca e criar]**.

      ![configurações de rede de borda](assets/tags-extension-edge.png)

Sua biblioteca é criada para as novas extensões e configurações. Uma build bem-sucedida é indicada por um <span style="color:green">●</span> no **[!UICONTROL Build inicial]** botão.


## Gerar instruções de instalação do SDK

1. Selecionar **[!UICONTROL Ambientes]** do painel esquerdo.

1. Selecione o **[!UICONTROL Desenvolvimento]** ícone de instalação ![Caixa](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Box_18_N.svg) .

   ![tela inicial dos ambientes](assets/tags-environments.png)

1. No [!UICONTROL Instruções de instalação em dispositivos móveis] , selecione a **[!UICONTROL iOS]** guia.

1. Você pode copiar ![Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) as instruções para configurar seu projeto usando o CocoaPods. Os CocoaPods são usados para gerenciar versões e downloads do SDK. Para saber mais, reveja o [documentação](https://cocoapods.org/).

   As instruções de instalação fornecem um bom ponto de partida para a implementação. Você pode encontrar informações adicionais [aqui](https://developer.adobe.com/client-sdks/documentation/getting-started/get-the-sdk/).

1. Selecione o **[!UICONTROL Swift]** guia abaixo **[!UICONTROL Adicionar código de inicialização]**. Este bloco de código mostra como importar os SDKs necessários e registrar as extensões no lançamento.

1. Copiar ![Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) o **[!UICONTROL ID do arquivo de ambiente]** e guarde-o no local necessário posteriormente. Essa ID exclusiva aponta para o ambiente de desenvolvimento. Cada ambiente (Produção, Armazenamento temporário, Desenvolvimento) tem seu próprio valor de ID exclusivo.

   ![instruções de instalação](assets/tags-install-instructions.png)

>[!NOTE]
>
>As instruções de instalação devem ser consideradas um ponto de partida e não uma documentação definitiva. As versões mais recentes do SDK e amostras de código podem ser encontradas no [documentação](https://developer.adobe.com/client-sdks/documentation/).

>[!INFO]
>
>No restante deste tutorial, você estará **não** usar as instruções do CocoaPods, mas observar uma configuração nativa baseada em pacotes Swift.


## Arquitetura de tags móveis

Se você estiver familiarizado com a versão da Web das tags, antigo Launch, é importante entender as diferenças nos dispositivos móveis.

* Na Web, uma propriedade de tag é renderizada no JavaScript, que é então (geralmente) hospedado na nuvem. Esse arquivo JavaScript é referenciado diretamente no site.

* Em uma propriedade de tag móvel, as regras e configurações são renderizadas em arquivos JSON que são hospedados na nuvem. Os arquivos JSON são baixados e lidos pela extensão Mobile Core no aplicativo móvel. As extensões são SDKs separados que funcionam juntos. Se você adicionar uma extensão à propriedade da tag, também deverá atualizar o aplicativo. Se você alterar uma configuração de extensão ou criar uma regra, essas alterações serão refletidas no aplicativo depois de publicar a biblioteca de tags atualizada.

>[!SUCCESS]
>
>Agora você tem uma propriedade de tag móvel para usar no restante deste tutorial.<br/>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Próximo: **[Instalar SDKs](install-sdks.md)**
