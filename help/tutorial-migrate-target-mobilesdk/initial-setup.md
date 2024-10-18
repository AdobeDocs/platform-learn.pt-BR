---
title: Configuração inicial - Migrar do Adobe Target para o Adobe Journey Optimizer - Extensão móvel de decisão
description: Saiba mais sobre e configure os elementos fundamentais importantes necessários para a implementação do SDK da Web da sua plataforma
source-git-commit: afbc8248ad81a5d9080a4fdba1167e09bbf3b33d
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Executar a configuração inicial da Coleção de dados

A migração da at.js para o SDK da Web da Platform requer uma configuração inicial para habilitar a captura de dados, os recursos e as funções adequados do SDK da Web da Platform. As seguintes etapas do [tutorial de implementação do SDK da Web da Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=pt-BR) devem ser concluídas antes que qualquer alteração na implementação do site ocorra:

- [Configure as permissões apropriadas](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/overview#prerequisites){target="_blank"} no Adobe Admin Console para a Coleção de Dados
- [Configurar um esquema XDM](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-schemas.html){target="_blank"} para transmitir dados estruturados ao Edge Network
- [Configurar um namespace de identidade](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities.html){target="_blank"} para personalização entre dispositivos e funcionalidade de mbox3rdPartyId
- [Criar uma sequência de dados](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-datastream.html){target="_blank"} para habilitar o encaminhamento de dados do Edge Network
- [Configurar a sequência de dados](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html#configure-the-datastream){target="_blank"} para habilitar o encaminhamento de dados para a Adobe Target

>[!CAUTION]
>
>Lembre-se de que esses aspectos de design devem ser coordenados entre as migrações do Target, do Analytics e do Audience Manager.

Quando a configuração inicial estiver concluída, a funcionalidade do Target deverá ser ativada usando o Edge Network Adobe Experience Platform.

Em seguida, saiba como [substituir a biblioteca at.js e configurar uma implementação básica do SDK da Web da plataforma](replace-library.md).

>[!NOTE]
>
>Estamos empenhados em ajudá-lo a ser bem-sucedido na migração para dispositivos móveis do Target da extensão do Target para a extensão do Decisioning. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
