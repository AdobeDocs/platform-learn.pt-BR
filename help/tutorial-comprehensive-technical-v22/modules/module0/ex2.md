---
title: Introdução - Use o sistema de demonstração ao lado da configuração da propriedade do Launch
description: Introdução - Use o sistema de demonstração ao lado da configuração da propriedade do Launch
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 9c0eddf5-bfd7-4e7a-a8e2-ccd55ccd966d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# 0.2 Usar o sistema de demonstração Ao lado da configuração da propriedade do cliente Adobe Experience Platform Data Collection

Depois de se inscrever no Tutorial técnico abrangente do Adobe Experience Platform, há um processo automatizado que fornecerá acesso ao Demo System, para que você possa acessar e executar a configuração abaixo.

Depois de ter acesso ao Demo System, continue com as etapas abaixo.

Ir para [https://dashboard.adobedemo.com/](https://dashboard.adobedemo.com/). Selecione a sandbox e clique em **Configuração rápida**.

![DSN](./images/dsnh1.png)

Você verá isto:

![DSN](./images/dsnhome.png)

Em **Geral** - **Ambiente**, selecione a instância do Adobe Experience Platform e a sandbox, neste caso:

- **Experience Platform International**
- **aepenablementfy22**
- Configuração: selecione **Global v2.0**

![DSN](./images/dsn1.png)

Em seguida, selecione a predefinição **Ativar usuário** e clique em **Iniciar**.

![DSN](./images/dsn2.png)

No pop-up, insira um nome para a propriedade Coleta de dados. Use esta convenção de nomenclatura: **Sistema de demonstração (DD/MM/AAAA)**. FYI: seu LDAP será anexado automaticamente, você não precisa adicioná-lo sozinho.

Clique em **Start**.

![DSN](./images/dsn3.png)

Em seguida, você verá esse pop-up, que mostra o progresso ao criar seu site e projetos de aplicativos móveis e suas propriedades de coleta de dados.

![DSN](./images/dsn4.png)

Depois que o processo de configuração rápida for concluído, você terá:

- 1 Projeto Web Retail, que permite o uso de um site de demonstração com a marca de demonstração Luma
- 1 Projeto de varejo móvel, que permite usar um aplicativo de demonstração para dispositivos móveis com a marca de demonstração Luma
- 1 Projeto CX App Retail, que possibilita o uso de um call center e de um aplicativo de clienteling com a marca de demonstração Luma
- 1 Propriedade Data Collection para web, que você usará para coletar dados do site
- 1 Propriedade Data Collection para dispositivos móveis, que você usará para coletar dados do aplicativo móvel

![DSN](./images/dsn5.png)

Mantenha essa tela aberta, conforme necessário, nas próximas etapas.

Próxima etapa: [0.3 Criar o conjunto de dados](./ex3.md)

[Voltar ao Módulo 0](./getting-started.md)

[Voltar para todos os módulos](./../../overview.md)
