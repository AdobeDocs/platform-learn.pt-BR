---
title: Assimilar e analise dados do Google Analytics no Adobe Experience Platform com o Conector de Source do BigQuery - Conectar GCP e BigQuery à Adobe Experience Platform
description: Assimilar e analise dados do Google Analytics no Adobe Experience Platform com o Conector de Source do BigQuery - Conectar GCP e BigQuery à Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: 86b04b4e-0439-4491-b700-5b0591c493b7
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '1757'
ht-degree: 1%

---

# 4.2.3 Conectar o GCP e o BigQuery ao Adobe Experience Platform

## Objetivos

- Explore a API e os serviços na Google Cloud Platform
- Estar familiarizado com o OAuth Playground para testar APIs do Google
- Crie sua primeira conexão do BigQuery no Adobe Experience Platform

## Contexto

A Adobe Experience Platform fornece um conector em **Fontes** que ajudará você a trazer conjuntos de dados do BigQuery para a Adobe Experience Platform. Esse conector de dados é baseado na API do Google BigQuery. Portanto, é importante preparar corretamente a Plataforma de nuvem do Google e o ambiente do BigQuery para receber chamadas de API da Adobe Experience Platform.

Para configurar o Conector do Source do BigQuery no Adobe Experience Platform, você precisará desses 4 valores:

- projeto
- clientId
- clientSecret
- refreshToken

Até agora você só tem o primeiro, a **ID do Projeto**. Esse valor de **ID do projeto** é uma ID aleatória que foi gerada pela Google quando você criou seu projeto BigQuery durante o exercício 12.1.

Copie a ID do projeto em um arquivo de texto separado.

| Credencial | Nomenclatura | Exemplo |
| ----------------- |-------------| -------------|
| ID do projeto | random | composto-tarefa-306413 |

Você pode verificar sua ID de projeto a qualquer momento clicando em seu **Nome do projeto** na barra de menu superior:

![demonstração](./images/ex1/projectMenu.png)

Você verá a ID do projeto no lado direito:

![demonstração](./images/ex1/projetcselection.png)

Neste exercício, você aprenderá a obter os outros 3 campos obrigatórios:

- clientId
- clientSecret
- refreshToken

## 4.2.3.1 API e serviços da nuvem do Google

Para iniciar, volte para a página inicial da Google Cloud Platform. Para fazer isso, basta clicar no logotipo no canto superior esquerdo da tela.

![demonstração](./images/ex2/5.png)

Quando você estiver na página inicial, vá para o menu esquerdo e clique em **APIs e serviços** e, em seguida, clique em **Painel**.

![demonstração](./images/ex2/4.png)

Você verá agora a página inicial de **APIs e serviços**.

![demonstração](./images/ex2/6.png)

Nesta página, você pode ver o uso de suas várias conexões de API do Google. Para configurar uma Conexão de API para que o Adobe Experience Platform possa ler a partir do BigQuery, é necessário seguir estas etapas:

- Primeiro, é necessário criar uma tela de consentimento OAuth para habilitar autenticações futuras. As razões de segurança da Google também exigem que um ser humano faça a primeira autenticação, antes que um acesso programático seja permitido.
- Em segundo lugar, você precisa de credenciais de API (clientId e clientSecret) que serão usadas para autenticação de API e acesso ao seu conector BigQuery.

## 4.2.3.2 Tela de consentimento do OAuth

Vamos começar com a criação da Tela de consentimento do OAuth. No menu esquerdo da página inicial de **APIs e serviços**, clique em **Tela de consentimento do OAuth**.

![demonstração](./images/ex2/6-1a.png)

Você verá isto:

![demonstração](./images/ex2/6-1.png)

Selecione o Tipo de Usuário: **Externo**. Em seguida, clique em **CRIAR**.

![demonstração](./images/ex2/6-2.png)

Você estará na **janela Configuração da tela de consentimento do OAuth**.

