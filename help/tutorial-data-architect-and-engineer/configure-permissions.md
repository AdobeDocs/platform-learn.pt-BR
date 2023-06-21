---
title: Configurar permissões
seo-title: Configure permissions | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Configurar permissões
description: Nesta lição, você configurará as permissões de usuário do Adobe Experience Platform usando Adobe Admin Console.
role: Data Architect, Data Engineer
feature: Access Control
kt: 4348
thumbnail: 4348-configure-permissions.jpg
exl-id: ca01f99e-f10c-4bf0-bef2-b011ac29a565
source-git-commit: 35242a037bc79f18e90399c47e47064634d26a37
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 3%

---

# Configurar permissões

<!--30min-->

Nesta lição, você configurará as permissões de usuário do Adobe Experience Platform usando [!DNL Adobe's Admin Console] e a variável [!UICONTROL Permissões] na interface da Platform.

O controle de acesso é um recurso essencial de privacidade no Experience Platform e recomendamos limitar as permissões ao mínimo necessário para que as pessoas executem suas funções. Consulte a [Documentação de controle de acesso](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=pt-BR) para obter mais informações.

Os arquitetos de dados e engenheiros de dados são usuários avançados do Adobe Experience Platform e você precisará de muitas permissões para concluir este tutorial e, posteriormente, em seu trabalho diário. Os arquitetos de dados provavelmente estão envolvidos na administração de *outros usuários da Platform* em sua empresa, como profissionais de marketing, analistas e cientistas de dados. Ao concluir esta lição, pense em como você pode usar esses recursos para gerenciar outros usuários em sua empresa.

**Arquitetos de dados** geralmente, configure permissões para outros usuários fora deste tutorial.

>[!IMPORTANT]
>
>Um Administrador de sistema de produtos da Adobe Experience Cloud deve concluir algumas etapas desta lição, que é chamada nos cabeçalhos da seção. Se você não for um Administrador do sistema, entre em contato com um da sua empresa e solicite que eles concluam essas tarefas. Também há uma tarefa que eles precisam concluir durante o [Configurar o Console do desenvolvedor e o Postman](set-up-developer-console-and-postman.md) lição.

## Sobre o Admin Console

A variável [!DNL Admin Console] é a interface usada para administrar o acesso do usuário a todos os produtos da Adobe Experience Cloud. Para obter acesso à Platform, um usuário ou deve ser adicionado ao Admin Console e, em seguida, todos os itens de permissão granulares são gerenciados na tela Permissões do Adobe Experience Platform.


Este é um resumo rápido das funções existentes para a Platform:

* **Usuários** de um perfil de produto pode concluir tarefas na interface do usuário da Platform de acordo com as permissões atribuídas no perfil do produto.
* **Desenvolvedores** Você pode criar credenciais de API e projetos no Console do Adobe Developer para começar a usar a API Experience Platform
* **Administradores de produto** O pode adicionar usuários e desenvolvedores ao produto Adobe Experience Platform na Adobe Admin Console, bem como gerenciar o acesso granular dos usuários na tela Permissões da interface da Platform.
* **Administradores do sistema** O pode adicionar administradores de produtos e administrar essencialmente quaisquer permissões para todos os produtos da Adobe Experience Cloud.

## Adicionar um usuário e desenvolvedor à `AEP-Default-All-Users` perfil de produto (requer um administrador do sistema ou administrador do produto)

Neste exercício, você, um Administrador do sistema ou um Administrador de produto adicionará você como Usuário e Desenvolvedor no produto Adobe Experience Platform do Adobe Admin Console.

>[!NOTE]
>
>Se você for um Administrador do Sistema que está ajudando um colega a fazer este tutorial, considere adicionar seu colega como um *Administrador do produto* para Adobe Experience Platform. Como um Administrador de produto, ele poderá concluir essas etapas por conta própria e administrar outros usuários do Experience Platform no futuro.

Para adicionar o participante do tutorial como um [!UICONTROL Usuário] e [!UICONTROL Desenvolvedor]:

1. Faça logon na [Adobe Admin Console](https://adminconsole.adobe.com)
1. Selecionar **[!UICONTROL Produtos]** na navegação superior
1. Selecionar **Adobe Experience Platform**
   ![Selecionar Adobe Experience Platform](assets/adminconsole-experiencePlatform.png)
1. Você já pode ter vários perfis na sua instância do Experience Platform. Selecione o `AEP-Default-All-Users` perfil
   ![Selecione Adicionar novo perfil](assets/adminconsole-newProfile.png)

1. Vá para a **[!UICONTROL Usuários]** guia
1. Selecione o **[!UICONTROL Adicionar usuário]** botão
   ![Selecione Adicionar usuário](assets/adminconsole-addUser.png)
1. Conclua o fluxo de trabalho para adicionar o participante do tutorial como usuário ao perfil do produto

1. Vá para a **[!UICONTROL Desenvolvedores]** guia
1. Selecione o **[!UICONTROL Adicionar desenvolvedor]** botão
   ![Selecione Adicionar usuário](assets/adminconsole-addDeveloper.png)
1. Conclua o fluxo de trabalho para adicionar o participante do tutorial como desenvolvedor ao perfil do produto


## Adicionar uma função no Adobe Experience Platform (requer um administrador do sistema ou administrador de produto)

Permissões granulares para o Experience Platform são gerenciadas na tela Permissões da interface da Platform. Somente administradores de sistema e de produtos têm acesso a essa tela. Portanto, se você não tiver privilégios de administrador, precisará da assistência de alguém que tiver.

As permissões são gerenciadas em Funções. Crie uma função para o tutorial:

1. Efetue logon no [Adobe Experience Platform](https://platform.adobe.com)
1. Selecionar **[!UICONTROL Permissões]** na navegação à esquerda, que direcionará você para a [!UICONTROL Funções] tela
1. Selecionar **[!UICONTROL Criar função]**

   ![Criar uma função no Experience Platform](assets/permissions-addRole.png)
1. Nomear a função `Luma Tutorial Platform` (adicione o nome do participante do tutorial ao final, se várias pessoas da sua empresa estiverem utilizando este tutorial) e selecione **[!UICONTROL Confirmar o]**

   ![Criar uma função no Experience Platform](assets/permissions-nameRole.png)


1. Adicione todos os itens de permissão para os seguintes recursos usando  **[!UICONTROL +]** e **[!UICONTROL Adicionar tudo]**:

   1. Modelagem de dados
   1. Gerenciamento de dados
   1. Gerenciamento de perfil
   1. Gerenciamento de identidade
   1. Administração de sandbox
   1. Serviço de query
   1. Coleção de dados
   1. Governança de dados
   1. Painéis
   1. Alertas

      ![Adicionar itens de permissão](assets/permissions-addPermissionItems.png)

1. Em Assimilação de dados, adicione os itens de permissão Gerenciar fontes e Exibir fontes.

1. Depois de adicionar todos os itens de permissão, selecione o botão Salvar
   ![Salvar itens de permissão](assets/permissions-savePermissions.png)

Você fará algumas pequenas atualizações nessa função após a [Criar uma sandbox](create-a-sandbox.md) e [Configurar o Console do desenvolvedor e o Postman](set-up-developer-console-and-postman.md) lições.

## Criar um perfil de produto de Coleção de dados (requer um administrador do sistema ou administrador de produto)

Neste exercício, você ou um Administrador do sistema da sua empresa criará um perfil de produto para a Coleção de dados (anteriormente conhecida como Adobe Experience Platform Launch) e o adicionará como administrador de perfil de produto.

>[!NOTE]
>
>Se você for um Administrador do sistema auxiliando um colega neste tutorial, considere adicioná-los como um *Administrador do produto* para Coleta de dados. Como administrador de produto, ele poderá concluir essas etapas por conta própria e administrar outros usuários da Coleção de dados no futuro.

Para criar o perfil de produto:

1. No [!DNL Adobe Admin Console] vá para o produto Coleta de dados da Adobe Experience Platform
1. Adicione um novo perfil chamado `Luma Tutorial Data Collection` (adicione o nome do participante do tutorial ao final se várias pessoas da sua empresa estiverem utilizando este tutorial)
1. Desative o **[!UICONTROL Propriedades]** > **[!UICONTROL Incluir automaticamente]** configuração
1. Não atribuir propriedades ou permissões neste momento
1. Adicionar o participante do tutorial como um administrador deste perfil

Após concluir essas etapas, você deverá ver que a variável `Luma Tutorial Data Collection` O perfil do está configurado com um administrador.
![Perfil de coleção de dados criado](assets/adminconsole-dc-profileCreated.png)

## Configurar o perfil de produto da coleção de dados

Agora que você é um administrador do `Luma Tutorial Data Collection` perfil de produto, é possível configurar as permissões e funções necessárias para concluir o tutorial.

### Adicionar permissões

Agora, você adicionará os itens de permissão individuais ao perfil:

1. No [Adobe Admin Console](https://adminconsole.adobe.com), vá para **[!UICONTROL Produtos]** > **[!UICONTROL Coleta de dados]**
1. Abra o `Luma Tutorial Data Collection` perfil
1. Vá para a **[!UICONTROL Permissões]** guia
1. Abertura **[!UICONTROL Plataformas]**
1. Verifique se todas as plataformas disponíveis estão selecionadas (você pode ver opções diferentes com base na sua licença)
1. **[!UICONTROL Salve]** quaisquer alterações
   ![Adicionar plataformas](assets/adminconsole-launch-addPlatforms.png)
1. Abertura **[!UICONTROL Propriedades]**
1. Verifique se **[!UICONTROL Incluir automaticamente]** Ativar/desativar está Desativado para que você não tenha acesso a nenhuma propriedade (adicionaremos uma mais tarde)
1. **[!UICONTROL Salve]** quaisquer alterações
   ![Remover propriedades](assets/adminconsole-launch-removeProperties.png)
1. Abertura **[!UICONTROL Direitos de propriedade]**
1. Selecionar **[!UICONTROL Adicionar tudo]** para adicionar todas as permissões de propriedade
1. **[!UICONTROL Salvar]**
   ![Remover propriedades](assets/adminconsole-launch-addPropertyRights.png)
1. Abertura **[!UICONTROL Direitos da empresa]**
1. Adicionar **[!UICONTROL Gerenciar propriedades]**
1. Selecione **[!UICONTROL Salvar]**
   ![Remover propriedades](assets/adminconsole-launch-companyRights.png)


### Adicionar a si mesmo como usuário

Agora, adicione a si mesmo como usuário ao perfil da Coleção de dados:

1. Vá para a **[!UICONTROL Usuários]** guia
1. Selecione o **[!UICONTROL Adicionar usuário]** botão
   ![Selecione Adicionar usuário](assets/adminconsole-launch-addUser.png)
1. Conclua o fluxo de trabalho para adicionar a si mesmo como usuário ao perfil do produto

Não é necessário adicionar a si mesmo como Desenvolvedor da Coleção de dados.

Agora você tem quase todas as permissões necessárias para concluir o tutorial. Haverá apenas mais dois ajustes que você fará dentro do [!DNL Adobe Admin Console], incluindo um depois de você [criar uma sandbox](create-a-sandbox.md)!
