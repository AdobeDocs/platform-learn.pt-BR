---
title: Bootcamp - Real-time Customer Profile - Visualize seu próprio Perfil do cliente em tempo real - UI
description: Bootcamp - Real-time Customer Profile - Visualize seu próprio Perfil do cliente em tempo real - UI
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 4c810767-00ab-4cae-baa9-97b0cb9bf2df
source-git-commit: ead28f5631fc430c41e8c756b23dc69ffe19510e
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 2%

---

# 1.2 Visualizar seu próprio Perfil do cliente em tempo real - Interface do usuário

Neste exercício, você fará logon na Adobe Experience Platform e visualizará seu próprio Perfil do cliente em tempo real na interface do usuário do .

## História

No Perfil do cliente em tempo real, todos os dados do perfil são mostrados junto aos dados do evento, bem como às associações de segmento existentes. Os dados mostrados podem vir de qualquer lugar, de aplicativos Adobe e soluções externas. Essa é a exibição mais poderosa no Adobe Experience Platform, o verdadeiro sistema de experiência de registro.

## 1.2.1 Usar a exibição de perfil do cliente no Adobe Experience Platform

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você será direcionado para a página inicial do Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, é necessário selecionar um **sandbox**. A sandbox a ser selecionada é chamada de ``Bootcamp``. Você pode fazer isso clicando no texto **[!UICONTROL Produto de produção]** na linha azul na parte superior da tela. Depois de selecionar a [!UICONTROL sandbox], você verá a tela mudar e agora você estará em seu [!UICONTROL sandbox].

![Assimilação de dados](./images/sb1.png)

No menu esquerdo, acesse **Perfis** e **Procurar**.

![Perfil do cliente](./images/homemenu.png)

No painel Visualizador de perfil do seu site, você pode encontrar a visão geral da identidade. Cada identidade está vinculada a um namespace.

![Perfil do cliente](./images/identities.png)

No painel Visualizador de perfil, você pode ver essa identidade atualmente:

| Namespace | Identidade |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 19428085896177382402834560825640259081 |

Com o Adobe Experience Platform, todas as IDs são igualmente importantes. Anteriormente, a ECID era a ID mais importante no contexto de Adobe e todas as outras IDs estavam vinculadas à ECID em uma relação hierárquica. Com o Adobe Experience Platform, esse não é mais o caso e cada ID pode ser considerada um identificador principal.

Normalmente, o identificador principal depende do contexto. Caso pergunte ao seu Call Center, **Qual é a ID mais importante?** provavelmente responderão. **o número de telefone!** Mas se você perguntar a sua equipe de CRM, eles responderão, **O endereço de email!**  A Adobe Experience Platform entende essa complexidade e a gerencia para você. Cada aplicativo, seja ele Adobe ou não, falará com a Adobe Experience Platform fazendo referência à ID que considera primária. E simplesmente funciona.

Para o campo **Namespace de identidade**, selecione **ECID** e para o campo **Valor de identidade** insira a ECID que você pode encontrar no painel Visualizador de perfil do site de bootcamp. Clique em **Exibir**. Em seguida, você verá seu perfil na lista. Clique no botão **ID do perfil** para abrir o perfil.

![Perfil do cliente](./images/popupecid.png)

Agora você vê uma visão geral de alguns **Atributos do perfil** do seu perfil de cliente.

![Perfil do cliente](./images/profile.png)

Ir para **Eventos**, onde é possível ver entradas para cada evento de experiência vinculado ao seu Perfil.

![Perfil do cliente](./images/profileee.png)

Finalmente, acesse a opção de menu **Associação de segmento**. Agora você verá todos os segmentos qualificados para este perfil.

![Perfil do cliente](./images/profileseg.png)

Agora vamos criar um novo segmento que permitirá personalizar a experiência do cliente para um cliente anônimo ou conhecido.

Próxima etapa: [1.3 Criar um segmento - Interface do usuário](./ex3.md)

[Voltar para Fluxo de Usuário 1](./uc1.md)

[Voltar para todos os módulos](../../overview.md)
