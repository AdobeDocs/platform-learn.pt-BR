---
title: Configuração inicial | Migrar o Target da at.js 2.x para o SDK da Web
description: Saiba mais sobre e configure os elementos fundamentais necessários para a implementação do SDK da Web da plataforma
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 2%

---

# Executar a configuração inicial da Coleta de dados

A migração da at.js para o SDK da Web da plataforma requer uma configuração inicial para habilitar a captura de dados, os recursos e as funções adequados do SDK da Web da plataforma. As etapas a seguir do [Tutorial de implementação do SDK da Web da plataforma](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=pt-BR) deve ser concluída antes de ocorrer qualquer alteração na implementação do site:

- [Configure as permissões apropriadas](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-permissions.html){target=&quot;_blank&quot;} na Adobe Admin Console para coleta de dados
- [Configurar um esquema XDM](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-schemas.html){target=&quot;_blank&quot;} para transmitir dados estruturados para a Rede de Borda
- [Configurar um namespace de identidade](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities.html){target=&quot;_blank&quot;} para personalização entre dispositivos e funcionalidade mbox3rdPartyId
- [Criar um conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-datastream.html){target=&quot;_blank&quot;} para habilitar o encaminhamento de dados da Rede de Borda
- [Configurar o fluxo de dados](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html#configure-the-datastream){target=&quot;_blank&quot;} para habilitar o encaminhamento de dados para o Adobe Target

>[!CAUTION]
>
>Lembre-se de que esses aspectos de design do SDK da Web devem ser coordenados entre as migrações do Target, do Analytics e do Audience Manager.

Quando a configuração inicial for concluída, a funcionalidade do Target deverá ser ativada usando a Rede de borda da Adobe Experience Platform.

Em seguida, saiba como [substitua a biblioteca at.js e configure uma implementação básica do SDK da Web da plataforma](replace-library.md).

>[!NOTE]
>
>Temos o compromisso de ajudar você a ser bem-sucedido com sua migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, informe-nos ao publicar em [este debate comunitário](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
