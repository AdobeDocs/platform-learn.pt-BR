---
title: Real-time CDP - Criar um segmento e executar ações - Enviar o segmento para DV360
description: Real-time CDP - Criar um segmento e executar ações - Enviar o segmento para DV360
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 2%

---

# 2.3.3 Realizar ação: enviar seu segmento para o DV360

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepSandboxName--``. Você pode fazer isso clicando no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. Depois de selecionar a [!UICONTROL sandbox] apropriada, você verá a alteração da tela e agora estará na [!UICONTROL sandbox] dedicada.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/sb1.png)

No menu esquerdo, vá para **Destinos** e, em seguida, vá para **Catálogo**. Você verá o **Catálogo de Destinos**.

![RTCDP](./images/rtcdpmenudest.png)

Em **Destinos**, clique em **Ativar Segmentos** no cartão **Google Display &amp; Video 360**.

![RTCDP](./images/rtcdpgoogleseg.png)

Selecione seu destino e clique em **Avançar**.

![RTCDP](./images/rtcdpcreatedest2.png)

Na lista de segmentos disponíveis, selecione o segmento criado no exercício anterior. Clique em **Next**.

![RTCDP](./images/rtcdpcreatedest3.png)

Na página **Agendamento de segmento**, clique em **Avançar**.

![RTCDP](./images/rtcdpcreatedest4.png)

Finalmente, na página **Revisão**, clique em **Concluir**.

![RTCDP](./images/rtcdpcreatedest5.png)

Seu segmento agora está vinculado ao Google DV360. Toda vez que um cliente se qualifica para esse segmento, um sinal é enviado ao Google DV360 para incluí-lo no Público-alvo no Google DV360.

Próxima etapa: [2.3.4 Executar ação: enviar seu segmento para um destino S3](./ex4.md)

[Voltar ao módulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Voltar a todos os módulos](../../../overview.md)
