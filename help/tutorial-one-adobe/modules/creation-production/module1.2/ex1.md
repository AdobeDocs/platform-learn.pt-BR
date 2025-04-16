---
title: Introdução ao Workfront Fusion
description: Learn how to use Workfront Fusion and Adobe I/O to query Adobe Firefly Services APIs
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 42e260e0-8af0-4d71-b634-48c1966bd912
source-git-commit: 603e48e0453911177823fe7ceb340f8ca801c5e1
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 1%

---

# 1.2.1 Getting started with Workfront Fusion

Saiba como usar o Workfront Fusion e o Adobe I/O para consultar APIs do Adobe Firefly Services.

## 1.2.1.1 Criar novo cenário

Ir para [https://experience.adobe.com/](https://experience.adobe.com/). Abra o **Workfront Fusion**.

![WF Fusion](./images/wffusion1.png)

Vá para **Cenários**.

![WF Fusion](./images/wffusion2.png)

Click the **+ icon** to create a new folder for your work.

![WF Fusion](./images/wffusion2a.png)

Name the folder `--aepUserLdap--` and select **Save**.

![WF Fusion](./images/wffusion2b.png)

Select your folder, and then select **Create new scenario**.

![WF Fusion](./images/wffusion3.png)

An empty scenario appears, select **tools** and select **Set multiple variables**.

![WF Fusion](./images/wffusion4.png)

Move the **clock** icon onto the newly added **Set multiple variables**.

![WF Fusion](./images/wffusion5.png)

Sua tela deve ter esta aparência.

![WF Fusion](./images/wffusion6.png)

Clique com o botão direito no ponto de interrogação e selecione **Excluir módulo**.

![WF Fusion](./images/wffusion7.png)

Próximo, clique com o botão direito do mouse em **Definir várias** variáveis e selecione **Configurações**.

![WF Fusion](./images/wffusion8.png)

## 1.2.1.2 Configurar a autenticação do Adobe I/O

Agora, é necessário configurar as variáveis necessárias para autenticar no Adobe I/O. No exercício anterior, você criou um projeto do Adobe I/O. As variáveis desse projeto do Adobe I/O agora precisam ser definidas no Workfront Fusion.

As seguintes variáveis precisam ser definidas:

| Chave | Valor |
|:-------------:| :---------------:| 
| `CONST_client_id` | a ID do cliente do projeto do Adobe I/O |
| `CONST_client_secret` | Segredo do cliente do seu projeto do Adobe I/O |
| `CONST_scope` | o escopo do projeto do Adobe I/O |

Encontre essas variáveis acessando [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects) e abrindo o projeto do Adobe I/O, chamado `--aepUserLdap-- One Adobe tutorial`.

![WF Fusion](./images/wffusion9.png)

No seu projeto, selecione **OAuth Serverto-Server** para ver os valores das chaves acima.

![WF Fusion](./images/wffusion10.png)

Usando as chaves e os valores acima, é possível configurar o **objeto Definir várias variáveis** . Selecione **Adicionar item**.

![WF Fusion](./images/wffusion11.png)

Insira o **nome da variável**: **CONST_client_id** e seu **valor da variável**, selecione **Adicionar**.

![WF Fusion](./images/wffusion12.png)

Selecione **Adicionar item**.

![WF Fusion](./images/wffusion13.png)

Enter **Variable name**: **CONST_client_secret** and its **Variable value**, select **Add**.

![WF Fusion](./images/wffusion14.png)

Selecione **Adicionar item**.

![WF Fusion](./images/wffusion15.png)

Insira o **nome da variável**: **CONST_scope** e seu **valor da variável**, selecione **Adicionar**.

![WF Fusion](./images/wffusion16.png)

Selecione **OK**.

![WF Fusion](./images/wffusion17.png)

Passe o mouse sobre **Definir várias variáveis** e selecione o ícone grande **+** para adicionar outra módulo.

![WF Fusion](./images/wffusion18.png)

Sua tela deve parecer curtir isso.

![WF Fusion](./images/wffusion19.png)

Na barra pesquisa, insira **http**. Selecione **HTTP** para abri-lo.

![WF Fusion](./images/wffusion21.png)

Selecione **Fazer uma solicitação**.

![WF Fusion](./images/wffusion20.png)

| Chave | Valor |
|:-------------:| :---------------:| 
| `URL` | `https://ims-na1.adobelogin.com/ims/token/v3` |
| `Method` | `POST` |
| `Body Type` | `x-www-form-urlencoded` |

Selecione **Adicionar item**.

![WF Fusion](./images/wffusion22.png)

Adicione itens para cada um dos valores abaixo:

| Chave | Valor |
|:-------------:| :---------------:| 
| `client_id` | sua variável predefinida para `CONST_client_id` |
| `client_secret` | sua variável predefinida para `CONST_client_secret` |
| `scope` | sua variável predefinida para `CONST_scope` |
| `grant_type` | `client_credentials` |

Configuration for `client_id`:

![WF Fusion](./images/wffusion23.png)

Configuração para `client_secret`.

![WF Fusion](./images/wffusion25.png)

Configuration for `scope`.

![WF Fusion](./images/wffusion26.png)

Configuration for `grant_type`.

![WF Fusion](./images/wffusion28.png)

Scroll down and check the box for **Parse response**. Selecione **OK**.

![WF Fusion](./images/wffusion27.png)

Sua tela deve ter esta aparência. Selecione **Executar uma vez**.

![WF Fusion](./images/wffusion29.png)

Depois que o cenário for executado, sua tela deverá ficar curtir:

![WF Fusion](./images/wffusion30.png)

Selecione o ícone de **ponto de interrogação** no objeto **Definir várias variáveis** para ver o que aconteceu quando esse objeto foi executado.

![WF Fusion](./images/wffusion31.png)

Selecione o ícone de **ponto de interrogação** no objeto **HTTP - Fazer uma solicitação** para ver o que aconteceu quando esse objeto foi executado. Na **SAÍDA**, consulte o **access_token** que está sendo retornado pela Adobe I/O.

![WF Fusion](./images/wffusion32.png)

Passe o mouse sobre **HTTP - Faça uma solicitação** e selecione o ícone **+** para adicionar outro módulo.

![WF Fusion](./images/wffusion33.png)

Na barra de pesquisa, procure por `tools`. Selecione **Ferramentas**.

![WF Fusion](./images/wffusion34.png)

Selecione **Definir várias variáveis**.

![WF Fusion](./images/wffusion35.png)

Selecione **Adicionar item**.

![WF Fusion](./images/wffusion36.png)

Defina **Variável nome** como `bearer_token`. Selecione `access_token` como o valor **do Variável dinâmico**. Selecione **Adicionar**.

![WF Fusion](./images/wffusion37.png)

Sua tela deve ter esta aparência. Selecione **OK**.

![WF Fusion](./images/wffusion38.png)

Selecione **Executar uma vez** novamente.

![WF Fusion](./images/wffusion39.png)

Depois que o cenário for executado, selecione o ícone **ponto de interrogação** no último objeto **Definir várias variáveis**. Você deve ver que o access_token está sendo armazenado na variável `bearer_token`.

![WF Fusion](./images/wffusion40.png)

Em seguida, clique com o botão direito no primeiro objeto **Definir vários valores** e selecione **Renomear**.

![WF Fusion](./images/wffusion41.png)

Defina o nome como **Inicializar constantes**. Selecione **OK**.

![WF Fusion](./images/wffusion42.png)

Renomear o segundo objeto a **Ser autenticado para E/S** Adobe Systems. Selecione **OK**.

![WF Fusion](./images/wffusion43.png)

Renomear o terceiro objeto para **definir o token** portador. Selecione **OK**.

![WF Fusion](./images/wffusion44.png)

Sua tela deve ter esta aparência:

![WF Fusion](./images/wffusion45.png)

Em seguida, altere o nome do cenário para `--aepUSerLdap-- - Adobe I/O Authentication`.

![WF Fusion](./images/wffusion46.png)

Selecione **Salvar**.

![WF Fusion](./images/wffusion47.png)

## Próximas etapas

Ir para [Usar APIs do Adobe no Workfront Fusion](./ex2.md){target="_blank"}

Retorne ao [Creative Workflow Automation with Workfront Fusion](./automation.md){target="_blank"}

Voltar para [Todos os Módulos](./../../../overview.md){target="_blank"}
