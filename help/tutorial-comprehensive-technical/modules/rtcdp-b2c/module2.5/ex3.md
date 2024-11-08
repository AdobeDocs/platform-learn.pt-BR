---
title: Coleta de dados da Adobe Experience Platform e encaminhamento pelo lado do servidor em tempo real - crie e configure um webhook personalizado
description: Criar e configurar um webhook personalizado
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 1%

---

# 2.5.3 Criar e configurar um webhook personalizado

## 2.5.3.1 Criar seu webhook personalizado

Ir para [https://webhook.site/](https://webhook.site/). Você verá algo assim:

![demonstração](./images/webhook1.png)

Você verá sua URL exclusiva, que tem esta aparência: `https://webhook.site/585126a1-41fc-4721-864b-d4aa8c268a1d`.

Este site criou este webhook para você e você poderá configurar este webhook no **[!DNL Event Forwarding property]** para começar a testar o encaminhamento de eventos.

## 2.5.3.2 Atualize sua propriedade de encaminhamento de eventos: Criar um elemento de dados

Vá para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) e vá para **Encaminhamento de Eventos**. Pesquise na propriedade de encaminhamento de eventos e clique nela para abri-la.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/prop1.png)

No menu esquerdo, vá para **Elementos de Dados**. Clique em **Criar novo elemento de dados**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/de1.png)

Você verá um novo elemento de dados para configurar.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/de2.png)

Faça a seguinte seleção:

- Como o **Nome**, digite **Evento XDM**.
- Como a **Extensão**, selecione **Principal**.
- Como o **Tipo de Elemento de Dados**, selecione **Caminho**.
- Como o **Caminho**, digite **arc.event.xdm**. Ao inserir este caminho, você filtrará a seção **XDM** da carga do evento enviada pelo site ou aplicativo móvel para a Adobe Edge.

Agora você terá isto. Clique em **Salvar**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/de3.png)

>[!NOTE]
>
>No caminho acima, é feita uma referência a **arc**. **arc** significa Contexto de Recurso de Adobe e **arc** sempre significa o maior objeto disponível no contexto do Servidor. Enriquecimentos e transformações podem ser adicionados a esse objeto **arc** usando as funções do Servidor de Coleta de Dados da Adobe Experience Platform.
>
>No caminho acima, é feita uma referência ao **evento**. **event** significa um evento exclusivo e o Adobe Experience Platform Data Collection Server sempre avaliará cada evento individualmente. Às vezes, você pode ver uma referência a **eventos** na carga enviada pelo lado do cliente do SDK da Web, mas no Adobe Experience Platform Data Collection Server, cada evento é avaliado individualmente.

## 2.5.3.3 Atualize sua propriedade do Servidor de coleta de dados da Adobe Experience Platform: Criar uma regra

No menu esquerdo, vá para **Regras**. Clique em **Criar nova regra**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl1.png)

Você verá uma nova regra a ser configurada. Insira o **Nome**: **Todas as páginas**. Para este exercício, não será necessário configurar uma condição. Em vez disso, você configurará uma ação. Clique no botão **+ Adicionar** em **Ações**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl2.png)

Você verá isso. Faça a seguinte seleção:

- Selecione a **Extensão**: **Conector de Nuvem do Adobe**.
- Selecione o **Tipo de ação**: **Fazer chamada de busca**.

Isso deve fornecer a você este **Nome**: **Conector de Nuvem Adobe - Fazer Chamada de Busca**. Agora você deve ver isso:

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl4.png)

Em seguida, configure o seguinte:

- Altere o método de solicitação de GET para **POST**
- Digite a URL do webhook personalizado que você criou em uma das etapas anteriores no site [https://webhook.site/](https://webhook.site/), que tem esta aparência: `https://webhook.site/585126a1-41fc-4721-864b-d4aa8c268a1d`

Agora você deve ter isso. Em seguida, vá para **Corpo**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl6.png)

Você verá isso. Clique no ícone do elemento de dados conforme indicado abaixo.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl7.png)

Na janela pop-up, selecione o elemento de dados **XDM Event** que você criou na etapa anterior. Clique em **Selecionar**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl8.png)

