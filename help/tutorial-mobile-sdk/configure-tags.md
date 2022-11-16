---
title: Configurar uma propriedade de tag
description: Saiba como configurar uma propriedade de tag no [!UICONTROL Coleta de dados] interface.
exl-id: 0c4b00cc-34e3-4d08-945e-3fd2bc1b6ccf
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 11%

---

# Configurar uma propriedade de tag

Saiba como configurar uma propriedade de tag no [!UICONTROL Coleta de dados] interface.

As tags no Adobe Experience Platform são a última palavra em gerenciamento de tags da Adobe. As tags oferecem aos clientes uma forma simples de implantar e gerenciar todas as tags de análise, de marketing e de anúncios necessárias para potencializar experiências de cliente relevantes. Saiba mais sobre [tags](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR) na documentação do produto.

## Pré-requisitos

Para concluir a lição, você deve ter permissão para criar uma propriedade de tag. Também é útil ter uma compreensão básica das tags.

>[!NOTE]
>
> O Platform launch (lado do cliente) agora está [tags](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)

## Objetivos de aprendizagem

Nesta lição, você:

* Instale e configure as extensões de tag para dispositivos móveis.
* Gere as instruções de instalação do SDK.

## Configuração inicial

1. Crie uma nova propriedade de tag móvel:
   1. No [Interface da Coleta de dados](https://experience.adobe.com/data-collection/){target=&quot;_blank&quot;}, selecione **[!UICONTROL Tags]** na navegação à esquerda
   1. Selecione **[!UICONTROL Nova propriedade]**

      ![criar uma propriedade de tag](assets/mobile-tags-new-property.png).
   1. Para o **[!UICONTROL Nome]**, insira `Mobile SDK Course`.
   1. Para o **[!UICONTROL Plataforma]**, selecione **[!UICONTROL Celular]**.
   1. Selecione **[!UICONTROL Salvar]**.

      ![configurar a propriedade tag](assets/mobile-tags-property-config.png)

      >[!NOTE]
      >
      > As configurações de consentimento padrão para as implementações do sdk móvel baseadas em borda, como aquela que você está fazendo neste tutorial, vêm do [!UICONTROL Extensão de consentimento] e não a [!UICONTROL Privacidade] na configuração da propriedade da tag. Você adicionará e configurará a extensão Consent posteriormente nesta lição. Para obter mais informações, consulte [a documentação](https://aep-sdks.gitbook.io/docs/resources/privacy-and-gdpr).


1. Abra a nova propriedade
1. Criar uma biblioteca:

   1. Ir para **[!UICONTROL Fluxo de publicação]** no painel de navegação esquerdo.
   1. Selecionar **[!UICONTROL Adicionar biblioteca]**.

      ![Selecione Adicionar biblioteca](assets/mobile-tags-create-library.png)

   1. Para o **[!UICONTROL Nome]**, insira `Initial Build`.
   1. Para o **[!UICONTROL Ambiente]**, selecione **[!UICONTROL Desenvolvimento]**.
   1. Selecionar  **[!UICONTROL Adicionar todos os recursos alterados]**.
   1. Selecionar **[!UICONTROL Salvar e criar no desenvolvimento]**.

      ![Criar a biblioteca](assets/mobile-tags-save-library.png)

   1. Finalmente, defina-a como sua **[!UICONTROL Biblioteca de trabalho]**.
      ![Selecionar como biblioteca de trabalho](assets/mobile-tags-working-library.png)
1. Selecionar **[!UICONTROL Extensões]**.

   As extensões Mobile Core e Profile devem ser pré-instaladas.

1. Selecionar **[!UICONTROL Catálogo]**.

   ![configuração inicial](assets/mobile-tags-starting.png)

1. Use o [!UICONTROL Pesquisar] para localizar e instalar as seguintes extensões. Nenhuma dessas extensões requer configuração:
   * Identidade
   * Garantia da AEP

## Configuração de extensão

1. Instale o **Consentimento** extensão.

   Para os fins deste tutorial, selecione **[!UICONTROL Pending]**. Saiba mais sobre a extensão de consentimento em [a documentação](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network).

   ![configurações de consentimento](assets/mobile-tags-extension-consent.png)

1. Instale o **Rede de borda Adobe Experience Platform** extensão.

   No **[!UICONTROL Configuração da borda]** na lista suspensa, selecione o conjunto de dados criado no [etapa anterior](create-datastream.md).

1. Selecionar **[!UICONTROL Salvar na biblioteca e criar]**.

   ![configurações de rede de borda](assets/mobile-tags-extension-edge.png)


## Gerar instruções de instalação do SDK

1. Selecionar **[!UICONTROL Ambientes]**.

1. Selecione o **[!UICONTROL Desenvolvimento]** ícone de instalação.

   ![tela inicial dos ambientes](assets/mobile-tags-environments.png)

1. Selecionar **[!UICONTROL iOS]**.

1. Selecionar **[!UICONTROL Swift]**.

   ![instruções de instalação](assets/mobile-tags-install-instructions.png)

1. As instruções de instalação fornecem um bom ponto de partida para a implementação.

   Você pode encontrar informações adicionais [here](https://aep-sdks.gitbook.io/docs/getting-started/get-the-sdk).

   * **[!UICONTROL ID do arquivo do ambiente]**: Essa ID exclusiva aponta para o ambiente de desenvolvimento, observe esse valor. Produção/armazenamento temporário/desenvolvimento terá valores de ID diferentes.
   * **[!UICONTROL Podfile]**: O CocoaPods é usado para gerenciar versões e downloads do SDK. Para saber mais, reveja o [documentação](https://cocoapods.org/).
   * **[!UICONTROL Código de inicialização]**: Este bloco de código mostra como importar os SDKs necessários e registrar as extensões no lançamento.

>[!NOTE]
>As instruções de instalação devem ser consideradas um ponto de partida e não uma documentação definitiva. As versões mais recentes do SDK e amostras de código podem ser encontradas no oficial [documentação](https://aep-sdks.gitbook.io/docs/).

## Arquitetura de tags móveis

Se você estiver familiarizado com a versão da Web das tags, o antigo Launch, é importante entender as diferenças no dispositivo móvel.

Na Web, uma propriedade de tag é renderizada no JavaScript, que é então (normalmente) hospedada na nuvem. Esse arquivo JS é referenciado diretamente no site.

Em uma propriedade de tag móvel, as regras e configurações são renderizadas em arquivos JSON que são hospedados na nuvem. Os arquivos JSON são baixados e lidos pela extensão Mobile Core no aplicativo móvel. As extensões são SDKs separados que trabalham em conjunto. Se você adicionar uma extensão à propriedade da tag, também deverá atualizar o aplicativo. Se você alterar uma configuração de extensão ou criar uma regra, essas alterações serão refletidas no aplicativo depois de publicar a biblioteca de tags atualizada.

Próximo: **[Instalar SDKs](install-sdks.md)**

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender sobre o Adobe Experience Platform Mobile SDK. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)