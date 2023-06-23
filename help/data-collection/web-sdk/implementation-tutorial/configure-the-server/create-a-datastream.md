---
title: Criar um fluxo de dados
description: Criar um fluxo de dados
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 52378f63-8a6d-49ed-a21a-65b74fe1ddc4
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# Criar um fluxo de dados

Os dados enviados pelo seu site atingem um conjunto de servidores Adobe chamados [Adobe Experience Platform Edge](https://business.adobe.com/products/experience-platform/experience-platform-edge-network.html). Essa rede é capaz de enviar seus dados para o [Conjunto de dados do Adobe Experience Platform criado anteriormente](create-a-schema.md) e outros produtos no Adobe Experience Cloud. Esses produtos Adobe também podem responder com dados para a sua página da Web. Por exemplo, a Rede de borda pode retornar conteúdo de personalização do Adobe Target.

Para configurar de quais produtos de Adobe a Rede de borda transfere dados de e para, você deve criar um fluxo de dados. Quando a Rede de borda recebe dados da sua página da Web, ela consulta o fluxo de dados criado, lê a configuração e, em seguida, encaminha os dados para os produtos de Adobe apropriados.

Para criar um fluxo de dados, primeiro navegue até a [!UICONTROL Datastreams] exibir em [!UICONTROL Coleta de dados]. Clique em [!UICONTROL Criar sequência de dados] no canto superior direito. Forneça um nome para o fluxo de dados.

![Nome e descrição da sequência de dados](../../../assets/implementation-strategy/datastream-name-description.png)

A próxima tela permite configurar quais produtos Adobe devem receber os dados enviados pelo seu site. Para os fins deste tutorial, habilite somente o Adobe Experience Platform, selecione o conjunto de dados criado anteriormente (que estará no padrão [!UICONTROL Prod] sandbox) e clique em [!UICONTROL Salvar].

![Configuração de produto de sequência de dados](../../../assets/implementation-strategy/datastream-product-configuration.png)

Sua sequência de dados foi criada.

## Ambientes de fluxo de dados

As empresas normalmente têm um caminho promocional para qualquer atualização de site. Alguém na empresa (um profissional de marketing ou engenheiro, dependendo das alterações) normalmente testa as alterações em um ambiente de desenvolvimento que somente essa pessoa está usando. Quando se sentirem confortáveis com as alterações, elas são promovidas a um ambiente de preparo em que recebem mais testes. Por fim, as alterações são publicadas no site de produção que os usuários veem. As sequências de dados são compatíveis com esse padrão de promoção.

Depois de clicar em [!UICONTROL Salvar], você deve ter notado que três ambientes de sequência de dados foram criados automaticamente para você: [!UICONTROL Ambiente de desenvolvimento], [!UICONTROL Ambiente de preparo], e [!UICONTROL Ambiente de produção].

![Ambientes de fluxo de dados](../../../assets/implementation-strategy/datastream-environments.png)

Se clicar em cada ambiente de fluxo de dados, você observará que todos receberam a mesma configuração fornecida. No entanto, esses ambientes podem ser personalizados individualmente.

Se você estiver familiarizado com as Tags do Adobe Experience Platform, talvez já esteja familiarizado com o conceito de um ambiente de desenvolvimento, preparo e produção. Os ambientes nas tags são relacionados aos ambientes em um fluxo de dados. À medida que você move uma biblioteca de tags pelo fluxo de trabalho de publicação de tags, do desenvolvimento ao preparo e produção, o ambiente de fluxo de dados usado também mudará automaticamente do [!UICONTROL Ambiente de desenvolvimento], para [!UICONTROL Ambiente de preparo], para [!UICONTROL Ambiente de produção]. Isso permite, por exemplo, enviar dados para um conjunto de dados enquanto suas alterações estão em desenvolvimento e enviar dados para um conjunto de dados diferente quando as alterações estiverem em produção. Isso pode manter os dados de produção livres de quaisquer dados de lixo gerados durante o processo de desenvolvimento. Discutiremos os ambientes de sequência de dados posteriormente ao configurar extensões na propriedade da tag.

O servidor agora está totalmente configurado para receber dados da página da Web.
