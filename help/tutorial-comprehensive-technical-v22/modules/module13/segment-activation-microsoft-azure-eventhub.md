---
title: Ativação de Segmento para o Hub de Eventos do Microsoft Azure
description: Ativação de Segmento para o Hub de Eventos do Microsoft Azure
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 73c2576d-0a69-4d56-a671-9ae1f75580b9
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 1%

---

# 13. Real-Time CDP: Ativação de Segmento para o Hub de Eventos do Microsoft Azure

**Autores: [Marc Meewis](https://www.linkedin.com/in/marcmeewis/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Neste módulo, você configurará um destino EventHub do Microsoft Azure como um destino em tempo real para a CDP em tempo real do Adobe Experience Platform. Você também irá configurar e implantar uma função do Azure que será acionada em tempo real sempre que o Adobe Experience Platform fornecer uma carga de segmento ao seu destino do Azure EventHub. A Função do Azure que você acionará mostrará o mecanismo dos recursos de ativação da CDP em tempo real do Adobe Experience Platform.

Como parte desse módulo, você também terá uma compreensão do que aciona a CDP em tempo real para realmente fornecer uma carga para um destino especificado. Também discutiremos o status de uma qualificação de segmento e como ela está relacionada à ativação.

A CDP em tempo real da Adobe Experience Platform oferece suporte à ativação de dados para o streaming de destinos de armazenamento na nuvem, permitindo exportar os dados e eventos do público-alvo em tempo real para esses destinos no formato JSON. Em seguida, você pode descrever a lógica comercial sobre esses eventos nos seus destinos

O Microsoft Azure Event Hubs é um serviço de assimilação de dados em tempo real totalmente gerenciado, simples, confiável e escalável. Transmitir milhões de eventos por segundo de qualquer fonte para criar pipelines de dados dinâmicos e responder imediatamente aos desafios comerciais.

## Objetivos de aprendizagem

- Familiarize-se com os Hubs de eventos do Microsoft Azure
- Configurar um destino RTCDP no Hub de Eventos do Microsoft Azure
- Entenda quando a CDP em tempo real é ativada e como a carga de ativação se parece
- Configurar o Código do Visual Studio para desenvolver, testar e implantar seu projeto do Azure
- Crie e implante uma função do Azure que consome qualificações de segmentos fornecidas em tempo real pela RTCDP

## Pré-requisitos

- Acesso ao [Adobe Experience Platform](https://experience.adobe.com/platform)
- Familiaridade com o ambiente do site de demonstração AEP
- Saiba como definir, usar e ativar segmentos de transmissão no Adobe Experience Platform

>[!IMPORTANT]
>
>Este tutorial foi criado para facilitar um formato específico de workshop. Ele usa sistemas e contas específicos aos quais você pode não ter acesso. Mesmo sem acesso, achamos que você ainda pode aprender muito lendo esse conteúdo muito detalhado. Se você participar de um dos workshops e precisar de suas credenciais de acesso, entre em contato com o representante do Adobe, que fornecerá as informações necessárias.

## Visão geral da arquitetura

Consulte a arquitetura abaixo, que destaca os componentes que serão discutidos e usados neste módulo.

![Visão geral da arquitetura](../../assets/images/architecturem18.png)

## Sandbox para usar

Para este módulo, use esta sandbox: `--module18sandbox--`.

>[!NOTE]
>
>Não se esqueça de instalar, configurar e usar a Extensão do Chrome, conforme referenciado em [0.1 - Instalar a extensão do Chrome para a documentação do Experience League](../module0/ex1.md)

## Exercícios

[13.0 Configurar o ambiente](./ex0.md)

Neste exercício, você configurará seu ambiente do Microsoft Azure.

[13.1 Configurar o ambiente do Microsoft Azure EventHub](./ex1.md)

Neste exercício, você irá configurar seu ambiente Microsoft Azure EventHub.

[13.2 Configurar o destino do Hub de eventos do Azure no Adobe Experience Platform](./ex2.md)

Neste exercício, você irá configurar sua conexão de destino CDP em tempo real que fornecerá segmentos em tempo real ao EventHub que você configurou no exercício anterior.

[13.3 Criar um segmento](./ex3.md)

Neste exercício, você criará um segmento de transmissão no Adobe Experience Platform

[13.4 Ativar segmento](./ex4.md)

Neste exercício, você ativará seu segmento de transmissão para o destino do EventHub da CDP em tempo real.

[13.5 Criar o projeto do Microsoft Azure](./ex5.md)

Neste exercício, você criará uma função do Azure que será acionada em tempo real quando a Adobe Experience Platform ativar as qualificações de segmento no destino do Hub de eventos do Azure correspondente.

[13.6 Cenário completo](./ex6.md)

Neste ponto, tudo está configurado. Agora você pode navegar no site de demonstração do AEP e obter qualificações de segmento entregues à sua função de Acionador do Microsoft Azure EventHub.

[Resumo e benefícios](./summary.md)

Resumo deste módulo e visão geral dos benefícios.

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender tudo o que há para saber sobre a Adobe Experience Platform. Se você tiver dúvidas, queira compartilhar comentários gerais de suas sugestões sobre conteúdo futuro, entre em contato diretamente com Wouter Van Geluwe, enviando um email para **vangeluw@adobe.com**.

[Voltar para todos os módulos](../../overview.md)
