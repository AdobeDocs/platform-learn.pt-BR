---
title: Criar uma propriedade de tag do Adobe Experience Platform e instalar extensões
description: Criar uma propriedade de tag do Adobe Experience Platform e instalar extensões
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 7403059f-b34c-48e0-9efe-b2db7a9afb27
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 1%

---

# Criar uma propriedade de tag do Adobe Experience Platform e instalar extensões

Agora que o código na página está enviando dados e eventos para a camada de dados, é hora do profissional de marketing ler os dados da camada de dados e enviar esses dados para a Adobe Experience Platform. Normalmente, isso exigiria duas bibliotecas JavaScript:

* Camada de dados do cliente Adobe: Em etapas anteriores, você criava uma matriz de camada de dados e enviava objetos para ela. Para acessar os dados, você deve carregar a biblioteca JavaScript da camada de dados do cliente do Adobe , que fornece maneiras de ser notificado sobre alterações e eventos da camada de dados e também fornece maneiras simples de acessar os dados.
* Adobe Experience Platform Web SDK: Essa biblioteca JavaScript se comunica com a Adobe Experience Platform Edge Network. O SDK lida com identidade, consentimento, coleta de dados, personalização, públicos-alvo e muito mais.

Embora você possa carregar essas bibliotecas individuais em seu site e usá-las diretamente, recomendamos que você use [Tags do Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR). Com Tags, você pode incorporar um único script ao seu HTML e usar a interface do usuário Tags para implantar a Camada de dados do cliente do Adobe e o SDK da Web do Adobe Experience Platform. Tags também permitem criar regras para o envio de dados, entre outras coisas. Este tutorial usa Tags para essa finalidade e presume que você tenha uma compreensão básica de como as Tags operam.

## Criar uma propriedade nas Tags

Se você ainda não tiver, [criar uma propriedade em Tags](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html#create-or-configure-a-property).

## Instalar a extensão Camada de dados do cliente do Adobe

Instale a extensão Adobe Client Data Layer navegando até o catálogo de extensões, localizando a extensão e clicando no respectivo [!UICONTROL Instalar] botão. Você deve ver uma tela de configuração.

![Instalação da extensão de camada de dados do cliente Adobe](../../../assets/implementation-strategy/acdl-extension-installation.png)

Neste tutorial, não há necessidade de alterar os valores padrão. Clique em [!UICONTROL Salvar].

## Instalar a extensão Adobe Experience Platform Web SDK

Em seguida, instale a extensão Adobe Experience Platform Web SDK, localizando a extensão no catálogo de extensões e clicando no respectivo [!UICONTROL Instalar] botão. Você deve ver uma tela de configuração.

![Instalação da extensão do SDK da Web da Adobe Experience Platform](../../../assets/implementation-strategy/web-sdk-extension-installation.png)

Em [Criar um conjunto de dados](../configure-the-server/create-a-datastream.md), você criou um conjunto de dados que a Adobe Experience Platform Edge Network faz referência para determinar para onde enviar os dados de entrada. Ao fazer solicitações do SDK da Web da Adobe Experience Platform para a Edge Network, você deve indicar qual rede de borda do armazenamento de dados deve fazer referência.

Para fazer isso, encontre a variável [!UICONTROL Datastream] e selecione o armazenamento de dados criado anteriormente. Você é apresentado com os mesmos ambientes de armazenamento de dados que você viu em [Criar um conjunto de dados](../configure-the-server/create-a-datastream.md).

![Seleção de fluxo de dados](../../../assets/implementation-strategy/web-sdk-datastream-selection.png)

Conforme discutido no [Criar um conjunto de dados](../configure-the-server/create-a-dataset.md), esses ambientes de conjunto de dados têm um relacionamento com os ambientes de Tags . Considere que você concluiu a instalação da extensão Adobe Experience Platform Web SDK, crie uma biblioteca de tags que inclua a extensão e publique a biblioteca em um ambiente de desenvolvimento de Tags. Quando a biblioteca de tags é carregada em sua página da Web e a extensão Adobe Experience Platform Web SDK faz uma solicitação para a Edge Network, a extensão inclui a variável [!UICONTROL Ambiente de desenvolvimento] ID do ambiente do datastream. A Edge Network, por sua vez, usa essa ID para ler a configuração do [!UICONTROL Ambiente de desenvolvimento] ambiente de fluxo de dados e encaminhar dados para os produtos Adobe apropriados.

No momento, você tem apenas um ambiente de armazenamento de dados de desenvolvimento, um ambiente de armazenamento de dados de armazenamento temporário e um ambiente de armazenamento de dados de produção. É por isso que a interface do usuário de configuração de extensão mostra todos pré-selecionados e inalteráveis. No entanto, é possível criar vários ambientes de desenvolvimento de conjunto de dados (um para você e um para seu colega de trabalho, talvez) usando a interface do usuário do conjunto de dados. Se você tivesse vários ambientes de armazenamento de dados de desenvolvimento, seria possível selecionar qual deles deseja usar para essa propriedade de tag.

Finalmente, role para baixo e desmarque [!UICONTROL Ativar coleta de dados de clique]. Por padrão, o SDK rastreia automaticamente os links para você. Neste tutorial, no entanto, demonstraremos como você pode rastrear seus próprios cliques em links usando informações de link personalizadas.

Clique no botão [!UICONTROL Salvar] para concluir a instalação da extensão Adobe Experience Platform Web SDK.

As extensões apropriadas foram instaladas. É hora de criar regras e elementos de dados.
