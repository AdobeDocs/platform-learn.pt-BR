---
title: Real-time CDP - Criar um segmento e executar ações - Enviar o segmento para um destino S3
description: Real-time CDP - Criar um segmento e executar ações - Enviar o segmento para um destino S3
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 3%

---

# 2.3.4 Realizar ação: enviar seu segmento para um destino S3

O Adobe Experience Platform também pode compartilhar públicos com destinos de marketing por email, como Salesforce Marketing Cloud, Oracle Eloqua, Oracle Responsys e Adobe Campaign.

Você pode usar o FTP ou SFTP como parte dos destinos dedicados para cada um desses Destinos de marketing por email, ou pode usar o AWS S3 para trocar listas de clientes entre o Adobe Experience Platform e esses Destinos de marketing por email.

Neste módulo, você configurará esse destino usando um bucket do AWS S3.

## 2.3.4.1 Criar seu S3 bucket

Acesse [https://console.aws.amazon.com](https://console.aws.amazon.com) e entre com a conta da Amazon criada anteriormente.

![ETL](./images/awshome.png)

Depois de fazer logon, você será redirecionado para o **Console de Gerenciamento do AWS**.

![ETL](./images/awsconsole.png)

No menu **Localizar Serviços**, procure **s3**. Clique no primeiro resultado da pesquisa: **S3 - Armazenamento Escalável na Nuvem**.

![ETL](./images/awsconsoles3.png)

Você verá a página inicial do **Amazon S3**. Clique em **Criar bloco**.

![ETL](./images/s3home.png)

Na tela **Criar bloco**, você precisa configurar dois itens:

- Nome: use o nome `aepmodulertcdp--aepUserLdap--`. Como exemplo, neste exercício, o nome do bucket é **aepmodulertcdpvangeluw**
- Região: utilizar a região **EU (Frankfurt) eu-central-1**

![ETL](./images/bucketname.png)

Deixe todas as outras configurações padrão como estão. Role para baixo e clique em **Criar bloco**.

![ETL](./images/createbucket.png)

Você verá seu bucket ser criado e será redirecionado para a página inicial do Amazon S3.

![ETL](./images/S3homeb.png)

## 2.3.4.2 Definir permissões para acessar o bucket do S3

A próxima etapa é configurar o acesso ao seu bucket do S3.

Para fazer isso, vá para [https://console.aws.amazon.com/iam/home](https://console.aws.amazon.com/iam/home).

O acesso aos recursos do AWS é controlado pelo Amazon Identity and Access Management (IAM).

Agora você verá esta página.

![ETL](./images/iam.png)

No menu esquerdo, clique em **Usuários**. Você verá a tela **Usuários**. Clique em **Adicionar usuários**.

![ETL](./images/iammenu.png)

Em seguida, configure o usuário:

- Nome do Usuário: use `s3_--aepUserLdap--_rtcdp` como um nome, portanto, neste exemplo, o nome é `s3_vangeluw_rtcdp`.
- Tipo de acesso do AWS: selecione **Access key - Programmatic access**.

Clique em **Avançar: Permissões**.

![ETL](./images/configuser.png)

Em seguida, você verá essa tela de permissões. Clique em **Anexar diretivas existentes diretamente**.

![ETL](./images/perm1.png)

Insira o termo de pesquisa **s3** para ver todas as políticas S3 relacionadas. Selecione a política **AmazonS3FullAccess**. Clique em **Avançar: Marcas**.

![ETL](./images/perm2.png)

Na tela **Tags**, não há necessidade de configurar nada. Clique em **Avançar: revisão**.

![ETL](./images/perm3.png)

Revise sua configuração. Clique em **Criar Usuário**.

![ETL](./images/review.png)

Seu usuário foi criado e você está vendo suas credenciais para acessar seu ambiente S3. Esta é a única vez que você verá suas credenciais. Por favor, anote-as.

![ETL](./images/cred.png)

Clique em **Mostrar** para ver sua chave de acesso secreta:

![ETL](./images/cred1.png)

>[!IMPORTANT]
>
>Armazene suas credenciais em um arquivo de texto no computador.
>
> - ID da chave de acesso: ...
> - Chave de acesso secreta: ...
>
> Depois de clicar em **Fechar**, você nunca mais verá suas credenciais!

Clique em **Fechar**.

![ETL](./images/close.png)

Agora você criou um bucket do AWS S3 com êxito e um usuário com permissões para acessá-lo.

## 2.3.4.3 Configurar o destino no Adobe Experience Platform

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepSandboxName--``. Você pode fazer isso clicando no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. Depois de selecionar a [!UICONTROL sandbox] apropriada, você verá a alteração da tela e agora estará na [!UICONTROL sandbox] dedicada.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/sb1.png)

No menu esquerdo, vá para **Destinos** e, em seguida, vá para **Catálogo**. Você verá o **Catálogo de Destinos**.

![RTCDP](./images/rtcdpmenudest.png)

Clique em **Armazenamento na Nuvem** e no botão **Configurar** (ou em **Ativar Segmentos**, dependendo do seu ambiente) no cartão **Amazon S3**.

![RTCDP](./images/rtcdp2.png)

Dependendo do seu ambiente, talvez seja necessário clicar em **+ Configurar novo destino** para começar a criar seu destino.

![RTCDP](./images/rtcdp2a.png)

Selecione **Nova Conta** como Tipo de Conta. Use as credenciais S3 fornecidas na etapa anterior:

| ID da chave de acesso | Chave de Acesso Secreta |
|:-----------------------:| :-----------------------:|
| AKIA... | Cm5Ln... |

Clique em **Conectar ao destino**.

![RTCDP](./images/rtcdpsfs3.png)

Você verá uma confirmação visual de que esse destino está conectado agora.

![RTCDP](./images/rtcdpsfs3connected.png)

É necessário fornecer um nome e uma pasta para que o Adobe Experience Platform possa se conectar ao bucket do S3.

Como convenção de nomenclatura, use o seguinte:

| ID da chave de acesso | Chave de Acesso Secreta |
|:-----------------------:| :-----------------------:|
| Nome | `AWS - S3 - --aepUserLdap--` |
| Descrição | `AWS - S3 - --aepUserLdap--` |
| Nome do bloco | `aepmodulertcdp--aepUserLdap--` |
| Caminho da pasta | / |

Clique em **Next**.

![RTCDP](./images/rtcdpsfs3connect2.png)

Agora, é possível anexar uma Política de governança de dados ao novo destino. Clique em **Next**.

![RTCDP](./images/rtcdpsfs3connect2gov.png)

Na lista de segmentos, procure o segmento que você criou no exercício 1 e selecione-o. Clique em **Next**.

![RTCDP](./images/s3a.png)

Você verá isso. Se desejar, edite a programação clicando no ícone **lápis**. **Criar Agendamento**.

![RTCDP](./images/s3bb.png)

Defina o cronograma de sua escolha. Selecione **Exportar arquivos incrementais** e defina a frequência como **A cada** 3 horas **.** Clique em **Criar**.

![RTCDP](./images/s3bbc.png)

Então você terá isto. Clique em **Next**.

![RTCDP](./images/s3bbca.png)

Agora é possível selecionar atributos para a exportação em direção ao AWS S3. Clique em **Adicionar novo campo** e verifique se o campo `--aepTenantId--.identification.core.ecid` foi adicionado e marcado como **Chave de Desduplicação**.

Como opção, você pode adicionar quantos outros campos forem necessários.

Depois de adicionar todos os campos, clique em **Avançar**.

![RTCDP](./images/s3c.png)

Revise sua configuração. Clique em **Concluir** para concluir sua configuração.

![RTCDP](./images/s3g.png)

Você voltará à tela Ativação de destino e verá seu segmento adicionado a esse destino.

![RTCDP](./images/s3j.png)

Se você quiser adicionar mais exportações de segmentos, clique em **Ativar segmentos** para reiniciar o processo e adicionar mais segmentos.

![RTCDP](./images/s3k.png)

Próxima etapa: [2.3.5 Executar Ação: enviar seu segmento para a Adobe Target](./ex5.md)

[Voltar ao módulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Voltar a todos os módulos](../../../overview.md)
