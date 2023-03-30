---
title: Importar dados de amostra para a Adobe Experience Platform
description: Saiba como configurar um ambiente de caixa de proteção do Experience Platform com alguns dados de amostra.
role: Developer
feature: API
kt: 7349
thumbnail: 7349.jpg
exl-id: da94f4bd-0686-4d6a-a158-506f2e401b4e
source-git-commit: d5988bd8e6d31b183e2a264bea4fb05cd90ef1a7
workflow-type: tm+mt
source-wordcount: '1832'
ht-degree: 5%

---

# Importar dados de amostra para a Adobe Experience Platform

Saiba como configurar um ambiente de sandbox da Experience Platform com dados de amostra. Usando uma coleção do Postman, você pode criar grupos de campos, esquemas, conjuntos de dados e, em seguida, importar dados de amostra para a Experience Platform.

## Caso de uso de dados de amostra

Os usuários da Experience Platform business geralmente precisam passar por uma série de etapas que incluem a identificação de grupos de campos, a criação de schemas, a preparação de dados, a criação de conjuntos de dados e, em seguida, a assimilação de dados, antes que possam explorar os recursos de marketing oferecidos pelo Experience Platform. Este tutorial automatiza algumas etapas para que você possa inserir dados em uma sandbox da Platform o mais rápido possível.

Este tutorial foca em uma marca fictícia de varejo chamada Luma. Eles investem no Adobe Experience Platform para combinar dados de fidelidade, CRM, catálogo de produtos e compra offline em perfis de clientes em tempo real e ativar esses perfis para elevar seu marketing ao próximo nível. Geramos dados de amostra para o Luma e, no restante deste tutorial, você importará esses dados para um de seus ambientes de sandbox do Experience Platform.

>[!NOTE]
>
>O resultado final deste tutorial é uma sandbox contendo dados semelhantes ao [Tutorial Introdução à Adobe Experience Platform para arquitetos de dados e engenheiros de dados](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html). Ela foi atualizada em abril de 2023 para oferecer suporte à variável [Desafios da Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer-learn/challenges/introduction-and-prerequisites.html?lang=pt-BR).


## Pré-requisitos

