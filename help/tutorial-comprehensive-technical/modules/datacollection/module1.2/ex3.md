---
title: Foundation - Assimilação de dados - Configurar conjuntos de dados
description: Foundation - Assimilação de dados - Configurar conjuntos de dados
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 7%

---

# 1.2.3 Configurar conjuntos de dados

Neste exercício, você configurará os conjuntos de dados necessários para capturar e armazenar informações de perfil e comportamento do cliente. Cada conjunto de dados criado nesse recurso usará um dos esquemas criados na etapa anterior.

## Story

Após definir qual é a resposta às perguntas **Quem é esse cliente?** e **O que este cliente faz?** deve ser semelhante a, agora é necessário criar um compartimento que use essas informações para receber e validar dados enviados para a Adobe Experience Platform.

## 1.2.3.1 - Criar conjuntos de dados

Agora é necessário criar dois conjuntos de dados:

- 1 conjunto de dados para capturar as informações que respondem à **Quem é este cliente?** - pergunta.
- 1 conjunto de dados para capturar as informações que respondem ao **O que este cliente faz?** - pergunta.

Faça logon no Adobe Experience Platform acessando esta URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, você precisa selecionar uma **[!UICONTROL sandbox]**. A sandbox a ser selecionada é chamada ``--module2sandbox--``. Você pode fazer isso clicando no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. Depois de selecionar a [!UICONTROL sandbox] apropriada, você verá a alteração da tela e agora estará na [!UICONTROL sandbox] dedicada.

![Assimilação de dados](./images/sb1.png)

No Adobe Experience Platform, clique em **[!UICONTROL Conjuntos de dados]** no menu no lado esquerdo da tela.  Você verá isto:

![Assimilação de dados](./images/menudatasets.png)

Vamos começar criando o conjunto de dados para capturar as informações de registro do site.

Você deve criar um novo conjunto de dados. Para criar um novo conjunto de dados, clique no botão **[!UICONTROL + Criar conjunto de dados]**.

![Assimilação de dados](./images/createdataset.png)

Depois de clicar no botão **[!UICONTROL + Criar Conjunto de Dados]**, você verá a tela a seguir.

![Assimilação de dados](./images/datasetsetup.png)

Você precisa definir um conjunto de dados a partir do esquema definido na etapa anterior. Clique na opção **[!UICONTROL Criar conjunto de dados a partir do esquema]**.

![Assimilação de dados](./images/datasetfromschema.png)

Na próxima tela, você deve selecionar o esquema criado em 1, `--aepUserLdap-- - Demo System - Profile Schema for Website`.

![Assimilação de dados](./images/schemaselection.png)

Depois de selecionar o esquema, clique em **[!UICONTROL Avançar]** para continuar.

![Assimilação de dados](./images/next.png)

Vamos nomear seu conjunto de dados.

Como o nome do nosso conjunto de dados, use este:

`--aepUserLdap-- - Demo System - Profile Dataset for Website`

Por exemplo, para ldap **[!UICONTROL vangeluw]**, este deve ser o nome do esquema:

**[!UICONTROL vangeluw - Sistema de Demonstração - Conjunto de Dados de Perfil para Site]**

Isso deve dar a você algo como isso:

![Assimilação de dados](./images/datasetname.png)

Clique em **[!UICONTROL Concluir]** para concluir a configuração do conjunto de dados.

![Assimilação de dados](./images/finish.png)

Agora você verá isto:

![Assimilação de dados](./images/dsoverview1.png)

Volte para a visão geral de [!UICONTROL Conjuntos de dados]. Agora você verá o conjunto de dados criado aparecer na visão geral.

![Assimilação de dados](./images/dsoverview2.png)

Em seguida, você configurará um segundo conjunto de dados para capturar as interações do site.

Você deve criar um novo conjunto de dados. Para criar um novo conjunto de dados, clique no botão **[!UICONTROL + Criar conjunto de dados]**.

![Assimilação de dados](./images/createdataset.png)

Depois de clicar no botão **[!UICONTROL + Criar Conjunto de Dados]**, você verá a tela a seguir.

![Assimilação de dados](./images/datasetsetup.png)

Você precisa definir um conjunto de dados a partir do esquema definido na etapa anterior. Clique na opção **[!UICONTROL Criar conjunto de dados a partir do esquema]**.

![Assimilação de dados](./images/datasetfromschema.png)

Na próxima tela, você deve selecionar o esquema criado na versão 2.2, `--aepUserLdap-- - Demo System - Event Schema for Website`.

![Assimilação de dados](./images/schemaselectionee.png)

Depois de selecionar o esquema, clique em **[!UICONTROL Avançar]** para continuar.

![Assimilação de dados](./images/next.png)

Vamos nomear seu conjunto de dados.

Como o nome do nosso conjunto de dados, usaremos:

`--aepUserLdap-- - Demo System - Event Dataset for Website`

Por exemplo, para ldap **[!UICONTROL vangeluw]**, este deve ser o nome do esquema:

**[!UICONTROL vangeluw - Sistema de Demonstração - Conjunto de Dados de Evento para Site]**

Isso deve dar a você algo como isso:

![Assimilação de dados](./images/datasetnameee.png)

Clique em **[!UICONTROL Concluir]** para concluir a configuração do conjunto de dados.

![Assimilação de dados](./images/finish.png)

Você verá isto:

![Assimilação de dados](./images/finish1.png)

Volte para a tela de visão geral [!UICONTROL Conjuntos de dados].

![Assimilação de dados](./images/datasetsoverview.png)

Agora é necessário ativar seus conjuntos de dados para fazer parte do Perfil de cliente em tempo real da Adobe Experience Platform.

Abra seu conjunto de dados `--aepUserLdap--` - Sistema de demonstração - Conjunto de dados do perfil para o site clicando nele.

Localize o ícone de alternância [!UICONTROL Perfil] no lado direito da tela.

![Assimilação de dados](./images/ds1.png)

Clique no botão de alternância [!UICONTROL Perfil] para habilitar este conjunto de dados para [!UICONTROL Perfil].

![Assimilação de dados](./images/ds2.png)

Clique em **[!UICONTROL Habilitar]**.

![Assimilação de dados](./images/ds3.png)

Seu conjunto de dados agora está habilitado para [!UICONTROL Perfil].

Retorne à visão geral dos conjuntos de dados e abra seu conjunto de dados `--aepUserLdap-- - Demo System - Event Dataset` para o Site clicando nele.

Localize o ícone de alternância [!UICONTROL Perfil] no lado direito da tela.

![Assimilação de dados](./images/ds4.png)

Clique no botão de alternância [!UICONTROL Perfil] para habilitar [!UICONTROL Perfil].

![Assimilação de dados](./images/ds2.png)

Clique em **[!UICONTROL Habilitar]**.

![Assimilação de dados](./images/ds5.png)

Seu conjunto de dados agora está habilitado para [!UICONTROL Perfil].

Próxima etapa: [1.2.4 Assimilação de dados de fontes offline](./ex4.md)

[Voltar ao módulo 1.2](./data-ingestion.md)

[Voltar a todos os módulos](../../../overview.md)
