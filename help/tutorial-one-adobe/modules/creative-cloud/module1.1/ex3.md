---
title: Trabalho com APIs do Photoshop
description: Saiba como trabalhar com as APIs do Photoshop e os serviços da Firefly
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 60eecc24-1713-4fec-9ffa-a3186db1a8ca
source-git-commit: d33df99e9c75e7d5feef503b68174b93860ac245
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 0%

---

# 1.1.3 Trabalho com APIs do Photoshop

Saiba como trabalhar com as APIs do Photoshop e os Serviços da Firefly.

## 1.1.3.1 Atualizar a integração do Adobe I/O

1. Ir para [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}.

![Nova integração do Adobe I/O](./images/iohome.png){zoomable="yes"}

1. Vá para **Projetos** e selecione o projeto criado no exercício anterior, chamado `--aepUserLdap-- Firefly`.

![Armazenamento do Azure](./images/ps1.png){zoomable="yes"}

1. Selecione **+ Adicionar ao Projeto** e **API**.

![Armazenamento do Azure](./images/ps2.png){zoomable="yes"}

1. Selecione **Creative Cloud** e escolha **Photoshop - Firefly Services**. Selecione **Próximo**.

![Armazenamento do Azure](./images/ps3.png){zoomable="yes"}

1. Selecione **Próximo**.

![Armazenamento do Azure](./images/ps4.png){zoomable="yes"}

Em seguida, é necessário selecionar um perfil de produto que defina quais permissões estão disponíveis para essa integração.

1. Selecione **Configuração Padrão dos Serviços Firefly** e **Configuração Padrão dos Serviços Creative Cloud Automation**.

1. Selecione **Salvar API configurada**.

![Armazenamento do Azure](./images/ps5.png){zoomable="yes"}

Seu projeto do Adobe I/O foi atualizado para funcionar com as APIs de serviços da Photoshop e da Firefly.

![Armazenamento do Azure](./images/ps6.png){zoomable="yes"}

## 1.1.3.2 Interagir programaticamente com um arquivo do PSD

>[!IMPORTANT]
>
>Se você for um funcionário da Adobe, siga as instruções aqui para usar o [PostBuster](./../../../postbuster.md).

1. Baixe o [citisignal-fiber.psd](./../../../assets/ff/citisignal-fiber.psd){target="_blank"} na área de trabalho.

1. Abra **citisignal-fiber.psd** no Photoshop.

![Armazenamento do Azure](./images/ps7.png){zoomable="yes"}

No painel **Camadas**, o designer do arquivo deu um nome exclusivo a cada camada. Você pode ver as informações da camada abrindo o arquivo PSD no Photoshop, mas também pode fazer isso de forma programática.

Vamos enviar sua primeira solicitação de API para APIs do Photoshop.

1. No Postman, antes de enviar solicitações de API para o Photoshop, é necessário autenticar no Adobe I/O. Abra a solicitação anterior com o nome **POST - Obter Token de Acesso**.

1. Vá para **Params** e verifique se o parâmetro **Scope** está definido corretamente. O **Valor** para **Escopo** deve ser semelhante a:

`openid,session,AdobeID,read_organizations,additional_info.projectedProductContext, ff_apis, firefly_api`

1. Selecione **Enviar**.

![Armazenamento do Azure](./images/ps8.png){zoomable="yes"}

Agora você tem um token de acesso válido para interagir com as APIs do Photoshop.

![Armazenamento do Azure](./images/ps9.png){zoomable="yes"}

### API do Photoshop - Hello World

Em seguida, vamos dizer olá para as APIs do Photoshop para testar se todas as permissões e o acesso estão definidos corretamente.

1. Na coleção **Photoshop**, abra a solicitação **Photoshop Hello (Test Auth.)**. Selecione **Enviar**.

![Armazenamento do Azure](./images/ps10.png){zoomable="yes"}

Você deve receber a resposta **Bem-vindo à API do Photoshop!**.

![Armazenamento do Azure](./images/ps11.png){zoomable="yes"}

Em seguida, para interagir programaticamente com o arquivo do PSD **citisignal-fiber.psd**, você precisa carregá-lo na sua conta de armazenamento. Você pode fazer isso manualmente — arrastando e soltando-o no contêiner usando o Azure Storage Explorer — mas dessa vez você deve fazer isso por meio da API.

### Fazer upload do PSD para o Azure

1. No Postman, abra a solicitação **Fazer upload do PSD para a conta de armazenamento do Azure**. No exercício anterior, você configurou essas variáveis de ambiente no Postman, que serão usadas agora:

- `AZURE_STORAGE_URL`
- `AZURE_STORAGE_CONTAINER`
- `AZURE_STORAGE_SAS_READ`
- `AZURE_STORAGE_SAS_WRITE`

Como você pode ver na solicitação **Fazer upload do PSD para a conta de armazenamento do Azure**, a URL está configurada para usar essas variáveis.

![Armazenamento do Azure](./images/ps12.png){zoomable="yes"}

