---
title: Configurar o ambiente do AEM CS
description: Configurar o ambiente do AEM CS
kt: 5342
doc-type: tutorial
exl-id: 62715072-0257-4d07-af1a-8becbb793459
source-git-commit: 490bc79332bb84520ba084ec784ea3ef48a68fb5
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 1%

---

# 1.1.2 Configurar o ambiente do AEM CS

## 1.1.2.1 Configurar seu repositório GitHub

Ir para [https://github.com](https://github.com){target="_blank"}. Clique em **Fazer logon**.

![AEMCS](./images/aemcssetup1.png)

Insira suas credenciais. Clique em **Fazer logon**.

![AEMCS](./images/aemcssetup2.png)

Depois de fazer logon, você verá seu Painel do GitHub.

![AEMCS](./images/aemcssetup3.png)

Ir para [https://github.com/adobe-rnd/aem-boilerplate-xcom](https://github.com/adobe-rnd/aem-boilerplate-xcom){target="_blank"}. Você verá isso. Clique em **Usar este modelo** e em **Criar um novo repositório**.

![AEMCS](./images/aemcssetup4.png)

Para o **Nome do repositório**, use `citisignal-aem-accs`. Defina a visibilidade como **Particular**. Clique em **Criar repositório**.

![AEMCS](./images/aemcssetup5.png)

Após alguns segundos, o repositório será criado.

![AEMCS](./images/aemcssetup6.png)

Em seguida, vá para [https://github.com/apps/aem-code-sync](https://github.com/apps/aem-code-sync){target="_blank"}. Clique em **Instalar** ou **Configurar**.

![AEMCS](./images/aemcssetup7.png)

Clique no botão **Continuar** ao lado da sua conta de usuário do GitHub.

![AEMCS](./images/aemcssetup8.png)

Clique em **Configurar** ao lado da sua conta de usuário do GitHub.

![AEMCS](./images/aemcssetup8a.png)

Clique em **Selecionar apenas repositórios** e, em seguida, adicionar o repositório que você acabou de criar.

![AEMCS](./images/aemcssetup9.png)

Role para baixo e clique em **Salvar**.

![AEMCS](./images/aemcssetup9a.png)

Você receberá essa confirmação.

![AEMCS](./images/aemcssetup10.png)

## 1.1.2.2 Atualizar o arquivo fstab.yaml

No repositório do GitHub, clique em para abrir o arquivo `fstab.yaml`.

![AEMCS](./images/aemcssetup11.png)

Clique no ícone **editar**.

![AEMCS](./images/aemcssetup12.png)

Agora é necessário atualizar o valor do campo **url** na linha 3.

![AEMCS](./images/aemcssetup13.png)

É necessário substituir o valor atual pelo URL do seu ambiente específico do AEM Sites CS em combinação com as configurações do seu repositório GitHub.

Este é o valor atual da URL: `https://author-p130360-e1272151.adobeaemcloud.com/bin/franklin.delivery/adobe-rnd/aem-boilerplate-xcom/main`.

Há 3 partes do URL que precisam ser atualizadas

`https://XXX/bin/franklin.delivery/YYY/ZZZ/main`

XXX deve ser substituído pelo URL do ambiente do AEM CS Author.

AAAA deve ser substituído pela conta de usuário do GitHub.

ZZZ deve ser substituído pelo nome do repositório GitHub usado no exercício anterior.

Você pode encontrar a URL do seu ambiente de autor do AEM CS acessando [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Clique no **Programa** para abri-lo.

![AEMCS](./images/aemcs6.png)

Em seguida, clique nos 3 pontos **...** na guia **Ambientes** e clique em **Exibir Detalhes**.

![AEMCS](./images/aemcs9.png)

Você verá os detalhes do seu ambiente, incluindo a URL do seu ambiente **Autor**. Copie o URL.

![AEMCS](./images/aemcs10.png)

XXX = `author-p166717-e1786231.adobeaemcloud.com`

Para o nome da conta de usuário do GitHub, você pode encontrá-lo facilmente no URL do seu navegador. Neste exemplo, o nome da conta de usuário é `woutervangeluwe`.

AAAA = `woutervangeluwe`

![AEMCS](./images/aemcs11.png)

Para o nome do repositório GitHub, você também pode encontrá-lo na janela do navegador aberta no GitHub. Nesse caso, o nome do repositório é `citisignal`.

ZZ = `citisignal-aem-accs`

![AEMCS](./images/aemcs12.png)

Esses 3 valores combinados levam a esta nova URL que precisa ser configurada no arquivo `fstab.yaml`.

`https://author-p166717-e1786231.adobeaemcloud.com/bin/franklin.delivery/woutervangeluwe/citisignal-aem-accs/main`

Clique em **Confirmar alterações...**.

![AEMCS](./images/aemcs13.png)

Clique em **Confirmar alterações**.

![AEMCS](./images/aemcs14.png)

O arquivo `fstab.yaml` foi atualizado.

## 1.1.2.3 Carregar ativos do CitiSignal

Ir para [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Clique no **Programa** para abri-lo.

![AEMCS](./images/aemcs6.png)

Em seguida, clique no URL do ambiente do autor.

![AEMCS](./images/aemcssetup18.png)

Clique em **Fazer logon com o Adobe**.

![AEMCS](./images/aemcssetup19.png)

Em seguida, você verá seu ambiente de Autor.

![AEMCS](./images/aemcssetup20.png)

Sua URL será assim: `https://author-p166717-e1786231.adobeaemcloud.com/ui#/aem/aem/start.html?appId=aemshell`

Agora é necessário acessar o ambiente **CRX Package Manager** do AEM. Para fazer isso, remova `ui#/aem/aem/start.html?appId=aemshell` da URL e substitua-a por `crx/packmgr`, o que significa que sua URL deve ficar semelhante a esta agora:
`https://author-p166717-e1786231.adobeaemcloud.com/crx/packmgr`.
Clique em **Enter** para carregar o ambiente do gerenciador de pacotes

![AEMCS](./images/aemcssetup22.png)

Em seguida, clique em **Carregar pacote**.

![AEMCS](./images/aemcssetup21.png)

Clique em **Procurar** para localizar o pacote a ser carregado.

O pacote a ser carregado é chamado de **citisignal-assets.zip** e pode ser baixado aqui: [https://tech-insiders.s3.us-west-2.amazonaws.com/one-adobe/citisignal-assets.zip](https://tech-insiders.s3.us-west-2.amazonaws.com/one-adobe/citisignal-assets.zip){target="_blank"}.

![AEMCS](./images/aemcssetup23.png)

Selecione o pacote e clique em **Abrir**.

![AEMCS](./images/aemcssetup24.png)

Em seguida, clique em **OK**.

![AEMCS](./images/aemcssetup25.png)

O pacote será carregado.

![AEMCS](./images/aemcssetup26.png)

Em seguida, clique em **Instalar** no pacote que acabou de carregar.

![AEMCS](./images/aemcssetup27.png)

Clique em **Instalar**.

![AEMCS](./images/aemcssetup28.png)

Após alguns minutos, o pacote será instalado.

![AEMCS](./images/aemcssetup29.png)

Agora você pode fechar esta janela.

## 1.1.2.4 Publicar ativos do CitiSignal

Ir para [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Clique no **Programa** para abri-lo.

![AEMCS](./images/aemcs6.png)

Em seguida, clique no URL do ambiente do autor.

![AEMCS](./images/aemcssetup18.png)

Clique em **Fazer logon com o Adobe**.

![AEMCS](./images/aemcssetup19.png)

Em seguida, você verá seu ambiente de Autor. Clique em **Assets**.

![AEMCS](./images/aemcsassets1.png)

Clique em **Arquivos**.

![AEMCS](./images/aemcsassets2.png)

Clique para selecionar a pasta **CitiSignal** e clique em **Gerenciar Publicação**.

![AEMCS](./images/aemcsassets3.png)

Clique em **Next**.

![AEMCS](./images/aemcsassets4.png)

Clique em **Publicar**.

![AEMCS](./images/aemcsassets5.png)

Seus ativos foram publicados.

## 1.1.2.5 Criar site do CitiSignal

Ir para [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Clique no **Programa** para abri-lo.

![AEMCS](./images/aemcs6.png)

Em seguida, clique no URL do ambiente do autor.

![AEMCS](./images/aemcssetup18.png)

Clique em **Fazer logon com o Adobe**.

![AEMCS](./images/aemcssetup19.png)

Em seguida, você verá seu ambiente de Autor. Clique em **Sites**.

![AEMCS](./images/aemcssetup30.png)

Clique em **Criar** e em **Site do modelo**.

![AEMCS](./images/aemcssetup31.png)

Clique em **Importar**.

![AEMCS](./images/aemcssetup32.png)

Agora é necessário importar um modelo pré-configurado para o site. Você pode baixar o modelo [aqui](./../../../assets/aem/citisignal-aem-sites-commerce-with-edge-delivery-services-template-0.4.0.zip){target="_blank"}. Salve o arquivo na área de trabalho.

Em seguida, selecione o arquivo `citisignal-aem-sites-commerce-with-edge-delivery-services-template-0.4.0.zip` e clique em **Abrir**.

![AEMCS](./images/aemcssetup33.png)

Você verá isso. Clique para selecionar o modelo que acabou de carregar e clique em **Avançar**.

![AEMCS](./images/aemcssetup34.png)

Agora você precisa preencher alguns detalhes.

- Título do site: use **CitiSignal**
- Nome do site: use **CitiSignal**
- URL do GitHub: copie o URL do repositório GitHub que você estava usando antes

![AEMCS](./images/aemcssetup35.png)

Então você terá isto. Clique em **Criar**.

![AEMCS](./images/aemcssetup36.png)

Seu site está sendo criado. Isso pode levar alguns minutos. Clique em **OK**.

![AEMCS](./images/aemcssetup37.png)

Atualize a tela após alguns minutos. Você verá o site do CitiSignal recém-criado.

![AEMCS](./images/aemcssetup38.png)

## 1.1.2.6 Atualizar o arquivo paths.json

No repositório do GitHub, clique em para abrir o arquivo `paths.json`.

![AEMCS](./images/aemcssetupjson1.png)

Clique no ícone **editar**.

![AEMCS](./images/aemcssetupjson2.png)

Agora é necessário atualizar a substituição do texto `aem-boilerplate-commerce` por `CitiSignal` nas linhas 3, 4, 5, 6, 7 e 10.

Clique em **Confirmar alterações**.

![AEMCS](./images/aemcssetupjson3.png)

Clique em **Confirmar alterações**.

![AEMCS](./images/aemcssetupjson4.png)

O arquivo `paths.json` foi atualizado.

## 1.1.2.7 Publicar site do CitiSignal

Em seguida, clique na caixa de seleção na frente de **CitiSignal**. Em seguida, clique em **Gerenciar publicação**.

![AEMCS](./images/aemcssetup39.png)

Clique em **Next**.

![AEMCS](./images/aemcssetup40.png)

Clique em **Incluir configurações secundárias**.

![AEMCS](./images/aemcssetup41.png)

Clique para marcar a caixa de seleção **Incluir filhos** e clique para desmarcar as outras caixas de seleção. Clique em **OK**.

![AEMCS](./images/aemcssetup42.png)

Clique em **Publicar**.

![AEMCS](./images/aemcssetup43.png)

Você será enviado de volta para cá. Clique em **CitiSignal**, marque a caixa de seleção na frente do **índice** e clique em **Editar**.

![AEMCS](./images/aemcssetup44.png)

Seu site será aberto no **Editor Universal**.

![AEMCS](./images/aemcssetup45.png)

Agora você pode acessar seu site indo até `main--citisignal-aem-accs--XXX.aem.page` e/ou `main--citisignal-aem-accs--XXX.aem.live`, depois de substituir XXX pela sua conta de usuário do GitHub, que neste exemplo é `woutervangeluwe`.

Neste exemplo, o URL completo torna-se isto:
`https://main--citisignal-aem-accs--woutervangeluwe.aem.page` e/ou `https://main--citisignal-aem-accs--woutervangeluwe.aem.live`.

Pode levar algum tempo até que todos os ativos sejam exibidos corretamente, pois precisam ser publicados primeiro.

Você verá isto:

![AEMCS](./images/aemcssetup46.png)

## Desempenho da página de teste 1.1.2.8

Ir para [https://pagespeed.web.dev/](https://pagespeed.web.dev/){target="_blank"}. Insira sua URL e clique em **Analisar**.

![AEMCS](./images/aemcssetup48.png)

Em seguida, você verá que seu site, em uma visualização para dispositivos móveis e desktop, obtém uma pontuação alta:

**Celular**:

![AEMCS](./images/aemcssetup49.png)

**Área de Trabalho**:

![AEMCS](./images/aemcssetup50.png)

Próxima etapa: [Desenvolver um bloco personalizado](./ex4.md){target="_blank"}

Voltar para o [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./aemcs.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
