---
title: Automação usando conectores
description: Automação usando conectores
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
source-git-commit: 6ef4ce94dbbcd65ab30bcfad24f4ddd746c26b82
workflow-type: tm+mt
source-wordcount: '1721'
ht-degree: 1%

---

# 1.2.4 Automação usando conectores

Agora, você começará a usar os conectores prontos para uso no Workfront Fusion para Photoshop e conectará a solicitação de Firefly Text-2-Image e as solicitações do Photoshop em um cenário.

## 1.2.4.1 Duplique e prepare seu cenário

No menu esquerdo, vá para **Cenários** e selecione sua pasta `--aepUserLdap--`. Você deverá ver o cenário criado antes, chamado `--aepUSerLdap-- - Adobe I/O Authentication`.

![WF Fusion](./images/wffc1.png)

Clique na seta para abrir o menu suspenso e selecione **Clonar**.

![WF Fusion](./images/wffc2.png)

Defina o **Nome** do cenário clonado como `--aepUserLdap-- - Firefly + Photoshop` e selecione a **Equipe de Destino** apropriada. Clique em **Adicionar** para adicionar um novo webhook.

![WF Fusion](./images/wffc3.png)

Defina o **nome do Webhook** para `--aepUserLdap-- - Firefly + Photoshop Webhook`. Clique em **Salvar**.

![WF Fusion](./images/wffc4.png)

Você deverá ver isso. Clique em **Salvar**.

![WF Fusion](./images/wffc5.png)

Você deverá ver isso. Clique no nó **Webhook**.

![WF Fusion](./images/wffc6.png)

Clique em **Copiar endereço para a área de transferência** e em **Redeterminar estrutura de dados**.

![WF Fusion](./images/wffc7.png)

Abra o Postman. Adicione uma nova solicitação na mesma pasta que você estava usando antes.

![WF Fusion](./images/wffc9.png)

Verifique se as seguintes configurações foram aplicadas:

- Nome da solicitação: `POST - Send Request to Workfront Fusion Webhook Firefly + Photoshop`
- Tipo de solicitação: `POST`
- URL de solicitação: cole o URL copiado do webhook do Cenário do Workfront Fusion.

Vá para **Corpo** e defina o **Tipo de Corpo** como **bruto** - **JSON**. Cole a seguinte carga no **Corpo**.

```json
{
    "psdTemplate": "citisignal-fiber.psd",
    "xlsFile": "placeholder",
    "prompt":"misty meadows",
    "cta": "Buy this now!",
    "button": "Click here to buy!"
}
```

Essa nova carga garantirá que todas as informações da variável sejam fornecidas de fora do cenário, em vez de serem codificadas no cenário. Em um cenário empresarial, uma organização precisa que um cenário seja definido de forma reutilizável, o que significa que várias variáveis precisam ser fornecidas como variáveis de entrada, em vez de serem codificadas no cenário.

Você deveria ficar com isso. Clique em **Enviar**.

![WF Fusion](./images/wffc10.png)

O webhook do Workfront Fusion ainda está aguardando entrada.

![WF Fusion](./images/wffc11.png)

Depois de clicar em **Enviar**, a mensagem deverá mudar para **Determinado com êxito**. Clique em **OK**.

![WF Fusion](./images/wffc12.png)

## 1.2.4.2 Atualizar o nó Firefly T2I

Clique no nó **Firefly T2I**. Você deverá ver isso. O prompt nesta solicitação foi previamente codificado para **cavalos em um campo**. Agora você removerá esse texto codificado e o substituirá por um campo proveniente do webhook.

![WF Fusion](./images/wffcfft2i1.png)

Remova o texto **cavalos em um campo** e substitua-o pela variável **prompt** que pode ser encontrada nas variáveis **Webhook**. Clique em **OK** para salvar suas alterações.

![WF Fusion](./images/wffcfft2i2.png)

## 1.2.4.2 Alterar plano de fundo do arquivo PSD

Agora você atualizará seu cenário para torná-lo mais inteligente usando conectores prontos para uso. Você também conectará a saída do Firefly ao Photoshop, para que a imagem de fundo do arquivo PSD seja alterada dinamicamente usando a saída da ação Gerar imagem do Firefly.

