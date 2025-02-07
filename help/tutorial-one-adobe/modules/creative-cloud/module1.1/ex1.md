---
title: Introdução aos serviços do Firefly
description: Saiba como usar o Postman e o Adobe I/O para consultar APIs de serviços Adobe Firefly
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: e6a549441d425801f2a554da9af803dca646009e
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---

# 1.1.1 Introdução aos Serviços Firefly

Saiba como usar o Postman e o Adobe I/O para consultar APIs de serviços de Adobe Firefly.

## 1.1.1.2 Configurar o projeto Adobe I/O

Neste exercício, o Adobe I/O é usado para consultar as APIs de serviços do Firefly. Siga estas etapas para configurar o Adobe I/O.

1. Ir para [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}.

![Adobe I/O Nova integração](./images/iohome.png)

1. Selecione a instância correta no canto superior direito da tela. Sua instância é `--aepImsOrgName--`. Em seguida, selecione **Criar novo projeto**.

![Adobe I/O Nova integração](./images/iocomp.png)

1. Selecione **+ Adicionar ao Projeto** e escolha **API**.

![Adobe I/O Nova integração](./images/adobe_io_access_api.png)

Sua tela deve ter esta aparência.

![Adobe I/O Nova integração](./images/api1.png)

1. Selecione **Creative Cloud** e escolha **Firefly - Firefly Services**, depois selecione **Próximo**.

![Adobe I/O Nova integração](./images/api3.png)

1. Forneça um nome para a credencial: `--aepUserLdap-- - Firefly Services OAuth credential`e selecione **Avançar**.

![Adobe I/O Nova integração](./images/api4.png)

1. Selecione o perfil padrão **Configuração de serviços de Firefly padrão** e selecione **Salvar API configurada**.

![Adobe I/O Nova integração](./images/api9.png)

Sua integração de Adobe I/O está pronta.

![Adobe I/O Nova integração](./images/api11.png)

## 1.1.1.3 Baixar o ambiente do Postman

1. Selecione **Baixar para Postman** e escolha **Servidor para servidor OAuth** para baixar um ambiente do Postman.

![Adobe I/O Nova integração](./images/iopm.png)

1. Selecione o nome do projeto.

![Adobe I/O Nova integração](./images/api13.png)

1. Selecione **Editar Projeto**.

![Adobe I/O Nova integração](./images/api14.png)

1. Digite um nome amigável para a integração: `--aepUserLdap-- Firefly`e selecione **Salvar**.

![Adobe I/O Nova integração](./images/api15.png)

A configuração da integração do Adobe I/O foi concluída.

![Adobe I/O Nova integração](./images/api16.png)

## 1.1.1.4 Autenticação Postman para Adobe I/O

>[!IMPORTANT]
>
>Se você for um funcionário da Adobe, siga as instruções aqui para usar o [PostBuster](./../../../postbuster.md).

