---
title: Criar um esquema
description: Criar um esquema
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 25d77367-046d-46bd-9640-60fbcea263da
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 3%

---

# Criar um esquema

Conforme discutido no [Estruturação de dados](../structuring-your-data.md), os dados enviados para a Adobe Experience Platform devem estar no XDM. Mais especificamente, seus dados devem corresponder a um _schema_. Um esquema é basicamente uma descrição de como os dados devem ser. Ela descreve os nomes dos campos e onde eles devem estar localizados nos dados. Ela também descreve o tipo de valor que cada campo deve ter (por exemplo, um booleano, uma string com 12 caracteres de comprimento, uma matriz de números).

O Adobe Experience Platform fornece alguns blocos componentes prontos para uso, conhecidos como grupos de campo, que são comuns no setor. Por exemplo, para o setor dos serviços financeiros, existem grupos de campos para transferências de saldos e pedidos de empréstimos. Para o setor de viagens e hospitalidade, há grupos de campo para voos e reservas de alojamento.

Recomendamos usar os grupos de campos incorporados, sempre que possível, ao criar o esquema. Também entendemos que você pode precisar de campos específicos da sua empresa. Por isso, você pode criar seus próprios grupos de campos personalizados para usar nos esquemas criados.

Vamos analisar a criação de um esquema para um site de comércio eletrônico típico.

Primeiro, navegue até o [!UICONTROL Esquemas] visualização dentro do Adobe Experience Platform.

![Exibição de esquemas](../../../assets/implementation-strategy/schemas-view.png)

Selecionar [!UICONTROL Criar esquema] no canto superior direito. Um menu é exibido. Selecionar [!UICONTROL ExperiênciaEvento XDM].

Nesse ponto, uma caixa de diálogo deve ser exibida perguntando quais grupos de campos você deseja adicionar ao esquema. O primeiro grupo de campos que você deve selecionar é o grupo de campos chamado [!UICONTROL AEP Web SDK ExperienceEvent]. Esse grupo de campos adiciona um conjunto de campos que acomoda dados coletados automaticamente pelo SDK da Web da Adobe Experience Platform.

![Mistura de SDK da Web da AEP](../../../assets/implementation-strategy/aep-web-sdk-mixin.png)

Como o site deste tutorial é um site de comércio eletrônico, você também deve selecionar a variável [!UICONTROL Detalhes de comércio] grupo de campos. Esse grupo permite enviar dados de comércio típicos como quais produtos estão sendo visualizados, adicionados ao carrinho e comprados.

![Mistura de detalhes do comércio](../../../assets/implementation-strategy/commerce-details-mixin.png)

Clique no botão [!UICONTROL Adicionar grupos de campos] na parte superior direita da caixa de diálogo. Nesse ponto, você deve ver a estrutura do esquema.

![Schema com mixins](../../../assets/implementation-strategy/schema-with-mixins.png)

Os grupos de campos adicionados estão listados à esquerda. Selecionar um grupo de campos destaca os campos à direita fornecidos por esse grupo de campos. Reserve um momento para explorar os campos disponíveis.

Finalmente, selecione [!UICONTROL Esquema sem título] à esquerda da tela, forneça um nome e uma descrição à direita da tela e clique em [!UICONTROL Salvar].

![Esquema com nome e descrição](../../../assets/implementation-strategy/schema-name-description.png)

Seu esquema foi criado. Em seguida, vamos aprender como criar um conjunto de dados para manter seus dados.

Para obter mais informações sobre como criar schemas, consulte [Criar um esquema (interface do usuário)](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=pt-BR).