Aqui, basta inserir o nome da tela de consentimento no campo **Nome do aplicativo** e selecionar o **Email de suporte do usuário**. Para o Nome do aplicativo, use esta convenção de nomenclatura:

| Nomenclatura | Exemplo |
| ----------------- |-------------| 
| `--aepUserLdap-- - AEP BigQuery Connector` | vangeluw - Conector do AEP BigQuery |

![demonstração](./images/ex2/6-3.png)

Em seguida, role para baixo até ver **Informações de contato do desenvolvedor** e preencha um endereço de email.

![demonstração](./images/ex2/6-3a.png)

Clique em **SALVAR E CONTINUAR**.

![demonstração](./images/ex2/6-4.png)

Você verá isso. Clique em **SALVAR E CONTINUAR**.

![demonstração](./images/ex2/o1.png)

Você verá isso. Clique em **SALVAR E CONTINUAR**.

![demonstração](./images/ex2/o2.png)

Você verá isso. Clique em **VOLTAR AO PAINEL**.

![demonstração](./images/ex2/o3.png)

Você verá isso. Clique em **PUBLISH APP**.

![demonstração](./images/ex2/o4.png)

Clique em **CONFIRM**.

![demonstração](./images/ex2/o5.png)

Você verá isso.

![demonstração](./images/ex2/o6.png)

Na próxima etapa, você concluirá a configuração da API e obterá suas credenciais de API.

## 4.2.3.3 Credenciais da API do Google: segredo do cliente e ID do cliente

No menu esquerdo, clique em **Credenciais**. Você verá isto:

![demonstração](./images/ex2/7.png)

Clique no botão **+ CRIAR CREDENCIAIS**.

![demonstração](./images/ex2/9.png)

Você verá três opções. Clique na **ID do cliente OAuth**:

![demonstração](./images/ex2/11.png)

Na próxima tela, selecione **Aplicativo web**.

![demonstração](./images/ex2/12.png)

Vários novos campos aparecerão. Agora é necessário inserir o **Nome** da ID de Cliente OAuth e também inserir os **URIs de redirecionamento autorizados**.

Siga esta convenção de nomenclatura:

| Campo | Valor | Exemplo |
| ----------------- |-------------| -------------| 
| Nome | ldap - Conector AEP BigQuery | vangeluw - Conector do Platform BigQuery |
| URIs de redirecionamento autorizados | https://developers.google.com/oauthplayground | https://developers.google.com/oauthplayground |

O campo **URIs de redirecionamento autorizados** é muito importante porque você precisará dele mais tarde para obter o RefreshToken necessário para concluir a configuração do Conector de Source do BigQuery no Adobe Experience Platform.

![demonstração](./images/ex2/12-1.png)

Antes de continuar, você precisa pressionar fisicamente o botão **Inserir** depois de inserir a URL para armazenar o valor no campo **URIs de redirecionamento autorizados**. Se você não clicar no botão **Inserir**, ocorrerão problemas posteriormente, no **Playground do OAuth 2.0**.

Em seguida, clique em **Criar**:

![demonstração](./images/ex2/19.png)

Agora você verá sua ID do cliente e seu Segredo do cliente.

![demonstração](./images/ex2/20.png)

Copie estes dois campos e cole-os em um arquivo de texto na sua área de trabalho. Você sempre pode acessar essas credenciais em um estágio posterior, mas é mais fácil salvá-las em um arquivo de texto ao lado da ID do projeto do BigQuery.

Para recapitular a configuração do BigQuery Source Connector no Adobe Experience Platform, agora você já tem esses valores disponíveis:

| Credenciais do BigQuery Connector | Valor |
| ----------------- |-------------| 
| ID do projeto | sua própria ID do projeto (por exemplo,: composer-task-306413) |
| clientid | yourclientid |
| cilentsecret | yourclientsecret |


O **refreshToken** ainda está ausente. O refreshToken é um requisito por motivos de segurança. No mundo das APIs, os tokens normalmente expiram a cada 24 horas. Portanto, o **refreshToken** é necessário para atualizar o token de segurança a cada 24 horas, para que a instalação do Source Connector possa continuar se conectando à Google Cloud Platform e ao BigQuery.

