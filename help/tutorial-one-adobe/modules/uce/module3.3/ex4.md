---
title: Offer Decisioning - Teste sua decisão usando o site de demonstração
description: Teste sua decisão usando o site de demonstração
kt: 5342
doc-type: tutorial
source-git-commit: 926f0f1f6d6b557fd7e59a89aaa3e09d831c82a6
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 2%

---

# 3.3.4 Combinar Adobe Target e Offer Decisioning

## 3.3.4.1 Coletar o link compartilhável do projeto de demonstração

Para carregar o projeto do site de demonstração no Adobe Target, primeiro é necessário coletar um link especial que permitirá à Adobe Target carregar o projeto do site de demonstração.

Para fazer isso, vá para [https://dsn.adobe.com/projects](https://builder.adobedemo.com/projects). Depois de fazer logon com sua Adobe ID, você verá isso. Clique no projeto do site para abri-lo.

![RTCDP](./images/builder1.png)

Agora vocês verão isto. Ir para **Compartilhar**. Clique em **Gerar link** e copie o link para a área de transferência.

![RTCDP](./images/builder2.png)

Vá para [https://bitly.com](https://bitly.com), cole o link copiado e clique em **Criar seu link**.

![RTCDP](./images/builder4.png)

Agora você receberá um link encurtado, que tem esta aparência: `https://adobe.ly/3PpGcFk`. Você precisará desse link no próximo exercício.

![RTCDP](./images/builder5.png)

## 3.3.4.2 Coletar

Agora vá para a página inicial do Adobe Experience Cloud em [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Clique em **Target**.

Na página inicial do **Adobe Target**, você verá todas as atividades existentes. Clique em **Criar atividade** e em **Direcionamento de experiência**.

Agora selecione **Visual** e cole seu link encurtado no campo **Inserir URL da Atividade**. Clique em **Criar**.

![RTCDP](./images/exclatcrxt1.png)

Você verá seu projeto de site de demonstração ser carregado no Visual Experience Composer.

>[!NOTE]
>
>Caso seu site não esteja carregando corretamente, instale e habilite esta extensão do Chrome: **Adobe Target VEC Helper** da Chrome Web Store e tente novamente.

![RTCDP](./images/vec1.png)

Clique na área que contém a oferta do Disney+. Selecione o **Contêiner** completo. Clique em **Inserir antes** e selecione **Decisão de Oferta**.

![RTCDP](./images/vec3.png)

Você então verá esse pop-up. Selecione sua sandbox `--aepSandboxName--` e selecione o posicionamento **Web - Image**.

![RTCDP](./images/vec4.png)

Em seguida, selecione sua decisão `--aepUserLdap-- - CitiSignal Decision`. Clique em **Salvar**.

![RTCDP](./images/vec5.png)

Você verá isso. Clique em **Regra de revisão**.

![RTCDP](./images/vec5a.png)

Certifique-se de adicionar uma regra de modelo adicional **URL** **contém** **nome-do-seu-projeto**. Clique em **Salvar**.

![RTCDP](./images/vec6.png)

Você verá isso. Clique em **Next**.

![RTCDP](./images/vec7.png)

Digite um nome para sua oferta, use este nome: `--aepUserLdap-- - XT with Offers (VEC)`. Clique em **Next**.

![RTCDP](./images/vec8.png)

Você verá isso. Defina sua **Métrica de meta** conforme indicado. Clique em **Salvar e fechar**.

![RTCDP](./images/vec9.png)

Sua oferta foi criada e está sendo publicada. Depois que a oferta for publicada, você poderá ativá-la.

![RTCDP](./images/vec11.png)

Próxima Etapa: [3.3.5 Use sua decisão em um email e sms](./ex5.md)

[Voltar ao módulo 3.3](./offer-decisioning.md)

[Voltar a todos os módulos](./../../../overview.md)
