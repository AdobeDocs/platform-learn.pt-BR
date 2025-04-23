---
title: Introdução - Criar sequência de dados
description: Introdução - Criar sequência de dados
kt: 5342
doc-type: tutorial
exl-id: d36057b4-64c6-4389-9612-d3c9cf013117
source-git-commit: e95acadeb7a0438f9be056dd426063ac8abc6bc0
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 1%

---

# Criar fluxo de dados

Ir para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/){target="_blank"}.

![DSN](./images/launchprop.png)

No menu esquerdo, clique em **[!UICONTROL Marcas]**. Após o exercício anterior, você agora tem três propriedades de Coleção de dados: uma para Web, uma para dispositivos móveis e uma para o aplicativo CX.

![DSN](./images/launchprop1.png)

Essas propriedades estão quase prontas para serem usadas, mas antes de começar a coletar dados usando essas propriedades, é necessário configurar um fluxo de dados. Você obterá mais informações sobre o conceito de sequência de dados e o que significa em um exercício posterior no módulo Coleção de dados.

Por enquanto, siga estas etapas.

## Criar a sequência de dados para a Web

Clique em **[!UICONTROL Datastreams]**.

![Clique no ícone Configuração do Edge na navegação à esquerda](./images/edgeconfig1a.png)

No canto superior direito da tela, selecione o nome da sandbox, que deve ser `--aepSandboxName--`.

![Clique no ícone Configuração do Edge na navegação à esquerda](./images/edgeconfig1b.png)

Clique em **[!UICONTROL Nova sequência de dados]**.

![Clique no ícone Configuração do Edge na navegação à esquerda](./images/edgeconfig1.png)

Para o **[!UICONTROL Nome]** e para a descrição opcional, digite `--aepUserLdap-- - One Adobe Datastream`. Para **Esquema de Mapeamento**, selecione **Sistema de Demonstração - Esquema de Evento para Site (Global v1.1)**. Clique em **Salvar**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig2.png)

Você verá isso. Clique em **Adicionar Serviço**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig3.png)

Selecione o serviço **[!UICONTROL Adobe Experience Platform]**, que irá expor campos adicionais. Você verá isso.

Para Conjunto de Dados de Evento, selecione **Sistema de Demonstração - Conjunto de Dados de Evento para Site (Global v1.1)** e para Conjunto de Dados de Perfil, selecione **Sistema de Demonstração - Conjunto de Dados de Perfil para Site (Global v1.1)**. Clique em **Salvar**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig4.png)

Agora vocês verão isto.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig5.png)

No menu esquerdo, clique em **[!UICONTROL Marcas]**.

Filtre os resultados da pesquisa para ver as propriedades da Coleção de dados. Abra a propriedade de **Web** clicando nela.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig10a.png)

Você verá isso. Clique em **Extensões**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig11.png)

Primeiro, clique na extensão Adobe Experience Platform Web SDK e em **Configurar**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig12.png)

Você verá isso. Consulte o menu **Datastreams** e verifique se a sandbox correta está selecionada, que no seu caso deve ser `--aepSandboxName--`.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig12a.png)

Abra a lista suspensa **Datastreams** e selecione a Datastream criada anteriormente.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig13.png)

Selecione sua **Sequência de dados** em todos os três ambientes diferentes. Em seguida, clique em **Salvar**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig14.png)

Vá para **Fluxo de Publicação**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig15.png)

Clique em **...** para **Principal** e em **Editar**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig16.png)

Clique em **Adicionar todos os recursos alterados** e em **Salvar e criar para desenvolvimento**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig17.png)

As alterações estão sendo publicadas e estarão prontas em alguns minutos, após os quais você verá o ponto verde ao lado de **Principal**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig17a.png)

## Criar a sequência de dados para dispositivos móveis

Ir para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/){target="_blank"}.

Clique em **[!UICONTROL Datastreams]**.

![Clique no ícone Datastream na navegação à esquerda](./images/edgeconfig1a.png)

No canto superior direito da tela, selecione o nome da sandbox, que deve ser `--aepSandboxName--`.

![Clique no ícone Configuração do Edge na navegação à esquerda](./images/edgeconfig1b.png)

Clique em **[!UICONTROL Nova sequência de dados]**.

![Clique no ícone Datastream na navegação à esquerda](./images/edgeconfig1.png)

Para o **[!UICONTROL Nome Amigável]**, e para a descrição opcional, digite `--aepUserLdap-- - One Adobe Datastream (Mobile)`. Para **Esquema de Mapeamento**, selecione **Sistema de Demonstração - Esquema de Evento para Aplicativo Móvel (Global v1.1)**. Clique em **Salvar**.

Clique em **[!UICONTROL Salvar]**.

![Nomeie a sequência de dados e salve](./images/edgeconfig2m.png)

Você verá isso. Clique em **Adicionar Serviço**.

![Nomeie a sequência de dados e salve](./images/edgeconfig3m.png)

Selecione o serviço **[!UICONTROL Adobe Experience Platform]**, que irá expor campos adicionais. Você verá isso.

Para o Conjunto de Dados de Evento, selecione **Sistema de Demonstração - Conjunto de Dados de Evento para Aplicativo Móvel (Global v1.1)** e, para o Conjunto de Dados de Perfil, selecione **Sistema de Demonstração - Conjunto de Dados de Perfil para Aplicativo Móvel (Global v1.1)**. Clique em **Salvar**.

![Nomeie a Configuração da Sequência de Dados e salve](./images/edgeconfig4m.png)

Você verá isso.

![Nomeie a Configuração da Sequência de Dados e salve](./images/edgeconfig5m.png)

A sequência de dados agora está pronta para ser usada na propriedade do Cliente da coleção de dados da Adobe Experience Platform para dispositivos móveis.

Vá para **Tags** e filtre os resultados da pesquisa para ver suas duas propriedades de Coleção de dados. Abra a propriedade de **Celular** clicando nela.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig10am.png)

Você verá isso. Clique em **Extensões**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig11m.png)

Clique na extensão **Adobe Experience Platform Edge Network** e em **Configurar**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig12m.png)

Você verá isso. Agora é necessário selecionar a sandbox e a sequência de dados corretas que você acabou de configurar. A sandbox a ser usada é `--aepSandboxName--` e a sequência de dados é chamada `--aepUserLdap-- - One Adobe Datastream (Mobile)`.

Para o **domínio do Edge Network**, use o domínio padrão.

Clique em **Salvar** para salvar as alterações.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig13m.png)

Vá para **Fluxo de Publicação**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig15m.png)

Clique no **...** ao lado de **Principal** e em **Editar**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig16m.png)

Clique em **Adicionar todos os recursos alterados** e em **Salvar e criar para desenvolvimento**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig17m.png)

As alterações estão sendo publicadas e estarão prontas em alguns minutos, após os quais você verá o ponto verde ao lado de **Principal**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig17ma.png)

## Próximas etapas

Ir para [Usar o site](./ex4.md){target="_blank"}

Volte para [Introdução](./getting-started.md){target="_blank"}

Voltar para [Todos os módulos](./../../../overview.md){target="_blank"}