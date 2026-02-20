---
title: Content Production Agent
description: Content Production Agent
kt: 5342
doc-type: tutorial
exl-id: cb1bf6f0-f329-4e38-ba64-36ffdc3b8bd4
source-git-commit: 7ea3bdc9557ea9e88ddd9693f9ffbfbc634857f8
workflow-type: tm+mt
source-wordcount: '859'
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

### Atualização de conteúdo

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

### Criação do formulário

A habilidade de Criação de formulários permite que os usuários criem formulários adaptáveis por meio de prompts de linguagem naturais, sem depender de equipes de desenvolvimento ou TI. Esse recurso acelera o desenvolvimento de formulários, mantendo a consistência da marca e permitindo que os usuários empresariais criem formulários sem um conhecimento técnico profundo do produto.


## Próximas etapas

Voltar para [AEM e Agentes](./aemagents.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
