---
title: GenStudio for Performance Marketing Crie seu bucket do Amazon AWS S3
description: GenStudio for Performance Marketing Crie seu bucket do Amazon AWS S3
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 044677e4-7ca3-4dfe-9067-640983681ea7
source-git-commit: 1f9a868c5e4ef4aa0e09d7f5d73a951006ee6c5a
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 7%

---

# 1.6.2 Criar o bucket do AWS S3

## 1.6.2.1 Crie seu bucket do S3

Vá para [https://console.aws.amazon.com](https://console.aws.amazon.com) e entre.

>[!NOTE]
>
>Se você ainda não tiver uma conta do AWS, crie uma nova conta do AWS usando seu endereço de email pessoal.

![ETL](./images/awshome.png)

Depois de fazer logon, você será redirecionado para o **Console de Gerenciamento do AWS**.

![ETL](./images/awsconsole.png)

Na barra de pesquisa, procure por **s3**. Clique no primeiro resultado da pesquisa: **S3 - Armazenamento Escalável na Nuvem**.

![ETL](./images/awsconsoles3.png)

Você verá a página inicial do **Amazon S3**. Clique em **Criar bloco**.

![ETL](./images/s3home.png)

Na tela **Criar Compartimento**, use o nome `--aepUserLdap---gspem-dam`.

![ETL](./images/bucketname.png)

Deixe todas as outras configurações padrão como estão. Role para baixo e clique em **Criar bloco**.

![ETL](./images/createbucket.png)

Você verá seu bucket ser criado e será redirecionado para a página inicial do Amazon S3.

![ETL](./images/S3homeb.png)

## Definir permissões para acessar seu bucket do S3

A próxima etapa é configurar o acesso ao seu bucket do S3.

Para fazer isso, vá para [https://console.aws.amazon.com/iam/home](https://console.aws.amazon.com/iam/home).

O acesso aos recursos do AWS é controlado pelo Amazon Identity and Access Management (IAM).

Agora você verá esta página.

![ETL](./images/iam.png)

No menu esquerdo, clique em **Usuários**. Você verá a tela **Usuários**. Clique em **Criar usuário**.

![ETL](./images/iammenu.png)

Em seguida, configure o usuário:

- Nome de Usuário: use `s3_--aepUserLdap--_gspem_dam`

Clique em **Next**.

![ETL](./images/configuser.png)

Em seguida, você verá essa tela de permissões. Clique em **Anexar políticas diretamente**.

![ETL](./images/perm1.png)

Insira o termo de pesquisa **s3** para ver todas as políticas S3 relacionadas. Selecione a política **AmazonS3FullAccess**. Role para baixo e clique em **Próximo**.

![ETL](./images/perm2.png)

Revise sua configuração. Clique em **Criar Usuário**.

![ETL](./images/review.png)

Você verá isso. Clique em **Exibir Usuário**.

![ETL](./images/review1.png)

Clique em **Credenciais de segurança** e em **Criar chave de acesso**.

![ETL](./images/cred.png)

Selecione o **Aplicativo em execução fora do AWS**. Role para baixo e clique em **Próximo**.

![ETL](./images/creda.png)

Clique em **Criar chave de acesso**

![ETL](./images/credb.png)

Você verá isso. Clique em **Mostrar** para ver sua chave de acesso secreta:

![ETL](./images/cred1.png)

Sua **Chave de acesso secreta** está sendo mostrada agora.

>[!IMPORTANT]
>
>Armazene suas credenciais em um arquivo de texto no computador.
>
> - ID da chave de acesso: ...
> - Chave de acesso secreta: ...
>
> Depois de clicar em **Concluído**, você nunca verá suas credenciais novamente!

Clique em **Concluído**.

![ETL](./images/cred2.png)

Agora você criou um bucket do AWS S3 com êxito e um usuário com permissões para acessá-lo.

## 1.6.2.2 Carregue o Assets no seu bucket do S3

Na barra de pesquisa, procure por **s3**. Clique no primeiro resultado da pesquisa: **S3 - Armazenamento Escalável na Nuvem**.

![ETL](./images/bucket1.png)

Clique para abrir o bucket do S3 recém-criado, que deve ser nomeado como `--aepUserLdap---gspem-dam`.

![ETL](./images/bucket2.png)

Clique em **Carregar**.

![ETL](./images/bucket3.png)

Você deverá ver isso.

![ETL](./images/bucket4.png)

Você pode baixar arquivos de imagem CitiSignal [aqui](./images/package.zip){target="_blank"}.

Exporte os arquivos para a área de trabalho.

![ETL](./images/bucket5.png)

Clique em **Adicionar pasta**.

![ETL](./images/bucket6.png)

Selecione a pasta **assets** da pasta de download **package**. Clique em **Carregar**.

![ETL](./images/bucket7.png)

Você deverá ver isso. Clique novamente em **Adicionar pasta**.

![ETL](./images/bucket8.png)

Selecione a pasta **miniaturas** da pasta de download **pacote**. Clique em **Carregar**.

![ETL](./images/bucket9.png)

Você deverá ver isso. Clique em **Carregar**.

![ETL](./images/bucket10.png)

O upload foi concluído. Clique em **Fechar**.

![ETL](./images/bucket11.png)

Agora você deve ter essa estrutura de pastas no seu bucket do S3.

![ETL](./images/bucket12.png)

## Próximas etapas

Ir para [Criar seu aplicativo DAM externo](./ex3.md){target="_blank"}

Voltar para [GenStudio for Performance Marketing - Extensibilidade](./genstudioext.md){target="_blank"}

Voltar para [Todos os Módulos](./../../../overview.md){target="_blank"}
