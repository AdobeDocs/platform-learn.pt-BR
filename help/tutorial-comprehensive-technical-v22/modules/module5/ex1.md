---
title: Serviços inteligentes - Preparação de dados do Customer AI (Assimilar)
description: AI do cliente - Preparação de dados (Assimilar)
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 60996e70-b033-4932-b614-b37014232f6e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 3%

---

# 5.1 AI do cliente - Preparação de dados (Assimilar)

Para que os Serviços inteligentes descubram insights de seus dados de eventos de marketing, os dados devem ser semanticamente enriquecidos e mantidos em uma estrutura padrão. Os Serviços inteligentes usam esquemas Adobe Experience Data Model (XDM) para alcançar isso.
Especificamente, todos os conjuntos de dados que são usados nos Serviços inteligentes devem estar em conformidade com a **Evento de experiência do consumidor** Esquema XDM.

## 5.1.1 Criar esquema

Neste exercício, você criará um schema que contenha a variável **Mistura de evento de experiência do consumidor**, que é exigido pela **Customer AI** Serviço inteligente.

Faça logon no Adobe Experience Platform acessando este URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer logon, você será direcionado para a página inicial do Adobe Experience Platform.

![Assimilação de dados](../module2/images/home.png)

Antes de continuar, é necessário selecionar um **sandbox**. A sandbox a ser selecionada é chamada de ``--module10sandbox--``. Você pode fazer isso clicando no texto **[!UICONTROL Produto de produção]** na linha azul na parte superior da tela. Depois de selecionar a sandbox apropriada, você verá a tela mudar e agora estará na sandbox dedicada.

![Assimilação de dados](../module2/images/sb1.png)

No menu esquerdo, clique em **Esquemas** e ir para **Procurar**. Clique em **Criar esquema**.

![Criar novo schema](./images/create-schema-button.png)

Na janela pop-up , selecione **ExperiênciaEvento XDM**.

![Criar novo schema](./images/xdmee.png)

Você verá isso.

![Criar novo schema](./images/xdmee1.png)

Pesquise e selecione o seguinte **Misturas** para adicionar a este Esquema:

- Evento de experiência do consumidor

   ![Novo esquema CEE](./images/cee.png)

- Detalhes da ID de usuário final

   ![Novo esquema CEE](./images/identitymap.png)

Clique em **Adicionar grupos de campos**.

![Definição de chave de identidade](./images/addmixin.png)

Você verá isso. Selecione a mistura **Detalhes da ID de usuário final**.

![Criar novo schema](./images/eui1.png)

Navegar até o campo **endUserIDs._experience.emailid.id**.

![Criar novo schema](./images/eui2.png)

No menu à direita do campo **endUserIDs._experience.emailid.id**, role para baixo e marque a caixa de seleção para **Identidade**, marque a caixa de seleção de **Identidade principal** e selecione o **Namespace de identidade** de **Email**.

![Criar novo schema](./images/eui3.png)

Navegar até o campo **endUserIDs._experience.mcid.id**. Marque a caixa de seleção para **Identidade** e selecione o **Namespace de identidade** de **ECID**. Clique em **Aplicar**.

![Criar novo schema](./images/eui4.png)

Dê um nome ao esquema agora.

Como o nome do nosso schema, você usará isto:

- `--demoProfileLdap-- - Demo System - Customer Experience Event`

Como exemplo, para ldap **vangeluco**, esse deve ser o nome do schema:

- **vangeluw - Sistema de demonstração - Evento de experiência do cliente**

Isso deveria te dar algo assim. Clique no botão **+ Adicionar** botão para adicionar novo **Misturas**.

![Criar novo schema](./images/xdmee2.png)

Selecione o nome do esquema. Agora, você deve ativar seu esquema para **Perfil**, clicando no botão **Perfil** alternar.

![Criar novo schema](./images/xdmee3.png)

Você verá isso. Clique em **Habilitar**.

![Criar novo schema](./images/xdmee4.png)

