---
title: CDP em tempo real - Crie um segmento e execute ações - Configure um destino de publicidade como o Google DV360
description: CDP em tempo real - Crie um segmento e execute ações - Configure um destino de publicidade como o Google DV360
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 40441815-428a-48dc-a12e-91220d4ba307
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 1%

---

# 6.2 Configurar um destino de publicidade como o Google DV360

>[!IMPORTANT]
>
>O conteúdo abaixo destina-se a FYI - Você **NOT** precisa configurar um novo destino para DV360. O destino já foi criado e você pode usá-lo no próximo exercício.

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você será direcionado para a página inicial do Adobe Experience Platform.

![Assimilação de dados](../module2/images/home.png)

Antes de continuar, é necessário selecionar um **sandbox**. A sandbox a ser selecionada é chamada de ``--aepSandboxId--``. Você pode fazer isso clicando no texto **[!UICONTROL Produto de produção]** na linha azul na parte superior da tela. Depois de selecionar a [!UICONTROL sandbox], você verá a tela mudar e agora você estará em seu [!UICONTROL sandbox].

![Assimilação de dados](../module2/images/sb1.png)

No menu esquerdo, acesse **Destinos**, em seguida, vá para **Catálogo**. Você verá o **Catálogo de destinos**.

![RTCDP](./images/rtcdp.png)

Em **Destinos**, clique em **Tela e vídeo do Google 360** e, em seguida, clique em **+ Configurar**.

![RTCDP](./images/rtcdpgoogle.png)

Você verá isso. Clique em **Ligar ao destino**.

![RTCDP](./images/rtcdpgooglecreate1.png)

Na próxima tela, você pode configurar o destino para o Google DV360.

![RTCDP](./images/rtcdpgooglecreatedest.png)

Insira um valor nos campos **Nome** e **Descrição**.

O campo **ID da conta** é **ID do anunciante** da conta DV360. Você pode encontrar isso aqui:

![RTCDP](./images/rtcdpgoogledv360advid.png)

O **Tipo de conta** deve ser definido como **Convidar anunciante**.

Agora você tem isso. Clique em **Próximo**.

![RTCDP](./images/rtcdpgoogldv360new.png)

>[!NOTE]
>
>A Google precisa incluir o Adobe na lista de permissões para que o Adobe Experience Platform envie dados para o Google DV360. Entre em contato com o Gerente de conta da Google para ativar esse fluxo de dados.

Depois de criar o destino, você verá isso. Opcionalmente, é possível selecionar uma política de governança de dados. Em seguida, clique em **Salvar e sair**.

![RTCDP](./images/rtcdpcreatedest1.png)

Em seguida, você verá uma lista de destinos disponíveis.
No próximo exercício, você conectará o segmento criado no exercício anterior ao destino Google DV360.

Próxima etapa: [6.3 Tomar medidas: enviar seu segmento para o DV360](./ex3.md)

[Voltar ao Módulo 6](./real-time-cdp-build-a-segment-take-action.md)

[Voltar para todos os módulos](../../overview.md)
