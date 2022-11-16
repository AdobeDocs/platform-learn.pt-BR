---
title: Offer Decisioning - Teste sua decisão
description: Offer Decisioning - Teste sua decisão
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: c14c50fc-e76d-4dcf-9cf5-ac38ae74b48d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1291'
ht-degree: 1%

---

# 9.3 Preparar a propriedade do cliente de coleta de dados da Adobe Experience Platform e a configuração do SDK da Web para o Offer Decisioning

>[!NOTE]
>
>O uso do Offer Decisioning no Adobe Experience Platform Web SDK está disponível no momento com acesso antecipado a usuários selecionados. Essa funcionalidade não está disponível para todas as organizações IMS.

## 9.3.1 Atualizar o conjunto de dados

Em [Exercício 0.2](./../../modules/module0/ex2.md), você criou seu próprio **[!UICONTROL Datastream]**. Em seguida, você usou o nome `--demoProfileLdap-- - Demo System Datastream`.

Neste exercício, você precisa configurar **[!UICONTROL Datastream]** para trabalhar com **[!DNL Offer Decisioning]**.

Para fazer isso, acesse [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Você verá isso. Clique em **[!UICONTROL Datastreams]** ou **[!UICONTROL Datastreams (Beta)]**.

No canto superior direito da tela, selecione o nome da sandbox, que deve ser `--aepSandboxId--`.

![Clique no ícone Configuração de borda no painel de navegação esquerdo](./images/edgeconfig1b.png)

Procure por seu **[!UICONTROL Datastream]**, que é nomeado como `--demoProfileLdap-- - Demo System Datastream`. Clique no seu **[!UICONTROL Datastream]** para abri-lo.

![WebSDK](./images/websdk1.png)

Você verá isso. Clique em **...** ao lado de **Adobe Experience Platform** e, em seguida, clique em **Editar**.

![WebSDK](./images/websdk3.png)

Para ativar **[!DNL Offer Decisioning]**, marque a caixa para **[!DNL Offer Decisioning]**. Clique em **Salvar**.

![WebSDK](./images/websdk5.png)

Seu **[!UICONTROL Datastream]** O agora está pronto para trabalhar com o **[!DNL Offer Decisioning]**.

![WebSDK](./images/websdk4.png)

## 9.3.2 Configure sua propriedade do cliente de coleta de dados do Adobe Experience Platform para solicitar ofertas personalizadas

Ir para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)para **[!UICONTROL Cliente]**. Procure por suas propriedades de Coleta de dados, que são nomeadas `--demoProfileLdap-- - Demo System (DD/MM/YYYY)`. Abra a propriedade do cliente Coleta de dados para Web.

![WebSDK](./images/launch1.png)

Na propriedade do , acesse **[!UICONTROL Regras]** e abrir a regra **[!UICONTROL Exibição da página]**.

![WebSDK](./images/launch2.png)

Clique para abrir o [!UICONTROL Ação] **[!UICONTROL AEP Web SDK - Enviar evento]**.

![WebSDK](./images/launch3.png)

Você verá isso. Você notará a opção de menu para **[!UICONTROL Escopos de decisão]**.

![WebSDK](./images/launch4.png)

Para cada solicitação enviada para a borda e para o Adobe Experience Platform, é possível fornecer um ou mais **[!UICONTROL Escopos de decisão]**. A **[!UICONTROL Âmbito de decisão]** é uma combinação de dois elementos:

- [!UICONTROL ID de decisão]
- [!UICONTROL ID de posicionamento]

Vamos primeiro ver onde você pode encontrar esses dois elementos.

### 9.3.2.1 Recuperar seu [!UICONTROL ID de posicionamento]

O [!UICONTROL ID de posicionamento] identifica o local e o tipo de ativo que é necessário. Por exemplo, a imagem principal na página inicial do site Luma corresponde ao cenário [!UICONTROL ID de posicionamento] para [!UICONTROL Web - Imagem].

>[!NOTE]
>
>Como parte do módulo 6, você já configurou uma atividade de Direcionamento de experiência do Adobe Target que alterará a imagem do local do herói na página inicial, como você pode ver na captura de tela. Por causa do exercício, agora você fará suas ofertas aparecerem na imagem abaixo da imagem herói, conforme indicado na captura de tela.

![WebSDK](./images/launch5.png)