Você deveria ter isso agora. Clique em **Salvar** para salvar o esquema.

![Criar novo schema](./images/xdmee5.png)

## 5.1.2 Criar conjunto de dados

No menu esquerdo, clique em **Conjuntos de dados** e ir para **Procurar**. Clique em **Criar conjunto de dados**.

![Conjunto de dados](./images/createds.png)

Clique em **Criar conjunto de dados a partir do esquema**.

![Conjunto de dados](./images/createdatasetfromschema.png)

Na próxima tela, selecione o conjunto de dados criado no exercício anterior, que é nomeado como **[!UICONTROL ldap - Sistema de demonstração - Evento de experiência do cliente]**. Clique em **Próximo**.

![Conjunto de dados](./images/createds1.png)

Como nome para o conjunto de dados, use `--demoProfileLdap-- - Demo System - Customer Experience Event Dataset`. Clique em **Concluir**.

![Conjunto de dados](./images/createds2.png)

Seu conjunto de dados foi criado. Ative o **Perfil** alternar.

![Conjunto de dados](./images/createds3.png)

Clique em **Habilitar**.

![Conjunto de dados](./images/createds4.png)

Agora você deve ter o seguinte:

![Conjunto de dados](./images/createds5.png)

Agora você está pronto para começar a assimilar dados de Evento de experiência do consumidor e começar a usar o serviço de IA do cliente.

## 5.1.3 Baixar dados de teste do Evento de experiência

Uma vez **Esquema** e **Conjunto de dados** estiver configurado, agora você está pronto para assimilar dados de Evento de experiência. Como o Customer AI requer dados em **2 trimestres, pelo menos**, será necessário assimilar dados preparados externamente.

Os dados preparados para os eventos de experiência devem estar em conformidade com os requisitos e o schema da variável [Mistura XDM do Evento de experiência do consumidor](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md).

Baixe o arquivo que contém os dados de amostra deste local: [https://dashboard.adobedemo.com/data](https://dashboard.adobedemo.com/data). Clique no botão **Baixar** botão.

![Conjunto de dados](./images/dsn1.png)

Agora você baixou um arquivo chamado **retail-v1-dec2020-xl.json.zip**. Coloque o arquivo na área de trabalho do seu computador e descompacte-o. Em seguida, você verá um arquivo chamado **retail-v1.json**. Você precisará deste arquivo no próximo exercício.

![Conjunto de dados](./images/ingest.png)

## 5.1.4 Assimilar dados do teste de evento de experiência

No Adobe Experience Platform, acesse **Conjuntos de dados** e abra seu conjunto de dados, que é nomeado como **[!UICONTROL ldap - Sistema de demonstração - Conjunto de dados do evento da experiência do cliente]**.

![Conjunto de dados](./images/ingest1.png)

No conjunto de dados, clique em **Escolher arquivos** para adicionar dados.

![Conjunto de dados](./images/ingest2.png)

Na janela pop-up , selecione o arquivo **retail-v1.json** e clique em **Abrir**.

![Conjunto de dados](./images/ingest3.png)

Você verá os dados que estão sendo importados e um novo lote será criado no **Carregamento** estado. Não saia desta página até que o arquivo seja carregado.

![Conjunto de dados](./images/ingest4.png)

Depois que o arquivo for carregado, você verá a alteração do status do lote de **Carregamento** para **Processamento**.

![Conjunto de dados](./images/ingest5.png)

A inserção e o processamento dos dados podem levar de 10 a 20 minutos.

Quando a assimilação de dados for bem-sucedida, o status do lote será alterado para **Sucesso**.

![Conjunto de dados](./images/ingest7.png)

![Conjunto de dados](./images/ingest8.png)

Próxima etapa: [5.2 Customer AI - Criar uma nova instância (Configurar)](./ex2.md)

[Voltar ao Módulo 5](./intelligent-services.md)

[Voltar para todos os módulos](./../../overview.md)
