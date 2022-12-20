---
title: Construir segmentos
seo-title: Build segments | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Construir segmentos
description: Nesta lição, criaremos alguns segmentos com base nos dados de perfil que assimilamos nas lições anteriores.
role: Data Architect
feature: Data Governance
kt: 4348
thumbnail: 4348-build-segments.jpg
exl-id: cd05e814-1ea7-48ba-adf6-1a71504c623e
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 2%

---

# Construir segmentos

<!-- 30 min-->
Nesta lição, criaremos alguns segmentos com base nos dados de perfil que assimilamos nas lições anteriores.

Depois de ter os Perfis do cliente em tempo real, você pode criar segmentos de indivíduos que compartilham características semelhantes e podem responder de forma semelhante às estratégias de marketing. Os blocos de construção desses segmentos são os campos XDM criados anteriormente.

**Arquitetos de dados** O precisará criar segmentos fora deste tutorial e suportar seus colegas com esta tarefa.

Antes de começar os exercícios, assista a este breve vídeo para saber mais sobre como criar segmentos:
>[!VIDEO](https://video.tv.adobe.com/v/27254?quality=12&learn=on)


## Permissões necessárias

No [Configurar permissões](configure-permissions.md) lição, você configura todos os controles de acesso necessários para concluir esta lição, especificamente:

* Itens de permissão **[!UICONTROL Gerenciamento de perfis]** > **[!UICONTROL Gerenciar segmentos]**, **[!UICONTROL Exibir segmentos]** e **[!UICONTROL Exportar segmento de público-alvo]**
* Itens de permissão **[!UICONTROL Gerenciamento de perfis]** > **[!UICONTROL Exibir perfis]** e **[!UICONTROL Gerenciar perfis]**
* Item de permissão **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* Acesso da função de usuário ao `Luma Tutorial Platform` perfil de produto
* Acesso da função de desenvolvedor ao `Luma Tutorial Platform` perfil de produto (para API)

## Criar um segmento básico

Vamos criar um segmento simples para clientes do programa de fidelidade com um status Gold ou Platinum

1. Na interface do usuário da Platform, acesse **[!UICONTROL Segmentos]** na navegação à esquerda
1. Selecione o **[!UICONTROL Criar segmento]** botão
1. À esquerda do construtor de esquema há três guias para Atributos (Dados de registro), Eventos (Dados de série de tempo) e Públicos-alvo
1. Selecione o ícone de engrenagem para observar o padrão do construtor de segmentos em mostrar apenas os campos com dados e permitir alterar a política de mesclagem
1. Na guia Atributos , navegue até a guia **Perfil individual XDM > Fidelidade** pasta (você também pode pesquisar por &quot;fidelidade&quot;)
1. Arrastar e soltar, `Tier` do menu de campos de atributo para a tela do construtor de segmentos
1. Selecionar `Tier` igual `Gold` ou `Platinum`
1. Selecionar **[!UICONTROL Atualizar estimativa]** para ver quantos perfis se qualificam para seu segmento
1. Como **[!UICONTROL Nome]**, insira `Luma customers with level Gold or Above`
1. Selecione **[!UICONTROL Salvar]**
   ![Segmento](assets/segment-goldOrAbove.png)

<!--## Build a sequential segment-->

## Criar um segmento dinâmico

Neste exercício, criaremos um segmento para clientes que compraram o mesmo produto duas vezes em 30 dias. Segmentos dinâmicos permitem dimensionar sua segmentação usando campos como variáveis.

1. Ir para **[!UICONTROL Segmentos]** na navegação à esquerda
1. Selecione o **[!UICONTROL Criar segmento]** botão
1. Selecione o **[!UICONTROL Eventos]** guia
1. Filtrar a lista para `purchases`
1. Arraste o **[!UICONTROL Compras]** tipo de evento na tela de desenho _duas vezes_
1. Selecione o ícone do relógio entre os dois **[!UICONTROL Compras]** e escolha &quot;em 30 dias&quot;
1. Confirme se a definição de segmento neste ponto é lida **&quot;Inclua público-alvo que tenha pelo menos 1 evento de Compras e, em seguida, em 30 dias tenha pelo menos 1 evento de Compras&quot;**

   ![Duas compras no prazo de 30 dias](assets/segment-twoPurchases.png)
1. Agora, altere o filtro de eventos para `sku`
1. Arraste o campo SKU para o segundo evento de compra
   ![Duas compras em 30 dias com SKU](assets/segment-twoPurchases-addSku.png)
1. Agora, limpe o filtro de eventos
1. Você deve ver no **[!UICONTROL Procurar variáveis]** , há pastas para os dois eventos de compra. Clique para explorar **[!UICONTROL Compras 1]**\
   ![Duas compras dentro de 30 dias com SKU, navegue pela primeira compra](assets/segment-twoPurchases-browsePurchaseOne.png)
1. Detalhe no **[!UICONTROL Itens da lista de produtos]** selecione a pasta **[!UICONTROL SKU]** e arraste-o para a direita do campo **[!UICONTROL igual]** operando. Ao passar o cursor do mouse sobre a área, solte-a na seção &quot;Adicionar operandos para comparar&quot;
1. Dê um nome ao seu segmento `Bought same product within 30 days`
1. Confirme se sua definição de público-alvo é **&quot;Inclua público-alvo que tenha pelo menos 1 evento de Compras e, em 30 dias, tenha pelo menos 1 evento de Compras em que (SKU é igual a Compras1 SKU)&quot;**
1. Selecione o botão **[!UICONTROL Salvar]**

   ![Comprou o mesmo produto no segmento dos últimos 30 dias](assets/segment-boughtSameProduct.png)

## Criar um segmento de várias entidades

Lembre-se de como criamos a relação entre a `Luma Offline Purchase Events Schema` e `Luma Product Catalog Schema` em lições anteriores? Fizemos isso para que pudéssemos usar a relação em nosso schema usando a segmentação de várias entidades.

Com o recurso avançado de segmentação de várias entidades, você pode criar segmentos usando várias classes XDM para estender seus esquemas. Como resultado, o construtor de segmentos pode acessar campos adicionais como se eles estivessem nativos no armazenamento de dados do perfil

Você criará o próximo segmento ao aplicar a relação criada entre seus `Luma Product Catalog Schema` e seu `Luma Offline Purchase Events Schema`.

1. Ir para **[!UICONTROL Segmentos]** na navegação à esquerda
1. Selecione o **[!UICONTROL Criar segmento]** botão
1. Selecione o **[!UICONTROL Eventos]** guia
1. Filtrar a lista para `purchases`
1. Arraste o **[!UICONTROL Compras]** tipo de evento na tela de desenho
1. Selecione o menu suspenso do relógio acima do evento e escolha **[!UICONTROL nos últimos 30 dias]**
1. Filtre o **[!UICONTROL Eventos]** listar para `category` e arraste a **[!UICONTROL Categoria do produto]** campo para **[!UICONTROL Compras]**
1. Altere o operador para **[!UICONTROL começa com]** e insira `men` na caixa de texto
1. Como **[!UICONTROL Nome]**, insira `Purchased a Men's product in the last 30 days`
1. Confirmar a definição do público-alvo `(Include audience who have at least 1 Purchases event where ((Product Category starts with men)) ) and occurs in last 30 day(s)`
1. Selecione o botão **[!UICONTROL Salvar]**

   ![Comprou o mesmo produto no segmento dos últimos 30 dias](assets/segment-purchasedMens.png)

## Segmentação em lote e streaming

Clique em **[!UICONTROL Segmentos]** na navegação à esquerda e vamos tomar um momento para revisar nossos três segmentos:

* Dois de nossos segmentos são segmentos em lote e um é um segmento de transmissão.
* O padrão da plataforma é a segmentação de fluxo sempre que possível, qualificando o cliente para um segmento assim que ele atender aos critérios. Quando as definições de segmento são muito complexas para transmissão, elas são convertidas automaticamente em lote. Nesse caso, o padrão para os dois segmentos era batch, pois a janela de retrospectiva dos eventos de compra era superior a sete dias. Para obter uma lista completa e atual das limitações de transmissão, consulte [a documentação](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/streaming-segmentation.html).
* Os trabalhos em lote são executados em uma programação diária, que pode ser desativada.

![Comprou o mesmo produto no segmento dos últimos 30 dias](assets/segment-review.png)

## Recursos adicionais

* [Documentação do Serviço de segmentação](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html)
* [Referência da API do serviço de segmentação](https://www.adobe.io/experience-platform-apis/references/segmentation/)

Há mais para segmentação, especialmente com a ativação de segmentos. Esses tópicos serão abordados em outro tutorial.

Você conseguiu através de todos os exercícios! Por favor, prossiga para a [conclusão](conclusion.md).
