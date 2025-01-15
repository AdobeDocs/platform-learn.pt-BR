---
title: Introdução aos serviços do Firefly
description: Introdução aos serviços do Firefly
kt: 5342
doc-type: tutorial
exl-id: 23ebf8b4-3f16-474c-afe1-520d88331417
source-git-commit: c5d015fee3650d9c5a154f0b1374d27b20d2ea42
workflow-type: tm+mt
source-wordcount: '1759'
ht-degree: 2%

---

# 1.2.2 Uso de APIs Adobe no Workfront Fusion

## 1.2.2.1 Usar a API de texto para imagem do Firefly com o Workfront Fusion

Passe o mouse sobre o segundo nó **Definir várias variáveis** e clique em **+** para adicionar outro módulo.

![WF Fusion](./images/wffusion48.png)

Pesquise por **http** e selecione **HTTP**.

![WF Fusion](./images/wffusion49.png)

Selecione **Fazer uma solicitação**.

![WF Fusion](./images/wffusion50.png)

Selecione estas variáveis:

- **URL**: `https://firefly-api.adobe.io/v3/images/generate`
- **Método**: `POST`

Clique em **Adicionar um cabeçalho**.

![WF Fusion](./images/wffusion51.png)

Você precisa inserir os seguintes cabeçalhos:

| Chave | Valor |
|:-------------:| :---------------:| 
| `x-api-key` | sua variável armazenada para `CONST_client_id` |
| `Authorization` | `Bearer ` + sua variável armazenada para `bearer_token` |
| `Content-Type` | `application/json` |
| `Accept` | `*/*` |

Insira os detalhes de `x-api-key`. Clique em **Adicionar**.

![WF Fusion](./images/wffusion52.png)

Clique em **Adicionar um cabeçalho**.

![WF Fusion](./images/wffusion53.png)

Insira os detalhes de `Authorization`. Clique em **Adicionar**.

![WF Fusion](./images/wffusion54.png)

Clique em **Adicionar um cabeçalho**. Insira os detalhes de `Content-Type`. Clique em **Adicionar**.

![WF Fusion](./images/wffusion541.png)

Clique em **Adicionar um cabeçalho**. Insira os detalhes de `Accept`. Clique em **Adicionar**.

![WF Fusion](./images/wffusion542.png)

Defina o **Tipo de corpo** como **Bruto**. Para **Tipo de conteúdo**, selecione **JSON (application/json)**.

![WF Fusion](./images/wffusion55.png)

Cole esta carga no campo **Solicitar conteúdo**.

```json
{
  "numVariations": 1,
  "size": {
    "width": 2048,
    "height": 2048
  },
  "prompt": "Horses in a field",
  "promptBiasingLocaleCode": "en-US"
}
```

Marque a caixa de seleção de **Analisar resposta**. Clique em **OK**.

![WF Fusion](./images/wffusion56.png)

Clique em **Executar uma vez**.

![WF Fusion](./images/wffusion57.png)

Depois que o cenário for executado, você deverá ver isso.

![WF Fusion](./images/wffusion58.png)

Clique no **?Ícone** no quarto nó, HTTP, para ver a resposta. Você deve ver um arquivo de imagem na resposta.

![WF Fusion](./images/wffusion59.png)

Copie o URL da imagem e abra-o em uma janela do navegador. Você deverá ver algo assim:

![WF Fusion](./images/wffusion60.png)

Clique com o botão direito do mouse no objeto **HTTP** e renomeie-o para **Firefly T2I**.

![WF Fusion](./images/wffusion62.png)

Clique em **Salvar** para salvar as alterações.

![WF Fusion](./images/wffusion61.png)

## 1.2.2.2 Usar a API do Photoshop com o Workfront Fusion

Clique na **chave inglesa** entre os nós **Set Bearer Token** e **Firefly T2I**. Selecione **Adicionar um roteador**.

![WF Fusion](./images/wffusion63.png)

Clique com o botão direito do mouse no objeto **Firefly T2I** e selecione **Clone**.

![WF Fusion](./images/wffusion64.png)

Arraste e solte o objeto clonado próximo ao objeto **Roteador** e ele se conectará automaticamente ao **Roteador**. Você deveria ficar com isso.

![WF Fusion](./images/wffusion65.png)

