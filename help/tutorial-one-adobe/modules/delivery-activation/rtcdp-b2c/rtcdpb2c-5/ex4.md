---
title: Coleta de dados e encaminhamento pelo lado do servidor em tempo real - crie e configure uma função da nuvem do Google
description: Criar e configurar uma função de nuvem do Google
kt: 5342
doc-type: tutorial
exl-id: bdee5a9b-2f1a-467e-9edc-a2e10a263694
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 1%

---

# 2.5.4 Encaminhar eventos para GCP Pub/Sub

>[!NOTE]
>
>Para este exercício, você precisa acessar um ambiente da Google Cloud Platform. Se você ainda não tiver acesso ao GCP, crie uma nova conta usando seu endereço de email pessoal.

## Criar seu Pub/Subtópico da Google Cloud

Ir para [https://console.cloud.google.com/](https://console.cloud.google.com/). Na barra de pesquisa, digite `pub/sub`. Clique no resultado da pesquisa **Pub/Sub - Mensagens globais em tempo real**.

![GCP](./images/gcp1.png)

Você verá isso. Clique em **CRIAR TÓPICO**.

![GCP](./images/gcp2.png)

Você verá isso. Para sua ID de Tópico, use `--aepUserLdap---event-forwarding`. Clique em **Criar**.

![GCP](./images/gcp6.png)

Seu tópico foi criado. Clique no **ID de assinatura** do tópico.

![GCP](./images/gcp7.png)

Você verá isso. Copie o **Nome do tópico** para a área de transferência e armazene-o, como você precisará dele nos próximos exercícios.

![GCP](./images/gcp8.png)

Agora vamos até Encaminhamento de evento de coleta de dados da Adobe Experience Platform para atualizar sua propriedade de Encaminhamento de eventos para iniciar o encaminhamento de eventos para Pub/Sub.


## Atualize sua propriedade de encaminhamento de eventos: Segredos

**Segredos** nas propriedades de Encaminhamento de Eventos são usados para armazenar credenciais que serão usadas para a autenticação em relação às APIs externas. Neste exemplo, é necessário configurar um segredo para armazenar o token OAuth da Google Cloud Platform, que será usado para autenticar ao usar Pub/Sub para transmitir dados em direção ao GCP.

Vá para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) e vá para **Segredos**. Clique em **Criar Novo Segredo**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/secret1.png)

Você verá isso. Siga estas instruções:

- Nome: use `--aepUserLdap---gcp-secret`
- Ambiente de Destino: selecione **Desenvolvimento**
- Tipo: **Google OAuth 2**
- Marque a caixa de seleção de **Pub/Sub**

Clique em **Criar Segredo**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/secret2.png)

Depois de clicar em **Criar Segredo**, você verá um pop-up para configurar a autenticação entre o segredo da propriedade de Encaminhamento de Eventos e o Google. Clique em **Criar e autorizar segredo `--aepUserLdap---gcp-secret` com o Google**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/secret3.png)

Clique em para selecionar sua conta do Google.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/secret4.png)

Clique em **Continuar**.

>[!NOTE]
>
>A mensagem pop-up pode variar. Autorize/permita o acesso solicitado para continuar com o exercício.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/secret5.png)

Após a autenticação bem-sucedida, você verá isso.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/secret6.png)

Seu segredo agora foi configurado com sucesso e pode ser usado em um elemento de dados.

## Atualizar a propriedade de encaminhamento de eventos: Elemento de dados

Para usar o segredo na propriedade de encaminhamento de eventos, é necessário criar um elemento de dados que armazenará o valor do segredo.

Vá para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) e vá para **Encaminhamento de Eventos**. Pesquise na propriedade de encaminhamento de eventos e clique nela para abri-la.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/prop1.png)

No menu esquerdo, vá para **Elementos de Dados**. Clique em **Adicionar elemento de dados**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/de1gcp.png)

Configure o elemento de dados da seguinte maneira:

- Nome: **Segredo GCP**
- Extensão: **Core**
- Tipo de Elemento de Dados: **Segredo**
- Segredo de desenvolvimento: selecione o segredo que você criou, chamado `--aepUserLdap---gcp-secret`

Clique em **Salvar**

![SSF da Coleção de Dados do Adobe Experience Platform](./images/secret7.png)

## Atualize sua propriedade de encaminhamento de eventos: Extensão

Com seu Segredo e Elemento de dados configurados, agora é possível configurar a extensão para a Google Cloud Platform na propriedade Encaminhamento de eventos.

Vá para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/), vá para **Encaminhamento de Eventos** e abra sua propriedade de Encaminhamento de Eventos.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/prop1.png)

Em seguida, vá para **Extensões**, para **Catálogo**. Clique na extensão **Google Cloud Platform** e em **Instalar**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/gext2.png)

Você verá isso. Clique no ícone Elemento de dados.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/gext3.png)