## 4.2.3.4 API do BigQuery e o refreshToken

Há muitas maneiras de obter um refreshToken para acessar as APIs da Google Cloud Platform. Uma dessas opções é, por exemplo, usar o Postman.
No entanto, o Google criou algo mais fácil de testar e reproduzir com suas APIs, uma ferramenta chamada **Playground do OAuth 2.0**.

Para acessar o **Playground do OAuth 2.0**, vá para [https://developers.google.com/oauthplayground](https://developers.google.com/oauthplayground).

Você verá a página inicial do **Playground** do OAuth 2.0.

![demonstração](./images/ex2/22.png)

Clique no ícone de **engrenagem** na parte superior direita da tela:

![demonstração](./images/ex2/22-1.png)

Verifique se as configurações são as mesmas que você pode ver na imagem acima.

Verifique novamente as configurações para ter 100% de certeza.

Quando terminar, marque a caixa de **Usar suas próprias credenciais do OAuth**

![demonstração](./images/ex2/22-2.png)

Dois campos devem aparecer e você tem o valor para eles.

![demonstração](./images/ex2/23.png)

Preencha os campos após esta tabela:

| Configurações da API do Playground | Suas credenciais da API do Google |
| ----------------- |-------------| 
| ID do cliente OAuth | sua ID do cliente (no arquivo de texto da área de trabalho) |
| Segredo do cliente OAuth | seu próprio Segredo do cliente (no arquivo de texto da área de trabalho) |

![demonstração](./images/ex2/23-a.png)

Copie a **ID do Cliente** e o **Segredo do Cliente** do arquivo de texto criado na área de trabalho.

![demonstração](./images/ex2/20.png)

Depois de preencher suas credenciais, clique em **Fechar**

![demonstração](./images/ex2/23-1.png)

No menu esquerdo, você pode ver todas as APIs do Google disponíveis. Pesquise por **BigQuery API v2**.

![demonstração](./images/ex2/27.png)

Em seguida, selecione o escopo conforme indicado na imagem abaixo:

![demonstração](./images/ex2/26.png)

Depois de selecioná-los, você verá um botão azul que diz **Autorizar APIs**. Clique nele.

![demonstração](./images/ex2/28.png)

Selecione a Conta da Google usada para configurar o GCP e o BigQuery.

Você pode ver um grande aviso: **Este aplicativo não foi verificado**. Isso está acontecendo porque seu Conector da Platform BigQuery ainda não foi revisado formalmente, portanto, a Google não sabe se é um aplicativo autêntico ou não. Você deve ignorar essa notificação.

Clique em **Avançado**.

![demonstração](./images/ex2/32.png)

Em seguida, clique em **Ir para ldap - Conector AEP BigQuery (não seguro)**.

![demonstração](./images/ex2/33.png)

Você será redirecionado para nossa Tela de consentimento OAuth criada.

![demonstração](./images/ex2/29.png)

Se você usar a Autenticação de dois fatores (2FA), insira o código de verificação enviado a você.

![demonstração](./images/ex2/30.png)

O Google mostrará oito prompts de **Permissão** diferentes. Clique em **Permitir** para todas as oito solicitações de permissão. (Esse é um procedimento que deve ser seguido e confirmado uma vez por um ser humano real, antes que a API permita solicitações programáticas)

Novamente, **oito janelas pop-up diferentes** não serão exibidas. Clique em **Permitir** para todas elas.

![demonstração](./images/ex2/29.png)

Após as oito solicitações de permissão, você verá esta visão geral. Clique em **Permitir** para concluir o processo.

![demonstração](./images/ex2/35.png)

Após o último clique de **Permitir**, você será redirecionado para o Playground do OAuth 2.0 e verá o seguinte:

![demonstração](./images/ex2/36.png)

Clique em **Código de autorização do Exchange para tokens**.

![demonstração](./images/ex2/36-1.png)

Após alguns segundos, a exibição **Etapa 2 - Código de autorização do Exchange para tokens** será fechada automaticamente, e você verá **Etapa 3 - Configurar solicitação para API**.

Você precisa voltar para a **Etapa 2 do código de autorização do Exchange para tokens**, portanto, clique na **Etapa 2 do código de autorização do Exchange para tokens** novamente para visualizar o **Atualizar token**.

![demonstração](./images/ex2/37.png)

Você verá agora o **token de atualização**.

![demonstração](./images/ex2/38.png)

Copie o **token de atualização** e cole-o no arquivo de texto na área de trabalho junto com as outras Credenciais do BigQuery Source Connector:

| Credenciais do BigQuery Source Connector | Valor |
| ----------------- |-------------| 
| ID do projeto | sua própria ID de projeto aleatória (por exemplo,: apt-summer-273608) |
| clientid | yourclientid |
| cilentsecret | yourclientsecret |
| refreshtoken | yourrefreshtoken |

Em seguida, vamos configurar seu Source Connector no Adobe Experience Platform.

## 4.2.3.5 - Conectar a Platform com sua própria tabela do BigQuery

Faça logon no Adobe Experience Platform acessando esta URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepSandboxName--``. Depois de selecionar a sandbox apropriada, você verá a alteração da tela e agora estará em sua sandbox dedicada.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/sb1.png)

