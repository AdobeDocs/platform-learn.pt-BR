---
title: Implementar o Experience Cloud em sites com tags
description: Implementar o Experience Cloud em sites com tags é o ponto de partida perfeito para desenvolvedores front-end ou profissionais de marketing técnico que desejam aprender como implementar as soluções da Adobe Experience Cloud em seu site.
recommendations: catalog, noDisplay
exl-id: 1b95f0b2-3062-49d1-9b0b-e6824a54008f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 43%

---

# Visão geral

_Implementar o Experience Cloud em sites com tags_ O é o ponto de partida perfeito para desenvolvedores front-end ou profissionais de marketing técnico que desejam aprender como implementar as soluções da Adobe Experience Cloud em seu site.

Cada lição contém exercícios práticos e informações essenciais para ajudar você a implementar a Experience Cloud e compreender seu valor.  Os sites de demonstração são fornecidos para que você complete o tutorial e possa aprender as técnicas subjacentes em um ambiente seguro. Após concluir este tutorial, você deve estar pronto para começar a implementar todas as suas soluções de marketing por meio de tags em seu próprio site.

>[!INFO]
>
>Este tutorial usa extensões e bibliotecas específicas do aplicativo (AppMeasurement.js para Adobe Analytics, at.js para Adobe Target). Se você deseja implementar o SDK da Web da Adobe Experience Platform, consulte o [Implementar o Adobe Experience Cloud com o SDK da Web](/help/tutorial-web-sdk/overview.md) tutorial.


Depois de concluir este, você poderá:

* Criar uma propriedade de tag

* Instalar uma propriedade de tag em um site

* Adicione as seguintes soluções da Adobe Experience Cloud:
   * **[Adobe Experience Platform Identity Service](id-service.md)**
   * **[Adobe Target](target.md)**
   * **[Adobe Analytics](analytics.md)**
   * **[Adobe Audience Manager](audience-manager.md)**

* Crie regras e elementos de dados para enviar dados para as soluções da Adobe

* Valide a implementação usando o Adobe Experience Cloud Debugger

* Publicar alterações por meio de ambientes de desenvolvimento, de armazenamento temporário e de produção

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo integrado à Adobe Experience Platform como um conjunto de tecnologias de coleção de dados. Várias alterações de terminologia foram implementadas na interface de que você deve estar ciente ao usar este conteúdo:
>
> * O Platform launch (lado do cliente) agora está **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)**
> * Agora o lado do servidor do Platform launch **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * As configurações de borda agora são **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=pt-BR)**


>[!NOTE]
>
>Tutoriais de várias soluções semelhantes também estão disponíveis para [Web SDK](../tutorial-web-sdk/overview.md) e [SDK móvel](../tutorial-mobile-sdk/overview.md).

## Pré-requisitos

Nessas lições, presume-se que você tenha uma Adobe ID e as permissões necessárias para concluir os exercícios. Caso contrário, pode ser necessário entrar em contato com o administrador da Experience Cloud para solicitar acesso.

* Para tags, você deve ter permissão para desenvolver, aprovar, publicar, gerenciar extensões e gerenciar ambientes. Para obter mais informações sobre permissões de tag de usuário, consulte [a documentação](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html).
* No Adobe Analytics, você deve conhecer o servidor de rastreamento e quais conjuntos de relatórios você usará para concluir este tutorial
* Para o Audience Manager, você deve conhecer seu Subdomínio Audience Manager (também conhecido como &quot;Nome do parceiro&quot;, &quot;ID do parceiro&quot; ou &quot;Subdomínio do parceiro&quot;)

Além disso, pressupõe-se que você esteja familiarizado com linguagens de desenvolvimento front-end como HTML e JavaScript. Não é necessário ser um especialista nesses idiomas para concluir as lições, mas você extrairá mais delas se ler e entender o código confortavelmente.

## Sobre tags

O recurso de tags do Adobe Experience Platform é a próxima geração de recursos de gerenciamento de tags de site e de SDKs móveis do Adobe. As tags oferecem aos clientes uma forma simples de implantar e gerenciar todas as soluções de análise, marketing e anúncios necessárias para potencializar experiências de cliente relevantes. Não há custo adicional para Tags. Ele está disponível para qualquer cliente da Adobe Experience Cloud.

As tags de sites permitem que você gerencie centralmente todas as soluções JavaScript relacionadas a análises, marketing e publicidade usadas em seu desktop e sites móveis. Por exemplo, se você implantar o Adobe Analytics, as tags gerenciarão a biblioteca JavaScript do AppMeasurement, preencherão variáveis e acionarão solicitações.

O conteúdo do container é minimizado, incluindo o código personalizado. Tudo é modular. Se você não precisar de um item, ele não será incluído na biblioteca. O resultado é uma implementação rápida e compacta.

Tags também é uma plataforma que permite que fornecedores de terceiros criem extensões para facilitar a implantação de suas soluções por meio de tags. Uma extensão é um pacote de código (JavaScript, HTML e CSS) que estende a interface das tags e a funcionalidade do cliente. Pense nas tags como um sistema operacional e nas extensões como os aplicativos usados para realizar as tarefas.

## Sobre as lições

Nessas lições, você implementará a Adobe Experience Cloud em um site de varejo falso chamado Luma. O [site Luma](https://luma.enablementadobe.com/content/luma/us/en.html) tem uma camada de dados avançada e uma funcionalidade que permitirá a criação de uma implementação realista. Você criará sua própria propriedade de tag, em sua própria organização do Experience Cloud, e a mapeará para nosso site hospedado do Luma usando o Experience Cloud Debugger.

[![Site Luma](images/overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html).

## Obter as ferramentas

1. Como você estará usando algumas extensões específicas do navegador, recomendamos concluir o tutorial usando o [navegador web Chrome](https://www.google.com/chrome/)
1. Adicione a extensão [Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) ao navegador Chrome.
1. Baixe a [página de exemplo html](https://www.enablementadobe.com/multi/web/basic-sample.html) (clique com o botão direito do mouse neste link e clique em &quot;Salvar link como&quot;)
1. Obtenha um editor de texto no qual é possível fazer alterações na página html de exemplo. (Se você não tiver um, recomendamos experimentar o [Brackets](https://brackets.io/))
1. Marcar o site [Luma](https://luma.enablementadobe.com/content/luma/us/en.html)

>[!NOTE]
>
>Você pode achar mais fácil concluir este tutorial com o site Luma aberto no Chrome, ao ler este tutorial e concluir as etapas da interface da Coleta de dados em um navegador diferente.

Vamos começar!

[Próximo: &quot;Criar uma propriedade de tag&quot; >](create-a-property.md)