Selecione o elemento de dados criado no exercício anterior, denominado **Segredo GCP**. Clique em **Selecionar**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/gext4.png)

Você verá isso. Clique em **Salvar**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/gext5.png)

## Atualizar a propriedade de encaminhamento de eventos: atualizar uma regra

Agora que sua extensão da Google Cloud Platform está configurada, é possível definir uma regra para começar a encaminhar dados do evento para o seu Pub/Subtópico. Para fazer isso, você precisará atualizar a regra **Todas as páginas** que criou em um dos exercícios anteriores.

No menu esquerdo, vá para **Regras**. No exercício anterior, você criou a regra **Todas as páginas**. Clique nessa regra para abri-la.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl1gcp.png)

Então você vai ver isso. Clique no ícone **+** em **Ações** para adicionar uma nova ação.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl2gcp.png)

Você verá isso. Faça a seguinte seleção:

- Selecione a **Extensão**: **Google Cloud Platform**.
- Selecione o **Tipo de Ação**: **Enviar Dados para o Pub/Sub** da Nuvem.

Isso deve fornecer a você este **Nome**: **Plataforma de Nuvem da Google - Enviar Dados para o Pub/Sub** da Nuvem. Agora você deve ver isso:

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl5gcp.png)

Agora é necessário configurar o Pub/Sub tópico criado anteriormente.

Você pode encontrar o **Nome do tópico** aqui, copie-o.

![GCP](./images/gcp8.png)

Cole o **Nome do tópico** na sua configuração de Regra. Em seguida, clique no ícone Elemento de dados ao lado do campo **Dados (obrigatórios)**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl6gcp.png)

Selecione **Evento XDM** e clique em **Selecionar**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl7gcp.png)

Você verá isso. Clique em **Manter alterações**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl8gcp.png)

Clique em **Salvar**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl9gcp.png)

Você verá isso.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl10gcp.png)

## Publicar suas alterações

Sua configuração foi concluída. Vá para **Fluxo de Publicação** para publicar suas alterações. Abra a biblioteca de desenvolvimento **Principal** clicando em **Editar** conforme indicado.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl12gcp.png)

Clique no botão **Adicionar todos os recursos alterados**, após o qual você verá sua Regra e Elemento de Dados aparecerem nesta biblioteca. Em seguida, clique em **Salvar e criar para desenvolvimento**. Suas alterações estão sendo implantadas.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl13gcp.png)

Após alguns minutos, você verá que a implantação foi concluída e está pronta para ser testada.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl14.png)

## Testar sua configuração

Ir para [https://dsn.adobe.com](https://dsn.adobe.com). Depois de fazer logon com sua Adobe ID, você verá isso. Clique nos 3 pontos **...** do projeto do site e clique em **Executar** para abri-lo.

![DSN](./../../datacollection/dc1.1/images/web8.png)

Você verá seu site de demonstração aberto. Selecione o URL e copie-o para a área de transferência.

![DSN](../../../getting-started/gettingstarted/images/web3.png)

Abra uma nova janela incógnita do navegador.

![DSN](../../../getting-started/gettingstarted/images/web4.png)

Cole o URL do site de demonstração que você copiou na etapa anterior. Você será solicitado a fazer logon usando sua Adobe ID.

![DSN](../../../getting-started/gettingstarted/images/web5.png)

Selecione o tipo de conta e conclua o processo de logon.

![DSN](../../../getting-started/gettingstarted/images/web6.png)

Em seguida, você verá seu site carregado em uma janela incógnita do navegador. Para cada exercício, será necessário usar uma janela do navegador nova e incógnita para carregar o URL do site de demonstração.

![DSN](../../../getting-started/gettingstarted/images/web7.png)

Alterne sua exibição para o Pub/Sub da Google Cloud e vá para **MESSAGES**. Clique em **PULL** e após alguns segundos você verá algumas mensagens na lista. Clique em uma mensagem para visualizar seu conteúdo.

![Configuração da Coleção de Dados do Adobe Experience Platform](./images/hook3gcp.png)

Agora você pode ver a carga XDM do seu evento no Google Pub/Sub. Agora você enviou com êxito os dados coletados pela Coleção de dados da Adobe Experience Platform, em tempo real, para um Pub/Sub endpoint da Google Cloud. A partir daí, esses dados podem ser usados por qualquer aplicativo da Google Cloud Platform, como o BigQuery para armazenamento e relatórios ou para casos de uso de aprendizado de máquina.

![Configuração da Coleção de Dados do Adobe Experience Platform](./images/hook4gcp.png)

## Próximas etapas

Ir para [2.5.5 Encaminhar eventos para AWS Kinesis e AWS S3](./ex5.md){target="_blank"}

Voltar para [Conexões do Real-Time CDP: Encaminhamento de Eventos](./aep-data-collection-ssf.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
