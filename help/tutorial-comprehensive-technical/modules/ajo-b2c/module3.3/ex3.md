---
title: Offer Decisioning - Teste sua decisão
description: Offer Decisioning - Teste sua decisão
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '1263'
ht-degree: 0%

---

# 3.3.3 Preparar a propriedade do Cliente de coleta de dados da Adobe Experience Platform e a configuração do SDK da Web para o Offer Decisioning

## 3.3.3.1 Atualizar a sequência de dados

No [Exercício 0.2](./../../../modules/gettingstarted/gettingstarted/ex2.md), você criou seu próprio **[!UICONTROL Datastream]**. Você usou o nome `--aepUserLdap-- - Demo System Datastream`.

Neste exercício, você precisa configurar esse **[!UICONTROL Datastream]** para funcionar com **[!DNL Offer Decisioning]**.

Para fazer isso, vá para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Você verá isso. Clique em **[!UICONTROL Datastreams]** ou **[!UICONTROL Datastreams (Beta)]**.

No canto superior direito da tela, selecione o nome da sandbox, que deve ser `--aepSandboxName--`.

![Clique no ícone Configuração do Edge na navegação à esquerda](./images/edgeconfig1b.png)

Procure pela sua **[!UICONTROL Sequência de dados]**, chamada `--aepUserLdap-- - Demo System Datastream`. Clique na **[!UICONTROL Sequência de dados]** para abri-la.

![SDKdaWeb](./images/websdk1.png)

Você verá isso. Clique em **...** ao lado de **Adobe Experience Platform** e em **Editar**.

![SDKdaWeb](./images/websdk3.png)

Para habilitar **[!DNL Offer Decisioning]**, marque a caixa para **[!DNL Offer Decisioning]**. Clique em **Salvar**.

![SDKdaWeb](./images/websdk5.png)

Seu **[!UICONTROL Datastream]** agora está pronto para funcionar com o **[!DNL Offer Decisioning]**.

![SDKdaWeb](./images/websdk4.png)

## 3.3.3.2 Configure a propriedade do Cliente de coleta de dados do Adobe Experience Platform para solicitar Ofertas personalizadas

Vá para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/), para **[!UICONTROL Client]**. Procure suas propriedades de Coleção de dados, chamadas de `--aepUserLdap-- - Demo System (DD/MM/YYYY)`. Abra a propriedade do cliente Coleção de dados para Web.

![SDKdaWeb](./images/launch1.png)

Na propriedade, vá para **[!UICONTROL Regras]** e abra a regra **[!UICONTROL Exibição de Página]**.

![SDKdaWeb](./images/launch2.png)

Clique para abrir o [!UICONTROL Action] **[!UICONTROL AEP Web SDK - Enviar evento]**.

![SDKdaWeb](./images/launch3.png)

Você verá isso. Você observará a opção de menu para **[!UICONTROL Escopos de Decisão]**.

![SDKdaWeb](./images/launch4.png)

Para cada solicitação enviada para a borda e para o Adobe Experience Platform, é possível fornecer um ou mais **[!UICONTROL Escopos de Decisão]**. Um **[!UICONTROL Escopo de Decisão]** é uma combinação de dois elementos:

- [!UICONTROL ID da decisão]
- [!UICONTROL ID de posicionamento]

Primeiro, vamos dar uma olhada onde você pode encontrar esses dois elementos.

### 3.3.3.2.1 Recupere sua [!UICONTROL ID de posicionamento]

A [!UICONTROL ID de Posicionamento] identifica a localização e o tipo do ativo necessário. Por exemplo, a imagem herói na página inicial do site Luma corresponde à [!UICONTROL ID de Posicionamento] para [!UICONTROL Web - Imagem].

>[!NOTE]
>
>Como parte do módulo 6, você já configurou uma atividade de Direcionamento de experiência do Adobe Target que alterará a imagem da localização principal na página inicial, como você pode ver na captura de tela. Para fins de exercício, agora você fará com que suas ofertas apareçam na imagem abaixo da imagem principal, conforme indicado na captura de tela.

![SDKdaWeb](./images/launch5.png)

Para localizar a [!UICONTROL ID de Posicionamento] para [!UICONTROL Web - Imagem], vá para a Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`. Para alterar a sandbox, clique em **Produção (VA7)** e selecione a sandbox na lista. Neste exemplo, a sandbox é chamada de **AEP Enablement FY22**. Você estará na exibição **Página inicial** da sua sandbox `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

Em seguida, vá para [!UICONTROL Componentes] e depois para [!UICONTROL Posicionamentos]. Clique no posicionamento [!UICONTROL Web - Imagem] para ver seus detalhes.

![SDKdaWeb](./images/launch6.png)

Como você pode ver na imagem acima, neste exemplo, a [!UICONTROL ID de Posicionamento] é `xcore:offer-placement:14bf09dc4190ebba`. Anote a [!UICONTROL ID de posicionamento] para o seu posicionamento para a [!UICONTROL Web - Imagem], pois será necessário no próximo exercício.

