---
title: Real-time CDP - Criar um segmento e executar ações - Enviar o segmento para a Adobe Target
description: Real-time CDP - Criar um segmento e executar ações - Enviar o segmento para a Adobe Target
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 3%

---

# 2.3.5 Realizar ação: enviar seu segmento para o Adobe Target

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepSandboxName--``. Você pode fazer isso clicando no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. Depois de selecionar a [!UICONTROL sandbox] apropriada, você verá a alteração da tela e agora estará na [!UICONTROL sandbox] dedicada.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/sb1.png)

## 2.3.5.1 Verificar o fluxo de dados

O destino do Adobe Target no Real-Time CDP é conectado ao fluxo de dados usado para assimilar dados na rede de Adobe. Se quiser secionar seu destino do Adobe Target, primeiro verifique se o fluxo de dados já está ativado para o Adobe Target. Seu datastream foi configurado no [Exercício 0.2 Criar seu Datastream](./../../../modules/gettingstarted/gettingstarted/ex2.md) e foi nomeado como `--aepUserLdap-- - Demo System Datastream`.

Vá para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) e clique em **Datastreams** ou **Datastreams (Beta)**.

![Assimilação de dados](./images/atdestds1.png)

No canto superior direito da tela, selecione o nome da sandbox, que deve ser `--aepSandboxName--`.

![Clique no ícone Configuração do Edge na navegação à esquerda](./images/edgeconfig1b.png)

Em Datastreams, pesquise por seu datastream chamado `--aepUserLdap-- - Demo System Datastream`. Clique na sequência de dados para abri-la.

![Assimilação de dados](./images/atdestds3.png)

Você verá isto, clique em **...** ao lado de **Adobe Experience Platform** e em **Editar**.

![Assimilação de dados](./images/atdestds4.png)

Marque as caixas de seleção para **Segmentação do Edge** e **Destinos do Personalization**. Clique em **Salvar**.

![Assimilação de dados](./images/atdestds4a.png)

Em seguida, clique em **+ Adicionar Serviço**.

![Assimilação de dados](./images/atdestds4b.png)

Selecione o serviço **Adobe Target**. Clique em **Salvar**.

![Assimilação de dados](./images/atdestds5.png)

A sequência de dados agora está configurada para o Adobe Target.

![Assimilação de dados](./images/atdestds5a.png)

## 2.3.5.2 Configurar o destino do Adobe Target

O Adobe Target está disponível como um destino no Real-Time CDP. Para configurar sua integração com o Adobe Target, vá para **Destinos**, para **Catálogo**.

![ÀS](./images/atdest1.png)

Clique em **Personalization** no menu **Categorias**. Você verá o cartão de destino **Adobe Target**. Clique em **Ativar segmentos** (ou **Configurar** dependendo do seu ambiente).

![ÀS](./images/atdest2.png)

Dependendo do seu ambiente, talvez seja necessário clicar em **+ Configurar novo destino** para começar a criar seu destino.

![ÀS](./images/atdest3.png)

Você verá isso.

![ÀS](./images/atdest4.png)

Na tela **Configurar novo destino**, você precisa configurar dois itens:

- Nome: use o nome `--aepUserLdap-- - Adobe Target (Web)`, que deve ter esta aparência: **vangeluw - Adobe Target (Web)**.
- ID da sequência de dados: é necessário selecionar a sequência de dados configurada no [Exercício 0.2 Criar sequência de dados](./../../../modules/gettingstarted/gettingstarted/ex2.md). O nome da sequência de dados deve ser: `--aepUserLdap-- - Demo System Datastream`.

Clique em **Next**.

![ÀS](./images/atdest5.png)

Na próxima tela, você pode selecionar uma política de governança. Não é necessário selecionar um. Nesse caso, não há necessidade de selecionar um. Portanto, clique em **Criar**.

![ÀS](./images/atdest6.png)

Seu destino foi criado e será mostrado na lista. Selecione seu destino e clique em **Avançar** para iniciar o envio de segmentos para seu destino.

![ÀS](./images/atdest7.png)

Na lista de segmentos disponíveis, selecione o segmento criado no [Exercício 6.1 Criar um segmento](./ex1.md), denominado `--aepUserLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`. Em seguida, clique em **Avançar**.

![ÀS](./images/atdest8.png)

Na próxima página, clique em **Avançar**.

![ÀS](./images/atdest9.png)

Clique em **Concluir**.

![ÀS](./images/atdest10.png)

Seu segmento agora está ativado para o Adobe Target.

![ÀS](./images/atdest11.png)

>[!IMPORTANT]
>
>Quando você acaba de criar seu destino do Adobe Target no Real-Time CDP, pode levar até uma hora para o destino ficar ativo. Esse é um tempo de espera único, devido à definição da configuração de back-end. Quando a configuração inicial de 1 hora de tempo de espera e backend for concluída, os segmentos de borda recém-adicionados enviados para o destino do Adobe Target estarão disponíveis para direcionamento em tempo real.

