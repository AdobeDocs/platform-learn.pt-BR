---
title: Bootcamp - Perfil do cliente em tempo real - Visualizar seu próprio Perfil do cliente em tempo real - Interface do usuário
description: Bootcamp - Perfil do cliente em tempo real - Visualizar seu próprio Perfil do cliente em tempo real - Interface do usuário
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 4c810767-00ab-4cae-baa9-97b0cb9bf2df
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# 1.2 Visualizar seu próprio Perfil de cliente em tempo real - Interface do usuário

Neste exercício, você fará logon no Adobe Experience Platform e visualizará seu próprio Perfil de cliente em tempo real na interface do.

## Story

No Perfil do cliente em tempo real, todos os dados do perfil são mostrados junto com os dados do evento, bem como com as associações de público-alvo existentes. Os dados mostrados podem vir de qualquer lugar, de aplicativos Adobe e soluções externas. Essa é a visualização mais eficiente no Adobe Experience Platform, o verdadeiro sistema de experiência de registro.

## 1.2.1 Usar a visualização de perfil do cliente no Adobe Experience Platform

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``Bootcamp``. Você pode fazer isso clicando no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. Depois de selecionar a [!UICONTROL sandbox] apropriada, você verá a alteração da tela e agora estará na [!UICONTROL sandbox] dedicada.



No menu esquerdo, vá para **Perfis** e para **Procurar**.

![Perfil do cliente](./images/homemenu.png)

No painel Visualizador de perfis do seu site, você pode encontrar a visão geral da identidade. Cada identidade está vinculada a um namespace.

![Perfil do cliente](./images/identities.png)




Com o Adobe Experience Platform, todas as IDs são igualmente importantes. Anteriormente, a ECID era a ID mais importante no contexto do Adobe e todas as outras IDs estavam vinculadas à ECID em uma relação hierárquica. Com o Adobe Experience Platform, esse não é mais o caso e cada ID pode ser considerada um identificador principal.

Normalmente, o identificador principal depende do contexto. Se você perguntar à Central de Atendimento, **Qual é a ID mais importante?** eles provavelmente responderão, **o número do telefone!** Mas se você perguntar à sua equipe de CRM, ela responderá: **O endereço de email!O** Adobe Experience Platform entende essa complexidade e a gerencia para você. Todos os aplicativos, sejam eles de Adobe ou não Adobe, falarão com a Adobe Experience Platform referindo-se à ID que eles consideram primária. E simplesmente funciona.

Para o campo **Namespace de identidade**, selecione **ECID** e, para o campo **Valor de identidade**, insira a ECID que você pode encontrar no painel Visualizador de Perfis do site de bootcamp. Clique em **Exibir**. Você verá seu perfil na lista. Clique na **ID do Perfil** para abrir seu perfil.

![Perfil do cliente](./images/popupecid.png)

Você agora está vendo uma visão geral de alguns **Atributos do perfil** importantes do seu perfil de cliente.

![Perfil do cliente](./images/profile.png)

Vá para **Eventos**, onde você pode ver entradas para cada evento de experiência vinculado ao seu Perfil.

![Perfil do cliente](./images/profileee.png)

Finalmente, vá para a opção de menu **Audience association**. Agora você verá todos os públicos-alvo qualificados para este perfil.

![Perfil do cliente](./images/profileseg.png)

Agora vamos criar um novo público-alvo que permitirá personalizar a experiência do cliente para um cliente anônimo ou conhecido.

Próxima Etapa: [1.3 Criar um público-alvo - Interface do Usuário](./ex3.md)

[Voltar para Fluxo de Usuário 1](./uc1.md)

[Voltar a todos os módulos](../../overview.md)
