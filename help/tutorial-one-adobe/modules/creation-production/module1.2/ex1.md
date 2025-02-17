---
title: Introdução ao Workfront Fusion
description: Saiba como usar o Workfront Fusion e o Adobe I/O para consultar APIs de serviços da Adobe Firefly
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 42e260e0-8af0-4d71-b634-48c1966bd912
source-git-commit: b083a817700320e8e45645702c2868423c1fae99
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 1%

---

# 1.2.1 Introdução ao Workfront Fusion

Saiba como usar o Workfront Fusion e o Adobe I/O para consultar as APIs de serviços da Adobe Firefly.

## 1.2.1.1 Criar novo cenário

1. Ir para [https://experience.adobe.com/](https://experience.adobe.com/). Abra o **Workfront Fusion**.

   ![WF Fusion](./images/wffusion1.png)

1. Vá para **Cenários**.

   ![WF Fusion](./images/wffusion2.png)

1. Selecione **Criar novo cenário**.

   ![WF Fusion](./images/wffusion2a.png)

1. Nomeie a pasta `--aepUserLdap--` e selecione **Salvar**.

   ![WF Fusion](./images/wffusion2b.png)

1. Selecione sua pasta e, em seguida, selecione **Criar novo cenário**.

   ![WF Fusion](./images/wffusion3.png)

1. Um cenário vazio é exibido, selecione **ferramentas** e selecione **Definir várias variáveis**.

   ![WF Fusion](./images/wffusion4.png)

1. Mova o ícone **relógio** para a **Set multiple variables** recém-adicionada.

   ![WF Fusion](./images/wffusion5.png)

   Sua tela deve ter esta aparência.

   ![WF Fusion](./images/wffusion6.png)

1. Clique com o botão direito no ponto de interrogação e selecione **Excluir módulo**.

   ![WF Fusion](./images/wffusion7.png)

1. Em seguida, clique com o botão direito em **Definir várias variáveis** e selecione **Configurações**.

   ![WF Fusion](./images/wffusion8.png)

## 1.2.1.2 Configurar a autenticação do Adobe I/O

Agora, é necessário configurar as variáveis necessárias para autenticar no Adobe I/O. No exercício anterior, você criou um projeto do Adobe I/O. As variáveis desse projeto do Adobe I/O agora precisam ser definidas no Workfront Fusion.

As seguintes variáveis precisam ser definidas:

| Chave | Valor |
|:-------------:| :---------------:| 
| `CONST_client_id` | a ID do cliente do projeto do Adobe I/O |
| `CONST_client_secret` | Segredo do cliente do seu projeto do Adobe I/O |
| `CONST_scope` | o escopo do projeto do Adobe I/O |

1. Encontre essas variáveis acessando [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects) e abrindo o projeto do Adobe I/O, chamado `--aepUserLdap-- Firefly`.

   ![WF Fusion](./images/wffusion9.png)

1. Em seu projeto, selecione **OAuth Serverto-Server** para ver os valores das chaves acima.

   ![WF Fusion](./images/wffusion10.png)

1. Usando as chaves e os valores acima, você pode configurar o objeto **Definir várias variáveis**. Selecione **Adicionar item**.

   ![WF Fusion](./images/wffusion11.png)

1. Insira o **nome da variável**: **CONST_client_id** e seu **valor da variável**, selecione **Adicionar**.

   ![WF Fusion](./images/wffusion12.png)

1. Selecione **Adicionar item**.

   ![WF Fusion](./images/wffusion13.png)

1. Insira o **nome da variável**: **CONST_client_secret** e seu **valor da variável**, selecione **Adicionar**.

   ![WF Fusion](./images/wffusion14.png)

1. Selecione **Adicionar item**.

   ![WF Fusion](./images/wffusion15.png)

1. Insira o **nome da variável**: **CONST_scope** e seu **valor da variável**, selecione **Adicionar**.

   ![WF Fusion](./images/wffusion16.png)

1. Selecione **OK**.

   ![WF Fusion](./images/wffusion17.png)

1. Passe o mouse sobre **Definir várias variáveis** e selecione o ícone grande **+** para adicionar outro módulo.

   ![WF Fusion](./images/wffusion18.png)

   Sua tela deve ter esta aparência.

   ![WF Fusion](./images/wffusion19.png)

1. Na barra de pesquisa, digite **http**. Selecione **HTTP** para abri-lo.

   ![WF Fusion](./images/wffusion21.png)

1. Selecione **Fazer uma solicitação**.

   ![WF Fusion](./images/wffusion20.png)

   | Chave | Valor |
   |:-------------:| :---------------:| 
   | `URL` | `https://ims-na1.adobelogin.com/ims/token/v3` |
   | `Method` | `POST` |
   | `Body Type` | `x-www-form-urlencoded` |

1. Selecione **Adicionar item**.

   ![WF Fusion](./images/wffusion22.png)

1. Adicione itens para cada um dos valores abaixo:

   | Chave | Valor |
   |:-------------:| :---------------:| 
   | `client_id` | sua variável predefinida para `CONST_client_id` |
   | `client_secret` | sua variável predefinida para `CONST_client_secret` |
   | `scope` | sua variável predefinida para `CONST_scope` |
   | `grant_type` | `client_credentials` |

1. Configuração para `client_id`:

   ![WF Fusion](./images/wffusion23.png)

1. Configuração para `client_secret`.

   ![WF Fusion](./images/wffusion25.png)

1. Configuração para `scope`.

   ![WF Fusion](./images/wffusion26.png)

1. Configuração para `grant_type`.

   ![WF Fusion](./images/wffusion28.png)

1. Role para baixo e marque a caixa para **Analisar resposta**. Selecione **OK**.

   ![WF Fusion](./images/wffusion27.png)

1. Sua tela deve ter esta aparência. Selecione **Executar uma vez**.

   ![WF Fusion](./images/wffusion29.png)

   Depois que o cenário for executado, sua tela deverá ter esta aparência:

   ![WF Fusion](./images/wffusion30.png)

1. Selecione o ícone de **ponto de interrogação** no objeto **Definir várias variáveis** para ver o que aconteceu quando esse objeto foi executado.

   ![WF Fusion](./images/wffusion31.png)

1. Selecione o ícone de **ponto de interrogação** no objeto **HTTP - Fazer uma solicitação** para ver o que aconteceu quando esse objeto foi executado. Na **SAÍDA**, consulte o **access_token** que está sendo retornado pela Adobe I/O.

   ![WF Fusion](./images/wffusion32.png)

1. Passe o mouse sobre **HTTP - Faça uma solicitação** e selecione o ícone **+** para adicionar outro módulo.

   ![WF Fusion](./images/wffusion33.png)

1. Na barra de pesquisa, procure por `tools`. Selecione **Ferramentas**.

   ![WF Fusion](./images/wffusion34.png)

1. Selecione **Definir várias variáveis**.

   ![WF Fusion](./images/wffusion35.png)

1. Selecione **Adicionar item**.

   ![WF Fusion](./images/wffusion36.png)

1. Definir **Nome da variável** como `bearer_token`. Selecione `access_token` como o **Valor da variável** dinâmica. Selecione **Adicionar**.

   ![WF Fusion](./images/wffusion37.png)

1. Sua tela deve ter esta aparência. Selecione **OK**.

   ![WF Fusion](./images/wffusion38.png)

1. Selecione **Executar uma vez** novamente.

   ![WF Fusion](./images/wffusion39.png)

1. Depois que o cenário for executado, selecione o ícone **ponto de interrogação** no último objeto **Definir várias variáveis**. Você deve ver que o access_token está sendo armazenado na variável `bearer_token`.

   ![WF Fusion](./images/wffusion40.png)

1. Em seguida, clique com o botão direito no primeiro objeto **Definir vários valores** e selecione **Renomear**.

   ![WF Fusion](./images/wffusion41.png)

1. Defina o nome como **Inicializar constantes**. Selecione **OK**.

   ![WF Fusion](./images/wffusion42.png)

1. Renomeie o segundo objeto para **Autenticar para o Adobe I/O**. Selecione **OK**.

   ![WF Fusion](./images/wffusion43.png)

1. Renomeie o terceiro objeto para **Definir Token de Portador**. Selecione **OK**.

   ![WF Fusion](./images/wffusion44.png)

   Sua tela deve ter esta aparência:

   ![WF Fusion](./images/wffusion45.png)

1. Em seguida, altere o nome do cenário para `--aepUSerLdap-- - Adobe I/O Authentication`.

   ![WF Fusion](./images/wffusion46.png)

1. Selecione **Salvar**.

   ![WF Fusion](./images/wffusion47.png)

## Próximas etapas

Ir para [Usar APIs do Adobe no Workfront Fusion](./ex2.md){target="_blank"}

Volte para [Automatização dos Serviços Adobe Firefly](./automation.md){target="_blank"}

Voltar para [Todos os Módulos](./../../../overview.md){target="_blank"}
