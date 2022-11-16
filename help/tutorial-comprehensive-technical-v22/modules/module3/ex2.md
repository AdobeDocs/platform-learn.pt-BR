---
title: Foundation - Perfil do cliente em tempo real - Visualize seu próprio Perfil do cliente em tempo real - Interface do usuário
description: Foundation - Perfil do cliente em tempo real - Visualize seu próprio Perfil do cliente em tempo real - Interface do usuário
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: ed13e37f-48eb-4668-b828-6c58340a7cc1
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 2%

---

# 3.2 Visualizar seu próprio Perfil do cliente em tempo real - Interface do usuário

Neste exercício, você fará logon na Adobe Experience Platform e visualizará seu próprio Perfil do cliente em tempo real na interface do usuário do .

## História

No Perfil do cliente em tempo real, todos os dados do perfil são mostrados junto aos dados do evento, bem como às associações de segmento existentes. Os dados mostrados podem vir de qualquer lugar, de aplicativos Adobe e soluções externas. Essa é a exibição mais poderosa no Adobe Experience Platform, o verdadeiro sistema de experiência de registro.

## 3.2.1 Usar a visualização do perfil do cliente no Adobe Experience Platform

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você será direcionado para a página inicial do Adobe Experience Platform.

![Assimilação de dados](../module2/images/home.png)

Antes de continuar, é necessário selecionar um **sandbox**. A sandbox a ser selecionada é chamada de ``--aepSandboxId--``. Você pode fazer isso clicando no texto **[!UICONTROL Produto de produção]** na linha azul na parte superior da tela. Depois de selecionar a [!UICONTROL sandbox], você verá a tela mudar e agora você estará em seu [!UICONTROL sandbox].

![Assimilação de dados](../module2/images/sb1.png)

No menu esquerdo, acesse **Perfis** e **Procurar**.

![Perfil do cliente](./images/homemenu.png)

No painel Visualizador de perfil do seu site, você pode encontrar várias identidades. Cada identidade é vinculada a um namespace.

![Perfil do cliente](./images/identities.png)

No painel Visualizador de perfil, você pode ver essas combinações de IDs e namespaces:

| Identidade | Namespace |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 1250756068732495704459439363261812234 |
| ID de email | woutervangeluwe+06022022-01@gmail.com |
| ID do número do dispositivo móvel | +32473622044+06022022-01 |

Com o Adobe Experience Platform, todas as IDs são igualmente importantes. Anteriormente, a ECID era a ID mais importante no contexto de Adobe e todas as outras IDs estavam vinculadas à ECID em uma relação hierárquica. Com o Adobe Experience Platform, esse não é mais o caso e cada ID pode ser considerada um identificador principal.

Normalmente, o identificador principal depende do contexto. Caso pergunte ao seu Call Center, **Qual é a ID mais importante?** provavelmente responderão. **o número de telefone!** Mas se você perguntar a sua equipe de CRM, eles responderão, **O endereço de email!**  A Adobe Experience Platform entende essa complexidade e a gerencia para você. Cada aplicativo, seja ele Adobe ou não, falará com a Adobe Experience Platform fazendo referência à ID que considera primária. E simplesmente funciona.

Para o campo **Namespace de identidade**, selecione **Email** e para o campo **Valor de identidade** insira o endereço de email usado para se registrar no exercício anterior. Clique em **Exibir**. Em seguida, você verá seu perfil na lista. Clique no botão **ID do perfil** para abrir o perfil.

![Perfil do cliente](./images/popupecid.png)

Agora você vê uma visão geral de alguns **Atributos do perfil** do seu perfil de cliente.

![Perfil do cliente](./images/profile.png)

Se quiser ver todos os atributos de perfil disponíveis para o seu perfil, acesse **Atributos**.

![Perfil do cliente](./images/profilattr.png)

Ir para **Eventos**, onde é possível ver entradas para cada evento de experiência vinculado ao seu Perfil.

![Perfil do cliente](./images/profileee.png)

Finalmente, acesse a opção de menu **Associação de segmento**. Agora você verá todos os segmentos qualificados para este perfil.

![Perfil do cliente](./images/profileseg.png)

Agora que você aprendeu a visualizar o perfil em tempo real de qualquer cliente usando a interface do usuário do Adobe Experience Platform, vamos fazer o mesmo por meio das APIs, usando o Postman e o Adobe I/O para consultar as APIs do Adobe Experience Platform.

Próxima etapa: [3.3 Visualizar seu próprio perfil de cliente em tempo real - API](./ex3.md)

[Voltar ao Módulo 3](./real-time-customer-profile.md)

[Voltar para todos os módulos](../../overview.md)
