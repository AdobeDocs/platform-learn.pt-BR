---
title: Real-time CDP - Criar um público-alvo e realizar ações - Criar um público-alvo
description: Real-time CDP - Criar um público-alvo e realizar ações - Criar um público-alvo
kt: 5342
doc-type: tutorial
exl-id: a46b1640-769d-4fb3-97e6-beaf9706efbf
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 2%

---

# 2.3.1 Criar um público-alvo

Neste exercício, você criará um público-alvo usando o construtor de públicos-alvo da Adobe Experience Platform.

## Contexto

Responder aos interesses de um cliente precisa ser em tempo real. Uma das maneiras de responder ao comportamento do cliente em tempo real é usando um público-alvo, com a condição de que o público-alvo se qualifique em tempo real. Neste exercício, você precisa construir um público-alvo, levando em conta a atividade real no site que estamos usando.

## Identifique o comportamento ao qual deseja reagir

Ir para [https://dsn.adobe.com](https://dsn.adobe.com). Depois de fazer logon com sua Adobe ID, você verá isso. Clique nos 3 pontos **...** do projeto do site e clique em **Executar** para abri-lo.

![DSN](./../../datacollection/module1.1/images/web8.png)

Você verá seu site de demonstração aberto. Selecione o URL e copie-o para a área de transferência.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Abra uma nova janela incógnita do navegador.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Cole o URL do site de demonstração que você copiou na etapa anterior. Você será solicitado a fazer logon usando sua Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Selecione o tipo de conta e conclua o processo de logon.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Em seguida, você verá seu site carregado em uma janela incógnita do navegador. Para cada exercício, será necessário usar uma janela do navegador nova e incógnita para carregar o URL do site de demonstração.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

Neste exemplo, você deseja responder a um cliente específico que exibe um produto específico.
Na página inicial do **Citi Signal**, vá para **Telefones e dispositivos** e clique no produto **Galaxy S24**.

![Assimilação de dados](./images/homegalaxy.png)

Portanto, quando alguém visitar a página do produto do **Galaxy S24**, você poderá realizar alguma ação. A primeira coisa a fazer para agir, é definir um público.

![Assimilação de dados](./images/homegalaxy1.png)

## Criar o público

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepSandboxName--``. Depois de selecionar a [!UICONTROL sandbox] apropriada, você verá a alteração da tela e agora estará na [!UICONTROL sandbox] dedicada.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/sb1.png)

No menu à esquerda, vá para **Públicos-alvo** e vá para **Procurar**, onde você pode ter uma visão geral de todos os públicos-alvo existentes. Clique no botão **Criar público-alvo** para começar a criar um novo público-alvo.

![Segmentação](./images/menuseg.png)

Selecione **Regra de compilação** e clique em **Criar**.

![Segmentação](./images/menuseg1.png)

Como mencionado acima, você precisa criar um público de todos os clientes que visualizaram o produto **Galaxy S24**.

Para criar esse público-alvo, é necessário adicionar um evento. Você pode encontrar todos os eventos clicando no ícone **Eventos** na barra de menus **Públicos-alvo**.

Em seguida, você verá o nó **XDM ExperienceEvent** de nível superior.

Para encontrar clientes que visitaram o produto **Galaxy S24**, clique em **XDM ExperienceEvent**.

![Segmentação](./images/findee.png)

Role para baixo até **Itens da lista de produtos** e clique nele.

![Segmentação](./images/see.png)

Selecione **Nome** e arraste e solte o objeto **Nome** do menu esquerdo **Itens de Lista de Produtos** na tela do construtor de públicos-alvo na seção **Eventos**.

![Segmentação](./images/eewebpdtlname1.png)

O parâmetro de comparação deve ser **igual a** e, no campo de entrada, digite `Galaxy S24`.

![Segmentação](./images/pv.png)

Agora, suas **Regras de Eventos** devem ter esta aparência. Toda vez que você adiciona um elemento ao construtor de público-alvo, você pode clicar no botão **Atualizar estimativa** para obter uma nova estimativa da população do público-alvo.

![Segmentação](./images/ldap4.png)

Dê um nome ao seu público-alvo e defina o **Método de Avaliação** como **Edge**.

Como convenção de nomenclatura, use:

- `--aepUserLdap-- - Interest in Galaxy S24`

Em seguida, clique no botão **Publish** para salvar seu público-alvo.

![Segmentação](./images/segmentname.png)

Você será redirecionado à página de visão geral do público-alvo.

![Segmentação](./images/savedsegment.png)

Próxima Etapa: [2.3.2 Revise como configurar o Destino DV360 usando Destinos](./ex2.md)

[Voltar ao módulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Voltar a todos os módulos](../../../overview.md)
