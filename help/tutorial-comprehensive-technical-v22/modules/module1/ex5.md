---
title: Foundation - Configuração da coleta de dados do Adobe Experience Platform e da extensão do SDK da Web - Implementar o Adobe Analytics e o Adobe Audience Manager
description: Foundation - Configuração da coleta de dados do Adobe Experience Platform e da extensão do SDK da Web - Implementar o Adobe Analytics e o Adobe Audience Manager
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: e3ef6534-9af9-4b8c-86d0-46f413f4ff6d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 11%

---

# 1.5 - Implementar o Adobe Analytics e o Adobe Audience Manager

## Contexto

Agora você sabe que os dados do XDM estão fluindo para a plataforma. Você explorará mais sobre o que é o XDM em [Módulo 2](./../module2/data-ingestion.md), bem como criar seu próprio esquema para rastrear variáveis personalizadas. Por enquanto, você verá o que acontece quando define seu Datastream para encaminhar dados para o Analytics e o Audience Manager.

## 1.5.1 Variáveis de mapeamento no Analytics

A Adobe Experience Platform [!DNL Web SDK] O mapeia determinados valores automaticamente, tornando uma nova implementação do Analytics por meio do SDK da Web o mais rápido possível. As variáveis mapeadas automaticamente são listadas [here](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html#data-collection).

Para dados XDM que não são mapeados automaticamente para [!DNL Adobe Analytics], você pode usar [dados de contexto](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=pt-BR) para corresponder a sua [schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=pt-BR). Em seguida, ele pode ser mapeado para [!DNL Analytics] usar [regras de processamento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html?lang=pt-BR) para preencher [!DNL Analytics] variáveis. Os dados de contexto e as regras de processamento serão conceitos familiares aos que trabalharam com o Analytics no passado, mas não se preocupam com os detalhes por enquanto se forem novos conceitos.

Você também pode usar um conjunto padrão de ações e listas de produtos para enviar ou recuperar dados com a AEP [!DNL Web SDK]. Para fazer isso, consulte [Produtos](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html?lang=en#data-collection).

### Dados de contexto

Para ser usado por [!DNL Analytics], os dados XDM são nivelados usando a notação de pontos e disponibilizados como `contextData`. A lista de pares de valores a seguir mostra um exemplo de `context data`:

```javascript
{
    "bh": "900",
    "bw": "1680",
    "c": "24",
    "c.a.d.key.[0]": "value1",
    "c.a.d.key.[1]": "value2",
    "c.a.d.object.key1": "value1",
    "c.a.d.object.key2.[0]": "value2",
    "c.a.x.environment.browserdetails.javascriptenabled": "true",
    "c.a.x.environment.type": "browser",
    "cust_hit_time_gmt": "1579781427",
    "g": "http://example.com/home",
    "gn": "home",
    "j": "1.8.5",
    "k": "Y",
    "s": "1680x1050",
    "tnta": "218287:1:0|0,218287:1:0|2,218287:1:0|1,218287:1:0|32767,218287:1:01,218287:1:0|0,218287:1:0|1,218287:1:0|0,218287:1:0|1",
    "user_agent": "Mozilla/5.0 AppleWebKit/537.36 Safari/537.36",
    "v": "Y"
}
```

### Regras de processamento

Todos os dados coletados pela rede de borda podem ser acessados pelas [regras de processamento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). Em [!DNL Analytics], você pode usar as regras de processamento para incorporar dados de contexto ao [!DNL Analytics] variáveis.

## 1.5.2 Audience Manager na rede Experience Platform Edge

O encaminhamento pelo lado do servidor não é um conceito novo para o Audience Manager, e o mesmo processo de antes se aplica. Também é possível sincronizar identidades.

## 1.5.3 Revise seu conjunto de dados para enviar dados para o Adobe Analytics

Caso deseje enviar os dados coletados pelo SDK da Web para a Adobe Analytics e a Adobe Audience Manager, siga essas etapas.

Ir para [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) e ir para **Datastreams**.

No canto superior direito da tela, selecione o nome da sandbox, que deve ser `--aepSandboxId--`. Abra o armazenamento de dados específico, que é nomeado como `--demoProfileLdap-- - Demo System Datastream`.

![Clique no ícone Configuração de borda no painel de navegação esquerdo](./images/edgeconfig1b.png)

Você verá isso. Para ativar o Adobe Analytics, clique em **+Adicionar serviço**.

![Depurador AEP](./images/aa2.png)

Você verá isso. Selecionar o serviço **Adobe Analytics**, depois disso, é necessário adicionar o conjunto de relatórios no Adobe Analytics para enviar dados no . Neste tutorial, isso está fora do escopo. Clique em **Cancelar**.

![Depurador AEP](./images/aa3.png)

## 1.5.4 Revise seu conjunto de dados para enviar dados para o Adobe Audience Manager

Você verá isso. Para ativar o Adobe Audience Manager, clique em **+Adicionar serviço**.

![Depurador AEP](./images/aa2.png)

Você verá isso. Selecionar o serviço **Adobe Audience Manager** depois disso, você pode decidir ativar ou desativar destinos de cookies e/ou destinos de URL do Adobe Audience Manager. Neste tutorial, essa configuração está fora do escopo. Clique em **Cancelar**.

![Depurador AEP](./images/aam1.png)

Próxima etapa: [1.6 Implementar o Adobe Target](./ex6.md)

[Voltar ao Módulo 1](./data-ingestion-launch-web-sdk.md)

[Voltar para todos os módulos](./../../overview.md)
