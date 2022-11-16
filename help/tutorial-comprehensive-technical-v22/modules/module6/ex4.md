---
title: CDP em tempo real - Crie um segmento e execute ações - Envie seu segmento para um destino S3
description: CDP em tempo real - Crie um segmento e execute ações - Envie seu segmento para um destino S3
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 5b0bcd69-7131-48a3-bd3e-773ba95cc42b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 3%

---

# 6.4 Tomar medidas: enviar seu segmento para um destino S3

O Adobe Experience Platform também tem a capacidade de compartilhar públicos para destinos de marketing por email, como o Salesforce Marketing Cloud, Oracle Eloqua, Oracle Responsys e Adobe Campaign.

Você pode usar o FTP ou SFTP como parte dos destinos dedicados para cada um desses Destinos de marketing de email, ou pode usar o AWS S3 para trocar listas de clientes entre o Adobe Experience Platform e esses Destinos de marketing de email.

Neste módulo, você configurará esse destino usando um bucket do AWS S3.

## 6.4.1 Criar o bucket S3

Ir para [https://console.aws.amazon.com](https://console.aws.amazon.com) e faça logon com a conta Amazon criada anteriormente.

![ETL](./images/awshome.png)

Depois de fazer logon, você será redirecionado para a variável **Console de gerenciamento do AWS**.

![ETL](./images/awsconsole.png)

No **Localizar Serviços** , pesquisar por **s3**. Clique no primeiro resultado da pesquisa: **S3 - Armazenamento escalável na nuvem**.

![ETL](./images/awsconsoles3.png)

Você verá o **Amazon S3** homepage. Clique em **Criar bucket**.

![ETL](./images/s3home.png)

No **Criar bucket** , você precisa configurar duas coisas:

- Nome: usar o nome `aepmodulertcdp--demoProfileLdap--`. Como exemplo, neste exercício, o nome do bucket é **aepmodulertcdpvangeluw**
- Região: usar a região **UE (Frankfurt) eu-central-1**

![ETL](./images/bucketname.png)

Deixe todas as outras configurações padrão como estão. Role para baixo e clique em **Criar bucket**.

![ETL](./images/createbucket.png)

Você verá seu bucket sendo criado e será redirecionado para a página inicial do Amazon S3.

![ETL](./images/S3homeb.png)

## 6.4.2 Defina as permissões para acessar seu bucket S3

A próxima etapa é configurar o acesso ao seu bucket S3.

Para fazer isso, acesse [https://console.aws.amazon.com/iam/home](https://console.aws.amazon.com/iam/home).

O acesso aos recursos da AWS é controlado pelo Amazon Identity and Access Management (IAM).

Agora você verá esta página.

![ETL](./images/iam.png)

No menu esquerdo, clique em **Usuários**. Você verá o **Usuários** tela. Clique em **Adicionar usuários**.

![ETL](./images/iammenu.png)

Em seguida, configure o usuário:

- Nome de usuário: use `s3_--demoProfileLdap--_rtcdp` como um nome, portanto, neste exemplo, o nome é `s3_vangeluw_rtcdp`.
- Tipo de acesso AWS: select **Chave de acesso - Acesso programático**.

Clique em **Próximo: Permissões**.

![ETL](./images/configuser.png)

Você verá essa tela de permissões. Clique em **Anexar as políticas existentes diretamente**.

![ETL](./images/perm1.png)

Insira o termo de pesquisa **s3** para ver todas as políticas S3 relacionadas. Selecionar a política **AmazonS3FullAccess**. Clique em **Próximo: Tags**.

![ETL](./images/perm2.png)

No **Tags** não há necessidade de configurar nada. Clique em **Próximo: Revisão**.

![ETL](./images/perm3.png)

Revise sua configuração. Clique em **Criar usuário**.

![ETL](./images/review.png)

Seu usuário foi criado e você está vendo suas credenciais para acessar o ambiente S3. É a única vez que você verá suas credenciais, então, por favor, anote-as.

![ETL](./images/cred.png)

Clique em **Mostrar** para ver sua chave de acesso Secret:

![ETL](./images/cred1.png)

>[!IMPORTANT]
>
>Armazene suas credenciais em um arquivo de texto em seu computador.
>
> - ID da chave de acesso: ...
> - Chave de acesso secreta: ...
>
> Depois de clicar **Fechar** você nunca verá suas credenciais novamente!

Clique em **Fechar**.

![ETL](./images/close.png)

Agora você criou com êxito um bucket do AWS S3 e criou um usuário com permissões para acessar esse bucket.

## 6.4.3 Configurar destino no Adobe Experience Platform

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você será direcionado para a página inicial do Adobe Experience Platform.

![Assimilação de dados](../module2/images/home.png)

Antes de continuar, é necessário selecionar um **sandbox**. A sandbox a ser selecionada é chamada de ``--aepSandboxId--``. Você pode fazer isso clicando no texto **[!UICONTROL Produto de produção]** na linha azul na parte superior da tela. Depois de selecionar a [!UICONTROL sandbox], você verá a tela mudar e agora você estará em seu [!UICONTROL sandbox].

![Assimilação de dados](../module2/images/sb1.png)

No menu esquerdo, acesse **Destinos**, em seguida, vá para **Catálogo**. Você verá o **Catálogo de destinos**.

![RTCDP](./images/rtcdpmenudest.png)

Clique em **Armazenamento na nuvem**, em seguida, clique no botão **Configurar** (ou ativar) **Ativar segmentos**, dependendo do seu ambiente) na **Amazon S3** cartão.

![RTCDP](./images/rtcdp2.png)

Dependendo do seu ambiente, talvez seja necessário clicar em **+ Configurar novo destino** para começar a criar o destino.

![RTCDP](./images/rtcdp2a.png)

Selecionar **Nova conta** como Tipo de conta. Use as credenciais do S3 que foram fornecidas a você na etapa anterior:

| ID da chave de acesso | Chave de acesso secreta |
|:-----------------------:| :-----------------------:|
| AKIA...... | Cm5Ln...... |

Clique em **Ligar ao destino**.

![RTCDP](./images/rtcdpsfs3.png)

Em seguida, você verá uma confirmação visual de que esse destino está conectado.

![RTCDP](./images/rtcdpsfs3connected.png)

É necessário fornecer um nome e uma pasta para que o Adobe Experience Platform possa se conectar ao bucket S3.

Como convenção de nomenclatura, use o seguinte:

| ID da chave de acesso | Chave de acesso secreta |
|:-----------------------:| :-----------------------:|
| Nome | `AWS - S3 - --demoProfileLdap--` |
| Descrição | `AWS - S3 - --demoProfileLdap--` |
| Nome do bucket | `aepmodulertcdp--demoProfileLdap--` |
| Caminho da pasta | / |

Clique em **Próximo**.

![RTCDP](./images/rtcdpsfs3connect2.png)

Agora é possível anexar opcionalmente uma Política de Governança de Dados ao seu novo destino. Clique em **Próximo**.

![RTCDP](./images/rtcdpsfs3connect2gov.png)

Na lista de segmentos, pesquise o segmento criado no exercício 1 e selecione-o. Clique em **Próximo**.

![RTCDP](./images/s3a.png)

Você verá isso. Se desejar, edite o agendamento clicando no botão **lápis** ícone . **Criar Programação**.

![RTCDP](./images/s3bb.png)

Defina seu cronograma de escolha. Selecionar **Exportar arquivos incrementais** e defina a frequência como **Por hora** each **3 horas**. Clique em **Criar**.

![RTCDP](./images/s3bbc.png)

Você terá isso. Clique em **Próximo**.

![RTCDP](./images/s3bbca.png)

Agora é possível selecionar atributos para a exportação para o AWS S3. Clique em **Adicionar novo campo** e garantir o campo `--aepTenantId--.identification.core.ecid` é adicionado e marcado como **Chave de desduplicação**.

Como opção, você pode adicionar quantos outros campos forem necessários.

Depois de adicionar todos os campos, clique em **Próximo**.

![RTCDP](./images/s3c.png)

Revise sua configuração. Clique em **Concluir** para concluir a configuração.

![RTCDP](./images/s3g.png)

Você estará de volta na tela de Ativação de destino e verá seu segmento adicionado a esse destino.

![RTCDP](./images/s3j.png)

Se quiser adicionar mais exportações de segmento, clique em **Ativar segmentos** para reiniciar o processo e adicionar mais segmentos.

![RTCDP](./images/s3k.png)

Próxima etapa: [6.5 Tomar medidas: enviar seu segmento para a Adobe Target](./ex5.md)

[Voltar ao Módulo 6](./real-time-cdp-build-a-segment-take-action.md)

[Voltar para todos os módulos](../../overview.md)
