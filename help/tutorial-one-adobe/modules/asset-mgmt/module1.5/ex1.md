---
title: Introdução ao Adobe Commerce as a Cloud Service
description: Introdução ao Adobe Commerce as a Cloud Service
kt: 5342
doc-type: tutorial
exl-id: 8603c8e2-c3ba-4976-9703-cef9e63924b8
source-git-commit: 7280f6b7d3579226f2d8c7f94e75ca8d3f2941cc
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 1.5.1 Introdução ao Adobe Commerce as a Cloud Service

Ir para [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Verifique se você está no ambiente correto, que deve ser nomeado como `--aepImsOrgName--`. Clique em **Commerce**.

![AEM Assets](./images/accs1.png)

## 1.5.1.1 Crie sua instância ACCS

Você deverá ver isso. Clique em **+ Adicionar instância**.

![AEM Assets](./images/accs2.png)

Preencha os campos desta forma:

- **Nome da instância**: `--aepUserLdap-- - ACCS`
- **Ambiente**: `Sandbox`
- **Região**: `North America`

Clique em **Adicionar instância**.

![AEM Assets](./images/accs3.png)

Sua instância está sendo criada. Isso pode levar de 5 a 10 minutos.

![AEM Assets](./images/accs4.png)

Quando a instância estiver pronta, clique na instância para abri-la.

![AEM Assets](./images/accs5.png)

## 1.5.1.2 Configurar o armazenamento do CitiSignal

Você deverá ver isso. Clique em **Entrar com o Adobe ID** e faça logon.

![AEM Assets](./images/accs6.png)

Depois de fazer logon, você deverá ver esta página inicial. O primeiro passo é configurar a loja do CitiSignal no Commerce. Clique em **Lojas**.

![AEM Assets](./images/accs7.png)

Clique em **Todas as lojas**.

![AEM Assets](./images/accs8.png)

Clique em **Criar Site**.

![AEM Assets](./images/accs9.png)

Preencha os campos desta forma:

- **Nome**: `CitiSignal`
- **Código**: `citisignal`

Clique em **Salvar Site**.

![AEM Assets](./images/accs10.png)

Você deveria voltar aqui. Clique em **Criar armazenamento**.

![AEM Assets](./images/accs11.png)

Preencha os campos desta forma:

- **Site**: `CitiSignal`
- **Nome**: `CitiSignal`
- **Código**: `citisignal`
- **Categoria raiz**: `Default Category`

Clique em **Salvar armazenamento**.

![AEM Assets](./images/accs12.png)

Você deveria voltar aqui. Clique em **Criar Exibição de Loja**.

![AEM Assets](./images/accs13.png)

Preencha os campos desta forma:

- **Armazenamento**: `CitiSignal`
- **Nome**: `CitiSignal`
- **Código**: `citisignal`
- **Status**: `Enabled`

Clique em **Salvar Exibição da Loja**.

![AEM Assets](./images/accs14.png)

Você deverá ver essa mensagem. Clique em **OK**.

![AEM Assets](./images/accs15.png)

Você deveria voltar aqui. Clique no site **CitiSignal** para abri-lo.

![AEM Assets](./images/accs16.png)

Marque a caixa de seleção para definir este site como o site padrão.

Clique em **Salvar Site**.

![AEM Assets](./images/accs16a.png)

Você deveria voltar aqui.

![AEM Assets](./images/accs16.png)

## 1.5.1.3 Configurar Categorias e Produtos

Vá para **Catálogo** e selecione **Categorias**.

![AEM Assets](./images/accs17.png)

Selecione **Categoria Padrão** e clique em **Adicionar Subcategoria**.

![AEM Assets](./images/accs18.png)

Insira o nome `Phones` e clique em **Salvar**.

![AEM Assets](./images/accs19.png)

Selecione **Categoria padrão** e clique novamente em **Adicionar subcategoria**.

![AEM Assets](./images/accs20.png)

Insira o nome `Watches` e clique em **Salvar**.

![AEM Assets](./images/accs21.png)

Em seguida, você deve criar duas categorias.

![AEM Assets](./images/accs22.png)

Em seguida, vá para **Catálogo** e selecione **Produtos**.

![AEM Assets](./images/accs23.png)

Você deverá ver isso. Clique em **Adicionar produto**.

![AEM Assets](./images/accs24.png)

Configure seu produto da seguinte maneira:

- **Nome do Produto**: `iPhone Air`
- **SKU**: `iPhone-Air`
- **Preço**: `999`
- **Quantidade**: `10000`
- **Categorias**: selecione `Phones`

Clique em **Salvar**.

![AEM Assets](./images/accs25.png)

Role para baixo até **Configurações** e clique em **Criar configurações**.

![AEM Assets](./images/accs26.png)

Você deverá ver isso. Clique em **Criar Novo Atributo**.

![AEM Assets](./images/accs27.png)

Defina o **Rótulo Padrão** como `Storage` e clique em **Adicionar Opção** em **Gerenciar Opções**.

![AEM Assets](./images/accs28.png)

Configure a primeira opção usando o nome `256GB` em todas as três colunas e clique novamente em **Adicionar Opção**.

![AEM Assets](./images/accs29.png)

Configure a segunda opção usando o nome `512GB` em todas as três colunas e clique novamente em **Adicionar Opção**.

![AEM Assets](./images/accs30.png)

Configure a terceira opção usando o nome `1TB` em todas as 3 colunas.

![AEM Assets](./images/accs31.png)

Role para baixo até **Propriedades da vitrine**. Defina as seguintes opções como **Sim**:

- **Usar na Pesquisa**
- **Permitir Marcas do HTML na Loja**
- **Visível nas Páginas do Catálogo na Loja**
- **Uso na Listagem de Produtos**

![AEM Assets](./images/accs32.png)

Role para cima e clique em **Salvar Atributo**.

![AEM Assets](./images/accs33.png)

Você deverá ver isso. Selecione ambos os atributos para **cor** e **armazenamento** e clique em **Avançar**.

![AEM Assets](./images/accs34.png)

Você deverá ver isso. Agora é necessário adicionar as opções de cor disponíveis. Para fazer isso, clique em **Criar novo valor**.

![AEM Assets](./images/accs35.png)

Insira o valor `Sky-Blue` e clique em **Criar novo valor**.

![AEM Assets](./images/accs36.png)

Insira o valor `Light-Gold` e clique em **Criar novo valor**.

![AEM Assets](./images/accs37.png)

Insira o valor `Cloud-White` e clique em **Criar novo valor**.

![AEM Assets](./images/accs38.png)

Insira o valor `Space-Black`. Clique em **Selecionar tudo**

![AEM Assets](./images/accs39.png)

Selecione todas as 3 opções em **Armazenamento** e clique em **Avançar**.

![AEM Assets](./images/accs40.png)

Mantenha as configurações padrão e clique em **Avançar**.

![AEM Assets](./images/accs41.png)

Você deverá ver isso. Clique em **Gerar Produtos**.

![AEM Assets](./images/accs42.png)

Defina a **Quantidade** de cada produto para `10000`. Clique em **Salvar**.

![AEM Assets](./images/accs43.png)

Role para baixo até **Produto em Sites** e marque a caixa de seleção **CitiSignal**.

Clique em **Salvar**.

![AEM Assets](./images/accs44.png)

Clique em **Confirmar**.

![AEM Assets](./images/accs45.png)

Você deverá ver isso. Clique em **Voltar**.

![AEM Assets](./images/accs46.png)

Agora você verá o produto **iPhone Air** e suas variações no Catálogo de Produtos.

![AEM Assets](./images/accs47.png)

Próxima etapa: [Conectar o ACCS à Loja AEM Sites CS/EDS](./ex2.md){target="_blank"}

Voltar para o [Adobe Commerce as a Cloud Service](./accs.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
