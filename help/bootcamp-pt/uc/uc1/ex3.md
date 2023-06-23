---
title: Bootcamp - Perfil do cliente em tempo real - Criar um segmento - Interface do usuário - Brasil
description: Bootcamp - Perfil do cliente em tempo real - Criar um segmento - Interface do usuário - Brasil
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 9b8d93b5-5bed-4600-8602-b438a0893612
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 2%

---

# 1.3 Segmento do crime - IU

Neste exercício, você irá criar um segmento usando o Construtor de Segmentos da Adobe Experience Platform.

## História

Acessado [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você acessará a página inicial da Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, você precisa atualizar um **sandbox**. O nome do sandbox a ser selecionado é ``Bootcamp``. É possível fazer isso no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. painel de navegação o sandbox, você é a tela e agora está você em seu [!UICONTROL sandbox] Comparar.

![Assimilação de dados](./images/sb1.png)

Sem menu à esquerda, acesso **Segmentos**. Nesta página, você uma visão geral de todos os segmentos existentes. Clique no botão + Criar segmento para iniciar um novo segmento.

![Segmentação](./images/menuseg.png)

Desde que não há novo em que o responsável de, você irá transformar a opção menu de seleção **Atributos** e a referência do **Perfil individual XDM**.

![Segmentação](./images/segmentationui.png)

Como o XDM é a linguagem que alimenta o setor de experiência, o XDM também é uma base para o construtor de segmentos. Todos os dados ingeridos na plataforma devem ser mapeados em relação ao XDM e, portanto, todos os dados se tornarem parte do mesmo modelo de dados, da origem desses dados. Isso oferece uma grande vantagem ao fluxo de trabalho, pois a partir interface do usuário do construtor de segmento, é possível dados de qualquer no fluxo de trabalho. Os no Condutor de, e usuário para estrategistas Adobe Target Adobe Campaign Adobe Audience Manager para.

Agora você pode criar um segmento de todos os clientes que visualizaram o produto **Real-Time CDP**.

Para a investigação do segmento, você acompanha um evento de experiência. Você pode encontrar todos os eventos de no **Eventos** na barra de menu **Campos**.

![Segmentação](./images/findee.png)

Em seguida, você verá o nó **XDM ExperienceEvents** do nível superior. Clique em **XDM ExperienceEvent**.

![Segmentação](./images/see.png)

Acessado **Itens da lista de produtos**.

![Segmentação](./images/plitems.png)

µ **Nome** e provas e solte o objeto **Nome** fazer menu à esquerda na tela do construtor de na **Eventos**. Em seguida, o seguinte é apresentado:

![Segmentação](./images/eewebpdtlname.png)

O ➡ de análise deve ser **igual a** e, no campo de entrada, insira **Real-time CDP**.

![Segmentação](./images/pv.png)

Sempre que interferência um elemento ao construtor de, você pode mudar no botão **Atualizar Estimativa** para obter uma nova doença da população em seu segmento.

![Segmentação](./images/refreshest.png)

Parágrafo **Método de avaliação**, **Edge**.

![Segmentação](./images/evedge.png)

Por fim, vamos dar um nome ao seu segmento e salvá-lo.

Como modelo de nomenclatura, uso:

- `seuSobrenome - Interest in Real-Time CDP`

Em seguida, clique no botão **Salvar e fechar** para salvar seu segmento.

![Segmentação](./images/segmentname.png)

Agora você irá mudar à página de visão geral segmento, onde verá uma aula de navegação dos clientes que se qualifica para o seu segmento.

![Segmentação](./images/savedsegment.png)

Agora você pode continuar no próximo exercício e usar seu segmento com o Adobe Target.

Próxima etapa: [1.4 Ação: Desejo seu segmento para o Adobe Target](./ex4.md)

[Retorno para Fluxo de monitoramento 1](./uc1.md)

[Retorno para Todos os compartilhados](../../overview.md)
