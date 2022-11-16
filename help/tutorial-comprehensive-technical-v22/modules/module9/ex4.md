---
title: Offer Decisioning - Teste sua decisão usando o site de demonstração
description: Teste sua decisão usando o site de demonstração
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: cdb2ba7d-bfc3-43ce-b9a1-1f0866322589
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 4%

---

# 9.4 Combinar Adobe Target e Offer Decisioning

## 9.4.1 Colete o link compartilhável do seu projeto de demonstração

Para carregar o projeto do site de demonstração no Adobe Target, primeiro é necessário coletar um link especial que permitirá que o Adobe Target carregue o projeto do site de demonstração.

Para fazer isso, acesse [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Depois de fazer logon com sua Adobe ID, você verá isso. Clique no projeto do seu site para abri-lo.

![RTCDP](./images/builder1.png)

Você verá isso agora. Clique em **Compartilhar**.

![RTCDP](./images/builder2.png)

Clique em **Gerar link** e, em seguida, copie o link para a área de transferência.

![RTCDP](./images/builder3.png)

Ir para [https://bitly.com](https://bitly.com), cole o link copiado e clique em **Encurtar**. Agora você terá um link encurtado, que se parece com o seguinte: `https://bit.ly/3JxN7aG`. Você precisará desse link no próximo exercício.

![RTCDP](./images/builder4.png)

## 9.4.2 Coleta

Agora vá para a página inicial do Adobe Experience Cloud acessando [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Clique em **Target**.

![RTCDP](../module6/images/excl.png)

No **Adobe Target** página inicial, você verá todas as atividades existentes.

![RTCDP](../module6/images/exclatov.png)

Clique em **+ Criar atividade** para criar uma nova Atividade.

![RTCDP](../module6/images/exclatcr.png)

Selecionar **Direcionamento de experiência**.

![RTCDP](./images/exclatcrxt.png)

Em seguida, selecione **Visual** e cole o link encurtado no campo **Inserir URL da atividade**. Clique em **Próximo**.

![RTCDP](./images/exclatcrxt1.png)

Em seguida, você verá seu projeto de demonstração do site sendo carregado no Visual Experience Composer.

![RTCDP](./images/vec1.png)

Ir para **Procurar** modo para clicar **Permitir tudo** no pop-up de consentimento do cookie.

![RTCDP](./images/vec2.png)

Clique na área que contém o texto **Categorias em destaque**. Clique em **Inserir antes** e depois selecione **Decisão da oferta**.

![RTCDP](./images/vec3.png)

Você verá esse pop-up. Selecionar a sandbox `--aepSandboxId--` e, em seguida, selecione a disposição **Web - Imagem**.

![RTCDP](./images/vec4.png)

Em seguida, selecione sua decisão `--demoProfileLdap-- - Luma Decision`. Clique em **Salvar**.

![RTCDP](./images/vec5.png)

Você verá isso. Certifique-se de adicionar uma regra de modelo adicional **URL** **contém** **nome do projeto**. CLick **Salvar**.

![RTCDP](./images/vec6.png)

Você verá isso. Clique em **Próximo**.

![RTCDP](./images/vec7.png)

Insira um nome para a oferta, use este nome: `--demoProfileLdap-- - XT with Offers (VEC)`. Clique em **Próximo**.

![RTCDP](./images/vec8.png)

Você verá isso. Defina as **Métrica de objetivo** conforme indicado. Clique em **Salvar e fechar**.

![RTCDP](./images/vec9.png)

Sua oferta foi criada e está sendo publicada.

![RTCDP](./images/vec10.png)

Depois que a oferta for publicada, você poderá ativá-la.

Próxima etapa: [9.5 Use sua decisão em um email e sms](./ex5.md)

[Voltar ao Módulo 9](./offer-decisioning.md)

[Voltar para todos os módulos](./../../overview.md)
