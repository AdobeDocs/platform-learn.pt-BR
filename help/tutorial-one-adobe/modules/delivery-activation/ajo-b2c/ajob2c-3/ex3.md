---
title: Offer Decisioning - Teste sua decisão
description: Offer Decisioning - Teste sua decisão
kt: 5342
doc-type: tutorial
exl-id: c40b9b8c-9717-403c-bf02-6b8f42a59c05
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 1%

---

# 3.3.3 Prepare sua propriedade do Cliente de coleta de dados da Adobe Experience Platform e a configuração do Web SDK para o Offer Decisioning

## 3.3.3.1 Atualizar a sequência de dados

Em [Introdução](./../../../../modules/getting-started/gettingstarted/ex2.md), você criou seu próprio **Datastream**. Você usou o nome `--aepUserLdap-- - Demo System Datastream`.

Neste exercício, você precisa configurar o **Datastream** para funcionar com o **Offer Decisioning**.

Para fazer isso, vá para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Você verá isso. Clique em **Datastream**.

No canto superior direito da tela, selecione o nome da sandbox, que deve ser `--aepSandboxName--`.

![Clique no ícone Configuração do Edge na navegação à esquerda](./images/edgeconfig1b.png)

Procure pela sua **Sequência de dados**, chamada `--aepUserLdap-- - Demo System Datastream`. Clique na **Sequência de dados** para abri-la.

![SDKdaWeb](./images/websdk1.png)

Você verá isso. Clique em **...** ao lado de **Adobe Experience Platform** e em **Editar**.

![SDKdaWeb](./images/websdk3.png)

Para habilitar **Offer Decisioning**, marque a caixa para **Offer Decisioning**. Clique em **Salvar**.

![SDKdaWeb](./images/websdk5.png)

Sua **Sequência de dados** agora está pronta para funcionar com o **Offer Decisioning**.

![SDKdaWeb](./images/websdk4.png)

## 3.3.3.2 Configure a propriedade do Cliente de coleta de dados do Adobe Experience Platform para solicitar Ofertas personalizadas

Ir para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/), para **Marcas**. Procure suas propriedades de Coleção de dados, chamadas de `--aepUserLdap-- - Demo System (DD/MM/YYYY)`. Abra a propriedade do cliente Coleção de dados para Web.

![SDKdaWeb](./images/launch1.png)

Na propriedade, vá para **Regras** e abra a regra **Exibição de Página**.

![SDKdaWeb](./images/launch2.png)

Clique para abrir o **Enviar Evento de Experiência de &quot;Exibição de Página&quot;** da Ação.

![SDKdaWeb](./images/launch3.png)

Você verá isso. Em **Personalization**, você observará a opção para **Escopos**.

![SDKdaWeb](./images/launch4.png)

Para cada solicitação enviada para a borda e para o Adobe Experience Platform, é possível fornecer um ou mais **Escopos de Decisão**. Um **Escopo de Decisão** é uma combinação de dois elementos:

- ID da decisão
- ID de posicionamento

Primeiro, vamos dar uma olhada onde você pode encontrar esses dois elementos.

### 3.3.3.2.1 Recuperar a ID de posicionamento

A ID de posicionamento identifica a localização e o tipo do ativo necessário. Por exemplo, a imagem herói na página inicial do site do CitiSignal corresponde à ID de posicionamento para Web - Imagem.

>[!NOTE]
>
>Como parte do exercício 2.3.5, você já configurou uma atividade de Direcionamento de experiência do Adobe Target que alterará a imagem da localização principal na página inicial, como você pode ver na captura de tela. Para este exercício, agora você fará com que suas ofertas apareçam na imagem abaixo da imagem principal, conforme indicado na captura de tela.

![SDKdaWeb](./images/launch5.png)

Para localizar a ID de Posicionamento para a Web - Imagem, vá para Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`. Você estará na exibição **Página inicial** da sua sandbox `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

Em seguida, vá para Componentes e, em seguida, para Disposições. Clique no posicionamento **Web - Imagem** para ver seus detalhes.