No exercício anterior, você desabilitou a rota **Firefly T2I**. Você deve desfazer isso agora. Clique no ícone **stop** para habilitar a rota novamente.

![WF Fusion](./images/wffc13.png)

Você verá que o ícone **parar** desaparece. Em seguida, clique no ícone **chave inglesa** na outra rota em direção à configuração do exercício anterior e selecione **Desabilitar rota**.

![WF Fusion](./images/wffc14.png)

Você deverá ver isso. Em seguida, passe o mouse sobre o nó **Firefly T2I** e clique no ícone **+**.

![WF Fusion](./images/wffc15.png)

No menu de pesquisa, digite `Photoshop`e clique na ação **Adobe Photoshop**.

![WF Fusion](./images/wffc16.png)

Selecione **Aplicar edições do PSD**.

![WF Fusion](./images/wffc17.png)

Você deverá ver isso. Clique em **Adicionar** para adicionar uma nova conexão ao Adobe Photoshop.

![WF Fusion](./images/wffc18.png)

Configure sua conexão da seguinte maneira:

- Tipo de conexão: selecione **Adobe Photoshop (Servidor para Servidor)**
- Nome da conexão: digite `--aepUserLdap-- - Adobe IO`
- ID do cliente: cole sua ID do cliente
- Segredo do cliente: cole seu Segredo do cliente

Clique em **Continuar**.

![WF Fusion](./images/wffc19.png)

