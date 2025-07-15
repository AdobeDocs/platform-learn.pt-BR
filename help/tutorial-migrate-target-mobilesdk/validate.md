---
title: Validar e solucionar problemas de implementação da extensão do Offer Decisioning e do Target
description: Saiba como validar e solucionar problemas de uma implementação móvel do Adobe Target usando a extensão do Offer Decisioning e do Target.
exl-id: edc6e25a-58d7-4145-97c3-bf48e980914f
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Validar e solucionar problemas de implementação da extensão do Offer Decisioning e do Target

Depois de migrar sua implementação do Target da extensão do Target para a extensão do Offer Decisioning e do Target, é importante validar se tudo está funcionando corretamente antes de publicar qualquer alteração no aplicativo de produção. A Adobe recomenda o seguinte, que é abordado em detalhes nesta página:

* Realizar uma validação técnica para garantir que a implementação básica e as solicitações e respostas do Platform Mobile SDK estejam corretas
* Garantir que as atividades do Target sejam entregues e renderizadas corretamente
* Verifique se os relatórios funcionam corretamente
* Rever públicos-alvo e scripts de perfil para garantir que eles sejam compatíveis com o Platform Mobile SDK e a extensão Otimize
* Verifique se as integrações com o Adobe ou aplicativos de terceiros funcionam corretamente

Cada implementação do Target é diferente, dependendo da arquitetura do site e dos recursos usados. Você pode usar as tabelas abaixo como ponto de partida e adicionar quaisquer itens exclusivos à sua implementação.

## Validação técnica e solução de problemas

A validação técnica e a solução de problemas com o Platform Mobile SDK e a extensão do Offer Decisioning e do Target foram aprimoradas com o Assurance. Consulte as seguintes páginas de documentação para saber mais sobre esta ferramenta essencial:

* [Configurando plug-ins de decisão no Assurance](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/assurance-setup/){target=_blank}

* [Validando a configuração Otimizar SDK](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/optimize-configuration-view/){target=_blank}

* [Revisar solicitações e simular diferentes experiências](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/review-simulate/){target=_blank}

Depois de executar as etapas de validação acima, você pode ter certeza de que a implementação do Platform Mobile SDK com a extensão do Offer Decisioning e do Target está pronta para entrar em produção.

Parabéns, você chegou ao fim do tutorial! Boa sorte ao migrar sua implementação do Adobe Target para a extensão do Offer Decisioning e do Target.

>[!NOTE]
>
>Estamos empenhados em ajudá-lo a ser bem-sucedido na migração para dispositivos móveis do Target da extensão do Target para a extensão do Offer Decisioning e do Target. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
