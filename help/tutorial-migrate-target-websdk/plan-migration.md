---
title: Planejamento | Migrar o Target da at.js 2.x para o SDK da Web
description: Saiba como planejar sua implementação do Adobe Target da at.js 2.x para o Adobe Experience Platform Web SDK.
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# Planejar a migração da at.js para o SDK da Web da plataforma

Antes de atualizar para o SDK da Web da plataforma no seu site, você deve avaliar sua implementação atual.

## Avaliar a implementação atual da at.js

A primeira etapa para uma migração bem-sucedida é ter uma compreensão firme de sua implementação atual do at.js Target. Há recursos, funções e código personalizado que você pode usar que exigem atualizações. Considere o seguinte ao avaliar:

### Quais recursos são compatíveis?

O SDK da Web da plataforma está em desenvolvimento ativo contínuo e os recursos e aprimoramentos são adicionados regularmente. Conforme você avalia a implementação atual da at.js, consulte o [casos de uso suportados](https://github.com/orgs/adobe/projects/18/views/1) para obter as informações mais recentes.

### Quais funções você usa hoje?

O SDK da Web da plataforma é uma nova biblioteca que consolida todas as soluções do Adobe para os sites em um único SDK. Isso permite uma integração mais rígida e habilita novos recursos exclusivos do Adobe Experience Platform. No entanto, isso também significa que as funções da at.js não são compatíveis com o SDK da Web da plataforma. Conforme você avalia a implementação atual, observe o seguinte:

- Funções da at.js como `getOffer()` e `applyOffer()`
- Modificações nas configurações globais do Target
- Integração com o Adobe Analytics
- Uso de um script de mitigação de cintilação
- Uso de tokens de resposta
- Uso de mbox, perfil e parâmetros de entidade
- Código personalizado exclusivo para sua implementação

### Qual abordagem de migração você seguirá?

Depois de revisitar sua implementação da at.js, é necessário determinar uma abordagem de migração. Há duas opções:

- Migre todos os aplicativos do Adobe de uma só vez em todo o site
- Migrar página por página

Como o SDK da Web da plataforma combina e habilita vários aplicativos do Adobe, você deve coordenar a migração do Target de outros aplicativos do Adobe, como o Analytics e o Audience Manager. Todas as bibliotecas Adobe em uma determinada página devem ser migradas ao mesmo tempo. Não há suporte para uma implementação mista do SDK da Web da plataforma para Target e AppMeasurement para Analytics em uma página específica. No entanto, uma implementação mista em diferentes páginas é compatível, por exemplo, SDK da Web da plataforma na página A e at.js com AppMeasurement na página B.

À medida que migrar, você deve planejar seguir o processo de teste e lançamento de novo código de sua empresa e usar coisas como ambientes de desenvolvimento, de controle de qualidade e de preparo, antes de lançar para produção.

>[!CAUTION]
>
>As ofertas de redirecionamento não são suportadas nas migrações página por página se o redirecionamento de uma página com uma biblioteca para uma página com uma biblioteca diferente


Em seguida, analise os detalhes [comparação da at.js com o SDK da Web da plataforma](detailed-comparison.md) para melhor compreender as diferenças técnicas e identificar as áreas que requerem maior atenção.

>[!NOTE]
>
>Temos o compromisso de ajudar você a ser bem-sucedido com sua migração do Target da at.js para o SDK da Web. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, informe-nos ao publicar em [este debate comunitário](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
