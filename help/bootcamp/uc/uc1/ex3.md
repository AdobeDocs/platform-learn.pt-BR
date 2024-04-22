---
title: Bootcamp - Perfil do cliente em tempo real - Criar um segmento - Interface do usuário
description: Bootcamp - Perfil do cliente em tempo real - Criar um segmento - Interface do usuário
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Segments
exl-id: 37d4a5e8-e2bc-4c8c-a74f-09f74ea79962
source-git-commit: ee5c0af17c12f1d90774a3a4150c9788e2368e39
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 3%

---

# 1.3 Criar um segmento - IU

Neste exercício, você criará um segmento usando o Construtor de segmentos da Adobe Experience Platform.

## Story

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, é necessário selecionar um **sandbox**. A sandbox a ser selecionada é chamada ``Bootcamp``. Você pode fazer isso clicando no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. Depois de selecionar as opções [!UICONTROL sandbox], você verá a alteração de tela e agora estará em seu dedicado [!UICONTROL sandbox].

![Assimilação de dados](./images/sb1.png)

No menu no lado esquerdo, acesse **Segmentos**. Nesta página, você pode ter uma visão geral de todos os segmentos existentes. Clique no link **+ Criar segmento** botão para começar a criar um novo segmento.

![Segmentação](./images/menuseg.png)

Quando estiver no novo construtor de segmentos, você notará imediatamente a **Atributos** e a opção de menu **Perfil individual XDM** referência.

![Segmentação](./images/segmentationui.png)

Como o XDM é a linguagem que impulsiona os negócios da experiência, o XDM também é a base para o construtor de segmentos. Todos os dados assimilados na Platform devem ser mapeados em relação ao XDM e, como tal, todos os dados se tornam parte do mesmo modelo de dados, independentemente de onde esses dados vêm. Isso oferece uma grande vantagem ao criar segmentos. A partir dessa interface do construtor de segmentos, é possível combinar dados de qualquer origem no mesmo fluxo de trabalho. Os segmentos criados no Construtor de segmentos podem ser enviados para soluções como Adobe Target, Adobe Campaign e Adobe Audience Manager para ativação.

Agora é necessário criar um segmento de todos os clientes que visualizaram o produto **Real-Time CDP**.

Para criar esse segmento, é necessário adicionar um Evento de experiência. Você pode encontrar todos os Eventos de experiência clicando no link **Eventos** ícone no **Campos** barra de menus.

![Segmentação](./images/findee.png)

Em seguida, você verá o nível superior, **XDM ExperienceEvents** nó. Clique em **XDM ExperienceEvent**.

![Segmentação](./images/see.png)

Ir para **Itens da lista de produtos**.

![Segmentação](./images/plitems.png)

Selecionar **Nome** e arraste e solte o **Nome** do menu esquerdo na tela do construtor de segmentos na janela **Eventos** seção. Você verá isto:

![Segmentação](./images/eewebpdtlname.png)

O parâmetro de comparação deve ser **igual a** e, no campo de entrada, digite **Real-time CDP**.

![Segmentação](./images/pv.png)

Toda vez que você adiciona um elemento ao construtor de segmentos, é possível clicar no **Atualizar Estimativa** para obter uma nova estimativa da população no seu segmento.

![Segmentação](./images/refreshest.png)

Como **Método de avaliação**, selecione **Edge**.

![Segmentação](./images/evedge.png)

Por fim, vamos dar um nome ao seu segmento e salvá-lo.

Como convenção de nomenclatura, use:

- `yourLastName - Interest in Real-Time CDP`

Em seguida, clique no link **Salvar e fechar** botão para salvar seu segmento.

![Segmentação](./images/segmentname.png)

Você será redirecionado para a página de visão geral do segmento agora, onde verá uma amostra dos perfis de clientes qualificados para o seu segmento.

![Segmentação](./images/savedsegment.png)

Agora você pode continuar com o próximo exercício e usar seu segmento com o Adobe Target.

Próxima etapa: [1.4 Ação: enviar o segmento para o Adobe Target](./ex4.md)

[Voltar para Fluxo de Usuário 1](./uc1.md)

[Voltar a todos os módulos](../../overview.md)
