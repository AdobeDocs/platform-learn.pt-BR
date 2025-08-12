---
title: Criar uma jornada com dados de público-alvo federado
seo-title: Build a journey with federated audience data | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Criar uma jornada com dados de público-alvo federado
description: Nesta lição, usaremos um público federado em uma jornada do Journey Optimizer.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-build-a-journey-with-federated-audience-data.jpg
hide: true
source-git-commit: b5611dccdba66d31f7dfcd96506e06d1bdd5fb3d
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# Criar uma Jornada com dados de público-alvo federado

Nesta lição, você aprenderá como um público-alvo federado pode ser usado em jornadas no Adobe Journey Optimizer (AJO). Isso inclui o uso de atributos consultados da Composição de público-alvo federado para personalizar as mensagens. Para dar continuidade à história do cliente SecurFinancial e tratar do caso de uso de redirecionamento e personalização de clientes, organizamos uma jornada para clientes pré-qualificados. O objetivo é enviar um e-mail personalizado com base nos atributos federados do Data Warehouse do SecurFinancial.

## Etapas

### Criar uma Jornada com um público-alvo de leitura

1. Navegue até o portal **Jornada** e clique no botão **Criar Jornada**.

   ![criar-uma-jornada](assets/create-journey.png)

2. Atualize as Propriedades da Jornada com um novo nome: **`SecurFinancial - Home Loan Offer`**.

3. Clique em **Orquestração** e arraste e solte o bloco **Ler público** na tela.

4. Clique no **ícone de lápis** ao lado da caixa Público-alvo no lado direito da tela.

5. Na barra de pesquisa, pesquise por **`SecureFinancial Customers - No Loans, Good Credit`** e clique em **Salvar**.

   ![criar-uma-jornada](assets/select-audience.png)

6. Deixe todas as configurações como padrão no menu do lado direito e clique em **Salvar**.

   ![save-audience-settings](assets/save-audience-settings.png)

### Personalizar email

1. Clique em **Ações**, em seguida, clique e arraste o bloco **Email** para a tela.

2. No menu do lado direito, clique em **Configuração de email** e selecione **EmailMarketing**. Clique em **Editar conteúdo**.

3. Na linha de assunto, adicione: **`Learn more about SecurFinancial Home Loan`**. Em seguida, clique em **Editar corpo do email**.

4. Clique no botão **Modelo de conteúdo** no canto superior direito. Localize e selecione o `SecureFinancial Template` e clique em **Confirmar**.

   ![jornada-email-config](assets/journey-email-config.png)

   ![confirmação-email-jornada](assets/journey-email-confirm.png)

5. Revise o modelo e clique em **Usar Modelo**.

6. Agora você estará no Designer de email. Passe o mouse sobre a macro `{profile.person.name.firstName}` e clique no **avatar da personalização**.

7. Na janela de personalização, vá para o seguinte caminho de pasta: **`[sandbox] > audienceEnrichment > CustomerAudienceUpload`**

8. Clique na pasta **ler público**. Os atributos de enriquecimento do público-alvo federado podem ser encontrados aqui.

9. Selecione o atributo **Nome** para o construtor de expressões. O email expressará dinamicamente o valor do nome do cliente para personalizar o email.

10. Clique em **Salvar**.

11. Agora que a personalização do nome foi adicionada, adicione `Hi, ` na frente da variável de personalização. Depois clique em **Salvar**.

   ![jornada-email-salvar](assets/journey-email-save.png)

12. Clique no botão **Voltar** duas vezes para retornar à tela de jornada. No menu **Ação: Email** à direita, clique em **Salvar**.

   ![salvar-jornada-final](assets/save-final-journey.png)

Parabéns! Você criou uma jornada no AJO usando um público-alvo federado e atributos de enriquecimento federados.

Agora vamos ver como [enriquecer os públicos-alvo existentes](audience-enrichment-demo.md) na Experience Platform com dados federados do data warehouse.