Agora você tem uma cópia idêntica baseada na solicitação HTTP **Firefly T2I**. Algumas das configurações da solicitação HTTP **Firefly T2I** são semelhantes ao que você precisa para interagir com a **API Photoshop**, o que economiza tempo. Agora, basta alterar as variáveis que não são as mesmas, como o URL da solicitação e a carga.

Altere a **URL** para `https://image.adobe.io/pie/psdService/text`.

![WF Fusion](./images/wffusion66.png)

Substitua o **Conteúdo da solicitação** pela carga abaixo:

```json
{
  "inputs": [
    {
      "storage": "external",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/sevoi-psd.psd{{AZURE_STORAGE_SAS_READ}}"
    }
  ],
  "options": {
    "layers": [
      {
        "name": "2048x2048-button",
        "text": {
          "content": "Click here"
        }
      },
      {
        "name": "2048x2048-cta",
        "text": {
          "content": "Buy this stuff"
        }
      }
    ]
  },
  "outputs": [
    {
      "storage": "azure",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/sevoi-psd-changed-text.psd{{AZURE_STORAGE_SAS_WRITE}}",
      "type": "vnd.adobe.photoshop",
      "overwrite": true
    }
  ]
}
```

![WF Fusion](./images/wffusion67.png)

Para que este **Solicitar conteúdo** funcione corretamente, algumas variáveis estão ausentes:

- `AZURE_STORAGE_URL`
- `AZURE_STORAGE_CONTAINER`
- `AZURE_STORAGE_SAS_READ`
- `AZURE_STORAGE_SAS_WRITE`

Volte para o primeiro nó, clique em **Inicializar constantes** e selecione **Adicionar item** para cada uma dessas variáveis.

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

Você deveria ficar com isso. Clique em **OK**.

![WF Fusion](./images/wffusion68.png)

Em seguida, volte para a solicitação HTTP clonada para atualizar o **Conteúdo da solicitação**. Você observará essas variáveis pretas no **Solicitar conteúdo**, que são as variáveis que você copiou do Postman. Agora é necessário alterá-los para as variáveis recém-definidas no Workfront Fusion. Substitua cada variável uma por uma excluindo o texto em preto e substituindo-o pela variável correta.

![WF Fusion](./images/wffusion70.png)

Há 3 alterações a serem feitas na seção **entradas**.

![WF Fusion](./images/wffusion71.png)

Também há 3 alterações a serem feitas na seção **saídas**. Clique em **OK**.

![WF Fusion](./images/wffusion72.png)

Clique com o botão direito no nó clonado e selecione **Renomear**. Altere o nome para **Photoshop Change Text**.

![WF Fusion](./images/wffusion73.png)

Você deveria ficar com isso.

![WF Fusion](./images/wffusion74.png)

Clique em **Executar uma vez**.

![WF Fusion](./images/wffusion75.png)

Clique no ícone **search** no nó **Photoshop Change Text** para ver a resposta. Você deve ter uma resposta semelhante a esta, com um link para um arquivo de status.

![WF Fusion](./images/wffusion76.png)

Antes de continuar com as interações da API do Photoshop, vamos desabilitar a rota para o nó **Firefly T2I** para não enviar chamadas de API desnecessárias para esse ponto de extremidade de API. Clique na **chave inglesa** e selecione **Desabilitar rota**.

![WF Fusion](./images/wffusion77.png)

Você deveria ficar com isso.

![WF Fusion](./images/wffusion78.png)

Em seguida, adicione outro nó **Definir várias variáveis**.

![WF Fusion](./images/wffusion79.png)

Coloque-o depois do nó **Photoshop Change Text**.

![WF Fusion](./images/wffusion80.png)

Clique no nó **Definir várias variáveis** e selecione **Adicionar item**. Selecione o valor da variável na resposta da solicitação anterior.

| Nome da variável | Valor da variável |
|:-------------:| :---------------:| 
| `psdStatusUrl` | `data > _links > self > href` |

Clique em **Adicionar**.

![WF Fusion](./images/wffusion81.png)

Clique em **OK**.

![WF Fusion](./images/wffusion82.png)

Clique com o botão direito do mouse no nó **Photoshop Change Text** e selecione **Clone**.

![WF Fusion](./images/wffusion83.png)

Arraste a solicitação HTTP clonada após o nó **Definir várias variáveis** que você acabou de criar.

