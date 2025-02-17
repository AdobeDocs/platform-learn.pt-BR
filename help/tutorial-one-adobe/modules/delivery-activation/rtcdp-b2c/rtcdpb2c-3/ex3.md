---
title: Real-time CDP - Criar um público-alvo e realizar ações - Enviar o público-alvo para DV360
description: Real-time CDP - Criar um público-alvo e realizar ações - Enviar o público-alvo para DV360
kt: 5342
doc-type: tutorial
exl-id: 5cdb1f66-580c-4b3f-ada6-e224762eab59
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 3%

---

# 2.3.3 Ação: enviar o público-alvo para o DV360

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepSandboxName--``. Depois de selecionar a [!UICONTROL sandbox] apropriada, você verá a alteração da tela e agora estará na [!UICONTROL sandbox] dedicada.

![Assimilação de dados](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

No menu esquerdo, vá para **Destinos** e vá para **Procurar**. Você verá o destino **DV360**. Clique nos 3 pontos **...** e clique em **Ativar públicos-alvo**.

![RTCDP](./images/rtcdpmenudest.png)

Na lista de públicos disponíveis, selecione o público criado no exercício anterior. Clique em **Next**.

![RTCDP](./images/rtcdpcreatedest3.png)

Na página **Agenda de Público-alvo**, clique em **Avançar**.

![RTCDP](./images/rtcdpcreatedest4.png)

Finalmente, na página **Revisão**, clique em **Concluir**.

![RTCDP](./images/rtcdpcreatedest5.png)

Seu público-alvo agora está vinculado ao Google DV360. Toda vez que um cliente se qualifica para esse público-alvo, um sinal é enviado ao Google DV360 para incluí-lo no público-alvo do Google DV360.

## Próximas etapas

Ir para [2.3.4 Realizar ação: enviar o público-alvo para um destino S3](./ex4.md){target="_blank"}

Voltar para a [CDP em tempo real - Criar um público-alvo e executar ações](./real-time-cdp-build-a-segment-take-action.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
