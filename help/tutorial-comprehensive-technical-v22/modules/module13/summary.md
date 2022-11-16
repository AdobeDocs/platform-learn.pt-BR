---
title: Ativação de segmento para o Hub de eventos do Microsoft Azure - Resumo e benefícios
description: Ativação de segmento para o Hub de eventos do Microsoft Azure - Resumo e benefícios
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 2174ac52-b5dd-4bc8-ab5f-4d84ae9ef19b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 1%

---

# Resumo e benefícios

Parabéns e obrigado por ter investido seu tempo em aprender sobre o Microsoft Azure Event Hub e o Adobe Experience Platform!
Neste módulo, você aprendeu a configurar uma instância do Hub de Eventos do Azure e a conectá-la ao Adobe Experience Platform.

## Benefícios

Vamos destacar os benefícios da integração do Adobe Experience Platform com o Microsoft Azure Event Hub:

- O Microsoft Azure Event Hubs as a Adobe Experience Platform Destination permite capturar a qualificação de segmentos em tempo real e processá-los usando uma função do Azure Event Hub. Com essa função do Hub de eventos do Azure, você pode criar qualquer tipo de manipulador de ativação de segmento personalizado e, dessa forma, integrar qualquer tipo de destino de terceiros.

- Embora os destinos sejam acionados apenas por segmentos especificados, a carga de ativação incluirá todos os segmentos para os quais determinado perfil se qualifica.

- Um segmento só aciona uma ativação quando seu status for alterado. Por exemplo, um perfil que se qualifica quatro vezes para um segmento em um período de três meses, apenas os dois primeiros serão ativados. O primeiro é uma mudança de status de para **realizado**, o segundo é acionado por uma alteração de status de **realizado** para **existente**.

- Ao ativar segmentos para perfis conhecidos, um mapa de identidade completo é incluído no payload de ativação. Sua função do Azure pode usar qualquer uma das identidades disponíveis para mapear os segmentos para um perfil gerenciado em um aplicativo de terceiros, ao usar o identificador de cliente do aplicativo.

- Neste módulo, a função do hub de eventos foi implantada localmente (modo de depuração no Visual Studio Code), oferecendo muitas opções de solução de problemas e depuração.

## Veja isso

- N/D

[Voltar ao Módulo 13](./segment-activation-microsoft-azure-eventhub.md)

[Voltar para todos os módulos](./../../overview.md)
