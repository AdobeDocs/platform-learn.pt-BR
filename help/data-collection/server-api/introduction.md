---
title: Introdução básica às APIs
description: Introdução às interfaces de programação de aplicativos
activity: understand
doc-type: article
feature-set: Experience Platform
feature: Server API,API,Data Collection,Integrations
level: Beginner
role: User,Developer
solution: Data Collection
topic: Integrations
exl-id: 9607e641-b0d5-49c1-b319-32ed0720e715
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '2087'
ht-degree: 0%

---

# API 101 - Uma introdução básica às APIs

API significa Application Programming Interface. Significa apenas o que diz — há interfaces entre programas e essas interfaces permitem que esses programas se comuniquem. Quando os programadores desenvolvem aplicativos de software, eles geralmente precisam de seu software para se comunicar com outro software ou hardware. A API define o que, como, quando, onde e por que para essas comunicações e interações.

As APIs são uma maneira de resolver desafios comerciais com software. Na maioria dos negócios, é um esforço colaborativo. Colaborar é sempre mais fácil com uma compreensão compartilhada de termos, conceitos e etapas principais.

Se você pensar em clicar em um link em uma página da Web, o navegador usará algumas APIs quando você clicar no link. O navegador reconhece o clique, faz a solicitação da página que você deseja visitar, recupera a página pela Internet e a exibe na tela. Há muitas etapas menores no meio, mas seu navegador é um software que se comunica e interage com uma variedade de APIs apenas para mostrar uma página da Web. Neste artigo, destacaremos termos, conceitos e etapas importantes ao usar ou discutir APIs.

Até o final deste artigo, você deve ter uma compreensão clara desses termos, conceitos e etapas fundamentais. A documentação da API pode ser extensa e as discussões sobre o uso de APIs para lidar com casos de uso específicos podem ser muito detalhadas. Navegar pela documentação e discutir APIs é mais fácil e produtivo com fundamentos claros e entendimento compartilhado.

>[!NOTE]
>
> Embora haja muitas APIs, o foco aqui será nas APIs da Web e do navegador: basicamente, quando um aplicativo de software interage com outro na internet.

## Termos e conceitos da API

O que uma palavra ou frase significa e como posso pensar sobre isso de forma simples e fácil? Em uma API, a parte &quot;aplicativo&quot; significa um aplicativo de software ou programa. A parte &quot;interface de programação&quot; refere-se ao modo e ao local em que um aplicativo interage com outro aplicativo para determinados fins. Em nosso exemplo de página da Web, quando você clica em um link, o navegador envia uma solicitação para um servidor para a página da Web.

![Imagem do hiperlink com URL de destino](../assets/api101-link-destination.png)

Nesta captura de tela, o cursor do mouse está passando o cursor sobre o link do Adobe Experience Platform. Na parte inferior está a barra de status do navegador da Web que mostra o &quot;endereço&quot; da página que o navegador receberá. Em outras palavras, clicar no link do Adobe Experience Platform instrui o navegador a &quot;obter essa página para mim, para que eu possa vê-la aqui na minha tela&quot;.

Quando um link é clicado, o navegador faz uma solicitação para um servidor obter uma página. Isso é uma `GET` , um dos métodos de solicitação comumente usados com APIs da Web. Uma coisa que o navegador precisa para atender à solicitação é o &quot;endereço&quot; da página - onde ele está na Web?

### Partes de um URL

![Barra de endereços do navegador com URL](../assets/api101-address-bar.png)

A maioria dos navegadores tem uma &quot;barra de endereços&quot; que mostra alguns ou todos os &quot;endereços&quot; de uma página da Web. Quando o navegador &quot;obtém&quot; a página do link que clicamos, ele exibe o &quot;endereço&quot; da página nesta barra de endereços. Então, qual é o &quot;endereço&quot; de uma página da Web?

Essa `https://business.adobe.com/products/experience-platform/adobe-experience-platform.html` acima está o endereço de uma página na Web e é chamado de URL ou Uniform Resource Locator. URLs podem se referir a uma página como esta, um arquivo de imagem, um vídeo ou outros tipos de arquivo.

![Partes de um URL](../assets/api101-url-parts.jpg)

Esse endereço, o URL, tem partes específicas muito relevantes para APIs da Web e do navegador.

**Esquema**

O `scheme` acima também é chamado de `protocol` com APIs da Web e normalmente `http` ou `https`. Protocolo de transferência HTTP ou HyperText é como recursos como páginas da Web são transferidos de um servidor da Web para um navegador da Web. HTTPS é a versão segura, onde a transferência acontece pela Internet usando segurança destinada a impedir interferência com o recurso que está sendo transferido. É comum ver um pequeno ícone de cadeado na barra de endereço do navegador ao visualizar uma página por HTTPS.

Para APIs da Web, as transferências desses recursos ocorrem por meio de solicitações HTTP — solicitações por HTTP em outras palavras.

**Hosts e domínios**

