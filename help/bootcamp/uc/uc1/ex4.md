---
title: Bootcamp - CDP em tempo real - Crie um segmento e execute ações - Envie seu segmento para o Adobe Target
description: Bootcamp - CDP em tempo real - Crie um segmento e execute ações - Envie seu segmento para o Adobe Target
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 6a76c2ab-96b7-4626-a6d3-afd555220b1e
source-git-commit: ead28f5631fc430c41e8c756b23dc69ffe19510e
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 1%

---

# 1.4 Tomar medidas: enviar seu segmento para a Adobe Target

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você será direcionado para a página inicial do Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, é necessário selecionar um **sandbox**. A sandbox a ser selecionada é chamada de ``Bootcamp``. Você pode fazer isso clicando no texto **[!UICONTROL Produto de produção]** na linha azul na parte superior da tela. Depois de selecionar a [!UICONTROL sandbox], você verá a tela mudar e agora você estará em seu [!UICONTROL sandbox].

![Assimilação de dados](./images/sb1.png)

## 1.4.1 Ativar seu segmento para o destino do Adobe Target

O Adobe Target está disponível como destino do Real-Time CDP. Para configurar a integração do Adobe Target, acesse **Destinos** para **Catálogo**.

Clique em **Personalização** no **Categorias** menu. Você verá o **Adobe Target** cartão de destino. Clique em **Ativar segmentos**.

![AT](./images/atdest1.png)

Selecione o destino ``Bootcamp Target`` e clique em **Próximo**.

![AT](./images/atdest3.png)

Na lista de segmentos disponíveis, selecione o segmento criado em [1.3 Criar um segmento](./ex3.md), que é nomeado como `yourLastName - Interest in Real-Time CDP`. Em seguida, clique em **Próximo**.

![AT](./images/atdest8.png)

Na próxima página, clique em **Próximo**.

![AT](./images/atdest9.png)

Clique em **Concluir**.

![AT](./images/atdest10.png)

Seu segmento agora é ativado no Adobe Target.

![AT](./images/atdest11.png)

>[!IMPORTANT]
>
>Quando você acabou de criar seu destino Adobe Target no Real-Time CDP, pode levar até uma hora para que o destino esteja ativo. Esse é um tempo de espera único, devido à configuração do back-end. Quando o tempo de espera inicial de 1 hora e a configuração de backend forem concluídos, os segmentos de borda recém-adicionados que são enviados para o destino do Adobe Target estarão disponíveis para direcionamento em tempo real.

## 1.4.2 Configurar a atividade baseada em formulário do Adobe Target

Agora que seu segmento do Real-Time CDP está configurado para ser enviado ao Adobe Target, você pode configurar a atividade de Direcionamento de experiência no Adobe Target. Neste exercício, você configurará uma atividade baseada no Visual Experience Composer.

Acesse a página inicial do Adobe Experience Cloud acessando [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Clique em **Target** para abri-lo.

![RTCDP](./images/excl.png)

No **Adobe Target** página inicial, você verá todas as atividades existentes.
Clique em **+ Criar atividade** para criar uma nova Atividade.

![RTCDP](./images/exclatov.png)

Selecionar **Direcionamento de experiência**.

![RTCDP](./images/exclatcrxt.png)

Selecionar **Visual** e defina a **URL da atividade** para `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`, mas antes de fazer isso, substitua XX por um número entre 01 e 30.

>[!IMPORTANT]
>
>Cada participante da ativação deve usar uma página da Web separada para evitar a colisão de várias experiências do Adobe Target. Você pode escolher uma página da Web e encontrar o URL acessando aqui: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as páginas compartilham o mesmo URL básico e terminam no número do participante.
>
>Como exemplo, o participante 1 deve usar o URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, o participante 30 deve usar URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

Selecionar o espaço de trabalho **Em Bootcamp**.

Clique em **Próximo**.

![RTCDP](./images/exclatcrxtdtlform.png)

Agora você está no Visual Experience Composer. Pode levar de 20 a 30 segundos até que o site esteja totalmente carregado.

![RTCDP](./images/atform1.png)

O público-alvo padrão está no momento **Todos os visitantes**. Clique no botão **3 pontos** ao lado de **Todos os visitantes** e clique em **Alterar público-alvo**.

![RTCDP](./images/atform3.png)

Agora você está vendo a lista de públicos disponíveis, e o segmento do Adobe Experience Platform que você criou e enviou anteriormente para o Adobe Target agora faz parte dessa lista. Selecione o segmento criado anteriormente no Adobe Experience Platform. Clique em **Atribuir público-alvo**.

![RTCDP](./images/exclatvecchaud.png)

Seu segmento do Adobe Experience Platform agora faz parte dessa atividade de direcionamento de experiência.

![RTCDP](./images/atform4.png)

Antes de alterar a imagem herói, você precisará clicar em **Permitir Tudo** no banner de cookie.

Para fazer isso, acesse **Procurar**

![RTCDP](./images/cook1.png)

Em seguida, clique em **Permitir Tudo**.

![RTCDP](./images/cook2.png)

Em seguida, volte para **Compor**.

![RTCDP](./images/cook3.png)

Agora vamos mudar a imagem herói na página inicial do site. Clique na imagem herói padrão no site e clique em **Substituir conteúdo** e depois selecione **Imagem**.

![RTCDP](./images/atform5.png)

Pesquisar o arquivo de imagem **rtcdp.png**. Selecione-o e clique em **Salvar**.

![RTCDP](./images/atform6.png)

Você verá a nova experiência com a nova imagem, para o público-alvo selecionado.

![RTCDP](./images/atform7.png)

Clique no título da atividade no canto superior esquerdo para renomeá-la.

![RTCDP](./images/exclatvecname.png)

Para o nome, use:

- `yourLastName - RTCDP - XT (VEC)`

Clique em **Próximo**.

![RTCDP](./images/atform8.png)

Clique em **Próximo**.

![RTCDP](./images/atform8a.png)

No **Metas e configurações** - página, vá para **Métricas de meta**.

![RTCDP](./images/atform9.png)

Defina a meta principal como **Envolvimento** - **Tempo no Site**. Clique em **Salvar e fechar**.

![RTCDP](./images/vec3.png)

Você está agora no **Visão geral da atividade** página. Ainda é necessário ativar sua atividade.

![RTCDP](./images/atform10.png)

Clique no campo **Inativo** e selecione **Ativar**.

![RTCDP](./images/atform11.png)

Em seguida, você receberá uma confirmação visual de que sua atividade agora está ativa.

![RTCDP](./images/atform12.png)

Sua atividade agora está ao vivo e pode ser testada no site de bootcamp.

Agora, volte ao seu site de demonstração e visite a página do produto para **Real-Time CDP**, você se qualificará instantaneamente para o segmento criado e verá a atividade do Adobe Target ser exibida na página inicial em tempo real.

>[!IMPORTANT]
>
>Cada participante da ativação deve usar uma página da Web separada para evitar a colisão de várias experiências do Adobe Target. Você pode escolher uma página da Web e encontrar o URL acessando aqui: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as páginas compartilham o mesmo URL básico e terminam no número do participante.
>
>Como exemplo, o participante 1 deve usar o URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, o participante 30 deve usar URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

Próxima etapa: [1.5 Tomar medidas: enviar seu segmento para a Facebook](./ex5.md)

[Voltar para Fluxo de Usuário 1](./uc1.md)

[Voltar para todos os módulos](../../overview.md)
