---
title: Foundation - Configuração da coleta de dados do Adobe Experience Platform e da extensão do SDK da Web - Explicando a coleta de dados do Adobe Experience Platform
description: Foundation - Configuração da coleta de dados do Adobe Experience Platform e da extensão do SDK da Web - Explicando a coleta de dados do Adobe Experience Platform
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: f498bb8c-659c-44b4-bb2e-36ea14640773
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 6%

---

# 1.1 Noções básicas sobre a coleta de dados do Adobe Experience Platform

## Contexto

A Coleta de dados do Adobe Experience Platform é usada por marcas para vários casos de uso. É um sistema Tag Management (TMS) de próxima geração que oferece aos clientes uma forma simples de implantar e gerenciar todas as soluções de análise, marketing e publicidade necessárias para potencializar experiências de cliente relevantes. Não há custo adicional para a coleta de dados da Adobe Experience Platform e ela está disponível para qualquer cliente da Adobe Experience Cloud. Uma marca pode usar a Coleta de dados do Adobe Experience Platform para:

- Implemente aplicativos Adobe Experience Cloud e Adobe Experience Platform.
- Gerenciar os diferentes requisitos de diferentes partes da organização fornecendo a cada uma delas seus próprios **Propriedade** para gerenciar.
- Permitir testes e gerenciamento do ciclo de vida.
- Insira javascript personalizado e tags de terceiros, todos gerenciados em um único lugar.

## Explore a interface do usuário

Ir para [Coleta de dados do Adobe Experience Platform](https://experience.adobe.com/#/data-collection/).

Ir para **Tags**. Agora você está vendo o **[!UICONTROL Propriedades]** exibir. As propriedades listadas aqui são para o gerenciamento de tutoriais. Essas propriedades representam...

- Propriedades do aplicativo e da Web
- Sites diferentes servindo clientes de maneiras diferentes. Por exemplo, Luma Retail teria uma propriedade, Luma Travel teria outra
- Sites herdados e atuais
- Um design específico do Adobe Analytics comum a vários sites diferentes
- Páginas internas da intranet ao lado de sites externos

![Exibir propriedades do Launch](./images/launch1.png)

Agora, dê uma olhada no painel esquerdo.

![Iniciar painel esquerdo](./images/launch2.png)

- **[!UICONTROL Tags]** fornece uma visão geral de todas as propriedades do lado do cliente
- **[!UICONTROL Superfícies do aplicativo]** fornece uma visão geral de todas as configurações do aplicativo para ativar as notificações por push (que são usadas/ativadas em combinação com o Project Sierra)
- **[!UICONTROL Datastreams]** são exploradas no [próximo exercício](./ex2.md)
- **[!UICONTROL Encaminhamento de evento]** fornece uma visão geral de todas as propriedades do lado do servidor que são exploradas no [Módulo 14 - Conexões Real-Time CDP: Encaminhamento de evento](../module14/aep-data-collection-ssf.md)

## Informações adicionais

A Coleta de dados do Adobe Experience Platform é uma ferramenta muito avançada com escopo além de um tutorial do Adobe Experience Platform. As empresas podem não usar a Coleta de dados do Adobe Experience Platform em seus recursos de gerenciamento de tags e, em vez disso, usar soluções de gerenciamento de tags que não sejam do Adobe para injetar código e gerenciar tags. O uso de uma solução de gerenciamento de tags que não seja do Adobe é compatível com o Adobe e a Adobe Professional Services.
Algumas outras leituras para os interessados em entender a Coleta de dados da Adobe Experience Platform estão incluídas abaixo.

- [Guia do usuário de coleta de dados do Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)
- [Implementar a Adobe Experience Cloud com o tutorial do SDK da web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=pt-BR)
- [Configurar permissões do usuário](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html)
- [Documentação da API](https://developer.adobelaunch.com/api/)

Próxima etapa: [1.2 Rede de borda, conjuntos de dados e coleta de dados do lado do servidor](./ex2.md)

[Voltar ao Módulo 1](./data-ingestion-launch-web-sdk.md)

[Voltar para todos os módulos](./../../overview.md)
