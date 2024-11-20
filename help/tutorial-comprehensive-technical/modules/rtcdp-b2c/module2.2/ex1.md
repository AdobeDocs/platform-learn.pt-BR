---
title: Serviços inteligentes - Preparação de dados da IA do cliente (assimilação)
description: IA do cliente - Preparação de dados (assimilação)
kt: 5342
doc-type: tutorial
exl-id: 71405859-cfc6-4991-a0b0-11c94818a0fa
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 1%

---

# 2.2.1 IA do cliente: preparação de dados (assimilação)

Para que os Serviços inteligentes descubram insights dos dados de eventos de marketing, os dados devem ser semanticamente enriquecidos e mantidos em uma estrutura padrão. Para isso, os Serviços inteligentes usam os esquemas do Adobe Experience Data Model (XDM).
Especificamente, todos os conjuntos de dados usados em Serviços inteligentes devem estar em conformidade com o esquema XDM do **Evento de experiência do consumidor**.

## Criar esquema

Neste exercício, você criará um esquema que contém o **mixin do Evento de Experiência do Consumidor**, que é exigido pelo Serviço Inteligente da **IA do Cliente**.

Faça logon no Adobe Experience Platform acessando esta URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](../../datacollection/module1.2/images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepSandboxName--``. Depois de selecionar a sandbox apropriada, você verá a alteração da tela e agora estará em sua sandbox dedicada.

![Assimilação de dados](../../datacollection/module1.2/images/sb1.png)

No menu esquerdo, clique em **Esquemas** e vá para **Procurar**. Clique em **Criar Esquema**.

![Criar novo esquema](./images/createschemabutton.png)

Na janela pop-up, selecione **Manual** e clique em **Selecionar**.

![Criar novo esquema](./images/schmanual.png)

Em seguida, selecione **Evento de experiência** e clique em **Avançar**.

![Criar novo esquema](./images/xdmee.png)

É necessário fornecer um nome para o esquema agora. Como o nome do nosso esquema, use este: `--aepUserLdap-- - Demo System - Customer Experience Event` e clique em **Concluir**.

![Criar novo esquema](./images/schname.png)

Você verá isso. Clique em **+ Adicionar** em Grupos de campos.

![Criar novo esquema](./images/xdmee1.png)

Pesquise e selecione os **Grupos de Campos** a seguir para adicionar a este Esquema:

- Evento de experiência do consumidor
- Detalhes da ID do usuário final

Clique em **Adicionar grupos de campos**.

![Novo esquema CEE](./images/cee.png)

Você verá isso. Clique no **Detalhes da ID do Usuário Final** do Grupo de Campos.

![Criar novo esquema](./images/eui1.png)

Navegue até o campo **endUserIDs._experience.emailid.id**.

![Criar novo esquema](./images/eui2.png)

No menu direito do campo **endUserIDs._experience.emailid.id**, role para baixo e marque a caixa de seleção de **Identidade**, marque a caixa de seleção de **Identidade Primária** e selecione o **Namespace de identidade** de **Email**. Clique em **Aplicar**.

![Criar novo esquema](./images/eui3.png)

Navegue até o campo **endUserIDs._experience.mcid.id**. Marque a caixa de seleção de **Identidade** e selecione o **Namespace de identidade** de **ECID**. Clique em **Aplicar**.

![Criar novo esquema](./images/eui4.png)

Então você terá isto. Em seguida, selecione o nome do schema. Agora você deve habilitar seu esquema para o **Perfil**, clicando na opção **Perfil**.

![Criar novo esquema](./images/xdmee3.png)

Você verá isso. Clique em **Habilitar**.

![Criar novo esquema](./images/xdmee4.png)

Agora você deve ter isso. Clique em **Salvar** para salvar seu esquema.

![Criar novo esquema](./images/xdmee5.png)

## Criar conjunto de dados

No menu esquerdo, clique em **Conjuntos de Dados** e vá para **Procurar**. Clique em **Criar conjunto de dados**.

![Conjunto de dados](./images/createds.png)

Clique em **Criar conjunto de dados do esquema**.

![Conjunto de dados](./images/createdatasetfromschema.png)

Na próxima tela, selecione o conjunto de dados criado no exercício anterior, denominado **[!UICONTROL ldap - Sistema de demonstração - Evento de experiência do cliente]**. Clique em **Next**.

![Conjunto de dados](./images/createds1.png)

Como um nome para seu conjunto de dados, use `--aepUserLdap-- - Demo System - Customer Experience Event Dataset`. Clique em **Concluir**.

![Conjunto de dados](./images/createds2.png)

Seu conjunto de dados foi criado. Habilitar a alternância **Perfil**.

![Conjunto de dados](./images/createds3.png)

Clique em **Habilitar**.

![Conjunto de dados](./images/createds4.png)

Agora você deve ter:

![Conjunto de dados](./images/createds5.png)

Agora você está pronto para começar a assimilar dados do Evento de experiência do consumidor e começar a usar o serviço de IA do cliente.

## Baixar dados de teste do Evento de experiência

Depois que o **Esquema** e o **Conjunto de dados** estiverem configurados, você estará pronto para assimilar dados do Evento de Experiência. Como a IA do cliente requer dados em **2 trimestres pelo menos**, será necessário assimilar dados preparados externamente.

Os dados preparados para os eventos de experiência devem estar em conformidade com os requisitos e o esquema do [Mixin do XDM do Evento de Experiência do Consumidor](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md).

Baixe o arquivo que contém dados de exemplo deste local: [https://dashboard.adobedemo.com/data](https://dashboard.adobedemo.com/data). Clique no botão **Baixar**.

![Conjunto de dados](./images/dsn1.png)

Como alternativa, se você não puder acessar o link acima, também poderá baixar o arquivo deste local: [https://aepmodule10.s3-us-west-2.amazonaws.com/retail-v1-dec2020-xl.json.zip](https://aepmodule10.s3-us-west-2.amazonaws.com/retail-v1-dec2020-xl.json.zip).

Você baixou um arquivo chamado **retail-v1-dec2020-xl.json.zip**. Coloque o arquivo na área de trabalho do seu computador e descompacte-o, e você verá um arquivo chamado **retail-v1.json**. Você precisará desse arquivo no próximo exercício.

![Conjunto de dados](./images/ingest.png)

## Assimilar dados de teste do Evento de experiência

No Adobe Experience Platform, vá para **Conjuntos de Dados** e abra seu conjunto de dados, denominado **[!UICONTROL ldap - Sistema de demonstração - Conjunto de Dados de Eventos de Experiência do Cliente]**.

![Conjunto de dados](./images/ingest1.png)

No seu conjunto de dados, clique em **Escolher arquivos** para adicionar dados.

![Conjunto de dados](./images/ingest2.png)

No pop-up, selecione o arquivo **retail-v1.json** e clique em **Abrir**.

![Conjunto de dados](./images/ingest3.png)

Você verá os dados sendo importados e um novo lote será criado no estado **Carregando**. Não saia desta página até que o arquivo seja carregado.

![Conjunto de dados](./images/ingest4.png)

Após carregar o arquivo, você verá a alteração do status do lote de **Carregando** para **Processando**.

![Conjunto de dados](./images/ingest5.png)

A assimilação e o processamento de dados podem levar de 10 a 20 minutos.

Quando a assimilação de dados for bem-sucedida, o status do lote será alterado para **Sucesso**.

![Conjunto de dados](./images/ingest7.png)

![Conjunto de dados](./images/ingest8.png)

Próxima etapa: [2.2.2 IA do cliente - Criar uma nova instância (Configurar)](./ex2.md)

[Voltar ao módulo 2.2](./intelligent-services.md)

[Voltar a todos os módulos](./../../../overview.md)
