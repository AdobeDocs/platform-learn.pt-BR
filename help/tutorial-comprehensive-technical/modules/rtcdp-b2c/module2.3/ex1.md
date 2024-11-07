---
title: Real-time CDP - Criar um segmento e executar ações - Criar um segmento
description: Real-time CDP - Criar um segmento e executar ações - Criar um segmento
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 2%

---

# 2.3.1 Criar um segmento

Neste exercício, você criará um segmento usando o construtor de segmentos da Adobe Experience Platform.

## 2.3.1.1 Contexto

No mundo de hoje, responder ao comportamento de um cliente precisa ser em tempo real. Uma das maneiras de responder ao comportamento do cliente em tempo real é usando um segmento, na condição de que o segmento se qualifique em tempo real. Neste exercício, você precisa criar um segmento, levando em conta a atividade real no site que estamos usando.

## 2.3.1.2 Identifique o comportamento ao qual você deseja reagir

Ir para [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Depois de fazer logon com sua Adobe ID, você verá isso. Clique no projeto do site para abri-lo.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

Agora você pode seguir o fluxo abaixo para acessar o site. Clique em **Integrações**.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web1.png)

Na página **Integrações**, é necessário selecionar a propriedade Coleção de dados criada no exercício 0.1.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web2.png)

Você verá seu site de demonstração aberto. Selecione o URL e copie-o para a área de transferência.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web3.png)

Abra uma nova janela incógnita do navegador.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web4.png)

Cole o URL do site de demonstração que você copiou na etapa anterior. Você será solicitado a fazer logon usando sua Adobe ID.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web5.png)

Selecione o tipo de conta e conclua o processo de logon.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web6.png)

Em seguida, você verá seu site carregado em uma janela incógnita do navegador. Para cada demonstração, será necessário usar uma janela do navegador nova e incógnita para carregar o URL do site de demonstração.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web7.png)

Neste exemplo, você deseja responder a um cliente específico que exibe um produto específico.
Na página inicial do **Luma**, vá para **Men** e clique no produto **PROTEUS FITNESS JACKSHIRT**.

![Assimilação de dados](./images/homenadia.png)

Portanto, quando alguém visita a página do produto **PROTEUS FITNESS JACKSHIRT**, você quer ser capaz de agir. A primeira coisa a fazer para agir é definir um segmento.

![Assimilação de dados](./images/homenadiapp.png)

## 2.3.1.3 Criar o segmento

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepSandboxName--``. Você pode fazer isso clicando no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. Depois de selecionar a [!UICONTROL sandbox] apropriada, você verá a alteração da tela e agora estará na [!UICONTROL sandbox] dedicada.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/sb1.png)

No menu no lado esquerdo, vá para **Segmentos** e vá para **Procurar**, onde você pode ter uma visão geral de todos os segmentos existentes. Clique no botão **Criar segmento** para começar a criar um novo segmento.

![Segmentação](./images/menuseg.png)

Como mencionado acima, você precisa criar um segmento de todos os clientes que visualizaram o produto **PROTEUS FITNESS JACKSHIRT**.

Para criar esse segmento, é necessário adicionar um evento. Você pode encontrar todos os eventos clicando no ícone **Eventos** na barra de menus **Segmentos**.

Em seguida, você verá o nó **XDM ExperienceEvent** de nível superior.

Para encontrar clientes que visitaram o produto **PROTEUS FITNESS JACKSHIRT**, clique em **XDM ExperienceEvent**.

![Segmentação](./images/findee.png)

Role para baixo até **Itens da lista de produtos** e clique nele.

![Segmentação](./images/see.png)

Selecione **Nome** e arraste e solte o objeto **Nome** do menu esquerdo **Itens de Lista de Produtos** na tela do construtor de segmentos na seção **Eventos**.

![Segmentação](./images/eewebpdtlname1.png)

O parâmetro de comparação deve ser **igual a** e, no campo de entrada, digite `PROTEUS FITNESS JACKSHIRT`.

![Segmentação](./images/pv.png)

Agora, suas **Regras de Eventos** devem ter esta aparência. Toda vez que você adiciona um elemento ao construtor de segmentos, é possível clicar no botão **Atualizar estimativa** para obter uma nova estimativa da população do seu segmento.

![Segmentação](./images/ldap4.png)

Por fim, vamos dar um nome ao seu segmento e salvá-lo.

Como convenção de nomenclatura, use:

- `--aepUserLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`

O nome do segmento deve ficar assim:
`vangeluw - Interest in PROTEUS FITNESS JACKSHIRT`

Em seguida, clique no botão **Salvar e fechar** para salvar seu segmento.

![Segmentação](./images/segmentname.png)

Agora você será levado de volta à página de visão geral do segmento.

![Segmentação](./images/savedsegment.png)

Próxima Etapa: [2.3.2 Revise como configurar o Destino DV360 usando Destinos](./ex2.md)

[Voltar ao módulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Voltar a todos os módulos](../../../overview.md)
