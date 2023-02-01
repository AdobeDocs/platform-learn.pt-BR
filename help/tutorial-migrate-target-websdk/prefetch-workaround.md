---
title: Solução alternativa para pré-busca | Migrar o Target da at.js 2.x para o SDK da Web
description: Saiba como implementar uma solução alternativa para transmitir parâmetros com busca prévia
source-git-commit: d061d2492d6d5e8e7a8a6e03ce63b9b6cd3793d8
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Solução alternativa para pré-busca

Todos os clientes do Target que não estavam em produção com o SDK da Web do Experience Platform antes de 1º de outubro de 2022 fazem uma solicitação para o Target a partir da rede de borda do Experience Platform usando o modo de &quot;busca prévia&quot;. A busca prévia permite que o navegador pré-carregue e armazene em cache as ofertas do Target para que estejam prontas para serem aplicadas quando o visitante atingir o estado correto da página. Isso é vantajoso em Aplicativos de página única (SPA), já que a experiência do usuário desejada pode ser renderizada o mais rápido possível, sem solicitações de rede adicionais. No entanto, há implicações importantes para implementações de SPA e não SPA.

Em vez de contar um visitante em uma atividade quando o conteúdo da oferta é entregue na solicitação de rede, os visitantes agora são contados em atividades quando um `propositionDisplay` A solicitação sendEvent é feita pelo SDK da Web. Essas solicitações são feitas automaticamente por atividades do Visual Experience Composer (VEC) quando renderDecisões for definido como true e quando a experiência for renderizada com êxito na página. Com escopos personalizados e quando renderDecisões é definido como falso, as solicitações propositionDisplay precisam ser iniciadas intencionalmente pelo implementador. Além disso, _todos os parâmetros utilizados para fins diferentes da qualificação imediata de atividade devem ser enviados através de um `propositionDisplay`  evento_.

## Por que a solução alternativa é necessária?

Em muitas implementações do Target, às vezes, solicitações de rede importantes são feitas sem esperar que uma atividade seja entregue. Por exemplo, os pedidos podem ser feitos para:

* Registrar conversões da ordem
* Definir parâmetros do perfil
* Acionar scripts de perfil
* Enviar parâmetros de entidade para preencher o catálogo do Recommendations

Infelizmente, no modo de busca prévia, eles não se comportam conforme o esperado. No modo de pré-busca, esses dados não são assimilados, a menos que façam parte de um `propositionDisplay`.

## Qual é a solução alternativa?

A solução alternativa consiste em três partes:

1. Definir um escopo personalizado como parte de `sendEvent`
1. Usar o escopo personalizado em uma atividade baseada em formulário (a atividade pode fornecer conteúdo padrão)
1. Use um manipulador de resposta para fazer outro `sendEvent` para o propositionDisplay e inclua os parâmetros necessários para capturar a ordem, defina os parâmetros do perfil, acione o script de perfil, envie os parâmetros da entidade, etc.

Por exemplo, este é um exemplo de como a solução alternativa pode ser usada para enviar um parâmetro de perfil:


```JavaScript
var data = {
    "__adobe": {
        "target": {
            "profile.gender": "male"
        }
    }
};
// Send the initial event with the data object and custom decision scope
alloy("sendEvent", {
    "renderDecisions": true,
    data,
    decisionScopes: ['profile-param-example']
}).then(function(result) {
    var propositions = result.propositions;
    var ctaProposition;
    if (propositions) {
        // Find the discount proposition, if it exists.
        for (var i = 0; i < propositions.length; i++) {
            var proposition = propositions[i];
            if (proposition.scope === "profile-param-example") {
                ctaProposition = proposition;
                break;
            }
        }
    }
    if (ctaProposition) {
        // Send a "decisioning.propositionDisplay" event signaling that the proposition has been rendered, and includes the data object again
        alloy("sendEvent", {
            xdm: {
                eventType: "decisioning.propositionDisplay",
                _experience: {
                    decisioning: {
                        propositions: [{
                            id: ctaProposition.id,
                            scope: ctaProposition.scope,
                            scopeDetails: ctaProposition.scopeDetails
                        }]
                    }
                }
            },
            data
        });
    }
});
```

Quando o perfil é definido como parte do propositionDisplay, ele salva no perfil do visitante e fica disponível em solicitações subsequentes. A mesma abordagem pode ser usada para relatar detalhes de conversão de pedido e parâmetros de entidade.

Nas tags , use o tipo de evento Enviar evento concluído para acionar um evento contendo o sendEvent adicional.

## Como faço para saber se minha implementação usa o modo de busca prévia?

Você deve abrir um tíquete de Atendimento ao cliente para descobrir se sua conta está usando o modo de busca prévia.


>[!NOTE]
>
>Temos o compromisso de ajudar você a ser bem-sucedido com sua migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, informe-nos ao publicar em [este debate comunitário](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).