---
title: Introdução aos serviços do Firefly
description: Introdução aos serviços do Firefly
kt: 5342
doc-type: tutorial
exl-id: 23ebf8b4-3f16-474c-afe1-520d88331417
source-git-commit: a0c16a47372d322a7931578adca30a246b537183
workflow-type: tm+mt
source-wordcount: '594'
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

Próxima Etapa: [1.2.3 ...](./ex3.md)

[Voltar ao módulo 1.2](./automation.md)

[Voltar a todos os módulos](./../../../overview.md)
