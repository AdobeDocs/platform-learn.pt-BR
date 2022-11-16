---
title: Criar um fluxo de dados
description: Criar um fluxo de dados
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 52378f63-8a6d-49ed-a21a-65b74fe1ddc4
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# Criar um fluxo de dados

Os dados enviados do site atingem um conjunto de servidores de Adobe chamadas [Adobe Experience Platform Edge](https://business.adobe.com/products/experience-platform/experience-platform-edge-network.html). Essa rede é capaz de enviar seus dados para o [Conjunto de dados Adobe Experience Platform criado anteriormente](create-a-schema.md) e outros produtos da Adobe Experience Cloud. Esses produtos Adobe também podem responder com dados para a sua página da Web. Por exemplo, a Edge Network pode retornar conteúdo de personalização da Adobe Target.

Para configurar quais produtos do Adobe Edge Network envia dados de e para, você deve criar um conjunto de dados. Quando a Edge Network recebe dados da sua página da Web, ela consulta o armazenamento de dados criado, lê a configuração e encaminha os dados para os produtos Adobe apropriados.

Para criar um armazenamento de dados, primeiro navegue até o [!UICONTROL Datastreams] exibir no [!UICONTROL Coleta de dados]. Clique em [!UICONTROL Criar fluxo de dados] no canto superior direito. Forneça um nome para o armazenamento de dados.

![Nome e descrição do conjunto de dados](../../../assets/implementation-strategy/datastream-name-description.png)

A próxima tela permite configurar quais produtos do Adobe devem receber os dados enviados do seu site. Para os fins deste tutorial, ative somente o Adobe Experience Platform, selecione o conjunto de dados criado anteriormente (que estará no padrão [!UICONTROL Prod] sandbox) e clique em [!UICONTROL Salvar].

![Configuração do produto Datastream](../../../assets/implementation-strategy/datastream-product-configuration.png)

Seu armazenamento de dados foi criado.

## Ambientes de fluxo de dados

As empresas geralmente têm um caminho de promoção para qualquer atualização de site. Alguém na empresa (um profissional de marketing ou engenheiro, dependendo das mudanças) normalmente testa suas alterações em um ambiente de desenvolvimento que somente essa pessoa está usando. Uma vez que se sintam confortáveis com as alterações, as alterações são promovidas para um ambiente de preparo onde recebem mais testes. Por fim, as alterações são publicadas no site de produção que os usuários veem. Os datastreams são compatíveis com esse padrão de promoção.

Depois de clicar [!UICONTROL Salvar], você deve ter notado que três ambientes de conjunto de dados foram criados automaticamente para você: [!UICONTROL Ambiente de desenvolvimento], [!UICONTROL Ambiente de preparo]e [!UICONTROL Ambiente de produção].

![Ambientes de fluxo de dados](../../../assets/implementation-strategy/datastream-environments.png)

Se clicar em cada ambiente de armazenamento de dados, você observará que todos receberam a mesma configuração fornecida. No entanto, esses ambientes podem ser personalizados individualmente.

Se você estiver familiarizado com as Tags do Adobe Experience Platform, talvez já esteja familiarizado com o conceito de um ambiente de desenvolvimento, armazenamento temporário e produção. Os ambientes nas Tags estão relacionados a ambientes em um conjunto de dados. À medida que você move uma biblioteca de tags pelo fluxo de trabalho de publicação de Tags do desenvolvimento para o armazenamento temporário, para a produção, o ambiente de armazenamento de dados usado também mudará automaticamente de [!UICONTROL Ambiente de desenvolvimento]para [!UICONTROL Ambiente de preparo]para [!UICONTROL Ambiente de produção]. Isso permite, por exemplo, enviar dados para um conjunto de dados enquanto suas alterações estão em desenvolvimento e enviar dados para um conjunto de dados diferente quando as alterações estiverem em produção. Isso pode manter seus dados de produção livres de quaisquer dados de lixo que você gerar durante o processo de desenvolvimento. Posteriormente, discutiremos os ambientes do armazenamento de dados ao configurar extensões na propriedade da tag.

O servidor agora está totalmente configurado para receber dados de sua página da Web.