![WF Fusion](./images/wffusion83.png)

Clique com o botão direito na solicitação HTTP clonada, selecione **Renomear** e altere o nome para **Status de verificação do Photoshop**.

![WF Fusion](./images/wffusion84.png)

Clique em para abrir a solicitação HTTP. Altere a URL para que ela faça referência à variável criada na etapa anterior e defina o **Método** como **GET**.

![WF Fusion](./images/wffusion85.png)

Remova o **Corpo** selecionando a opção vazia.

![WF Fusion](./images/wffusion86.png)

Clique em **OK**.

![WF Fusion](./images/wffusion87.png)

Clique em **Executar uma vez**.

![WF Fusion](./images/wffusion88.png)

Em seguida, você deve obter uma resposta que contenha o campo **status**, com o status definido como **em execução**. O Photoshop leva alguns segundos para concluir o processo.

![WF Fusion](./images/wffusion89.png)

Agora que você sabe que a resposta precisa de um pouco mais de tempo para ser concluída, talvez seja uma boa ideia adicionar um cronômetro na frente dessa solicitação HTTP para que ela não seja executada imediatamente.

Clique no nó **Ferramentas** e selecione **Suspender**.

![WF Fusion](./images/wffusion90.png)

Posicione o nó **Suspensão** entre **Definir várias variáveis** e **Verificar Status do Photoshop**. Defina o **Atraso** para **5** segundos. Clique em **OK**.

![WF Fusion](./images/wffusion91.png)

Então você terá isto. O desafio com a configuração abaixo é que 5 segundos de espera podem ser suficientes, mas talvez não sejam suficientes. Na realidade, seria melhor ter uma solução mais inteligente, como um loop do...while que verifica o status a cada 5 segundos até que o status seja igual a **bem-sucedido**. Agora, você implementará essa tática nas próximas etapas.

![WF Fusion](./images/wffusion92.png)

Clique na **chave inglesa** entre **Definir várias variáveis** e **Suspender**. Selecione **Adicionar módulo**.

![WF Fusion](./images/wffusion93.png)

Pesquise por `flow` e selecione **Controle de Fluxo**.

![WF Fusion](./images/wffusion94.png)

Selecione **Repetidor**.

![WF Fusion](./images/wffusion95.png)

Definir as **Repetições** a **20**. Clique em **OK**.

![WF Fusion](./images/wffusion96.png)

Em seguida, clique em **+** no **Photoshop Check Status** para adicionar outro módulo.

![WF Fusion](./images/wffusion97.png)

Pesquise por **flow** e selecione **Flow Control**.

![WF Fusion](./images/wffusion98.png)

Selecione **Agregador de Matriz**.

![WF Fusion](./images/wffusion99.png)

Definir **Módulo Source** como **Repetidor**. Clique em **OK**.

![WF Fusion](./images/wffusion100.png)

Você deve ter isto:

![WF Fusion](./images/wffusion101.png)

Clique na **chave inglesa** e selecione **Adicionar um módulo**.

![WF Fusion](./images/wffusion102.png)

Pesquise por **ferramentas** e selecione **Ferramentas**.

![WF Fusion](./images/wffusion103.png)

Selecione **Obter várias variáveis**.

![WF Fusion](./images/wffusion104.png)

Clique em **+ Adicionar item** e defina o **Nome da variável** como `done`.

![WF Fusion](./images/wffusion105.png)

Clique em **OK**.

![WF Fusion](./images/wffusion106.png)

Clique no nó **Definir várias variáveis** que você configurou anteriormente. Para inicializar a variável **concluído**, é necessário defini-la aqui como `false`. Clique em **+ Adicionar item**.

![WF Fusion](./images/wffusion107.png)

Para o **nome da variável**, use `done`. Para definir o status, é necessário um valor booleano. Para localizar o valor booleano, clique no ícone de **engrenagem** e selecione `false`. Clique em **Adicionar**.

![WF Fusion](./images/wffusion108.png)

Clique em **OK**.

![WF Fusion](./images/wffusion109.png)

Em seguida, clique no ícone **chave inglesa** depois do nó **Get multiple variables** que você configurou.

![WF Fusion](./images/wffusion110.png)

Selecione **Configurar um filtro**. Agora é necessário verificar o valor da variável **concluído**. Se o valor for definido como **false**, a próxima parte do loop deverá ser executada. Se o valor estiver definido como **true**, significa que o processo já foi concluído com êxito, portanto, não há necessidade de continuar com a próxima parte do loop.

