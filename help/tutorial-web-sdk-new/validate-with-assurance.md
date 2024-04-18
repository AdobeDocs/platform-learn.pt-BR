---
title: Validar implementações do SDK da Web com o Experience Platform Assurance
description: Saiba como validar a implementação do SDK da Web da sua plataforma com o Adobe Experience Platform Assurance. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Web SDK,Tags,Assurance
exl-id: 31e381ea-fbaf-495f-a6e9-2ff6c0d36939
source-git-commit: fe8b92c560c9676a44935005cc558388244d6aea
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 2%

---

# Validar implementações do SDK da Web com o Experience Platform Assurance

O Adobe Experience Platform Assurance é um produto da Adobe Experience Cloud que ajuda a inspecionar, testar, simular e validar a maneira como você coleta dados ou fornece experiências. Leia mais sobre [Adobe Assurance](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=en).


## Objetivos de aprendizagem

No final desta lição, você poderá:

* Iniciar uma sessão do Assurance
* Exibir solicitações enviadas para e do Platform Edge Network

## Pré-requisitos

Você está familiarizado com as tags de Coleção de dados e a [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} e concluíram as lições anteriores no tutorial:

* [Configurar um esquema XDM](configure-schemas.md)
* [Configurar um namespace de identidade](configure-identities.md)
* [Configurar uma sequência de dados](configure-datastream.md)
* [Extensão SDK da Web instalada na propriedade da tag](install-web-sdk.md)
* [Criar elementos de dados](create-data-elements.md)
* [Criar identidades](create-identities.md)
* [Criar uma regra de tag](create-tag-rule.md)
* [Validar com o Debugger](validate-with-debugger.md)


## Iniciar e exibir uma sessão do Assurance

Há várias maneiras de iniciar uma sessão do Assurance.

### Iniciar uma sessão do Assurance no Debugger

Toda vez que você ativa o Edge Trace no Adobe Experience Platform Debugger, uma sessão do Assurance é iniciada em segundo plano.

Analisar como fizemos isso na lição Debugger:

1. Vá para a [Site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html) e use o depurador para [alterne a propriedade da tag no site para sua própria propriedade de desenvolvimento](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. Na navegação à esquerda de **[!UICONTROL Experience Platform Debugger]** selecionar **[!UICONTROL Logs]**
1. Selecione o **[!UICONTROL Edge]** e selecione **[!UICONTROL Conectar]**

   ![Connect Edge Trace](assets/analytics-debugger-edgeTrace.png)
1. Com o Edge Trace ativado, você pode ver um ícone de link de saída na parte superior. Selecione o ícone para abrir o Assurance. Uma nova guia no navegador é aberta.

   ![Iniciar sessão do Assurance](assets/validate-debugger-start-assurnance.png)


### Iniciar uma sessão do Assurance a partir da interface do Assurance

1. Abra o [Interface da coleção de dados](https://experience.adobe.com/#/data-collection/home){target="_blank"}
1. Selecione Assurance na navegação à esquerda
1. Selecione Criar sessão
   ![Criar uma sessão do Assurance](assets/assurance-create-session.png)
1. Selecionar Início
1. Nomeie a sessão, por exemplo, `Luma Web SDK validation`
1. Como a variável **[!UICONTROL URL base]** inserir `https://luma.enablementadobe.com/`
   ![Nomear a sessão de garantia](assets/assurance-name-session.png)
1. Na tela seguinte, selecione **[!UICONTROL Copiar link]**
1. Selecione o ícone para copiar o link para a área de transferência
1. Cole o URL em seu navegador, que abrirá o site Luma com um parâmetro de URL especial `adb_validation_sessionid` e iniciar a sessão
1. Na interface do Assurance, você deve ver uma mensagem indicando que se conectou com êxito à sessão e deve ver eventos capturados na interface do Assurance.
   ![A sessão de garantia conectou-se](assets/assurance-success.png)

## Validar o estado atual da implementação do SDK da Web

Há informações limitadas para exibir neste estágio da implementação. Um valor que podemos ver é a sua ID de Experience Cloud (ECID) gerada no Edge Network da plataforma:

1. Selecione a linha com o evento chamado Identificador de Resposta Adobe.
1. Um menu é exibido à direita. Selecione o `+` assinar ao lado de `[!UICONTROL ACPExtensionEvent]`
1. Fazer drill-down selecionando `[!UICONTROL payload > 0 > payload > 0 > namespace]`. A ID mostrada nos últimos `0` corresponde ao `ECID`. Você sabe que pelo valor que aparece em `namespace` correspondência `ECID`

   ![Garantia para validar a ECID](assets/validate-assurance-ecid.png)

   >[!CAUTION]
   >
   >Você pode ver um valor de ECID truncado devido à largura da janela. Basta selecionar a barra de alças na interface e arrastar para a esquerda para visualizar toda a ECID.

Nas lições futuras, você usa o Assurance para validar cargas totalmente processadas que chegam a um aplicativo Adobe habilitado no seu fluxo de dados.

Com um objeto XDM sendo acionado agora em uma página e sabendo como validar sua coleção de dados, você estará pronto para configurar os aplicativos de Adobe individuais usando o SDK da Web da Platform.

[Próximo: ](setup-experience-platform.md)

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Web SDK. Se você tiver dúvidas, quiser compartilhar feedback geral ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
