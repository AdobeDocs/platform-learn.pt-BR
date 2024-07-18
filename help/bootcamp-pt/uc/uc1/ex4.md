---
title: Bootcamp - CDP em tempo real - Criar um segmento e realizar ações - Enviar seu segmento para a Adobe Target - Brasil
description: Bootcamp - CDP em tempo real - Criar um segmento e realizar ações - Enviar seu segmento para a Adobe Target - Brasil
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
solution: Experience Platform, Target
feature: Segments, Integrations
exl-id: 862afd4c-1b6c-48fe-bc1f-967c065642e0
source-git-commit: ee5c0af17c12f1d90774a3a4150c9788e2368e39
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# 1.4 Ação: Desejo seu segmento para o Adobe Target

Acessado [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você acessará a página inicial da Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, você seleciona **sandbox**. O nome do sandbox a ser selecionado é Bootcamp. É possível fazer isso no texto **[!UICONTROL Produção Prod]** na linha azul na parte superior da tela. Depois de pegar a sandbox, você verá a tela e agora você está em seu [!UICONTROL sandbox].

![Assimilação de dados](./images/sb1.png)

## 1.4.1 Ativo seu segmento para o destino do Adobe Target

O Adobe Target está disponível como um destino do CDP em tempo real. Para contaminsua integração com o Adobe Target, acesse **Destinos** e **Catálogo**.

Clique em **Personalization** sem menu **Categorias**. Você verá o cartão de destino do **Adobe Target**. Clique em **Ativar segmentos**.

![ÀS](./images/atdest1.png)

ou destino ``Bootcamp Target`` e clique **Próximo**.

![ÀS](./images/atdest3.png)

Na lista de segmentos, o segmento que você criou em [1.3 ócio um segmento](./ex3.md), com o nome `yourLastName - Interest in Real-Time CDP`. Em seguida, clique em **Próximo**.

![ÀS](./images/atdest8.png)

Na próxima página, clique em **Próximo**.

![ÀS](./images/atdest9.png)

Clique em **Concluir**.

![ÀS](./images/atdest10.png)

Seu segmento agora está ocupado para o Adobe Target.

![ÀS](./images/atdest11.png)

>[!IMPORTANT]
>
>Imediato criar seu novo destino do Adobe Target no Real-Time CDP, pode levar até uma hora para o destino. Este é um um tempo de espera devido à definição da configuração de back-end. Depois que o tempo de espera inicial de 1 hora e a configuração do back-end, os segmentos de de passagem-que são atribuídos ao do Adobe Target para segmentação em tempo.

## 1.4.2 Configurar sua atividade no Adobe Target

que seu segmento Real-Time CDP está configurado para ser enviado ao Adobe Target, é possível acompanhar sua atividade de segmentação por experiência no Adobe Target. Neste exercício, você irá modificar uma base baseada no Visual Experience Composer.

Acessar a página inicial da Adobe Experience Cloud [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Clique em **Target** para abrir.

![RTCDP](./images/excl.png)

Na página inicial do **Adobe Target**, você verá todas as como atividades existentes.
Clique em **+ Criar atividade** para criar uma nova atividade.

![RTCDP](./images/exclatov.png)

µ **Direcionamento de experiência**.

![RTCDP](./images/exclatcrxt.png)

µ {0 Visual **e ➡ a** Atividade URL **como `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`, mas, antes disso, substitua XX por um número entre 01 e 60.**

>[!IMPORTANT]
>
>Cada participante da capacitação deve usar uma página da Web para evitar a colisão de experiências do Adobe Target. É possível escolher uma página da Web e encontrar um URL acessando: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as partes do participante a mesma URL base e terminam com o número do participante.
>
>Por exemplo, o participante 1 deve usar um URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, o participante 30 deve usar um URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

ou espaço de trabalho **AT Bootcamp**.

Clique em **Próximo**.

![RTCDP](./images/exclatcrxtdtlform.png)

Agora você não está no Visual Experience Composer. Pode de levar 20 a 30 segundos que o site carregado.

![RTCDP](./images/atform1.png)

Documentação, o público padrão são **Todos os visitantes**. Clique nos **3 pontos** ao lado de **Todos os visitantes** e clique em **Alterar público**.

![RTCDP](./images/atform3.png)

Agora você está vendo a lista de compromissos, e o segmento da Adobe Experience Platform pré-enviada e enviada ao Adobe Target agora faz parte da dessa lista. o segmento que você precedeu na Adobe Experience Platform. Clique em **Atribuir público**.

![RTCDP](./images/exclatvecchaud.png)

Seu segmento da Adobe Experience Platform agora parte dessa Atividade de segmentação por experiência.

![RTCDP](./images/atform4.png)

Antes de mudar a imagem principal, você deve mudar em **Permitir tudo** sem banner de cookies.

Isso, vá para **Procurar**

![RTCDP](./images/cook1.png)

Em seguida, clique em **Permitir tudo**.

![RTCDP](./images/cook2.png)

Em seguida, representante para **Compor**.

![RTCDP](./images/cook3.png)

Agora vamos mudar a imagem principal na página inicial do site. Clique na imagem principal padrão no site, clique em **Substituir conteúdo** e **Imagem**.

![RTCDP](./images/atform5.png)

Pesquisa o arquivo de imagem **rtcdp.png**. e clique em **Salvar**.

![RTCDP](./images/atform6.png)

Você verá a nova experiência com a nova imagem para o seu público selecionado

![RTCDP](./images/atform7.png)

Clique no título da sua atividade no canto superior para o exibido.

![RTCDP](./images/exclatvecname.png)

Para o nome, use:

- `seuSobrenome - RTCDP - XT (VEC)`

Clique em **Próximo**.

![RTCDP](./images/atform8.png)

Clique em **Próximo**.

![RTCDP](./images/atform8a.png)

Na página **Metas e configurações**, acessada **Métricas de meta**.

![RTCDP](./images/atform9.png)

Defina uma Meta principal como **Envolvimento** - **Tempo no Site**. Clique em **Salvar e fechar**.

![RTCDP](./images/vec3.png)

Agora você está na página **Visão geral da atividade**. Você ainda precisa de sua atividade.

![RTCDP](./images/atform10.png)

Clique no campo **Inativo** e **Ativar**.

![RTCDP](./images/atform11.png)

Você controla uma visão de que sua atividade está ativa.

![RTCDP](./images/atform12.png)

Agora sua atividade está ativa e pode ser testada no site do bootcamp.

Se agora você vai ao seu site de navegação e visitar a página do produto para **Real-Time CDP**, você se qualifica para o segmento que criou e verá a Adobe Target na página inicial em tempo real.

>[!IMPORTANT]
>
>Cada participante da capacitação deve usar uma página da Web para evitar a colisão de experiências do Adobe Target. É possível escolher uma página da Web e encontrar um URL acessando ao link: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as partes do participante a mesma URL base e terminam com o número do participante.
>
>Por exemplo, o participante 1 deve usar um `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, o participante 30 deve usar um URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

Próxima etapa: [1.5 Ação: desejada seu segmento para o Facebook](./ex5.md)

[Retorno para Fluxo de monitoramento 1](./uc1.md)

[Retorno para Todos os compartilhados](../../overview.md)