Para encontrar o [!UICONTROL ID de posicionamento] para [!UICONTROL Web - Imagem] acesse o Adobe Journey Optimizer acessando [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Você será redirecionado para o **Início**  no Journey Optimizer. Primeiro, certifique-se de usar a sandbox correta. A sandbox a ser usada é chamada de `--aepSandboxId--`. Para alterar de uma sandbox para outra, clique em **Produto de produção (VA7)** e selecione a sandbox na lista. Neste exemplo, a sandbox é chamada de **Ativação AEP FY22**. Você estará no **Início** exibição da sandbox `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

Em seguida, acesse [!UICONTROL Componentes] e depois [!UICONTROL Posicionamentos]. Clique no botão [!UICONTROL Web - Imagem] para ver seus detalhes.

![WebSDK](./images/launch6.png)

Como você pode ver na imagem acima, neste exemplo, a variável [!UICONTROL ID de posicionamento] é `xcore:offer-placement:14bf09dc4190ebba`. Anote o [!UICONTROL ID de posicionamento] para sua disposição para [!UICONTROL Web - Imagem] como você precisará no próximo exercício.

### 9.3.2.2 Recuperar seu [!UICONTROL ID de decisão]

O [!UICONTROL ID de decisão] O identifica qual combinação de ofertas personalizadas e ofertas de fallback você gostaria de usar. No exercício anterior, você criou o seu próprio [!UICONTROL Decisão] e nomeá-lo `--demoProfileLdap-- - Luma Decision`.

Para encontrar o [!UICONTROL ID de decisão] para seu `--demoProfileLdap-- - Luma Decision`, vá para [https://platform.adobe.com](https://platform.adobe.com).

Em seguida, acesse [!UICONTROL Ofertas] e então vá para [!UICONTROL Decisões]. Clique para selecionar a [!UICONTROL Decisão], que é nomeado como `--demoProfileLdap-- - Luma Decision`.

![WebSDK](./images/launch7.png)

Como você pode ver na imagem acima, neste exemplo, a variável [!UICONTROL ID de decisão] é `xcore:offer-activity:14c052382e1b6505`. Anote o [!UICONTROL ID de decisão] para sua decisão `--demoProfileLdap-- - Luma Decision` como você precisará no próximo exercício.

Agora que você recuperou os dois elementos, é necessário criar um **[!UICONTROL Escopos de decisão]**, você pode continuar com a próxima etapa, que envolve a codificação do escopo de decisão.

### 9.3.2.3 Codificação BASE64

O **[!UICONTROL Âmbito de decisão]** é necessário inserir uma string codificada em BASE64. Essa string codificada em BASE64 é uma combinação do [!UICONTROL ID de posicionamento] e [!UICONTROL ID de decisão], como você pode ver abaixo.

```json
{
  "activityId":"xcore:offer-activity:14c052382e1b6505",
  "placementId":"xcore:offer-placement:14bf09dc4190ebba"
}
```

O **[!UICONTROL Âmbito de decisão]** podem ser geradas de duas formas:

- Usar um serviço público como [https://www.base64encode.org/](https://www.base64encode.org/). Insira o código JSON como mencionado acima, clique em **[!UICONTROL Codificar]** e você terá sua sequência codificada BASE64 abaixo.

   ![WebSDK](./images/launch8.png)

- Recupere a string codificada do BASE64 do Adobe Experience Platform. Ir para [!UICONTROL Decisões] e clique em para abrir o [!UICONTROL Decisão], que é nomeado como `--demoProfileLdap-- - Luma Decision`.

   ![WebSDK](./images/launch9.png)

   Após abertura `--demoProfileLdap-- - Luma Decision`Você verá isso. Localize a disposição [!UICONTROL Web - Imagem] e clique no botão **[!UICONTROL Copiar]** botão. Em seguida, clique em **[!UICONTROL Escopo de decisão codificado]**. O **[!UICONTROL Âmbito de decisão]** agora é copiada para a área de transferência.

   ![WebSDK](./images/launch10.png)

Em seguida, volte para o Launch, para a sua ação **[!UICONTROL AEP Web SDK - Enviar evento]**.

![WebSDK](./images/launch4.png)

Cole o escopo de decisão codificado no campo de entrada.

![WebSDK](./images/launch11.png)

Salve as alterações na ação **[!UICONTROL AEP Web SDK - Enviar evento]** clicando em **[!UICONTROL Manter alterações]**.

![WebSDK](./images/keepchanges.png)

Em seguida, clique em **[!UICONTROL Salvar]** ou **[!UICONTROL Salvar na biblioteca]**

![WebSDK](./images/launch12.png)

Na Coleta de dados do Adobe Experience Platform, acesse **[!UICONTROL Fluxo de publicação]** e abra o **[!UICONTROL Biblioteca de desenvolvimento]** que é nomeado **[!UICONTROL Principal]**. Clique em **[!UICONTROL + Adicionar todos os recursos alterados]** e, em seguida, clique em **[!UICONTROL Salvar e criar para desenvolvimento]**. Suas alterações serão publicadas no site de demonstração.

![WebSDK](./images/launch13.png)

Cada vez que você carrega um **Página Geral** agora, como por exemplo a página inicial do site de demonstração, o Offer Decisioning avaliará a oferta aplicável e retornará uma resposta ao site com os detalhes da oferta a ser exibida. A exibição da oferta no site requer configuração adicional, o que você fará na próxima etapa.

## 9.3.3 Configure sua propriedade de cliente de coleta de dados do Adobe Experience Platform para receber e aplicar ofertas personalizadas

Ir para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)para **[!UICONTROL Propriedades]**. Procure por suas propriedades de Coleta de dados, que são nomeadas `--demoProfileLdap-- - Demo System (DD/MM/YYYY)`. Abra a propriedade Coleta de dados para Web.

![WebSDK](./images/launch1.png)

Na propriedade do , acesse **[!UICONTROL Regras]**.

![WebSDK](./images/decrec1.png)

Pesquisar e abrir a regra **Decisão recebida**.

![WebSDK](./images/decrec2.png)

Você verá isso. Abra a ação **Coloque a oferta na página**.

![WebSDK](./images/decrec6a.png)

Clique em **[!UICONTROL Abrir editor]**

![WebSDK](./images/decrec6.png)

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

As Linhas 26-27-28-29 aplicarão a imagem que está sendo retornada pelo Offer Decisioning ao site. Clique em **[!UICONTROL Salvar]**.

![WebSDK](./images/decrec7.png)

Clique em **[!UICONTROL Manter alterações]**.

![WebSDK](./images/keepchanges1dd.png)

Em seguida, clique em **[!UICONTROL Salvar]** ou **[!UICONTROL Salvar na biblioteca]**

![WebSDK](./images/decrec8.png)

Na Coleta de dados do Adobe Experience Platform, acesse **[!UICONTROL Fluxo de publicação]** e abra o **[!UICONTROL Biblioteca de desenvolvimento]** que é nomeado **[!UICONTROL Principal]**. Clique em **[!UICONTROL + Adicionar todos os recursos alterados]** e, em seguida, clique em **[!UICONTROL Salvar e criar para desenvolvimento]**. Suas alterações serão publicadas no site de demonstração.

![WebSDK](./images/decrec9.png)

Com essa alteração, essa regra na Coleta de dados do Adobe Experience Platform agora estará ouvindo a resposta do Offer Decisioning, que faz parte da resposta do SDK da Web, e quando a resposta for recebida, a imagem da oferta será exibida na página inicial.

Ao olhar para o site de demonstração, você verá que esta imagem será substituída agora:

>[!NOTE]
>
>Como parte do módulo 6, você já configurou uma atividade de Direcionamento de experiência do Adobe Target que alterará a imagem do local do herói na página inicial, como você pode ver na captura de tela. Por causa do exercício, agora você fará suas ofertas aparecerem na imagem abaixo da imagem herói, conforme indicado na captura de tela.

![WebSDK](./images/launch5.png)

E em vez das imagens padrão do site Luma, você verá uma oferta como esta. Nesse caso, a oferta de fallback é exibida.

![WebSDK](./images/decrec10.png)

Agora você configurou dois tipos de personalização:

- 1 Atividade de Direcionamento de experiência usando Adobe Target no Módulo 6
- 1 Implementação do Offer decisioning usando a propriedade Coleta de dados

No próximo exercício, você verá como poderá combinar suas ofertas e decisões que foram criadas no Adobe Journey Optimizer com uma atividade de Direcionamento de experiência da Adobe Target.

Próxima etapa: [9.4 Combinar Adobe Target e Offer Decisioning](./ex4.md)

[Voltar ao Módulo 9](./offer-decisioning.md)

[Voltar para todos os módulos](./../../overview.md)