O `business.adobe.com` é o host do recurso que está sendo solicitado. Quando o link de exemplo é clicado, o navegador usa essa parte do URL para localizar o servidor onde a página está hospedada. Nem sempre é exatamente o mesmo que o servidor da Web, mas em um nível básico podemos pensar nele como o servidor onde o navegador obterá a página que solicitamos.

Os nomes de domínio fazem parte do Sistema de Nome de Domínio, mais conhecido como DNS. A maioria das pessoas pensa em `adobe.com` ou `example.com` como um &quot;nome de domínio&quot;, mas há partes relevantes para APIs. `www.adobe.com` e `business.adobe.com` pode ser chamado de nomes de domínio, mas a variável `www.` e `business.` partes são chamadas de subdomínios. As APIs geralmente interagem com um URL que inclui um subdomínio como `api.example.com` ou `sub.www.example.com`.

É muito comum ver o termo _host_ consulte um nome de domínio completo, incluindo qualquer subdomínio como `business.adobe.com`. Também é comum ver os termos _domínio_ ou _nome do domínio_ ao se referir a um host sem o subdomínio como `adobe.com`. A memorização dos termos específicos para cada parte e a variação de um host não é importante aqui. Mas estar ciente de que esses termos são comumente usados é importante para que você possa esclarecer quaisquer especificidades relevantes para seus negócios e discussões.

**Origem**

A origem é outro termo para estar ciente de que está intimamente relacionado às partes de um URL. Em um nível básico, uma origem é basicamente a `scheme` mais o `host` mais o `domain` like `https://business.adobe.com`. Valores diferentes geralmente representam origens diferentes, como `https://business.adobe.com` e `http://business.adobe.com` não têm a mesma origem porque têm regimes diferentes. `https://www.adobe.com` e `https://business.adobe.com` também não são a mesma origem em muitos usos devido aos diferentes subdomínios.

**Path**

O último bit no exemplo de URL acima é o `path` ao recurso - a página em nosso exemplo. O `/products/experience-platform/` em geral, representa pastas ou diretórios no servidor da Web. Assim como temos pastas ou diretórios em nossos computadores para documentos e fotos, também temos pastas em servidores da Web para organizar o conteúdo. E finalmente, o `/adobe-experience-platform.html` parte é o nome do arquivo — a página da Web.

Há outras partes mais detalhadas de um URL que serão destacadas na próxima parte desta série.

### APIs de terceiros

Às vezes, as APIs da Web são chamadas de APIs de terceiros. Pense nisso como as partes envolvidas em uma transação. No nosso exemplo de link, você (ou, mais especificamente, seu navegador) é o primeiro participante na solicitação da página. O servidor da Web é o segundo. Então, onde está o terceiro?

É comum que uma página da Web inclua conteúdo ou recursos de outros hosts ou fontes. Nesses casos, quando o navegador começa a exibir a página, ele faz outro conjunto de solicitações para esses outros hosts ou &quot;terceiros&quot;, que hospedam esses recursos. Isso é muito comum, especialmente para conteúdo de mídia como vídeos ou imagens, mas também para dados que precisam ser atualizados no momento em que são visualizados ou usados. Obter a hora atual do dia, o tempo atual ou uma mensagem de boas-vindas personalizada para uma pessoa específica são exemplos em que uma API de terceiros pode fornecer o recurso certo na hora certa. É comum que essas solicitações venham dessas APIs de terceiros.

## Uso comum para APIs da Web