* Você tem acesso às APIs do Experience Platform e sabe como autenticar. Caso contrário, reveja esta [tutorial](https://experienceleague.adobe.com/docs/platform-learn/tutorials/platform-api-authentication.html?lang=pt-BR).
* Você tem acesso a uma sandbox de desenvolvimento de Experience Platform.
* Você sabe sua ID de locatário do Experience Platform. Você pode obtê-lo fazendo um [solicitação de API](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/getting-started.html?lang=en#know-your-tenant_id)
ou extraindo-a do URL ao fazer logon na conta da plataforma. Por exemplo, no URL a seguir, o locatário é &quot;
`techmarketingdemos`&quot; `https://experience.adobe.com/#/@techmarketingdemos/sname:prod/platform/home`.

## Uso do Postman {#postman}

### Configurar variáveis de ambiente

Antes de seguir as etapas, certifique-se de ter baixado a variável [Postman](https://www.postman.com/downloads/) aplicativo.  Vamos começar!

1. Baixe o [platform-utils-main.zip](../assets/data-generator/platform-utils-main.zip) , que contém todos os arquivos necessários para este tutorial.

   >[!NOTE]
   >
   >Os dados do usuário contidos na variável [platform-utils-main.zip](../assets/data-generator/platform-utils-main.zip) O ficheiro é fictício e deve ser utilizado apenas para fins de demonstração.

1. Na pasta de downloads, mova o arquivo `platform-utils-main.zip` para o local desejado em seu computador e descompacte-o.
1. No `luma-data` , abra todas as `json` arquivos em um editor de texto e substitua todas as instâncias de `_yourOrganizationID` com sua própria ID de locatário, precedida por um sublinhado.
1. Abrir `luma-offline-purchases.json` e `luma-web-events.json` em um editor de texto e atualize todos os carimbos de data e hora para que os eventos ocorram no último mês (por exemplo, pesquise por `"timestamp":"2022-11` e substituir o ano e o mês)
1. Observe a localização da pasta descompactada, pois você precisará dela posteriormente ao configurar a variável `FILE_PATH` Variável de ambiente do Postman:

   >[!NOTE]
   > Para obter o caminho do arquivo na Mac, navegue até o `platform-utils-main` , clique com o botão direito do mouse na pasta e selecione **Obter informações** opção.
   >
   > ![Caminho do arquivo Mac](../assets/data-generator/images/mac-file-path.png)

   >[!NOTE]
   > Para obter o caminho do arquivo em suas janelas, clique em para abrir o local da pasta desejada e clique com o botão direito do mouse à direita do caminho na barra de endereços. Copie o endereço para obter o caminho do arquivo.
   > 
   > ![Caminho do arquivo do Windows](../assets/data-generator/images/windows-file-path.png)

1. Abra o Postman e crie um novo espaço de trabalho na **Áreas de trabalho** menu suspenso:\
   ![Criar espaço de trabalho](../assets/data-generator/images/create-workspace.png)
1. Insira um **Nome** e opcional **Resumo** para o seu espaço de trabalho e clique em **Criar espaço de trabalho**. O Postman mudará para seu novo espaço de trabalho ao criá-lo.
   ![Salvar espaço de trabalho](../assets/data-generator/images/save-workspace.png)
1. Agora ajuste algumas configurações para executar as coleções do Postman neste espaço de trabalho. No cabeçalho do Postman, clique no ícone de engrenagem e selecione **Configurações** para abrir o modal de configurações. Você também pode usar o atalho de teclado (CMD/CTRL + ,) para abrir a modal.
1. Em `General` , atualize o tempo limite da solicitação em ms para `5000 ms` e ativar `allow reading file outside this directory`
   ![Configurações](../assets/data-generator/images/settings.png)

   >[!NOTE]
   > Se os arquivos forem carregados de dentro do diretório de trabalho, ele será executado sem problemas em todos os dispositivos, se os mesmos arquivos forem armazenados em outros dispositivos. No entanto, se você deseja executar arquivos de fora do diretório de trabalho, uma configuração deve ser ativada para declarar a mesma intenção. Se o seu `FILE_PATH` não for o mesmo que o caminho do diretório de trabalho do Postman, essa opção deverá ser ativada.

1. Feche o **Configurações** painel.
1. Selecione o **Ambientes** e depois selecione **Importar**:
   ![Importação de Ambiente](../assets/data-generator/images/env-import.png)
1. Importe o arquivo de ambiente json baixado, `DataInExperiencePlatform.postman_environment`
1. No Postman, selecione o ambiente na lista suspensa superior direita e clique no ícone de olho para exibir as variáveis de ambiente:
   ![Seleção de ambiente](../assets/data-generator/images/env-selection.png)

1. Verifique se as variáveis de ambiente a seguir foram preenchidas. Para saber como obter o valor das variáveis de ambiente, verifique o [Autenticar para APIs do Experience Platform](/help/platform/authentication/platform-api-authentication.md) tutorial para obter instruções passo a passo.

   * `CLIENT_SECRET`
   * `API_KEY`—`Client ID` no Adobe Developer Console
   * `TECHNICAL_ACCOUNT_ID`
   * `META_SCOPE`
   * `IMS`
   * `IMS_ORG`—`Organization ID` no Adobe Developer Console
   * `PRIVATE_KEY`
   * `SANDBOX_NAME`
   * `CONTAINER_ID`
   * `TENANT_ID`—certifique-se de liderar com um sublinhado, por exemplo `_techmarketingdemos`
   * `platform_end_point`
   * `FILE_PATH`—use o caminho da pasta local onde você descompactou o `platform-utils-main.zip` arquivo. Certifique-se de incluir o nome da pasta, por exemplo `/Users/dwright/Desktop/platform-utils-main`

1. **Salvar** o ambiente atualizado

### Importar coleções do Postman

Em seguida, é necessário importar as coleções para o Postman.

1. Selecionar **Coleções** e escolha a opção de importação:

   ![Coleções](../assets/data-generator/images/collections.png)

1. Importe as seguintes coleções:

   * `0-Authentication.postman_collection.json`
   * `1-Luma-Loyalty-Data.postman_collection.json`
   * `2-Luma-CRM-Data.postman_collection.json`
   * `3-Luma-Product-Catalog.postman_collection.json`
   * `4-Luma-Offline-Purchase-Events.postman_collection.json`
   * `5-Luma-Product-Inventory-Events.postman_collection.json`
   * `6-Luma-Test-Profiles.postman_collection.json`
   * `7-Luma-Web-Events.postman_collection.json`

   ![Importação de Coleções](../assets/data-generator/images/collection-files.png)

### Autenticar

Em seguida, é necessário autenticar e gerar um token de usuário. Esteja ciente de que os métodos de geração de tokens usados neste tutorial são adequados apenas para uso não relacionado à produção. A assinatura local carrega uma biblioteca do JavaScript de um host de terceiros e a assinatura remota envia a chave privada para um serviço da Web de propriedade e operado pelo Adobe. Embora o Adobe não armazene essa chave privada, as chaves de produção nunca devem ser compartilhadas com ninguém.

1. Abra o `Authentication` , selecione a `IMS: JWT Generate + Auth via User Token` POST e clique em `SEND` para autenticar e obter o token de acesso.

   ![Importação de Coleções](../assets/data-generator/images/authentication.png)

1. Revise as variáveis de ambiente e observe que a variável `JWT_TOKEN` e `ACCESS_TOKEN` agora são preenchidas.

### Importar dados

Agora você pode preparar e importar os dados para a sandbox da Platform. As coleções de Postman que você importou farão todo o trabalho pesado!

1. Abra o `1-Luma-Loyalty-Data` coleção e clique em **Executar** na guia visão geral para iniciar um Collection Runner.

   ![Importação de Coleções](../assets/data-generator/images/loyalty.png)

1. Na janela do runner da coleção, selecione o ambiente na lista suspensa e atualize o **Atraso** para `4000ms`, marque a opção **Salvar respostas** e verifique se a ordem de execução está correta. Clique no botão **Executar dados de fidelidade do Luma** botão

   ![Importação de Coleções](../assets/data-generator/images/loyalty-run.png)

   >[!NOTE]
   >
   >**1-Luma-Loyalty-Data** cria um schema para dados de fidelidade do cliente. O esquema é baseado na classe Perfil individual XDM, no grupo de campos padrão e em um grupo de campos e tipo de dados personalizados. A coleção cria um conjunto de dados usando o esquema e faz upload de dados de fidelidade do cliente de amostra para o Adobe Experience Platform.

   >[!NOTE]
   >
   >Se houver falha em solicitações de coleta durante o executor da coleta do Postman, pare a execução e execute as solicitações de coleta uma por uma.

1. Se tudo correr bem, todas as solicitações no `Luma-Loyalty-Data` A coleção deve ser aprovada.

   ![Resultado da Fidelidade](../assets/data-generator/images/loyalty-result.png)

1. Agora vamos fazer logon no [Interface do Adobe Experience Platform](https://platform.adobe.com/) e navegue até os conjuntos de dados.
1. Abra o `Luma Loyalty Dataset` conjunto de dados e, na janela de atividade do conjunto de dados, é possível visualizar uma execução em lote bem-sucedida que assimilou 1000 registros. Você também pode clicar na opção visualizar conjunto de dados para verificar os registros assimilados. Talvez seja necessário aguardar vários minutos para confirmar que 1000 [!UICONTROL Novos fragmentos de perfil] foram criadas.
   ![Conjunto de dados de fidelidade](../assets/data-generator/images/loyalty-dataset.png)
1. Repita as etapas 1 a 3 para executar as outras coleções:
   * `2-Luma-CRM-Data.postman_collection.json` cria um esquema e um conjunto de dados preenchido para dados do CRM de clientes. O esquema é baseado na classe Perfil individual XDM que compreende Detalhes demográficos, Detalhes de contato pessoal, Detalhes de preferência e um grupo de campo de identidade personalizado.
   * `3-Luma-Product-Catalog.postman_collection.json` cria um esquema e um conjunto de dados preenchido para informações do catálogo de produtos. O esquema é baseado em uma classe personalizada de catálogo de produtos e usa um grupo de campos personalizado de catálogo de produtos.
   * `4-Luma-Offline-Purchase-Events.postman_collection.json` cria um esquema e um conjunto de dados preenchido para dados de eventos de compra offline de clientes. O esquema é baseado na classe XDM ExperienceEvent e inclui uma identidade personalizada e grupos de campos Detalhes de comércio .
   * `5-Luma-Product-Inventory-Events.postman_collection.json` cria um esquema e um conjunto de dados preenchido para eventos relacionados a produtos que entram e saem do estoque. O esquema é baseado em uma classe de evento comercial personalizada e em um grupo de campo personalizado.
   * `6-Luma-Test-Profiles.postman_collection.json` cria um esquema e um conjunto de dados preenchido com perfis de teste para usar no Adobe Journey Optimizer
   * `7-Luma-Web-Events.postman_collection.json` cria um esquema e um conjunto de dados preenchido com dados históricos da Web simples.


## Validação

Os dados de amostra foram projetados para que, quando as coleções forem executadas, os Perfis do cliente em tempo real sejam criados e combinem dados de vários sistemas. Um bom exemplo disso é o primeiro registro dos conjuntos de dados de fidelidade, CRM e compra offline. Procure esse perfil para confirmar que os dados foram assimilados. No [Interface do Adobe Experience Platform](https://platform.adobe.com/):

1. Ir para **[!UICONTROL Perfis]** > **[!UICONTROL Procurar]**
1. Selecionar `Luma Loyalty Id` como **[!UICONTROL Namespace de identidade]**
1. Procurar por `5625458` como **[!UICONTROL Valor de identidade]**
1. Abra o `Daniel Wright` perfil

>[!TIP]
>
>Se você não vir o perfil, verifique o [!UICONTROL Conjuntos de dados] para confirmar que todos os conjuntos de dados foram criados e assimilados com êxito. Se isso parecer bom, espere 15 minutos e veja se o perfil está disponível no visualizador.  Se houver problemas com a assimilação de dados, verifique as mensagens de erro para tentar localizar o problema. Você também pode tentar ativar o diagnóstico de erros no [!UICONTROL Conjuntos de dados] e arraste e solte o arquivo de dados json para assimilar novamente os dados.


![Abrir um perfil](../assets/data-generator/images/validation-profile-open.png)

Ao navegar pelos dados no **[!UICONTROL Atributos]** e **[!UICONTROL Eventos]** , você deve ver que o perfil contém dados dos vários arquivos de dados:
![Dados do evento do arquivo de eventos de Compra offline](../assets/data-generator/images/validation-profile-events.png)

## Próximas etapas

Se você quiser saber mais sobre o Adobe Journey Optimizer, esta sandbox contém tudo o que você precisa para pegar a variável [Desafios da Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer-learn/challenges/introduction-and-prerequisites.html?lang=pt-BR)

Se você quiser saber mais sobre as políticas de mesclagem, governança de dados, serviço de query e o construtor de segmentos, vá para [lição 11 do tutorial Introdução aos arquitetos de dados e engenheiros de dados](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/create-merge-policies.html?lang=en). As lições anteriores deste outro tutorial permitem criar manualmente tudo o que acabou de ser preenchido por essas coleções do Postman — aproveite o início da página!

Se quiser criar uma implementação de SDK da Web de amostra para vincular a essa sandbox, verifique o
[Implementar o Adobe Experience Cloud com o tutorial do SDK da Web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=pt-BR). Depois de configurar as lições &quot;Configuração inicial&quot;, &quot;Configuração de tags&quot; e &quot;Configurar Experience Platform&quot; do tutorial do SDK da Web, faça logon no site Luma usando os primeiros dez endereços de email na `luma-crm.json` arquivo usando a senha `test` para ver os fragmentos de perfil se mesclam aos dados carregados neste tutorial.

Se você deseja criar uma amostra da implementação do SDK móvel para vincular a essa sandbox, consulte
[Tutorial Implementar o Adobe Experience Cloud em aplicativos móveis](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html?lang=pt-BR). Após configurar as lições de &quot;Configuração inicial&quot;, &quot;Implementação do aplicativo&quot; e &quot;Experience Platform&quot; do tutorial do SDK da Web, faça logon no site Luma usando os primeiros endereços de email na `luma-crm.json` para ver uma mesclagem de fragmento de perfil com dados carregados neste tutorial.

## Redefinir ambiente de sandbox {#reset-sandbox}

A redefinição de uma sandbox de não produção exclui todos os recursos associados a ela (esquemas, conjuntos de dados e assim por diante), mantendo o nome da sandbox e as permissões associadas. Essa sandbox &quot;limpa&quot; continua disponível com o mesmo nome para usuários que têm acesso a ela.

Siga as etapas [here](https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html?lang=en#reset-a-sandbox) para redefinir um ambiente sandbox.
