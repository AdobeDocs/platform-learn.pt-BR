---
title: Habilitar suporte entre domínios - Migrar o Target da at.js 2.x para o SDK da Web
description: Saiba como configurar o Adobe Target para aplicativos móveis e entre domínios em cenários de navegador da Web usando o SDK da Web do Experience Platform.
exl-id: 6ec24ddc-8f6d-4331-a3ae-bd0f3a7d6e78
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# Ativar perfis de visitantes entre domínios

O SDK da Web da Platform oferece suporte a recursos de compartilhamento de ID de visitante que permitem aos clientes fornecer experiências personalizadas com mais precisão em seus domínios. Esse recurso permite fornecer personalização consistente em domínios e melhora a precisão do relatório de atividades do visitante, sem depender de cookies de terceiros.

## Pré-requisitos

Para usar o compartilhamento de ID entre domínios, você deve usar o SDK da Web da plataforma versão 2.11.0 ou posterior. Esse recurso também é compatível com o VisitorAPI.js versão 1.7.0 ou posterior.

O compartilhamento de ID entre domínios funciona ao anexar um parâmetro de cadeia de caracteres de consulta `adobe_mc` especial à URL do domínio de destino. Esse parâmetro é usado para especificar a ID do visitante em vez de gerar uma nova ID ou usar uma ID existente.

O domínio de destino deve usar qualquer uma dessas bibliotecas para o compartilhamento de ID entre domínios para processar o parâmetro `adobe_mc` e compartilhar a ID do visitante corretamente.

## Comparação de abordagens

Antes de implementar, determine primeiro se sua implementação existente usa a função `visitor.appendVisitorIDsTo()`. Qualquer código personalizado que use essa função deve ser atualizado para usar o novo comando do SDK da Web `appendIdentityToUrl`.

| VisitorAPI.js | SDK da Web da Platform |
| --- | --- |
| `visitor.appendVisitorIDsTo(*url*)` | `alloy("appendIdentityToUrl", { url: *url* })` |

## Usando o comando `appendIdentityToURL`

Para compartilhamento de ID entre domínios, o SDK da Web versão 2.11.0 adiciona suporte para o comando `appendIdentityToUrl`. Quando usado, este comando gera o parâmetro da cadeia de caracteres de consulta `adobe_mc`.

O comando aceita um objeto com uma propriedade, `url`, e retorna um objeto com a url da propriedade.

Esse comando não aguarda por nenhuma atualização de consentimento. Se o consentimento não foi fornecido, o URL é retornado inalterado.

Se uma ECID não for fornecida, o ponto de extremidade `/acquire` será chamado para gerar uma ECID.

Veja abaixo um exemplo de como implementar o compartilhamento de ID entre domínios.

Esse código adiciona um ouvinte de eventos para todos os cliques na página. Se o clique estava em um link para um domínio correspondente, neste caso adobe.com ou behance.com, ele adiciona a identidade ao URL e redireciona o usuário para lá.

```Javascript
document.addEventListener("click", event => {
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) {
    return;
  }
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith("adobe.com") && !url.hostname.endsWith("behance.com")) {
    return;
  }
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    document.location = result.url;
  });
});
```

>[!TIP]
>
>Ao usar o recurso de tags (antigo Launch) para implementar o SDK da Web, o compartilhamento de ID entre domínios pode ser realizado sem o código personalizado. Consulte a [documentação dedicada](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html#tags-extension) para obter mais detalhes.

>[!NOTE]
>
>O SDK da Web da Platform também oferece suporte ao compartilhamento de ID móvel para Web para casos de uso de aplicativos móveis nativos. Para obter mais informações, consulte a documentação dedicada sobre o [compartilhamento de ID móvel para a Web e entre domínios](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html).

Em seguida, saiba como [atualizar públicos-alvo e scripts de perfil](update-audiences.md) para garantir a compatibilidade com o SDK da Web da Platform.

>[!NOTE]
>
>Estamos empenhados em ajudar você a ter sucesso com a migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