## 2.3.5.3 Configurar a atividade do Adobe Target baseada em formulários

Agora que seu segmento do Real-Time CDP está configurado para ser enviado para o Adobe Target, você pode configurar sua atividade de Direcionamento de experiência no Adobe Target. Neste exercício, você configurará uma atividade baseada em formulário.

Vá para a página inicial do Adobe Experience Cloud em [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Clique em **Target** para abri-lo.

![RTCDP](./images/excl.png)

Na página inicial do **Adobe Target**, você verá todas as atividades existentes.

![RTCDP](./images/exclatov.png)

Clique em **+ Criar atividade** para criar uma nova Atividade.

![RTCDP](./images/exclatcr.png)

Selecione **Direcionamento de experiência**.

![RTCDP](./images/exclatcrxt.png)

Selecione **Formulário** e selecione **Nenhuma Restrição de Propriedade**. Clique em **Next**.

![RTCDP](./images/exclatcrxtdtlform.png)

Agora você está no compositor de atividades baseado em formulários.

![RTCDP](./images/atform1.png)

Para o campo **LOCATION 1**, selecione **target-global-mbox**.

![RTCDP](./images/atform2.png)

O público-alvo padrão é atualmente **Todos os visitantes**. Clique nos **3 pontos** ao lado de **Todos os visitantes** e clique em **Alterar público**.

![RTCDP](./images/atform3.png)

Agora você está vendo a lista de públicos-alvo disponíveis, e o segmento do Adobe Experience Platform criado anteriormente e enviado para o Adobe Target agora faz parte dessa lista. Selecione o segmento criado anteriormente no Adobe Experience Platform. Clique em **Atribuir público**.

![RTCDP](./images/exclatvecchaud.png)

Seu segmento do Adobe Experience Platform agora faz parte dessa atividade de direcionamento de experiência.

![RTCDP](./images/atform4.png)

Agora vamos alterar a Imagem do Herói na página inicial do site. Clique para abrir a lista suspensa ao lado de **Conteúdo padrão** e clique em **Criar oferta HTML**.

![RTCDP](./images/atform5.png)

Cole o código a seguir. Em seguida, clique em **Avançar**.

```javascript
<script>document.querySelector("#home > div > div > div > div > div.banner_img.d-none.d-lg-block > img").src="https://parsefiles.back4app.com/hgJBdVOS2eff03JCn6qXXOxT5jJFzialLAHJixD9/ff92fdc3885972c0090ad5419e0ef4d4_Luma - Product - Proteus - Hero Banner.png"; document.querySelector(".banner_text > *").remove()</script>
```

![RTCDP](./images/atform6.png)

Você verá a nova experiência com a nova imagem para o Público-alvo selecionado.

![RTCDP](./images/atform7.png)

Clique no título da atividade no canto superior esquerdo para renomeá-la.

![RTCDP](./images/exclatvecname.png)

Para o nome, use:

- `--aepUserLdap-- - RTCDP - XT (Form)`

![RTCDP](./images/atform8.png)

Clique em **Next**.

![RTCDP](./images/exclatvecnamenext.png)

Na página **Metas e configurações** -, vá para **Métricas de meta**.

![RTCDP](./images/atform9.png)

Defina a Meta primária como **Envolvimento** - **Tempo no site**.

![RTCDP](./images/vec3.png)

Clique em **Salvar e fechar**.

![RTCDP](./images/vecsave.png)

Agora você está na página **Visão geral da atividade**. Você ainda precisa ativar sua Atividade.

![RTCDP](./images/atform10.png)

Clique no campo **Inativo** e selecione **Ativar**.

![RTCDP](./images/atform11.png)

Em seguida, você receberá uma confirmação visual de que sua atividade está online.

![RTCDP](./images/atform12.png)

Sua atividade agora está ao vivo e pode ser testada no site de demonstração.

>[!IMPORTANT]
>
>Quando você acaba de criar seu destino do Adobe Target no Real-Time CDP, pode levar até uma hora para o destino ficar ativo. Esse é um tempo de espera único, devido à definição da configuração de back-end. Quando a configuração inicial de 1 hora de tempo de espera e backend for concluída, os segmentos de borda recém-adicionados enviados para o destino do Adobe Target estarão disponíveis para direcionamento em tempo real.

Se agora você voltar ao seu site de demonstração e visitar a página do produto PROTEUS FITNESS JACKSHIRT, você se qualificará instantaneamente para o segmento que criou e verá a atividade do Adobe Target ser exibida na página inicial em tempo real.

![RTCDP](./images/atform13.png)

Próxima Etapa: [2.3.6 Públicos-Alvo Externos](./ex6.md)

[Voltar ao módulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Voltar a todos os módulos](../../../overview.md)
