---
title: Offer Decisioning - Teste sua decisão usando o site de demonstração
description: Teste sua decisão usando o site de demonstração
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 3%

---

# 3.3.4 Combinar Adobe Target e Offer Decisioning

## 3.3.4.1 Coletar o link compartilhável do projeto de demonstração

Para carregar o projeto do site de demonstração no Adobe Target, primeiro é necessário coletar um link especial que permitirá à Adobe Target carregar o projeto do site de demonstração.

Para fazer isso, vá para [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Depois de fazer logon com sua Adobe ID, você verá isso. Clique no projeto do site para abri-lo.

![RTCDP](./images/builder1.png)

Agora vocês verão isto. Clique em **Compartilhar**.

![RTCDP](./images/builder2.png)

Clique em **Gerar link** e copie o link para a área de transferência.

![RTCDP](./images/builder3.png)

Vá para [https://bitly.com](https://bitly.com), cole o link copiado e clique em **Encurtar**. Agora você receberá um link encurtado, que tem esta aparência: `https://bit.ly/3JxN7aG`. Você precisará desse link no próximo exercício.

![RTCDP](./images/builder4.png)

## 3.3.4.2 Coletar

Agora vá para a página inicial do Adobe Experience Cloud em [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Clique em **Target**.

![RTCDP](./../../../modules/rtcdp-b2c/module2.3/images/excl.png)

Na página inicial do **Adobe Target**, você verá todas as atividades existentes.

![RTCDP](./../../../modules/rtcdp-b2c/module2.3/images/exclatov.png)

Clique em **+ Criar atividade** para criar uma nova Atividade.

![RTCDP](./../../../modules/rtcdp-b2c/module2.3/images/exclatcr.png)

Selecione **Direcionamento de experiência**.

![RTCDP](./images/exclatcrxt.png)

Agora selecione **Visual** e cole seu link encurtado no campo **Inserir URL da Atividade**. Clique em **Next**.

![RTCDP](./images/exclatcrxt1.png)

Você verá seu projeto de site de demonstração ser carregado no Visual Experience Composer.

![RTCDP](./images/vec1.png)

Vá para o modo **Procurar** e clique em **Permitir tudo** no pop-up de consentimento do cookie.

![RTCDP](./images/vec2.png)

Clique na área que contém o texto **Categorias em destaque**. Clique em **Inserir antes** e selecione **Decisão de Oferta**.

![RTCDP](./images/vec3.png)

Você então verá esse pop-up. Selecione sua sandbox `--aepSandboxName--` e selecione o posicionamento **Web - Image**.

![RTCDP](./images/vec4.png)

Em seguida, selecione sua decisão `--aepUserLdap-- - Luma Decision`. Clique em **Salvar**.

![RTCDP](./images/vec5.png)

Você verá isso. Certifique-se de adicionar uma regra de modelo adicional **URL** **contém** **nome-do-seu-projeto**. Clique em **Salvar**.

![RTCDP](./images/vec6.png)

Você verá isso. Clique em **Next**.

![RTCDP](./images/vec7.png)

Digite um nome para sua oferta, use este nome: `--aepUserLdap-- - XT with Offers (VEC)`. Clique em **Next**.

![RTCDP](./images/vec8.png)

Você verá isso. Defina sua **Métrica de meta** conforme indicado. Clique em **Salvar e fechar**.

![RTCDP](./images/vec9.png)

Sua oferta foi criada e está sendo publicada.

![RTCDP](./images/vec10.png)

Depois que a oferta for publicada, você poderá habilitá-la.

Próxima Etapa: [3.3.5 Use sua decisão em um email e sms](./ex5.md)

[Voltar ao módulo 3.3](./offer-decisioning.md)

[Voltar a todos os módulos](./../../../overview.md)
