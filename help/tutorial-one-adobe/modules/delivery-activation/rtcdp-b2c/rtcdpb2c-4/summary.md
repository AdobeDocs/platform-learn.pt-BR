---
title: Audience Activation para o Hub de eventos do Microsoft Azure - Resumo e benefícios
description: Audience Activation para o Hub de eventos do Microsoft Azure - Resumo e benefícios
kt: 5342
doc-type: tutorial
exl-id: f081af11-3ea0-47cc-ae74-24a0e0231d66
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 1%

---

# Resumo e benefícios

Parabéns e obrigado por investir seu tempo aprendendo sobre o Hub de Eventos do Microsoft Azure e o Adobe Experience Platform.
Neste módulo, você aprendeu a configurar uma instância do Azure Event Hub e como conectá-la ao Adobe Experience Platform.

## Benefícios

Vamos destacar os benefícios da integração do Adobe Experience Platform com o Hub de eventos do Microsoft Azure:

- Os Hubs de eventos do Microsoft Azure como um Destino do Adobe Experience Platform permitem capturar a qualificação de público-alvo em tempo real e processá-los usando uma função do Hub de eventos do Azure. Com essa função do Hub de eventos do Azure, você pode criar qualquer tipo de manipulador de ativação de público-alvo personalizado e, como tal, integrar qualquer tipo de destino de terceiros.

- Embora os destinos sejam acionados somente por públicos-alvo especificados, a carga de ativação incluirá todos os públicos-alvo para os quais determinado perfil se qualifica.

- Um público-alvo só aciona uma ativação quando seu status é alterado. Por exemplo, um perfil que se qualifica quatro vezes para um público-alvo em um período de três meses, apenas as duas primeiras serão ativadas. O primeiro é uma alteração de status de para **realizado**, o segundo é acionado por uma alteração de status de **realizado** para **existente**.

- Ao ativar públicos para perfis conhecidos, um mapa de identidade completo é incluído no payload de ativação. Sua função do Azure pode usar qualquer uma das identidades disponíveis para mapear os públicos-alvo para um perfil gerenciado em um aplicativo de terceiros, enquanto usa o identificador do cliente do aplicativo.

- Neste módulo, a função do hub de eventos foi implantada localmente (modo de depuração no Visual Studio Code), oferecendo várias opções de solução de problemas e depuração.

## Veja isto

- N/D

## Próximas etapas

Voltar para [Real-Time CDP: Audience Activation para o Hub de Eventos do Microsoft Azure](./segment-activation-microsoft-azure-eventhub.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
