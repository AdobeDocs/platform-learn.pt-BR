---
title: Testar a implementação
description: Testar a implementação
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: e2213c23-d395-4c57-8c6c-0319cd0fb0ac
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 2%

---

# Testar a implementação

Agora que você configurou a página da Web e implantou a biblioteca de tags da Adobe Experience Platform, é hora de testar a implementação.

Abra a página do produto no navegador. Você pode fazer isso clicando em _Arquivo_ depois _Abrir arquivo..._ no navegador ou você pode hospedar a página em um servidor da web e inserir o URL apropriado.

Depois que a página for carregada, você verá algo como isto:

![Página da Web](../../assets/implementation-strategy/webpage.png)

Não é bonito, mas vai dar certo.

## Inspect a exibição de página e eventos de exibição de produto

Abra as ferramentas do desenvolvedor em seu navegador e clique no painel de rede. Atualize sua página.

Nesse ponto, você deve ver quatro solicitações:

1. product.html - A página da Web.
2. launch-###########-development.js - A biblioteca do Launch.
3. interagir - O evento de exibição de página que está sendo enviado ao servidor.
4. interagir - O evento de exibição de produto que está sendo enviado ao servidor.

Fique à vontade para inspecionar as cargas de cada solicitação. Para o primeiro `interact` solicitação, você poderá ver a carga sendo enviada com uma `eventType` de `web.webpagedetails.pageViews`.

![Inspeção de solicitação de exibição de página](../../assets/implementation-strategy/webpage-page-viewed-inspection.png)

Para o segundo `interact` solicitação, você poderá ver a carga sendo enviada com uma `eventType` de `commerce.productViews`.

![Inspeção de solicitação de exibição de produto](../../assets/implementation-strategy/webpage-product-view-inspection.png)

Fique à vontade para contornar o restante dos dados enviados, incluindo as informações do produto.

## Inspect abre o carrinho e adiciona aos eventos do carrinho

Em seguida, clique no link _Adicionar ao carrinho_ botão.

Você deve ver duas solicitações adicionais, a primeira com um `eventType` de `commerce.productListOpens` (para abrir um novo carrinho) e o segundo com um `eventType` de `commerce.productListAdds` (para adicionar o produto ao carrinho).

## Evento Inspect the download app link click

Dependendo do navegador, clicar em um link que leva você para fora da página atual pode limpar o painel de rede. Como você deseja inspecionar a solicitação de rede para o evento de clique de link que ocorre logo antes de sair da página, será necessário configurar seu navegador para preservar os logs de rede nas páginas. Isso é feito verificando um _Preservar log_ no painel de rede (Chrome, Safari, Edge) ou ao clicar em um ícone de engrenagem e marcar uma _Logs persistentes_ no menu exibido (Firefox).

Em seguida, clique no link _Baixar o aplicativo_ link.

Você deve ver mais um `interact` solicitação será exibida no painel rede. Se você inspecionar a solicitação, deve encontrar um `eventType` de `web.webinteraction.linkClicks` bem como detalhes sobre o link clicado.

## Verifique se os dados chegam ao conjunto de dados do Adobe Experience Platform

Agora que as solicitações estão sendo enviadas, você também verificará se os dados estão chegando com segurança no conjunto de dados do Adobe Experience Platform que você criou. Comece navegando até o [!UICONTROL Conjuntos de dados] exibir dentro do Adobe Experience Platform.

Selecione o conjunto de dados criado anteriormente.

Talvez seja necessário aguardar alguns minutos, mas logo você deverá ver indicações de dados sendo processados e inseridos em seu conjunto de dados. Você também deve ver se o processamento teve êxito ou falhou. Se falhar, você será capaz de ver por que falhou. As falhas normalmente ocorrem porque os dados que você está enviando não correspondem ao esquema e você precisará ajustar seus dados ou esquema adequadamente.

![Assimilação do conjunto de dados](../../assets/implementation-strategy/dataset-ingestion.png)

## Usar a extensão Adobe Experience Platform Debugger

Para obter mais informações sobre como sua implementação está se comportando no navegador e nos servidores Adobe, verifique a extensão do navegador Adobe Experience Platform Debugger!

[Extensão Adobe Experience Platform Debugger para o Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

[Extensão Adobe Experience Platform Debugger para Firefox](https://addons.mozilla.org/pt-BR/firefox/addon/adobe-experience-platform-dbg/)
