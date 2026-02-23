---
title: Introdução aos agentes do AEM
description: Introdução aos agentes do AEM
kt: 5342
doc-type: tutorial
exl-id: cb1bf6f0-f329-4e38-ba64-36ffdc3b8bd4
source-git-commit: d2b746d50ec559e0b29a7adb27c3521b0e00d386
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 1%

---

# 1.6.1 Introdução aos agentes do AEM

>[!IMPORTANT]
>
>Para concluir este exercício, você precisa ter acesso a um ambiente de trabalho do AEM Sites e do Assets CS com EDS e os vários agentes do AEM precisam estar habilitados para a organização IMS que você está usando.
>
>Se você ainda não tiver esse ambiente, vá para o exercício [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Siga as instruções aqui e você terá acesso a esse ambiente.

>[!IMPORTANT]
>
>Se você configurou anteriormente um programa do AEM CS com um ambiente do AEM Sites e do Assets CS, pode ser que sua sandbox do AEM CS tenha hibernado. Considerando que a deshibernação de uma sandbox desse tipo leva de 10 a 15 minutos, seria uma boa ideia iniciar o processo de deshibernação agora para que você não precise aguardar mais tarde.

## Agente de Descoberta 1.6.1.1

O Adobe Experience Manager (AEM) Discovery Agent é uma ferramenta alimentada por IA do AEM as a Cloud Service que permite aos usuários localizar, recuperar e utilizar conteúdo — inclusive Assets, Fragmentos de conteúdo e Adaptive Forms — usando prompts de linguagem natural. Ele elimina a necessidade de filtragem manual, com muitos cliques ou complexa, entendendo a intenção e realizando pesquisas no repositório.

Para usar o **Discovery Agent**, primeiro você criará algumas marcas na Adobe Experience Manager e marcará alguns ativos usando essas marcas. Depois disso, você poderá usar o Assistente de IA para descobrir ativos de maneira fácil e empresarial.

Ir para [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. A organização que você deve selecionar é `--aepImsOrgName--`.

### Criar e usar tags com a Assets

Clique para abrir seu Programa Cloud Manager, que deve ser chamado de `--aepUserLdap-- - CitiSignal AEM+ACCS`.

![Agentes da AEM](./images/aemagents1.png)

Clique no URL do seu ambiente para abri-lo.

![Agentes da AEM](./images/aemagents2.png)

Clique no ícone **martelo**.

![Agentes da AEM](./images/aemagents3.png)

Em **Geral**, clique em **Marcação**.

![Agentes da AEM](./images/aemagents4.png)

Você deverá ver isso. Clique em **Criar** e selecione **Criar Namespace**.

![Agentes da AEM](./images/aemagents5.png)

No campo **Título**, digite: `CitiSignal`. Clique em **Criar**.

![Agentes da AEM](./images/aemagents6.png)

Detalhe o namespace **CitiSignal** clicando nele. Clique em **Criar** e selecione **Criar Marca**.

![Agentes da AEM](./images/aemagents7.png)

No campo **Título**, digite: `Campaign`. Clique em **Enviar**.

![Agentes da AEM](./images/aemagents8.png)

Selecione a tag **Campaign** clicando nela. Clique em **Criar** e selecione **Criar Marca**.

![Agentes da AEM](./images/aemagents9.png)

No campo **Título**, digite: `Winter 2026`. Clique em **Enviar**.

![Agentes da AEM](./images/aemagents10.png)

Selecione a tag **Campaign** clicando nela. Clique em **Criar** e selecione **Criar Marca**.

![Agentes da AEM](./images/aemagents11.png)

No campo **Título**, digite: `Spring 2026`. Clique em **Enviar**.

![Agentes da AEM](./images/aemagents12.png)

Agora você deve ter isso.

![Agentes da AEM](./images/aemagents13.png)

Clique em **Adobe Experience Manager** e em **Assets**.

![Agentes da AEM](./images/aemagents14.png)

Clique em **Arquivos**.

![Agentes da AEM](./images/aemagents15.png)

Clique duas vezes na pasta **CitiSignal** para abri-la.

![Agentes da AEM](./images/aemagents16.png)

Clique em **Criar** e selecione **Arquivos**.

![Agentes da AEM](./images/aemagents17.png)

Baixe o arquivo [citisignal-images-campaign.zip](./assets/citisignal-images-campaign.zip) e descompacte-o na área de trabalho.

![Agentes da AEM](./images/aemagents17a.png)

Selecione. os 3 arquivos que você acabou de baixar e clique em **abrir**.

![Agentes da AEM](./images/aemagents18.png)

Clique em **Carregar**.

![Agentes da AEM](./images/aemagents19.png)

Você deverá ver isso.

![Agentes da AEM](./images/aemagents20.png)

Selecione a primeira imagem e clique em **Propriedades**.

![Agentes da AEM](./images/aemagents21.png)

Clique no ícone da **pasta** em Marcas.

![Agentes da AEM](./images/aemagents22.png)

Selecione a tag **Segundo trimestre de 2026** e clique em **Selecionar**. Repita esse processo para estas imagens:

- citisignal_lion.png
- citisignal_leopard.png
- citisignal_gorilla.png
- citisignal_rabbit.png

![Agentes da AEM](./images/aemagents23.png)

Depois de selecionar esta marca para todas as imagens, vá para **Experience Manager Assets**.

![Agentes da AEM](./images/aemagents24.png)

Selecione o repositório que você está usando.

![Agentes da AEM](./images/aemagents25.png)

Vá para **Assets** e abra a pasta **CitiSignal**.

![Agentes da AEM](./images/aemagents26.png)

Abra a primeira imagem.

![Agentes da AEM](./images/aemagents27.png)

Selecione **Aprovado** e clique em **Salvar**.

![Agentes da AEM](./images/aemagents28.png)

Em **Marcas**, você pode ver a marca selecionada anteriormente.

![Agentes da AEM](./images/aemagents29.png)

Repita esse processo para que todas as 4 imagens sejam aprovadas.

![Agentes da AEM](./images/aemagents30.png)

Em seguida, vá para **Meu espaço de trabalho** e clique para abrir o **Assistente de IA**.

![Agentes da AEM](./images/aemagents31.png)

Digite o prompt a seguir e clique em **Enviar**.

```javascript
find all assets tagged with 'Spring 2026'
```

![Agentes da AEM](./images/aemagents32.png)

Caso tenha acesso a vários ambientes do AEM Assets CS, você verá algo como isso. Clique na resposta proposta para o ambiente que você deseja usar e clique em **Enviar**.

![Agentes da AEM](./images/aemagents34.png)

Você deverá ver uma resposta semelhante. Clique no ícone para expandir o Assistente de IA para tela cheia.

![Agentes da AEM](./images/aemagents35.png)

Revise as respostas.

![Agentes da AEM](./images/aemagents36.png)

Na janela do Assistente de IA, você pode clicar em para visualizar qualquer um desses ativos.

![Agentes da AEM](./images/aemagents37.png)

Você será levado diretamente para o AEM Assets CS, para essa imagem específica.

![Agentes da AEM](./images/aemagents38.png)

Em seguida, também é possível revisar qualquer outro metadado disponível.

![Agentes da AEM](./images/aemagents39.png)

## Agente de produção de experiência do 1.6.1.2

### Atualização de conteúdo - Assets

A habilidade Atualização de conteúdo atualiza o conteúdo existente — incluindo fragmentos de conteúdo, páginas, formulários e ativos — com facilidade. O agente pode executar ações como atualizar, remover, substituir ou adicionar elementos de conteúdo para manter as experiências precisas e atuais. As entradas podem ser descrições de linguagem natural e, quando usadas com PDFs Jira, as capturas de tela também podem fornecer entradas.

Volte para a tela Assistente de IA.

![Agentes da AEM](./images/aemagents40.png)

Digite o prompt a seguir e clique em **Enviar**.

`Generate multiple social media formats (Instagram 1080x1920, Facebook 1200x630, Twitter 1200x675) for the third image`

![Agentes da AEM](./images/aemagents40a.png)

Após alguns minutos, você verá uma resposta semelhante.

![Agentes da AEM](./images/aemagents41.png)

Revise as imagens geradas.

![Agentes da AEM](./images/aemagents42.png)

### Atualização de conteúdo - Páginas

Volte para o ambiente de Autor do Adobe Experience Manager e vá para **Sites**.

![Agentes da AEM](./images/aemagents43.png)

Vá para **CitiSignal**. Clique em **Criar** e selecione **Página**.

![Agentes da AEM](./images/aemagents44.png)

Selecione **Página** e clique em **Avançar**.

![Agentes da AEM](./images/aemagents45.png)

Insira os seguintes valores:

- Título: **Fibra Máx**
- Nome: **fibra-máx**
- Título da Página: **Fibra Máx**

Clique em **Criar**.

![Agentes da AEM](./images/aemagents46.png)

Selecione **Abrir**.

![Agentes da AEM](./images/aemagents47.png)

Você deverá ver isso.

![Agentes da AEM](./images/aemagents48.png)

Clique na área em branco para selecionar o componente **seção**. Em seguida, clique no ícone de adição **+** no menu direito e selecione **Herói**.

![Agentes da AEM](./images/aemagents49.png)

Você deverá ver isso. Clique em **+ Adicionar** para adicionar uma imagem.

![Agentes da AEM](./images/aemagents50.png)

Selecione o repositório de ativos. Em seguida, abra a pasta **CitiSignal**.

![Agentes da AEM](./images/aemagents51.png)

Escolha a imagem do leão que você carregou anteriormente. Clique em **Selecionar**.

![Agentes da AEM](./images/aemagents52.png)

Você deverá ver isso. Clique na área **texto** para alterar o texto.

![Agentes da AEM](./images/aemagents53.png)

Cole esse texto na área de trabalho:

```
This winter, be as fast as a lion.
```

Selecione **Cabeçalho 1** e clique em **Concluído**.

![Agentes da AEM](./images/aemagents54.png)

Você deverá ver isso. Vá para **Árvore de conteúdo** e selecione a área **Seção**.

![Agentes da AEM](./images/aemagents55.png)

Clique no ícone **+** e selecione **Cartões**.

![Agentes da AEM](./images/aemagents56.png)

Você deverá ver isso. Verifique se na **árvore de conteúdo**, **Cartões** está selecionado.

Em seguida, clique no botão **+** 4 vezes.

![Agentes da AEM](./images/aemagents57.png)

Agora você deve ver isto, onde há 4 objetos **Cartão** no objeto **Cartões**.

![Agentes da AEM](./images/aemagents58.png)

Selecione o primeiro **Cartão**. Clique na área **texto** para alterar o texto.

![Agentes da AEM](./images/aemagents59.png)

Cole o texto a seguir. Verifique se a primeira linha de texto está usando o **Título 1**. Clique em **Concluído**.

```
99.9% network reliability

Game, video chat and stream on multiple devices with ultra low lag.
```

![Agentes da AEM](./images/aemagents60.png)

Selecione o segundo **Cartão**. Clique na área **texto** para alterar o texto.

![Agentes da AEM](./images/aemagents61.png)

Cole o texto a seguir. Verifique se a primeira linha de texto está usando o **Título 1**. Clique em **Concluído**.

```
3-year

price lock guarantee

For new and existing Fiber Max customers on all internet plans.

No hidden fees.
```

![Agentes da AEM](./images/aemagents62.png)

Selecione o terceiro **Cartão**. Clique na área **texto** para alterar o texto.

![Agentes da AEM](./images/aemagents63.png)

Cole o texto a seguir. Verifique se a primeira linha de texto está usando o **Título 1**. Clique em **Concluído**.

```
More ways to save

Save over 45% on the best entertainment with CitiSignal
```

![Agentes da AEM](./images/aemagents64.png)

Selecione o quarto **Cartão**. Clique na área **texto** para alterar o texto.

![Agentes da AEM](./images/aemagents65.png)

Cole o texto a seguir. Verifique se a primeira linha de texto está usando o **Título 1**. Clique em **Concluído**.

```
Get Fiber Max now!

Fill out the form here to get started.
```

![Agentes da AEM](./images/aemagents66.png)

Agora você deve ter isso. Clique em **Publicar**.

![Agentes da AEM](./images/aemagents67.png)

Clique novamente em **Publicar**.

![Agentes da AEM](./images/aemagents68.png)

Clique em **Abrir página**.

![Agentes da AEM](./images/aemagents69.png)

Copie o URL da página como você precisará dele a seguir.

A URL deve ser semelhante a esta: `https://author-pXXXXXX-eXXXXXXX.adobeaemcloud.com/content/CitiSignal/fiber-max.html`.

![Agentes da AEM](./images/aemagents70.png)

Ir para [https://experience.adobe.com/#/experiencemanager/](https://experience.adobe.com/#/experiencemanager/). Clique para abrir o **Assistente de IA**.

![Agentes da AEM](./images/aemagents71.png)

Cole o prompt a seguir e clique em **enviar**. Substitua XXX neste prompt pelo URL copiado na etapa anterior.

```
On the page XXX, please make the following changes:

- change the word 'winter' to 'spring'
- change the word 'lion' to 'leopard'
- change the image in the hero block to use the image 'citisignal_leopard.png'
- change the text '99.9% network reliability' to '99.999% network reliability'
```

![Agentes da AEM](./images/aemagents72.png)

Após 1-2 minutos, você deve ver isso. Digite o prompt `generate` e clique em **Enviar**.

![Agentes da AEM](./images/aemagents74.png)

Alguns minutos depois, você verá uma confirmação como essa de que as alterações foram executadas. Clique em **Visualizar a página atualizada**.

![Agentes da AEM](./images/aemagents75.png)

Agora você obtém uma confirmação visual das alterações que foram feitas. Essa página de visualização é meramente informativa. Não é possível executar ações a partir dessa página.

![Agentes da AEM](./images/aemagents76.png)

Para executar uma ação, clique em **Editar no AEM**.

![Agentes da AEM](./images/aemagents75a.png)

No Editor universal, agora você vê todas as alterações em detalhes, com a capacidade de alterar qualquer coisa. Depois de revisar a página, clique em **Publicar**.

![Agentes da AEM](./images/aemagents77.png)

Clique novamente em **Publicar**. A alteração feita ainda não foi publicada no ambiente de produção. Em vez disso, ele foi publicado em **Inicializações** na AEM.

Os lançamentos permitem desenvolver conteúdo com eficiência para uma versão futura. Uma inicialização é criada para permitir que você faça alterações na preparação para uma publicação futura, ao mesmo tempo em que mantém suas páginas atuais. Isso significa que você está editando duas versões ao mesmo tempo: páginas publicadas no momento e uma versão dessas páginas a serem publicadas posteriormente. Quando essa hora chegar, você poderá substituir as páginas originais e publicar a nova versão.

![Agentes da AEM](./images/aemagents78.png)

Para **Promover** suas alterações pendentes para uma versão futura, volte para a AEM. Clique em **Adobe Experience Manager** na parte superior da página, clique no ícone **martelo** e selecione **Inicializações**.

![Agentes da AEM](./images/aemagents79.png)

Agora você deve ver uma **Inicialização** pendente. Marque a caixa de seleção na frente da **Inicialização** pendente.

![Agentes da AEM](./images/aemagents80.png)

Clique em **Promover**.

![Agentes da AEM](./images/aemagents81.png)

Selecione **Promover lançamento completo** e clique em **Avançar**.

![Agentes da AEM](./images/aemagents82.png)

Clique em **Promover**.

![Agentes da AEM](./images/aemagents83.png)

Você deve ver isso agora. Suas alterações estão em produção agora.

![Agentes da AEM](./images/aemagents84.png)

Atualize a página. Agora você deve ver todas as alterações na página publicada.

![Agentes da AEM](./images/aemagents85.png)

Como alternativa, em vez de passar pelo processo de promoção manual, você também pode inserir o prompt `accept` no Assistente do AI.

![Agentes da AEM](./images/aemagents86.png)

Você deverá receber uma confirmação de que as alterações foram publicadas.

![Agentes da AEM](./images/aemagents87.png)

### Atualização de conteúdo - Criação do formulário

No módulo [Adobe Experience Manager Forms com Edge Delivery Services](./../../asset-mgmt/module1.3/aemforms.md){target="_blank"} você pode encontrar as etapas envolvidas na criação de um formulário de forma manual.

A habilidade de Criação de formulários agora permite que os usuários criem formulários adaptáveis por meio de prompts de linguagem naturais, sem depender de equipes de desenvolvimento ou TI. Esse recurso acelera o desenvolvimento de formulários, mantendo a consistência da marca e permitindo que os usuários empresariais criem formulários sem um conhecimento técnico profundo do produto.

Ir para [https://experience.adobe.com/#/ai-assistant/chat](https://experience.adobe.com/#/ai-assistant/chat).

![Agentes da AEM](./images/aemagentsforms1.png)

Digite o prompt a seguir e clique em **enviar**.

```
Create a new adaptive form using Edge Delivery Services and the existing CitiSignal site, with the following details:
- Form name: "citisignal-fiber-max-interest-2"
- Form fields: 4 text input fields are needed, for "first-name", "last-name", "email" and "city"
- When the form is submitted, send the submission to a spreadsheet, with this URL: https://docs.google.com/spreadsheets/d/1WwKrcM8mZ2d_W3sMheUAw3nFhP_OFk05TsqxhHkudfQ/edit?usp=sharing.
```

## Próximas etapas

Ir para [1.6.2 Servidores e Cursor MCP do AEM](./ex2.md){target="_blank"}

Voltar para [AEM e Agentes](./aemagents.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