1. Em **Body**, selecione o arquivo **citisignal-fiber.psd**.

![Armazenamento do Azure](./images/ps13.png){zoomable="yes"}

1. Sua tela deve ter esta aparência. Selecione **Enviar**.

![Armazenamento do Azure](./images/ps14.png){zoomable="yes"}

Você deve obter essa resposta vazia do Azure, o que significa que seu arquivo está armazenado no contêiner na sua conta de Armazenamento do Azure.

![Armazenamento do Azure](./images/ps15.png){zoomable="yes"}

Se você usar o Azure Storage Explorer para examinar seu arquivo, atualize sua pasta.

![Armazenamento do Azure](./images/ps16.png){zoomable="yes"}

### API do Photoshop - Obter manifesto

Em seguida, é necessário obter o arquivo de manifesto do arquivo do PSD.

1. No Postman, abra a solicitação **Photoshop - Obter Manifesto do PSD**. Ir para **Corpo**.

O corpo deve ter esta aparência:

```json
{
  "inputs": [
    {
      "storage": "external",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber.psd{{AZURE_STORAGE_SAS_READ}}"
    }
  ],
  "options": {
    "thumbnails": {
      "type": "image/jpeg"
    }
  }
}
```

1. Selecione **Enviar**.

Na resposta, agora você vê um link. Como as operações no Photoshop às vezes podem levar algum tempo para serem concluídas, o Photoshop fornece um arquivo de status como resposta à maioria das solicitações recebidas. Para entender o que está acontecendo com sua solicitação, você precisa ler o arquivo de status.

![Armazenamento do Azure](./images/ps17.png){zoomable="yes"}

1. Para ler o arquivo de status, abra a solicitação **Photoshop - Obter Status PS**. Você pode ver que esta solicitação está usando uma variável como URL, que é uma variável definida pela solicitação anterior enviada, **Photoshop - Obter Manifesto do PSD**. As variáveis estão definidas nos **Scripts** de cada solicitação. Selecione **Enviar**.

![Armazenamento do Azure](./images/ps18.png){zoomable="yes"}

Sua tela deve ter esta aparência. Atualmente, o status está definido como **pendente**, o que significa que o processo ainda não foi concluído.

![Armazenamento do Azure](./images/ps19.png){zoomable="yes"}

1. Selecione para enviar mais algumas vezes no **Photoshop - Obter Status PS**, até que o status seja alterado para **bem-sucedido**. Isso pode levar alguns minutos.

Quando a resposta estiver disponível, você poderá ver que o arquivo json contém informações sobre todas as camadas do arquivo PSD. Essas informações são úteis, pois é possível identificar o nome ou a ID da camada.

![Armazenamento do Azure](./images/ps20.png){zoomable="yes"}

Como exemplo, pesquise pelo texto `2048x2048-cta`. Sua tela deve ter esta aparência:

![Armazenamento do Azure](./images/ps21.png){zoomable="yes"}

### API do Photoshop - Alterar texto

Em seguida, é necessário alterar o texto da chamada para ação usando as APIs.

1. No Postman, abra a solicitação **Photoshop - Alterar Texto** e vá para **Corpo**.

Sua tela deve ter esta aparência:

- primeiro, um arquivo de entrada é especificado: `citisignal-fiber.psd`
- segundo, a camada a ser alterada é especificada, com o texto a ser alterado para
- terceiro, um arquivo de saída foi especificado: `citisignal-fiber-changed-text.psd`

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
        "name": "2048x2048-cta",
        "text": {
          "content": "Get Fiber now!"
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

O arquivo de saída tem um nome diferente, porque você não deseja substituir o arquivo de entrada original.

1. Selecione **Enviar**.

![Armazenamento do Azure](./images/ps23.png){zoomable="yes"}

Assim como antes, a resposta contém um link que aponta para o arquivo de status que acompanha o progresso.

![Armazenamento do Azure](./images/ps22.png){zoomable="yes"}

1. Para ler o arquivo de status, abra a solicitação **Photoshop - Obter Status PS** e selecione **Enviar**. Se o status não estiver definido como **êxito** imediatamente, aguarde alguns segundos e selecione **Enviar** novamente.

1. Selecione o URL para baixar o arquivo de saída.

![Armazenamento do Azure](./images/ps24.png){zoomable="yes"}

1. Abra **citisignal-fiber-changed-text.psd** depois de baixar o arquivo no computador. Você deve ver que o espaço reservado para a chamada à ação foi substituído pelo texto **Obter fibra agora!**.

![Armazenamento do Azure](./images/ps25.png){zoomable="yes"}

Você também pode ver esse arquivo em seu contêiner usando o explorador do Armazenamento do Azure.

![Armazenamento do Azure](./images/ps26.png){zoomable="yes"}

## Próximas etapas

Ir para a [API de Modelos personalizados do Firefly](./ex4.md){target="_blank"}

Retorne para [Visão geral dos Serviços da Adobe Firefly](./firefly-services.md){target="_blank"}

Voltar para [Todos os Módulos](./../../../overview.md){target="_blank"}
