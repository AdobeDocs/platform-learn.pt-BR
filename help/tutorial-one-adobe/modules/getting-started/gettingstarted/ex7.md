---
title: Introdução - Configuração do Postman
description: Introdução - Configuração do Postman
kt: 5342
doc-type: tutorial
exl-id: c2a28819-5877-4f53-96c0-e4e5095d8cec
source-git-commit: a1da1c73cbddacde00211190a1ca3d36f7a2c329
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

# Opção 1: usar o Postman

>[!IMPORTANT]
>
>Se você for um funcionário da Adobe, siga as instruções para [instalar o PostBuster](./ex8.md){target="_blank"}!

## Download de ambiente do Postman

Vá para [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"} e abra o projeto.

![Nova integração do Adobe I/O](./images/iopr.png)

Clique na API **Firefly - Firefly Services**. Em seguida, clique em **Baixar para Postman** e escolha **Servidor a Servidor OAuth** para baixar um ambiente do Postman.

![Nova integração do Adobe I/O](./images/iopm.png)

## Autenticação do Postman para o Adobe I/O

Baixe e instale a versão relevante do Postman para seu sistema operacional em [Downloads da Postman](https://www.postman.com/downloads/){target="_blank"}.

![Nova integração do Adobe I/O](./images/getstarted.png)

Inicie o aplicativo.

No Postman, há dois conceitos: Ambientes e Coleções.

O arquivo de ambiente contém todas as variáveis de ambiente mais ou menos consistentes. No ambiente, você encontrará informações como o IMSOrg do seu ambiente do Adobe, além de credenciais de segurança como a ID do cliente e outras. Você baixou o arquivo de ambiente durante a configuração do Adobe I/O anteriormente e ele é nomeado como **`oauth_server_to_server.postman_environment.json`**.

A coleção contém várias solicitações de API que podem ser usadas. Você usará as coleções abaixo:

- 1 coleção para autenticação no Adobe I/O
- 1 Coleta para os exercícios do Adobe Firefly Services neste módulo
- 1 Coleção para os exercícios do Adobe Frame.io V4 neste módulo

Baixe o [postman-ff.zip](./../../../assets/postman/postman-ff.zip){target="_blank"} no desktop local.

![Nova integração do Adobe I/O](./images/pmfolder.png)

No arquivo **postman-ff.zip** estão os seguintes arquivos:

- `Adobe IO - OAuth.postman_collection.json`
- `FF - Firefly Services Tech Insiders.postman_collection.json`
- `Frame.io V4 - Tech Insiders.postman_collection.json`

Descompacte o **postman-ff.zip** e armazene os seguintes arquivos em uma pasta na sua área de trabalho:

- `Adobe IO - OAuth.postman_collection.json`
- `FF - Firefly Services Tech Insiders.postman_collection.json`
- `Frame.io V4 - Tech Insiders.postman_collection.json`
- `oauth_server_to_server.postman_environment.json`

![Nova integração do Adobe I/O](./images/pmfolder1.png)

No Postman, selecione **Importar**.

![Nova integração do Adobe I/O](./images/postmanui.png)

Selecione **Arquivos**.

![Nova integração do Adobe I/O](./images/choosefiles.png)

Escolha todos os arquivos da pasta e selecione **Abrir** e **Importar**.

![Nova integração do Adobe I/O](./images/selectfiles.png)

Clique em **Importar**.

![Nova integração do Adobe I/O](./images/impconfirm.png)

Agora você tem tudo o que precisa no Postman para começar a interagir com o Firefly Services por meio das APIs.

## Solicitar um token de acesso

Em seguida, para garantir que você esteja autenticado corretamente, é necessário solicitar um token de acesso.

Certifique-se de ter selecionado o ambiente correto antes de executar qualquer solicitação, verificando a lista suspensa Ambiente no canto superior direito. O Ambiente selecionado deve ter um nome semelhante a este, `--aepUserLdap-- One Adobe OAuth Credential`.

![Postman](./images/envselemea1.png)

O Ambiente selecionado deve ter um nome semelhante a este, `--aepUserLdap-- One Adobe OAuth Credential`.

![Postman](./images/envselemea.png)

Agora que o ambiente e as coleções do Postman estão configurados e funcionando, você pode autenticar do Postman para o Adobe I/O.

Na coleção **Adobe IO - OAuth**, selecione a solicitação denominada **POST - Obter Token de Acesso** e selecione **Enviar**.

Aviso em **Parâmetros de Consulta**, duas variáveis são referenciadas, `API_KEY` e `CLIENT_SECRET`. Essas variáveis foram obtidas do ambiente selecionado, `--aepUserLdap-- One Adobe OAuth Credential`.

![Postman](./images/ioauth.png)

Se for bem-sucedido, uma resposta contendo um token de portador, um token de acesso e uma janela de expiração será exibida na seção **Corpo** do Postman.

![Postman](./images/ioauthresp.png)

Você deve ver uma resposta semelhante contendo as seguintes informações:

| Chave | Valor |
|:-------------:| :---------------:| 
| token_type | **portador** |
| access_token | **eyJhbGciOiJSUz...** |
| expires_in | **86399** |

O **bearer-token** do Adobe I/O tem um valor específico (o access_token muito longo) e uma janela de expiração, e agora é válido por 24 horas. Isso significa que, após 24 horas, se você quiser usar o Postman para interagir com as APIs do Adobe, precisará gerar um novo token executando essa solicitação novamente.

Agora o ambiente do Postman está configurado e funcionando.

## Próximas etapas

Vá para [Aplicativos a serem instalados](./ex9.md){target="_blank"}

Volte para [Introdução](./getting-started.md){target="_blank"}

Voltar para [Todos os módulos](./../../../overview.md){target="_blank"}
