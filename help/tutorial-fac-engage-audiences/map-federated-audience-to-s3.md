---
title: Mapear um público-alvo federado para um destino S3
seo-title: Map a Federated Audience to an S3 Destination | Engage with audiences directly from your data warehouse using Federated Audience Composition
breadcrumb-title: Mapear um público-alvo federado para S3
description: Neste exercício, mapearemos um público-alvo federado para um destino downstream do Real-Time CDP para oferecer suporte a uma experiência offline personalizada.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
exl-id: a47b8f7b-7bd0-43a0-bc58-8b57d331b444
source-git-commit: 7e2f7bbb392eba51c0d6b9ccc8224c2081a01c7c
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Mapear um Público federado para um destino S3 para aproveitar os atributos do público-alvo para enriquecimento

Você pode aproveitar os atributos de público-alvo no data warehouse para enriquecer a experiência do público-alvo em workflows de ativação downstream usando destinos do RTCDP. Para o SecurFinancial, esses atributos federados podem ser usados para aprimorar a experiência de personalização offline do público-alvo do cliente. Abaixo, o público-alvo federado é mapeado para um destino do Amazon S3 pré-configurado.

## Etapas

1. Navegue até o portal **Destinos**.

2. Clique no botão **3 do menu de pontos** ao lado do destino pré-configurado do Amazon S3 e clique em **Ativar Públicos-alvo**.

   ![ativar-públicos](assets/activate-audiences.png)

3. Selecione o **destino S3** e clique em **Avançar**.

   ![selecionar-destino-s3](assets/select-s3-destination.png)

4. Selecione o público-alvo apropriado. Em nosso exemplo: **Clientes SecureFinancial - Sem Empréstimos, Bom Crédito** público-alvo.

   ![select-s3-audience](assets/select-s3-audience.png)

5. Na seção **Agendando**, use as configurações padrão e clique em **Avançar**.

6. Na etapa **Mapping**, escolha a chave de eliminação de duplicação. Em nosso exemplo, `xdm: personalEmail.address` está incluído e selecionado como a **Chave de Eliminação de Duplicação**. Em seguida, clique em **Avançar**:

   ![chave-de-desduplicação](assets/deduplication-key.png)

7. Na etapa de mapeamento, selecione atributos de enriquecimento com base nos mapeamentos de campo de público-alvo na composição de público-alvo federado. Clique no ícone de **lápis (editar)** para exibir os atributos pré-selecionados.

   ![editar-atributos](assets/edit-attributes.png)

   ![atributos finais](assets/final-attribution.png)

8. Revise seu mapeamento de público e clique em **Concluir**.

>[**!SUMMARY**]
>
> Criamos um público-alvo com sucesso e o ativamos para um destino S3 com facilidade. Qualquer outra solução pode pegar esse público-alvo e usá-lo imediatamente. A interface amigável permite que as equipes de marketing criem e ativem públicos rapidamente sem mover dados subjacentes. Os clientes que fazem essa abordagem ENTRARAM NO AR com seu primeiro caso de uso em cerca de um mês.


Agora vamos [criar uma jornada](build-journey-federated-audience.md).
