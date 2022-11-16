---
title: Offer Decisioning - Use sua decisão em um e-mail
description: Use sua decisão em um email
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 0fb8c244-1025-479f-b82e-374d1aa5e4dc
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 11%

---

# 9.5 Use sua decisão em um e-mail

Neste exercício, você usará sua decisão para personalizar o delivery de um email e SMS.

Ir para **Jornada**. Encontre a jornada criada no exercício 7.2, que é chamada de `--demoProfileLdap-- - Account Creation Journey`. Clique na jornada para abri-la.

![Journey Optimizer](./images/emailoffer1.png)

Você verá isso. Clique em **Criar uma nova versão**.

![Journey Optimizer](./images/journey1.png)

Clique em **Criar uma nova versão**.

![Journey Optimizer](./images/journey2.png)

Clique no botão **Email** e clique em **Editar conteúdo**.

![Journey Optimizer](./images/journey3.png)

Em seguida, você verá o painel de mensagens. Clique em **Email Designer**.

![Journey Optimizer](./images/emailoffer2.png)

Você verá isso.

![Journey Optimizer](./images/emailoffer5.png)

Você verá isso. Arraste um novo **Coluna 1:1** componente de estrutura na tela.

![Journey Optimizer](./images/emailoffer6.png)

No menu , acesse **Componentes de conteúdo**. Selecione o **Decisão da oferta** e arraste e solte esse componente no espaço reservado da oferta de conteúdo do email, conforme indicado. Em seguida, clique em **Adicionar**.

![Journey Optimizer](./images/emailoffer7.png)

Selecione o tipo de disposição que deseja incluir no email. No **Posicionamentos** seleção do menu suspenso **Email - Imagem** e selecione sua decisão `--demoProfileLdap-- - Luma Decision`. Clique em **Adicionar**.

![Journey Optimizer](./images/emailoffer8.png)

Agora você vê todas as ofertas personalizadas e a oferta de fallback sendo visualizada no designer de email. Clique em  **Simular conteúdo** para visualizar a mensagem de email com um perfil de cliente real.

![Journey Optimizer](./images/emailoffer9.png)

Comece identificando qual perfil você deseja usar para a visualização. Selecione o **email** namespace e insira o endereço de email de um perfil de cliente que você criou no site de demonstração. Em seguida, clique em **Visualizar**.

![Journey Optimizer](./images/emailoffer10.png)

Depois que o email for exibido e a oferta for exibida corretamente, clique no botão **Fechar** botão.

![Journey Optimizer](./images/emailoffer11.png)

Finalmente, clique em **Salvar**.

![Journey Optimizer](./images/emailoffer12.png)

Agora, clique na seta para voltar à tela anterior.

![Journey Optimizer](./images/emailoffer13.png)

Você verá isso. Clique na seta no canto superior esquerdo para retornar à jornada.

![Journey Optimizer](./images/emailoffer14.png)

Clique em **Ok** para fechar **Email** ação.

![Journey Optimizer](./images/emailoffer14a.png)

Clique em **Publicar** para publicar sua jornada atualizada.

![Journey Optimizer](./images/emailoffer14b.png)

Confirme clicando em **Publicar** novamente.

![Journey Optimizer](./images/emailoffer15.png)

Sua mensagem foi publicada.

![Journey Optimizer](./images/emailoffer16.png)

Ao criar uma nova conta no site de demonstração, você receberá este email:

![Journey Optimizer](./images/emailoffer17.png)

Terminou este exercício.

Próxima etapa: [9.6 Teste sua decisão usando a API](./ex6.md)

[Voltar ao Módulo 9](./offer-decisioning.md)

[Voltar para todos os módulos](./../../overview.md)
