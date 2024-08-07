---
title: Bootcamp - CDP em tempo real - Criar um segmento e realizar ações - Enviar seu segmento para DV360 - Brasil
description: Bootcamp - CDP em tempo real - Criar um segmento e realizar ações - Enviar seu segmento para DV360 - Brasil
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
feature: Destinations
exl-id: acb32859-6f82-44e0-8948-a045a9fe2afe
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 1%

---

# 1.5 Ação: Desejo seu segmento para o Facebook

Acessado [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você acessará a página inicial da Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, você seleciona **sandbox**. O nome do sandbox a ser selecionado é Bootcamp. É possível fazer isso no texto **[!UICONTROL Produção Prod]** na linha azul na parte superior da tela. Depois de pegar a sandbox, você verá a tela e agora você está em seu [!UICONTROL sandbox].

![Assimilação de dados](./images/sb1.png)

Nenhum menu à esquerda, vá para **Destinos** e, em seguida, vá para **Catálogo**. Você verá o **Catálogo de destinos**. Em **Destinos**, clique em **Ativar Segmentos** no cartão **Público-alvo personalizado do Facebook**.

![RTCDP](./images/rtcdpgoogleseg.png)

o **bootcamp-facebook** e clique em **Próximo**.

![RTCDP](./images/rtcdpcreatedest2.png)

Na lista de conjuntos, o segmento que criou no exercício anterior. Clique em **Próximo**.

![RTCDP](./images/rtcdpcreatedest3.png)

Na página **Mapeamento**, se a caixa de seleção **Aplicar transformação** está. Clique em **Próximo**.

![RTCDP](./images/rtcdpcreatedest4a.png)

Na página **Agendamento de segmento**, uma **Origem do seu público-alvo** e como **Diretamente dos clientes**. Clique em **Próximo**.

![RTCDP](./images/rtcdpcreatedest4.png)

Por fim, na página **Avaliação**, clique em **Concluir**.

![RTCDP](./images/rtcdpcreatedest5.png)

Seu segmento agora está vinculado aos Públicos Personalizados do Facebook. Sempre que um cliente se qualificar para esse segmento, um sinal será enviado ao lado do servidor do Facebook para incluir cliente não personalizado no lado do Facebook.

Não há Facebook, você tem seu segmento da Adobe Experience Platform em Públicos Personalizados:

![RTCDP](./images/rtcdpcreatedest5b.png)

Agora você pode ver seu público no Facebook:

![RTCDP](./images/rtcdpcreatedest5a.png)

[Retorno para Fluxo de monitoramento 1](./uc1.md)

[Retorno para Todos os compartilhados](../../overview.md)
