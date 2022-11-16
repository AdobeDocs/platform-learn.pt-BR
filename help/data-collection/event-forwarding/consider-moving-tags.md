---
title: Considere mover as tags de fornecedor para o encaminhamento de eventos
description: Saiba como avaliar uma tag de fornecedor do lado do cliente para distribuição de dados do lado do servidor.
feature: Event Forwarding, Tags, Integrations
solution: Data Collection
kt: 9921
level: Intermediate, Experienced
role: Admin, Developer, Architect
exl-id: f8fd351a-435c-4cc1-b987-ed2ead20d4d6
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 3%

---

# Pense em mover as tags de fornecedor do lado do cliente para o encaminhamento de eventos

Há vários motivos convincentes para considerar a mudança de tags de fornecedores do lado do cliente para fora de navegadores e dispositivos, e para um servidor. Neste artigo, discutimos como avaliar uma tag de fornecedor do lado do cliente para possivelmente movê-la para uma propriedade de encaminhamento de evento.

Essa avaliação só é necessária se você estiver considerando remover uma tag do fornecedor do lado do cliente e substituí-la pela distribuição de dados do lado do servidor em uma propriedade de encaminhamento de evento. Este artigo pressupõe que você esteja familiarizado com as noções básicas do [coleta de dados](https://experienceleague.adobe.com/docs/data-collection.html)e [encaminhamento de eventos](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html).

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) para obter uma referência consolidada das alterações de terminologia.

Os fornecedores de navegador estão alterando a forma como tratam cookies de terceiros. Fornecedores e tecnologias de publicidade e marketing geralmente exigem o uso de muitas tags do lado do cliente. Esses desafios são apenas dois motivos convincentes para os clientes adicionarem a distribuição de dados do lado do servidor.

>[!NOTE]
>
>`Tag` neste artigo significa código do lado do cliente, normalmente JavaScript de um fornecedor usado para coleta de dados no navegador ou dispositivo, enquanto um visitante interage com o site ou aplicativo. `Website` ou `site` aqui se refere a um site, um aplicativo da Web ou um aplicativo para um dispositivo móvel. Uma &quot;tag&quot; para esses fins também é frequentemente chamada de pixel.

## Casos de uso e dados {#use-cases-data}

