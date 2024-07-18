---
title: Pense em mover as tags de fornecedor para o encaminhamento de eventos
description: Saiba como avaliar uma tag de fornecedor do lado do cliente para distribuição de dados do lado do servidor.
feature: Event Forwarding, Tags, Integrations
role: Admin, Developer, Architect, Data Engineer
level: Intermediate, Experienced
jira: KT-9921
exl-id: f8fd351a-435c-4cc1-b987-ed2ead20d4d6
source-git-commit: 7edf8fc46943ae2f1e6e2e20f4d589d7959310c8
workflow-type: tm+mt
source-wordcount: '1279'
ht-degree: 2%

---

# Pense em mover as tags de fornecedor do lado do cliente para o encaminhamento de eventos

Há vários motivos convincentes para considerar a mudança das tags de fornecedor do lado do cliente dos navegadores e dispositivos para um servidor. Neste artigo, discutimos como avaliar uma tag de fornecedor do lado do cliente para a possibilidade de movê-la para uma propriedade de encaminhamento de eventos.

Essa avaliação só será necessária se você estiver considerando remover uma tag de fornecedor do lado do cliente e substituí-la pela distribuição de dados do lado do servidor em uma propriedade de encaminhamento de eventos. Este artigo supõe que você esteja familiarizado com as noções básicas da [coleta de dados](https://experienceleague.adobe.com/docs/data-collection.html) e do [encaminhamento de eventos](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html).

>[!NOTE]
>
>O Adobe Experience Platform Launch foi reformulado como um conjunto de tecnologias de coleção de dados na Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) para obter uma referência consolidada das alterações de terminologia.

Os fornecedores de navegador estão alterando a maneira como tratam cookies de terceiros. Fornecedores e tecnologias de Advertising e marketing geralmente exigem o uso de muitas tags do lado do cliente. Esses desafios são apenas dois motivos convincentes pelos quais nossos clientes estão adicionando distribuição de dados do lado do servidor.

>[!NOTE]
>
>`Tag` neste artigo significa código do lado do cliente, normalmente JavaScript de um fornecedor usado para coleta de dados no navegador ou dispositivo enquanto um visitante interage com o site ou aplicativo. `Website` ou `site` aqui refere-se a um site, um aplicativo Web ou um aplicativo para um dispositivo móvel. Uma &quot;tag&quot; para esses propósitos também é frequentemente chamada de pixel.

## Casos de uso e dados {#use-cases-data}

