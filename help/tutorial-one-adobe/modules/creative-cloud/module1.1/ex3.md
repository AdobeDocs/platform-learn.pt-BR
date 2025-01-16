---
title: Trabalho com APIs do Photoshop
description: Trabalho com APIs do Photoshop
kt: 5342
doc-type: tutorial
exl-id: 60eecc24-1713-4fec-9ffa-a3186db1a8ca
source-git-commit: a4933bd49988cd16c4382ad4327d01ae58b52bbb
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 0%

---

# 1.1.3 Trabalho com APIs do Photoshop

## 1.1.3.1 Atualize a integração do Adobe I/O

Ir para [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home).

![Adobe I/O Nova integração](./images/iohome.png)

Vá para **Projetos** e clique para abrir o projeto que você criou no exercício anterior, que se chama `--aepUserLdap-- Firefly`.

![Armazenamento do Azure](./images/ps1.png)

Clique em **+ Adicionar ao Projeto** e em **API**.

![Armazenamento do Azure](./images/ps2.png)

Selecione **Creative Cloud** e clique em **Photoshop - Firefly Services**. Clique em **Next**.

![Armazenamento do Azure](./images/ps3.png)

Clique em **Next**.

![Armazenamento do Azure](./images/ps4.png)

Em seguida, é necessário selecionar um perfil de produto que definirá quais permissões estão disponíveis para essa integração.

Selecione o perfil **Configuração padrão dos serviços de Firefly** e **Configuração padrão dos serviços de automação de Creative Cloud**.

Clique em **Salvar API configurada**.

![Armazenamento do Azure](./images/ps5.png)

Seu projeto Adobe I/O foi atualizado para funcionar com as APIs de serviços Photoshop e Firefly.

![Armazenamento do Azure](./images/ps6.png)

## 1.1.3.2 Interagir programaticamente com um arquivo PSD

Baixe o arquivo Vá para [citisignal-fiber.psd](./../../../assets/ff/citisignal-fiber.psd) na área de trabalho.

Abra o arquivo **citisignal-fiber.psd** no Photoshop. Você deveria ficar com isso.

![Armazenamento do Azure](./images/ps7.png)

No painel **Camadas**, você verá que o designer do arquivo deu um nome exclusivo a cada camada. Você pode ver as informações da camada abrindo o arquivo PSD no Photoshop, mas também pode fazer isso de forma programática.

Vamos enviar sua primeira solicitação de API para APIs do Photoshop.

Vá para o Postman. Antes de enviar solicitações de API para o Photoshop, é necessário autenticar no Adobe I/O. Abra a solicitação anterior com o nome **POST - Obter Token de Acesso**.

Vá para **Params** e verifique se o parâmetro **Scope** está definido corretamente. O **Valor** para **Escopo** deve ser semelhante a:

`openid,session,AdobeID,read_organizations,additional_info.projectedProductContext, ff_apis, firefly_api`

Em seguida, clique em **Enviar**.

![Armazenamento do Azure](./images/ps8.png)

Em seguida, você tem um token de acesso válido para interagir com as APIs do Photoshop.

![Armazenamento do Azure](./images/ps9.png)

### 1.1.3.2.1 API do Photoshop - Hello World

Em seguida, vamos dizer olá para as APIs do Photoshop para testar se todas as permissões e o acesso estão definidos corretamente. Na coleção **Photoshop**, abra a solicitação com o nome **Photoshop Hello (Test Auth.)**. Clique em **Enviar**.

![Armazenamento do Azure](./images/ps10.png)

Você deve receber esta resposta: **Bem-vindo à API do Photoshop!**.

![Armazenamento do Azure](./images/ps11.png)

Em seguida, para interagir programaticamente com o arquivo PSD **citisignal-fiber.psd**, você precisa carregá-lo na sua conta de armazenamento. Você pode fazer isso manualmente, arrastando e soltando-o no contêiner usando o explorador do Armazenamento do Azure, mas dessa vez, você deve fazer isso por meio da API.

### 1.1.3.2.2 Fazer upload do PSD para o Azure

No Postman, abra a solicitação **Fazer upload do PSD para a conta de armazenamento do Azure**. No exercício anterior, você configurou essas variáveis de ambiente no Postman, que agora será usado:

- `AZURE_STORAGE_URL`
- `AZURE_STORAGE_CONTAINER`
- `AZURE_STORAGE_SAS_READ`
- `AZURE_STORAGE_SAS_WRITE`

