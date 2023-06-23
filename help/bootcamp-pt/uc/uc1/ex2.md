---
title: Bootcamp - Perfil do cliente em tempo real - Visualizar seu próprio Perfil do cliente em tempo real - Interface do usuário - Brasil
description: Bootcamp - Perfil do cliente em tempo real - Visualizar seu próprio Perfil do cliente em tempo real - Interface do usuário - Brasil
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 4eebb080-77fd-4162-aa64-d599f1274c93
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 2%

---

# 1.2 Visualizar seu perfil de cliente em tempo real - UI

Neste exercício, você fará login na Adobe Experience Platform e de perfil em tempo real na UI.

## História

Não Perfil do cliente em tempo real, todos os dados do perfil são reivindicados com os dados do evento, além das tentativas de registros existentes. Os dados mostrados podem vir de qualquer lugar, de visitantes da Adobe e vigilância. Essa é a combinação mais segura da Adobe Experience Platform, o local do sistema de experiência.

## 1.2.1 Uso de um do perfil do cliente na Adobe Experience Platform

Acessado [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você acessará a página inicial da Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, você precisa atualizar um **sandbox**. O nome do sandbox a ser selecionado é Bootcamp. É possível fazer isso no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. painel de navegação o sandbox, você é a tela e agora está você em seu [!UICONTROL sandbox] Comparar.

![Assimilação de dados](./images/sb1.png)

Sem menu à esquerda, acesso **Perfis** e **Procurar**.

![Perfil do cliente](./images/homemenu.png)

No painel Visualizador de perfil no seu site, você pode encontrar a visão geral da identidade. Cada identidade está vinculada a um namespace.

![Perfil do cliente](./images/identities.png)

Não há painel Visualizador de perfil, agora você pode ver uma identidade a seguir:

| Namespace | Identidade |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 19428085896177382402834560825640259081 |

Com a Adobe Experience Platform IDs de todos os são importantes. Anµ, o ECID era o ID mais importante no contexto da Adobe e todos os outros IDs estavam vinculados ECID em uma relação hierárquica. Com a Adobe Experience Platform, isso mudou e cada ID pode ser considerado um identificador exclusivo.

, o identificador dependente do contexto. Com você alternará com seu call center: **Qual é o ID mais importante?** Eles provavelmente responderão: **o número de telefone!** Mas se você alternará à sua equipe de CRM, eles responderão: **o endereço de e-mail!** Uma Adobe Experience Platform que acompanha a experiência e gerencia isso. Um movimento ativo, um movimento ativo da Adobe ou não, se comunicará com a Adobe Experience Platform referindo-se ao ID que o principal. E simples funciona.

Pará o campo **Namespace de identidade**, **ECID** e para o campo **Valor de identidade** insira o ECID que você pode encontrar no painel Visualizador de perfil do site do Bootcamp. Clique em **Exibir**. Você verá seu perfil na lista. Clique em não **ID do perfil** para abrir seu perfil.

![Perfil do cliente](./images/popupecid.png)

Agora você tem uma visão geral de alguns **Atributos de perfil** principais do seu perfil de cliente.

![Perfil do cliente](./images/profile.png)

Acessado **Eventos**, onde você pode ver as entradas de cada evento de experiência ao perfil.

![Perfil do cliente](./images/profileee.png)

Por fim, acesse a opção de menu **Associação de segmento**. Agora você verá todos os segmentos que se qualifica para este perfil.

![Perfil do cliente](./images/profileseg.png)

Agora vamos criar um novo segmento que muda que você personaliza a experiência do cliente para um cliente anônimo ou conhecido.

Próxima etapa: [1.3 Segmento do crime - IU](./ex3.md)

[Retorno para Fluxo de monitoramento 1](./uc1.md)

[Retorno para Todos os compartilhados](../../overview.md)
