---
title: Coleta de dados - FAC - Criar uma composição federada
description: Foundation - FAC - Criar uma composição federada
kt: 5342
doc-type: tutorial
exl-id: 293bf825-d0d6-48cf-9cbf-69f622597678
source-git-commit: 1c91cb2129f827fd39dc065baf5d8ea067a5731a
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 3%

---

# 1.3.3 Criar uma composição federada

Agora você pode configurar a composição do público-alvo federado na AEP.

Faça logon no Adobe Experience Platform acessando esta URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./../module1.2/images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepSandboxName--``. Depois de selecionar a sandbox apropriada, você verá a alteração da tela e agora estará em sua sandbox dedicada.

![Assimilação de dados](./../module1.2/images/sb1.png)

## 1.3.3.1 Criar seu público-alvo

No menu esquerdo, vá para **Audiences** e depois vá para **Federated compositions**. Clique em **Criar composição**.

![FAC](./images/fedcomp1.png)

Para o rótulo, use este: `--aepUserLdap-- - CitiSignal Fiber`. Selecione o modelo de dados criado no exercício anterior, denominado `--aepUserLdap-- - CitiSignal Snowflake Data Model`. Clique em **Criar**.

![FAC](./images/fedcomp2.png)

Você verá isso.

![FAC](./images/fedcomp3.png)

Clique no ícone **+** e clique em **Criar público-alvo**.

![FAC](./images/fedcomp4.png)

Você verá isso. Selecione **Criar audiência**. Clique no ícone **pesquisar** para selecionar um esquema.

![FAC](./images/fedcomp5.png)

Selecione o esquema **CK_HOUSEHOLDS**. Clique em **Confirmar**.

![FAC](./images/fedcomp6.png)

Em seguida, clique em **Continuar**.

![FAC](./images/fedcomp7.png)

Agora você pode começar a criar a consulta que será enviada para o Snowflake. Clique no ícone **+** e em **Condição personalizada**.

![FAC](./images/fedcomp8.png)

Selecione o atributo **ISELIGIBLEFORFIBER** Clique em **Confirmar**.

![FAC](./images/fedcomp9.png)

Você verá isso. Defina o campo **Value** como **True**. Clique em **Calcular** para encaminhar a consulta para Snowflake e obter uma estimativa dos perfis que agora estão qualificados.

![FAC](./images/fedcomp10.png)

Em seguida, clique novamente no ícone **+** e clique novamente em **Condição personalizada** para adicionar outra condição.

![FAC](./images/fedcomp11.png)

A segunda condição a ser adicionada é: `Is the user an existing CitiSignal Mobile subscriber?`. A maneira de responder a essa pergunta é usar o relacionamento entre a família e o cliente principal da organização, que é definido em outra tabela, **CK_PERSONS**. Você pode detalhar no menu de atributos usando o link **household2person**.

![FAC](./images/fedcomp12.png)

Selecione o atributo **ISMOBILESUB** e clique em **Confirmar**.

![FAC](./images/fedcomp13.png)

Defina o campo **Valor** como **Verdadeiro** Clique em **Calcular** novamente para atualizar o número de perfis que serão direcionados. Clique em **Confirmar**.

![FAC](./images/fedcomp14.png)

Clique no ícone **+** e em **Salvar público-alvo**.

![FAC](./images/fedcomp15.png)

Defina o **Rótulo do público-alvo** como `--aepUserLdap-- - CitiSignal Eligible for Fiber`.

Clique em **+ Adicionar mapeamento de público-alvo**.

![FAC](./images/fedcomp16.png)

Selecione **HOUSEHOLD_ID** e clique em **Confirmar**.

![FAC](./images/fedcomp17.png)

Clique em **+ Adicionar mapeamento de público-alvo**.

![FAC](./images/fedcomp18.png)

Detalhe clicando em **Targeting dimension**.

![FAC](./images/fedcomp18a.png)

Detalhe clicando no link **household2person**.

![FAC](./images/fedcomp18b.png)

Selecione o campo **NAME**. Clique em **Confirmar**.

![FAC](./images/fedcomp18c.png)

Clique em **+ Adicionar mapeamento de público-alvo**.

![FAC](./images/fedcomp20.png)

Detalhe clicando em **Targeting dimension**.

![FAC](./images/fedcomp20a.png)

Detalhe clicando no link **household2person**.

![FAC](./images/fedcomp20b.png)

Selecione o campo **EMAIL**. Clique em **Confirmar**.

![FAC](./images/fedcomp20c.png)

Você verá isso. Agora é necessário definir o **Campo de identidade principal**, defina-o como **Household2person_EMAIL**.

Clique em **Salvar**.

![FAC](./images/fedcomp21.png)

Sua composição foi concluída. Clique em **Iniciar** para executá-lo.

O query será agora enviado para o Snowflake, que consultará os dados de origem lá. Os resultados serão enviados de volta para a AEP, mas os dados de origem permanecerão no Snowflake.

O público-alvo agora é preenchido e pode ser direcionado de dentro do ecossistema da AEP.

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao módulo 1.3](./fac.md)

[Voltar a todos os módulos](../../../overview.md)
