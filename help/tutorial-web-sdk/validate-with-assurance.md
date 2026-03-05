---
title: Validar implementações do Web SDK com o Experience Platform Assurance
description: Saiba como validar a implementação do SDK da web da Platform com o Adobe Experience Platform Assurance. Esta lição é parte do tutorial Implementar a Adobe Experience Cloud com o SDK da web.
feature: Web SDK,Tags,Assurance
jira: KT-15406
exl-id: 31e381ea-fbaf-495f-a6e9-2ff6c0d36939
source-git-commit: da65f13f95a6d1258655e8eebc76cf024221a610
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 5%

---

# Validar implementações do Web SDK com o Experience Platform Assurance

O [Adobe Experience Platform Assurance](https://experienceleague.adobe.com/pt-br/docs/experience-platform/assurance/home) é um recurso que ajuda a inspecionar, testar, simular e validar a maneira como você coleta dados ou fornece experiências.

Conforme você aprendeu na lição [Configurar uma sequência de dados](configure-datastream.md), o Platform Web SDK envia dados da sua propriedade digital para o Platform Edge Network. Em seguida, o Platform Edge Network encaminha os dados para os serviços ativados no fluxo de dados. Você pode validar as solicitações que entram e saem do Platform Edge Network usando o Assurance.

![Diagrama de validação do Web SDK e do Adobe Experience Platform](assets/dc-websdk-validation.png)


## Objetivos de aprendizagem

No final desta lição, você poderá:

* Iniciar uma sessão do Assurance
* Exibir solicitações enviadas para e do Platform Edge Network

## Pré-requisitos

Você está familiarizado com as tags de Coleção de dados e o [site de demonstração do Luma](https://luma.enablementadobe.com){target="_blank"} e concluiu as lições anteriores no tutorial:

* [Configurar um esquema XDM](configure-schemas.md)
* [Configurar um namespace de identidade](configure-identities.md)
* [Configurar uma sequência de dados](configure-datastream.md)
* [Extensão do Web SDK instalada na propriedade da tag](install-web-sdk.md)
* [Criar elementos de dados](create-data-elements.md)
* [Capturar identidades](create-identities.md)
* [Criar uma regra de tag](create-tag-rule.md)
* [Validar com o Debugger](validate-with-debugger.md)


## Iniciar e exibir uma sessão do Assurance

Há várias maneiras de iniciar uma sessão do Assurance.


### Ativar o Edge Trace no Debugger

Para ativar o Edge Trace:

1. Vá para o [site de demonstração do Luma](https://luma.enablementadobe.com) e use o depurador para [alternar a propriedade da marca no site para sua própria propriedade de desenvolvimento](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. Verifique se você está conectado ao Debugger mostrando o nome da organização. Se o seu nome de usuário estiver sendo exibido, saia e tente entrar novamente.
1. Na navegação à esquerda do **[!UICONTROL Experience Platform Debugger]**, selecione **[!UICONTROL Logs]**
1. Selecione a guia **[!UICONTROL Edge]** e selecione **[!UICONTROL Conectar]**

   ![Conectar ao Edge Trace](assets/assurance-edgeTrace-connect.png)

1. Está vazio por enquanto

   ![Edge Trace Conectado](assets/analytics-debugger-edge-connected.png)

1. Atualize a [página inicial do Luma](https://luma.enablementadobe.com/) e verifique o **[!UICONTROL Experience Platform Debugger]** novamente para ver os dados que entram na Platform Edge Network. Nas lições futuras, você poderá ver as solicitações enviadas ao habilitar serviços no fluxo de dados.

   ![Solicitações no Edge Trace](assets/validate-edge-trace.png)

   Toda vez que você ativa o Edge Trace no Adobe Experience Platform Debugger, uma sessão do Assurance é iniciada em segundo plano. Embora seja possível revisar as informações aqui, a interface do Assurance provavelmente será muito mais útil.

1. Com o Edge Trace ativado, você pode ver um ícone de link de saída na parte superior. Selecione o ícone para abrir o Assurance.

   ![Iniciar sessão do Assurance](assets/validate-debugger-start-assurnance.png)

1. Uma nova guia do navegador é aberta com a interface do Assurance.

### Iniciar uma sessão do Assurance na interface do Assurance

1. Abra a [interface da Coleção de Dados](https://experience.adobe.com/#/data-collection/home){target="_blank"}
1. Selecione Assurance na navegação à esquerda
1. Selecione Criar sessão
   ![Criar uma sessão do Assurance](assets/assurance-create-session.png)
1. Usar a opção **[!UICONTROL Conexão de deep link]**
1. Selecionar **[!UICONTROL Início]**
1. Nomeie a sessão, por exemplo, `Luma Web SDK validation`
1. Como a **[!UICONTROL URL Base]**, digite `https://luma.enablementadobe.com/`
   ![Nomear a sessão do Assurance](assets/assurance-name-session.png)
1. Na próxima tela, selecione **[!UICONTROL Copiar Link]**
1. Selecione o ícone para copiar o link para a área de transferência
1. Cole a URL no seu navegador, que abrirá o site Luma com um parâmetro de URL especial `adb_validation_sessionid` e iniciará a sessão
1. Na interface do Assurance, você deve ver uma mensagem indicando que se conectou com êxito à sessão e deve ver eventos capturados na interface do Assurance.
   ![A sessão do Assurance foi conectada](assets/assurance-success.png)

## Validar o estado atual da implementação do Web SDK

Há informações limitadas para exibir neste estágio da implementação, pois ainda não habilitamos nenhum serviço no fluxo de dados.

### Exibir solicitações de entrada do Web SDK com `Alloy Request`

Podemos exibir a ocorrência recebida do Web SDK como recebida pela borda:

1. Selecionar a linha `Alloy Request`
1. Examine Evento Bruto (ou expanda nós na [!UICONTROL Carga] > `ACPExtensionEventData`) até encontrar seu objeto XDM com variáveis familiares:

   ![Solicitação de liga](assets/assurance-alloy-request.png)


### Exibir a resposta em `Alloy Response Handle`

Como você sabe, a Experience Cloud Id (ECID) fica visível na resposta do Web SDK depois de ser gerada na Platform Edge Network. Vamos procurá-lo na resposta, conforme visualizado no Assurance:

1. Filtre e selecione a linha com o evento chamado `Alloy Response Handle`.
1. Um menu é exibido à direita. Selecione o sinal de `+` ao lado de `[!UICONTROL ACPExtensionEventData]`
1. Detalhe selecionando `[!UICONTROL payload > 0 > payload > 0 > namespace]`. A ID mostrada no último `0` corresponde ao `ECID`. Você sabe que pelo valor que aparece abaixo de `namespace` correspondendo a `ECID`

   ![Resposta do Assurance Alloy](assets/assurance-alloy-response.png)

   >[!CAUTION]
   >
   >Você pode ver um valor de ECID truncado devido à largura da janela. Basta selecionar a barra de alças na interface e arrastar para a esquerda para visualizar toda a ECID.

Nas lições futuras, você usa o Assurance para validar cargas totalmente processadas que chegam a um aplicativo do Adobe habilitado no fluxo de dados.

Com um objeto XDM sendo acionado agora em uma página e sabendo como validar sua coleção de dados, você estará pronto para configurar o Experience Platform e os aplicativos individuais da Adobe usando o Platform Web SDK.

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [postagem de discussão da Comunidade Experience League](https://experienceleaguecommunities.adobe.com/adobe-experience-platform-18/tutorial-discussion-implement-adobe-experience-cloud-with-web-sdk-tutorial-248848)
