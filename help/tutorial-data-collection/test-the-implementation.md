---
title: Testar a implementação
description: Testar a implementação
exl-id: 66eb1d4e-32eb-45fc-8da4-8d3c04dc3c7a
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 2%

---

# Testar a implementação

Agora que sua página da Web está configurada e sua biblioteca de tags da Adobe Experience Platform está implantada, é hora de testar a implementação.

1. Abra a página do produto no navegador. Você pode fazer isso clicando em _Arquivo_ then _Abrir arquivo..._ em seu navegador ou você pode hospedar sua página em um servidor da Web e inserir o URL apropriado.

Depois que a página carregar, você verá algo como o seguinte:
![Página Web](assets/webpage.png)

Não é bonito, mas faz o trabalho.

## Inspect os eventos de exibição de página e exibição de produto

1. Abra as ferramentas do desenvolvedor em seu navegador e clique no painel Rede. Atualize a página.
Nesse ponto, você deve ver quatro solicitações:
* product.html - sua página da Web.
* launch-###########-development.js - A biblioteca do Launch.
* interagir - O evento de exibição de página que está sendo enviado para o servidor.
* interagir - O evento de exibição de produto que está sendo enviado para o servidor.
Inspect a carga de cada solicitação:
1. Para o primeiro `interact` , você poderá ver a carga sendo enviada com um `eventType` de `web.webpagedetails.pageViews`.
   ![Inspeção de solicitação de exibição de página](assets/webpage-page-viewed-inspection.png)
1. Para o segundo `interact` , você poderá ver a carga sendo enviada com um `eventType` de `commerce.productViews`.
   ![Inspeção de solicitação de visualização do produto](assets/webpage-product-view-inspection.png)
1. Revise o restante dos dados enviados, incluindo as informações do produto.

## Inspect o carrinho aberto e adicionar aos eventos do carrinho

1. Em seguida, clique em **_Adicionar ao carrinho_**botão.

Você deve ver duas solicitações adicionais, a primeira com um `eventType` de `commerce.productListOpens` (para abrir um novo carrinho) e o segundo com um `eventType` de `commerce.productListAdds` (para adicionar o produto ao carrinho).

## Evento de clique no link do aplicativo de download do Inspect

Dependendo do navegador, clicar em um link que o afaste da página atual pode limpar o painel da rede. Como você deseja inspecionar a solicitação de rede para o evento de clique em links que ocorre antes de sair da página, é necessário configurar o navegador para preservar os logs de rede nas páginas.

1. Preservar logs de rede verificando uma **_Preservar log_** caixa de seleção no painel de rede (Chrome, Safari, Edge) ou ao clicar em um ícone de engrenagem e marcar uma **_Logs persistentes_** no menu exibido (Firefox).
1. Clique no botão **_Baixar o aplicativo_** link . Você deveria ver mais um `interact` solicitação exibida no painel de rede.
1. Localize a solicitação com uma `eventType` de `web.webinteraction.linkClicks`e revise os detalhes sobre o link que foi clicado.

## Verifique se os dados chegam ao conjunto de dados do Adobe Experience Platform

Agora que as solicitações estão sendo enviadas, verifique se os dados estão chegando com segurança no conjunto de dados do Adobe Experience Platform que você criou.

1. Navegue até o **[!UICONTROL Conjuntos de dados]** visualização dentro do Adobe Experience Platform.
1. Selecione o [conjunto de dados](configure-the-server/create-a-dataset.md) que você criou para este tutorial.
Pode ser necessário aguardar alguns minutos, mas em breve você verá indicações de dados serem processados e inseridos em seu conjunto de dados. Você também deve ver se o processamento foi bem-sucedido ou falhou. Se falhou, você verá por que falhou. As falhas normalmente ocorrem porque os dados que você está enviando não correspondem ao esquema e você precisa ajustar seus dados ou esquema de acordo.
   ![Assimilação do conjunto de dados](assets/dataset-ingestion.png)

## Usar a extensão do Adobe Experience Platform Debugger

Para obter mais informações sobre como sua implementação está se comportando no navegador e nos servidores do Adobe Debugger, verifique a extensão do navegador Adobe Experience Platform Debugger!

[Extensão do Adobe Experience Platform Debugger para Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

[Extensão do Adobe Experience Platform Debugger para Firefox](https://addons.mozilla.org/pt-BR/firefox/addon/adobe-experience-platform-dbg/)

[Próximo: ](summary.md)

>[!NOTE]
>
>Obrigado por investir seu tempo para aprender sobre a coleta de dados. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)