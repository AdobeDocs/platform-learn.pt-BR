---
title: Automação usando conectores
description: Automação usando conectores
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 0b20ba91-28d4-4f4d-8abe-074f802c389e
source-git-commit: d4cb1ff51c9367fd0d249806e50b676d8a83c557
workflow-type: tm+mt
source-wordcount: '1991'
ht-degree: 1%

---

# 1.2.4 Automação usando conectores

Agora, você começará a usar os conectores prontos para uso no Workfront Fusion para Photoshop e conectará a solicitação de Firefly Text-2-Image e as solicitações do Photoshop em um cenário.

## 1.2.4.1 Atualizar variáveis

Antes de continuar com a configuração do conector, as seguintes variáveis precisam ser adicionadas ao módulo **Inicializar constantes**.

- `AZURE_STORAGE_URL`
- `AZURE_STORAGE_CONTAINER`
- `AZURE_STORAGE_SAS_READ`
- `AZURE_STORAGE_SAS_WRITE`

Volte para o primeiro nó, selecione **Inicializar constantes** e escolha **Adicionar item** para cada uma dessas variáveis.

![WF Fusion](./images/wffusion69.png)

| Chave | Exemplo de valor |
|:-------------:| :---------------:| 
| `AZURE_STORAGE_URL` | `https://vangeluw.blob.core.windows.net` |
| `AZURE_STORAGE_CONTAINER` | `vangeluw` |
| `AZURE_STORAGE_SAS_READ` | `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D` |
| `AZURE_STORAGE_SAS_WRITE` | `?sv=2023-01-03&st=2025-01-13T17%3A21%3A09Z&se=2025-01-14T17%3A21%3A09Z&sr=c&sp=racwl&sig=FD4m0YyyqUj%2B5T8YyTFJDi55RiTDC9xKtLTgW0CShps%3D` |

Você pode encontrar suas variáveis voltando ao Postman e abrindo suas **Variáveis de ambiente**.

![Armazenamento do Azure](./../module1.1/images/az105.png)

Copie esses valores no Workfront Fusion e adicione um novo item para cada uma dessas 4 variáveis.

Sua tela deve ter esta aparência. Selecione **OK**.

![WF Fusion](./images/wffusion68.png)

## 1.2.4.2 Ativar seu cenário usando um webhook

Até o momento, você executou o cenário manualmente para testar. Agora vamos atualizar seu cenário com um webhook, para que ele possa ser ativado de um ambiente externo.

Selecione **+**, procure por **webhook** e selecione **Webhooks**.

![WF Fusion](./images/wffusion216.png)

Selecione **Webhook personalizado**.

![WF Fusion](./images/wffusion217.png)

Arraste o módulo **Webhook personalizado** para o início do cenário. Em seguida, selecione o ícone **relógio** e arraste-o para o módulo **Webhook personalizado**.

![WF Fusion](./images/wffusion217a.png)

Você deverá ver isso. Em seguida, arraste o ponto vermelho no primeiro módulo em direção ao ponto roxo no segundo módulo.

![WF Fusion](./images/wffusion217b.png)

Você deverá ver isso. Em seguida, clique no módulo **Webhook personalizado**.

![WF Fusion](./images/wffusion217c.png)

Clique em **Adicionar**.

![WF Fusion](./images/wffusion218.png)

Defina o **nome do Webhook** para `--aepUserLdap-- - Firefly + Photoshop Webhook`. Clique em **Salvar**.

![WF Fusion](./images/wffusion219.png)

O URL do webhook está disponível. Clique em **Copiar endereço para a área de transferência** para copiar a URL.

![WF Fusion](./images/wffusion221.png)

Abra o Postman e adicione uma nova pasta à coleção **FF - Firefly Services Tech Insiders**.

![WF Fusion](./images/wffusion222.png)

Nomeie sua pasta `--aepUserLdap-- - Workfront Fusion`.

![WF Fusion](./images/wffusion223.png)

Na pasta que você acabou de criar, selecione os 3 pontos **...** e selecione **Adicionar solicitação**.

![WF Fusion](./images/wffusion224.png)

