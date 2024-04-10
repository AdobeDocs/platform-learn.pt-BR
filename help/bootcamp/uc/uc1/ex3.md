---
title: Bootcamp - Perfil do cliente em tempo real - Criar um público-alvo - Interface do usuário
description: Bootcamp - Perfil do cliente em tempo real - Criar um público-alvo - Interface do usuário
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Audiences
exl-id: 37d4a5e8-e2bc-4c8c-a74f-09f74ea79962
source-git-commit: 0474808b42925bf95529e10a42a0563f0ecc43b8
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 3%

---

# 1.3 Criar um público-alvo - Interface do usuário

Neste exercício, você criará um público-alvo usando o Audience Builder da Adobe Experience Platform.

## Story

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, é necessário selecionar um **sandbox**. A sandbox a ser selecionada é chamada ``Bootcamp``. Você pode fazer isso clicando no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. Depois de selecionar as opções [!UICONTROL sandbox], você verá a alteração de tela e agora estará em seu dedicado [!UICONTROL sandbox].

![Assimilação de dados](./images/sb1.png)

No menu no lado esquerdo, acesse **Públicos-alvo**. Nesta página, você verá Painéis com informações essenciais sobre **Público** desempenho.

![Segmentação](./images/menuseg.png)

Clique em **Procurar** para ter uma visão geral de todos os públicos-alvo existentes. Clique no link **+ Criar público-alvo** botão para começar a criar um novo público-alvo.


![Segmentação](./images/segmentationui.png)

Um pop-up será exibido perguntando se você deseja **&#39;Compor público-alvo&#39;** ou **&#39;Criar regra&#39;**. Escolher **&#39;Criar regra&#39;** para continuar e clique em **criar**.

![Segmentação][def]

Quando estiver no construtor de público-alvo, você notará imediatamente a **Atributos** e a opção de menu **Perfil individual XDM** referência.


Como o XDM é a linguagem que impulsiona os negócios da experiência, o XDM também é a base para o construtor de público-alvo. Todos os dados assimilados na Platform devem ser mapeados em relação ao XDM e, como tal, todos os dados se tornam parte do mesmo modelo de dados, independentemente de onde esses dados vêm. Isso oferece uma grande vantagem ao criar públicos-alvo, como nessa interface única do construtor de públicos-alvo, é possível combinar dados de qualquer origem no mesmo fluxo de trabalho. Os públicos-alvo criados no Audience Builder podem ser enviados para soluções como Adobe Target, Adobe Campaign ou qualquer outro canal de ativação.

Agora é necessário criar um público-alvo de todos os clientes que visualizaram o produto **Real-Time CDP**.

Para criar esse público-alvo, é necessário adicionar um Evento de experiência. Você pode encontrar todos os Eventos de experiência clicando no link **Eventos** ícone no **Campos** barra de menus.

![Segmentação](./images/findee.png)

Em seguida, você verá o nível superior, **XDM ExperienceEvents** nó. Clique em **XDM ExperienceEvent**.

![Segmentação](./images/see.png)

Ir para **Itens da lista de produtos**.

![Segmentação](./images/plitems.png)

Selecionar **Nome** e arraste e solte o **Nome** do menu esquerdo para a tela do audience builder na janela **Eventos** seção. Você verá isto:

![Segmentação](./images/eewebpdtlname.png)

O parâmetro de comparação deve ser **igual a** e, no campo de entrada, digite **Real-time CDP**.

![Segmentação](./images/pv.png)

Toda vez que você adiciona um elemento ao construtor de público-alvo, pode clicar no **Atualizar Estimativa** para obter uma nova estimativa da população no seu público-alvo.

![Segmentação](./images/refreshest.png)

Como **Método de avaliação**, selecione **Edge**.

![Segmentação](./images/evedge.png)

Por fim, vamos dar um nome ao seu público e salvá-lo.

Como convenção de nomenclatura, use:

- `yourLastName - Interest in Real-Time CDP`

Em seguida, clique no link **Salvar e fechar** botão para salvar o público-alvo.

![Segmentação](./images/segmentname.png)

Você será redirecionado para a página de visão geral do público-alvo agora, onde verá uma pré-visualização de exemplo dos perfis do cliente qualificados para o seu público-alvo.

![Segmentação](./images/savedsegment.png)

Agora você pode continuar com o próximo exercício e usar seu público com o Adobe Target.

Próxima etapa: [1.4 Ação: enviar o público-alvo para a Adobe Target](./ex4.md)

[Voltar para Fluxo de Usuário 1](./uc1.md)

[Voltar a todos os módulos](../../overview.md)


[def]: ./images/segmentationpopup.png
