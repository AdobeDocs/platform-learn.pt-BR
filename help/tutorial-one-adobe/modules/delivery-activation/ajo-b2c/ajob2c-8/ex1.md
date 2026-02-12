---
title: Configuração da sua base de dados relacional
description: Configuração da sua base de dados relacional
kt: 5342
doc-type: tutorial
exl-id: 532e5f2c-971f-488f-bef4-3a8141408cc8
source-git-commit: 7a595d9b1fb3dc6a3b5b413e65dbaaaf5ac143c4
workflow-type: tm+mt
source-wordcount: '1805'
ht-degree: 4%

---

# 3.8.1 Configuração da sua base de dados relacional

Faça login no Adobe Journey Optimizer em [https://experience.adobe.com](https://experience.adobe.com). Clique em **Journey Optimizer**.

![OC do AJO](./images/aechome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`.

![OC do AJO](./images/ajohome.png)

## 3.8.1.1 Configuração de esquema baseada em relação

Um esquema com base relacional é a definição formal do modelo de dados com base em modelo.

Especifica:

- O conjunto de tabelas
- As colunas em cada tabela
- As restrições
- As relações entre tabelas

Organizar esquemas ou tabelas em um modelo de dados baseado em modelo é estruturar seus dados em várias tabelas. Certifique-se de que cada tabela armazene um tipo de entidade/esquema.

Ao assimilar dados no para uso com as Campanhas orquestradas da Adobe Journey Optimizer, as seguintes fontes estão disponíveis:

- Amazon S3
- Google Cloud Storage
- SFTP
- Snowflake
- Google BigQuery
- Data Landing Zone
- Azure Databricks
- Upload de arquivo local

A primeira etapa deste exercício é a configuração dos esquemas XDM com base relacional. No menu esquerdo, role até **Gerenciamento de dados** e selecione **Esquemas**. Clique em **+ Criar esquema**.

![OC do AJO](./images/ajoocdata1.png)

Selecione **Relacional**.

![OC do AJO](./images/ajoocdata2.png)

Selecione **Carregar arquivo DDL** e clique em **Escolher arquivos**.

![OC do AJO](./images/ajoocdata3.png)

Baixe o arquivo [citisignal_ddl_tables_only.sql](./assets/citisignal_ddl_tables_only.sql) na área de trabalho.

![OC do AJO](./images/ajoocdata4.png)

Selecione o arquivo **`citisignal_ddl_tables_only.sql`** e clique em **abrir**.

![OC do AJO](./images/ajoocdata5.png)

Você deverá ver isso. Clique em **Next**.

![OC do AJO](./images/ajoocdata6.png)

### Identidade

Alguns de seus esquemas contêm identificadores pessoais e esses campos devem ser marcados como **Identidade**, e você precisa selecionar o **Namespace** que é aplicável a esse tipo específico de identidade.

**`citisignal_accounts`**

Para este esquema, vá para o campo **account_id** e defina o tipo **Identity** como **Sistema de Demonstração - CRMID**.

![OC do AJO](./images/ajoocdata7.png)

**`citisignal_recipients`**

Para este esquema, vá para o campo **account_id** e defina o tipo **Identidade** como **Sistema de Demonstração - CRMID**, vá para o campo **email** e defina o tipo **Identidade** como **Email**.

![OC do AJO](./images/ajoocdata8.png)

### Controle de versão

Para rastrear as atualizações nos dados que serão assimilados em relação a esses esquemas, é necessário definir um campo que será usado para rastrear a versão dos dados carregados. O campo usado para isso em todos esses esquemas é o campo **última modificação**, que contém um carimbo de data/hora dos dados carregados.

Agora é necessário marcar a caixa de seleção para **Controle de Versão** para o campo **última modificação** em cada um desses esquemas.

**`citisignal_products`**

Marque a caixa de seleção para **Controle de Versão** para o campo **última modificação**.

![OC do AJO](./images/ajoocdata9.png)

**`citisignal_product_bundles`**

Marque a caixa de seleção para **Controle de Versão** para o campo **última modificação**.

![OC do AJO](./images/ajoocdata10.png)

**`citisignal_product_relationships`**

Marque a caixa de seleção para **Controle de Versão** para o campo **última modificação**.

![OC do AJO](./images/ajoocdata11.png)

**`citisignal_accounts`**

Marque a caixa de seleção para **Controle de Versão** para o campo **última modificação**.

![OC do AJO](./images/ajoocdata12.png)

**`citisignal_recipients`**

Marque a caixa de seleção para **Controle de Versão** para o campo **última modificação**.

![OC do AJO](./images/ajoocdata13.png)

**`citisignal_mobile_subscriptions`**

Marque a caixa de seleção para **Controle de Versão** para o campo **última modificação**.

![OC do AJO](./images/ajoocdata14.png)

**`citisignal_internet_subscriptions`**

Marque a caixa de seleção para **Controle de Versão** para o campo **última modificação**.

![OC do AJO](./images/ajoocdata15.png)

**`citisignal_tv_subscriptions`**

Marque a caixa de seleção para **Controle de Versão** para o campo **última modificação**.

![OC do AJO](./images/ajoocdata16.png)

**`citisignal_equipment_subscriptions`**

Marque a caixa de seleção para **Controle de Versão** para o campo **última modificação**.

![OC do AJO](./images/ajoocdata17.png)

**`citisignal_mobile_usage_summary`**

Marque a caixa de seleção para **Controle de Versão** para o campo **última modificação**.

![OC do AJO](./images/ajoocdata18.png)

**`citisignal_internet_usage_summary`**

Marque a caixa de seleção para **Controle de Versão** para o campo **última modificação**.

![OC do AJO](./images/ajoocdata19.png)

**`citisignal_offers`**

Marque a caixa de seleção para **Controle de Versão** para o campo **última modificação**.

![OC do AJO](./images/ajoocdata20.png)

**`citisignal_offer_eligibility`**

Marque a caixa de seleção para **Controle de Versão** para o campo **última modificação**.

![OC do AJO](./images/ajoocdata21.png)

### Nome do esquema

Ao assimilar esses esquemas para fins de ativação em uma sandbox compartilhada, é necessário alterar o nome de cada esquema para que ele seja exclusivo nessa sandbox específica. O motivo para fazer essa alteração é evitar conflitos de nomenclatura de esquema.

Para este laboratório, você deve adicionar seu LDAP na frente de cada nome de esquema, o que significa que cada nome de esquema deve ter este prefixo: `--aepUserLdap--_`

**`citisignal_products`**

Altere o nome do esquema para `--aepUserLdap--_ citisignal_products`.

![OC do AJO](./images/ajoocdatan9.png)

**`citisignal_product_bundles`**

Altere o nome do esquema para `--aepUserLdap--_ citisignal_product_bundles`.

![OC do AJO](./images/ajoocdatan10.png)

**`citisignal_product_relationships`**

Altere o nome do esquema para `--aepUserLdap--_ citisignal_product_relationships`.

![OC do AJO](./images/ajoocdatan11.png)

**`citisignal_accounts`**

Altere o nome do esquema para `--aepUserLdap--_ citisignal_accounts`.

![OC do AJO](./images/ajoocdatan12.png)

**`citisignal_recipients`**

Altere o nome do esquema para `--aepUserLdap--_ citisignal_recipients`.

![OC do AJO](./images/ajoocdatan13.png)

**`citisignal_mobile_subscriptions`**

Altere o nome do esquema para `--aepUserLdap--_ citisignal_mobile_subscriptions`.

![OC do AJO](./images/ajoocdatan14.png)

**`citisignal_internet_subscriptions`**

Altere o nome do esquema para `--aepUserLdap--_ citisignal_internet_subscriptions`.

![OC do AJO](./images/ajoocdatan15.png)

**`citisignal_tv_subscriptions`**

Altere o nome do esquema para `--aepUserLdap--_ citisignal_internet_subscriptions`.

![OC do AJO](./images/ajoocdatan16.png)

**`citisignal_equipment_subscriptions`**

Altere o nome do esquema para `--aepUserLdap--_ citisignal_equipment_subscriptions`.

![OC do AJO](./images/ajoocdatan17.png)

**`citisignal_mobile_usage_summary`**

Altere o nome do esquema para `--aepUserLdap--_ citisignal_mobile_usage_summary`.

![OC do AJO](./images/ajoocdatan18.png)

**`citisignal_internet_usage_summary`**

Altere o nome do esquema para `--aepUserLdap--_ citisignal_internet_usage_summary`.

![OC do AJO](./images/ajoocdatan19.png)

**`citisignal_offers`**

Altere o nome do esquema para `--aepUserLdap--_ citisignal_offers`.

![OC do AJO](./images/ajoocdatan20.png)

**`citisignal_offer_eligibility`**

Altere o nome do esquema para `--aepUserLdap--_ citisignal_offer_eligibility`.

![OC do AJO](./images/ajoocdatan21.png)

Seus esquemas agora estão prontos para serem salvos. Clique em **Concluído**.

![OC do AJO](./images/ajoocdata22.png)

Você deverá ver isso. Clique em **Salvar**.

![OC do AJO](./images/ajoocdata23.png)

Clique em **Abrir trabalhos**.

![OC do AJO](./images/ajoocdata24.png)

Você deverá ver isso. Aguarde até que o trabalho seja concluído com êxito antes de prosseguir para a próxima etapa.

![OC do AJO](./images/ajoocdata25.png)

Depois que o trabalho for concluído com sucesso, você poderá continuar com a próxima etapa. Isso pode levar de 5 a 10 minutos.

![OC do AJO](./images/ajoocdata26.png)

Agora que seus esquemas XDM relacionais estão configurados e com dados sendo assimilados, você pode começar a usar esses dados para criar sua campanha orquestrada no próximo exercício.

## 3.8.1.2 assimilação de dados

Vá para **Conjuntos de dados**. Em seguida, você deve ver um conjunto de dados que foi criado para cada esquema criado.

![OC do AJO](./images/ajoocdata27.png)

Baixe o arquivo [data.zip](./assets/data.zip) na área de trabalho e descompacte-o.

![OC do AJO](./images/ajoocdata28.png)

Abra a pasta **dados**. Você deve ver um arquivo CSV para cada um dos esquemas criados. Agora é necessário fazer upload desses dados em cada conjunto de dados correspondente. Para esse laboratório, você fará isso fazendo um upload de arquivo local em cada conjunto de dados.

![OC do AJO](./images/ajoocdata29.png)

**`vangeluw_citisignal_products`**

Vá para **Fontes**, pesquise por `local` e clique em **Adicionar dados** em **Carregamento de Arquivo Local**.

![OC do AJO](./images/ajoocdatas10.png)

Habilite o alternador para **Habilitar captura de dados de alteração**.

Selecione o conjunto de dados `vangeluw_citisignal_products`.

Clique em **Next**.

![OC do AJO](./images/ajoocdatas9a.png)

Clique em **Escolher arquivos**. Selecione o arquivo **`citisignal_products.csv`** e clique em **abrir**.

![OC do AJO](./images/ajoocdatas9b.png)

Clique em **Avançar**

![OC do AJO](./images/ajoocdatas9c.png)

Clique em **Concluir**.

![OC do AJO](./images/ajoocdatas9d.png)

Após alguns minutos, você pode ver os dados sendo assimilados em seu conjunto de dados.

![OC do AJO](./images/ajoocdatas9e.png)

**`vangeluw_citisignal_product_bundles`**

Vá para **Fontes**, pesquise por `local` e clique em **Adicionar dados** em **Carregamento de Arquivo Local**.

![OC do AJO](./images/ajoocdatas10.png)

Habilite o alternador para **Habilitar captura de dados de alteração**.

Selecione o conjunto de dados `vangeluw_citisignal_product_bundles`.

Clique em **Next**.

![OC do AJO](./images/ajoocdatas10a.png)

Clique em **Escolher arquivos**. Selecione o arquivo **`citisignal_product_bundles.csv`** e clique em **abrir**.

![OC do AJO](./images/ajoocdatas10b.png)

Clique em **Avançar**

![OC do AJO](./images/ajoocdatas10c.png)

Clique em **Concluir**.

![OC do AJO](./images/ajoocdatas10d.png)

Após alguns minutos, você pode ver os dados sendo assimilados em seu conjunto de dados.

![OC do AJO](./images/ajoocdatas10e.png)

**`vangeluw_citisignal_product_relationships`**

Vá para **Fontes**, pesquise por `local` e clique em **Adicionar dados** em **Carregamento de Arquivo Local**.

![OC do AJO](./images/ajoocdatas10.png)

Habilite o alternador para **Habilitar captura de dados de alteração**.

Selecione o conjunto de dados `vangeluw_citisignal_product_relationships`.

Clique em **Next**.

![OC do AJO](./images/ajoocdatas11a.png)

Clique em **Escolher arquivos**. Selecione o arquivo **`citisignal_product_relationships.csv`** e clique em **abrir**.

![OC do AJO](./images/ajoocdatas11b.png)

Clique em **Avançar**

![OC do AJO](./images/ajoocdatas11c.png)

Clique em **Concluir**.

![OC do AJO](./images/ajoocdatas11d.png)

Após alguns minutos, você pode ver os dados sendo assimilados em seu conjunto de dados.

![OC do AJO](./images/ajoocdatas11e.png)

**`vangeluw_citisignal_accounts`**

Vá para **Fontes**, pesquise por `local` e clique em **Adicionar dados** em **Carregamento de Arquivo Local**.

![OC do AJO](./images/ajoocdatas10.png)

Habilite o alternador para **Habilitar captura de dados de alteração**.

Selecione o conjunto de dados `vangeluw_citisignal_accounts`.

Clique em **Next**.

![OC do AJO](./images/ajoocdatas12a.png)

Clique em **Escolher arquivos**. Selecione o arquivo **`citisignal_accounts.csv`** e clique em **abrir**.

![OC do AJO](./images/ajoocdatas12b.png)

Clique em **Avançar**

![OC do AJO](./images/ajoocdatas12c.png)

Clique em **Concluir**.

![OC do AJO](./images/ajoocdatas12d.png)

Após alguns minutos, você pode ver os dados sendo assimilados em seu conjunto de dados.

![OC do AJO](./images/ajoocdatas12e.png)

**`vangeluw_citisignal_recipients`**

Vá para **Fontes**, pesquise por `local` e clique em **Adicionar dados** em **Carregamento de Arquivo Local**.

![OC do AJO](./images/ajoocdatas10.png)

Habilite o alternador para **Habilitar captura de dados de alteração**.

Selecione o conjunto de dados `vangeluw_citisignal_recipients`.

Clique em **Next**.

![OC do AJO](./images/ajoocdatas13a.png)

Clique em **Escolher arquivos**. Selecione o arquivo **`citisignal_recipients.csv`** e clique em **abrir**.

![OC do AJO](./images/ajoocdatas13b.png)

Clique em **Avançar**

![OC do AJO](./images/ajoocdatas13c.png)

Clique em **Concluir**.

![OC do AJO](./images/ajoocdatas13d.png)

Após alguns minutos, você pode ver os dados sendo assimilados em seu conjunto de dados.

![OC do AJO](./images/ajoocdatas13e.png)

**`vangeluw_citisignal_mobile_subscriptions`**

Vá para **Fontes**, pesquise por `local` e clique em **Adicionar dados** em **Carregamento de Arquivo Local**.

![OC do AJO](./images/ajoocdatas10.png)

Habilite o alternador para **Habilitar captura de dados de alteração**.

Selecione o conjunto de dados `vangeluw_citisignal_mobile_subscriptions`.

Clique em **Next**.

![OC do AJO](./images/ajoocdatas14a.png)

Clique em **Escolher arquivos**. Selecione o arquivo **`citisignal_mobile_subscriptions.csv`** e clique em **abrir**.

![OC do AJO](./images/ajoocdatas14b.png)

Clique em **Avançar**

![OC do AJO](./images/ajoocdatas14c.png)

Clique em **Concluir**.

![OC do AJO](./images/ajoocdatas14d.png)

Após alguns minutos, você pode ver os dados sendo assimilados em seu conjunto de dados.

![OC do AJO](./images/ajoocdatas14e.png)

**`vangeluw_citisignal_internet_subscriptions`**

Vá para **Fontes**, pesquise por `local` e clique em **Adicionar dados** em **Carregamento de Arquivo Local**.

![OC do AJO](./images/ajoocdatas10.png)

Habilite o alternador para **Habilitar captura de dados de alteração**.

Selecione o conjunto de dados `vangeluw_citisignal_internet_subscriptions`.

Clique em **Next**.

![OC do AJO](./images/ajoocdatas15a.png)

Clique em **Escolher arquivos**. Selecione o arquivo **`citisignal_internet_subscriptions.csv`** e clique em **abrir**.

![OC do AJO](./images/ajoocdatas15b.png)

Clique em **Avançar**

![OC do AJO](./images/ajoocdatas15c.png)

Clique em **Concluir**.

![OC do AJO](./images/ajoocdatas15d.png)

Após alguns minutos, você pode ver os dados sendo assimilados em seu conjunto de dados.

![OC do AJO](./images/ajoocdatas15e.png)

**`vangeluw_citisignal_tv_subscriptions`**

Vá para **Fontes**, pesquise por `local` e clique em **Adicionar dados** em **Carregamento de Arquivo Local**.

![OC do AJO](./images/ajoocdatas10.png)

Habilite o alternador para **Habilitar captura de dados de alteração**.

Selecione o conjunto de dados `vangeluw_citisignal_tv_subscriptions`.

Clique em **Next**.

![OC do AJO](./images/ajoocdatas16a.png)

Clique em **Escolher arquivos**. Selecione o arquivo **`citisignal_tv_subscriptions.csv`** e clique em **abrir**.

![OC do AJO](./images/ajoocdatas16b.png)

Clique em **Avançar**

![OC do AJO](./images/ajoocdatas16c.png)

Clique em **Concluir**.

![OC do AJO](./images/ajoocdatas16d.png)

Após alguns minutos, você pode ver os dados sendo assimilados em seu conjunto de dados.

![OC do AJO](./images/ajoocdatas16e.png)

**`vangeluw_citisignal_equipment_subscriptions`**

Vá para **Fontes**, pesquise por `local` e clique em **Adicionar dados** em **Carregamento de Arquivo Local**.

![OC do AJO](./images/ajoocdatas10.png)

Habilite o alternador para **Habilitar captura de dados de alteração**.

Selecione o conjunto de dados `vangeluw_citisignal_equipment_subscriptions`.

Clique em **Next**.

![OC do AJO](./images/ajoocdatas17a.png)

Clique em **Escolher arquivos**. Selecione o arquivo **`citisignal_equipment_subscriptions.csv`** e clique em **abrir**.

![OC do AJO](./images/ajoocdatas17b.png)

Clique em **Avançar**

![OC do AJO](./images/ajoocdatas17c.png)

Clique em **Concluir**.

![OC do AJO](./images/ajoocdatas17d.png)

Após alguns minutos, você pode ver os dados sendo assimilados em seu conjunto de dados.

![OC do AJO](./images/ajoocdatas17e.png)

**`vangeluw_citisignal_mobile_usage_summary`**

Vá para **Fontes**, pesquise por `local` e clique em **Adicionar dados** em **Carregamento de Arquivo Local**.

![OC do AJO](./images/ajoocdatas10.png)

Habilite o alternador para **Habilitar captura de dados de alteração**.

Selecione o conjunto de dados `vangeluw_citisignal_mobile_usage_summary`.

Clique em **Next**.

![OC do AJO](./images/ajoocdatas18a.png)

Clique em **Escolher arquivos**. Selecione o arquivo **`citisignal_mobile_usage_summary.csv`** e clique em **abrir**.

![OC do AJO](./images/ajoocdatas18b.png)

Clique em **Avançar**

![OC do AJO](./images/ajoocdatas18c.png)

Clique em **Concluir**.

![OC do AJO](./images/ajoocdatas18d.png)

Após alguns minutos, você pode ver os dados sendo assimilados em seu conjunto de dados.

![OC do AJO](./images/ajoocdatas18e.png)

**`vangeluw_citisignal_internet_usage_summary`**

Vá para **Fontes**, pesquise por `local` e clique em **Adicionar dados** em **Carregamento de Arquivo Local**.

![OC do AJO](./images/ajoocdatas10.png)

Habilite o alternador para **Habilitar captura de dados de alteração**.

Selecione o conjunto de dados `vangeluw_citisignal_internet_usage_summary`.

Clique em **Next**.

![OC do AJO](./images/ajoocdatas19a.png)

Clique em **Escolher arquivos**. Selecione o arquivo **`citisignal_internet_usage_summary.csv`** e clique em **abrir**.

![OC do AJO](./images/ajoocdatas19b.png)

Clique em **Avançar**

![OC do AJO](./images/ajoocdatas19c.png)

Clique em **Concluir**.

![OC do AJO](./images/ajoocdatas19d.png)

Após alguns minutos, você pode ver os dados sendo assimilados em seu conjunto de dados.

![OC do AJO](./images/ajoocdatas19e.png)

**`vangeluw_citisignal_offers`**

Vá para **Fontes**, pesquise por `local` e clique em **Adicionar dados** em **Carregamento de Arquivo Local**.

![OC do AJO](./images/ajoocdatas10.png)

Habilite o alternador para **Habilitar captura de dados de alteração**.

Selecione o conjunto de dados `vangeluw_citisignal_offers`.

Clique em **Next**.

![OC do AJO](./images/ajoocdatas20a.png)

Clique em **Escolher arquivos**. Selecione o arquivo **`citisignal_offers.csv`** e clique em **abrir**.

![OC do AJO](./images/ajoocdatas20b.png)

Clique em **Avançar**

![OC do AJO](./images/ajoocdatas20c.png)

Clique em **Concluir**.

![OC do AJO](./images/ajoocdatas20d.png)

Após alguns minutos, você pode ver os dados sendo assimilados em seu conjunto de dados.

![OC do AJO](./images/ajoocdatas20e.png)

**`vangeluw_citisignal_offer_eligibility`**

Vá para **Fontes**, pesquise por `local` e clique em **Adicionar dados** em **Carregamento de Arquivo Local**.

![OC do AJO](./images/ajoocdatas10.png)

Habilite o alternador para **Habilitar captura de dados de alteração**.

Selecione o conjunto de dados `vangeluw_citisignal_offer_eligibility`.

Clique em **Next**.

![OC do AJO](./images/ajoocdatas21a.png)

Clique em **Escolher arquivos**. Selecione o arquivo **`citisignal_offer_eligibility.csv`** e clique em **abrir**.

![OC do AJO](./images/ajoocdatas21b.png)

Clique em **Avançar**

![OC do AJO](./images/ajoocdatas21c.png)

Clique em **Concluir**.

![OC do AJO](./images/ajoocdatas21d.png)

Após alguns minutos, você pode ver os dados sendo assimilados em seu conjunto de dados.

![OC do AJO](./images/ajoocdatas21e.png)

Todos os dados agora são assimilados. No próximo exercício, você começará a usar esses dados como parte de uma campanha orquestrada.

## Próximas etapas

Vá para [Criar sua campanha orquestrada](./ex2.md){target="_blank"}

Voltar para [Adobe Journey Optimizer: Campanhas](./ajocampaigns.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
