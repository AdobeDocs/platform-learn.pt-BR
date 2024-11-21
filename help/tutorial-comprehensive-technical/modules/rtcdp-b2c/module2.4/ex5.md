---
title: Audience Activation para o Hub de eventos do Microsoft Azure - Ativar público
description: Audience Activation para o Hub de eventos do Microsoft Azure - Ativar público
kt: 5342
doc-type: tutorial
exl-id: 89cfda0e-6c5e-45ab-9506-f0f0f6211e7f
source-git-commit: b4a7144217a68bc0b1bc70b19afcbc52e226500f
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 4%

---

# 2.4.5 Ativar o público-alvo

## Adicionar público ao Destino do Hub de Eventos do Azure

Neste exercício, você adicionará seu público-alvo `--aepUserLdap-- - Interest in Plans` ao seu destino do Hub de Eventos do Azure `--aepUserLdap---aep-enablement`.

Faça logon no Adobe Experience Platform acessando esta URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepSandboxName--``. Depois de selecionar a sandbox apropriada, você verá a alteração da tela e agora estará em sua sandbox dedicada.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/sb1.png)

Vá para **Destinos** e clique em **Procurar**. Em seguida, você verá todos os destinos disponíveis. Localize seu destino, clique nos 3 pontos**...** conforme indicado abaixo e clique em **Ativar públicos**.

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

Próxima etapa: [2.4.6 Criar seu Projeto do Microsoft Azure](./ex6.md)

[Voltar ao módulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Voltar a todos os módulos](./../../../overview.md)
