---
title: Estruturação de dados
description: Estruturação de dados
exl-id: 8d176389-25a4-4718-afff-efd2f87204ed
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# Estruturação de dados

As empresas têm a sua própria linguagem para comunicar sobre o seu domínio. As concessionárias de carros lidam com marcas, modelos e cilindros. As companhias aéreas lidam com números de voo, classe de serviço e atribuições de lugares. Alguns desses termos são exclusivos de uma empresa específica, alguns são compartilhados entre um negócio vertical e alguns são compartilhados por quase todas as empresas. Para termos que são compartilhados entre um negócio vertical ou ainda mais amplo, você pode começar a fazer coisas poderosas com seus dados ao nomear e estruturar esses termos de uma maneira comum.

Por exemplo, muitas empresas lidam com pedidos. E se, coletivamente, essas empresas decidissem modelar um pedido de maneira semelhante? Por exemplo, e se o modelo de dados consistisse de um objeto com um `priceTotal` propriedade que representava o preço total do pedido? E se esse objeto também tivesse propriedades nomeadas `currencyCode` e `purchaseOrderNumber`? Talvez o objeto do pedido contenha uma propriedade chamada `payments` seria uma matriz de objetos de pagamento. Cada objeto representaria um pagamento para a ordem. Por exemplo, talvez um cliente tenha pago parte do pedido com um cartão-presente e o restante com um cartão de crédito. Você pode começar a construir um modelo que se pareça com isto:

```json
{
  "order": {
    "priceTotal": 89.50,
    "currencyCode": "EUR",
    "purchaseOrderNumber": "JWN20192388410012",
    "payments": [
      {
        "paymentType": "gift_card",
        "paymentAmount": 50
      },
      {
        "paymentType": "credit_card",
        "paymentAmount": 39.50
      }
    ]
  }
}
```

Se todas as empresas que lidam com pedidos decidissem modelar seus dados de pedido de maneira consistente para termos que são comuns no setor, coisas mágicas poderiam começar a acontecer. As informações poderiam ser trocadas de forma mais fluida dentro e fora da sua organização, em vez de interpretar e traduzir constantemente os dados (props e evars, qualquer um?). O aprendizado de máquina poderia entender mais facilmente quais dados _meios_ e fornecer insights acionáveis. As interfaces do usuário para surfar dados relevantes podem se tornar mais intuitivas. Seus dados podem ser perfeitamente integrados a parceiros e fornecedores que seguem a mesma modelagem.

## XDM

Este é o objetivo do Adobe [Experience Data Model](https://business.adobe.com/products/experience-platform/experience-data-model.html). O XDM fornece modelagem normativa para dados comuns no setor, além de permitir que você estenda o modelo para suas necessidades específicas. A Adobe Experience Platform é criada em torno do XDM e, como tal, os dados enviados para o Experience Platform precisam estar no XDM. Em vez de pensar em onde e como você pode transformar seus modelos de dados atuais em XDM antes de enviar os dados para o Experience Platform, considere adotar o XDM de forma mais abrangente em sua organização para que a tradução raramente precise ocorrer.

[Próximo: ](configure-the-server/create-a-schema.md)

>[!NOTE]
>
>Obrigado por investir seu tempo para aprender sobre a coleta de dados. Em caso de dúvidas, desejo compartilhar comentários gerais ou ter sugestões sobre conteúdo futuro, compartilhe-as sobre isso [Posto de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
