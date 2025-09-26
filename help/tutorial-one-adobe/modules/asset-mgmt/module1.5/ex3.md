---
title: Conectar o ACCS ao AEM Assets CS
description: Conectar o ACCS ao AEM Assets CS
kt: 5342
doc-type: tutorial
exl-id: 2b944efe-3997-46a0-9eb0-61dfda67f5b9
source-git-commit: 7280f6b7d3579226f2d8c7f94e75ca8d3f2941cc
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 1.5.3 Conectar o ACCS ao AEM Assets CS

>[!IMPORTANT]
>
>Para concluir este exercício, você precisa ter acesso a um AEM Sites e Assets CS com ambiente EDS em funcionamento.
>
>Se você ainda não tiver esse ambiente, vá para o exercício [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Siga as instruções aqui e você terá acesso a esse ambiente.

>[!IMPORTANT]
>
>Se você configurou anteriormente um programa do AEM CS com um ambiente do AEM Sites e do Assets CS, pode ser que sua sandbox do AEM CS tenha hibernado. Considerando que a deshibernação de uma sandbox desse tipo leva de 10 a 15 minutos, seria uma boa ideia iniciar o processo de deshibernação agora para que você não precise aguardar mais tarde.

Após concluir o exercício anterior, você pode ver um produto sendo retornado pelo ACCS para o seu site, mas ele ainda não tinha uma imagem. No final deste exercício, você também deverá ver uma imagem sendo retornada.

![ACCS+AEM Sites](./images/accsaemsites11.png)

## 1.5.3.1 Atualizar Configuração De Pipeline

Ir para [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. A organização que você deve selecionar é `--aepImsOrgName--`.

Clique para abrir seu Programa Cloud Manager, que deve ser chamado de `--aepUserLdap-- - CitiSignal AEM+ACCS`.

![ACCS+AEM Assets](./images/accsaemassets1.png)

Role para baixo e clique em **Acessar informações do repositório** na guia **Pipelines**.

![ACCS+AEM Assets](./images/accsaemassets2.png)

Você deverá ver isso. Clique em **Gerar senha**.

![ACCS+AEM Assets](./images/accsaemassets3.png)

Clique novamente em **Gerar senha**.

![ACCS+AEM Assets](./images/accsaemassets4.png)

Você deverá ter uma senha disponível. Em seguida, clique no ícone **copiar** ao lado do campo **linha de comando Git**.

![ACCS+AEM Assets](./images/accsaemassets5.png)

Crie um novo diretório em um local de escolha no seu computador e nomeie-o como **GitHub do AEM Pipeline**.

![ACCS+AEM Assets](./images/accsaemassets6.png)

Clique com o botão direito do mouse na pasta e selecione **Novo Terminal na Pasta**.

![ACCS+AEM Assets](./images/accsaemassets7.png)

Você deverá ver isso.

![ACCS+AEM Assets](./images/accsaemassets8.png)

Cole a **linha de comando do Git** que você copiou anteriormente na janela Terminal.

![ACCS+AEM Assets](./images/accsaemassets9.png)

É necessário inserir um nome de usuário. Copie o nome de usuário do Pipeline de programa do Cloud Manager **Acesse as informações do repositório** e clique em **inserir**.

![ACCS+AEM Assets](./images/accsaemassets10.png)

Em seguida, você precisa digitar a senha. Copie a senha do Pipeline de programa do Cloud Manager **Acesse as informações do repositório** e clique em **inserir**.

![ACCS+AEM Assets](./images/accsaemassets11.png)

Isso pode levar um minuto. Depois de concluído, você terá uma cópia local do repositório Git vinculada ao pipeline do programa.

![ACCS+AEM Assets](./images/accsaemassets12.png)

Você verá um novo diretório no **GitHub do AEM Pipeline**. Abra esse diretório.

![ACCS+AEM Assets](./images/accsaemassets13.png)

Selecione todos os arquivos nesse diretório e exclua todos eles.

![ACCS+AEM Assets](./images/accsaemassets14.png)

Verifique se o diretório está vazio.

![ACCS+AEM Assets](./images/accsaemassets15.png)

Ir para [https://github.com/ankumalh/assets-commerce](https://github.com/ankumalh/assets-commerce). Clique em **&lt;> Código** e selecione **Baixar ZIP**. Baixe o arquivo e solte-o na área de trabalho.

![ACCS+AEM Assets](./images/accsaemassets15a.png)

Em seguida, copie o arquivo **assets-commerce-main.zip** na área de trabalho e descompacte-o. Abra a pasta **assets-commerce-main**.

![ACCS+AEM Assets](./images/accsaemassets16.png)

Copie todos os arquivos do diretório **assets-commerce-main** para o diretório vazio do diretório do Repositório de Pipelines do Programa.

![ACCS+AEM Assets](./images/accsaemassets17.png)

Em seguida, abra o **Microsoft Visual Studio Code** e abra a pasta que contém o Repositório de Pipelines do seu Programa no **Microsoft Visual Studio Code**.

![ACCS+AEM Assets](./images/accsaemassets18.png)

Vá para **Pesquisar** no menu esquerdo e procure por `<my-app>`. Você precisa substituir todas as ocorrências de `<my-app>` por `--aepUserLdap--citisignalaemaccs`.

Clique no ícone **substituir tudo**.

![ACCS+AEM Assets](./images/accsaemassets19.png)

Clique em **Substituir**.

![ACCS+AEM Assets](./images/accsaemassets20.png)

Os novos arquivos agora estão prontos para serem carregados de volta no repositório Git, que está vinculado ao Repositório de pipelines do programa. Para fazer isso, abra a pasta **AEM Pipeline GitHub** e clique com o botão direito do mouse na pasta que contém os novos arquivos. Selecione **Novo Terminal na Pasta**.

![ACCS+AEM Assets](./images/accsaemassets21.png)

Você deverá ver isso. Cole o comando `git add .` e pressione **enter**.

![ACCS+AEM Assets](./images/accsaemassets22.png)

Você deverá ver isso. Cole o comando `git commit -m "add assets integration"` e pressione **enter**.

![ACCS+AEM Assets](./images/accsaemassets23.png)

Você deverá ver isso. Cole o comando `git push origin main` e pressione **enter**.

![ACCS+AEM Assets](./images/accsaemassets24.png)

Você deverá ver isso. Suas alterações foram implantadas no repositório Git do pipeline do programa.

![ACCS+AEM Assets](./images/accsaemassets25.png)

Volte para o Cloud Manager e clique em **Fechar**.

![ACCS+AEM Assets](./images/accsaemassets26.png)

Depois de fazer alterações no repositório Git do Pipeline, é necessário executar o pipeline **Implantar no Desenvolvimento** novamente. Clique nos 3 pontos **...** e selecione **Executar**.

![ACCS+AEM Assets](./images/accsaemassets27.png)

Clique em **Executar**. A execução de uma implantação de pipeline pode levar de 10 a 15 minutos. Antes de continuar, aguarde até que a implantação do pipeline seja concluída com êxito.

![ACCS+AEM Assets](./images/accsaemassets28.png)

## 1.5.3.2 Habilitar a integração do AEM Assets no ACCS

Volte para a instância do ACCS. No menu esquerdo, vá para **Lojas** e selecione **Configuração**.

![ACCS+AEM Assets](./images/accsaemassets49.png)

Role para baixo no menu até **ADOBE SERVICES** e abra a **Integração com o AEM Assets**. Você deverá ver isso.

![ACCS+AEM Assets](./images/accsaemassets50.png)

Preencha as seguintes variáveis:

- **ID do Programa AEM Assets**: você pode obter a ID do Programa da URL do Autor do AEM CS. Neste exemplo, a ID do programa é `166717`.

![ACCS+AEM Assets](./images/accsaemassets50a.png)

- **ID de Ambiente do AEM Assets**: você pode obter a ID de Ambiente da URL do Autor do AEM CS. Neste exemplo, a ID de Ambiente é `1786231`.

![ACCS+AEM Assets](./images/accsaemassets50b.png)

- **ID do Cliente IMS do Seletor de Ativos**: definido como `1`
- **Sincronização habilitada**: definida como `Yes`
- **Proprietário da visualização**: definido como `AEM Assets`
- **Regra de correspondência de ativos**: `Match by product SKU`
- **Corresponder por nome de atributo SKU de produto**: `commerce:skus`

Clique em **Salvar configuração**.

![ACCS+AEM Assets](./images/accsaemassets51.png)

Você deverá ver isso.

![ACCS+AEM Assets](./images/accsaemassets52.png)

## 1.5.3.3 Atualizar config.json

Acesse o repositório GitHub criado ao configurar o ambiente do AEM Sites CS/EDS. Esse repositório foi criado no exercício [1.1.2 Configure seu ambiente do AEM CS](./../../../modules/asset-mgmt/module2.1/ex3.md){target="_blank"} e deve ser nomeado como **citisignal-aem-accs**.

No diretório raiz, role para baixo e clique para abrir o arquivo **config.json**. Clique no ícone **editar** para fazer alterações no arquivo.

![ACCS+AEM Assets](./images/accsaemassets101.png)

Adicione o trecho de código abaixo na linha 5 `"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/XXX/graphql",`:

```json
 "commerce-assets-enabled": "true",
```

Clique em **Confirmar alterações...**.

![ACCS+AEM Assets](./images/accsaemassets102.png)

Clique em **Confirmar alterações**.

![ACCS+AEM Assets](./images/accsaemassets103.png)

Sua alteração foi salva e será publicada em breve. Pode levar alguns minutos para que a alteração fique visível na loja.

![ACCS+AEM Assets](./images/accsaemassets104.png)

## 1.5.3.4 Verificar campos do Commerce no AEM Assets CS

Faça logon no ambiente de Autor do AEM CS e vá para **Assets**.

![ACCS+AEM Assets](./images/accsaemassets30.png)

Vá para **Arquivos**.

![ACCS+AEM Assets](./images/accsaemassets31.png)

Abra a pasta **CitiSignal**.

![ACCS+AEM Assets](./images/accsaemassets32.png)

Passe o mouse sobre qualquer ativo e clique no ícone **info**.

![ACCS+AEM Assets](./images/accsaemassets33.png)

Agora você deve ver uma guia **Commerce** que contém dois novos atributos de metadados.

![ACCS+AEM Assets](./images/accsaemassets34.png)

Seu ambiente do AEM Assets CS agora oferece suporte à integração com o Commerce. Agora você pode começar a carregar imagens de produtos.

## 1.5.3.4 Carregar Assets do produto e vincular aos produtos

[Baixe as imagens do produto aqui](./images/Product_Images.zip). Após o download, exporte os arquivos para sua área de trabalho.

![ACCS+AEM Assets](./images/accsaemassets35.png)

Clique em **Criar** e selecione **Pasta**.

![ACCS+AEM Assets](./images/accsaemassets36.png)

Insira o valor **Product_Images** para os campos **Title** e **Name**. Clique em **Criar**.

![ACCS+AEM Assets](./images/accsaemassets37.png)

Clique em para abrir a pasta que acabou de criar.

![ACCS+AEM Assets](./images/accsaemassets38.png)

Clique em **Criar** e selecione **Arquivos**.

![ACCS+AEM Assets](./images/accsaemassets39.png)

Navegue até a pasta **Product_Images** na área de trabalho, selecione todos os arquivos e clique em **Abrir**.

![ACCS+AEM Assets](./images/accsaemassets40.png)

Clique em **Carregar**.

![ACCS+AEM Assets](./images/accsaemassets41.png)

As imagens serão disponibilizadas na pasta. Passe o mouse sobre o produto **iPhone-Air-Light-Gold.png** e clique no ícone **Propriedades**.

![ACCS+AEM Assets](./images/accsaemassets42.png)

Role para baixo e defina o campo **Status da revisão** como **Aprovado**. A integração AEM Assets CS - ACCS funciona somente para imagens aprovadas.

![ACCS+AEM Assets](./images/accsaemassets44.png)

Role para cima, vá para a guia **Commerce** e clique em **Adicionar** em **SKUs do produto**.

![ACCS+AEM Assets](./images/accsaemassets45.png)

Adicione os seguintes SKUs para este produto:

| Chave | Valor | Uso |
|:-------------:| :---------------:| :---------------:| 
| `iPhone-Air-Light-Gold` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Light-Gold-256GB` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Light-Gold-512GB` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Light-Gold-1TB` | `1` | `thumbnail, image, swatch_image, small_image` |

Você deveria ficar com isso. Clique em **Salvar e fechar**.

![ACCS+AEM Assets](./images/accsaemassets46.png)

Passe o mouse sobre o produto **iPhone-Air-Space-Black.png** e clique no ícone **Propriedades**.

![ACCS+AEM Assets](./images/accsaemassets47.png)

Role para baixo e defina o campo **Status da revisão** como **Aprovado**. A integração AEM Assets CS - ACCS funciona somente para imagens aprovadas.

![ACCS+AEM Assets](./images/accsaemassets48.png)

Role para cima, vá para a guia **Commerce** e clique em **Adicionar** em **SKUs do produto**.

![ACCS+AEM Assets](./images/accsaemassets201.png)

Adicione os seguintes SKUs para este produto:

| Chave | Valor | Uso |
|:-------------:| :---------------:| :---------------:| 
| `iPhone-Air-Space-Black` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Space-Black-256GB` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Space-Black-512GB` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Space-Black-1TB` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air` | `1` | `thumbnail, image, swatch_image, small_image` |

Você deveria ficar com isso. Clique em **Salvar e fechar**.

![ACCS+AEM Assets](./images/accsaemassets202.png)

Passe o mouse sobre o produto **iPhone-Air-Sky-Blue.png** e clique no ícone **Propriedades**.

![ACCS+AEM Assets](./images/accsaemassets203.png)

Role para baixo e defina o campo **Status da revisão** como **Aprovado**. A integração AEM Assets CS - ACCS funciona somente para imagens aprovadas.

![ACCS+AEM Assets](./images/accsaemassets204.png)

Role para cima, vá para a guia **Commerce** e clique em **Adicionar** em **SKUs do produto**.

![ACCS+AEM Assets](./images/accsaemassets205.png)

Adicione os seguintes SKUs para este produto:

| Chave | Valor | Uso |
|:-------------:| :---------------:| :---------------:| 
| `iPhone-Air-Sky-Blue` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Sky-Blue-256GB` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Sky-Blue-512GB` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Sky-Blue-1TB` | `1` | `thumbnail, image, swatch_image, small_image` |

Você deveria ficar com isso. Clique em **Salvar e fechar**.

![ACCS+AEM Assets](./images/accsaemassets206.png)

Passe o mouse sobre o produto **iPhone-Air-Cloud-White.png** e clique no ícone **Propriedades**.

![ACCS+AEM Assets](./images/accsaemassets207.png)

Role para baixo e defina o campo **Status da revisão** como **Aprovado**. A integração AEM Assets CS - ACCS funciona somente para imagens aprovadas.

![ACCS+AEM Assets](./images/accsaemassets208.png)

Role para cima, vá para a guia **Commerce** e clique em **Adicionar** em **SKUs do produto**.

![ACCS+AEM Assets](./images/accsaemassets209.png)

Adicione os seguintes SKUs para este produto:

| Chave | Valor | Uso |
|:-------------:| :---------------:| :---------------:| 
| `iPhone-Air-Cloud-White` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Cloud-White-256GB` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Cloud-White-512GB` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Cloud-White-1TB` | `1` | `thumbnail, image, swatch_image, small_image` |

Você deveria ficar com isso. Clique em **Salvar e fechar**.

![ACCS+AEM Assets](./images/accsaemassets210.png)

Cada imagem do **iPhone Air** agora deve ter **miniaturas verdes**, indicando que o ativo foi aprovado.

![ACCS+AEM Assets](./images/accsaemassets250.png)

## 1.5.3.5 Verificar imagens do produto na vitrine do AEM Sites CS/EDS

>[!NOTE]
>
>Pode levar até 15 minutos para que as alterações feitas acima sejam implantadas com êxito. Se você ainda não vir sua imagem sendo exibida, aguarde 15 minutos e tente novamente.

Para verificar se a integração está funcionando, é necessário abrir o site do CitiSignal.

Para acessar seu site, vá para `main--citisignal-aem-accs--XXX.aem.page` e/ou `main--citisignal-aem-accs--XXX.aem.live`, depois de substituir XXX pela sua conta de usuário do GitHub, que neste exemplo é `woutervangeluwe`.

Neste exemplo, o URL completo torna-se isto:
`https://main--citisignal-aem-accs--woutervangeluwe.aem.page` e/ou `https://main--citisignal-aem-accs--woutervangeluwe.aem.live`.

Você deverá ver isso. Vá para **Telefones**.

![ACCS+AEM Assets](./images/accsaemassets150.png)

Você deverá ver uma imagem do produto sendo mostrada para o **iPhone Air**. Clique em **iPhone Air**.

![ACCS+AEM Assets](./images/accsaemassets151.png)

Você deverá ver isso. Altere as opções de cor e armazenamento e você verá as imagens alteradas dinamicamente com base nas escolhas feitas.

![ACCS+AEM Assets](./images/accsaemassets152.png)

Este é um exemplo de alteração da cor para **Light-Gold** e do tamanho do armazenamento para **256GB**.

![ACCS+AEM Assets](./images/accsaemassets153.png)

Próxima etapa: [Resumo e benefícios](./summary.md){target="_blank"}

Voltar para o [Adobe Commerce as a Cloud Service](./accs.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
