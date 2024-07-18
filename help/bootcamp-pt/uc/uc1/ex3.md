---
title: Bootcamp - Perfil do cliente em tempo real - Criar um segmento - Interface do usuário - Brasil
description: Bootcamp - Perfil do cliente em tempo real - Criar um segmento - Interface do usuário - Brasil
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Segments
exl-id: 9b8d93b5-5bed-4600-8602-b438a0893612
source-git-commit: ee5c0af17c12f1d90774a3a4150c9788e2368e39
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 2%

---

# 1.3 Segmento do crime - IU

Neste exercício, você irá criar um segmento usando o Construtor de Segmentos da Adobe Experience Platform.

## História

Acessado [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você acessará a página inicial da Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, você seleciona **sandbox**. O nome do sandbox a ser selecionado é ``Bootcamp``. É possível fazer isso no texto **[!UICONTROL Produção Prod]** na linha azul na parte superior da tela. Depois de pegar a sandbox, você verá a tela e agora você está em seu [!UICONTROL sandbox].

![Assimilação de dados](./images/sb1.png)

Nenhum menu à esquerda, acessado **Segmentos**. Nesta página, você uma visão geral de todos os segmentos existentes. Clique no botão + Criar segmento para iniciar um novo segmento.

![Segmentação](./images/menuseg.png)

Quando não há nenhum novo criador de segmentos, você vai mudar a opção de menu **Atributos** e a referência do **Perfil Individual XDM**.

![Segmentação](./images/segmentationui.png)

Como o XDM é a linguagem que alimenta o setor de experiência, o XDM também é uma base para o construtor de segmentos. Todos os dados ingeridos na plataforma devem ser mapeados em relação ao XDM e, portanto, todos os dados se tornarem parte do mesmo modelo de dados, da origem desses dados. Isso oferece uma grande vantagem ao fluxo de trabalho, pois a partir interface do usuário do construtor de segmento, é possível dados de qualquer no fluxo de trabalho. Os no Condutor de, e usuário para estrategistas Adobe Target Adobe Campaign Adobe Audience Manager para.

Agora você pode criar um segmento de todos os clientes que visualizaram o produto **Real-Time CDP**.

Para a investigação do segmento, você acompanha um evento de experiência. Você pode encontrar todos os Eventos de alteração no **Eventos** na barra de menu **Campos**.

![Segmentação](./images/findee.png)

Em seguida, você verá o nó **XDM ExperienceEvents** do nível superior. Clique em **XDM ExperienceEvent**.

![Segmentação](./images/see.png)

Acessar **Itens da Lista de Produtos**.

![Segmentação](./images/plitems.png)

**Nome** e conduta solte o objeto **Nome** do menu à esquerda na tela do construtor de na **Eventos**. Em seguida, o seguinte é apresentado:

![Segmentação](./images/eewebpdtlname.png)

O mistura de usar deve **equals** e, no campo de entrada, insira **CDP em tempo real**.

![Segmentação](./images/pv.png)

Sempre que basear um elemento ao construtor de segmentos, você pode mudar no botão **Atualizar Estimativa** para obter uma nova entidade da população em seu segmento.

![Segmentação](./images/refreshest.png)

Para **Método De Avaliação**, **Edge**.

![Segmentação](./images/evedge.png)

Por fim, vamos dar um nome ao seu segmento e salvá-lo.

Como modelo de nomenclatura, uso:

- `seuSobrenome - Interest in Real-Time CDP`

Em seguida, clique no botão **Salvar e fechar** para salvar seu segmento.

![Segmentação](./images/segmentname.png)

Agora você irá mudar à página de visão geral segmento, onde verá uma aula de navegação dos clientes que se qualifica para o seu segmento.

![Segmentação](./images/savedsegment.png)

Agora você pode continuar no próximo exercício e usar seu segmento com o Adobe Target.

Próxima etapa: [1.4 Ação: desejada seu segmento para o Adobe Target](./ex4.md)

[Retorno para Fluxo de monitoramento 1](./uc1.md)

[Retorno para Todos os compartilhados](../../overview.md)
