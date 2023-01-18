---
title: Bootcamp - CDP em tempo real - Crie um segmento e execute ações - Envie seu segmento para DV360
description: Bootcamp - CDP em tempo real - Crie um segmento e execute ações - Envie seu segmento para DV360
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 31f46e37-f1c0-4730-8520-1ccd98df6501
source-git-commit: ead28f5631fc430c41e8c756b23dc69ffe19510e
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---

# 1.5 Tomar medidas: enviar seu segmento para a Facebook

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você será direcionado para a página inicial do Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, é necessário selecionar um **sandbox**. A sandbox a ser selecionada é chamada de ``Bootcamp``. Você pode fazer isso clicando no texto **[!UICONTROL Produto de produção]** na linha azul na parte superior da tela. Depois de selecionar a [!UICONTROL sandbox], você verá a tela mudar e agora você estará em seu [!UICONTROL sandbox].

![Assimilação de dados](./images/sb1.png)

No menu esquerdo, acesse **Destinos**, em seguida, vá para **Catálogo**. Você verá o **Catálogo de destinos**. Em **Destinos**, clique em **Ativar segmentos** no **Público-alvo personalizado do facebook** cartão.

![RTCDP](./images/rtcdpgoogleseg.png)

Selecione o destino **bootcamp-facebook** e clique em **Próximo**.

![RTCDP](./images/rtcdpcreatedest2.png)

Na lista de segmentos disponíveis, selecione o segmento que você criou no exercício anterior. Clique em **Próximo**.

![RTCDP](./images/rtcdpcreatedest3.png)

No **Mapeamento** verifique se a variável **Aplicar transformação** a caixa de seleção está ativada. Clique em **Próximo**.

![RTCDP](./images/rtcdpcreatedest4a.png)

No **Agendamento do segmento** selecione o **Origem do público-alvo** e defina-o como **Diretamente dos clientes**. Clique em **Próximo**.

![RTCDP](./images/rtcdpcreatedest4.png)

Por último, no **Revisão** página, clique em **Concluir**.

![RTCDP](./images/rtcdpcreatedest5.png)

Seu segmento agora está vinculado aos Públicos personalizados da Facebook. Toda vez que um cliente se qualifica para esse segmento, um sinal será enviado para o lado do servidor do Facebook para incluir esse cliente no Público-alvo personalizado no lado do Facebook.

No Facebook, você encontrará seu segmento no Adobe Experience Platform em Públicos personalizados :

![RTCDP](./images/rtcdpcreatedest5b.png)

Agora é possível ver seu público-alvo personalizado aparecer no Facebook:

![RTCDP](./images/rtcdpcreatedest5a.png)

[Voltar para Fluxo de Usuário 1](./uc1.md)

[Voltar para todos os módulos](../../overview.md)