A primeira etapa é definir os casos de uso implementados com a tag de fornecedor do lado do cliente. Por exemplo, considere o pixel (Meta) do Facebook. Movê-lo do nosso site para a [API de Meta Conversões](https://exchange.adobe.com/apps/ec/109168/meta-conversions-api) com a extensão de encaminhamento de eventos significa documentar os casos de uso específicos primeiro.

Para o código de fornecedor atual do lado do cliente:

- Que evento específico e outros pontos de dados são expostos e passados para a tag do lado do cliente?
- Quando e onde ocorre essa transferência de dados?

É útil fazer uma lista, planilha, diagrama ou outro registro dos dados e da sequência de eventos para documentar essa avaliação, mesmo que seja apenas para seu próprio uso. Certifique-se de incluir rótulos para fontes de dados — de onde eles são provenientes? Destinos - para onde vai? E transformações — o que acontece entre a origem e o destino?

Em nosso exemplo, estamos rastreando conversões com o pixel do Facebook quando os visitantes interagem com nosso site após visualizar um anúncio do Facebook. Eles também podem interagir com nosso site depois de visualizar anúncios relacionados em outra plataforma social. Para ver essas conversões nas ferramentas e nos relatórios de publicidade do Facebook, os dados necessários devem chegar ao Facebook. Esses dados podem incluir eventos de conversão, como downloads, registros, curtidas ou compras.

### Dados {#data}

Com a tag existente do lado do cliente, quando ela é executada ou executada em nosso site, o que acontece com os dados do nosso caso de uso? Podemos capturar os dados necessários no cliente, sem a tag do fornecedor, para que possamos enviá-los para o encaminhamento de eventos? Ao usar [tags](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR) ou outros sistemas de gerenciamento de tags, a maioria dos dados de interação do visitante está disponível para coleta e distribuição. Mas os dados necessários para nosso caso de uso estão disponíveis quando e onde precisamos deles, no formato necessário, sem a etiqueta do fornecedor do lado do cliente? Estas são algumas perguntas adicionais sobre dados a serem consideradas:

- Há uma ID de usuário fornecedor necessária para cada evento?
- Em caso afirmativo, como ele pode ser coletado ou gerado sem a tag do lado do cliente?
- O fornecedor exige especificamente o código do lado do cliente no tempo de execução?
- Quais outros dados são necessários? De onde virão esses dados?

A maioria das tags de fornecedores do lado do cliente não requer muitos pontos de dados para nenhum caso de uso específico, mas é útil observar os casos de uso e os dados necessários durante essas avaliações.

## APIs do fornecedor {#vendor-apis}

Agora sabemos os casos de uso específicos a serem implementados, os dados necessários e a sequência de eventos da origem ao destino. Para determinar se o caso de uso é adequado para o encaminhamento de eventos, agora podemos investigar os detalhes da API do fornecedor.

>[!IMPORTANT]
>
>Embora muitos fornecedores estejam ativando APIs para transferência de servidor para servidor, no momento, também há muitos que não têm APIs adequadas para essas finalidades.

### Investigação de APIs {#investigate-apis}

Estas são algumas etapas que podemos seguir para investigar os pontos de acesso da API do fornecedor.

O fornecedor tem APIs projetadas para transferência de dados de eventos de servidor para servidor? Primeiro, encontre os requisitos para esses endpoints de API específicos:

- Os endpoints da API existem para enviar os dados necessários? Para encontrar os endpoints compatíveis com seus casos de uso, consulte a documentação do desenvolvedor ou da API do fornecedor.
- Eles permitem a transmissão de dados do evento ou somente de dados em lote?
- A quais métodos de autenticação eles dão suporte? Token, HTTP, versão de credenciais de cliente OAuth ou outro? Consulte [aqui](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) para obter os métodos compatíveis com o encaminhamento de eventos.
- Qual é o deslocamento de atualização da API? Essa limitação é compatível com os mínimos de encaminhamento de eventos? Detalhes [aqui](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html#:~:text=you%20can%20configure%20the%20Refresh%20Offset%20value%20for%20the%20secret).
- Quais dados são necessários para os endpoints relevantes?
- Eles exigem um identificador de usuário específico do fornecedor com cada chamada para o endpoint?
- Se eles exigirem esse identificador, onde e como ele pode ser gerado ou capturado, sem o código do lado do cliente?

Em outras palavras:

- O fornecedor fornece os endpoints de API necessários para nossos casos de uso?
- Eles têm um método de autenticação compatível para o encaminhamento de eventos?
- É possível acessar todos os dados necessários para uma implementação do encaminhamento de eventos (do lado do cliente ou de outras chamadas de API)?

A tag provavelmente é uma boa candidata para migrar do cliente para nossos servidores em uma propriedade de encaminhamento de eventos se pudermos responder sim a essas perguntas.

Se o fornecedor não tiver os endpoints de API para dar suporte a nossos casos de uso, é óbvio que a tag do fornecedor não é uma boa candidata para usar o encaminhamento de eventos no lugar da tag do fornecedor do lado do cliente.

E se eles tiverem APIs, mas também exigirem algum visitante único ou ID de usuário em cada chamada de API? Como podemos acessar essa ID se não tivermos o código do lado do cliente do fornecedor (tag) em execução no site?

Alguns fornecedores estão alterando seus sistemas para o novo mundo sem cookies de terceiros. Essas alterações incluem o uso de identificadores exclusivos alternativos, como uma [UUID](https://developer.mozilla.org/en-US/docs/Glossary/UUID) ou outra [ID gerada pelo cliente](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html). Se o fornecedor permitir uma ID gerada pelo cliente, podemos enviá-la do cliente para o Platform Edge Network com SDK da Web ou móvel ou possivelmente recebê-la de uma chamada de API no encaminhamento de eventos. Quando enviamos dados para esse fornecedor em uma regra de encaminhamento de eventos, simplesmente incluímos esse identificador conforme necessário.

Se o fornecedor exigir dados (como uma ID exclusiva específica do fornecedor, por exemplo) que só possam ser gerados ou acessados pela própria tag do lado do cliente, essa tag do fornecedor provavelmente não será uma boa candidata para ser movida. _Não é recomendável tentar reverter a engenharia de uma marca do lado do cliente com a ideia de mover essa coleção de dados para o encaminhamento de eventos sem as APIs apropriadas._

A extensão [Adobe Experience Platform Cloud Connector](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/cloud-connector/overview.html) pode fazer solicitações HTTP conforme necessário com fornecedores que tenham as APIs apropriadas para transferência de dados de evento de servidor para servidor. Embora as extensões específicas do fornecedor sejam ideais e mais extensões estejam em desenvolvimento ativo no momento, podemos implementar regras de encaminhamento de eventos hoje usando a extensão Cloud Connector, sem esperar por extensões adicionais do fornecedor.

## Ferramentas {#tools}

Investigar e testar os pontos de extremidade da API do fornecedor é mais fácil com ferramentas como o [Postman](https://www.postman.com/) ou extensões do editor de texto como o Visual Studio Code [Thunder Client](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client) ou o [HTTP Client](https://marketplace.visualstudio.com/items?itemName=mkloubert.vscode-http-client).

## Próximas etapas {#next-steps}

Este artigo forneceu uma sequência de etapas para avaliar uma tag do lado do cliente do fornecedor e possivelmente movê-la para o lado do servidor em uma propriedade de encaminhamento de eventos. Para obter mais informações sobre tópicos relacionados, consulte estes links:

- [Tag Management](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR) no Adobe Experience Platform
- [Encaminhamento de eventos](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html) para processamento no lado do servidor
- [Atualizações de terminologia](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) na coleção de dados
