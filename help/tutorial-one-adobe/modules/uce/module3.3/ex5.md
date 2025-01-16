---
title: Offer Decisioning - Use sua decisão em um email
description: Use sua decisão em um email
kt: 5342
doc-type: tutorial
source-git-commit: 91dbf1aac923c26608528b163bbd68218d45425b
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 1%

---

# 3.3.5 Use sua decisão em um email

Neste exercício, você usará sua decisão para personalizar o delivery de um email e SMS.

Vá para **Jornada**. Localize a jornada criada no exercício 3.1.3, denominado `--aepUserLdap-- - Registration Journey`. Clique na jornada para abri-la.

![Journey Optimizer](./images/emailoffer1.png)

Você verá isso. Clique em **... Mais** e, em seguida, clique em **Criar uma nova versão**.

![Journey Optimizer](./images/journey1.png)

Clique em **Criar uma nova versão**.

![Journey Optimizer](./images/journey2.png)

Clique na ação **Email** e em **Editar conteúdo**.

![Journey Optimizer](./images/journey3.png)

Em seguida, você verá o painel da mensagem. Clique em **Editar corpo do email**.

![Journey Optimizer](./images/emailoffer2.png)

Você verá isso. Arraste um novo componente de estrutura **1:1 coluna** para a tela.

![Journey Optimizer](./images/emailoffer6.png)

No menu, vá para **Conteúdo**. Selecione o componente **Offer decision** e arraste e solte esse componente no espaço reservado de oferta de conteúdo do email, conforme indicado. Em seguida, clique em **Adicionar**.

![Journey Optimizer](./images/emailoffer7.png)

Selecione o tipo de posicionamento que deseja incluir no email. No menu suspenso **Posicionamentos**, selecione **Email - Imagem** e escolha sua decisão `--aepUserLdap-- - CitiSignal Decision`. Clique em **Adicionar**.

![Journey Optimizer](./images/emailoffer8.png)

Agora é possível percorrer todas as ofertas personalizadas e a oferta substituta, todas sendo visualizadas dentro do designer de email. Clique em **Salvar**.

![Journey Optimizer](./images/emailoffer9.png)

Agora, clique na seta para voltar à tela anterior.

![Journey Optimizer](./images/emailoffer13.png)

Clique na seta no canto superior esquerdo para voltar à jornada.

![Journey Optimizer](./images/emailoffer14.png)

Clique em **Salvar** para fechar sua ação de **Email**.

![Journey Optimizer](./images/emailoffer14a.png)

Clique em **Publish** para publicar sua jornada atualizada.

![Journey Optimizer](./images/emailoffer14b.png)

Confirme clicando em **Publish** novamente.

![Journey Optimizer](./images/emailoffer15.png)

Sua mensagem foi publicada.

![Journey Optimizer](./images/emailoffer16.png)

Ao criar uma nova conta no site de demonstração, você receberá este email:

![Journey Optimizer](./images/emailoffer17.png)

Você concluiu este exercício.

Próxima etapa: [3.3.6 Teste sua decisão usando a API](./ex6.md)

[Voltar ao módulo 3.3](./offer-decisioning.md)

[Voltar a todos os módulos](./../../../overview.md)
