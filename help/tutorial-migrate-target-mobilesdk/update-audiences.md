---
title: Atualizar públicos-alvo e scripts de perfil do Target - Migrar a implementação do Adobe Target no aplicativo móvel para o Adobe Journey Optimizer - Extensão de decisão
description: Saiba como atualizar públicos-alvo e scripts de perfil do Adobe Target para compatibilidade com a extensão do Decisioning.
exl-id: de3ce2c7-0066-496a-a8a7-994d7ce3d92c
source-git-commit: b8baa6d48b9a99d2d32fad2221413b7c10937191
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Atualizar públicos-alvo e scripts de perfil do Target para compatibilidade com a extensão móvel do Decisioning


Após concluir as atualizações técnicas para migrar o Target para a extensão Decisioning, talvez seja necessário atualizar alguns dos públicos-alvo, scripts de perfil e atividades para garantir uma transição suave.

>[!INFO]
>
>Se você migrar todos os parâmetros da mbox para o objeto `data.__adobe.target`, não precisará atualizar os públicos, scripts de perfil e atividades, conforme mostrado abaixo.


Se você migrar parâmetros de mbox para o objeto `xdm`, antes de publicar suas alterações na produção, deverá:

* Atualizar públicos-alvo que usam parâmetros de mbox
* Atualizar scripts de perfil que usam parâmetros mbox
* Atualizar todas as ofertas e atividades usando substituição de token de parâmetro de mbox (por exemplo, `${mbox.parameter_name}`)

## Ajustar públicos

Se você migrar parâmetros de mbox para o objeto `xdm`, os públicos-alvo que usam parâmetros de mbox personalizados deverão ser atualizados para usar os novos nomes de parâmetros XDM. Por exemplo, um parâmetro personalizado para `page_name` provavelmente seria mapeado para `web.webpagedetails.pageName`.

Uma abordagem para garantir a compatibilidade com a extensão do Target e a extensão de Decisão é atualizar qualquer público relevante para que `OR` condições sejam usadas, conforme mostrado abaixo:

![Como exibir e atualizar um público-alvo do Target para compatibilidade com a extensão do Decisioning](assets/target-audience-update.png){zoomable="yes"}

## Editar scripts de perfil

Se você migrar parâmetros mbox para o objeto `xdm`, scripts de perfil deverão ser atualizados para fazer referência aos novos nomes de parâmetros XDM, semelhantes aos públicos-alvo. Além da alteração dos nomes de parâmetros da mbox, não há diferença na forma como os scripts de perfil funcionam entre uma implementação do Target e do Decisioning.

Uma abordagem para garantir a compatibilidade é usar `OR` condições no código de script do perfil.

Exemplo de script de perfil:

```Javascript
if(mbox.param('pageName') == 'Product Details'){
  return true
}
```

Atualização do script de perfil para compatibilidade com o Platform Web SDK:

```Javascript
if((mbox.param('pageName') == 'Product Details') || (mbox.param('web.webPageDetails.pageName') =='Product Details')){
  return true
}
```

Para obter mais informações e práticas recomendadas, consulte a documentação dedicada sobre [scripts de perfil](https://experienceleague.adobe.com/en/docs/target/using/audiences/visitor-profiles/profile-parameters).

## Atualizar tokens de parâmetro para conteúdo dinâmico

Se você migrar parâmetros mbox para o objeto `xdm` e tiver ofertas, designs de recomendações ou atividades que usam [substituição de conteúdo dinâmico](https://experienceleague.adobe.com/en/docs/target/using/experiences/offers/passing-profile-attributes-to-the-html-offer), talvez seja necessário atualizá-los de acordo para levar em conta os novos nomes de parâmetros XDM.

Dependendo de como você está usando a substituição de token para parâmetros mbox, talvez seja possível aprimorar a configuração existente para levar em conta nomes de parâmetros antigos e novos. No entanto, em situações em que o código JavaScript personalizado não é possível, como em ofertas JSON, você deve criar cópias e fazer atualizações após a conclusão da migração e estar ativo no site de produção.

Exemplo de oferta JSON:

```JSON
{
  "pageName" : "${mbox.page_name}",
  "layoutVariation" : "grid"
}
```

Exemplo de oferta JSON usando nomes de parâmetro de objeto XDM:

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
>Estamos empenhados em ajudá-lo a ser bem-sucedido na migração para dispositivos móveis do Target da extensão do Target para a extensão do Decisioning. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