![SDKdaWeb](./images/launch6.png)

Como você pode ver na imagem acima, neste exemplo, a ID de posicionamento é `dps:offer-placement:1a08a14ccfe533b6`. Anote a ID de posicionamento para seu posicionamento na Web - Imagem necessária no próximo exercício.

### 3.3.3.2.2 Recuperar a ID da Offer Decision

A **ID da Offer Decision** identifica qual combinação de ofertas personalizadas e oferta substituta você gostaria de usar. No exercício anterior, você criou sua própria Decisão e a nomeou como `--aepUserLdap-- - CitiSignal Decision`.

Para encontrar a ID de Offer Decision para o seu `--aepUserLdap-- - CitiSignal Decision`, vá para Ofertas e, em seguida, vá para Decisões. Clique para selecionar sua Decisão, chamada `--aepUserLdap-- - CitiSignal Decision`.

![SDKdaWeb](./images/launch7.png)

Como você pode ver na imagem acima, neste exemplo, a ID da decisão é `dps:offer-activity:1a08ba4b529b2fb2`. Anote a ID de decisão da oferta para sua decisão `--aepUserLdap-- - CitiSignal Decision`, pois você precisará dela no próximo exercício.

Agora que você recuperou os dois elementos necessários para criar um **Escopos de Decisão**, você pode continuar com a próxima etapa, que envolve a codificação do escopo de decisão.

### 3.3.3.2.3 Codificação BASE64

O **Escopo de Decisão** que você precisa inserir é uma cadeia de caracteres codificada em BASE64. Essa string codificada em BASE64 é uma combinação da ID de posicionamento e da ID de decisão, como você pode ver abaixo:

```json
{
  "xdm:activityId": "dps:offer-activity:1a08ba4b529b2fb2",
  "xdm:placementId": "dps:offer-placement:1a08a14ccfe533b6"
}
```

Você pode recuperar a string codificada em BASE64 do Adobe Experience Platform. Vá para Decisões e clique para abrir sua Decisão, chamada `--aepUserLdap-- - CitiSignal Decision`.

![SDKdaWeb](./images/launch9.png)

Depois de abrir `--aepUserLdap-- - CitiSignal Decision`, você verá isso. Localize a Web de posicionamento - Imagem e clique no botão **Copiar**. Em seguida, clique em **Escopo de decisão codificado**. O **Escopo da Decisão** foi copiado para a área de transferência.

![SDKdaWeb](./images/launch10.png)

Em seguida, volte para o Launch, para sua ação **AEP Web SDK - Enviar evento**.

![SDKdaWeb](./images/launch4.png)

Cole o escopo de decisão codificado no campo de entrada. Salve as alterações na ação **AEP Web SDK - Enviar evento** clicando em **[!UICONTROL Manter alterações]**.

![SDKdaWeb](./images/launch11.png)

Em seguida, clique em **[!UICONTROL Salvar]**.

![SDKdaWeb](./images/launch12.png)

Na Coleta de Dados do Adobe Experience Platform, vá para **[!UICONTROL Fluxo de Publicação]** e abra sua **[!UICONTROL Biblioteca de Desenvolvimento]** chamada **[!UICONTROL Principal]**. Clique em **[!UICONTROL + Adicionar todos os recursos alterados]** e em **[!UICONTROL Salvar e criar para desenvolvimento]**. As alterações serão publicadas no site de demonstração.

![SDKdaWeb](./images/launch13.png)

Toda vez que você carregar uma **Página geral** agora, como por exemplo, a página inicial do site de demonstração, a Offer Decisioning avaliará qual é a oferta aplicável e retornará uma resposta ao site com os detalhes da oferta a ser mostrada. Mostrar a oferta no site requer configuração adicional, o que você fará na próxima etapa.

## 3.3.3.3 Configure sua propriedade do Cliente de coleta de dados do Adobe Experience Platform para receber e aplicar Ofertas personalizadas

