---
title: CDP em tempo real - Crie um segmento e execute ações - Crie um segmento
description: CDP em tempo real - Crie um segmento e execute ações - Crie um segmento
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: c0778e81-4282-433d-9e02-37e32bf370ef
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 2%

---

# 6.1 Criar um segmento

Neste exercício, você criará um segmento usando o construtor de segmentos do Adobe Experience Platform.

## 6.1.1 Contexto

No mundo de hoje, responder ao comportamento de um cliente precisa ser em tempo real. Uma das maneiras de responder ao comportamento do cliente em tempo real é usando um segmento, na condição de que o segmento se qualifique em tempo real. Neste exercício, você precisa criar um segmento, levando em conta a atividade real no site que temos usado.

## 6.1.2 Identifique o comportamento ao qual deseja reagir

Ir para [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Depois de fazer logon com sua Adobe ID, você verá isso. Clique no projeto do seu site para abri-lo.

![DSN](../module0/images/web8.png)

Agora você pode seguir o fluxo abaixo para acessar o site. Clique em **Integrações**.

![DSN](../module0/images/web1.png)

No **Integrações** , é necessário selecionar a propriedade Data Collection criada no exercício 0.1.

![DSN](../module0/images/web2.png)

Você verá seu site de demonstração aberto. Selecione o URL e copie-o para a área de transferência.

![DSN](../module0/images/web3.png)

Abra uma nova janela incógnita do navegador.

![DSN](../module0/images/web4.png)

Cole o URL do site de demonstração, que você copiou na etapa anterior. Em seguida, você será solicitado a fazer logon usando sua Adobe ID.

![DSN](../module0/images/web5.png)

Selecione o tipo de conta e conclua o processo de logon.

![DSN](../module0/images/web6.png)

Você verá seu site carregado em uma janela incógnita do navegador. Para cada demonstração, você precisará usar uma nova janela incógnita do navegador para carregar o URL do site de demonstração.

![DSN](../module0/images/web7.png)

Neste exemplo, você deseja responder a um cliente específico que visualiza um produto específico.
No **Luma** homepage, vá para **Homens** e clique no produto **JACKSHIRT DE ADEQUAÇÃO DO PROTEUS**.

![Assimilação de dados](./images/homenadia.png)

Assim, quando alguém visitar a página do produto para **JACKSHIRT DE ADEQUAÇÃO DO PROTEUS**, você deseja poder tomar medidas. A primeira coisa a fazer para agir é definir um segmento.

![Assimilação de dados](./images/homenadiapp.png)

## 6.1.3 Criar o segmento

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você será direcionado para a página inicial do Adobe Experience Platform.

![Assimilação de dados](../module2/images/home.png)

Antes de continuar, é necessário selecionar um **sandbox**. A sandbox a ser selecionada é chamada de ``--aepSandboxId--``. Você pode fazer isso clicando no texto **[!UICONTROL Produto de produção]** na linha azul na parte superior da tela. Depois de selecionar a [!UICONTROL sandbox], você verá a tela mudar e agora você estará em seu [!UICONTROL sandbox].

![Assimilação de dados](../module2/images/sb1.png)

No menu no lado esquerdo, vá para **Segmentos** e então vá para **Procurar** onde você pode ver uma visão geral de todos os segmentos existentes. Clique no botão **Criar segmento** botão para começar a criar um novo segmento.

![Segmentação](./images/menuseg.png)

Como mencionado acima, é necessário criar um segmento com base em todos os clientes que visualizaram o produto **JACKSHIRT DE ADEQUAÇÃO DO PROTEUS**.

Para criar esse segmento, é necessário adicionar um evento . Você pode encontrar todos os eventos clicando no botão **Eventos** no ícone na **Segmentos** barra de menu.

Em seguida, você verá o nível superior **ExperiênciaEvento XDM** nó .

Para encontrar clientes que visitaram a **JACKSHIRT DE ADEQUAÇÃO DO PROTEUS** produto, clique em **ExperiênciaEvento XDM**.

![Segmentação](./images/findee.png)

Role para baixo até **Itens da lista de produtos** e clique nele.

![Segmentação](./images/see.png)

Selecionar **Nome** e arraste e solte a **Nome** objeto da esquerda **Itens da lista de produtos** na tela do construtor de segmentos na **Eventos** seção.

![Segmentação](./images/eewebpdtlname1.png)

O parâmetro de comparação deve ser **igual** e, no campo de entrada, digite `PROTEUS FITNESS JACKSHIRT`.

![Segmentação](./images/pv.png)

Seu **Regras de evento** Agora deve ficar assim. Toda vez que você adicionar um elemento ao construtor de segmentos, você pode clicar no botão **Atualizar Estimativa** para obter uma nova estimativa da população em seu segmento.

![Segmentação](./images/ldap4.png)

Por fim, vamos dar um nome ao seu segmento e salvá-lo.

Como convenção de nomenclatura, use:

- `--demoProfileLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`

O nome do segmento deve ser semelhante a:
`vangeluw - Interest in PROTEUS FITNESS JACKSHIRT`

Em seguida, clique no botão **Salvar e fechar** para salvar o segmento.

![Segmentação](./images/segmentname.png)

Agora você será redirecionado para a página de visão geral do segmento.

![Segmentação](./images/savedsegment.png)

Próxima etapa: [6.2 Revise como configurar o destino DV360 usando destinos](./ex2.md)

[Volte para o Módulo 11](./real-time-cdp-build-a-segment-take-action.md)

[Voltar para todos os módulos](../../overview.md)
