---
title: Executar o fluxo de trabalho personalizado de forma programática
description: Executar o fluxo de trabalho personalizado de forma programática
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
source-git-commit: a3a78b12f8244c8288eb0fffc82ad769776eb118
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# 1.7.2 Execute o fluxo de trabalho personalizado de forma programática

## 1.7.2.1 Execute seu fluxo de trabalho personalizado com o Postman

Depois de publicar seu fluxo de trabalho no exercício anterior, você verá algo como isso. Clique no botão **Copiar** para copiar a carga de exemplo.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw61.png)

Abra o Postman e crie uma nova **Coleção** usando o nome **Fluxos de Trabalho Personalizados do Firefly**. Clique em **adicionar solicitação**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw62.png)

Você deverá ver uma nova solicitação vazia. Na barra de endereços, cole a carga útil copiada do fluxo de trabalho publicado.

O Postman reconhecerá o comando cURL que você colou e coletará todas as informações da carga e as adicionará na solicitação da maneira correta para você.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw63.png)

Agora você deve ver estas **variáveis de cabeçalho**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw64.png)

Vá para **Corpo**, onde você deve ver algo semelhante a isto.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw65.png)

Agora é necessário fornecer as instruções necessárias no corpo desta solicitação. Ao trabalhar com arquivos de forma programática, o uso de URLs pré-assinados é necessário. Para este exercício, você pode encontrar URLs pré-assinados abaixo para as 3 imagens que fazem parte deste exercício. Esses URLs pré-assinados foram criados usando os recursos de armazenamento do Microsoft Azure. Se quiser saber mais sobre como criar URLs pré-assinados, confira aqui: [Otimize seu processo do Firefly usando o Microsoft Azure e URLs pré-assinados](./../module1.1/ex2.md).

Para este exercício, você pode usar os URLs abaixo para que não seja necessário criar novos URLs pré-assinados.

- **airpods.jpg**

```
https://techinsiders.blob.core.windows.net/vangeluw/airpods.jpg?sv=2023-01-03&st=2026-03-11T01%3A22%3A04Z&se=2027-03-12T01%3A22%3A00Z&sr=b&sp=r&sig=MmQi9lS4lm4DJM1BELmZZM7VLa4ln5zYOcuGisLnrz4%3D
```

- **watch.jpg**

```
https://techinsiders.blob.core.windows.net/vangeluw/watch.jpg?sv=2023-01-03&st=2026-03-11T01%3A26%3A54Z&se=2027-03-12T01%3A26%3A00Z&sr=b&sp=r&sig=xCwQ09E%2F%2FT%2B7RLcb31Fum4uUBfsX0xHITKZTz4Ds9Zs%3D
```

- **phone.jpg**

```
https://techinsiders.blob.core.windows.net/vangeluw/phone.png?sv=2023-01-03&st=2026-03-11T01%3A27%3A20Z&se=2027-03-12T01%3A27%3A00Z&sr=b&sp=r&sig=VVbX88P2sFSHHo9lmgoRhXRIXb42c0nDQhM9Z8nUG%2Bc%3D
```

Você também precisa fornecer prompts como parte da solicitação do Postman. Abaixo estão os prompts que você pode usar.

- **Prompt 1**:

```
magazine quality photo of a phone on a red pedestal with a pink background surrounded by origami style pink paper hearts
```

- **Prompt 2**:

```
background hearts fluttering
```

Esta é uma amostra de carga, mas você não pode copiá-la e reutilizá-la, pois os campos **node_id** são exclusivos para o seu fluxo de trabalho, portanto, isso é apenas para dar uma ideia de como a carga deve ser:

```json
{
    "workflow": {
        "workflowId": "e0c63806-cf7c-442d-8884-26d57e9c0518",
        "inputs": [
            [
                {
                    "node_id": "node_1772156869527_d8mjasues_1_u10dlg",
                    "content": [
                        {
                            "presignedUrl": "https://techinsiders.blob.core.windows.net/vangeluw/airpods.jpg?sv=2023-01-03&st=2026-03-11T01%3A22%3A04Z&se=2027-03-12T01%3A22%3A00Z&sr=b&sp=r&sig=MmQi9lS4lm4DJM1BELmZZM7VLa4ln5zYOcuGisLnrz4%3D",
                            "storageType": "Azure"
                        }
                    ]
                },
                {
                    "node_id": "node_1772157264659_oq2csr2nn_5_fh5hek",
                    "content": "magazine quality photo of a phone on a red pedestal with a pink background surrounded by origami style pink paper hearts"
                },
                {
                    "node_id": "node_1772157397147_qdwxiyktg_8_nm0o2k",
                    "content": "background hearts fluttering"
                }
            ]
        ]
    }
}
```