Você verá isso. Clique em **Manter alterações**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl9.png)

Você verá isso. Clique em **Salvar**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl10.png)

Agora você configurou sua primeira regra em uma propriedade de encaminhamento de eventos. Vá para **Fluxo de Publicação** para publicar suas alterações.
Abra a biblioteca de desenvolvimento **Principal** clicando em **Editar** conforme indicado.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl11.png)

Clique no botão **Adicionar todos os recursos alterados**, após o qual você verá sua Regra e Elemento de Dados aparecerem nesta biblioteca. Em seguida, clique em **Salvar e criar para desenvolvimento**. Suas alterações estão sendo implantadas.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl13.png)

Após alguns minutos, você verá que a implantação foi concluída e está pronta para ser testada.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl14.png)

## 2.5.3.4 Testar a configuração

Ir para [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Depois de fazer logon com sua Adobe ID, você verá isso. Clique no projeto do site para abri-lo.

![DSN](../../gettingstarted/gettingstarted/images/web8.png)

Agora você pode seguir o fluxo abaixo para acessar o site. Clique em **Integrações**.

![DSN](../../gettingstarted/gettingstarted/images/web1.png)

Na página **Integrações**, é necessário selecionar a propriedade Coleção de dados criada no exercício 0.1.

![DSN](../../gettingstarted/gettingstarted/images/web2.png)

Você verá seu site de demonstração aberto. Selecione o URL e copie-o para a área de transferência.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Abra uma nova janela incógnita do navegador.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Cole o URL do site de demonstração que você copiou na etapa anterior. Você será solicitado a fazer logon usando sua Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Selecione o tipo de conta e conclua o processo de logon.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Em seguida, você verá seu site carregado em uma janela incógnita do navegador. Para cada demonstração, será necessário usar uma janela do navegador nova e incógnita para carregar o URL do site de demonstração.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

Ao abrir a Exibição do desenvolvedor do seu navegador, você pode inspecionar as solicitações de Rede conforme indicado abaixo. Ao usar o filtro **interagir**, você verá as solicitações de rede enviadas pelo Cliente de Coleção de Dados da Adobe Experience Platform para a Adobe Edge.

![Configuração da Coleção de Dados do Adobe Experience Platform](./images/hook1.png)

Se você selecionar a carga bruta, vá para [https://jsonformatter.org/json-pretty-print](https://jsonformatter.org/json-pretty-print) e cole a carga. Clique em **Tornar Bonito**. Você verá a carga JSON, o objeto **events** e o objeto **xdm**. Em uma das etapas anteriores, ao definir o Elemento de dados, você usou a referência **arc.event.xdm**, que resultará na análise do objeto **xdm** desta carga.

![Configuração da Coleção de Dados do Adobe Experience Platform](./images/hook2.png)

Mude sua exibição para o site [https://webhook.site/](https://webhook.site/), que você usou em uma das etapas anteriores. Agora você deve ter uma visualização semelhante a esta, com solicitações de rede sendo mostradas no menu esquerdo. Você está vendo a carga **xdm** que foi filtrada para fora da solicitação de rede mostrada acima.

![Configuração da Coleção de Dados do Adobe Experience Platform](./images/hook3.png)

Role para baixo na carga para encontrar o nome da página, que neste caso é **vangeluw-OCUC** (que é o nome do projeto do seu site de demonstração).

![Configuração da Coleção de Dados do Adobe Experience Platform](./images/hook4.png)

Agora, ao navegar pelo site, você verá solicitações de rede adicionais tornando-se disponíveis neste webhook personalizado em tempo real.

![Configuração da Coleção de Dados do Adobe Experience Platform](./images/hook5.png)

Agora você configurou o encaminhamento pelo lado do servidor de cargas SDK da Web/XDM para um webhook personalizado externo. Nos próximos exercícios, você configurará uma abordagem semelhante e enviará esses mesmos dados para os ambientes do Google e do AWS.

Próxima etapa: [2.5.4 Criar e configurar uma Função de Nuvem do Google](./ex4.md)

[Voltar ao módulo 2.5](./aep-data-collection-ssf.md)

[Voltar a todos os módulos](./../../../overview.md)
