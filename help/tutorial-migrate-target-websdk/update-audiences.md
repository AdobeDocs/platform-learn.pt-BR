---
title: Atualizar públicos-alvo e scripts de perfil - Migrar o Target da at.js 2.x para o SDK da Web
description: Saiba como atualizar públicos-alvo e scripts de perfil da Adobe Target para compatibilidade com o SDK da Web do Experience Platform.
exl-id: 2c0f85f7-6e8c-4d0b-8ed5-53897d06e563
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Atualizar públicos-alvo e scripts de perfil do Target para compatibilidade com o SDK da Web da plataforma

Após concluir as atualizações técnicas para migrar o Target para o SDK da Web da plataforma, talvez seja necessário atualizar alguns de seus públicos, scripts de perfil e atividades para garantir uma transição suave.

Todos os parâmetros de mbox do Target devem ser passados no formato XDM com uma implementação do SDK da Web da Platform. Antes de publicar suas alterações na produção, você deve:

* Atualizar públicos-alvo que usam parâmetros de mbox
* Atualizar scripts de perfil que usam parâmetros mbox
* Atualizar todas as ofertas e atividades usando substituição de token de parâmetro de mbox (por exemplo, `${mbox.parameter_name}`)

## Ajustar públicos

Todos os públicos-alvo que usam parâmetros mbox personalizados devem ser atualizados para usar os novos nomes de parâmetros XDM. Por exemplo, um parâmetro personalizado para `page_name` provavelmente seria mapeado para `web.webpagedetails.pageName`.

Uma abordagem para garantir a compatibilidade com a at.js e o SDK da Web da Platform é atualizar qualquer público relevante para que as condições `OR` sejam usadas, como mostrado abaixo:

![Como exibir e atualizar um público-alvo do Target para compatibilidade com o SDK da Web da plataforma](assets/target-audience-update.png){zoomable="yes"}

## Editar scripts de perfil

Os scripts de perfil devem ser atualizados para fazer referência a novos nomes de parâmetros XDM, semelhantes aos públicos-alvo. Além da alteração dos nomes de parâmetros da mbox, não há diferença na forma como os scripts de perfil funcionam entre uma at.js e uma implementação do SDK da Web da Platform.

Uma abordagem para garantir a compatibilidade é usar `OR` condições no código de script do perfil.

Exemplo de script de perfil:

```Javascript
if(mbox.param('pageName') == 'Product Details'){
  return true
}
```

Atualização do script de perfil para compatibilidade com o SDK da Web da Platform:

```Javascript
if((mbox.param('pageName') == 'Product Details') || (mbox.param('web.webPageDetails.pageName') =='Product Details')){
  return true
}
```

Para obter mais informações e práticas recomendadas, consulte a documentação dedicada sobre [scripts de perfil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html?lang=pt-BR).

## Atualizar tokens de parâmetro para conteúdo dinâmico

Se você tiver ofertas, designs de recomendações ou atividades que usam [substituição de conteúdo dinâmico](https://experienceleague.adobe.com/docs/target/using/experiences/offers/passing-profile-attributes-to-the-html-offer.html?lang=pt-BR), talvez seja necessário atualizá-los de acordo para levar em conta os novos nomes de parâmetros XDM.

Dependendo de como você está usando a substituição de token para parâmetros mbox, talvez seja possível aprimorar a configuração existente para levar em conta nomes de parâmetros antigos e novos. No entanto, em situações em que o código JavaScript personalizado não é possível, como em ofertas JSON, você deve criar cópias e fazer atualizações após a conclusão da migração e estar ativo no site de produção.

Exemplo de oferta JSON:

```JSON
{
  "pageName" : "${mbox.page_name}",
  "layoutVariation" : "grid"
}
```

Exemplo de oferta JSON usando nomes de parâmetro do SDK da Web da plataforma:

```JSON
{
  "pageName" : "${mbox.web.webPagedDetails.pageName}",
  "layoutVariation" : "grid"
}
```

Se você optar por fazer ajustes após a migração para levar em conta os novos nomes de parâmetros da mbox XDM, pause todas as atividades afetadas durante o evento de migração para evitar que a atividade exiba erros para os visitantes.

Em seguida, saiba como [validar a implementação do Target](validate.md).

>[!NOTE]
>
>Estamos empenhados em ajudar você a ter sucesso com a migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=pt#M463).
