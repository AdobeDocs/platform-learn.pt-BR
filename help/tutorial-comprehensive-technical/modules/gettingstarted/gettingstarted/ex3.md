---
title: Introdução - Criar sequência de dados
description: Introdução - Criar sequência de dados
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 1%

---

# 0.3 Criar a sequência de dados

Ir para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Após o exercício anterior, você agora tem duas propriedades de Coleção de dados: uma para Web e outra para dispositivos móveis.

![DSN](./images/launchprop.png)

Essas propriedades estão quase prontas para serem usadas, mas antes de começar a coletar dados usando essas propriedades, é necessário configurar um fluxo de dados. Você obterá mais informações sobre o conceito do que é um fluxo de dados e o que significa no Exercício 1.2.

Por enquanto, siga estas etapas.

## 0.3.1 Criar a sequência de dados para a Web

Clique em **[!UICONTROL Datastreams]** ou **[!UICONTROL Datastreams (Beta)]**.

![Clique no ícone Configuração do Edge na navegação à esquerda](./images/edgeconfig1a.png)

No canto superior direito da tela, selecione o nome da sandbox, que deve ser `--aepSandboxName--`.

![Clique no ícone Configuração do Edge na navegação à esquerda](./images/edgeconfig1b.png)

Clique em **[!UICONTROL Nova sequência de dados]**.

![Clique no ícone Configuração do Edge na navegação à esquerda](./images/edgeconfig1.png)

Para o **[!UICONTROL Nome Amigável]**, e para a descrição opcional, digite `--aepUserLdap-- - Demo System Datastream`. Para Esquema de Evento, selecione **Sistema de Demonstração - Esquema de Evento para Site (Global v1.1)**. Clique em **Salvar**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig2.png)

Você verá isso. Clique em **Adicionar Serviço**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig3.png)

Selecione o serviço **[!UICONTROL Adobe Experience Platform]**, que irá expor campos adicionais. Você verá isso.

Para Conjunto de Dados de Evento, selecione **Sistema de Demonstração - Conjunto de Dados de Evento para Site (Global v1.1)** e para Conjunto de Dados de Perfil, selecione **Sistema de Demonstração - Conjunto de Dados de Perfil para Site (Global v1.1)**. Clique em **Salvar**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig4.png)

Agora vocês verão isto.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig5.png)

Por enquanto, é isso. No [Módulo 1.1](./../../../modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md), você aprenderá mais sobre o SDK da Web e como configurar todos os seus recursos.

No menu esquerdo, clique em **[!UICONTROL Marcas]**.

Filtre os resultados da pesquisa para ver suas duas propriedades da Coleção de dados. Abra a propriedade de **Web** clicando nela.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig10a.png)

Você verá isso. Clique em **Extensões**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig11.png)

Na extensão SDK da Web do Adobe Experience Platform, clique em **Configurar**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig12.png)

Você verá isso. Para **Datastreams**, você verá um valor fictício definido como 1. Agora é necessário clicar no botão de opção **Escolher da lista**. Na lista suspensa, selecione o fluxo de dados criado anteriormente.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig13.png)

Selecione sua **Sequência de dados**. DICA: você pode filtrar os resultados na lista suspensa facilmente digitando seu `--aepUserLdap--`.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig14.png)

Role para baixo até ver **Coleção de dados**. Certifique-se de que a caixa de seleção **Habilitar coleta de dados de cliques** não esteja habilitada. Clique em **Salvar** para salvar as alterações.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig14a.png)

Vá para **Fluxo de Publicação**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig15.png)

Clique em **...** para **Principal** e em **Editar**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig16.png)

Clique em **Adicionar todos os recursos alterados** e em **Salvar e criar para desenvolvimento**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig17.png)

Suas alterações estão sendo publicadas e estarão prontas em alguns minutos.

## 0.3.2 Criar a sequência de dados para dispositivos móveis

Ir para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/).

Clique em **[!UICONTROL Datastreams]** ou **[!UICONTROL Datastreams (Beta)]**.

![Clique no ícone Datastream na navegação à esquerda](./images/edgeconfig1a.png)

No canto superior direito da tela, selecione o nome da sandbox, que deve ser `--aepSandboxName--`.

![Clique no ícone Configuração do Edge na navegação à esquerda](./images/edgeconfig1b.png)

Clique em **[!UICONTROL Nova sequência de dados]**.

![Clique no ícone Datastream na navegação à esquerda](./images/edgeconfig1.png)

Para o **[!UICONTROL Nome Amigável]**, e para a descrição opcional, digite `--aepUserLdap-- - Demo System Datastream (Mobile)`. Para Esquema de Evento, selecione **Sistema de Demonstração - Esquema de Evento para Aplicativo Móvel (Global v1.1)**. Clique em **Salvar**.

Clique em **[!UICONTROL Salvar]**.

![Nomeie a sequência de dados e salve](./images/edgeconfig2m.png)

Você verá isso. Clique em **Adicionar Serviço**.

![Nomeie a sequência de dados e salve](./images/edgeconfig3m.png)

Selecione o serviço **[!UICONTROL Adobe Experience Platform]**, que irá expor campos adicionais. Você verá isso.

Para o Conjunto de Dados de Evento, selecione **Sistema de Demonstração - Conjunto de Dados de Evento para Aplicativo Móvel (Global v1.1)** e, para o Conjunto de Dados de Perfil, selecione **Sistema de Demonstração - Conjunto de Dados de Perfil para Aplicativo Móvel (Global v1.1)**. Clique em **Salvar**.

![Nomeie a Configuração da Sequência de Dados e salve](./images/edgeconfig4m.png)

Você verá isso.

![Nomeie a Configuração da Sequência de Dados e salve](./images/edgeconfig5m.png)

A sequência de dados agora está pronta para ser usada na propriedade do cliente de coleta de dados da Adobe Experience Platform para dispositivos móveis.

Vá para **Tags** e filtre os resultados da pesquisa para ver suas duas propriedades de Coleção de dados. Abra a propriedade de **Celular** clicando nela.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig10am.png)

Você verá isso. Clique em **Extensões**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig11m.png)

Na extensão **Adobe Experience Platform Edge Network**, clique em **Configurar**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig12m.png)

Você verá isso. Agora é necessário selecionar a sandbox e a sequência de dados corretas que você acabou de configurar. A sandbox a ser usada é `--aepSandboxName--` e a sequência de dados é chamada `--aepUserLdap-- - Demo System Datastream (Mobile)`.

Para o **domínio Edge Network**, use o domínio padrão **edge.adobedc.net**.

Clique em **Salvar** para salvar as alterações.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig13m.png)

Vá para **Fluxo de Publicação**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig15m.png)

Clique no **...** ao lado de **Principal** e em **Editar**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig16m.png)

Clique em **Adicionar todos os recursos alterados** e em **Salvar e criar para desenvolvimento**.

![Nomear a Configuração do Edge e salvar](./images/edgeconfig17m.png)

Suas alterações estão sendo publicadas e estarão prontas em alguns minutos.

Próxima Etapa: [0.4 Usar o site](./ex4.md)

[Voltar ao módulo 0](./getting-started.md)

[Voltar a todos os módulos](./../../../overview.md)