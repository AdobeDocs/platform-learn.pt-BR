---
title: Mapear um público-alvo federado para S3
seo-title: Map a federated audience to S3 | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Mapear um público-alvo federado para S3
description: Nesta lição, mapearemos um público-alvo federado para um destino downstream do Real-Time CDP para oferecer suporte a uma experiência offline personalizada.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
hide: true
source-git-commit: a5ae2695763bc3d6dce786861dcbc15f3422c035
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# Mapear o público-alvo federado para S3 para aproveitar os atributos do público-alvo para enriquecimento

Neste exercício, você aprenderá a aproveitar os atributos de público-alvo no data warehouse para enriquecer a experiência do público-alvo em workflows de ativação downstream usando destinos do RTCDP. Para o SecurFinancial, esses atributos federados podem ser usados para aprimorar a experiência de personalização offline do público-alvo do cliente. Neste exemplo, mapearemos o público-alvo federado para um destino do Amazon S3 pré-configurado.

## Etapas

1. Navegue até o portal **Destinos**.

2. Clique no botão **3 do menu de pontos** ao lado do destino pré-configurado do Amazon S3 e clique em **Ativar Públicos-alvo**.

   ![ativar-públicos](assets/activate-audiences.png)

3. Selecione o **destino S3** e clique em **Avançar**.

   ![selecionar-destino-s3](assets/select-s3-destination.png)

4. Selecione o público **SecureFinancial Customers - No Loans, Good Credit**.

   ![select-s3-audience](assets/select-s3-audience.png)

5. Na seção **Agendando**, deixe todas as configurações padrão e clique em **Avançar**.

6. Na etapa **Mapping**, verifique se o item a seguir está incluído e selecionado como a **Chave de Desduplicação**. Em seguida, clique em **Avançar**:
   - `xdm: personalEmail.address`

   ![chave-de-desduplicação](assets/deduplication-key.png)

7. Na etapa de mapeamento a seguir, é possível selecionar atributos de enriquecimento com base nos mapeamentos de campo de público-alvo na composição de público-alvo federado. Clique no ícone de **lápis (editar)** para exibir os atributos pré-selecionados.

   ![editar-atributos](assets/edit-attributes.png)

   ![atributos finais](assets/final-attribution.png)

8. Revise seu mapeamento de público e clique em **Concluir**.

Estamos prontos para avançar para [criar uma jornada](build-journey-federated-audience.md).