No menu esquerdo, vá para Origens. Você verá a página inicial de **Fontes**. No menu **Fontes**, clique em **Bancos de dados**. Clique no cartão **Google BigQuery**. Em seguida, clique em **Configurar** ou **+ Configurar**.

![demonstração](./images/1.png)

Agora você deve criar uma nova conexão.

Clique em **Nova conta**. Agora é necessário preencher todos os campos abaixo, com base na configuração que você fez no GCP e no BigQuery.

![demonstração](./images/3.png)

Vamos começar nomeando a conexão:

Use esta convenção de nomenclatura:

| Credenciais do BigQuery Connector | Valor | Exemplo |
| ----------------- |-------------| -------------| 
| Nome da conta | `--aepUserLdap-- - BigQuery Connection` | vangeluw - Conexão BigQuery |
| Descrição | `--aepUserLdap-- - BigQuery Connection` | vangeluw - Conexão BigQuery |

O que deve dar a você algo como isso:

![demonstração](./images/ex2/39-a.png)

Em seguida, preencha os detalhes do GCP e da API do BigQuery **Autenticação de conta** que você armazenou em um arquivo de texto na sua área de trabalho:

| Credenciais do BigQuery Connector | Valor |
| ----------------- |-------------| 
| ID do projeto | sua própria ID de projeto aleatória (por exemplo,: apt-summer-273608) |
| clientId | ... |
| clientSecret | ... |
| refreshToken | ... |

Os detalhes da **Autenticação da Conta** agora devem ter esta aparência:

![demonstração](./images/ex2/39-xx.png)

Após preencher todos esses campos, clique em **Conectar à origem**.

![demonstração](./images/ex2/39-2.png)

Se os detalhes da **Autenticação da Conta** foram preenchidos corretamente, você verá agora uma confirmação visual de que a conexão está funcionando corretamente, ao ver a confirmação **Conectado**.

![demonstração](./images/ex2/projectid.png)

Agora que sua conexão foi criada, clique em **Avançar**:

![demonstração](./images/42.png)

Agora você verá o conjunto de dados do BigQuery criado durante o exercício 12.2.

![demonstração](./images/datasets.png)

Muito bem! No próximo exercício, você carregará dados dessa tabela e os mapeará em relação a um esquema e conjunto de dados na Adobe Experience Platform.

Próxima etapa: [4.2.4 Carregar dados do BigQuery no Adobe Experience Platform](./ex4.md)

[Voltar ao módulo 4.2](./customer-journey-analytics-bigquery-gcp.md)

[Voltar a todos os módulos](./../../../overview.md)
