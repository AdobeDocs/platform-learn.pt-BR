---
title: Coleta de dados do Adobe Experience Platform e encaminhamento pelo lado do evento em tempo real - Criar uma propriedade de encaminhamento do evento de coleta de dados do Adobe Experience Platform
description: Criar uma propriedade de Encaminhamento de evento de coleta de dados do Adobe Experience Platform
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 2ca908a3-28b9-48d4-b96e-00951de530ba
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 2%

---

# 14.1 Criar uma propriedade de Encaminhamento de evento de coleta de dados do Adobe Experience Platform

>[!NOTE]
>
>A extensão para dispositivos móveis do Adobe Experience Platform Edge está atualmente em BETA. O uso desta extensão é somente por convite. Entre em contato com o Gerente de sucesso do cliente do Adobe para saber mais e obter acesso aos materiais deste tutorial.

## 14.1.1 O que é uma propriedade de Encaminhamento de evento de coleta de dados do Adobe Experience Platform?

Normalmente, quando os dados são coletados usando a Coleta de dados do Adobe Experience Platform, eles são coletados na variável **Lado do cliente**. O **Lado do cliente** é um ambiente como um site ou um aplicativo móvel. No Módulo 0 e no Módulo 1, a configuração de uma propriedade do cliente de coleta de dados da Adobe Experience Platform foi discutida em profundidade e você implementou a propriedade do cliente de coleta de dados da Adobe Experience Platform em seu site e aplicativo móvel, para que os dados pudessem ser coletados lá quando um cliente interagia com o site e o aplicativo móvel.

Quando esses dados de interação são coletados pela propriedade Cliente da coleta de dados do Adobe Experience Platform, uma solicitação é enviada pelo site ou aplicativo móvel ao Adobe Edge. O Edge é o ambiente de coleta de dados de entrada do Adobe e é o ponto de entrada para dados de sequência de cliques no ecossistema do Adobe. A partir do Edge, os dados coletados são enviados para aplicativos como Adobe Experience Platform, Adobe Analytics, Adobe Audience Manager ou Adobe Target.

Com a adição de uma propriedade Adobe Experience Platform Data Collection Event Forwarding , agora é possível configurar uma propriedade Adobe Experience Platform Data Collection que escuta os dados recebidos no Edge. Quando a propriedade Adobe Experience Platform Data Collection Event Forwarding que está sendo executada no Edge vê os dados recebidos, ela tem a capacidade de usar esses dados e encaminhá-los para outro lugar. Que em outro lugar também pode ser um webhook externo não-Adobe, o que possibilita enviar esses dados para, por exemplo, seu lago de dados preferido, um aplicativo de decisão ou qualquer outro aplicativo que tenha a capacidade de abrir um webhook.

A configuração de uma propriedade do Adobe Experience Platform Data Collection Event Forwarding parece familiar a uma propriedade do cliente, com a capacidade de configurar elementos de dados e regras da mesma forma como no passado com as propriedades do Adobe Experience Platform Data Collection Client . No entanto, a maneira como os dados serão acessados e usados será um pouco diferente, dependendo do caso de uso.

Vamos começar criando a propriedade Adobe Experience Platform Data Collection Event Forwarding .

## 14.1.2 Criar uma propriedade de Encaminhamento de evento de coleta de dados do Adobe Experience Platform

Ir para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). No menu esquerdo, clique em **Encaminhamento de evento**. Em seguida, você verá uma visão geral de todas as propriedades disponíveis do Adobe Experience Platform Data Collection Event Forwarding. Clique no botão **Nova propriedade.**

![Coleta de dados do Adobe Experience Platform SSF](./images/launchhome.png)

Agora é necessário inserir um nome para a propriedade Adobe Experience Platform Data Collection Event Forwarding . Como convenção de nomenclatura, use `--demoProfileLdap-- - Demo System (DD/MM/YYYY) (Edge)`. Por exemplo, neste exemplo, o nome é **vangeluw - Demo System (22/02/2022) (Edge)**. Clique em **Salvar**.

![Coleta de dados do Adobe Experience Platform SSF](./images/ssf1.png)

Você estará de volta à lista de propriedades do Adobe Experience Platform Data Collection Event Forwarding. Clique em para abrir a propriedade que você acabou de criar.

![Coleta de dados do Adobe Experience Platform SSF](./images/ssf2.png)

## 14.1.2 Configurar a extensão do conector do Adobe Cloud

No menu esquerdo, acesse **Extensões**. Você verá que a variável **Núcleo** A extensão do já está configurada.

![Coleta de dados do Adobe Experience Platform SSF](./images/ssf3.png)

Ir para **Catálogo**. Você verá o **Conector da nuvem do Adobe** extensão. Clique em **Instalar** para instalá-lo.

![Coleta de dados do Adobe Experience Platform SSF](./images/ssf4.png)

A extensão será adicionada. Não há configuração para fazer nesta etapa. Você será enviado de volta para a visão geral das extensões instaladas.

![Coleta de dados do Adobe Experience Platform SSF](./images/ssf5.png)

## 14.1.3 Implantar sua propriedade de Encaminhamento do evento de coleta de dados do Adobe Experience Platform

No menu esquerdo, acesse **Fluxo de publicação**. Clique em **Adicionar biblioteca**.

![Coleta de dados do Adobe Experience Platform SSF](./images/ssf6.png)

Insira o nome **Principal**, selecione o ambiente **Desenvolvimento (desenvolvimento)** e clique em **+ Adicionar todos os recursos alterados**.

![Coleta de dados do Adobe Experience Platform SSF](./images/ssf7.png)

Você verá isso. Clique em **Salvar e criar para desenvolvimento**.

![Coleta de dados do Adobe Experience Platform SSF](./images/ssf8.png)

Sua biblioteca será criada, o que pode levar de 1 a 2 minutos.

![Coleta de dados do Adobe Experience Platform SSF](./images/ssf9.png)

Por fim, sua biblioteca será criada e pronta.

![Coleta de dados do Adobe Experience Platform SSF](./images/ssf10.png)

Próxima etapa: [14.2 Atualize seu conjunto de dados para disponibilizar os dados para sua propriedade de Encaminhamento de eventos da coleta de dados](./ex2.md)

[Voltar ao Módulo 14](./aep-data-collection-ssf.md)

[Voltar para todos os módulos](./../../overview.md)