Defina o **Tipo de método** como **POST** e cole a URL do seu webhook na barra de endereços.

![WF Fusion](./images/wffusion225.png)

É necessário enviar um corpo personalizado, para que os elementos variáveis possam ser fornecidos de uma fonte externa para o cenário do Workfront Fusion.

Vá para **Corpo** e selecione **bruto**.

![WF Fusion](./images/wffusion226.png)

Cole o texto abaixo no corpo da solicitação. Selecione **Enviar**.

```json
{
    "psdTemplate": "citisignal-fiber.psd",
    "xlsFile": "placeholder",
    "prompt":"misty meadows",
    "cta": "Buy this now!",
    "button": "Click here to buy!"
}
```

![WF Fusion](./images/wffusion229.png)

De volta ao Workfront Fusion, é exibida uma mensagem em seu webhook personalizado que diz: **Determinado com êxito**.

![WF Fusion](./images/wffusion227.png)

## Conector do Adobe Firefly do 1.2.4.3

Clique no ícone **+** para adicionar um novo módulo.

![WF Fusion](./images/wffcff2.png)

Insira o termo de pesquisa `Adobe Firefly` e selecione **Adobe Firefly**.

![WF Fusion](./images/wffcff2a.png)

Selecione **Gerar uma imagem**.

![WF Fusion](./images/wffcff3.png)

Clique no módulo **Adobe Firefly** para abri-lo e em **Adicionar** para criar uma nova conexão.

![WF Fusion](./images/wffcff5.png)

Preencha os seguintes campos:

- **Nome da conexão**: use `--aepUserLdap-- - Firefly connection`.
- **Ambiente**: usar **Produção**.
- **Tipo**: usar **Conta pessoal**.
- **ID do Cliente**: copie a **ID do Cliente** do seu projeto do Adobe I/O chamado `--aepUserLdap-- - One Adobe tutorial`.
- **Segredo do Cliente**: copie o **Segredo do Cliente** do seu projeto do Adobe I/O chamado `--aepUserLdap-- - One Adobe tutorial`.