![WF Fusion](./images/wffusion111.png)

Para o rótulo, use **Concluído?**. Defina a **Condição** usando a variável já existente **concluída**, o operador deve ser definido como **Igual a** e o valor deve ser a variável booleana `false`. Clique em **OK**.

![WF Fusion](./images/wffusion112.png)

Em seguida, libere espaço entre os nós **Status de verificação do Photoshop** e **Agregador de matriz**. Em seguida, clique no ícone **chave inglesa** e selecione **Adicionar um roteador**. Você está fazendo isso porque, após verificar o status do arquivo Photoshop, deve haver dois caminhos. Se o status for `succeeded`, a variável de **concluído** deverá ser definida como `true`. Se o status não for igual a `succeeded`, o loop deve continuar. O roteador permitirá verificar e definir isso.

![WF Fusion](./images/wffusion113.png)

Depois de adicionar o roteador, clique no ícone **chave inglesa** e selecione **Configurar um filtro**.

![WF Fusion](./images/wffusion114.png)

Para o rótulo, use **Concluído**. Defina a **Condição** usando a resposta do nó **Verificar Status do Photoshop** escolhendo o campo de resposta **dados.saídas[].status**. O operador deve ser definido como **Igual a** e o valor deve ser `succeeded`. Clique em **OK**.

![WF Fusion](./images/wffusion115.png)

Em seguida, clique no nó vazio com o ponto de interrogação e procure **ferramentas**. Em seguida, selecione **Ferramentas**.

![WF Fusion](./images/wffusion116.png)

Selecione **Definir várias variáveis**.

![WF Fusion](./images/wffusion117.png)

Quando essa ramificação do roteador é usada, significa que o status da criação do arquivo Photoshop foi concluído com êxito. Isso significa que o loop do...while não precisa mais continuar verificando o status no Photoshop, então você deve definir a variável `done` como `true`.

Para o **nome da variável**, use `done`. Para o **valor de variável**, você deve usar o valor booleano `true`. Clique no ícone de **engrenagem** e selecione `true`. Clique em **Adicionar**.

![WF Fusion](./images/wffusion118.png)

Clique em **OK**.

![WF Fusion](./images/wffusion119.png)

Em seguida, clique com o botão direito do mouse no nó **Definir várias variáveis** que acabou de criar e selecione **Clonar**.

![WF Fusion](./images/wffusion120.png)

Arraste o nó clonado para que ele se conecte com o **agregador de matriz**. Em seguida, clique com o botão direito do mouse no nó e selecione **Renomear** e altere o nome para `Placeholder End`.

![WF Fusion](./images/wffusion122.png)

Remova a variável existente e clique em **+ Adicionar item**. Para o **Nome da variável**, use `placeholder`, para o **Valor da variável**, use `end`. Clique em **Adicionar** e em **OK**.

![WF Fusion](./images/wffusion123.png)

Clique em **Salvar** para salvar seu cenário. Em seguida, clique em **Executar uma vez**.

![WF Fusion](./images/wffusion124.png)

Seu cenário será executado e deve ser concluído com êxito. Você observará que o loop do...while que você configurou funcionou bem. Na execução abaixo, você pode ver que o **Repetidor** foi executado 20 vezes com base na bolha no nó **Ferramentas > Obter várias variáveis**. Depois desse nó, você configurou um filtro que verificou o status e, somente se o status não for igual a **bem-sucedido**, os próximos nós serão executados. Nesta execução, a parte após o filtro foi executada apenas uma vez, pois o status já era **bem-sucedido** na primeira execução.

![WF Fusion](./images/wffusion125.png)

Você pode verificar o status da criação do novo arquivo do Photoshop clicando na bolha da solicitação HTTP **Verificar status** do Photoshop e detalhando o campo **status**.

![WF Fusion](./images/wffusion126.png)

Agora você configurou a versão básica de um cenário repetível que automatiza várias etapas. No próximo exercício, você vai iterar nisso adicionando complexidade.

Próxima etapa: [1.2.3 Automação de processos com o Workfront Fusion](./ex3.md)

[Voltar ao módulo 1.2](./automation.md)

[Voltar a todos os módulos](./../../../overview.md)
