---
title: Atualizar públicos-alvo e scripts de perfil | Migrar o Target da at.js 2.x para o SDK da Web
description: Saiba como atualizar públicos-alvo e scripts de perfil do Adobe Target para compatibilidade com o Experience Platform Web SDK.
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---

# Atualizar públicos-alvo do Target e scripts de perfil para compatibilidade com o SDK da Web da plataforma

Após concluir as atualizações técnicas para migrar o Target para o SDK da Web da plataforma, talvez seja necessário atualizar alguns de seus públicos-alvo, scripts de perfil e atividades para garantir uma transição suave.

Todos os parâmetros de mbox do Target devem ser enviados no formato XDM com uma implementação do SDK da Web da plataforma. Antes de publicar suas alterações na produção, você deve:

* Atualizar públicos-alvo que usam parâmetros mbox
* Atualizar scripts de perfil que usam parâmetros de mbox
* Atualize qualquer oferta e atividade usando a substituição de token do parâmetro da mbox (por exemplo, `${mbox.parameter_name}`)

## Ajustar públicos-alvo

Qualquer público-alvo que use parâmetros mbox personalizados deve ser atualizado para usar os novos nomes de parâmetros XDM. Por exemplo, um parâmetro personalizado para `page_name` provavelmente seria mapeado para `web.webpagedetails.pageName`.

Uma abordagem para garantir a compatibilidade com o at.js e o SDK da Web da plataforma é atualizar qualquer público relevante para que `OR` são usadas, conforme mostrado abaixo:

![Como visualizar a atualização de um público-alvo do Target para compatibilidade com o SDK da Web da plataforma](assets/target-audience-update.png)

## Editar scripts de perfil

Os scripts de perfil devem ser atualizados para fazer referência aos novos nomes de parâmetros XDM, de modo semelhante aos públicos-alvo. Além da alteração dos nomes de parâmetros da mbox, não há diferença na maneira como os scripts de perfil funcionam entre uma at.js e uma implementação do SDK da Web da plataforma.

Uma abordagem para garantir a compatibilidade é utilizar `OR` no código do script de perfil.

Exemplo de script de perfil:

```Javascript
if(mbox.param('pageName') == 'Product Details'){
  return true
}
```

Script de perfil atualizado para compatibilidade com o SDK da Web da plataforma:

```Javascript
if((mbox.param('pageName') == 'Product Details') || (mbox.param('page.webpagedetails.pageName') =='Product Details')){
  return true
}
```

Para obter mais informações e práticas recomendadas, consulte a documentação dedicada sobre [scripts de perfil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html).

## Atualizar tokens de parâmetro para conteúdo dinâmico

Se você tiver ofertas, designs de recomendações ou atividades que usam [substituição de conteúdo dinâmico](https://experienceleague.adobe.com/docs/target/using/experiences/offers/passing-profile-attributes-to-the-html-offer.html), elas podem precisar ser atualizadas adequadamente para considerar os novos nomes de parâmetros XDM.

Dependendo de como você está usando a substituição de token para parâmetros de mbox, talvez seja possível aprimorar sua configuração existente para cuidar dos nomes de parâmetro novos e antigos. No entanto, em situações em que o código JavaScript personalizado não é possível, como em ofertas JSON, você deve criar cópias e fazer atualizações depois que a migração for concluída e ativa no site de produção.

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
  "pageName" : "${mbox.web.webpagedetails.pageName}",
  "layoutVariation" : "grid"
}
```

Se você optar por fazer ajustes após a migração para levar em conta os novos nomes de parâmetro da mbox XDM, não deixe de pausar quaisquer atividades afetadas durante o evento de migração para evitar erros de exibição de atividade para os visitantes.

Em seguida, saiba como [validar a implementação do Target](validate.md).

>[!NOTE]
>
>Temos o compromisso de ajudar você a ser bem-sucedido com sua migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, informe-nos ao publicar em [este debate comunitário](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).