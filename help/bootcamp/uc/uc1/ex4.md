---
title: Bootcamp - CDP em tempo real - Criar um público-alvo e realizar ações - Enviar seu público-alvo para a Adobe Target
description: Bootcamp - CDP em tempo real - Criar um público-alvo e realizar ações - Enviar seu público-alvo para a Adobe Target
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
solution: Experience Platform, Target
feature: Audiences, Integrations
exl-id: 6a76c2ab-96b7-4626-a6d3-afd555220b1e
source-git-commit: 9d12b3e3ad2238cf79aca3d9723e7e60d72e765c
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 1%

---

# 1.4 Ação: enviar o público-alvo para a Adobe Target

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, é necessário selecionar um **sandbox**. A sandbox a ser selecionada é chamada ``Bootcamp``. Você pode fazer isso clicando no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. Depois de selecionar as opções [!UICONTROL sandbox], você verá a alteração de tela e agora estará em seu dedicado [!UICONTROL sandbox].

![Assimilação de dados](./images/sb1.png)

## 1.4.1 Ativar o público-alvo para o destino do Adobe Target

O Adobe Target está disponível como um destino no Real-Time CDP. Para configurar a integração do Adobe Target, acesse **Destinos**, para **Catálogo**.

Clique em **Personalização** no **Categorias** menu. Você verá a **Adobe Target** cartão de destino. Clique em **Ativar públicos**.

![EM](./images/atdest1.png)

Selecionar o destino ``Bootcamp Target`` e clique em **Próxima**.

![EM](./images/atdest3.png)

Na lista de públicos disponíveis, selecione o público criado no [1.3 Criar um público-alvo](./ex3.md), que se chama `yourLastName - Interest in Real-Time CDP`. Em seguida, clique em **Próxima**.

![EM](./images/atdest8.png)

Na próxima página, clique em **Próxima**.

![EM](./images/atdest9.png)

Clique em **Concluir**.

![EM](./images/atdest10.png)

Seu público-alvo agora está ativado para o Adobe Target.

![EM](./images/atdest11.png)

>[!IMPORTANT]
>
>Quando você acaba de criar seu destino do Adobe Target no Real-Time CDP, pode levar até uma hora para o destino ficar ativo. Esse é um tempo de espera único, devido à definição da configuração de back-end. Quando o tempo de espera inicial de uma hora e a configuração de backend forem concluídas, os públicos-alvo de borda recém-adicionados enviados para o destino do Adobe Target estarão disponíveis para direcionamento em tempo real.

## 1.4.2 Configurar a atividade do Adobe Target baseada em formulários

Agora que seu público-alvo do Real-Time CDP está configurado para ser enviado para o Adobe Target, você pode configurar sua atividade de Direcionamento de experiência no Adobe Target. Neste exercício, você configurará uma atividade baseada no Visual Experience Composer.

Acesse a página inicial do Adobe Experience Cloud em [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Clique em **Target** para abri-lo.

![RTCDP](./images/excl.png)

No **Adobe Target** home page, você verá todas as Atividades existentes.
Clique em **+ Criar atividade** para criar uma nova Atividade.

![RTCDP](./images/exclatov.png)

Selecionar **Direcionamento de experiência**.

![RTCDP](./images/exclatcrxt.png)

Selecionar **Visual** e defina o **URL da atividade** para `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`, mas antes disso, substitua XX por um número entre 01 e 30.

>[!IMPORTANT]
>
>Todos os participantes da ativação devem usar uma página da Web separada para evitar a colisão de várias experiências do Adobe Target. Você pode escolher uma página da Web e encontrar o URL acessando aqui: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as páginas compartilham o mesmo URL base e terminam no número do participante.
>
>Como exemplo, o participante 1 deve usar o URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, o participante 30 deve usar o URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

Selecione o espaço de trabalho **AT Bootcamp**.

Clique em **Avançar**.

![RTCDP](./images/exclatcrxtdtlform.png)

Você está agora no Visual Experience Composer. Pode levar de 20 a 30 segundos até que o site seja totalmente carregado.

![RTCDP](./images/atform1.png)

O público-alvo padrão é atualmente **Todos os visitantes**. Clique no link **3 pontos** ao lado de **Todos os visitantes** e clique em **Alterar público-alvo**.

![RTCDP](./images/atform3.png)

Você está vendo a lista de públicos-alvo disponíveis, e o público-alvo da Adobe Experience Platform criado anteriormente e enviado para o Adobe Target agora faz parte dessa lista. Selecione o público criado anteriormente no Adobe Experience Platform. Clique em **Atribuir público-alvo**.

![RTCDP](./images/exclatvecchaud.png)

Seu público-alvo do Adobe Experience Platform agora faz parte dessa atividade de direcionamento de experiência.

![RTCDP](./images/atform4.png)

Antes de alterar a imagem herói, clique em **Permitir todos** no banner de cookie.

Para fazer isso, acesse **Procurar**

![RTCDP](./images/cook1.png)

Clique em **Permitir todos**.

![RTCDP](./images/cook2.png)

Em seguida, volte para **Compor**.

![RTCDP](./images/cook3.png)

Agora vamos alterar a imagem herói na página inicial do site. Clique na imagem herói padrão no site e clique em **Substituir conteúdo** e selecione **Imagem**.

![RTCDP](./images/atform5.png)

Procure o arquivo de imagem **rtcdp.png**. Selecione-a e clique em **Salvar**.

![RTCDP](./images/atform6.png)

Você verá a nova experiência com a nova imagem para o Público-alvo selecionado.

![RTCDP](./images/atform7.png)

Clique no título da atividade no canto superior esquerdo para renomeá-la.

![RTCDP](./images/exclatvecname.png)

Para o nome, use:

- `yourLastName - RTCDP - XT (VEC)`

Clique em **Avançar**.

![RTCDP](./images/atform8.png)

Clique em **Avançar**.

![RTCDP](./images/atform8a.png)

No **Metas e configurações** - página, vá para **Métricas de meta**.

![RTCDP](./images/atform9.png)

Defina a meta principal como **Envolvimento** - **Tempo no site**. Clique em **Salvar e fechar**.

![RTCDP](./images/vec3.png)

Agora você está no **Visão geral da atividade** página. Você ainda precisa ativar sua Atividade.

![RTCDP](./images/atform10.png)

Clique no campo **Inativo** e selecione **Ativar**.

![RTCDP](./images/atform11.png)

Em seguida, você receberá uma confirmação visual de que sua atividade está online.

![RTCDP](./images/atform12.png)

Sua atividade agora está online e pode ser testada no site de bootcamp.

Se você voltar ao site de demonstração e visitar a página do produto para **Real-Time CDP**, você se qualificará instantaneamente para o público-alvo criado e verá a atividade do Adobe Target ser exibida na página inicial em tempo real.

>[!IMPORTANT]
>
>Todos os participantes da ativação devem usar uma página da Web separada para evitar a colisão de várias experiências do Adobe Target. Você pode escolher uma página da Web e encontrar o URL acessando aqui: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as páginas compartilham o mesmo URL base e terminam no número do participante.
>
>Como exemplo, o participante 1 deve usar o URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, o participante 30 deve usar o URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

Próxima etapa: [1.5 Ação: enviar o público-alvo para a Facebook](./ex5.md)

[Voltar para Fluxo de Usuário 1](./uc1.md)

[Voltar a todos os módulos](../../overview.md)
