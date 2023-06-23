---
title: Configurar o Console do desenvolvedor e o Postman
seo-title: Set up Developer Console and Postman | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Configurar o Console do desenvolvedor e o Postman
description: Nesta lição, você configurará um projeto no Console do Adobe Developer e fornecerá [!DNL Postman] Coleções para que você possa começar a usar as APIs da Platform.
role: Data Architect, Data Engineer
feature: API
jira: KT-4348
thumbnail: 4348-set-up-developer-console-and-postman.jpg
exl-id: 72b541fa-3ea1-4352-b82b-c5b79ff98491
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 1%

---

# Configurar o Console do desenvolvedor e [!DNL Postman]

<!--30min-->

Nesta lição, você configurará um projeto no Console do Adobe Developer e baixará [!DNL Postman] coleções para que você possa começar a usar as APIs da Platform.

Para concluir os exercícios de API neste tutorial, [baixe o aplicativo Postman para o seu sistema operacional.](https://www.postman.com/downloads/) Embora não seja necessário para usar APIs de Experience Platform, o Postman facilita os fluxos de trabalho de API, e o Adobe Experience Platform fornece dezenas de coleções do Postman para ajudar você a executar chamadas de API e saber como elas operam. O restante deste tutorial presume algum conhecimento prático do Postman. Para obter ajuda, consulte o [Documentação do Postman](https://learning.postman.com/).

A Platform é criada como API. Embora as opções de interface também existam para todas as principais tarefas, você pode querer usar a API da plataforma em algum momento. Por exemplo, para assimilar dados, mover itens entre sandboxes, automatizar tarefas de rotina ou usar novos recursos da Platform antes que a interface do usuário tenha sido criada.

**Arquitetos de dados** e **Engenheiros de dados** pode precisar usar a API da plataforma fora deste tutorial.

## Permissões necessárias

No [Configurar permissões](configure-permissions.md) você configura todos os controles de acesso necessários para concluir esta lição.

<!--
* Permission item Sandboxes > `Luma Tutorial`
* Developer-role access to the `Luma Tutorial Platform` product profile
-->

## Configurar o console do Adobe Developer

O Adobe Developer Console é o destino do desenvolvedor para acessar APIs e SDKs do Adobe, ouvir eventos quase em tempo real, executar funções no tempo de execução ou criar plug-ins ou aplicativos do App Builder. Você o usará para acessar a API Experience Platform. Para obter mais detalhes, consulte [Documentação do console do Adobe Developer](https://www.adobe.io/apis/experienceplatform/console/docs.html)

1. Crie uma pasta no computador local chamada `Luma Tutorial Assets` para arquivos usados no tutorial.

1. Abra o [Console do Adobe Developer](https://console.adobe.io){target="_blank"}

1. Faça logon e confirme se você está na organização correta

1. Selecionar **[!UICONTROL Criar novo projeto]** in [!UICONTROL Início rápido] menu.

   ![Criar novo projeto](assets/adobeio-createNewProject.png)


1. No projeto recém-criado, selecione a variável **[!UICONTROL Editar Projeto]** botão
1. Altere o **[!UICONTROL Título do projeto]** para `Luma Tutorial API Project` (adicione seu nome ao final se várias pessoas da sua empresa estiverem fazendo este tutorial)
1. Selecione **[!UICONTROL Salvar]**

   ![Configuração da API do projeto do console do Adobe Developer](assets/adobeio-renameProject.png)


1. Selecionar **[!UICONTROL Adicionar API]**

   ![Configuração da API do projeto do console do Adobe Developer](assets/adobeio-addAPI.png)

1. Filtrar a lista selecionando **[!UICONTROL Adobe Experience Platform]**

1. Na lista de APIs disponíveis, selecione **[!UICONTROL API EXPERIENCE PLATFORM]** e selecione **[!UICONTROL Próxima]**.

   ![Configuração da API do projeto do console do Adobe Developer](assets/adobeio-AEPAPI.png)

1. Selecionar **[!UICONTROL Servidor OAuth para servidor]** como credencial e selecione **[!UICONTROL Próxima]**.
   ![Selecionar servidor OAuth para servidor](assets/adobeio-choose-auth.png)

1. Selecione o `AEP-Default-All-Users` perfil do produto e selecione **[!UICONTROL Salvar API configurada]**

   ![Selecionar perfil de produto](assets/adobeio-selectProductProfile.png)

1. Agora o projeto do Developer Console foi criado.

1. No **[!UICONTROL Experimente]** da página, selecione **[!UICONTROL Baixar para Postman]** e selecione **[!UICONTROL Servidor OAuth para servidor]** para baixar o [!DNL Postman] arquivo json do ambiente. Salve o `oauth_server_to_server.postman_environment.json` no seu `Luma Tutorial Assets` pasta.


   ![Configuração da API do projeto do console do Adobe Developer](assets/adobeio-io-api.png)

## Faça um administrador do sistema adicionar a credencial de API à função

Para usar a credencial de API para interagir com o Experience Platform, será necessário que um administrador do sistema atribua as credenciais de API à função criada na lição anterior.  Caso você não seja um Administrador do sistema, envie-os:

1. A variável [!UICONTROL Nome] da sua credencial de API (`Credential in Luma Tutorial API Project`)
1. A variável [!UICONTROL Email da conta técnica] da sua credencial (isso ajudará o Administrador do sistema a encontrar a credencial)

   ![[!UICONTROL Nome] e [!UICONTROL Email da conta técnica] da sua credencial](assets/postman-credentialDetails.png)

Estas são as instruções para o Administrador do sistema:

1. Efetue logon no [Adobe Experience Platform](https://platform.adobe.com)
1. Selecionar **[!UICONTROL Permissões]** na navegação à esquerda, que direcionará você para a [!UICONTROL Funções] tela
1. Abra o `Luma Tutorial Platform` função
   ![Abrir a função](assets/postman-openRole.png)
1. Selecione o **[!UICONTROL Credenciais da API]** guia
1. Selecionar **[!UICONTROL Adicionar credenciais de API]**
   ![Adicionar credencial](assets/postman-addCredential.png)
1. Localize o `Credential in Luma Tutorial API Project` credencial, filtragem com o [!UICONTROL Email da conta técnica] fornecido pelo participante do tutorial, se a lista for longa
1. Selecionar a credencial
1. Selecione **[!UICONTROL Salvar]**


   ![Adicionar credencial](assets/postman-findCredential.png)

## Configurar o Postman

>[!CAUTION]
>
>A interface do Postman é atualizada regularmente. As capturas de tela neste tutorial foram feitas com o Postman v10.15.1 para Mac, mas as opções de interface podem ter sido alteradas.


1. Baixar e instalar [[!DNL Postman]](https://www.postman.com/downloads/)
1. Abertura [!DNL Postman] e criar um espaço de trabalho
   ![Importar ambiente](assets/postman-createWorkspace.png)

1. Importe o arquivo de ambiente json baixado, `oauth_server_to_server.postman_environment.json`
   ![Importar ambiente](assets/postman-importEnvironment.png)
1. Entrada [!DNL Postman], selecione seu ambiente na lista suspensa

1. Selecione o ícone para exibir as variáveis de ambiente:

   ![Alterar ambiente](assets/postman-changeEnvironment.png)


### Adicionar o nome da sandbox e a ID do locatário

A variável `SANDBOX_NAME` e `TENANT_ID` e `CONTAINER_ID` As variáveis não são incluídas na exportação do console do Adobe Developer, portanto, as adicionamos manualmente:

1. Entrada [!DNL Postman], abra o **Variáveis de ambiente**
1. Selecione o **Editar** link à direita do nome do ambiente
1. No **Adicionar novo campo de variável**, insira `SANDBOX_NAME`
1. Em ambos os campos de valor, informe `luma-tutorial`, o nome que demos à nossa sandbox na lição anterior. Se você usou um nome diferente para sua sandbox, por exemplo, luma-tutorial-ignatiusjreilly, certifique-se de usar esse valor.
1. No **Adicionar novo campo de variável**, insira `TENANT_ID`
1. Alterne para o navegador da Web e procure a ID do locatário da sua empresa acessando a interface do Experience Platform e extraindo a parte do URL *após o sinal @*. Por exemplo, minha id de locatário é `techmarketingdemos` mas o seu é diferente:

   ![Obter a ID do locatário do URL da interface da plataforma](assets/postman-getTenantId.png)

1. Copie esse valor e retorne ao campo [!DNL Postman] Tela Gerenciar ambientes
1. Cole sua ID do locatário nos dois campos de valor
1. No **Adicionar novo campo de variável**, insira `CONTAINER_ID`
1. Enter `global` em ambos os campos de valor

   >[!NOTE]
   >
   >`CONTAINER_ID` é um campo cujo valor alteramos várias vezes durante o tutorial. Quando `global` for usada, a API interagirá com elementos fornecidos pelo Adobe na sua conta da Platform. Quando `tenant` for usada, a API interagirá com seus próprios elementos personalizados.

1. Selecione **Salvar**

   ![Campos SANDBOX_NAME, TENANT_ID e CONTAINER_ID adicionados como variáveis de ambiente](assets/postman-addEnvFields.png)



## Fazer chamadas de API

### Recuperar um token de acesso

O Adobe fornece um conjunto avançado de [!DNL Postman] coleções para ajudar a explorar a API do Experience Platform. Essas coleções estão no [GitHub de exemplos do Adobe Experience Platform Postman](https://github.com/adobe/experience-platform-postman-samples). Você deve marcar este repositório como você usará isso várias vezes neste tutorial e posteriormente ao implementar o Experience Platform para sua própria empresa.

A primeira coleção funciona com as APIs do Adobe Identity Management Service (IMS). É uma maneira conveniente de recuperar um token de acesso de dentro do Postman.

Para gerar o token de acesso:

1. Baixe o [Coleção de APIs de serviço do Identity Management](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) ao seu `Luma Tutorial Assets` pasta
1. Importar a coleção para [!DNL Postman]
1. Selecionar a solicitação **oAuth: solicitar token de acesso** solicitar e selecionar **Enviar**
1. Você deve obter um `200 OK` resposta com um token de acesso na resposta

   ![Solicitar os tokens](assets/postman-requestToken.png)

1. O token de acesso deve ser armazenado automaticamente como o **ACCESS_TOKEN** variável de ambiente do [!DNL Postman] ambiente.

   ![Postman](assets/postman-config.png)


### Interagir com uma API da plataforma

Agora vamos fazer uma chamada à API da plataforma para confirmar se configuramos tudo corretamente.

Abra o [Experience Platform [!DNL Postman] coleções no GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Há muitas coleções nesta página, para várias APIs da plataforma. Eu recomendo fortemente marcá-lo.

Agora, vamos fazer nossa primeira chamada de API:

1. Baixe o [Coleção de APIs do registro de esquema](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Schema%20Registry%20API.postman_collection.json) ao seu `Luma Tutorial Assets` pasta
1. Importar para [!DNL Postman]
1. Abertura **API do registro de esquemas > Esquemas > Listar esquemas**
1. Olhe para o **Params** e **Cabeçalhos** e observe como elas incluem algumas das variáveis de ambiente inseridas anteriormente.
1. Observe que **Cabeçalhos > Aceitar campo de valor** está definida como `application/vnd.adobe.xed-id+json`. As APIs do Registro de esquema exigem uma dessas [valores do cabeçalho Aceitar especificados](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/getting-started.html?lang=en#accept) que fornecem diferentes formatos na resposta.
1. Selecionar **Enviar** para fazer sua primeira chamada de API da plataforma!

Espero que você tenha tido sucesso `200 OK` resposta contendo uma lista dos esquemas XDM fornecidos pelo Adobe disponíveis em sua sandbox, como mostrado abaixo.

![Primeira chamada de API no Postman](assets/postman-firstAPICall.png)

Se a chamada não tiver sido bem-sucedida, aguarde um pouco para depurar usando os detalhes de resposta de erro da chamada da API e revise as etapas acima. Se você ficar paralisado, solicite ajuda no [Fórum da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform/ct-p/adobe-experience-platform-community?profile.language=pt) ou use o link no lado direito desta página para &quot;Registrar um problema&quot;.

Com suas permissões da Platform, sandbox e [!DNL Postman] configurado, você está pronto para [dados de modelo em esquemas](model-data-in-schemas.md)!