Além do horário, do tempo ou do conteúdo personalizado, há muitos usos para APIs da Web. Plataformas de mídia social como Twitter, TikTok, Facebook, LinkedIn, Snapchat, Pinterest e outras têm uma variedade de APIs que os programadores podem usar com seus aplicativos. E é claro que a Adobe também tem [uma grande variedade de APIs](https://developer.adobe.com/apis) que os programadores usam para que seus softwares possam interagir com produtos e serviços de Adobe. Os produtos e serviços de software acessam outros produtos e serviços de software por meio dessas APIs.

## Exemplo de APIs

As APIs de navegador permitem que os programadores interajam diretamente com os recursos do navegador. A API da bateria permite que o software verifique o status da bateria de um dispositivo para que ele possa alertá-lo, se necessário. A API de área de transferência permite que o software copie ou cole com a área de transferência do seu dispositivo. A API de tela cheia permite que o software apresente a opção para expandir a exibição para a tela cheia do dispositivo, como o YouTube.

A API de acesso a dados do Adobe Experience Platform é uma API da Web que permite aos programadores acessar e baixar arquivos de conjunto de dados do Adobe Experience Platform para que possam usar os dados do perfil do cliente em seus próprios programas. É muito comum que APIs como essa façam parte de um processo de automação de software em que o software é programado para executar uma sequência de etapas usando várias APIs em combinação. Geralmente, isso pode ser uma economia significativa em comparação com a execução manual dessas mesmas etapas.

## Endpoints da API

Quando os programadores &quot;usam&quot; um navegador ou uma API da Web em seus programas, eles normalmente fazem solicitações para enviar ou receber recursos, como nosso navegador de exemplo solicitando uma página da Web. A documentação da API frequentemente lista &quot;endpoints&quot; para essas solicitações, por exemplo: `https://platform.adobe.io/data/foundation/export/files/{dataSetFileId}`. Esse é o padrão específico ou &quot;endpoint&quot; da API de acesso a dados da plataforma que um programador usará para obter um arquivo de conjunto de dados.

O `{dataSetFileId}` cercado por essas chaves representa um valor que o programador precisa enviar na solicitação. Portanto, o URL na solicitação da API real seria semelhante a `https://platform.adobe.io/data/foundation/export/files/xyz123brb` em que `xyz123brb` precisa ser uma ID válida do arquivo de conjunto de dados que o programador deseja receber.

Em outras palavras, da mesma forma que o navegador obtém uma página em um URL específico, as solicitações de API obtêm recursos de, ou enviam recursos para, um endpoint específico como esse exemplo de conjunto de dados.

## Métodos de solicitação HTTP

Nesse ponto, deve estar claro que as APIs da Web fazem solicitações de recursos como páginas da Web ou conjuntos de dados. Como a maioria dos conceitos de software, essas solicitações HTTP seguem padrões repetíveis. Uma solicitação é enviada de um aplicativo de software para outro aplicativo de software que avalia a solicitação e, em seguida, responde: o navegador solicita uma página de um servidor da Web e responde com o conteúdo da página.

Todo o processo, de solicitação a resposta, envolve muitas etapas menores e muito detalhadas, mas os métodos de solicitação são simples. Os métodos de solicitação definem a operação que está sendo solicitada.

**`GET`**

O `GET` O método de solicitação é usado ao solicitar uma resposta que forneça um recurso, como nossa página da Web e exemplos de conjunto de dados. Quando clicamos em um link em um navegador ou tocamos em um link em um dispositivo móvel, estamos criando um `GET` solicitação em segundo plano.

**`POST`**

O `POST` envia dados com a solicitação. Pode parecer estranho que uma &quot;solicitação&quot; envie dados, mas a ideia é que fazer a solicitação da API esteja pedindo ao endpoint — o software de recebimento — para aceitar a solicitação e, no caso de um `POST`, para também aceitar os dados que estão sendo enviados. Os dados enviados geralmente são gravados em um armazenamento de dados como um banco de dados ou arquivo, para que possam ser salvos.

**`PUT`**

O `PUT` o método de solicitação é semelhante a `POST` como ele envia dados, mas se os dados enviados já existirem no ponto de extremidade, uma `PUT` atualizará os dados existentes, substituindo-os. A `POST` não atualiza, simplesmente envia, portanto, vários `POST` As solicitações podem criar vários registros dos dados enviados, em vez de atualizar qualquer registro existente.

**`PATCH`**

O `PATCH` O método de solicitação é usado para enviar dados que atualizam parte de um registro existente, como quando alteramos nosso endereço atualizando nosso perfil de conta. Com um `POST` solicite a criação de um perfil adicional e com um `PUT`, o perfil existente pode ser substituído, mas usando o `PATCH` simplesmente atualizamos a parte relevante do registro existente, como nosso endereço.

**`DELETE`**

O `DELETE` O método de solicitação remove um recurso especificado na solicitação, como se clicássemos em um link para excluir nosso perfil de conta totalmente.

Há vários outros, mas esta é uma lista dos métodos mais comuns ao trabalhar com APIs.

### Exemplo de solicitação

Agora que você tem os termos básicos, os conceitos e as etapas envolvidos com as APIs, podemos observar um exemplo de solicitação de API na prática.

A página do nosso exemplo de navegador tem um URL de `https://business.adobe.com/products/experience-platform/adobe-experience-platform.html`. Quando o link do Adobe Experience Platform é clicado, o navegador faz uma `GET` para esta página. Como temos o navegador para fazer o trabalho para nós, tudo o que precisamos fazer é clicar, mas se um programador quiser que essa solicitação aconteça em um aplicativo de software, ele terá que fornecer todos os detalhes necessários para que a solicitação da API seja atendida com sucesso.

Veja como isso pode parecer no código:

```js
fetch(
  "https://business.adobe.com/products/experience-platform/adobe-experience-platform.html",
  {
    headers: {
      accept:
        "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9",
      "accept-language": "en-US,en;q=0.9",
      "sec-ch-ua":
        '" Not A;Brand";v="99", "Chromium";v="101", "Microsoft Edge";v="101"',
      "sec-fetch-dest": "document",
      "sec-fetch-mode": "navigate",
      "sec-fetch-site": "none",
      "sec-fetch-user": "?1",
      "upgrade-insecure-requests": "1",
    },
    referrerPolicy: "strict-origin-when-cross-origin",
    body: null,
    method: "GET",
    mode: "cors",
    credentials: "include",
  }
);
```

No código acima, você pode ver a variável `URL` o navegador está solicitando, e para baixo perto da parte inferior é a variável `method: "GET"` método de solicitação. As outras linhas de código também são parte da solicitação, mas estão além do escopo deste artigo.


*[API]: Interface de programação de aplicativos *[URL]: Endereço Uniforme de Recursos *[HTTP]: Protocolo de transferência do HyperText *[DNS]: Sistema de Nome de Domínio
