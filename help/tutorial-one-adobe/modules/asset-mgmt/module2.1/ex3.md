---
title: AEM CS - Bloco personalizado básico
description: AEM CS - Bloco personalizado básico
kt: 5342
doc-type: tutorial
exl-id: 57c08a88-d885-471b-ad78-1dba5992da9d
source-git-commit: 7537cd4d4ca6bc25afcb8f61a736498b0c297850
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 1%

---

# 1.1.3 Desenvolver um bloco personalizado básico

## 1.1.3.1 Configurar o ambiente de desenvolvimento local

Vá para [https://desktop.github.com/download/](https://desktop.github.com/download/){target="_blank"}, baixe e instale o **Github Desktop**.

![Bloquear](./images/block1.png){zoomable="yes"}

Depois que o Github Desktop for instalado, acesse o repositório GitHub criado no exercício anterior. Clique em **&lt;> Código** e em **Abrir com o GitHub Desktop**.

![Bloquear](./images/block2.png){zoomable="yes"}

Seu repositório GitHub será aberto no GitHub Desktop. Você pode alterar o **Caminho Local**. Clique em **Clonar**.

![Bloquear](./images/block3.png){zoomable="yes"}

Uma pasta local será criada.

![Bloquear](./images/block4.png){zoomable="yes"}

Abra o Visual Studio Code. Ir para **Arquivo** > **Abrir pasta**.

![Bloquear](./images/block5.png){zoomable="yes"}

Selecione a pasta usada pela configuração do GitHub para **citisignal**.

![Bloquear](./images/block6.png){zoomable="yes"}

Você verá agora que a pasta está aberta no Visual Studio Code e está pronto para criar um novo bloco.

![Bloquear](./images/block7.png){zoomable="yes"}

## 1.1.3.2 Criar um bloco personalizado básico

A Adobe recomenda desenvolver blocos em uma abordagem de três fases:

- Crie a definição e o modelo do bloco, revise-o e leve-o para produção.
- Crie conteúdo com o novo bloco.
- Implemente a decoração e os estilos do novo bloco.

### component-definition.json

No Visual Studio Code, abra o arquivo **component-definition.json**.

![Bloquear](./images/block8.png){zoomable="yes"}

Role para baixo até ver o componente **Quote**. Coloque o cursor próximo ao colchete do último componente.

![Bloquear](./images/block9.png){zoomable="yes"}

Cole esse código e insira uma vírgula **,** após o bloco de código:

```json
{
  "title": "FiberOffer",
  "id": "fiberoffer",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "FiberOffer",
          "model": "fiberoffer",
          "offerText": "<p>Fiber will soon be available in your region!</p>",
          "offerCallToAction": "Get your offer now!",
          "offerImage": ""
        }
      }
    }
  }
}
```

Salve as alterações.

![Bloquear](./images/block10.png){zoomable="yes"}

### component-models.json

No Visual Studio Code, abra o arquivo **component-models.json**.

![Bloquear](./images/block11.png){zoomable="yes"}

Role para baixo até ver o último item. Coloque o cursor próximo ao colchete do último componente.

![Bloquear](./images/block12.png){zoomable="yes"}

Insira uma vírgula **,**, e, por push, insira e, na próxima linha, cole este código:

```json
{
  "id": "fiberoffer",
  "fields": [
     {
       "component": "richtext",
       "name": "offerText",
       "value": "",
       "label": "Offer Text",
       "valueType": "string"
     },
     {
       "component": "richtext",
       "valueType": "string",
       "name": "offerCallToAction",
       "label": "Offer CTA",
       "value": ""
     },
     {
       "component": "reference",
       "valueType": "string",
       "name": "offerImage",
       "label": "Offer Image",
        "multi": false
     }
   ]
}
```

Salve as alterações.

![Bloquear](./images/block13.png){zoomable="yes"}

### component-filters.json

No Visual Studio Code, abra o arquivo **component-filters.json**.

![Bloquear](./images/block14.png){zoomable="yes"}

Em **seção**, insira uma vírgula **,** e a ID do seu componente **fiberoffer** após a última linha atual.

Salve as alterações.

![Bloquear](./images/block15.png){zoomable="yes"}

## 1.1.3.3 Confirme suas alterações

Agora você fez várias alterações em seu projeto que precisam ser enviadas de volta ao repositório do GitHub. Para fazer isso, abra o **GitHub Desktop**.

Você deverá ver os 3 arquivos que acabou de editar em **Alterações**. Revise suas alterações.

![Bloquear](./images/block16.png){zoomable="yes"}

Digite um nome para a sua PR, `Fiber Offer custom block`. Clique em **Confirmar para principal**.

![Bloquear](./images/block17.png){zoomable="yes"}

Você deverá ver isso. Clique em **Origem de push**.

![Bloquear](./images/block18.png){zoomable="yes"}

Após alguns segundos, suas alterações foram enviadas para o repositório do GitHub.

![Bloquear](./images/block19.png){zoomable="yes"}

No navegador, vá para a conta GitHub e para o repositório criado para o CitiSignal. Você deverá ver algo assim, mostrando que suas alterações foram recebidas.

![Bloquear](./images/block20.png){zoomable="yes"}

## 1.1.3.4 Adicionar seu bloco a uma página

Agora que seu bloco básico de cotações está definido e comprometido com o projeto CitiSignal, você pode adicionar um bloco **fiberoffer** a uma página existente.

Ir para [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Clique no **Programa** para abri-lo.

![AEMCS](./images/aemcs6.png){zoomable="yes"}

Em seguida, clique nos 3 pontos **...** na guia **Ambientes** e clique em **Exibir Detalhes**.

![AEMCS](./images/aemcs9.png){zoomable="yes"}

Você verá os detalhes do ambiente. Clique na URL do seu ambiente **Author**.

>[!NOTE]
>
>É possível que seu ambiente esteja hibernado. Se esse for o caso, será necessário cancelar a hibernação do ambiente primeiro.

![AEMCS](./images/aemcs10.png){zoomable="yes"}

Em seguida, você deverá ver seu ambiente de autor do AEM. Ir para **Sites**.

![AEMCS](./images/block21.png){zoomable="yes"}

Vá para **CitiSignal** > **us** > **en**.

![AEMCS](./images/block22.png){zoomable="yes"}

Clique em **Criar** e selecione **Página**.

![AEMCS](./images/block23.png){zoomable="yes"}

Selecione **Página** e clique em **Avançar**.

![AEMCS](./images/block24.png){zoomable="yes"}

Insira os seguintes valores:

- Título: **Fibra de CitiSignal**
- Nome: **citisignal-fiber**
- Título da página: **Fibra de CitiSignal**

Clique em **Criar**.

![AEMCS](./images/block25.png){zoomable="yes"}

Você deverá ver isso.

![AEMCS](./images/block26.png){zoomable="yes"}

Clique na área em branco para selecionar o componente **seção**. Em seguida, clique no ícone de mais **+** no menu direito.

![AEMCS](./images/block27.png){zoomable="yes"}

Em seguida, você deve ver seu bloco personalizado mostrado na lista de blocos disponíveis. Clique para selecioná-la.

![AEMCS](./images/block28.png){zoomable="yes"}

Você verá campos como **Texto da oferta**, **CTA da oferta** e **Imagem da oferta** sendo adicionados ao editor. Clique em **+ Adicionar** no campo **Imagem da oferta** para selecionar uma imagem.

![AEMCS](./images/block29.png){zoomable="yes"}

Você deverá ver isso. Clique para abrir a pasta **citisignal**.

![AEMCS](./images/blockpub1.png){zoomable="yes"}

Selecione a imagem **product-enrichment-1.png**. Clique em **Selecionar**.

![AEMCS](./images/blockpub2.png){zoomable="yes"}

Você deveria ficar com isso. Clique em **Publicar**.

![AEMCS](./images/blockpub3.png){zoomable="yes"}

Clique novamente em **Publicar**.

![AEMCS](./images/blockpub4.png){zoomable="yes"}

Sua nova página foi publicada.

## 1.1.3.5 Adicionar sua nova página ao menu de navegação

Na visão geral do AEM Sites, vá para **CitiSignal** > **Fragmentos** e marque a caixa de seleção para **Cabeçalho**. Clique em **Edit**.

![AEMCS](./images/nav0.png){zoomable="yes"}

Adicione uma opção de menu ao menu de navegação com o texto `Fiber`. Selecione o texto **Fibra** e clique no ícone **link**.

![AEMCS](./images/nav1.png){zoomable="yes"}

Digite isto para o **URL** `/us/en/citisignal-fiber` e clique no ícone **V** para confirmar.

![AEMCS](./images/nav3.png){zoomable="yes"}

Você deveria ficar com isso. Clique em **Publicar**.

![AEMCS](./images/nav4.png){zoomable="yes"}

Clique novamente em **Publicar**.

![AEMCS](./images/nav5.png){zoomable="yes"}

Agora é possível exibir as alterações em seu site indo para `main--citisignal--XXX.aem.page/us/en/` e/ou `main--citisignal--XXX.aem.live/us/en/`, depois de substituir XXX pela sua conta de usuário do GitHub, que neste exemplo é `woutervangeluwe`.

Neste exemplo, o URL completo torna-se isto:
`https://main--citisignal--woutervangeluwe.aem.page/us/en/` e/ou `https://main--citisignal--woutervangeluwe.aem.live/us/en/`.

Você deverá ver isso. Clique em **Fibra**.

![AEMCS](./images/nav6.png){zoomable="yes"}

Aqui está seu bloco personalizado básico, mas agora renderizado no site.

![AEMCS](./images/nav7.png){zoomable="yes"}

Próxima Etapa: [Bloco Personalizado Avançado](./ex5.md){target="_blank"}

Voltar para o [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./aemcs.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