### 3.3.3.2.2 Recupere sua [!UICONTROL ID da Decisão]

A [!UICONTROL ID da Decisão] identifica qual combinação de Ofertas Personalizadas e Oferta Substituta você gostaria de usar. No exercício anterior, você criou sua própria [!UICONTROL Decisão] e a nomeou como `--aepUserLdap-- - Luma Decision`.

Para encontrar a [!UICONTROL ID da Decisão] para o seu `--aepUserLdap-- - Luma Decision`, vá para [https://platform.adobe.com](https://platform.adobe.com).

Em seguida, vá para [!UICONTROL Ofertas] e vá para [!UICONTROL Decisões]. Clique para selecionar sua [!UICONTROL Decisão], chamada `--aepUserLdap-- - Luma Decision`.

![SDKdaWeb](./images/launch7.png)

Como você pode ver na imagem acima, neste exemplo, a [!UICONTROL ID da Decisão] é `xcore:offer-activity:14c052382e1b6505`. Anote a [!UICONTROL ID de decisão] para sua decisão `--aepUserLdap-- - Luma Decision` como você precisará dela no próximo exercício.

Agora que você recuperou os dois elementos necessários para criar um **[!UICONTROL Escopos de Decisão]**, você pode continuar com a próxima etapa, que envolve a codificação do escopo de decisão.

### 3.3.3.2.3 Codificação BASE64

O **[!UICONTROL Escopo de Decisão]** que você precisa inserir é uma cadeia de caracteres codificada em BASE64. Esta cadeia de caracteres codificada em BASE64 é uma combinação da [!UICONTROL ID de Posicionamento] e da [!UICONTROL ID de Decisão], como você pode ver abaixo.

```json
{
  "activityId":"xcore:offer-activity:14c052382e1b6505",
  "placementId":"xcore:offer-placement:14bf09dc4190ebba"
}
```

O **[!UICONTROL Escopo de Decisão]** pode ser gerado de duas maneiras:

- Use um serviço público como [https://www.base64encode.org/](https://www.base64encode.org/). Insira o código JSON como mencionado acima, clique em **[!UICONTROL Codificar]** e você obterá sua cadeia de caracteres codificada em BASE64 abaixo.

  ![SDKdaWeb](./images/launch8.png)

- Recupere a string codificada em BASE64 do Adobe Experience Platform. Vá para [!UICONTROL Decisões] e clique para abrir sua [!UICONTROL Decisão], chamada `--aepUserLdap-- - Luma Decision`.

  ![SDKdaWeb](./images/launch9.png)

  Depois de abrir `--aepUserLdap-- - Luma Decision`, você verá isso. Localize o posicionamento [!UICONTROL Web - Imagem] e clique no botão **[!UICONTROL Copiar]**. Em seguida, clique em **[!UICONTROL Escopo de decisão codificado]**. O **[!UICONTROL Escopo da Decisão]** foi copiado para a área de transferência.

  ![SDKdaWeb](./images/launch10.png)

Em seguida, volte para o Launch, para sua ação **[!UICONTROL AEP Web SDK - Enviar evento]**.

![SDKdaWeb](./images/launch4.png)

Cole o escopo de decisão codificado no campo de entrada.

![SDKdaWeb](./images/launch11.png)

Salve as alterações na ação **[!UICONTROL AEP Web SDK - Enviar evento]** clicando em **[!UICONTROL Manter alterações]**.

![SDKdaWeb](./images/keepchanges.png)

Em seguida, clique em **[!UICONTROL Salvar]** ou **[!UICONTROL Salvar na Biblioteca]**

![SDKdaWeb](./images/launch12.png)

Na Coleta de Dados do Adobe Experience Platform, vá para **[!UICONTROL Fluxo de Publicação]** e abra sua **[!UICONTROL Biblioteca de Desenvolvimento]** chamada **[!UICONTROL Principal]**. Clique em **[!UICONTROL + Adicionar todos os recursos alterados]** e em **[!UICONTROL Salvar e criar para desenvolvimento]**. As alterações serão publicadas no site de demonstração.

![SDKdaWeb](./images/launch13.png)

Toda vez que você estiver carregando uma **Página Geral** agora, como por exemplo, a página inicial do site de demonstração, o Offer Decisioning avaliará qual é a oferta aplicável e retornará uma resposta ao site com os detalhes da oferta a ser mostrada. Mostrar a oferta no site requer configuração adicional, o que você fará na próxima etapa.

## 3.3.3.3 Configure sua propriedade do Cliente de coleta de dados do Adobe Experience Platform para receber e aplicar Ofertas personalizadas

Ir para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/), para **[!UICONTROL Propriedades]**. Procure suas propriedades de Coleção de dados, chamadas de `--aepUserLdap-- - Demo System (DD/MM/YYYY)`. Abra a propriedade Coleção de dados para Web.

![SDKdaWeb](./images/launch1.png)

Na propriedade, vá para **[!UICONTROL Regras]**.

![SDKdaWeb](./images/decrec1.png)

Pesquise e abra a regra **Decisão Recebida**.

![SDKdaWeb](./images/decrec2.png)

Você verá isso. Abra a ação **Colocar a oferta na página**.

![SDKdaWeb](./images/decrec6a.png)

Clique em **[!UICONTROL Abrir editor]**

![SDKdaWeb](./images/decrec6.png)

Substitua o código colando o código abaixo no editor.

```javascript
if(!Array.isArray(event.decisions)) {
  console.log('No decisions returned')
  return;
}
console.log("decision",event.decisions)

event.decisions.forEach(function(payload) {
  payload.items.forEach(function(item){
    console.log("Response from Offer Decisioning ", item.data.content);
   
    var element = document.querySelector("#root > div > div > div.app-content > div > section.feature_part.padding_top > div > div.row.align-items-center.justify-content-between > div.col-lg-7.col-sm-6.\\30  > div");
    if(!element){
      console.log("Offer Placement Area Selector not found")
      return;
    }
    if(!item.data){
      return
    }
    //check if offer already exists
    var offer = document.querySelector("#root > div > div > div.app-content > div > section.feature_part.padding_top > div > div.row.align-items-center.justify-content-between > div.col-lg-7.col-sm-6.\\30  > div");
    if(!offer){ 
      element.insertAdjacentHTML('afterbegin', item.data.content) 
    }
    else { 
      console.log("item.data.deliveryURL: " + item.data.deliveryURL)
      document.querySelector("#root > div > div > div.app-content > div > section.feature_part.padding_top > div > div.row.align-items-center.justify-content-between > div.col-lg-7.col-sm-6.\\30  > div").style.background="url('"+item.data.deliveryURL+"')";
      document.querySelector("#root > div > div > div.app-content > div > section.feature_part.padding_top > div > div.row.align-items-center.justify-content-between > div.col-lg-7.col-sm-6.\\30  > div").style.backgroundRepeat="no-repeat";
      document.querySelector("#root > div > div > div.app-content > div > section.feature_part.padding_top > div > div.row.align-items-center.justify-content-between > div.col-lg-7.col-sm-6.\\30  > div").style.backgroundPosition="center center";
      document.querySelector("#root > div > div > div.app-content > div > section.feature_part.padding_top > div > div.row.align-items-center.justify-content-between > div.col-lg-7.col-sm-6.\\30  > div").style.backgroundSize = "contain";
    }  
  })
});
```

As linhas 26-27-28-29 aplicarão a imagem que está sendo retornada pelo Offer Decisioning ao site. Clique em **[!UICONTROL Salvar]**.

![SDKdaWeb](./images/decrec7.png)

Clique em **[!UICONTROL Manter alterações]**.

![SDKdaWeb](./images/keepchanges1dd.png)

Em seguida, clique em **[!UICONTROL Salvar]** ou **[!UICONTROL Salvar na Biblioteca]**

![SDKdaWeb](./images/decrec8.png)

Na Coleta de Dados do Adobe Experience Platform, vá para **[!UICONTROL Fluxo de Publicação]** e abra sua **[!UICONTROL Biblioteca de Desenvolvimento]** chamada **[!UICONTROL Principal]**. Clique em **[!UICONTROL + Adicionar todos os recursos alterados]** e em **[!UICONTROL Salvar e criar para desenvolvimento]**. As alterações serão publicadas no site de demonstração.

![SDKdaWeb](./images/decrec9.png)

Com essa alteração, essa regra na Coleção de dados da Adobe Experience Platform agora escutará a resposta do Offer Decisioning, que faz parte da resposta do SDK da Web, e quando a resposta for recebida, a imagem da oferta será exibida na página inicial.

No site de demonstração, você verá que essa imagem será substituída agora:

>[!NOTE]
>
>Como parte do módulo 6, você já configurou uma atividade de Direcionamento de experiência do Adobe Target que alterará a imagem da localização principal na página inicial, como você pode ver na captura de tela. Para fins de exercício, agora você fará com que suas ofertas apareçam na imagem abaixo da imagem principal, conforme indicado na captura de tela.

![SDKdaWeb](./images/launch5.png)

E em vez das imagens padrão do site Luma, você verá uma oferta como esta. Nesse caso, a oferta substituta é exibida.

![SDKdaWeb](./images/decrec10.png)

Agora você configurou dois tipos de personalização:

- 1 Atividade de Direcionamento de experiência usando o Adobe Target no Módulo 6
- 1 implementação de Offer decisioning usando sua propriedade de Coleção de dados

No próximo exercício, você verá como combinar suas ofertas e decisões que foram criadas no Adobe Journey Optimizer com uma atividade de Direcionamento de experiência do Adobe Target.

Próxima Etapa: [3.3.4 Combinar Adobe Target e Offer Decisioning](./ex4.md)

[Voltar ao módulo 3.3](./offer-decisioning.md)

[Voltar a todos os módulos](./../../../overview.md)
