---
title: CDP em tempo real - Crie um segmento e execute ações
description: CDP em tempo real - Crie um segmento e execute ações
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 147d9153-5742-4857-aae1-0ec434a1e626
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 1%

---

# 6. CDP em tempo real - Crie um segmento e execute ações

**Autor: [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/), [Alberto De Caro](https://www.linkedin.com/in/albertodecaro/), [Benedikt Wedenik](https://www.linkedin.com/in/benedikt-wedenik/)**

Neste módulo, você configurará um segmento de transmissão e ativará o segmento para vários destinos.

## Objetivos de aprendizagem

- Saiba como criar um segmento e habilitá-lo para transmissão contínua.
- Saiba como configurar um destino de publicidade usando a interface do usuário do Adobe Experience Platform.
- Saiba como conectar um segmento a um destino e ativá-lo.
- Saiba como usar segmentos do Adobe Experience Platform no Adobe Audience Manager e como usar segmentos do Adobe Audience Manager no Adobe Experience Platform, graças ao compartilhamento de segmentos bidirecional.

## Pré-requisitos

- Acesso ao Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acesso ao Adobe Target
- Acesso ao AWS S3

>[!IMPORTANT]
>
>Este tutorial foi criado para facilitar um formato específico de workshop. Ele usa sistemas e contas específicos aos quais você pode não ter acesso. Mesmo sem acesso, achamos que você ainda pode aprender muito lendo esse conteúdo muito detalhado. Se você participar de um dos workshops e precisar de suas credenciais de acesso, entre em contato com o representante do Adobe, que fornecerá as informações necessárias.

## Visão geral da arquitetura

Consulte a arquitetura abaixo, que destaca os componentes que serão discutidos e usados neste módulo.

![Visão geral da arquitetura](../../assets/images/architecturem11.png)

## Sandbox para usar

Para este módulo, use esta sandbox: `--module11sandbox--`.

>[!NOTE]
>
>Não se esqueça de instalar, configurar e usar a Extensão do Chrome, conforme referenciado em [0.1 - Instalar a extensão do Chrome para a documentação do Experience League](../module0/ex1.md)

## Exercícios

[6.1 Criar um segmento](./ex1.md)

Saiba como criar um segmento.

[6.2 Revise como configurar o destino DV360 usando destinos](./ex2.md)

Saiba como configurar um destino de publicidade usando a interface do usuário do Real-Time CDP.

[6.3 Tomar medidas: enviar seu segmento para o DV360](./ex3.md)

Conecte o segmento que você criou no exercício 6.1 ao DV360 de destino.

[6.4 Tomar medidas: enviar seu segmento para um destino S3](./ex4.md)

Use o segmento criado no exercício 6.1 e envie-o para um destino S3, normalmente usado para destinos de Marketing de email .

[6.5 Tomar medidas: enviar seu segmento para a Adobe Target](./ex5.md)

Use o segmento criado no exercício 6.1 para configurar uma Atividade de Direcionamento de experiência no Adobe Target.

[6.6 Públicos-alvo externos](./ex6.md)

Importe públicos de um sistema de origem externa para o Adobe Experience Platform.

[SDK de destinos 6.7](./ex7.md)

Configure seu próprio destino usando o SDK de Destinos.

[Resumo e benefícios](./summary.md)

Resumo deste módulo e visão geral dos benefícios.

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender tudo o que há para saber sobre a Adobe Experience Platform. Se você tiver dúvidas, queira compartilhar comentários gerais de suas sugestões sobre conteúdo futuro, entre em contato diretamente com Wouter Van Geluwe, enviando um email para **vangeluw@adobe.com**.

[Voltar para todos os módulos](../../overview.md)
