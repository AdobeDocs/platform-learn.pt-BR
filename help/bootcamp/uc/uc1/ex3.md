---
title: Bootcamp - Real-time Customer Profile - Create a segment - UI
description: Bootcamp - Real-time Customer Profile - Create a segment - UI
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 37d4a5e8-e2bc-4c8c-a74f-09f74ea79962
source-git-commit: ead28f5631fc430c41e8c756b23dc69ffe19510e
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 3%

---

# 1.3 Criar um segmento - Interface do usuário

Neste exercício, você criará um segmento usando o Construtor de segmentos do Adobe Experience Platform.

## História

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você será direcionado para a página inicial do Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, é necessário selecionar um **sandbox**. A sandbox a ser selecionada é chamada de ``Bootcamp``. Você pode fazer isso clicando no texto **[!UICONTROL Produto de produção]** na linha azul na parte superior da tela. Depois de selecionar a [!UICONTROL sandbox], você verá a tela mudar e agora você estará em seu [!UICONTROL sandbox].

![Assimilação de dados](./images/sb1.png)

No menu no lado esquerdo, vá para **Segmentos**. Nesta página, você pode ver uma visão geral de todos os segmentos existentes. Clique no botão **+ Criar segmento** botão para começar a criar um novo segmento.

![Segmentação](./images/menuseg.png)

Quando estiver no novo construtor de segmentos, você imediatamente notará o **Atributos** e a **Perfil individual XDM** referência.

![Segmentação](./images/segmentationui.png)

Como o XDM é a linguagem que alimenta os negócios da experiência, o XDM também é a base do construtor de segmentos. Todos os dados assimilados na Platform devem ser mapeados em relação ao XDM e, como tal, todos os dados se tornam parte do mesmo modelo de dados, independentemente de onde esses dados vêm. Isso oferece uma grande vantagem ao criar segmentos, a partir dessa interface do usuário do construtor de segmentos, é possível combinar dados de qualquer origem no mesmo fluxo de trabalho. Os segmentos criados no Construtor de segmentos podem ser enviados para soluções como Adobe Target, Adobe Campaign e Adobe Audience Manager para ativação.

Agora é necessário criar um segmento de todos os clientes que visualizaram o produto **Real-Time CDP**.

Para criar esse segmento, é necessário adicionar um Evento de experiência. Você pode encontrar todos os Eventos de experiência clicando no botão **Eventos** no ícone na **Campos** barra de menu.

![Segmentação](./images/findee.png)

Em seguida, você verá o nível superior, **ExperienceEvents XDM** nó . Clique em **ExperiênciaEvento XDM**.

![Segmentação](./images/see.png)

Ir para **Itens da lista de produtos**.

![Segmentação](./images/plitems.png)

Selecionar **Nome** e arraste e solte a **Nome** objeto do menu esquerdo na tela do construtor de segmentos na **Eventos** seção. Você verá isso:

![Segmentação](./images/eewebpdtlname.png)

O parâmetro de comparação deve ser **igual** e, no campo de entrada, digite **CDP em tempo real**.

![Segmentação](./images/pv.png)

Toda vez que você adicionar um elemento ao construtor de segmentos, você pode clicar no botão **Atualizar Estimativa** para obter uma nova estimativa da população em seu segmento.

![Segmentação](./images/refreshest.png)

As **Método de avaliação**, selecione **Edge**.

![Segmentação](./images/evedge.png)

Por fim, vamos dar um nome ao seu segmento e salvá-lo.

Como convenção de nomenclatura, use:

- `yourLastName - Interest in Real-Time CDP`

Em seguida, clique no botão **Salvar e fechar** para salvar o segmento.

![Segmentação](./images/segmentname.png)

Agora você será redirecionado para a página de visão geral do segmento, onde verá uma amostra de perfis de clientes qualificados para o seu segmento.

![Segmentação](./images/savedsegment.png)

Agora você pode continuar para o próximo exercício e usar seu segmento com o Adobe Target.

Próxima etapa: [1.4 Tomar medidas: enviar seu segmento para a Adobe Target](./ex4.md)

[Voltar para Fluxo de Usuário 1](./uc1.md)

[Voltar para todos os módulos](../../overview.md)
