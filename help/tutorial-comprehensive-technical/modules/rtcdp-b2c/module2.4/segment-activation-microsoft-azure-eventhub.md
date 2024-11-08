---
title: Ativação de segmento para o Hub de eventos do Microsoft Azure
description: Ativação de segmento para o Hub de eventos do Microsoft Azure
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 2.4 Real-Time CDP: Ativação de segmentos para o Hub de eventos do Microsoft Azure

**Autores: [Marc Meewis](https://www.linkedin.com/in/marcmeewis/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Neste módulo, você configurará um destino do Microsoft Azure EventHub como destino em tempo real para a CDP em tempo real do Adobe Experience Platform. Você também configurará e implantará uma função do Azure que será acionada em tempo real sempre que a Adobe Experience Platform entregar uma carga de segmento para seu destino do Azure EventHub. A Azure Function que você acionará mostrará o mecanismo dos recursos de ativação da Adobe Experience Platform Real-time CDP.

Como parte desse módulo, você também compreenderá o que aciona a Real-time CDP para realmente fornecer uma carga útil a um destino especificado. Também discutiremos o status de uma qualificação de segmento e como ela está relacionada à ativação.

A CDP em tempo real da Adobe Experience Platform é compatível com a ativação de dados para destinos de armazenamento na nuvem de transmissão, permitindo exportar dados e eventos de público-alvo em tempo real para esses destinos no formato JSON. Em seguida, você pode descrever a lógica de negócios sobre esses eventos em seus destinos

Os Hubs de eventos do Microsoft Azure são um serviço de assimilação de dados totalmente gerenciado e em tempo real que é simples, confiável e escalável. Transmita milhões de eventos por segundo de qualquer fonte para criar pipelines de dados dinâmicos e responder imediatamente aos desafios comerciais.

## Objetivos de aprendizagem

- Familiarize-se com os Hubs de Eventos do Microsoft Azure
- Configure um destino RTCDP para seu Hub de Eventos do Microsoft Azure
- Entenda quando a Real-time CDP é ativada e como é a carga de ativação
- Configure o Visual Studio Code para desenvolver, testar e implantar seu projeto do Azure
- Criar e implantar uma função do Azure que consome qualificações de segmentos entregues em tempo real pela RTCDP

## Pré-requisitos

- Acesso ao [Adobe Experience Platform](https://experience.adobe.com/platform)
- Familiaridade com o ambiente do site de demonstração da AEP
- Entenda como definir, usar e ativar segmentos de transmissão no Adobe Experience Platform

>[!NOTE]
>
>Não se esqueça de instalar, configurar e usar a Extensão do Chrome, conforme referenciado em [0.1 - Instalar a extensão do Chrome para a documentação do Experience League](../../gettingstarted/gettingstarted/ex1.md)

## Exercícios

[2.4.0 Configurar o ambiente](./ex0.md)

Neste exercício, você configurará seu ambiente do Microsoft Azure.

[2.4.1 Configurar o ambiente do Microsoft Azure EventHub](./ex1.md)

Neste exercício, você configurará seu ambiente do Microsoft Azure EventHub.

[2.4.2 Configurar o destino do Hub de eventos do Azure no Adobe Experience Platform](./ex2.md)

Neste exercício, você configurará sua conexão de destino da Real-time CDP que fornecerá segmentos em tempo real ao EventHub configurado no exercício anterior.

[2.4.3 Criar um segmento](./ex3.md)

Neste exercício, você criará um segmento de transmissão no Adobe Experience Platform

[2.4.4 Ativar segmento](./ex4.md)

Neste exercício, você ativará o segmento de transmissão para o destino do Real-time CDP EventHub.

[2.4.5 Criar seu projeto do Microsoft Azure](./ex5.md)

Neste exercício, você criará uma função do Azure que será acionada em tempo real quando a Adobe Experience Platform ativar qualificações de segmento para o destino do Hub de eventos do Azure correspondente.

[2.4.6 Cenário completo](./ex6.md)

Neste ponto, tudo está configurado. Agora você pode navegar pelo seu site de demonstração da AEP e obter qualificações de segmento entregues à sua função de Acionador do EventHub do Microsoft Azure.

[Resumo e benefícios](./summary.md)

Resumo desse módulo e visão geral dos benefícios.

>[!NOTE]
>
>Obrigado por investir seu tempo aprendendo tudo o que há para saber sobre o Adobe Experience Platform e seus aplicativos. Em caso de dúvidas, envie um email para **techinsiders@adobe.com** para compartilhar comentários gerais sobre sugestões para conteúdo futuro. Entre em contato diretamente com o Tech Insiders.

[Voltar a todos os módulos](../../../overview.md)
