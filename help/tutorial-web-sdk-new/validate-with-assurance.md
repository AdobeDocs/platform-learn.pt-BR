---
title: Validar implementações do SDK da Web com o Experience Platform Assurance
description: Saiba como validar a implementação do SDK da Web da sua plataforma com o Adobe Experience Platform Assurance. Esta lição é parte do tutorial Implementar o Adobe Experience Cloud com o SDK da Web.
feature: Web SDK,Tags,Assurance
source-git-commit: 4361d8e688ff2c2f3b5472f2cfff246efa627c7f
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---

# Validar implementações do SDK da Web com o Experience Platform Assurance


## Iniciar uma sessão do Assurance

O Adobe Experience Platform Assurance é um produto da Adobe Experience Cloud que ajuda a inspecionar, testar, simular e validar a maneira como você coleta dados ou fornece experiências.

Leia mais sobre [Adobe Assurance](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=en).

Toda vez que você ativa o Edge Trace, uma sessão do Assurance é iniciada em segundo plano.

Para exibir a sessão do Assurance,

1. Com o Edge Trace ativado, você pode ver um ícone de link de saída na parte superior. Selecione o ícone para abrir o Assurance. Uma nova guia no navegador é aberta.

   ![Iniciar sessão do Assurance](assets/validate-debugger-start-assurnance.png)

1. Selecione a linha com o evento chamado Identificador de Resposta Adobe.
1. Um menu é exibido à direita. Selecione o `+` assinar ao lado de `[!UICONTROL ACPExtensionEvent]`
1. Fazer drill-down selecionando `[!UICONTROL payload > 0 > payload > 0 > namespace]`. A ID mostrada nos últimos `0` corresponde ao `ECID`. Você sabe que pelo valor que aparece em `namespace` correspondência `ECID`

   ![Garantia para validar a ECID](assets/validate-assurance-ecid.png)

   >[!CAUTION]
   >
   >Você pode ver um valor de ECID truncado devido à largura da janela. Basta selecionar a barra de alças na interface e arrastar para a esquerda para visualizar toda a ECID.

Nas lições futuras, você usa o Assurance para validar cargas totalmente processadas que chegam a um aplicativo Adobe habilitado no seu fluxo de dados.

Com um objeto XDM sendo acionado agora em uma página e sabendo como validar sua coleção de dados, você estará pronto para configurar os aplicativos de Adobe individuais usando o SDK da Web da Platform.