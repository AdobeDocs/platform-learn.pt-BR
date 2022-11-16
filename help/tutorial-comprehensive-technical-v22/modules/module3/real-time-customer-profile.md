---
title: Foundation - Perfil do cliente em tempo real
description: Foundation - Perfil do cliente em tempo real
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 050e5d99-544d-4a86-a7f6-9f103381dca5
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 1%

---

# 3. Base - Perfil do cliente em tempo real

**Autor: [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Neste módulo, realizaremos um aprofundamento dos recursos de Perfil do cliente em tempo real e Identidade da Adobe Experience Platform. Você aprenderá como os públicos-alvo podem ser definidos, a função do Serviço de identidade e a ID do Experience Cloud e como definir consultas do construtor de segmentos para definir seus próprios segmentos.

## Objetivos de aprendizagem

- Saiba como visualizar o Perfil do cliente em tempo real por meio da interface do usuário do Adobe Experience Platform
- Saiba como criar um segmento usando o Construtor de segmentos do Adobe Experience Platform
- Saiba como criar um segmento e armazenar os resultados do segmento em um conjunto de dados usando APIs do Adobe Experience Platform
- Saiba mais sobre o impacto do acesso a um perfil completo do cliente, incluindo o comportamento em tempo real, em ambientes offline

## Pré-requisitos

- Acesso ao [Adobe Experience Platform](https://experience.adobe.com/platform)
- Acesso ao [https://public.aepdemo.net](https://public.aepdemo.net)
- **Baixar estes ativos**:
   - [Coleções do Postman](./../../assets/postman/postman_profile.zip)

>[!IMPORTANT]
>
>Este tutorial foi criado para facilitar um formato específico de workshop. Ele usa sistemas e contas específicos aos quais você pode não ter acesso. Mesmo sem acesso, achamos que você ainda pode aprender muito lendo esse conteúdo muito detalhado. Se você participar de um dos workshops e precisar de suas credenciais de acesso, entre em contato com o representante do Adobe, que fornecerá as informações necessárias.

## Visão geral da arquitetura

Consulte a arquitetura abaixo, que destaca os componentes que serão discutidos e usados neste módulo.

![Visão geral da arquitetura](../../assets/images/architecturem3.png)

## Sandbox para usar

Para este módulo, use esta sandbox: `--aepSandboxId--`.

>[!NOTE]
>
>Não se esqueça de instalar, configurar e usar a Extensão do Chrome, conforme referenciado em [0.1 - Instalar a extensão do Chrome para a documentação do Experience League](../module0/ex1.md)

## Exercícios

[3.1 Visite o site](./ex1.md)

Neste exercício, você seguirá um script e passará pelo site.

[3.2 Visualizar seu próprio perfil de cliente em tempo real - Interface do usuário](./ex2.md)

Neste exercício, você fará logon no Adobe Experience Platform e visualizará seu próprio Perfil do cliente em tempo real na interface do usuário do .

[3.3 Visualizar seu próprio perfil de cliente em tempo real - API](./ex3.md)

Neste exercício, você usará o Postman e o Adobe I/O para visualizar seu próprio perfil de cliente em tempo real, utilizando as APIs do Adobe Experience Platform.

[3.4 Criar um segmento - Interface do usuário](./ex4.md)

Neste exercício, você criará um segmento usando o Construtor de segmentos do Adobe Experience Platform.

[3.5 Criar um segmento - API](./ex5.md)

Neste exercício, você usará o Postman e o Adobe I/O para criar um segmento e armazenar os resultados desse segmento como um conjunto de dados, usando as APIs do Adobe Experience Platform.

[3.6 Veja o Perfil do cliente em tempo real em ação no Call Center](./ex6.md)

Neste exercício, você representará um funcionário da central de atendimento que recebe uma chamada de um cliente. Para realmente afetar a experiência deste cliente, você precisará acessar todas as informações disponíveis em tempo real.

[Resumo e benefícios](./summary.md)

Resumo deste módulo e visão geral dos benefícios.

>[!NOTE]
>
>Obrigado por investir seu tempo em aprender tudo o que há para saber sobre a Adobe Experience Platform. Se você tiver dúvidas, queira compartilhar comentários gerais de suas sugestões sobre conteúdo futuro, entre em contato diretamente com Wouter Van Geluwe, enviando um email para **vangeluw@adobe.com**.

[Voltar para todos os módulos](../../overview.md)
