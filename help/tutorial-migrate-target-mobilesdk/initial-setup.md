---
title: Configuração inicial - Migrar do Adobe Target para o Adobe Journey Optimizer - Extensão móvel de decisão
description: Saiba mais sobre e configure os elementos fundamentais importantes necessários para a implementação do Platform Web SDK
exl-id: dfc5abc8-0e79-454a-b1bb-6a42b1219771
source-git-commit: a928fb5c8e48e71984b75faf4eb397814caac6aa
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 5%

---

# Executar a configuração inicial da Coleção de dados

A migração do Target SDK para o Otimize SDK requer uma configuração inicial para habilitar a captura de dados, os recursos e as funções adequados do Otimize SDK. As etapas a seguir devem ser concluídas antes que qualquer alteração na implementação do site ocorra:

- [Configure as permissões apropriadas](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/overview#permissions){target="_blank"} no Adobe Admin Console para a Coleção de Dados
- [Configurar um esquema XDM](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-schema){target="_blank"} para transmitir dados estruturados à Edge Network
- [Configurar o esquema](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-your-schema){target="_blank"} para receber dados do Adobe Target
- [Configurar um namespace de identidade](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/app-implementation/identity#set-up-a-custom-identity-namespace){target="_blank"} para personalização entre dispositivos e funcionalidade de mbox3rdPartyId
- [Criar uma sequência de dados](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-datastream){target="_blank"} para habilitar o encaminhamento de dados do Edge Network
- [Configurar a sequência de dados](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-datastream-configuration){target="_blank"} para habilitar o encaminhamento de dados para a Adobe Target
- [Configurar a propriedade Tag](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#install-adobe-journey-optimizer---decisioning-tags-extension){target="_blank"} para a extensão de Decisão

>[!BEGINTABS]

>[!TAB Extensão de decisão]

Extensões de tag instaladas ao usar a extensão do Decisioning:

1. Adobe Journey Optimizer - Decisão
1. Adobe Experience Platform Edge Network
1. Mobile Core
1. Perfil
1. Consentimento
1. Identidade
1. AEP Assurance (opcional, necessário para depuração)

![Extensões de marca instaladas ao usar a extensão de Decisão](assets/tag-extensions-decisioning.png)

>[!TAB Extensão do Target]

Extensões de tag instaladas ao usar a extensão do Target:

1. Adobe Target
1. Mobile Core
1. Perfil
1. Adobe Analytics (opcional, necessário se estiver usando o Adobe Analytics como fonte de relatórios para atividades do Adobe Target)

![Extensões de marca instaladas ao usar a extensão do Target](assets/tag-extensions-target.png)

>[!ENDTABS]

Em seguida, saiba como [substituir o SDK do Target](replace-library.md).

>[!NOTE]
>
>Estamos empenhados em ajudá-lo a ser bem-sucedido na migração para dispositivos móveis do Target da extensão do Target para a extensão do Decisioning. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
