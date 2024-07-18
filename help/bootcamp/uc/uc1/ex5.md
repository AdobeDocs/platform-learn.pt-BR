---
title: Bootcamp - CDP em tempo real - Criar um público-alvo e agir - Enviar seu público-alvo para DV360
description: Bootcamp - CDP em tempo real - Criar um público-alvo e realizar ações - Enviar seu público-alvo para DV360
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
feature: Destinations
exl-id: 31f46e37-f1c0-4730-8520-1ccd98df6501
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---

# 1.5 Ação: enviar o público-alvo para a Facebook

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``Bootcamp``. Você pode fazer isso clicando no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. Depois de selecionar a [!UICONTROL sandbox] apropriada, você verá a alteração da tela e agora estará na [!UICONTROL sandbox] dedicada.

![Assimilação de dados](./images/sb1.png)

No menu esquerdo, vá para **Destinos** e, em seguida, vá para **Catálogo**. Você verá o **Catálogo de Destinos**. Em **Destinos**, clique em **Ativar públicos-alvo** no cartão **Público-alvo personalizado do Facebook**.

![RTCDP](./images/rtcdpgoogleseg.png)

Selecione o destino **bootcamp-facebook** e clique em **Avançar**.

![RTCDP](./images/rtcdpcreatedest2.png)

Na lista de públicos disponíveis, selecione o público criado no exercício anterior. Clique em **Next**.

![RTCDP](./images/rtcdpcreatedest3.png)

Na página **Mapeamento**, verifique se a caixa de seleção **Aplicar Transformação** está habilitada. Clique em **Next**.

![RTCDP](./images/rtcdpcreatedest4a.png)

Na página **Agenda de Público-alvo**, selecione a **Origem do seu público-alvo** e defina-a como **Diretamente dos clientes**. Clique em **Next**.

![RTCDP](./images/rtcdpcreatedest4.png)

Finalmente, na página **Revisão**, clique em **Concluir**.

![RTCDP](./images/rtcdpcreatedest5.png)

Seu público-alvo agora está vinculado aos Públicos-alvo personalizados da Facebook. Toda vez que um cliente se qualifica para esse público-alvo, um sinal é enviado para o lado do servidor do Facebook para incluí-lo no Público-alvo personalizado no lado do Facebook.

No Facebook, você encontrará seu público-alvo da Adobe Experience Platform em Públicos-alvo personalizados:

![RTCDP](./images/rtcdpcreatedest5b.png)

Agora você pode ver seu público-alvo personalizado no Facebook:

![RTCDP](./images/rtcdpcreatedest5a.png)

[Voltar para Fluxo de Usuário 1](./uc1.md)

[Voltar a todos os módulos](../../overview.md)
