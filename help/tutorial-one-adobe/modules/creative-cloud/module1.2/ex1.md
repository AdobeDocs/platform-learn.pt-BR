---
title: Introdução ao Workfront Fusion
description: Introdução ao Workfront Fusion
kt: 5342
doc-type: tutorial
exl-id: 42e260e0-8af0-4d71-b634-48c1966bd912
source-git-commit: a4933bd49988cd16c4382ad4327d01ae58b52bbb
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 2%

---

# 1.2.1 Introdução ao Workfront Fusion

Neste exercício, você usará o Workfront Fusion e o Adobe I/O para consultar APIs de serviços de Adobe Firefly.

## 1.2.1.1 Criar novo cenário

Ir para [https://experience.adobe.com/](https://experience.adobe.com/). Clique para abrir o **Workfront Fusion**.

![WF Fusion](./images/wffusion1.png)

Você deverá ver isso. Vá para **Cenários**.

![WF Fusion](./images/wffusion2.png)

Clique em **Criar novo cenário**.

![WF Fusion](./images/wffusion3.png)

Você verá um cenário vazio. Clique no ícone **ferramentas** e selecione **Definir várias variáveis**.

![WF Fusion](./images/wffusion4.png)

Agora é necessário mover o ícone **relógio** para a **Definir várias variáveis** recém-adicionada.

![WF Fusion](./images/wffusion5.png)

Você verá isso.

![WF Fusion](./images/wffusion6.png)

Em seguida, clique com o botão direito no ponto de interrogação e selecione **Excluir módulo**.

![WF Fusion](./images/wffusion7.png)

Em seguida, clique com o botão direito no objeto **Definir várias variáveis** e selecione **Configurações**.

![WF Fusion](./images/wffusion8.png)

## 1.2.1.2 Configurar autenticação de Adobe I/O

Agora, é necessário configurar as variáveis necessárias para a autenticação no Adobe I/O. No exercício anterior, você criou um projeto Adobe I/O. As variáveis desse projeto Adobe I/O agora precisam ser definidas no Workfront Fusion.

As seguintes variáveis precisam ser definidas:

| Chave | Valor |
|:-------------:| :---------------:| 
| `CONST_client_id` | a ID do cliente do projeto Adobe I/O |
| `CONST_client_secret` | Segredo do cliente do seu projeto Adobe I/O |
| `CONST_scope` | seu escopo do projeto Adobe I/O |

Você pode encontrar essas variáveis acessando [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects) e abrindo o projeto Adobe I/O, denominado `--aepUserLdap-- Firefly`.

![WF Fusion](./images/wffusion9.png)

Em seu projeto, clique em **Servidor-Servidor-OAuth** para ver os valores das chaves acima.

![WF Fusion](./images/wffusion10.png)

Com as chaves e os valores acima, você pode configurar o objeto **Definir várias variáveis**. Clique em **Adicionar item**.

![WF Fusion](./images/wffusion11.png)

Insira o **Nome da variável**: **CONST_client_id** e seu **Valor da variável**, clique em **Adicionar**.

![WF Fusion](./images/wffusion12.png)

Clique em **Adicionar item**.

![WF Fusion](./images/wffusion13.png)

Insira o **nome da variável**: **CONST_client_secret** e seu **valor da variável**, clique em **Adicionar**.

![WF Fusion](./images/wffusion14.png)

Clique em **Adicionar item**.

![WF Fusion](./images/wffusion15.png)

Insira o **Nome da variável**: **CONST_scope** e seu **Valor da variável**, clique em **Adicionar**.

![WF Fusion](./images/wffusion16.png)

Clique em **OK**.

![WF Fusion](./images/wffusion17.png)

Passe o mouse sobre o objeto **Definir várias variáveis** e clique no ícone grande **+** para adicionar outro módulo.

![WF Fusion](./images/wffusion18.png)

Você deverá ver isso.

![WF Fusion](./images/wffusion19.png)

Na barra de pesquisa, digite **http**. Selecione **HTTP** para abri-lo.

![WF Fusion](./images/wffusion21.png)

e selecione **Fazer uma solicitação**.

![WF Fusion](./images/wffusion20.png)

| Chave | Valor |
|:-------------:| :---------------:| 
| `URL` | `https://ims-na1.adobelogin.com/ims/token/v3` |
| `Method` | `POST` |
| `Body Type` | `x-www-form-urlencoded` |

Clique em **Adicionar item**.

![WF Fusion](./images/wffusion22.png)

Adicione itens para cada um dos valores abaixo:

| Chave | Valor |
|:-------------:| :---------------:| 
| `client_id` | sua variável predefinida para `CONST_client_id` |
| `client_secret` | sua variável predefinida para `CONST_client_secret` |
| `scope` | sua variável predefinida para `CONST_scope` |
| `grant_type` | `client_credentials` |

Configuração para `client_id`.

![WF Fusion](./images/wffusion23.png)

Configuração para `client_secret`.

![WF Fusion](./images/wffusion25.png)

Configuração para `scope`.

![WF Fusion](./images/wffusion26.png)

Configuração para `grant_type`.

![WF Fusion](./images/wffusion28.png)

Visão geral da configuração. Role para baixo e marque a caixa de seleção para **Analisar resposta**. Clique em **OK**.

![WF Fusion](./images/wffusion27.png)

Você deverá ver isso. Clique em **Executar uma vez**.

![WF Fusion](./images/wffusion29.png)

Depois que o cenário for executado, você deverá ver isso.

![WF Fusion](./images/wffusion30.png)

Clique no ícone de **ponto de interrogação** no objeto **Definir várias variáveis** para ver o que aconteceu quando esse objeto foi executado.

![WF Fusion](./images/wffusion31.png)

Clique no ícone de **ponto de interrogação** no objeto **HTTP - Fazer uma solicitação** para ver o que aconteceu quando esse objeto foi executado. Na **SAÍDA**, você verá o **access_token** sendo retornado pelo Adobe I/O.

![WF Fusion](./images/wffusion32.png)

Passe o mouse sobre o objeto **HTTP - Fazer uma solicitação** e clique no ícone **+** para adicionar outro módulo.

![WF Fusion](./images/wffusion33.png)

Na barra de pesquisa, procure por `tools`. Selecione **Ferramentas**.

![WF Fusion](./images/wffusion34.png)

Selecione **Definir várias variáveis**.

![WF Fusion](./images/wffusion35.png)

Selecione **Adicionar item**.

![WF Fusion](./images/wffusion36.png)

Defina o **Nome da variável** como `bearer_token`. Selecione `access_token` como o **Valor da variável** dinâmica. Clique em **Adicionar**.

![WF Fusion](./images/wffusion37.png)

Você deveria ficar com isso. Clique em **OK**.

![WF Fusion](./images/wffusion38.png)

Clique novamente em **Executar uma vez**.

![WF Fusion](./images/wffusion39.png)

Depois que o cenário for executado, clique no ícone **ponto de interrogação** no último objeto **Definir várias variáveis**. Você deverá ver que o access_token está sendo armazenado na variável `bearer_token`.

![WF Fusion](./images/wffusion40.png)

Em seguida, clique com o botão direito no primeiro objeto **Definir vários valores** e selecione **Renomear**.

![WF Fusion](./images/wffusion41.png)

Defina o nome como **Inicializar constantes**. Clique em **OK**.

![WF Fusion](./images/wffusion42.png)

Renomeie o segundo objeto e defina o nome como **Autenticar para Adobe I/O**. Clique em **OK**.

![WF Fusion](./images/wffusion43.png)

Renomeie o terceiro objeto e defina o nome como **Definir Token de Portador**. Clique em **OK**.

![WF Fusion](./images/wffusion44.png)

Você deveria ficar com isso.

![WF Fusion](./images/wffusion45.png)

Em seguida, altere o nome do cenário para `--aepUSerLdap-- - Adobe I/O Authentication`.

![WF Fusion](./images/wffusion46.png)

Clique em **Salvar**.

![WF Fusion](./images/wffusion47.png)

Próxima etapa: [1.2.2 Usar APIs Adobe no Workfront Fusion](./ex2.md)

[Voltar ao módulo 1.2](./automation.md)

[Voltar a todos os módulos](./../../../overview.md)
