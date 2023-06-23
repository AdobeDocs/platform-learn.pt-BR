---
title: Estruturação dos dados
description: Estruturação dos dados
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: d300429a-5a66-4b61-97cb-b934fc8e8291
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Estruturação dos dados

As empresas têm sua própria linguagem para se comunicar sobre seus domínios. As concessionárias de automóveis lidam com marcas, modelos e cilindros. As companhias aéreas lidam com números de voo, classe de serviço e atribuições de assentos. Alguns desses termos são exclusivos de uma empresa específica, alguns são compartilhados entre um setor vertical e alguns são compartilhados por quase todas as empresas. Para termos que são compartilhados entre um setor vertical ou mesmo mais amplo, você pode começar a fazer coisas poderosas com seus dados ao nomear e estruturar esses termos de uma maneira comum.

Por exemplo, muitas empresas lidam com pedidos. E se coletivamente essas empresas decidissem modelar um pedido de maneira semelhante. Por exemplo, e se o modelo de dados consistisse em um objeto com uma `priceTotal` propriedade que representava o preço total do pedido. E se esse objeto também tiver propriedades chamadas? `currencyCode` e `purchaseOrderNumber`. Talvez o objeto da ordem contenha uma propriedade chamada `payments` que seria uma matriz de objetos de pagamento. Cada objeto representaria um pagamento para o pedido. Por exemplo, talvez um cliente tenha pago parte do pedido com um cartão-presente e pago o restante usando um cartão de crédito. Você pode começar a construir um modelo com esta aparência:

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

Se todas as empresas que lidam com pedidos decidissem modelar seus dados de pedidos de maneira consistente para termos comuns no setor, coisas mágicas poderiam começar a acontecer. As informações poderiam ser trocadas de forma mais fluida dentro e fora da organização, em vez de interpretar e traduzir constantemente os dados (props e evars, alguém?). O aprendizado de máquina poderia entender mais facilmente o que seus dados _significa_ e fornecer insights acionáveis. As interfaces do usuário para encontrar dados relevantes podem se tornar mais intuitivas. Seus dados podem ser perfeitamente integrados a parceiros e fornecedores que estejam seguindo a mesma modelagem.

## XDM

Esse é o objetivo do Adobe [Experience Data Model](https://business.adobe.com/products/experience-platform/experience-data-model.html). O XDM fornece modelagem prescritiva para dados comuns no setor, além de permitir estender o modelo para suas necessidades específicas. O Adobe Experience Platform é construído com base no XDM e, como tal, os dados enviados para o Experience Platform precisarão estar no XDM. Em vez de pensar em onde e como você pode transformar seus modelos de dados atuais em XDM antes de enviar os dados para o Experience Platform, considere adotar o XDM de forma mais abrangente em toda a organização para que a tradução raramente precise ocorrer.