Ir para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/), para **[!UICONTROL Propriedades]**. Procure suas propriedades de Coleção de dados, chamadas de `--aepUserLdap-- - Demo System (DD/MM/YYYY)`. Abra a propriedade Coleção de dados para Web.

![SDKdaWeb](./images/launch1.png)

Na propriedade, vá para **Regras**. Pesquise e abra a regra **Exibir Oferta (Offer Decisioning)**.

![SDKdaWeb](./images/decrec2.png)

Você verá isso. Abra a ação **Exibir a oferta na página**.

![SDKdaWeb](./images/decrec6a.png)

Clique em **[!UICONTROL Abrir editor]**

![SDKdaWeb](./images/decrec6.png)

Substitua o código colando o código abaixo no editor.

```javascript
if (!Array.isArray(event.decisions)) {
  console.log("No personalization decisions");
  return;
}

console.log("Received response from Offer Decisioning", event.decisions);

event.decisions.forEach(function (payload) {
  payload.items.forEach(function (item) {
    console.log("Offer", item.data.deliveryURL);

    if (!item.data || item.data?.deliveryURL==null) {
      return;
    }
    console.log("item.data.deliveryURL", item.data.deliveryURL)
    //document.querySelector(".TopRibbon").innerHTML = item.data.content;
    document.querySelector("#SpectrumProvider > div.App > div > div.Page.home > main > div:nth-child(2)").innerHTML = "<img style='max-width:100%;' src='"+item.data.deliveryURL+"'/>";
    document.querySelector("#SpectrumProvider > div.App > div > div.Page.home > main > div:nth-child(2) > img").style.backgroundRepeat="no-repeat";
    document.querySelector("#SpectrumProvider > div.App > div > div.Page.home > main > div:nth-child(2) > img").style.backgroundPosition="center center";
    document.querySelector("#SpectrumProvider > div.App > div > div.Page.home > main > div:nth-child(2) > img").style.backgroundSize = "contain";
  });
});
```

As linhas 17 aplicarão a imagem que está sendo retornada pelo Offer Decisioning ao site. Clique em **[!UICONTROL Salvar]**.

![SDKdaWeb](./images/decrec7.png)

Clique em **[!UICONTROL Manter alterações]**.

![SDKdaWeb](./images/keepchanges1dd.png)

Em seguida, clique em **[!UICONTROL Salvar]**.

![SDKdaWeb](./images/decrec8.png)

Na Coleta de Dados do Adobe Experience Platform, vá para **[!UICONTROL Fluxo de Publicação]** e abra sua **[!UICONTROL Biblioteca de Desenvolvimento]** chamada **[!UICONTROL Principal]**. Clique em **[!UICONTROL + Adicionar todos os recursos alterados]** e em **[!UICONTROL Salvar e criar para desenvolvimento]**. As alterações serão publicadas no site de demonstração.

![SDKdaWeb](./images/decrec9.png)

Com essa alteração, essa regra na Coleção de dados da Adobe Experience Platform agora escutará a resposta do Offer Decisioning, que faz parte da resposta do Web SDK, e quando a resposta for recebida, a imagem da oferta será exibida na página inicial.

No site de demonstração, você verá que essa imagem será substituída agora. Em vez das imagens padrão do site CitiSignal, você verá uma oferta como esta. Nesse caso, a oferta substituta é exibida.

![SDKdaWeb](./images/decrec10.png)

Agora você configurou dois tipos de personalização:

- 1 Atividade de Direcionamento de experiência usando o Adobe Target no exercício 2.3.5
- 1 Implementação do Offer Decisioning usando a propriedade Coleção de dados

No próximo exercício, você verá como combinar suas ofertas e decisões que foram criadas no Adobe Journey Optimizer com uma atividade de Direcionamento de experiência do Adobe Target.

## Próximas etapas

Ir para [3.3.4 Combinar Adobe Target e Offer Decisioning](./ex4.md){target="_blank"}

Voltar para [Offer Decisioning](offer-decisioning.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
