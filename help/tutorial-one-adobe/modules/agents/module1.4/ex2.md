---
title: Implementar o Brand Concierge no seu site
description: Implementar o Brand Concierge no seu site
kt: 5342
doc-type: tutorial
source-git-commit: fb1fc5c72723cc4e1ede87f90410feb0cc314eea
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 0%

---

# 1.4.2 Implementar o Brand Concierge em seu site

>[!IMPORTANT]
>
>Para concluir este exercício, você precisa ter acesso a um ambiente de trabalho do AEM Assets CS Author e a um site do AEM CS/EDS.
>
>Se você não tiver um ambiente como esse, acesse [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Siga as instruções aqui e você terá acesso a esse ambiente.

>[!IMPORTANT]
>
>Se você tiver configurado anteriormente um Programa AEM CS com um ambiente AEM Assets CS, pode ser que sua sandbox AEM CS tenha hibernado. Considerando que a deshibernação de uma sandbox desse tipo leva de 10 a 15 minutos, seria uma boa ideia iniciar o processo de deshibernação agora para que você não precise aguardar mais tarde.

## 1.4.2.1 Configure seu site para mostrar o Brand Concierge - AEM Author

Para que o Brand Concierge apareça em seu site, é necessário criar um novo bloco personalizado que precise ser adicionado a uma nova página, e garantir que sua nova página seja adicionada à navegação do site.

Agora é necessário configurar as seguintes coisas nesta ordem:

- Crie um novo bloco personalizado que será usado para carregar o Brand Concierge em seu site.
- Crie uma nova página em seu site para o Brand Concierge.
- Vincule o bloco personalizado recém-criado na página do Brand Concierge recém-criada.
- Adicione uma referência para navegar até a página do Brand Concierge recém-criada no arquivo de cabeçalho de navegação do site.

### Criar novo bloco personalizado

Para criar o novo bloco personalizado, navegue até o repositório GitHub que está vinculado ao seu site.

![Bloquear](./images/block1.png)

#### component-definition.json

Role para baixo até ver o arquivo **component-definition.json** e abri-lo

![Bloquear](./images/block8.png)

Clique no ícone **pencl** para começar a editar o arquivo.

![Bloquear](./images/block8a.png)

Role para baixo até ver os **Blocos**. Coloque o cursor abaixo do colchete do componente **Cartões**

![Bloquear](./images/block9.png)

Cole esse código e insira uma vírgula **,** após o bloco de código:

```json
{
  "title": "BrandConcierge",
  "id": "brandconcierge",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "BrandConcierge",
          "model": "brandconcierge"
        }
      }
    }
  }
},
```

Clique em **Confirmar alterações...**.

![Bloquear](./images/block10.png)

Clique em **Confirmar alterações**.

![Bloquear](./images/block10a.png)

#### component-models.json

Role para baixo até ver o arquivo **component-models.json** e clique no ícone **lápis** para começar a editar o arquivo.

![Bloquear](./images/block11.png)

Role para baixo até ver o último item. Coloque o cursor próximo ao colchete do último componente.

![Bloquear](./images/block12.png)

Insira uma vírgula **,**, e, por push, insira e, na próxima linha, cole este código:

```json
{
  "id": "brandconcierge",
  "fields": []
}
```

Clique em **Confirmar alterações...**.

![Bloquear](./images/block13.png)

Clique em **Confirmar alterações**.

![Bloquear](./images/block13a.png)

#### component-filters.json

Role para baixo até ver o arquivo **component-filters.json** e clique no ícone **lápis** para começar a editar o arquivo.

![Bloquear](./images/block14.png)

Você deverá ver isso.

![Bloquear](./images/block14a.png)

Em **seção**, insira uma vírgula `,` e cole a identificação do componente `"brandconcierge"` após a última linha atual.

Clique em **Confirmar alterações...**.

![Bloquear](./images/block15.png)

Clique em **Confirmar alterações**.

![Bloquear](./images/block15a.png)

#### brandconcierge.css

Ao criar um bloco, é prática recomendada criar um arquivo para o estilo do bloco e ele deve ter o mesmo nome do bloco. agora você deve criar o arquivo, que deixaremos vazio por enquanto.

Vá para a pasta **blocos**. Em seguida, clique em **Adicionar arquivo** e selecione **Criar novo arquivo**.

![Bloquear](./images/css1.png)

Na caixa de texto, digite `brandconcierge/brandconcierge.css`. O arquivo pode permanecer vazio por enquanto. Clique em **Confirmar alterações...**.

![Bloquear](./images/css2.png)

Clique em **Confirmar alterações**.

![Bloquear](./images/css3.png)

#### brandconcierge.js

Ao criar um bloco, é prática recomendada criar um arquivo para o javascript relacionado ao bloco e ele deve ter o mesmo nome do bloco.

Clique em **Adicionar arquivo** e selecione **Criar novo arquivo**.

![Bloquear](./images/js1.png)

Na caixa de texto, digite `brandconcierge.js`. O arquivo pode permanecer vazio por enquanto. Clique em **Confirmar alterações...**.

```javascript
export default function decorate(block) {
  block.setAttribute('id', 'brand-concierge-mount');
}
```

![Bloquear](./images/js2.png)

Clique em **Confirmar alterações**.

![Bloquear](./images/js3.png)

### Criar nova página e vincular novo bloco personalizado

Ir para [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Clique no **Programa** para abri-lo.

![AEMCS](./images/aemcs6.png)

Em seguida, clique nos 3 pontos **...** na guia **Ambientes** e clique em **Exibir Detalhes**.

![AEMCS](./images/aemcs9.png)

Você verá os detalhes do ambiente. Clique na URL do seu ambiente **Author**.

>[!NOTE]
>
>É possível que seu ambiente esteja hibernado. Se esse for o caso, será necessário cancelar a hibernação do ambiente primeiro. Você pode encontrar instruções sobre como cancelar a hibernação no vídeo abaixo.

>[!VIDEO](https://video.tv.adobe.com/v/3478141?quality=12&learn=on)

![AEMCS](./images/aemcs10.png)

Em seguida, você deverá ver seu ambiente de autor do AEM. Ir para **Sites**.

![AEMCS](./images/block21.png)

Vá para **CitiSignal**. Clique em **Criar** e selecione **Página**.

![AEMCS](./images/block23.png)

Selecione **Página** e clique em **Avançar**.

![AEMCS](./images/block24.png)

Insira os seguintes valores:

- Título: **Brand Concierge**
- Nome: **brandconcierge**
- Título da página: **Brand Concierge**

Clique em **Criar**.

![AEMCS](./images/block25.png)

Selecione **Abrir**.

![AEMCS](./images/block22.png)

Você deverá ver isso.

![AEMCS](./images/block26.png)

Clique na área em branco para selecionar o componente **seção**. Em seguida, clique no ícone de mais **+** no menu direito.

![AEMCS](./images/block27.png)

Em seguida, você deve ver seu bloco personalizado mostrado na lista de blocos disponíveis. Clique para selecioná-la.

![AEMCS](./images/block28.png)

Você deverá ver um bloco vazio sendo adicionado a essa página. Este bloco será carregado dinamicamente usando as bibliotecas javascript que você adicionará na próxima etapa.

Clique em **Publicar**.

![AEMCS](./images/block29.png)

Clique novamente em **Publicar**.

![AEMCS](./images/block30.png)

Sua nova página foi publicada e agora pode ser adicionada ao cabeçalho de navegação na próxima etapa.

### Atualizar arquivo de cabeçalho de navegação

Na visão geral do AEM Sites, vá para **CitiSignal** e marque a caixa de seleção do arquivo **Header/nav**. Clique em **Edit**.

![AEMCS](./images/nav0.png)

Selecione o campo **Texto** na tela de visualização e clique no campo **Texto**, no lado direito da tela, para editá-lo.

![AEMCS](./images/nav0a.png)

Crie uma nova opção de menu no menu de navegação com o texto `Brand Concierge`. Em seguida, selecione o texto **Brand Concierge** e clique no ícone **link**.

![AEMCS](./images/nav1.png)

Digite isto para o campo **Caminho ou URL** `/content/CitiSignal/brandconcierge.html` e digite `Brand Concierge` para o campo **Título**. Clique em **Salvar**.

![AEMCS](./images/nav3.png)

Você deveria ficar com isso. Clique em **Concluído**.

![AEMCS](./images/nav4.png)

Você deveria ficar com isso. Clique em **Publicar**.

![AEMCS](./images/nav4a.png)

Clique novamente em **Publicar**.

![AEMCS](./images/nav5.png)

A nova página agora é adicionada ao menu.

## 1.4.2.2 Configure seu site para exibir o Brand Concierge - GitHub

Depois de atualizar o conteúdo usando o ambiente do AEM Author, agora é necessário atualizar parte do código no repositório do GitHub usado para o seu site.

### Bibliotecas Javascript

As seguintes bibliotecas são necessárias para implementar o Brand Concierge em seu site em execução no AEM CS/EDS:

- [styleconfigurations.js](./assets/styleconfigurations.js)
- [alloy.js](./assets/alloy.js)
- [brandconciergemain.js](./assets/brandconciergemain.js)

Baixe todos os 3 arquivos no desktop.

![Brand Concierge](./images/aem0.png)

Vá para o projeto GitHub do site do AEM CS/EDS. Ir para **scripts**.

![Brand Concierge](./images/aem1.png)

Clique em **Adicionar arquivo** e selecione **Carregar arquivos**.

![Brand Concierge](./images/aem3.png)

Clique em **Escolher seus arquivos**.

![Brand Concierge](./images/aem3a.png)

Selecione todos os 3 arquivos **styleConfigurations.js, alloy.js e brandconciergemain.js** da sua área de trabalho e clique em **Abrir**.

![Brand Concierge](./images/aem4.png)

Clique em **Confirmar alterações**.

![Brand Concierge](./images/aem5.png)

### Atualizar head.html

Na etapa anterior, você carregou 3 novas bibliotecas. Essas bibliotecas agora precisam ser carregadas quando seu site for carregado e a maneira de fazer isso é adicionar referências a esses arquivos no arquivo **head.html**.

Além disso, você também precisa fornecer instruções no arquivo **head.html** para garantir que as bibliotecas sejam carregadas na ordem correta e de maneira correta.

Para fazer isso, vá para o projeto GitHub do seu site do AEM CS/EDS clicando em **Código**.

![Brand Concierge](./images/aem6.png)

Role para baixo um pouco. Abra o arquivo **head.html**.

![Brand Concierge](./images/aem7.png)

Clique no ícone de **lápis** para editar este arquivo.

![Brand Concierge](./images/aem8.png)

Você deverá ver isso.

![Brand Concierge](./images/aem9.png)

Role para baixo até a linha 43 e cole o seguinte:

Há dois campos no código abaixo que você precisa atualizar:

>[!IMPORTANT]
>
>- **datastreamId** está definido no momento como &quot;XXXXX&quot; e precisa ser substituído pela ID da sequência de dados criada na etapa anterior.
>- **orgId** precisa ser substituída pela ID de Organização IMS da sua instância do Adobe Experience Cloud.

```javascript
<script src="/scripts/styleconfigurations.js"></script>

<script>
		!function (n, o) {
      o.forEach(function (o) {
        n[o] || ((n.__alloyNS = n.__alloyNS ||
          []).push(o), n[o] = function () {
            var u = arguments; return new Promise(
              function (i, l) { n[o].q.push([i, l, u]) })
          }, n[o].q = [])
      })
    }
      (window, ["alloy"]);
	</script>


<script src="/scripts/alloy.js"></script>

<script>
	alloy("configure", {
		defaultConsent: "in",
        edgeDomain: "edge.adobedc.net",
        edgeBasePath: "ee",
        datastreamId: "XXXXX", // replace datastreamId
        orgId: "--aepImsOrgId--", // replace ims org Id
        debugEnabled: true,
        idMigrationEnabled: false,
        thirdPartyCookiesEnabled: false,
        prehidingStyle: ".personalization-container { opacity: 0 !important }",
    });

window["alloy"]("sendEvent", {
    conversation: {
        fetchConversationalExperience: true
    }
}).then(result => {
    console.log("Conversation experience fetched", result);
    window["alloy"]("bootstrapConversationalExperience", {
        selector: "#brand-concierge-mount",
        src: "/scripts/brandconciergemain.js",
        stylingConfigurations: window.styleConfiguration,
        stickySession: true // create a sticky session cookie with expiration
    })
});
</script>
```

Clique em **Confirmar alteração...**.

![Brand Concierge](./images/aem10.png)

Clique em **Confirmar alteração**.

![Brand Concierge](./images/aem11.png)

Agora você atualizou o código necessário para carregar as bibliotecas do em seu site.

![Brand Concierge](./images/aem12.png)

## 1.4.2.3 Testar sua configuração

Você poderá testar suas alterações no site indo até `main--citisignal-aem-accs--XXX.aem.page` ou `main--citisignal-aem-accs--XXX.aem.live`, depois de substituir XXX pela sua conta de usuário do GitHub, que neste exemplo é `woutervangeluwe`.

Neste exemplo, o URL completo torna-se isto:
`https://main--citisignal-aem-accs--woutervangeluwe.aem.page` e/ou `https://main--citisignal-aem-accs--woutervangeluwe.aem.live`.

Pode levar algum tempo até que todos os ativos sejam exibidos corretamente, pois precisam ser publicados primeiro.

Você deverá ver isso. Clique em **Brand Concierge**.

![Brand Concierge](./images/aem13.png)

Você deverá ver essa Brand Concierge onde é possível inserir seu prompt.

![Brand Concierge](./images/aem14.png)

Voltar para [Brand Concierge](./brandconcierge.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}