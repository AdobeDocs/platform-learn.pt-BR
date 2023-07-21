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
source-wordcount: '912'
ht-degree: 0%

---

# 1.4 Ação: Desejo seu segmento para o Adobe Target

Acessado [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você acessará a página inicial da Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, você precisa atualizar um **sandbox**. O nome do sandbox a ser selecionado é Bootcamp. É possível fazer isso no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. painel de navegação o sandbox, você é a tela e agora está você em seu [!UICONTROL sandbox] Comparar.

![Assimilação de dados](./images/sb1.png)

## 1.4.1 Ativo seu segmento para o destino do Adobe Target

O Adobe Target está disponível como um destino do CDP em tempo real. Para inferir sua integração com o Adobe Target, acesse **Destinos** e **Catálogo**.

Clique em **Personalização** nenhum menu **Categorias**. Você verá o cartão de destino do **Adobe Target**. Clique em **Ativar segmentos**.

![EM](./images/atdest1.png)

o destino ``Bootcamp Target`` e clique **Próxima**.

![EM](./images/atdest3.png)

Na lista de conjuntos, o segmento que você criou em [1.3 Segmento de crime](./ex3.md), com o nome `yourLastName - Interest in Real-Time CDP`. Em seguida, clique em **Próxima**.

![EM](./images/atdest8.png)

Na próxima página, clique em **Próxima**.

![EM](./images/atdest9.png)

Clique em **Concluir**.

![EM](./images/atdest10.png)

Seu segmento agora está ocupado para o Adobe Target.

![EM](./images/atdest11.png)

>[!IMPORTANT]
>
>Imediato criar seu novo destino do Adobe Target no Real-Time CDP, pode levar até uma hora para o destino. Este é um um tempo de espera devido à definição da configuração de back-end. Depois que o tempo de espera inicial de 1 hora e a configuração do back-end, os segmentos de de passagem-que são atribuídos ao do Adobe Target para segmentação em tempo.

## 1.4.2 Configurar sua atividade no Adobe Target

que seu segmento Real-Time CDP está configurado para ser enviado ao Adobe Target, é possível acompanhar sua atividade de segmentação por experiência no Adobe Target. Neste exercício, você irá modificar uma base baseada no Visual Experience Composer.

Acessar a página inicial da Adobe Experience Cloud acessando [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Clique em **Target** para abrir.

![RTCDP](./images/excl.png)

Na página inicial do **Adobe Target**, você verá todas as atividades existentes.
Clique em **+ Criar atividade** para criar uma nova atividade.

![RTCDP](./images/exclatov.png)

µ **Direcionamento de experiência**.

![RTCDP](./images/exclatcrxt.png)

µ **Visual** e ➡ a **URL da atividade** como `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`, mas, antes disso, substitua XX por um número entre 01 e 60.

>[!IMPORTANT]
>
>Cada participante da capacitação deve usar uma página da Web para evitar a colisão de experiências do Adobe Target. É possível escolher uma página da Web e encontrar um URL acessando: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as partes do participante a mesma URL base e terminam com o número do participante.
>
>Por exemplo, o participante 1 deve usar um URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, o participante 30 deve usar um URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

o espaço de trabalho **AT Bootcamp**.

Clique em **Próxima**.

![RTCDP](./images/exclatcrxtdtlform.png)

Agora você não está no Visual Experience Composer. Pode de levar 20 a 30 segundos que o site carregado.

![RTCDP](./images/atform1.png)

público padrão são **Todos os visitantes**. Clique soe **3 pontos** ao lado de **Todos os visitantes** e clique em **Alterar público-alvo**.

![RTCDP](./images/atform3.png)

Agora você está vendo a lista de compromissos, e o segmento da Adobe Experience Platform pré-enviada e enviada ao Adobe Target agora faz parte da dessa lista. o segmento que você precedeu na Adobe Experience Platform. Clique em **Atribuir público-alvo**.

![RTCDP](./images/exclatvecchaud.png)

Seu segmento da Adobe Experience Platform agora parte dessa Atividade de segmentação por experiência.

![RTCDP](./images/atform4.png)

Antes de mudar a imagem principal, você deve mudar em **Permitir todos** nenhum banner de cookies.

Para isso, vá para **Procurar**

![RTCDP](./images/cook1.png)

Em seguida, clique em **Permitir todos**.

![RTCDP](./images/cook2.png)

Em seguida, representante para **Compor**.

![RTCDP](./images/cook3.png)

Agora vamos mudar a imagem principal na página inicial do site. Clique na imagem principal padrão sem site, clique em **Substituir conteúdo** e **Imagem**.

![RTCDP](./images/atform5.png)

Pesquisa o arquivo de imagem **rtcdp.png**. e clique em **Salvar**.

![RTCDP](./images/atform6.png)

Você verá a nova experiência com a nova imagem para o seu público selecionado

![RTCDP](./images/atform7.png)

Clique no título da sua atividade no canto superior para o exibido.

![RTCDP](./images/exclatvecname.png)

Para o nome, use:

- `seuSobrenome - RTCDP - XT (VEC)`

Clique em **Próxima**.

![RTCDP](./images/atform8.png)

Clique em **Próxima**.

![RTCDP](./images/atform8a.png)

Na página **Metas e configurações**, acesso **Métricas de meta**.

![RTCDP](./images/atform9.png)

Definir uma meta principal como **Envolvimento** - **Tempo no site**. Clique em **Salvar e fechar**.

![RTCDP](./images/vec3.png)

Agora você está na página **Visão geral da atividade**. Você ainda precisa de sua atividade.

![RTCDP](./images/atform10.png)

Clique no campo **Inativo** e **Ativar**.

![RTCDP](./images/atform11.png)

Você controla uma visão de que sua atividade está ativa.

![RTCDP](./images/atform12.png)

Agora sua atividade está ativa e pode ser testada no site do bootcamp.

Veja agora você ao seu site de documentação e visitar a página do produto para **Real-Time CDP**, você se qualifica classificados para o segmento que criou e verá a atividade do Adobe Target na página inicial em tempo real.

>[!IMPORTANT]
>
>Cada participante da capacitação deve usar uma página da Web para evitar a colisão de experiências do Adobe Target. É possível escolher uma página da Web e encontrar um URL acessando ao link: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as partes do participante a mesma URL base e terminam com o número do participante.
>
>Por exemplo, o participante 1 deve usar a `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, o participante 30 deve usar um URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

Próxima etapa: [1.5 Ação: Desejo seu segmento para o Facebook](./ex5.md)

[Retorno para Fluxo de monitoramento 1](./uc1.md)

[Retorno para Todos os compartilhados](../../overview.md)
