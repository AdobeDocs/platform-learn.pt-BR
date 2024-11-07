---
title: Ativação de segmento para o Hub de eventos do Microsoft Azure - Ativar segmento
description: Ativação de segmento para o Hub de eventos do Microsoft Azure - Ativar segmento
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 2%

---

# 2.4.4 Ativar segmento

## 2.4.4.1 Adicionar segmento ao destino do Hub de eventos do Azure

Neste exercício, você adicionará seu segmento `--aepUserLdap-- - Interest in Equipment` ao seu destino do Hub de Eventos do Azure `--aepUserLdap---aep-enablement`.

Faça logon no Adobe Experience Platform acessando esta URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepSandboxName--``. Você pode fazer isso clicando no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. Depois de selecionar a sandbox apropriada, você verá a alteração da tela e agora estará em sua sandbox dedicada.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/sb1.png)

Vá para **Destinos** e clique em **Procurar**. Em seguida, você verá todos os destinos disponíveis. Localize seu destino e clique no ícone **+**, conforme indicado abaixo.

![5-01-select-destination.png](./images/5-01-select-destination.png)

Você verá isso. Pesquise seu segmento usando o ldap e selecione `--aepUserLdap-- - Interest in Equipment` na lista de segmentos.

Clique em **Next**.

![5-04-select-segment.png](./images/5-04-select-segment.png)

A Adobe Experience Platform Real-time CDP pode fornecer uma carga para dois tipos de destinos, destinos de segmento e destinos de perfil.

Os destinos de segmento receberão uma carga de qualificação de segmento predefinida que será discutida posteriormente. Essa carga contém **todas** as qualificações de segmento para um perfil específico. Mesmo para segmentos que não estão na lista de ativação do destino. Um exemplo desse destino de segmento são os **Hubs de Eventos do Azure** e o **AWS Kinesis**.

Os destinos baseados em perfil permitem escolher qualquer atributo (firstName, lastName, ...) do Esquema de união de perfil XDM e incluí-lo na carga de ativação. Um exemplo desse destino é o **Email Marketing**.

Como seu destino do Azure Event Hub é um destino **segment**, selecione, por exemplo, o campo `--aepTenantId--.identification.core.ecid`.

Clique em **Adicionar novo campo**, clique em procurar esquema e selecione o campo `--aepTenantId--identification.core.ecid` (exclua qualquer outro campo que seja exibido automaticamente).

Clique em **Next**.

![5-05-select-attributes.png](./images/5-05-select-attributes.png)

Clique em **Concluir**.

![5-06-destination-finish.png](./images/5-06-destination-finish.png)

Seu segmento agora está ativado em direção ao destino do Hub de eventos da Microsoft.

![5-07-destination-segment-Added.png](./images/5-07-destination-segment-added.png)

Próxima etapa: [2.4.5 Criar seu Projeto do Microsoft Azure](./ex5.md)

[Voltar ao módulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Voltar a todos os módulos](./../../../overview.md)
