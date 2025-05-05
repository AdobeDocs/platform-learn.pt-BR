---
title: Construir segmentos
seo-title: Build segments | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Construir segmentos
description: Nesta lição, criaremos alguns segmentos com base nos dados de perfil assimilados nas lições anteriores.
role: Data Architect
feature: Data Governance
jira: KT-4348
thumbnail: 4348-build-segments.jpg
exl-id: cd05e814-1ea7-48ba-adf6-1a71504c623e
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 0%

---

# Construir segmentos

<!-- 30 min-->
Nesta lição, criaremos alguns segmentos com base nos dados de perfil assimilados nas lições anteriores.

Depois de ter Perfis de clientes em tempo real, você pode criar segmentos de indivíduos que compartilham características semelhantes e podem responder de forma semelhante às estratégias de marketing. Os blocos de construção desses segmentos são os campos XDM criados anteriormente.

**Os Arquitetos de Dados** precisarão criar segmentos fora deste tutorial e dar suporte a seus colegas nessa tarefa.

Antes de começar os exercícios, assista a este vídeo curto para saber mais sobre a criação de segmentos:
>[!VIDEO](https://video.tv.adobe.com/v/31685?learn=on&enablevpops&captions=por_br)


## Permissões necessárias

Na lição [Configurar Permissões](configure-permissions.md), você configura todos os controles de acesso necessários para concluir esta lição, especificamente:

* Itens de permissão **[!UICONTROL Gerenciamento de perfil]** > **[!UICONTROL Gerenciar segmentos]**, **[!UICONTROL Exibir segmentos]** e **[!UICONTROL Exportar segmento de público-alvo]**
* Itens de permissão **[!UICONTROL Gerenciamento de perfil]** > **[!UICONTROL Exibir perfis]** e **[!UICONTROL Gerenciar perfis]**
* Item de permissão **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* Acesso de função de usuário ao perfil de produto `Luma Tutorial Platform`
* Acesso da função de desenvolvedor ao perfil de produto `Luma Tutorial Platform` (para API)

## Criar um segmento básico

Vamos criar um segmento simples para clientes do programa de fidelidade com status Ouro ou Platina

1. Na interface do usuário da Platform, acesse **[!UICONTROL Segmentos]** na navegação à esquerda
1. Selecione o botão **[!UICONTROL Criar segmento]**
1. À esquerda do construtor de esquemas, há três guias para Atributos (Registrar dados), Eventos (Dados de séries de tempo) e Públicos-alvo.
1. Selecione o ícone de engrenagem para observar como o construtor de segmentos mostra, por padrão, apenas os campos com dados e permite alterar a política de mesclagem
1. Na guia Atributos, navegue até a pasta **Perfil individual XDM > Fidelidade** (você também pode pesquisar por &quot;fidelidade&quot;)
1. Arraste e solte `Tier` do menu de campos de atributo para a tela do construtor de segmentos
1. Selecionar `Tier` igual a `Gold` ou `Platinum`
1. Selecione **[!UICONTROL Atualizar estimativa]** para ver quantos perfis se qualificam para o seu segmento
1. Como o **[!UICONTROL Nome]**, digite `Luma customers with level Gold or Above`
1. Selecione **[!UICONTROL Salvar]**
   ![Segmento](assets/segment-goldOrAbove.png)

<!--## Build a sequential segment-->

## Criar um segmento dinâmico

Neste exercício, criaremos um segmento para clientes que compraram o mesmo produto duas vezes em 30 dias. Os segmentos dinâmicos permitem dimensionar a segmentação usando campos como variáveis.

1. Vá para **[!UICONTROL Segmentos]** na navegação à esquerda
1. Selecione o botão **[!UICONTROL Criar segmento]**
1. Selecione a guia **[!UICONTROL Eventos]**
1. Filtrar a lista para `purchases`
1. Arraste o tipo de evento **[!UICONTROL Compras]** para a tela _duas vezes separadas_
1. Selecione o ícone do relógio entre os dois eventos **[!UICONTROL Compras]** e escolha &quot;dentro de 30 dias&quot;
1. Confirme se a definição do segmento neste ponto é **&quot;Incluir público-alvo que tenha pelo menos 1 evento de compras e, em 30 dias, tenha pelo menos 1 evento de compras&quot;**
   ![Duas compras em 30 dias](assets/segment-twoPurchases.png)
1. Agora altere o filtro de eventos para `sku`
1. Arraste o campo SKU para o segundo evento de compra
   ![Duas compras em 30 dias com SKU](assets/segment-twoPurchases-addSku.png)
1. Agora, limpe o filtro de eventos
1. Você deve ver na seção **[!UICONTROL Procurar variáveis]**, que há pastas para os dois eventos de compra. Clique para explorar **[!UICONTROL Compras 1]**\
   ![Duas compras em 30 dias com SKU, navegue pela primeira compra](assets/segment-twoPurchases-browsePurchaseOne.png)
1. Detalhe a pasta **[!UICONTROL itens de lista de produtos]**, selecione o campo **[!UICONTROL SKU]** e arraste-o para a direita do operando **[!UICONTROL equals]**. Quando você estiver passando o mouse sobre a área, solte-a na seção &quot;Adicionar para comparar operandos&quot;
1. Nomeie seu segmento `Bought same product within 30 days`
1. Confirme se a definição do seu público-alvo é **&quot;Incluir público-alvo que tenha pelo menos 1 evento de compras e, em 30 dias, tenha pelo menos 1 evento de compras onde (SKU é igual a Purchases1 SKU)&quot;**
1. Selecione o botão **[!UICONTROL Salvar]**

   ![Comprou o mesmo produto no segmento dos últimos 30 dias](assets/segment-boughtSameProduct.png)

## Criar um segmento com várias entidades

Lembra-se de como criamos a relação entre o `Luma Offline Purchase Events Schema` e o `Luma Product Catalog Schema` em lições anteriores? Fizemos isso para que pudéssemos usar o relacionamento em nosso esquema usando a segmentação de várias entidades.

Com o recurso avançado de segmentação de várias entidades, você pode criar segmentos usando várias classes XDM para estender seus esquemas. Como resultado, o construtor de segmentos pode acessar campos adicionais como se fossem nativos do armazenamento de dados do perfil

Você criará o próximo segmento aplicando a relação que você criou entre o `Luma Product Catalog Schema` e o `Luma Offline Purchase Events Schema`.

1. Vá para **[!UICONTROL Segmentos]** na navegação à esquerda
1. Selecione o botão **[!UICONTROL Criar segmento]**
1. Selecione a guia **[!UICONTROL Eventos]**
1. Filtrar a lista para `purchases`
1. Arraste o tipo de evento **[!UICONTROL Compras]** para a tela
1. Selecione a lista suspensa de relógio acima do evento e escolha **[!UICONTROL nos últimos 30 dias]**
1. Filtre a lista **[!UICONTROL Eventos]** para `category` e arraste o campo **[!UICONTROL Categoria do Produto]** até **[!UICONTROL Compras]**
1. Altere o operador para **[!UICONTROL começa com]** e insira `men` na caixa de texto
1. Como o **[!UICONTROL Nome]**, digite `Purchased a Men's product in the last 30 days`
1. Confirmar a definição de público-alvo `(Include audience who have at least 1 Purchases event where ((Product Category starts with men)) ) and occurs in last 30 day(s)`
1. Selecione o botão **[!UICONTROL Salvar]**

   ![Comprou o mesmo produto no segmento dos últimos 30 dias](assets/segment-purchasedMens.png)

## Segmentação em lote e por transmissão

Clique em **[!UICONTROL Segmentos]** na navegação à esquerda e vamos rever nossos três segmentos:

* Dois de nossos segmentos são segmentos em lote e um é um segmento de transmissão.
* A plataforma assume o padrão de segmentação por transmissão sempre que possível, qualificando o cliente para um segmento assim que ele atender aos critérios. Quando as definições de segmento são muito complexas para transmissão, elas são convertidas automaticamente em lote. Nesse caso, os dois segmentos padronizaram o lote porque a janela de retrospectiva dos eventos de compra era maior que sete dias. Para obter uma lista completa e atual das limitações de transmissão, consulte [a documentação](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/streaming-segmentation.html?lang=pt-BR).
* Os processos em lote são executados diariamente e podem ser desativados.

![Comprou o mesmo produto no segmento dos últimos 30 dias](assets/segment-review.png)

## Recursos adicionais

* [Documentação do Serviço de segmentação](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=pt-BR)
* [Referência da API do serviço de segmentação](https://www.adobe.io/experience-platform-apis/references/segmentation/)

Há mais a segmentar, especialmente com a ativação de segmentos. Esses tópicos serão abordados em outro tutorial.

Você passou por todos os exercícios! Prossiga para a [conclusão](conclusion.md).
