---
title: Dados do ciclo de vida
description: Saiba como coletar dados do ciclo de vida em um aplicativo móvel.
exl-id: 75b2dbaa-2f84-4b95-83f6-2f38a4f1d438
source-git-commit: b2e1bf08d9fb145ba63263dfa078c96258342708
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 2%

---

# Dados do ciclo de vida

Saiba como coletar dados do ciclo de vida em um aplicativo móvel.

A extensão de ciclo de vida do SDK do Adobe Experience Platform Mobile habilita a coleta de dados do ciclo de vida do seu aplicativo móvel. A extensão de rede de borda da Adobe Experience Platform envia esses dados do ciclo de vida para a rede de borda da Platform, onde são encaminhados para outros aplicativos e serviços de acordo com a configuração da sequência de dados. Saiba mais sobre o [Extensão de ciclo de vida](https://developer.adobe.com/client-sdks/documentation/lifecycle-for-edge-network/) na documentação do produto.


## Pré-requisitos

* O aplicativo com SDKs instalados e configurados foi criado e executado com sucesso.
* Importado o SDK do Assurance.

   ```swift
   import AEPAssurance
   ```

* Registrada a extensão do Assurance conforme descrito no [lição anterior](install-sdks.md).

## Objetivos de aprendizagem

Nesta lição, você vai:

* Adicionar grupo de campos de ciclo de vida ao esquema.
* Ative métricas de ciclo de vida precisas iniciando/pausando corretamente à medida que o aplicativo se move entre o primeiro e o segundo plano.
* Envie dados do aplicativo para a Platform Edge Network.
* Validar no Assurance.

## Adicionar grupo de campos do ciclo de vida ao esquema

O grupo de campos Evento de experiência do consumidor adicionado no [lição anterior](create-schema.md) já contém os campos de ciclo de vida, portanto, você pode ignorar esta etapa. Se você não usar o grupo de campos Evento de experiência do consumidor em seu próprio aplicativo, poderá adicionar os campos de ciclo de vida fazendo o seguinte:

1. Navegue até a interface do esquema conforme descrito na seção [lição anterior](create-schema.md).
1. Abra o esquema &quot;Aplicativo Luma&quot; e selecione **[!UICONTROL Adicionar]**.
   ![selecione adicionar](assets/mobile-lifecycle-add.png)
1. Na barra de pesquisa, digite &quot;lifecycle&quot;.
1. Marque a caixa de seleção ao lado de **[!UICONTROL Detalhes do ciclo de vida do AEP Mobile]**.
1. Selecione **[!UICONTROL Adicionar grupos de campos]**.
   ![adicionar grupo de campos](assets/mobile-lifecycle-lifecycle-field-group.png)
1. Selecione **[!UICONTROL Salvar]**.
   ![save](assets/mobile-lifecycle-lifecycle-save.png)


## Alterações de implementação

Agora você pode atualizar `AppDelegate.swift` para registrar os eventos do ciclo de vida:

1. Quando iniciado, se o aplicativo sair do estado em segundo plano, o iOS pode chamar o `applicationWillEnterForeground:` método delegado. Add `lifecycleStart:`

   ```swift
   MobileCore.lifecycleStart(additionalContextData: nil)
   ```

1. Quando o aplicativo entrar em segundo plano, pause a coleta de dados do ciclo de vida no `applicationDidEnterBackground:` método delegado.

   ```swift
   MobileCore.lifecyclePause()
   ```

>[!NOTE]
>
>Para o iOS 13 e posterior, revise o [documentação](https://developer.adobe.com/client-sdks/documentation/mobile-core/lifecycle/#register-lifecycle-with-mobile-core-and-add-appropriate-startpause-calls) para um código ligeiramente diferente.

## Validar com garantia

1. Revise o [instruções de configuração](assurance.md) e conecte seu simulador ou dispositivo ao Assurance.
1. Inicie o aplicativo.
1. Envie o aplicativo para o plano de fundo. Verificar `LifecyclePause`.
1. Coloque o aplicativo em primeiro plano. Verificar `LifecycleResume`.
   ![validar ciclo de vida](assets/mobile-lifecycle-lifecycle-assurance.png)


## Encaminhar dados para a Rede de borda da plataforma

O exercício anterior despacha os eventos em primeiro e segundo plano para o SDK móvel. Para enviar esses eventos para a Platform Edge Network, siga as etapas listadas [aqui](https://developer.adobe.com/client-sdks/documentation/lifecycle-for-edge-network/#configure-a-rule-to-forward-lifecycle-metrics-to-platform). Depois que os eventos forem enviados à Platform Edge Network, eles serão encaminhados a outros aplicativos e serviços de acordo com a configuração do fluxo de dados.

Depois de adicionar a regra para enviar os eventos de ciclo de vida à Platform Edge Network, você deverá ver `Application Close (Background)` e `Application Launch (Foreground)` eventos que contêm dados XDM no Assurance.

![validar ciclo de vida enviado ao Platform Edge](assets/mobile-lifecycle-edge-assurance.png)



Próximo: **[Rastrear eventos](events.md)**

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar feedback geral ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)