Você pode encontrar a **ID do Cliente** e o **Segredo do Cliente** do seu projeto do Adobe I/O [aqui](https://developer.adobe.com/console/projects.){target="_blank"}.

![WF Fusion](./images/wffc20.png)

Depois de preencher todos os campos, clique em **Continuar**. Sua conexão será validada automaticamente.

![WF Fusion](./images/wffcff6.png)

Em seguida, selecione a variável **prompt** que é fornecida para o cenário pelo **webhook personalizado** de entrada.

![WF Fusion](./images/wffcff7.png)

Defina a **versão do modelo** **prompt** para **imagem4 padrão**. Clique em **OK**.

![WF Fusion](./images/wffcff7b.png)

Clique em **Salvar** para salvar suas alterações e em **Executar uma vez** para testar sua configuração.

![WF Fusion](./images/wffcff8.png)

Vá para o Postman, verifique o prompt na sua solicitação e clique em **Enviar**.

![WF Fusion](./images/wffcff8a.png)

Depois de clicar em enviar, volte para o Workfront Fusion e clique no ícone de bolha no módulo **Adobe Firefly** para verificar os detalhes.

![WF Fusion](./images/wffcff9.png)

Acesse **OUTPUT** para **Details** > **url** para localizar o URL da imagem gerada pelo **Adobe Firefly**.

![WF Fusion](./images/wffcff10.png)

Copie o URL e cole-o no navegador. Agora você deve ver uma imagem que representa o prompt enviado pela solicitação do Postman, neste caso **misty meadows**.

![WF Fusion](./images/wffcff11.png)

## 1.2.4.2 Alterar plano de fundo do arquivo PSD

Agora você atualizará seu cenário para torná-lo mais inteligente usando mais conectores prontos para uso. Você também conectará a saída do Firefly ao Photoshop, para que a imagem de fundo do arquivo PSD seja alterada dinamicamente usando a saída da ação Gerar imagem do Firefly.

Você deverá ver isso. Em seguida, passe o mouse sobre o módulo **Adobe Firefly** e clique no ícone **+**.

![WF Fusion](./images/wffc15.png)

No menu de pesquisa, digite `Photoshop` e clique na ação **Adobe Photoshop**.

![WF Fusion](./images/wffc16.png)

Selecione **Aplicar edições do PSD**.

![WF Fusion](./images/wffc17.png)

Você deverá ver isso. Clique em **Adicionar** para adicionar uma nova conexão ao Adobe Photoshop.

![WF Fusion](./images/wffc18.png)

Configure sua conexão da seguinte maneira:

- Tipo de conexão: selecione **Adobe Photoshop (Servidor para Servidor)**
- Nome da conexão: digite `--aepUserLdap-- - Adobe I/O`
- ID do cliente: cole sua ID do cliente
- Segredo do cliente: cole seu Segredo do cliente

Clique em **Continuar**.

![WF Fusion](./images/wffc19.png)

Para encontrar sua **ID do Cliente** e **Segredo do Cliente**, vá para [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"} e abra seu projeto do Adobe I/O, denominado `--aepUserLdap-- One Adobe tutorial`. Vá para **OAuth Server-to-Server** para encontrar a ID do Cliente e o Segredo do Cliente. Copie esses valores e cole-os na configuração de conexão no Workfront Fusion.

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

Role para baixo até ver **Entrada**. Agora é necessário definir o que precisa ser inserido na camada de plano de fundo. Nesse caso, você precisa selecionar a saída do módulo **Adobe Firefly**, que contém a imagem gerada dinamicamente.

Para **Armazenamento**, selecione **Externo**. Para **Local do arquivo**, será necessário copiar e colar a variável `{{XX.details[].url}}` da saída do módulo **Adobe Firefly**, mas será necessário substituir **XX** na variável pelo número de sequência do módulo **Adobe Firefly**, que neste exemplo é **5**.

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

Clique em **Salvar** para salvar suas alterações e em **Executar uma vez** para testar sua configuração.

![WF Fusion](./images/wffc33a.png)

Vá para o Postman, verifique o prompt na sua solicitação e clique em **Enviar**.

![WF Fusion](./images/wffcff8a.png)

Você deverá ver isso. Clique na bolha no módulo **Adobe Photoshop - Aplicar edições do PSD**.

![WF Fusion](./images/wffc33b.png)

Agora você pode ver que um novo arquivo do PSD foi gerado com sucesso e armazenado em sua Conta de Armazenamento do Microsoft Azure.

![WF Fusion](./images/wffc33c.png)

## 1.2.4.3 Alterar camadas de texto do arquivo PSD

Em seguida, passe o mouse sobre o módulo **Adobe Photoshop - Aplicar edições do PSD** e clique no ícone **+**.

![WF Fusion](./images/wffc34.png)

Selecione **Adobe Photoshop**.

![WF Fusion](./images/wffc35.png)

Selecione **Editar camadas de texto**.

![WF Fusion](./images/wffc36.png)

Você deverá ver isso. Primeiro, selecione a conexão do Adobe Photoshop já configurada anteriormente, que deve ser chamada de `--aepUserLdap-- Adobe I/O`.

![WF Fusion](./images/wffc37.png)

Para o **Arquivo de entrada**, selecione **Azure** para **Armazenamento do arquivo de entrada** e certifique-se de selecionar a saída da solicitação anterior, **Adobe Photoshop - Aplicar edições do PSD**, que você pode definir da seguinte maneira: ``{{XX.data[].`_links`.renditions[].href}}`` (substitua XX pelo número de sequência do módulo anterior Adobe Photoshop - Aplicar edições do PSD).

Em seguida, clique em **+Adicionar item** em **Camadas** para começar a adicionar as camadas de texto que precisam ser atualizadas.

![WF Fusion](./images/wffc37a.png)

Há duas alterações a serem feitas, o texto do CTA e o texto do botão no arquivo **citisignal-fiber.psd** precisam ser atualizados.

Para localizar os nomes das camadas, abra o arquivo **citisignal-fiber.psd**. No arquivo, você observará que a camada que contém o call to action é chamada **2048x2048-cta**.

![WF Fusion](./images/wffc38.png)

No arquivo **citisignal-fiber.psd**, você também observará que a camada que contém o call to action é chamada **2048x2048-button-text**.

![WF Fusion](./images/wffc44.png)

Primeiro, é necessário configurar as alterações que devem ocorrer na camada **2048x2048-cta**. Insira o nome **2048x2048-cta** em **Nome** na caixa de diálogo.

![WF Fusion](./images/wffc39.png)

Role para baixo até ver **Texto** > **Conteúdo**. Selecione a variável **cta** na carga do Webhook. Clique em **Adicionar**.

![WF Fusion](./images/wffc40.png)

Você deverá ver isso. Clique em **+Adicionar item** em **Camadas** para começar a adicionar a próxima camada de texto que precisa ser atualizada.

![WF Fusion](./images/wffc40a.png)

Digite o nome **2048x2048-button-text** em **Nome** na caixa de diálogo.

![WF Fusion](./images/wffc40b.png)

Role para baixo até ver **Texto** > **Conteúdo**. Selecione a variável **button** na carga do Webhook. Clique em **Adicionar**.

![WF Fusion](./images/wffc40c.png)

Você deverá ver isso.

![WF Fusion](./images/wffc40d.png)

Role para baixo até ver **Saída**. Para **Armazenamento**, selecione **Azure**. Para **Local do arquivo**, insira o local abaixo. Observe a adição da variável `{{timestamp}}` ao nome de arquivo, que é usada para garantir que cada arquivo gerado tenha um nome exclusivo. Além disso, defina o **Type** como **vnd.adobe.photoshop**.

`{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text-{{timestamp}}.psd{{1.AZURE_STORAGE_SAS_WRITE}}`

Defina **Type** como **vnd.adobe.photoshop**. Clique em **OK**.

![WF Fusion](./images/wffc41.png)

Clique em **Salvar** para salvar as alterações.

![WF Fusion](./images/wffc47.png)

## 1.2.4.4 resposta do Webhook

Depois de aplicar essas alterações ao arquivo do Photoshop, agora é necessário configurar uma **resposta do Webhook** que será enviada de volta para o aplicativo que tiver ativado esse cenário.

Passe o mouse sobre o módulo **Adobe Photoshop - Editar camadas de texto** e clique no ícone **+**.

![WF Fusion](./images/wffc48.png)

Procure por `webhooks` e selecione **Webhook**.

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

Copie e cole a variável `{{XX.data[]._links.renditions[].href}}` e substitua **XX** pelo número de sequência do último módulo **Adobe Photoshop - Editar camadas de texto**, que neste caso é **7**.

![WF Fusion](./images/wffc52.png)

Habilite a caixa de seleção para **Mostrar configurações avançadas** e clique em **Adicionar item**.

![WF Fusion](./images/wffc52b.png)

No campo **Chave**, digite `Content-Type`. No campo **Valor**, digite `application/json`. Clique em **Adicionar**.

![WF Fusion](./images/wffc52a.png)

Você deveria ficar com isso. Clique em **OK**.

![WF Fusion](./images/wffc53.png)

Clique em **Alinhamento automático**.

![WF Fusion](./images/wffc54.png)

Você deverá ver isso. Clique em **Salvar** para salvar suas alterações e em **Executar uma vez** para testar seu cenário.

![WF Fusion](./images/wffc55.png)

Volte para o Postman e clique em **Enviar**. O prompt que está sendo usado aqui é **misty meadows**.

![WF Fusion](./images/wffc56.png)

O cenário será ativado e, após algum tempo, uma resposta será mostrada no Postman contendo o URL do arquivo do PSD recém-criado.

![WF Fusion](./images/wffc58.png)

Como lembrete: depois que o cenário for executado no Workfront Fusion, você poderá ver informações sobre cada módulo clicando na bolha acima de cada módulo.

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

Ir para [1.2.3 Frame.io e Workfront Fusion](./ex3.md){target="_blank"}

Retorne ao [Creative Workflow Automation with Workfront Fusion](./automation.md){target="_blank"}

Voltar para [Todos os Módulos](./../../../overview.md){target="_blank"}