Depois de fazer as alterações na carga, ela deve ficar assim. Depois de concluído, clique em **Enviar**. Em seguida, use **CMD + S** ou **CTRL + S** para **salvar** sua solicitação.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw66.png)

Na carga de resposta, agora é possível encontrar alguns links. Esses links permitem consultar o **status** do fluxo de trabalho e, uma vez que o status seja **concluído**, você poderá usar a URL de **resultados** para recuperar a imagem e o vídeo gerados.

Selecione a URL do **status** e copie-a.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw67.png)

Clique nos 3 pontos na solicitação que você está usando no momento e selecione **Duplicar**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw69.png)

Na nova solicitação, altere o tipo de solicitação para **GET** e substitua a URL pela URL de status que você acabou de copiar.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw70.png)

Em **Corpo**, verifique se tudo foi excluído. Em seguida, clique em **Enviar**. Você deve receber uma carga de resposta semelhante, que mostrará um status. Você pode reenviar esta solicitação até que o status seja alterado para **concluído**. Não esqueça de usar **CMD + S** ou **CTRL + S** para **salvar** sua solicitação.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw71.png)

Volte para a primeira solicitação **POST**. Agora copie a URL de **resultados**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw72.png)

Clique nos 3 pontos **...** na segunda solicitação criada e selecione **Duplicar**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw73.png)

Na nova solicitação, cole a URL de **resultados** copiada e clique em **Enviar**. Não esqueça de usar **CMD + S** ou **CTRL + S** para **salvar** sua solicitação.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw74.png)

Role para baixo na carga de resposta, onde você encontrará referências à imagem e ao vídeo que foram criados. Clique nos links para abrir esses arquivos.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw75.png)

Aqui está a imagem que foi gerada.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw76.png)

## 1.7.2.2 Execute seu fluxo de trabalho personalizado com o Workfront Fusion

Ir para [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Abra o **Workfront Fusion**.

![WF Fusion](./images/wffusion1.png)

Vá para **Cenários**. Se você ainda não tiver uma pasta, crie uma pasta e, para o nome da pasta, use: `--aepUserLdap--`. Selecione sua pasta e, em seguida, selecione **Criar novo cenário**.

![WF Fusion](./images/wffusion2.png)

Você deverá ver isso.

![WF Fusion](./images/wffusion3.png)

Depois de publicar seu fluxo de trabalho no exercício anterior, você verá algo como isso. Clique no botão **Copiar** para copiar a carga de exemplo.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw61.png)

Volte para o cenário do Workfront Fusion. Use **CMD + V** ou **CTRL + V** para colar a carga copiada no cenário. O Workfront Fusion detectará automaticamente a solicitação cURL e criará um novo módulo **HTTP - Fazer uma solicitação** automaticamente.

Arraste o ícone **relógio** para o módulo **HTTP - Fazer uma solicitação**.

![WF Fusion](./images/wffusion5.png)

Você deverá ver isso. Clique no módulo **HTTP - Fazer uma solicitação** para abri-lo.

![WF Fusion](./images/wffusion6.png)

Você deve ver que as variáveis **Header** já estão disponíveis.

![WF Fusion](./images/wffusion7.png)

Role para baixo para ver a carga útil padrão. Clique no **ícone** conforme indicado para embelezar a carga JSON.

![WF Fusion](./images/wffusion8.png)

Volte para o Postman, para a primeira solicitação **POST**. Copie a carga.

![WF Fusion](./images/wffusion9.png)

Volte para o cenário do Workfront Fusion. Substitua a carga padrão existente pela carga copiada do Postman. Clique no **ícone** conforme indicado para embelezar a carga JSON.

Marque a caixa de seleção de **Analisar resposta**.

Clique em **OK**.

![WF Fusion](./images/wffusion10.png)

Salve as alterações e clique em **Executar uma vez**.

![WF Fusion](./images/wffusion11.png)

Depois que o cenário for executado, você poderá ver uma resposta semelhante à recebida no Postman. Com essas informações disponíveis no Workfront Fusion, agora é possível criar uma base para sondar a URL de **status** até que o status seja concluído. Depois disso, você poderá usar a URL de **resultados** para coletar a imagem e o vídeo gerados.

![WF Fusion](./images/wffusion12.png)

## Próximas etapas

Voltar para [Fluxos de Trabalho Personalizados do Firefly](./workflowbuilder.md){target="_blank"}

Voltar para [Todos os Módulos](./../../../overview.md){target="_blank"}