A primeira etapa é definir os casos de uso implementados com a tag de fornecedor do lado do cliente. Por exemplo, considere o pixel do Facebook (Meta). Movimentação de nosso site para o [API de conversões do facebook](https://exchange.adobe.com/apps/ec/105509/facebook-conversions-api-extension) com a extensão de encaminhamento de evento significa documentar os casos de uso específicos primeiro.

Para o código de fornecedor atual do lado do cliente:

- Qual evento específico e outros pontos de dados são expostos e passados para a tag do lado do cliente?
- Quando e onde essa transferência de dados acontece?

É útil fazer uma lista, planilha, diagrama ou outro registro dos dados e da sequência de eventos para documentar essa avaliação, mesmo que seja somente para seu próprio uso. Certifique-se de incluir rótulos para fontes de dados — de onde ele vem? Destinos — para onde vai? E transformações — o que acontece com ele entre origem e destino?

Em nosso exemplo, estamos rastreando conversões com o pixel do Facebook quando os visitantes interagem com nosso site após visualizar um anúncio do Facebook. Eles também podem interagir com nosso site após visualizar anúncios relacionados em outra plataforma social. Para ver essas conversões nas ferramentas e relatórios de publicidade do Facebook, os dados necessários devem chegar ao Facebook. Esses dados podem incluir eventos de conversão como downloads, registros, curtidas ou compras.

### Dados {#data}

Com a tag existente no lado do cliente, quando ela é executada ou executada em nosso site, o que acontece com os dados do nosso caso de uso? Podemos capturar os dados de que precisamos no cliente, sem a tag do fornecedor, para que possamos enviá-los para o encaminhamento do evento? Ao usar [tags](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html) Para outros sistemas de gerenciamento de tags, a maioria dos dados de interação do visitante está disponível para coleta e distribuição. Mas os dados de que precisamos para nosso caso de uso estão disponíveis quando precisamos, onde precisamos e no formato necessário, sem a tag do fornecedor do cliente? Aqui estão algumas outras questões de dados a serem consideradas:

- Existe uma ID de usuário de fornecedor necessária para cada evento?
- Em caso afirmativo, como é possível coletá-lo ou gerá-lo sem a tag do lado do cliente?
- O fornecedor precisa especificamente de seu código do lado do cliente no tempo de execução?
- Que outros dados são necessários? De onde virão esses dados?

A maioria das tags de fornecedores do lado do cliente não requer muitos pontos de dados para qualquer caso de uso específico, mas é útil observar os casos de uso e os dados necessários durante essas avaliações.

## APIs do fornecedor {#vendor-apis}

Agora sabemos os casos de uso específicos a serem implementados, os dados necessários e a sequência de eventos da origem para o destino. Para determinar se o caso de uso é adequado para o encaminhamento do evento, agora podemos investigar os detalhes da API do fornecedor.

>[!IMPORTANT]
>
>Embora muitos fornecedores estejam habilitando APIs para transferência de servidor para servidor, também há muitos que atualmente não têm APIs adequadas para esses propósitos.

### Investigando APIs {#investigate-apis}

Estas são algumas etapas que podemos tomar para investigar endpoints de API do fornecedor.

O fornecedor tem APIs projetadas para transferência de dados de eventos de servidor para servidor? Primeiro, encontre os requisitos para esses pontos de extremidade de API específicos:

- Os endpoints da API existem para enviar os dados necessários? Para encontrar os endpoints que suportam seus casos de uso, consulte a documentação do desenvolvedor ou da API do fornecedor.
- Eles permitem dados de evento de fluxo ou apenas dados em lote?
- Quais métodos de autenticação eles suportam? Token, HTTP, versão de credenciais de cliente OAuth ou outro? Consulte [here](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) para métodos compatíveis com o encaminhamento de eventos.
- Qual é o deslocamento de atualização de sua API? Essa limitação é compatível com os mínimos de encaminhamento de eventos? Detalhes [here](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html#:~:text=you%20can%20configure%20the%20Refresh%20Offset%20value%20for%20the%20secret).
- Quais dados eles exigem para os endpoints relevantes?
- Eles exigem um identificador de usuário específico do fornecedor com cada chamada para o endpoint?
- Se eles exigirem esse identificador, onde e como ele pode ser gerado ou capturado, sem código do lado do cliente?

Por outras palavras:

- O fornecedor fornece os pontos de extremidade da API necessários para nossos casos de uso?
- Eles têm um método de autenticação compatível para o encaminhamento de eventos?
- Podemos acessar todos os dados necessários para uma implementação de encaminhamento de evento (do lado do cliente ou de outras chamadas de API)?

A tag provavelmente é uma boa candidata para migrar do cliente para nossos servidores em uma propriedade de encaminhamento de evento se pudermos responder sim a essas perguntas.

Se o fornecedor não tiver os pontos de extremidade da API para suportar nossos casos de uso, obviamente essa tag do fornecedor não é uma boa candidata para usar o encaminhamento de eventos no lugar da tag do fornecedor do lado do cliente.

E se elas tiverem APIs, mas também exigirem alguma ID de visitante ou usuário exclusiva com cada chamada de API? Como podemos acessar essa ID se não tivermos o código do lado do cliente do fornecedor (tag) em execução no site?

Alguns fornecedores estão mudando seus sistemas para o novo mundo sem cookies de terceiros. Essas alterações incluem o uso de identificadores exclusivos alternativos, como um [UUID](https://developer.mozilla.org/en-US/docs/Glossary/UUID) ou outro [ID gerada pelo cliente](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html). Se o fornecedor permitir uma ID gerada pelo cliente, podemos enviá-la do cliente para a Rede de borda da plataforma com SDK da Web ou móvel, ou possivelmente obtê-la de uma chamada de API no encaminhamento de eventos. Quando enviamos dados para esse fornecedor em uma regra de encaminhamento de evento, incluímos esse identificador conforme necessário.

Se o fornecedor exigir dados (como uma ID exclusiva específica do fornecedor, por exemplo) que só possam ser gerados ou acessados por sua própria tag do cliente, essa tag do fornecedor provavelmente não é uma boa candidata para se mover. _Não é recomendável tentar fazer a engenharia reversa de uma tag do lado do cliente com a ideia de mover essa coleta de dados para o encaminhamento de eventos sem as APIs apropriadas._

O [Conector da Adobe Experience Platform Cloud](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/cloud-connector/overview.html) A extensão pode fazer solicitações HTTP conforme necessário com fornecedores que têm as APIs apropriadas para transferência de dados de eventos de servidor para servidor. Embora seja interessante ter extensões específicas do fornecedor e mais extensões estejam em desenvolvimento ativo no momento, podemos implementar regras de encaminhamento de eventos hoje usando a extensão Conector da nuvem, sem esperar por extensões adicionais do fornecedor.

## Ferramentas {#tools}

Investigar e testar endpoints de API do fornecedor é mais fácil com ferramentas como [Postman](https://www.postman.com/)ou extensões do editor de texto como o Visual Studio Code [Cliente Thunder](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client)ou [Cliente HTTP](https://marketplace.visualstudio.com/items?itemName=mkloubert.vscode-http-client).

## Próximas etapas {#next-steps}

Este artigo forneceu uma sequência de etapas para avaliar uma tag do lado do cliente do fornecedor e possivelmente movê-la do lado do servidor em uma propriedade de encaminhamento de eventos. Para obter mais informações sobre tópicos relacionados, consulte estes links:

- [Gerenciamento de tags](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html) no Adobe Experience Platform
- [Encaminhamento de evento](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html) para processamento no servidor
- [Atualizações de terminologia](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) na coleta de dados
