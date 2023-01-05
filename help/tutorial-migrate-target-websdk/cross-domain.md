---
title: Habilitar suporte entre domínios | Migrar o Target da at.js 2.x para o SDK da Web
description: Saiba como configurar o Adobe Target para domínios cruzados e aplicativos móveis em cenários de navegador da Web usando o SDK da Web do Experience Platform.
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---

# Ativar perfis de visitante entre domínios

O SDK da Web da plataforma é compatível com os recursos de compartilhamento de ID de visitante que permitem que os clientes entreguem experiências personalizadas com mais precisão em todos os domínios. Esse recurso permite fornecer personalização consistente entre domínios e melhora a precisão dos relatórios de atividade do visitante, sem depender de cookies de terceiros.

## Pré-requisitos

Para usar o compartilhamento de ID entre domínios, você deve usar o SDK da Web da plataforma versão 2.11.0 ou posterior. Esse recurso também é compatível com a versão 1.7.0 ou posterior de VisitorAPI.js.

O compartilhamento de ID entre domínios funciona ao anexar um `adobe_mc` parâmetro da string de consulta para o URL do domínio de destino. Esse parâmetro é usado para especificar a ID de visitante em vez de gerar uma nova ID ou usar uma ID existente.

O domínio de destino deve usar qualquer uma dessas bibliotecas para o compartilhamento de ID entre domínios para processar a variável `adobe_mc` e compartilhar a ID do visitante corretamente.

## Comparação de abordagens

Antes de implementar, determine primeiro se sua implementação existente usa a variável `visitor.appendVisitorIDsTo()` . Qualquer código personalizado que use essa função deve ser atualizado para usar o novo `appendIdentityToUrl` comando SDK da Web.

| VisitorAPI.js | SDK da Web da Platform |
| --- | --- |
| `visitor.appendVisitorIDsTo(*url*)` | `alloy("appendIdentityToUrl", { url: *url* })` |

## Usar o `appendIdentityToURL` comando

Para compartilhamento de ID entre domínios, o SDK da Web versão 2.11.0 adiciona suporte para a variável `appendIdentityToUrl` comando. Quando usado, esse comando gera a variável `adobe_mc` parâmetro da string de consulta.

O comando aceita um objeto com uma propriedade, `url`e retorna um objeto com o url da propriedade.

Este comando não espera por nenhuma atualização de consentimento. Se o consentimento não tiver sido fornecido, o URL retornará inalterado.

Se uma ECID não for fornecida, a variável `/acquire` endpoint é chamado para gerar uma ECID.

Abaixo está um exemplo de como você pode implementar o compartilhamento de ID entre domínios.

Esse código adiciona um ouvinte de evento para todos os cliques na página. Se o clique estava em um link para um domínio correspondente, neste caso adobe.com ou behance.com, ele adiciona a identidade ao URL e redireciona o usuário lá.

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
>Ao usar o recurso de tags (antigo Launch) para implementar o SDK da Web, o compartilhamento de ID entre domínios pode ser feito sem código personalizado. Consulte a [documentação dedicada](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html#tags-extension) para obter mais detalhes.

>[!NOTE]
>
>O SDK da Web da plataforma também oferece suporte ao compartilhamento de IDs da Web para dispositivos móveis em casos de uso de aplicativos móveis nativos. Para obter mais informações, consulte a documentação dedicada sobre [compartilhamento de IDs entre domínios e dispositivos móveis para a Web](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html).

Em seguida, saiba como [atualizar públicos-alvo e scripts de perfil](update-audiences.md) para garantir a compatibilidade com o SDK da Web da plataforma.

>[!NOTE]
>
>Temos o compromisso de ajudar você a ser bem-sucedido com sua migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, informe-nos ao publicar em [este debate comunitário](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).