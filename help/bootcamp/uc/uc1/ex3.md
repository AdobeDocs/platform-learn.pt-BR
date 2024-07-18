---
title: Bootcamp - Perfil do cliente em tempo real - Criar um público-alvo - Interface do usuário
description: Bootcamp - Perfil do cliente em tempo real - Criar um público-alvo - Interface do usuário
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Audiences
exl-id: 37d4a5e8-e2bc-4c8c-a74f-09f74ea79962
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 3%

---

# 1.3 Criar um público-alvo - Interface do usuário

Neste exercício, você criará um público-alvo usando o Audience Builder da Adobe Experience Platform.

## Story

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``Bootcamp``. Você pode fazer isso clicando no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. Depois de selecionar a [!UICONTROL sandbox] apropriada, você verá a alteração da tela e agora estará na [!UICONTROL sandbox] dedicada.

![Assimilação de dados](./images/sb1.png)

No menu no lado esquerdo, vá para **Públicos-alvo**. Nesta página, você verá Painéis com informações essenciais sobre o desempenho do **Público**.

![Segmentação](./images/menuseg.png)

Clique em **Procurar** para ter uma visão geral de todos os públicos existentes. Clique no botão **+ Criar público-alvo** para começar a criar um novo público-alvo.


![Segmentação](./images/segmentationui.png)

Será exibido um Pop-Ip perguntando se você deseja **&#39;Compor público-alvo&#39;** ou **&#39;Criar regra&#39;**. Escolha a **&#39;Regra de compilação&#39;** para continuar e clique em **criar**.

![Segmentação][def]

Quando estiver no construtor de público-alvo, você notará imediatamente a opção de menu **Atributos** e a referência ao **Perfil individual XDM**.


Como o XDM é a linguagem que impulsiona os negócios da experiência, o XDM também é a base para o construtor de público-alvo. Todos os dados assimilados na Platform devem ser mapeados em relação ao XDM e, como tal, todos os dados se tornam parte do mesmo modelo de dados, independentemente de onde esses dados vêm. Isso oferece uma grande vantagem ao criar públicos-alvo, como nessa interface única do construtor de públicos-alvo, é possível combinar dados de qualquer origem no mesmo fluxo de trabalho. Os públicos-alvo criados no Audience Builder podem ser enviados para soluções como Adobe Target, Adobe Campaign ou qualquer outro canal de ativação.

Agora é necessário criar uma audiência de todos os clientes que visualizaram o produto **Real-Time CDP**.

Para criar esse público-alvo, é necessário adicionar um Evento de experiência. Você pode encontrar todos os Eventos de Experiência clicando no ícone **Eventos** na barra de menus **Campos**.

![Segmentação](./images/findee.png)

Em seguida, você verá o nó **XDM ExperienceEvents** de nível superior. Clique em **XDM ExperienceEvent**.

![Segmentação](./images/see.png)

Vá para **Itens da Lista de Produtos**.

![Segmentação](./images/plitems.png)

Selecione **Nome** e arraste e solte o objeto **Nome** do menu esquerdo na tela do construtor de públicos-alvo na seção **Eventos**. Você verá isto:

![Segmentação](./images/eewebpdtlname.png)

O parâmetro de comparação deve ser **igual a** e, no campo de entrada, insira **CDP em tempo real**.

![Segmentação](./images/pv.png)

Toda vez que você adiciona um elemento ao construtor de público-alvo, você pode clicar no botão **Atualizar estimativa** para obter uma nova estimativa da população do público-alvo.

![Segmentação](./images/refreshest.png)

Como **Método de Avaliação**, selecione **Edge**.

![Segmentação](./images/evedge.png)

Por fim, vamos dar um nome ao seu público e salvá-lo.

Como convenção de nomenclatura, use:

- `yourLastName - Interest in Real-Time CDP`

Em seguida, clique no botão **Salvar e fechar** para salvar seu público-alvo.

![Segmentação](./images/segmentname.png)

Você será redirecionado para a página de visão geral do público-alvo agora, onde verá uma pré-visualização de exemplo dos perfis do cliente qualificados para o seu público-alvo.

![Segmentação](./images/savedsegment.png)

Agora você pode continuar com o próximo exercício e usar seu público com o Adobe Target.

Próxima etapa: [1.4 Executar Ação: enviar seu público-alvo para a Adobe Target](./ex4.md)

[Voltar para Fluxo de Usuário 1](./uc1.md)

[Voltar a todos os módulos](../../overview.md)


[def]: ./images/segmentationpopup.png
