---
title: Usar APIs do Adobe no Workfront Fusion
description: Saiba como usar APIs do Adobe no Workfront Fusion
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 23ebf8b4-3f16-474c-afe1-520d88331417
source-git-commit: 603e48e0453911177823fe7ceb340f8ca801c5e1
workflow-type: tm+mt
source-wordcount: '1749'
ht-degree: 0%

---

# 1.2.2 Uso de APIs do Adobe no Workfront Fusion

Saiba como usar APIs do Adobe no Workfront Fusion.

## 1.2.2.1 Usar a API Texto para Imagem do Firefly com o Workfront Fusion

Passe o mouse sobre o segundo nó **Definir várias variáveis** e selecione **+** para adicionar outro módulo.

![WF Fusion](./images/wffusion48.png)

Pesquise por **http** e selecione **HTTP**.

![WF Fusion](./images/wffusion49.png)

Selecione **Fazer uma solicitação**.

![WF Fusion](./images/wffusion50.png)

Selecione estas variáveis:

- **URL**: `https://firefly-api.adobe.io/v3/images/generate`
- **Método**: `POST`

Selecione **Adicionar um cabeçalho**.

![WF Fusion](./images/wffusion51.png)

Insira os seguintes cabeçalhos:

| Chave | Valor |
|:-------------:| :---------------:| 
| `x-api-key` | sua variável armazenada para `CONST_client_id` |
| `Authorization` | `Bearer ` + sua variável armazenada para `bearer_token` |
| `Content-Type` | `application/json` |
| `Accept` | `*/*` |

Insira os detalhes de `x-api-key`. Selecione **Adicionar**.

![WF Fusion](./images/wffusion52.png)

Selecione **Adicionar um cabeçalho**.

![WF Fusion](./images/wffusion53.png)

Insira os detalhes de `Authorization`. Selecione **Adicionar**.

![WF Fusion](./images/wffusion54.png)

Selecione **Adicionar um cabeçalho**. Insira os detalhes de `Content-Type`. Selecione **Adicionar**.

![WF Fusion](./images/wffusion541.png)

Selecione **Adicionar um cabeçalho**. Insira os detalhes de `Accept`. Selecione **Adicionar**.

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

Marque a caixa **Analisar resposta**. Selecione **OK**.

![WF Fusion](./images/wffusion56.png)

Selecione **Executar uma vez**.

![WF Fusion](./images/wffusion57.png)

Sua tela deve ter esta aparência.

![WF Fusion](./images/wffusion58.png)

Selecionar o **?Ícone** no quarto nó, HTTP, para ver a resposta. Você deve ver um arquivo de imagem na resposta.

![WF Fusion](./images/wffusion59.png)

Copie o URL da imagem e abra-o em uma janela do navegador. Sua tela deve ter esta aparência:

![WF Fusion](./images/wffusion60.png)

Clique com o botão direito em **HTTP** e renomeie para **Firefly T2I**.

![WF Fusion](./images/wffusion62.png)

Selecione **Salvar** para salvar suas alterações.

![WF Fusion](./images/wffusion61.png)

## 1.2.2.2 Usar a API do Photoshop com o Workfront Fusion

Selecione **** a chave entre os nós **Set Bearer Token** e **Firefly T2I**. Selecione **Adicionar um roteador**.

![WF Fusion](./images/wffusion63.png)

Clique com o botão **direito do mouse no objeto Firefly T2I** e selecione **Clonar**.

![WF Fusion](./images/wffusion64.png)

Arraste e solte o objeto clonado perto do **objeto Roteador** , ele se conecta automaticamente ao **Roteador**. Sua tela deve ter esta aparência:

![WF Fusion](./images/wffusion65.png)

Agora você tem uma cópia idêntica baseada na solicitação HTTP **Firefly T2I**. Algumas das configurações da solicitação HTTP **Firefly T2I** são semelhantes ao que você precisa para interagir com a **API Photoshop**, o que economiza tempo. Agora, você só precisa alterar as variáveis que não são as mesmas, como o URL da solicitação e a carga.

