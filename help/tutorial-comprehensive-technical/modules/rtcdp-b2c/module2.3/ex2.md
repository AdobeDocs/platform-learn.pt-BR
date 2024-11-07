---
title: Real-time CDP - Criar um segmento e executar ações - Configurar um destino do Advertising como o Google DV360
description: Real-time CDP - Criar um segmento e executar ações - Configurar um destino do Advertising como o Google DV360
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 1%

---

# 2.3.2 Configurar um destino do Advertising como o Google DV360

>[!IMPORTANT]
>
>O conteúdo abaixo é intencional como informação - Você **NÃO** precisa configurar um novo destino para DV360. O destino já foi criado e você pode usá-lo no próximo exercício.

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepSandboxName--``. Você pode fazer isso clicando no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. Depois de selecionar a [!UICONTROL sandbox] apropriada, você verá a alteração da tela e agora estará na [!UICONTROL sandbox] dedicada.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/sb1.png)

No menu esquerdo, vá para **Destinos** e, em seguida, vá para **Catálogo**. Você verá o **Catálogo de Destinos**.

![RTCDP](./images/rtcdp.png)

Em **Destinos**, clique em **Google Display &amp; Video 360** e em **+ Configurar**.

![RTCDP](./images/rtcdpgoogle.png)

Você verá isso. Clique em **Conectar ao destino**.

![RTCDP](./images/rtcdpgooglecreate1.png)

Na próxima tela, você poderá configurar seu destino para o Google DV360.

![RTCDP](./images/rtcdpgooglecreatedest.png)

Insira um valor nos campos **Nome** e **Descrição**.

O campo **ID da Conta** é a **ID do Anunciante** da Conta DV360. Você pode encontrar isso aqui:

![RTCDP](./images/rtcdpgoogledv360advid.png)

O **Tipo de Conta** deve ser definido como **Convidar Anunciante**.

Agora você tem isto. Clique em **Next**.

![RTCDP](./images/rtcdpgoogldv360new.png)

>[!NOTE]
>
>A Google precisa adicionar o Adobe à lista de permissões para que o Adobe Experience Platform envie dados para o Google DV360. Entre em contato com o Gerente de conta da Google para ativar esse fluxo de dados.

Depois de criar o destino, você verá isso. Opcionalmente, é possível selecionar uma política de governança de dados. Em seguida, clique em **Salvar e sair**.

![RTCDP](./images/rtcdpcreatedest1.png)

Você verá uma lista de destinos disponíveis.
No próximo exercício, você conectará o segmento criado no exercício anterior ao destino do Google DV360.

Próxima Etapa: [2.3.3 Realizar Ação: enviar seu segmento para DV360](./ex3.md)

[Voltar ao módulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Voltar a todos os módulos](../../../overview.md)