Para localizar sua **ID do Cliente** e seu **Segredo do Cliente**, vá para [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"} e abra seu projeto do Adobe I/O, denominado `--aepUserLdap-- One Adobe tutorial`. Vá para **OAuth Server-to-Server** para encontrar a ID do Cliente e o Segredo do Cliente. Copie esses valores e cole-os na configuração de conexão no Workfront Fusion.

![WF Fusion](./images/wffc20.png)

Depois de clicar em **Continuar**, uma janela pop-up será mostrada brevemente enquanto suas credenciais estiverem sendo verificadas. Depois de concluído, você deve ver isso.

![WF Fusion](./images/wffc21.png)

Agora é necessário inserir o local do arquivo do PSD com o qual você deseja que o Fusion funcione. Para **Armazenamento**, selecione **Azure** e para **Local do arquivo**, digite `{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/{{1.AZURE_STORAGE_SAS_READ}}`. Coloque o cursor próximo ao segundo `/`. Em seguida, verifique as variáveis disponíveis e role para baixo para localizar a variável **psdTemplate**. Clique na variável **psdTemplate** para selecioná-la.

![WF Fusion](./images/wffc22.png)

Você deverá ver isso.

![WF Fusion](./images/wffc23.png)

Role para baixo até ver **Camadas**. Clique em **Adicionar item**.

![WF Fusion](./images/wffc24.png)

Você deverá ver isso. Agora é necessário inserir o nome da camada no modelo Photoshop PSD que é usada para o plano de fundo do arquivo.

![WF Fusion](./images/wffc25.png)

No arquivo **citisignal-fiber.psd**, você encontrará a camada usada para o plano de fundo. Neste exemplo, essa camada é chamada de **2048x2048-background**.

![WF Fusion](./images/wffc26.png)

Cole o nome **2048x2048-background** na caixa de diálogo do Workfront Fusion.

![WF Fusion](./images/wffc27.png)

Role para baixo até ver **Entrada**. Agora é necessário definir o que precisa ser inserido na camada de plano de fundo. Nesse caso, você precisa selecionar a saída do objeto Firefly T2I, que contém a imagem gerada dinamicamente.

Para **Armazenamento**, selecione **Externo**. Para **Local do arquivo**, pesquise e localize a variável `data.outputs[].image.url` da saída da solicitação **Firefly T2I**.

![WF Fusion](./images/wffc28.png)

Em seguida, role para baixo até ver **Editar**. Defina **Editar** como **Sim** e defina **Tipo** como **Camada**. Clique em **Adicionar**.

![WF Fusion](./images/wffc29.png)

Você deverá ver isso. Em seguida, é necessário definir a saída da ação. Clique em **Adicionar item** em **saídas**.

![WF Fusion](./images/wffc30.png)

Selecione o **Azure** para **Armazenamento**, cole este `{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/citisignal-fiber-replacedbg.psd{{1.AZURE_STORAGE_SAS_WRITE}}` em **Local do Arquivo** e selecione **vnd.adobe.photoshop** em **Tipo**. Clique para habilitar **Mostrar configurações avançadas**.

![WF Fusion](./images/wffc31.png)

Em **Configurações Avançadas**, selecione **Sim** para substituir arquivos com o mesmo nome.
Clique em **Adicionar**.

![WF Fusion](./images/wffc32.png)

Você deveria ficar com isso. Clique em **OK**.

![WF Fusion](./images/wffc33.png)

## 1.2.4.3 Alterar camadas de texto do arquivo PSD

### Texto do Plano de Ação

Em seguida, passe o mouse sobre o nó **Adobe Photoshop - Aplicar edições do PSD** e clique no ícone **+**.

![WF Fusion](./images/wffc34.png)

Selecione **Adobe Photoshop**.

![WF Fusion](./images/wffc35.png)

Selecione **Editar camadas de texto**.

![WF Fusion](./images/wffc36.png)

Você deverá ver isso. Primeiro, selecione a conexão do Adobe Photoshop já configurada anteriormente, que deve ser chamada de `--aepUserLdap-- Adobe IO`.

Agora é necessário definir o local do **Arquivo de entrada**, que é a saída da etapa anterior e em **Camadas**, é necessário inserir o **Nome** da camada de texto que você deseja alterar.

![WF Fusion](./images/wffc37.png)

Para o **Arquivo de entrada**, selecione **Azure** para **Armazenamento do arquivo de entrada** e certifique-se de selecionar a saída da solicitação anterior, **Adobe Photoshop - Aplicar edições do PSD**, que você pode usar aqui: `data[]._links.renditions[].href`

![WF Fusion](./images/wffc37a.png)

Abra o arquivo **citisignal-fiber.psd**. No arquivo, você observará que a camada que contém a chamada à ação é chamada **2048x2048-cta**.

![WF Fusion](./images/wffc38.png)

Insira o nome **2048x2048-cta** em **Nome** na caixa de diálogo.

![WF Fusion](./images/wffc39.png)

Role para baixo até ver **Texto** > **Conteúdo**. Selecione a variável **cta** na carga do Webhook.

![WF Fusion](./images/wffc40.png)

Role para baixo até ver **Saída**. Para **Armazenamento**, selecione **Azure**. Para **Local do arquivo**, insira o local abaixo. Observe a adição da variável `{{timestamp}}` ao nome de arquivo, que é usada para garantir que cada arquivo gerado tenha um nome exclusivo. Além disso, defina o **Type** como **vnd.adobe.photoshop**. Clique em **OK**.

`{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text-{{timestamp}}.psd{{1.AZURE_STORAGE_SAS_WRITE}}`

![WF Fusion](./images/wffc41.png)

### Texto do botão

Clique com o botão direito do mouse no nó que acabou de criar e selecione **Clonar**. Isso criará um segundo objeto semelhante.

![WF Fusion](./images/wffc42.png)

Você deverá ver isso. Primeiro, selecione a conexão do Adobe Photoshop já configurada anteriormente, que deve ser chamada de `--aepUserLdap-- Adobe IO`.

Agora é necessário definir o local do **Arquivo de entrada**, que é a saída da etapa anterior e em **Camadas**, é necessário inserir o **Nome** da camada de texto que você deseja alterar.

![WF Fusion](./images/wffc43.png)

Para o **Arquivo de entrada**, selecione **Azure** para **Armazenamento do arquivo de entrada** e certifique-se de selecionar a saída da solicitação anterior, **Adobe Photoshop - Editar camadas de texto**, que você pode usar aqui: `data[]._links.renditions[].href`

Abra o arquivo **citisignal-fiber.psd**. No arquivo, você observará que a camada que contém a chamada à ação é chamada **2048x2048-button-text**.

![WF Fusion](./images/wffc44.png)

Insira o nome **2048x2048-cta** em **Nome** na caixa de diálogo.

![WF Fusion](./images/wffc43.png)

Role para baixo até ver **Texto** > **Conteúdo**. Selecione a variável **cta** na carga do Webhook.

![WF Fusion](./images/wffc45.png)

Role para baixo até ver **Saída**. Para **Armazenamento**, selecione **Azure**. Para **Local do arquivo**, insira o local abaixo. Observe a adição da variável `{{timestamp}}` ao nome de arquivo, que é usada para garantir que cada arquivo gerado tenha um nome exclusivo. Além disso, defina o **Type** como **vnd.adobe.photoshop**. Clique em **OK**.

`{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text-{{timestamp}}.psd{{1.AZURE_STORAGE_SAS_WRITE}}`

![WF Fusion](./images/wffc46.png)

Clique em **Salvar** para salvar as alterações.

![WF Fusion](./images/wffc47.png)

## 1.2.4.4 resposta do Webhook

Depois de aplicar essas alterações ao arquivo do Photoshop, agora é necessário configurar uma **resposta do Webhook** que será enviada de volta para o aplicativo que tiver ativado esse cenário.

Passe o mouse sobre o nó **Adobe Photoshop - Editar camadas de texto** e clique no ícone **+**.

![WF Fusion](./images/wffc48.png)

Pesquise por **webhook** e selecione **Webhook**.

![WF Fusion](./images/wffc49.png)

Selecione **resposta do Webhook**.

![WF Fusion](./images/wffc50.png)

Você deverá ver isso. Cole a carga abaixo no **Corpo**.

```json
{
    "newPsdTemplate": ""
}
```

![WF Fusion](./images/wffc51.png)

Selecione o caminho `data[]._links.renditions[].href` na saída da solicitação anterior. Habilite a caixa de seleção para **Mostrar configurações avançadas** e clique em **Adicionar item**.

![WF Fusion](./images/wffc52.png)

No campo **Chave**, digite `Content-Type`. No campo **Valor**, digite `application/json`. Clique em **Salvar**.

![WF Fusion](./images/wffc52a.png)

Você deveria ficar com isso. Clique em **OK**.

![WF Fusion](./images/wffc53.png)

Clique em **Alinhamento automático**.

![WF Fusion](./images/wffc54.png)

Você deverá ver isso. Clique em **Executar uma vez**.

![WF Fusion](./images/wffc55.png)

Volte para o Postman e clique em **Enviar**. O prompt que está sendo usado aqui é **misty meadows**.

![WF Fusion](./images/wffc56.png)

O cenário será ativado e, após algum tempo, uma resposta será mostrada no Postman contendo o URL do arquivo do PSD recém-criado.

![WF Fusion](./images/wffc58.png)

Como lembrete: depois que o cenário for executado no Workfront Fusion, você poderá ver informações sobre cada nó clicando na bolha acima de cada nó.

![WF Fusion](./images/wffc59.png)

Usando o Azure Storage Explorer, você pode encontrar e abrir o arquivo do PSD recém-criado clicando duas vezes nele no Azure Storage Explorer.

![WF Fusion](./images/wffc60.png)

O arquivo deve ter esta aparência, com o plano de fundo substituído por um plano de fundo com **prados nebulosos**.

![WF Fusion](./images/wffc61.png)

Se você executar o cenário novamente e enviar uma nova solicitação do Postman usando um prompt diferente, verá como o cenário se tornou fácil e reutilizável. Neste exemplo, o novo prompt sendo usado é **deserto ensolarado**.

![WF Fusion](./images/wffc62.png)

E alguns minutos depois, um novo arquivo PSD foi gerado com um novo plano de fundo.

![WF Fusion](./images/wffc63.png)

## Próximas etapas

Ir para [Resumo e Benefícios da Automação de Serviços da Firefly](./summary.md){target="_blank"}

Volte para [Automatização dos Serviços Adobe Firefly](./automation.md){target="_blank"}

Voltar para [Todos os Módulos](./../../../overview.md){target="_blank"}