Altere a **URL** para `https://image.adobe.io/pie/psdService/text`.

![WF Fusion](./images/wffusion66.png)

Substituir **Solicitar conteúdo** pela carga abaixo:

```json
  {
    "inputs": [
      {
        "storage": "external",
        "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber.psd{{AZURE_STORAGE_SAS_READ}}"
      }
    ],
    "options": {
      "layers": [
        {
          "name": "2048x2048-button-text",
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
        "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text.psd{{AZURE_STORAGE_SAS_WRITE}}",
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

Em seguida, volte para a solicitação HTTP clonada para atualizar o **Conteúdo da solicitação**. Observe as variáveis pretas em **Solicitar conteúdo**, que são as variáveis copiadas do Postman. É necessário alterar para as variáveis recém-definidas no Workfront Fusion. Substitua cada variável uma por uma excluindo o texto em preto e substituindo-o pela variável correta.

![WF Fusion](./images/wffusion70.png)

Faça estas 3 alterações na seção **entradas**. Selecione **OK**.

![WF Fusion](./images/wffusion71.png)

Faça estas 3 alterações na seção **saídas**. Selecione **OK**.

![WF Fusion](./images/wffusion72.png)

Clique com o botão direito no nó clonado e selecione **Renomear**. Altere o nome para **Photoshop Change Text**.

![WF Fusion](./images/wffusion73.png)

Sua tela deve ter esta aparência:

![WF Fusion](./images/wffusion74.png)

Selecione **Executar uma vez**.

![WF Fusion](./images/wffusion75.png)

Selecione o ícone de **pesquisa** no nó **Texto de Alteração do Photoshop** para ver a resposta. Você deve ter uma resposta semelhante a esta, com um link para um arquivo de status.

![WF Fusion](./images/wffusion76.png)

Antes de continuar com as interações de API do Photoshop, desabilite a rota para o nó **Firefly T2I** para não enviar chamadas de API desnecessárias para esse ponto de extremidade de API. Selecione o ícone de **chave inglesa** e selecione **Desabilitar rota**.

![WF Fusion](./images/wffusion77.png)

Sua tela deve ter esta aparência:

![WF Fusion](./images/wffusion78.png)

Em seguida, adicione outro nó **Definir várias variáveis**.

![WF Fusion](./images/wffusion79.png)

Coloque-o depois do nó **Photoshop Change Text**.

![WF Fusion](./images/wffusion80.png)

Selecione o nó **Definir várias variáveis**, selecione **Adicionar item**. Selecione o valor da variável na resposta da solicitação anterior.

| Nome da variável | Valor da variável |
|:-------------:| :---------------:| 
| `psdStatusUrl` | `data > _links > self > href` |

Selecione **Adicionar**.

![WF Fusion](./images/wffusion81.png)

Selecione **OK**.

![WF Fusion](./images/wffusion82.png)

Clique com o botão direito do mouse no nó **Photoshop Change Text** e selecione **Clone**.

![WF Fusion](./images/wffusion83.png)

Arraste a solicitação HTTP clonada após o nó **Definir várias variáveis** que você acabou de criar.

![WF Fusion](./images/wffusion83.png)

Clique com o botão direito do mouse na solicitação HTTP clonada, selecione **Renomear** e altere o nome para **Status de verificação** Photoshop.

![WF Fusion](./images/wffusion84.png)

Selecione para abrir a solicitação HTTP. Altere o URL para que ele faça referência aos variável criados na etapa anterior e defina o **Método** para **GET**.

![WF Fusion](./images/wffusion85.png)

Remova o **Corpo** selecionando a opção vazia.

![WF Fusion](./images/wffusion86.png)

Selecione **OK**.

![WF Fusion](./images/wffusion87.png)

Selecione **Executar uma vez**.

![WF Fusion](./images/wffusion88.png)

Uma resposta que contém o campo **status**, com o status definido como **em execução** é exibida. O Photoshop leva alguns segundos para concluir o processo.

![WF Fusion](./images/wffusion89.png)

Agora que você sabe que a resposta precisa de um pouco mais de tempo para ser concluída, talvez seja uma boa ideia adicionar um cronômetro na frente dessa solicitação HTTP para que ela não seja executada imediatamente.

Selecione o nó **Ferramentas** e selecione **Suspender**.

![WF Fusion](./images/wffusion90.png)

Posicione o nó **Suspensão** entre **Definir várias variáveis** e **Verificar Status do Photoshop**. Defina o **Atraso** para **5** segundos. Selecione **OK**.

![WF Fusion](./images/wffusion91.png)

Sua tela deve ter esta aparência. O desafio com a configuração abaixo é que 5 segundos de espera podem ser suficientes, mas talvez não sejam suficientes. Na realidade, seria melhor ter uma solução mais inteligente, como um loop do...while que verifica o status a cada 5 segundos até que o status seja igual a **bem-sucedido**. Então, você pode implementar essa tática nas próximas etapas.

![WF Fusion](./images/wffusion92.png)

Selecione a **chave inglesa** entre **Definir várias variáveis** e **Suspender**. Selecione **Adicionar módulo**.

![WF Fusion](./images/wffusion93.png)

Pesquise por `flow` e selecione **Controle de Fluxo**.

![WF Fusion](./images/wffusion94.png)

Selecione **Repetidor**.

![WF Fusion](./images/wffusion95.png)

Definir **Repetições** a **20**. Selecione **OK**.

![WF Fusion](./images/wffusion96.png)

Em seguida, selecione **+** no **Photoshop Check Status** para adicionar outro módulo.

![WF Fusion](./images/wffusion97.png)

Pesquise por **flow** e selecione **Flow Control**.

![WF Fusion](./images/wffusion98.png)

Selecione **Agregador de Matriz**.

![WF Fusion](./images/wffusion99.png)

Definir **Módulo Source** como **Repetidor**. Selecione **OK**.

![WF Fusion](./images/wffusion100.png)

Sua tela deve ter esta aparência:

![WF Fusion](./images/wffusion101.png)

Selecione o ícone da **chave inglesa** e selecione **Adicionar um módulo**.

![WF Fusion](./images/wffusion102.png)

Pesquise por **ferramentas** e selecione **Ferramentas**.

![WF Fusion](./images/wffusion103.png)

Selecione **Obter várias variáveis**.

![WF Fusion](./images/wffusion104.png)

Selecione **+ Adicionar item** e defina o **Nome da variável** como `done`.

![WF Fusion](./images/wffusion105.png)

Selecione **OK**.

![WF Fusion](./images/wffusion106.png)

Selecione o nó **Definir várias variáveis** que você configurou anteriormente. Para inicializar a variável **concluído**, é necessário defini-la aqui como `false`. Selecione **+ Adicionar item**.

![WF Fusion](./images/wffusion107.png)

Use `done` para o **Nome da variável**

Para definir o status, é necessário um valor booleano. Para localizar o valor booleano, selecione **engrenagem** e depois `false`. Selecione **Adicionar**.

![WF Fusion](./images/wffusion108.png)

Selecione **OK**.

![WF Fusion](./images/wffusion109.png)

Próximo, selecione **o**&#x200B;ícone chave depois que as **variáveis Obter várias** nó configuradas.

![WF Fusion](./images/wffusion110.png)

Selecione **Configurar um filtro**. Agora, é necessário verificar o valor do variável **realizada**. Se esse valor for definido como **false**, a próxima parte do loop deverá ser executada. Se o valor estiver definido **como true**, significa que o processo já foi concluído com êxito, portanto, não há necessidade de continuar com a próxima parte do loop.

![WF Fusion](./images/wffusion111.png)

Para o rótulo, use **Concluído?**. Defina a **Condição** usando a variável já existente **concluída**, o operador deve ser definido como **Igual a** e o valor deve ser a variável booleana `false`. Selecione **OK**.

![WF Fusion](./images/wffusion112.png)

Em seguida, libere espaço entre os nós **Status de verificação do Photoshop** e **Agregador de matriz**. Em seguida, selecione o ícone **chave inglesa** e selecione **Adicionar um roteador**. Você está fazendo isso porque, após verificar o status do arquivo Photoshop, deve haver dois caminhos. Se o status for `succeeded`, a variável de **concluído** deverá ser definida como `true`. Se o status não for igual a `succeeded`, o loop deve continuar. O roteador permitirá verificar e definir isso.

![WF Fusion](./images/wffusion113.png)

Depois de adicionar o roteador, selecione o ícone de **chave inglesa** e selecione **Configurar um filtro**.

![WF Fusion](./images/wffusion114.png)

Para o rótulo, use **Concluído**. Defina a **Condição** usando a resposta do nó **Verificar Status do Photoshop** escolhendo o campo de resposta **dados.saídas[].status**. O operador deve ser definido como **Igual a** e o valor deve ser `succeeded`. Selecione **OK**.

![WF Fusion](./images/wffusion115.png)

Em seguida, selecione o nó vazio com o ponto de interrogação e procure **ferramentas**. Em seguida, selecione **Ferramentas**.

![WF Fusion](./images/wffusion116.png)

Selecione **Definir várias variáveis**.

![WF Fusion](./images/wffusion117.png)

Quando essa ramificação do roteador é usada, significa que o status da criação do arquivo Photoshop foi concluído com êxito. Isso significa que o loop do...while não precisa mais continuar verificando o status no Photoshop, então você deve definir a variável `done` como `true`.

Para o **nome da variável**, use `done`.

Para o **valor de variável**, você deve usar o valor booleano `true`. Selecione o ícone de **engrenagem** e selecione `true`. Selecione **Adicionar**.

![WF Fusion](./images/wffusion118.png)

Selecione **OK**.

![WF Fusion](./images/wffusion119.png)

Em seguida, clique com o botão direito do mouse no nó **Definir várias variáveis** que acabou de criar e selecione **Clonar**.

![WF Fusion](./images/wffusion120.png)

Arraste o nó clonado para que ele se conecte com o **agregador de matriz**. Em seguida, clique com o botão direito do mouse no nó e selecione **Renomear** e altere o nome para `Placeholder End`.

![WF Fusion](./images/wffusion122.png)

Remova a variável existente e selecione **+ Adicionar item**. Para o **Nome da variável**, use `placeholder`, para o **Valor da variável**, use `end`. Selecione **Adicionar** e **OK**.

![WF Fusion](./images/wffusion123.png)

Selecione **Salvar** para salvar seu cenário. Em seguida, selecione   **Executar uma vez**.

![WF Fusion](./images/wffusion124.png)

O cenário é executado e deve ser concluído com êxito. Observe que o loop do...while configurado funciona bem. Na execução abaixo, você pode ver que o **Repetidor** foi executado 20 vezes com base na bolha no nó **Ferramentas > Obter várias variáveis**. Depois desse nó, você configurou um filtro que verificou o status e, somente se o status não for igual a **bem-sucedido**, os próximos nós serão executados. Nesta execução, a parte após o filtro foi executada apenas uma vez, pois o status já era **bem-sucedido** na primeira execução.

![WF Fusion](./images/wffusion125.png)

Você pode verificar o status da criação do novo arquivo do Photoshop clicando na bolha da solicitação HTTP **Verificar status** do Photoshop e detalhando o campo **status**.

![WF Fusion](./images/wffusion126.png)

Agora você configurou a versão básica de um cenário repetível que automatiza várias etapas. No próximo exercício, você vai iterar nisso adicionando complexidade.

## Próximas etapas

Ir para [Automação de processos com o Workfront Fusion](./ex3.md){target="_blank"}

Retorne ao [Creative Workflow Automation with Workfront Fusion](./automation.md){target="_blank"}

Voltar para [Todos os Módulos](./../../../overview.md){target="_blank"}
