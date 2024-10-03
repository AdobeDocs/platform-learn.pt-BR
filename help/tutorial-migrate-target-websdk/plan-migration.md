---
title: Planejamento - Migrar o Target da at.js 2.x para o SDK da Web
description: Saiba como planejar a implementação do Adobe Target de at.js 2.x para o Adobe Experience Platform Web SDK.
exl-id: 0e8f9cde-f361-4f69-886d-aad3074cd9b2
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Planejar a migração da at.js para o SDK da Web da plataforma

Antes de atualizar para o SDK da Web da Platform em seu site, você deve avaliar sua implementação atual.

## Avaliar a implementação atual da at.js

A primeira etapa para uma migração bem-sucedida é ter uma sólida compreensão da sua implementação atual do at.js Target. Há recursos, funções e código personalizado que você pode usar que exigem atualizações. Considere o seguinte ao avaliar:

### Quais recursos são compatíveis?

O SDK da Web da Platform está em desenvolvimento ativo contínuo, e recursos e melhorias são adicionados regularmente. Conforme você avalia a implementação atual da at.js, consulte a página [casos de uso suportados](https://github.com/orgs/adobe/projects/18/views/1) para obter as informações mais recentes.

### Que funções você usa hoje?

O Platform Web SDK é uma nova biblioteca que consolida todas as soluções de Adobe para os sites em um único SDK. Isso permite uma integração mais estreita e novos recursos exclusivos do Adobe Experience Platform. No entanto, isso também significa que as funções da at.js não são compatíveis com o SDK da Web da plataforma. Ao avaliar sua implementação atual, anote o seguinte:

- Funções da at.js, como `getOffer()` e `applyOffer()`
- Modificações nas configurações globais do Target
- Integração com o Adobe Analytics
- Uso de um script de mitigação de cintilação
- Uso de tokens de resposta
- Uso de parâmetros de mbox, perfil e entidade
- Código personalizado exclusivo para sua implementação

### Qual abordagem de migração você adotará?

Depois de revisitar a implementação da at.js, é necessário determinar uma abordagem de migração. Há duas opções:

- Migre todos os aplicativos de Adobe de uma só vez em todo o site
- Migrar página por página

Como o SDK da Web da Platform combina e habilita vários aplicativos Adobe, você deve coordenar a migração do Target de outros aplicativos Adobe, como o Analytics e o Audience Manager. Todas as bibliotecas de Adobe em uma determinada página devem ser migradas ao mesmo tempo. Não há suporte para uma implementação mista do SDK da Web da Platform para Target e AppMeasurement para Analytics em uma página específica. No entanto, uma implementação mista em diferentes páginas é compatível, por exemplo, SDK da Web da Platform na página A e at.js com AppMeasurement na página B.

À medida que você migra, deve seguir o processo da empresa para testar e lançar novos códigos e usar coisas como desenvolvimento, controle de qualidade e ambientes de preparo antes de liberar para produção.

>[!CAUTION]
>
>As ofertas de redirecionamento não são suportadas em migrações página por página se o redirecionamento de uma página com uma biblioteca for para uma página com uma biblioteca diferente


Em seguida, analise a [comparação detalhada da at.js com o SDK da Web da Platform](detailed-comparison.md) para obter uma melhor compreensão das diferenças técnicas e identificar áreas que exigem foco adicional.

>[!NOTE]
>
>Estamos empenhados em ajudar você a ter sucesso com a migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
