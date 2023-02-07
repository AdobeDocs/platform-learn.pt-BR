---
title: Bootcamp - CDP em tempo real - Crie um segmento e execute ações - Envie seu segmento para o Adobe Target - Brasil
description: Bootcamp - CDP em tempo real - Crie um segmento e execute ações - Envie seu segmento para o Adobe Target - Brasil
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 5d824244766135cd4998feab48be7f6a69c42a70
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# 1.4 Ação: segmento do ambiente para o Adobe Target

Acesse [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de &quot;Faça&quot;, você vai acessar um início do logon no Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, você precisa selecionar um **sandbox**. O nome faz sandbox a ser selecionado é Bootcamp. É possível isto clicando texto **[!UICONTROL Produto de produção]** na linha azul na parte superior da tela. Depois de selecionar o sandbox apropriado, você verá a tela mudando e agora está em sua [!UICONTROL sandbox] dedicado.

![Assimilação de dados](./images/sb1.png)

## 1.4.1 O segmento ativo para o destino Adobe Target

O Adobe Target está disponível como destino do CDP em tempo real. Para configurar sua empresa com o Adobe Target, acesse **Destinos** e **Catálogo**.

Clique em **Personalização** nenhum menu **Categorias**. Você verá o cartão de destino **Adobe Target**. Clique em **Ativar segmentos**.

![AT](./images/atdest1.png)

Selecione de Destino ``Bootcamp Target`` e panelinha **Próximo**.

![AT](./images/atdest3.png)

Na lista de segmentos disponíveis, selecione do segmento que você criou em [1.3 Segmento de Crie](./ex3.md), com o nome `yourLastName - Interest in Real-Time CDP`. Em **Próximo**.

![AT](./images/atdest8.png)

No início, clique em **Próximo**.

![AT](./images/atdest9.png)

Clique em **Concluir**.

![AT](./images/atdest10.png)

Seu segmento agora está ativado para o Adobe Target.

![AT](./images/atdest11.png)

>[!IMPORTANT]
>
>Imediapós, Real-Time CDP do Adobe Target no., onde leva uma hora que se encontra ativado. Este é um tempo de espera único à configuração. Depois que que o tempo de início do início de 1 hora e a configuração back-end forem concluídos, os segmentos de borda recém-adicionados que são enviados ao destino Adobe Target estarão para segem tempo real.

## 1.4.2 Configuração do Adobe Target

Agora que o segmento é o Real-Time CDP está configurado para ser enviado ao Adobe Target, é possível configurar sua Adobe Target de Segmentação por experiência no. Você vai configurar uma não baseada Visual Experience Composer.

Acessar o início da Adobe Experience Cloud [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Clique em **Target** para.

![RTCDP](./images/excl.png)

Na posição inicial **Adobe Target**, você .
Clique em **+ Criar atividade** Para uma nova.

![RTCDP](./images/exclatov.png)

Selecione **Direcionamento de experiência**.

![RTCDP](./images/exclatcrxt.png)

Selecione **Visual** e defina a **URL da atividade** como `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`, mas, antes disso, substitua XX por um número inteiro 01 e 60.

>[!IMPORTANT]
>
>participante reiniciar a capacidade da Web separada para evitar um colisão de várias do Adobe Target. É possível voltar escolher uma vez na Web e acessar um URL: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as páginas compartil em uma mesma base de URL e terminam com o número do participante.
>
>Por exemplo, o participante 1 usar a URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, o participante 30 usar uma URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

Selecione no espaço de trabalho **Em Bootcamp**.

Clique em **Próximo**.

![RTCDP](./images/exclatcrxtdtlform.png)

Agora você está no Visual Experience Composer. Pode levar 20 a 30 segundos até que local esteja carregado.

![RTCDP](./images/atform1.png)

Atualmente, o padrão são **Todos os visitantes**. Clique nos **3 pontos** ao lado **Todos os visitantes** e panelinha **Alterar público-alvo**.

![RTCDP](./images/atform3.png)

Agora você está vendendo a lista de disponíveis, e o segmento da Adobe Experience Platform que você criou anteriormente e Adobe Target agora faz parte lista. Selecione no segmento que você criou anteriormente na Adobe Experience Platform. Clique em **Atribuir público-alvo**.

![RTCDP](./images/exclatvecchaud.png)

Seu segmento da Adobe Experience Platform agora faz parte de segmentação por experiência.

![RTCDP](./images/atform4.png)

Antes de alterar a imagem, você clicar em **Permitir Tudo** sem banner de cookies.

Para isso, vá para **Procurar**

![RTCDP](./images/cook1.png)

Em **Permitir Tudo**.

![RTCDP](./images/cook2.png)

Em, torne para **Compor**.

![RTCDP](./images/cook3.png)

Agora, mude uma imagem principal no site inicial. Clique na imagem principal da família no site, clique em **Substituir conteúdo** e selecione **Imagem**.

![RTCDP](./images/atform5.png)

Pesquisas sobre assinaturas **rtcdp.png**. Selecione e clique em **Salvar**.

![RTCDP](./images/atform6.png)

Você verá uma nova experiência com uma nova imagem para o seu Público selecionado

![RTCDP](./images/atform7.png)

Clique no título da sua, canto superior renomeá-la.

![RTCDP](./images/exclatvecname.png)

Para o nome, use:

- `seuSobrenome - RTCDP - XT (VEC)`

Clique em **Próximo**.

![RTCDP](./images/atform8.png)

Clique em **Próximo**.

![RTCDP](./images/atform8a.png)

Na tela **Metas e configurações**, acesse **Métricas de meta**.

![RTCDP](./images/atform9.png)

Defina um Meta-principal como **Envolvimento** - **Tempo no Site**. Clique em **Salvar e fechar**.

![RTCDP](./images/vec3.png)

Agora, você **Visão geral da atividade**. Você precisa ativar sua atividade.

![RTCDP](./images/atform10.png)

Clique no campo **Inativo** e selecione **Ativar**.

![RTCDP](./images/atform11.png)

Você receberá uma confirmação visual de que é confiscora está ativa.

![RTCDP](./images/atform12.png)

Ágora, ativa e pode testada

Veja agora você está no site de demonstração e visitar um passo para o produto **Real-Time CDP** Por outro lado, você qualificará o instantará para o segmento que e Adobe Target a exibida no início em tempo real.

>[!IMPORTANT]
>
>participante reiniciar a capacidade da Web separada para evitar um colisão de várias do Adobe Target. É possível voltar ao início da Web e um link de acesso ao URL: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as páginas compartil em uma mesma base de URL e terminam com o número do participante.
>
>Por exemplo, o participante 100 `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, o participante 30 usar uma URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

Proxima. [1.5 Ação: segmento do ambiente para o Facebook](./ex5.md)

[Retornar para Fluxo de Correio](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
