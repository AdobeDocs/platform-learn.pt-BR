---
title: Configuração inicial - Migrar a implementação do Adobe Target no aplicativo móvel para a extensão do Offer Decisioning e do Target
description: Saiba mais sobre e configure os elementos fundamentais importantes necessários para a implementação do Platform Web SDK
exl-id: dfc5abc8-0e79-454a-b1bb-6a42b1219771
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 6%

---

# Executar a configuração inicial da Coleção de dados

A migração do Target SDK para o Otimize SDK requer uma configuração inicial para habilitar a captura de dados, os recursos e as funções adequados do Otimize SDK. As seguintes etapas devem ser concluídas antes de qualquer alteração na implementação do aplicativo móvel ocorrer:

- [Configure as permissões apropriadas](https://experienceleague.adobe.com/pt-br/docs/platform-learn/implement-web-sdk/overview#permissions){target="_blank"} no Adobe Admin Console para a Coleção de Dados
- [Configurar um esquema XDM](https://experienceleague.adobe.com/pt-br/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-schema){target="_blank"} para transmitir dados estruturados à Edge Network
- [Configurar o esquema](https://experienceleague.adobe.com/pt-br/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-your-schema){target="_blank"} para receber dados do Adobe Target
- [Configurar um namespace de identidade](https://experienceleague.adobe.com/pt-br/docs/platform-learn/implement-mobile-sdk/app-implementation/identity#set-up-a-custom-identity-namespace){target="_blank"} para personalização entre dispositivos e funcionalidade de mbox3rdPartyId
- [Criar uma sequência de dados](https://experienceleague.adobe.com/pt-br/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-datastream){target="_blank"} para habilitar o encaminhamento de dados do Edge Network
- [Configurar a sequência de dados](https://experienceleague.adobe.com/pt-br/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-datastream-configuration){target="_blank"} para habilitar o encaminhamento de dados para a Adobe Target
- [Configure a propriedade Tag](https://experienceleague.adobe.com/pt-br/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#install-adobe-journey-optimizer---decisioning-tags-extension){target="_blank"} para a extensão do Offer Decisioning e do Target

## Configuração de extensão

>[!BEGINTABS]

>[!TAB Extensão do Offer Decisioning e do Target]

Extensões de tag instaladas ao usar a extensão do Offer Decisioning e do Target:

1. Offer Decisioning e Target
1. Adobe Experience Platform Edge Network
1. Mobile Core
1. Perfil
1. Consentimento
1. Identidade
1. AEP Assurance (opcional, necessário para depuração)

![Extensões de marca instaladas ao usar a extensão do Offer Decisioning e do Target](assets/tag-extensions-decisioning.png)

>[!TAB Extensão do Target]

Extensões de tag instaladas ao usar a extensão do Target:

1. Adobe Target
1. Mobile Core
1. Perfil
1. Adobe Analytics (opcional, necessário se estiver usando o Adobe Analytics como fonte de relatórios para atividades do Adobe Target)

![Extensões de marca instaladas ao usar a extensão do Target](assets/tag-extensions-target.png)

>[!ENDTABS]

## Configuração da sequência de dados

A extensão de Destino tem [configurações configuráveis](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui) que com a extensão de Decisão são [configuradas na sequência de dados](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#adobe-experience-platform-data-collection-setup).

| Extensão do Target | Extensão do Offer Decisioning e do Target | Notas |
| --- | --- | --- | 
| Código do cliente | n/d | Definido automaticamente pela borda usando os detalhes da Organização IMS |
| ID do ambiente | ID do ambiente de destino | Configurado na sequência de dados |
| Propriedade do Workspace de destino | Token de propriedade | Configurado na sequência de dados |
| Tempo limite | Tempo limite | Configurável na extensão do Offer Decisioning e do Target e em Otimizar SDK. O tempo limite padrão é de 10 segundos. |
| Domínio do servidor | Domínio do Edge Network | Definido na extensão do Adobe Experience Platform Edge Network |

Em seguida, saiba como [substituir o SDK do Target](replace-sdk.md).

>[!NOTE]
>
>Estamos empenhados em ajudá-lo a ser bem-sucedido na migração para dispositivos móveis do Target da extensão do Target para a extensão do Offer Decisioning e do Target. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484?profile.language=pt#M625).
