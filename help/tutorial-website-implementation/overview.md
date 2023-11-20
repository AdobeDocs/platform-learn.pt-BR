---
title: Implementar o Experience Cloud em sites com tags
description: Implementar o Experience Cloud em sites com tags é o ponto de partida perfeito para desenvolvedores front-end ou profissionais de marketing técnicos que desejam aprender como implementar as soluções da Adobe Experience Cloud no site.
recommendations: catalog, noDisplay
exl-id: 1b95f0b2-3062-49d1-9b0b-e6824a54008f
source-git-commit: 2483409b52562e13a4f557fe5bdec75b5afb4716
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 39%

---

# Visão geral

_Implementar o Experience Cloud em sites com tags_ O é o ponto de partida perfeito para desenvolvedores front-end ou profissionais técnicos que desejam aprender como implementar as soluções da Adobe Experience Cloud no site.

Cada lição contém exercícios práticos e informações essenciais para ajudar você a implementar a Experience Cloud e compreender seu valor.  Os sites de demonstração são fornecidos para que você complete o tutorial e possa aprender as técnicas subjacentes em um ambiente seguro. Após concluir este tutorial, você deve estar pronto para começar a implementar todas as suas soluções de marketing por meio de tags em seu próprio site.

>[!INFO]
>
>Este tutorial usa extensões e bibliotecas específicas do aplicativo (AppMeasurement.js para Adobe Analytics, at.js para Adobe Target). Se estiver querendo implementar o Adobe Experience Platform Web SDK, consulte a [Implementar o Adobe Experience Cloud com o SDK da Web](/help/tutorial-web-sdk/overview.md) tutorial.


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
>O Adobe Experience Platform Launch está sendo integrado à Adobe Experience Platform como um conjunto de tecnologias de coleção de dados. Várias alterações de terminologia foram implementadas na interface do que você deve estar ciente ao usar esse conteúdo:
>
> * O Platform launch (lado do cliente) agora é **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)**
> * O Platform launch Server Side agora é **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * As configurações de borda agora são **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=pt-BR)**

>[!NOTE]
>
>Tutoriais de várias soluções semelhantes também estão disponíveis para [SDK da Web](../tutorial-web-sdk/overview.md) e [SDK móvel](../tutorial-mobile-sdk/overview.md).

## Pré-requisitos

Nessas lições, presume-se que você tenha uma Adobe ID e as permissões necessárias para concluir os exercícios. Caso contrário, pode ser necessário entrar em contato com o administrador da Experience Cloud para solicitar acesso.

* Para tags, você deve ter permissão para desenvolver, aprovar, publicar, gerenciar extensões e gerenciar ambientes. Para obter mais informações sobre permissões de usuário de tags, consulte [a documentação](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html).
* No Adobe Analytics, você deve conhecer o servidor de rastreamento e quais conjuntos de relatórios você usará para concluir este tutorial
* Para o Audience Manager, você deve conhecer seu subdomínio do Audience Manager (também conhecido como &quot;Nome do parceiro&quot;, &quot;ID do parceiro&quot; ou &quot;Subdomínio do parceiro&quot;)

Além disso, pressupõe-se que você esteja familiarizado com linguagens de desenvolvimento front-end como HTML e JavaScript. Não é necessário ser um especialista nessas linguagens para concluir as lições, mas você extrairá mais delas se ler e entender o código confortavelmente.

## Sobre tags

O recurso de tags da Adobe Experience Platform é a próxima geração de recursos de gerenciamento de tags de site e de SDKs móveis da Adobe. As tags oferecem aos clientes uma forma simples de implantar e gerenciar todas as soluções de análise, de marketing e de anúncios necessárias para potencializar experiências de cliente relevantes. Não há custo adicional para Tags. Ele está disponível para qualquer cliente da Adobe Experience Cloud.

As tags para sites permitem gerenciar centralmente todas as soluções JavaScript relacionadas a análises, marketing e publicidade usadas em seu desktop e sites móveis. Por exemplo, se você implantar o Adobe Analytics, as tags gerenciarão a biblioteca JavaScript do AppMeasurement, preencherão variáveis e acionarão solicitações.

