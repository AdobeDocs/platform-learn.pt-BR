---
title: Criar um público-alvo
seo-title: Create an audience | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Criar um público-alvo
description: Nesta lição, configuramos uma conexão entre o Adobe Experience Platform e o Data Warehouse corporativo para ativar a Federated Audience Composition.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
hide: true
source-git-commit: a5ae2695763bc3d6dce786861dcbc15f3422c035
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 3%

---


# Exercício de criação de público-alvo

Este exercício orienta você na criação de um público-alvo do Data Warehouse usando a Composição de público-alvo federado. Criamos um público-alvo para qualificar clientes do SecurFinancial com uma pontuação de crédito de 650 ou superior e que atualmente não têm um empréstimo em seu portfólio do SecurFinancial.

## Etapas

1. No portal **Cliente > Públicos-alvo**, clique na guia **Federated compositions**.
2. Clique em **Criar composição**.

   ![criar-composição](assets/create-composition.png)

3. Rotular sua composição como `SecurFinancial Customers - No Loans, Good Credit + [your lab user ID]`. Clique em **Criar**.

4. Clique no botão **+** na tela e selecione **Criar público-alvo**. O painel direito deve ser exibido.

5. Clique em **Selecionar um esquema**, selecione o esquema **FSI_CRM** e clique em **Confirmar**.

6. Clique em **Continuar**. Na janela do construtor de consultas, clique no botão **+** e depois em **Condição Personalizada**. Crie as seguintes condições:
   - `CURRENTPRODUCTS does not contain loan`
   - `AND`
   - `CREDITSCORE greater than or equal to 650`
   - Usamos dados de preferência de marketing para segmentar clientes que optaram pelo email como canal de comunicação preferido:
   - `AND`
   - `CONSENTSMARKETINGPREFERRED equal to email`

   **Observação:** o campo de valor diferencia maiúsculas de minúsculas.

   Sua consulta agora deve ser semelhante a:

   ![construtor de consultas](assets/query-builder.png)

7. Clique no botão **+** seguinte e em **Salvar público-alvo**.

   Rotular esta etapa como `SecurFinancial Customers - No Loans, Good Credit + [your lab user ID]`. Use o mesmo valor que o rótulo do público-alvo.

8. Adicione os seguintes mapeamentos de público-alvo:
   - **Campo de público-alvo do Source:** EMAIL
   - **Campo de público-alvo do Source:** PRODUTOSATUAIS
   - **Campo de público-alvo do Source:** NOME

9. Selecione a identidade e o namespace principais a serem usados para perfis:
   - **Campo de identidade principal:** email
   - **Namespace de identidade:** email

10. Clique em **Salvar** e em **Iniciar** para executar a consulta da composição que acabou de criar.

**Observação:** usamos informações de produto e crédito para criar nosso público-alvo que não moveu dados confidenciais, como pontuação de crédito, para plataformas downstream para ativação.

Para obter mais informações sobre a composição de públicos, visite [Experience League](https://experienceleague.adobe.com/pt-br/docs/federated-audience-composition/using/compositions/create-composition/create-composition){target="_blank"}.

Agora que nosso público-alvo federado foi criado, vamos avançar com [o mapeamento para uma conta S3](map-federated-audience-to-s3.md).