1. Baixe e instale a versão relevante do Postman para seu sistema operacional em [Downloads da Postman](https://www.postman.com/downloads/){target="_blank"}.

![Adobe I/O Nova integração](./images/getstarted.png)

1. Inicie o aplicativo.

No Postman, há dois conceitos: Ambientes e Coleções.

- O arquivo de ambiente contém todas as variáveis de ambiente mais ou menos consistentes. No ambiente, você encontrará informações como o IMSOrg do seu ambiente Adobe, além de credenciais de segurança como a ID do cliente e outras. Você baixou o arquivo de ambiente durante a configuração do Adobe I/O anteriormente e ele é nomeado como **`oauth_server_to_server.postman_environment.json`**.

- A coleção contém várias solicitações de API que podem ser usadas. Usaremos 2 coleções
   - 1 coleção para autenticação no Adobe I/O
   - 1 Coleta para os exercícios neste módulo

1. Baixe o [postman.zip](./../../../assets/postman/postman-ff.zip) no desktop local.

![Adobe I/O Nova integração](./images/pmfolder.png)

No arquivo **postman.zip** estão os seguintes arquivos:

    - `Adobe IO - OAuth.postman_collection.json`
    - `FF - Firefly Services Tech Insiders.postman_collection.json`

1. Descompacte o **postman-ff.zip** e armazene os 2 arquivos a seguir em uma pasta na sua área de trabalho:
- Adobe IO - OAuth.postman_collection.json
- FF - Firefly Services Tech Insiders.postman_collection.json
- oauth_server_to_server.postman_environment.json

![Adobe I/O Nova integração](./images/pmfolder1.png)

1. No Postman, selecione **Importar**.

![Adobe I/O Nova integração](./images/postmanui.png)

1. Selecione **Arquivos**.

![Adobe I/O Nova integração](./images/choosefiles.png)

1. Escolha os três arquivos da pasta e selecione **Abrir** e **Importar**.

![Adobe I/O Nova integração](./images/selectfiles.png)

![Adobe I/O Nova integração](./images/impconfirm.png)

Não, você tem tudo o que precisa no Postman para começar a interagir com os Serviços Firefly por meio das APIs.

## 1.1.1.5 Solicitar um token de acesso

Em seguida, para garantir que você esteja autenticado corretamente, é necessário solicitar um token de acesso.

1. Certifique-se de ter selecionado o ambiente correto antes de executar qualquer solicitação, verificando a lista suspensa Ambiente no canto superior direito. O Ambiente selecionado deve ter um nome semelhante a este, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/envselemea1.png)

O Ambiente selecionado deve ter um nome semelhante a este, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/envselemea.png)

Agora que o ambiente e as coleções do Postman estão configurados e funcionando, você pode autenticar do Postman para o Adobe I/O.

1. Na coleção **Adobe IO - OAuth**, selecione a solicitação denominada **POST - Obter Token de Acesso** e selecione **Enviar**.

Aviso em **Parâmetros de Consulta**, duas variáveis são referenciadas, `API_KEY` e `CLIENT_SECRET`. Essas variáveis foram obtidas do ambiente selecionado, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/ioauth.png)

Se for bem-sucedido, uma resposta contendo um token de portador, um token de acesso e uma janela de expiração será exibida na seção **Corpo** do Postman.

![Postman](./images/ioauthresp.png)


Você deve ver uma resposta semelhante contendo as seguintes informações:

| Chave | Valor |
|:-------------:| :---------------:| 
| token_type | **portador** |
| access_token | **keyJhbGciOiJSU...** |
| expires_in | **86399** |

O Adobe I/O **bearer-token** tem um valor específico (o access_token muito longo) e uma janela de expiração e agora é válido por 24 horas. Isso significa que, após 24 horas, se você quiser usar o Postman para autenticar no Adobe I/O, precisará gerar um novo token executando essa solicitação novamente.

## 1.1.1.6 API de serviços do Firefly, imagem do texto 2

Agora você está pronto para enviar sua primeira solicitação para as APIs de serviços do Firefly.

1. Selecione a solicitação denominada **POST - Firefly - T2I V3** da coleção **FF - Firefly Services Tech Insiders**.

![Firefly](./images/ff1.png)

1. Copie o URL da imagem da resposta e abra-o em seu navegador da Web para exibir a imagem.

![Firefly](./images/ff2.png)

Você deve ver uma bela imagem representando `horses in a field`.

![Firefly](./images/ff3.png)

Fique à vontade para brincar com a solicitação da API antes de continuar com o próximo exercício.

## Próximas etapas

Vá para [Otimizar seu processo de Firefly usando o Microsoft Azure e URLs pré-assinadas](./ex2.md){target="_blank"}

Retorne para [Visão Geral dos Serviços Adobe Firefly](./firefly-services.md){target="_blank"}

Voltar para [Todos os módulos](./../../../overview.md){target="_blank"}