O conteúdo do container é minimizado, incluindo o código personalizado. Tudo é modular. Se você não precisar de um item, ele não será incluído na biblioteca. O resultado é uma implementação rápida e compacta.

Tags também é uma plataforma que permite que fornecedores de terceiros criem extensões para facilitar a implantação de suas soluções por meio de tags. Uma extensão é um pacote de código (JavaScript, HTML e CSS) que estende a interface das tags e a funcionalidade do cliente. Pense nas tags como um sistema operacional e nas extensões como os aplicativos usados para realizar as tarefas.

## Sobre as lições

Nessas lições, você implementará a Adobe Experience Cloud em um site de varejo falso chamado Luma. O [site Luma](https://luma.enablementadobe.com/content/luma/us/en.html) tem uma camada de dados avançada e uma funcionalidade que permitirá a criação de uma implementação realista. Você criará sua própria propriedade de tag, em sua própria organização da Experience Cloud, e a mapeará para o nosso site hospedado do Luma usando a Experience Cloud Debugger.

[![Site Luma](images/overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html).

## Obter as ferramentas

1. Como você estará usando algumas extensões específicas do navegador, recomendamos concluir o tutorial usando o [navegador web Chrome](https://www.google.com/chrome/)
1. Adicione o [Adobe Experience Platform Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) extensão para o navegador Chrome
1. Copie o exemplo de código de página html

   +++Exemplo de código de página html

   ```html
   <!doctype html>
   <html lang="en">
   <head>
       <title>Tags: Sample HTML Page</title>
       <!--Preconnect and DNS-Prefetch to improve page load time. REPLACE "techmarketingdemos" WITH YOUR OWN AAM PARTNER ID, TARGET CLIENT CODE, AND ANALYTICS TRACKING SERVER-->
       <link rel="preconnect" href="//dpm.demdex.net">
       <link rel="preconnect" href="//fast.techmarketingdemos.demdex.net">
       <link rel="preconnect" href="//techmarketingdemos.demdex.net">
       <link rel="preconnect" href="//cm.everesttech.net">
       <link rel="preconnect" href="//techmarketingdemos.tt.omtrdc.net">
       <link rel="preconnect" href="//techmarketingdemos.sc.omtrdc.net">
       <link rel="dns-prefetch" href="//dpm.demdex.net">
       <link rel="dns-prefetch" href="//fast.techmarketingdemos.demdex.net">
       <link rel="dns-prefetch" href="//techmarketingdemos.demdex.net">
       <link rel="dns-prefetch" href="//cm.everesttech.net">
       <link rel="dns-prefetch" href="//techmarketingdemos.tt.omtrdc.net">
       <link rel="dns-prefetch" href="//techmarketingdemos.sc.omtrdc.net">
       <!--/Preconnect and DNS-Prefetch-->
       <!--Data Layer to enable rich data collection and targeting-->
       <script>
       var digitalData = {
           "page": {
               "pageInfo" : {
                   "pageName": "Home"
                   }
               }
       };
       </script>
       <!--/Data Layer-->
       <!--jQuery or other helper libraries-->
       <script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
       <!--/jQuery-->
       <!--Tags Header Embed Code: REPLACE THE NEXT LINE WITH THE EMBED CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
       <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
       <!--/Tags Header Embed Code-->
   </head>
   <body>
       <h1>Tags: Sample HTML Page</h1>
       <p>This is a very simple page to demonstrate basic implementation concepts of Tags</p>
       <p>See <a href="https://docs.adobe.com/content/help/en/experience-cloud/implementing-in-websites-with-launch/index.html">Implementing the Experience Cloud in Websites with Tags</a> for the complete tutorial</p>
   </body>
   </html>
   ```

+++

1. Obtenha um editor de texto no qual é possível fazer alterações na página html de exemplo. (Se você não tiver um, recomendamos experimentar o [Brackets](https://brackets.io/))
1. Marcar o site [Luma](https://luma.enablementadobe.com/content/luma/us/en.html)

>[!NOTE]
>
>Você pode achar mais fácil concluir este tutorial com o site Luma aberto no Chrome, ao ler este tutorial e concluir as etapas da interface da Coleção de dados em um navegador diferente.

Vamos começar!

[Próximo: &quot;Criar uma propriedade de tag&quot; >](create-a-property.md)
