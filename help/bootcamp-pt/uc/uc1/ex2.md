---
title: Bootcamp - Perfil do cliente em tempo real - Visualizar seu próprio Perfil do cliente em tempo real - Interface do usuário - Brasil
description: Bootcamp - Perfil do cliente em tempo real - Visualizar seu próprio Perfil do cliente em tempo real - Interface do usuário - Brasil
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 4eebb080-77fd-4162-aa64-d599f1274c93
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 1%

---

# 1.2 Visualizar seu perfil de cliente em tempo real - UI

Neste exercício, você fará login na Adobe Experience Platform e de perfil em tempo real na UI.

## História

Não Perfil do cliente em tempo real, todos os dados do perfil são reivindicados com os dados do evento, além das tentativas de registros existentes. Os dados mostrados podem vir de qualquer lugar, de visitantes da Adobe e vigilância. Essa é a combinação mais segura da Adobe Experience Platform, o local do sistema de experiência.

## 1.2.1 Uso de um do perfil do cliente na Adobe Experience Platform

Acessado [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você acessará a página inicial da Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, você seleciona **sandbox**. O nome do sandbox a ser selecionado é Bootcamp. É possível fazer isso no texto **[!UICONTROL Produção Prod]** na linha azul na parte superior da tela. Depois de pegar a sandbox, você verá a tela e agora você está em seu [!UICONTROL sandbox].

![Assimilação de dados](./images/sb1.png)

Nenhum menu à esquerda, acessado **Perfis** e **Procurar**.

![Perfil do cliente](./images/homemenu.png)

No painel Visualizador de perfil no seu site, você pode encontrar a visão geral da identidade. Cada identidade está vinculada a um namespace.

![Perfil do cliente](./images/identities.png)

No painel Visualizador de perfil, agora você pode ver uma identidade próxima a seguinte:

| Namespace | Identidade |
|:-------------:| :---------------:|
| ID Experience Cloud (ECID) | 19428085896177382402834560825640259081 |

Com a Adobe Experience Platform IDs de todos os são importantes. Anµ, o ECID era o ID mais importante no contexto da Adobe e todos os outros IDs estavam vinculados ECID em uma relação hierárquica. Com a Adobe Experience Platform, isso mudou e cada ID pode ser considerado um identificador exclusivo.

, o identificador dependente do contexto. Se você alternar com seu Call Center: **Qual é o ID mais Importante?** Provavelmente responderão: **o número de telefone!** Mas se você tem a sua equipe de CRM, eles responderão: **o endereço de e-mail!** A Adobe Experience Platform pega essa mudança e gerencia isso para. Um movimento ativo, um movimento ativo da Adobe ou não, se comunicará com a Adobe Experience Platform referindo-se ao ID que o principal. E simples funciona.

Para o campo **Namespace de identidade**, **ECID** e para o campo **Valor de identidade** dentro do ECID que você pode encontrar no painel Visualizador de perfil do site do Bootcamp. Clique em **Exibir**. Você verá seu perfil na lista. Clique em **ID do Perfil** para abrir seu perfil.

![Perfil do cliente](./images/popupecid.png)

Agora você uma visão geral de alguns **Atributos de perfil** principais do seu perfil de cliente.

![Perfil do cliente](./images/profile.png)

Acessado **Eventos**, onde você pode ver as entradas de cada evento de experiência vinculado ao seu Perfil.

![Perfil do cliente](./images/profileee.png)

Por fim, acesse a opção de menu **Segmento de afiliação**. Agora você verá todos os segmentos que se qualifica para este perfil.

![Perfil do cliente](./images/profileseg.png)

Agora vamos criar um novo segmento que muda que você personaliza a experiência do cliente para um cliente anônimo ou conhecido.

Próxima etapa: [1.3 Segmento de um crime - IU](./ex3.md)

[Retorno para Fluxo de monitoramento 1](./uc1.md)

[Retorno para Todos os compartilhados](../../overview.md)
