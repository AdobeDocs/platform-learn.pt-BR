---
title: Ativação de segmento para o Hub de eventos do Microsoft Azure - Ativar segmento
description: Ativação de segmento para o Hub de eventos do Microsoft Azure - Ativar segmento
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 250f8536-b6bd-4c64-a552-80d5c6fb6358
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 2%

---

# 13.4 Ativar segmento

## 13.4.1 Adicionar segmento ao destino do Hub de eventos do Azure

Neste exercício, você adicionará seu segmento `--demoProfileLdap-- - Interest in Equipment` para `--demoProfileLdap---aep-enablement` Destino do Hub de Eventos do Azure.

Faça logon no Adobe Experience Platform acessando este URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer logon, você será direcionado para a página inicial do Adobe Experience Platform.

![Assimilação de dados](../module2/images/home.png)

Antes de continuar, é necessário selecionar um **sandbox**. A sandbox a ser selecionada é chamada de ``--aepSandboxId--``. Você pode fazer isso clicando no texto **[!UICONTROL Produto de produção]** na linha azul na parte superior da tela. Depois de selecionar a sandbox apropriada, você verá a tela mudar e agora estará na sandbox dedicada.

![Assimilação de dados](../module2/images/sb1.png)

Ir para **Destinos**, depois clique em **Procurar**. Em seguida, você verá todos os destinos disponíveis. Localize seu destino e clique no botão **+** conforme indicado abaixo.

![5-01-select-destination.png](./images/5-01-select-destination.png)

Você verá isso. Procure seu segmento usando seu ldap e selecione `--demoProfileLdap-- - Interest in Equipment` na lista de segmentos.

Clique em **Próximo**.

![5-04-select-segment.png](./images/5-04-select-segment.png)

A CDP em tempo real da Adobe Experience Platform pode fornecer uma carga para dois tipos de destinos, destinos de segmento e destinos de perfil.

Os destinos de segmento receberão uma carga de qualificação de segmento predefinida que será discutida posteriormente. Essa carga contém **all** as qualificações de segmento para um perfil específico. Mesmo para segmentos que não estão na lista de ativação do destino. Um exemplo desse destino de segmento é **Hubs de Eventos do Azure** e **AWS Kinesis**.

Os destinos baseados em perfil permitem escolher qualquer atributo (firstName, lastName, ...) do Esquema de união de perfis do XDM e incluí-lo na carga de ativação. Um exemplo desse destino é o **Marketing por email**.

Porque seu destino do Hub de Eventos do Azure é um **segmento** destino, selecione, por exemplo, o campo `--aepTenantId--.identification.core.ecid`.

Clique em **Adicionar novo campo**, clique em procurar schema e selecione o campo `--aepTenantId--identification.core.ecid` (exclua qualquer outro campo que fosse exibido automaticamente).

Clique em **Próximo**.

![5-05-select-attributes.png](./images/5-05-select-attributes.png)

Clique em **Concluir**.

![5-06-destination-end.png](./images/5-06-destination-finish.png)

Seu segmento agora é ativado no destino do Hub de eventos do Microsoft.

![5-07-destination-segment-added.png](./images/5-07-destination-segment-added.png)

Próxima etapa: [13.5 Criar o projeto do Microsoft Azure](./ex5.md)

[Voltar ao Módulo 13](./segment-activation-microsoft-azure-eventhub.md)

[Voltar para todos os módulos](./../../overview.md)