Como você pode ver na solicitação **Carregar PSD para a Conta de Armazenamento do Azure**, a URL está configurada para usar essas variáveis.

![Armazenamento do Azure](./images/ps12.png)

Em **Body**, você deve adicionar e selecionar o arquivo **citisignal-fiber.psd**.

![Armazenamento do Azure](./images/ps13.png)

Você deveria ficar com isso. Clique em **Enviar**.

![Armazenamento do Azure](./images/ps14.png)

Você deve receber essa resposta vazia do Azure, o que significa que seu arquivo está armazenado no contêiner na sua conta de Armazenamento do Azure.

![Armazenamento do Azure](./images/ps15.png)

Se você usa o Azure Storage Explorer para dar uma olhada, você verá seu arquivo depois de atualizar sua pasta.

![Armazenamento do Azure](./images/ps16.png)

### 1.1.3.2.3 API do Photoshop - Obter manifesto

Em seguida, é necessário obter o arquivo de manifesto do arquivo PSD. No Postman, abra a solicitação **Photoshop - Obter Manifesto de PSD**. Ir para **Corpo**.

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

Clique em **Enviar**.

Na resposta, agora você vê um link. Como as operações no Photoshop às vezes podem levar algum tempo para serem concluídas, a Photoshop fornecerá um arquivo de status como resposta à maioria das solicitações recebidas. Para entender o que está acontecendo com sua solicitação, você precisa ler o arquivo de status.

![Armazenamento do Azure](./images/ps17.png)

Para ler o arquivo de status, abra a solicitação **Photoshop - Obter Status PS**. Você verá que esta solicitação está usando uma variável como URL, que é uma variável definida pela solicitação anterior enviada, **Photoshop - Obter Manifesto de PSD**. As variáveis estão definidas nos **Scripts** de cada solicitação.

Clique em **Enviar**.

![Armazenamento do Azure](./images/ps18.png)

Você deverá ver isso. Atualmente, o status está definido como **pendente**, o que significa que o processo ainda não foi concluído.

![Armazenamento do Azure](./images/ps19.png)

Você pode clicar mais algumas vezes na solicitação **Photoshop - Obter Status PS**, até que o status seja alterado para **bem-sucedido**. Isso pode levar alguns minutos.

Quando a resposta estiver disponível, você usará um arquivo json que contém informações sobre todas as camadas do arquivo PSD. Essas informações são úteis, pois coisas como o nome da camada ou a ID da camada podem ser vistas aqui.

![Armazenamento do Azure](./images/ps20.png)

Como exemplo, pesquise pelo texto `2048x2048-cta`. Você deverá ver isso.

![Armazenamento do Azure](./images/ps21.png)

### 1.1.3.2.4 API do Photoshop - Alterar texto

Em seguida, agora é necessário alterar o texto da chamada para ação usando as APIs. No Postman, abra a solicitação **Photoshop - Alterar Texto** e vá para **Corpo**.

Você deverá ver isso. Você pode ver que:

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

O arquivo de saída tem um nome diferente, pois você não deseja substituir o arquivo de entrada original.

Clique em **Enviar**.

![Armazenamento do Azure](./images/ps23.png)

Assim como antes, a resposta contém um link que aponta para o arquivo de status que acompanha o progresso.

![Armazenamento do Azure](./images/ps22.png)

Para ler o arquivo de status, abra a solicitação **Photoshop - Obter Status PS** novamente e clique em **Enviar**. Se o status não estiver definido como **êxito** imediatamente, aguarde alguns segundos e clique em **Enviar** novamente.

Quando o status estiver definido como **êxito**, você deverá ver isso. No caminho `outputs[0]._links.renditions[0].href`, você deve ver a URL do arquivo de saída que foi criado pelo Photoshop e que contém o texto alterado.

Clique no URL para baixar o arquivo de saída.

![Armazenamento do Azure](./images/ps24.png)

O arquivo **citisignal-fiber-changed-text.psd** será baixado no computador e depois poderá ser aberto. Você deverá ver que o espaço reservado para a chamada à ação foi substituído pelo texto **Obter fibra agora!**.

![Armazenamento do Azure](./images/ps25.png)

Por fim, você também verá esse arquivo em seu contêiner usando o explorador do Armazenamento do Azure.

![Armazenamento do Azure](./images/ps26.png)

Você concluiu este exercício agora.

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao módulo 1.1](./firefly-services.md)

[Voltar a todos os módulos](./../../../overview.md)
