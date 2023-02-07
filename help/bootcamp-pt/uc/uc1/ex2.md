---
title: Bootcamp - Real-time Customer Profile - Visualize seu próprio Perfil do cliente em tempo real - UI - Brasil
description: Bootcamp - Real-time Customer Profile - Visualize seu próprio Perfil do cliente em tempo real - UI - Brasil
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 5d824244766135cd4998feab48be7f6a69c42a70
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 2%

---

# 1.2 Visualizar seu inimigo de cliente em tempo real - IU

Você faz o logon na Adobe Experience Platform e visualizar, no perfil em tempo.

## História

Nenhum Perfil do cliente em tempo real, todos os dados do são exibidos são juntamente com o evento das associações de segmentos existentes. Os dados mostrados podem vir de qualquer lugar, de aplicativos da Adobe e soluções. Essa é uma exibição mais poderosa da Adobe Experience Platform, ou verdadeiro local do experiência.

## 1.2.1 Uso de um visualização do cliente na Adobe Experience Platform

Acesse [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de &quot;Faça&quot;, você vai acessar um início do logon no Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, você precisa selecionar um **sandbox**. O nome faz sandbox a ser selecionado é Bootcamp. É possível isto clicando texto **[!UICONTROL Produto de produção]** na linha azul na parte superior da tela. Depois de selecionar o sandbox apropriado, você verá a tela mudando e agora está em sua [!UICONTROL sandbox] dedicado.

![Assimilação de dados](./images/sb1.png)

Sem menu à esquerda, acesse **Perfis** e **Procurar**.

![Perfil do cliente](./images/homemenu.png)

Não painel Visualizador de nenhum site, você está  a visão geral da identidade. Cada identidade está vinculada um namespace.

![Perfil do cliente](./images/identities.png)

Não painel Visualizador de, agora você pode ver uma semelhante a seguinte:

| Namespace | Identidade |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 19428085896177382402834560825640259081 |

Com uma Adobe Experience Platform, todos os os IDs são igualmente importantes. Anteriormente, a ECID era o ID mais importante no contexto do Adobe e os outros IDs estavam ao ECID em uma hierárqu ica. Com uma Adobe Experience Platform, Mudou e cada ID considerado um identificador primário.

Normalmente, identificador primário depende fazer. Consulte você ao seu Call Center: **Qual é o ID mais importante?** Eles provavelmente responderão: **Número de telefone!** Mas se você à sua equipe de CRM, eles responderão: **o endereço de e-mail!** Uma Adobe Experience Platform entende essa complexidade e gerenci a isso para você. Cada aplicativo, Um aplicativo da Adobe ou, comunicará com um Adobe Experience Platform referindo-se ao consideram principal. E simplesmente funciona.

Para o campo **Namespace de identidade** selecione **ECID** e para o campo **Valor de identidade** insira na ECID você não pode painel Visualizador do site de Bootcamp. Clique em **Exibir**. Você está com você. Clique em **ID do perfil** Para você.

![Perfil do cliente](./images/popupecid.png)

Agora você tem uma visão geral de alguns **Os atributos de renda** importantes de seu inimigo.

![Perfil do cliente](./images/profile.png)

Acesse **Eventos**, onde você pode ver como entradas de cada evento de experiência ao seu Perfil.

![Perfil do cliente](./images/profileee.png)

Por fim, acesse o menu de **Associação de segmento**. Agora, você todos os seus conhecimentos para o segmentos.

![Perfil do cliente](./images/profileseg.png)

Agora que você é um segmento que permitirá um cliente do cliente para anôn imo ou conhecido.

Proxima. [1.3 Segmento de Crie - Interface do usuário](./ex3.md)

[Retornar para Fluxo de Correio](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
