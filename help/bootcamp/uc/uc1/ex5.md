---
title: Bootcamp - CDP em tempo real - Criar um segmento e realizar ações - Enviar seu segmento para DV360
description: Bootcamp - CDP em tempo real - Criar um segmento e realizar ações - Enviar seu segmento para DV360
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 31f46e37-f1c0-4730-8520-1ccd98df6501
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---

# 1.5 Ação: enviar o segmento para o Facebook

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, é necessário selecionar um **sandbox**. A sandbox a ser selecionada é chamada ``Bootcamp``. Você pode fazer isso clicando no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. Depois de selecionar as opções [!UICONTROL sandbox], você verá a alteração de tela e agora estará em seu dedicado [!UICONTROL sandbox].

![Assimilação de dados](./images/sb1.png)

No menu esquerdo, vá para **Destinos**, em seguida, vá para **Catálogo**. Você verá a **Catálogo de destinos**. Entrada **Destinos**, clique em **Ativar segmentos** no **Público-alvo personalizado do facebook** cartão.

![RTCDP](./images/rtcdpgoogleseg.png)

Selecionar o destino **bootcamp-facebook** e clique em **Próxima**.

![RTCDP](./images/rtcdpcreatedest2.png)

Na lista de segmentos disponíveis, selecione o segmento criado no exercício anterior. Clique em **Próximo**.

![RTCDP](./images/rtcdpcreatedest3.png)

No **Mapeamento** página, verifique se a variável **Aplicar transformação** está ativada. Clique em **Próximo**.

![RTCDP](./images/rtcdpcreatedest4a.png)

No **Agendamento do segmento** selecione a **Origem do seu público** e defina-o como **Diretamente dos clientes**. Clique em **Próximo**.

![RTCDP](./images/rtcdpcreatedest4.png)

Por último, no **Revisão** clique em **Concluir**.

![RTCDP](./images/rtcdpcreatedest5.png)

Seu segmento agora está vinculado aos Públicos-alvo personalizados do Facebook. Toda vez que um cliente se qualifica para esse segmento, um sinal é enviado para o lado do servidor do Facebook para incluir esse cliente no Público-alvo personalizado no lado do Facebook.

No Facebook, você encontrará seu segmento do Adobe Experience Platform em Públicos-alvo personalizados:

![RTCDP](./images/rtcdpcreatedest5b.png)

Agora você pode ver seu público-alvo personalizado no Facebook:

![RTCDP](./images/rtcdpcreatedest5a.png)

[Voltar para Fluxo de Usuário 1](./uc1.md)

[Voltar a todos os módulos](../../overview.md)
