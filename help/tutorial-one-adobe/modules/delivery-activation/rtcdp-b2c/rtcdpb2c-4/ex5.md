---
title: Audience Activation para o Hub de eventos do Microsoft Azure - Ativar público
description: Audience Activation para o Hub de eventos do Microsoft Azure - Ativar público
kt: 5342
doc-type: tutorial
exl-id: e6bac0ce-4a1e-4458-af3e-3d6ac40b9cb5
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 5%

---

# 2.4.5 Ativar o público-alvo

## Adicionar público ao Destino do Hub de Eventos do Azure

Neste exercício, você adicionará seu público-alvo `--aepUserLdap-- - Interest in Plans` ao seu destino do Hub de Eventos do Azure `--aepUserLdap---aep-enablement`.

Faça logon no Adobe Experience Platform acessando esta URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepSandboxName--``. Depois de selecionar a sandbox apropriada, você verá a alteração da tela e agora estará em sua sandbox dedicada.

![Assimilação de dados](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

Vá para **Destinos** e clique em **Procurar**. Em seguida, você verá todos os destinos disponíveis. Localize seu destino, clique nos 3 pontos&#x200B;**...** conforme indicado abaixo e clique em **Ativar públicos**.

![5-01-select-destination.png](./images/501selectdestination.png)

Você verá isso. Pesquise seu público usando o LDAP e selecione `--aepUserLdap-- - Interest in Plans` na lista de públicos.

Clique em **Next**.

![5-04-select-segment.png](./images/504selectsegment.png)

Clique em **Adicionar novo campo**, clique em procurar esquema e selecione o campo `--aepTenantId--identification.core.ecid` (exclua qualquer outro campo que seja exibido automaticamente).

Clique em **Next**.

![5-05-select-attributes.png](./images/505selectattributes.png)

Clique em **Concluir**.

![5-06-destination-finish.png](./images/506destinationfinish.png)

Seu público-alvo agora está ativado para o destino do Microsoft Event Hub.

![5-07-destination-segment-Added.png](./images/507destinationsegmentadded.png)

## Próximas etapas

Ir para [2.4.6 Criar seu Projeto do Microsoft Azure](./ex6.md){target="_blank"}

Voltar para [Real-Time CDP: Audience Activation para o Hub de Eventos do Microsoft Azure](./segment-activation-microsoft-azure-eventhub.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
