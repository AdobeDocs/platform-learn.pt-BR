---
title: Frame.io e Workfront Fusion
description: Frame.io e Workfront Fusion
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 37de6ceb-833e-4e75-9201-88bddd38a817
source-git-commit: da6917ec8c4e863e80eef91280e46b20816a5426
workflow-type: tm+mt
source-wordcount: '2674'
ht-degree: 0%

---

# 1.2.5 Frame.io e Workfront Fusion

No exercício anterior, você configurou o cenário `--aepUserLdap-- - Firefly + Photoshop` e configurou um webhook de entrada para acionar o cenário, além de uma resposta de webhook quando o cenário foi concluído com êxito. Em seguida, você usou o Postman para acionar esse cenário. O Postman é uma ótima ferramenta para testes, mas em um cenário comercial real, os usuários empresariais não usariam o Postman para acionar um cenário. Em vez disso, eles usariam outro aplicativo e esperariam que esse outro aplicativo ativasse um cenário no Workfront Fusion. Neste exercício, isso é exatamente o que você fará com o Frame.io.

>[!NOTE]
>
>Para concluir com êxito este exercício, você precisa ser um usuário administrador na sua conta Frame.io. O exercício abaixo foi criado para o Frame.io V3 e será atualizado posteriormente para o Frame.io V4.

## 1.2.5.1 Acessando Frame.io

Ir para [https://app.frame.io/projects](https://app.frame.io/projects){target="_blank"}.

Clique no ícone **+** para criar seu próprio projeto no Frame.io.

![E/S de Quadro](./images/frame1.png)

Insira o nome `--aepUserLdap--` e clique em **Criar projeto**.

![E/S de Quadro](./images/frame2.png)

Você verá seu projeto no menu esquerdo.
Em um dos exercícios anteriores, você baixou o [citisignal-fiber.psd](./../../../assets/ff/citisignal-fiber.psd){target="_blank"} na área de trabalho. Selecione esse arquivo e arraste-o e solte-o na pasta do projeto que acabou de ser criada.

![E/S de Quadro](./images/frame3.png)

## 1.2.5.2 Workfront Fusion e Frame.io

No exercício anterior, você criou o cenário `--aepUserLdap-- - Firefly + Photoshop`, que começou com um webhook personalizado e terminou com uma resposta de webhook. O uso dos webhooks foi testado usando o Postman, mas obviamente, o objetivo de tal cenário é ser chamado por um aplicativo externo. Como dito antes, o Frame.io será esse exercício, mas entre o Frame.io e o `--aepUserLdap-- - Firefly + Photoshop` é necessário outro cenário do Workfront Fusion. agora você configurará esse cenário.

Ir para [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Abra o **Workfront Fusion**.

![WF Fusion](./images/wffusion1.png)

No menu esquerdo, vá para **Cenários** e selecione sua pasta `--aepUserLdap--`. Clique em **Criar um novo cenário**.

![E/S de Quadro](./images/frame4.png)

Use o nome `--aepUserLdap-- - Frame IO Custom Action`.

![E/S de Quadro](./images/frame5.png)

Clique no **objeto de ponto de interrogação** na tela. Digite o texto `webhook` na caixa de pesquisa e clique em **Webhooks**.

![E/S de Quadro](./images/frame6.png)

Clique em **Webhook personalizado**.

![E/S de Quadro](./images/frame7.png)

Clique em **Adicionar** para criar uma nova url de webhook.

![E/S de Quadro](./images/frame8.png)

Para o **nome do Webhook**, use `--aepUserLdap-- - Frame IO Custom Action Webhook`. Clique em **Salvar**.

![E/S de Quadro](./images/frame9.png)

Você deverá ver isso. Deixe essa tela aberta e intacta, pois você precisará dela em uma próxima etapa. Você terá que copiar a URL do webhook em uma próxima etapa, clicando em **Copiar endereço para a área de transferência**.

![E/S de Quadro](./images/frame10.png)

Ir para [https://developer.frame.io/](https://developer.frame.io/){target="_blank"}. Clique em **FERRAMENTAS DO DESENVOLVEDOR** e escolha **Ações Personalizadas**.

![E/S de Quadro](./images/frame11.png)

Clique em **Criar uma Ação Personalizada**.

![E/S de Quadro](./images/frame12.png)

Insira os seguintes valores:

- **NAME**: usar `--aepUserLdap-- - Frame IO Custom Action Fusion`
- **DESCRIÇÃO**: usar `--aepUserLdap-- - Frame IO Custom Action Fusion`
- **EVENT**: usar `fusion.tutorial`.
- **URL**: insira a URL do webhook que você acabou de criar no Workfront Fusion
- **EQUIPE**: selecione a equipe Frame.io apropriada, neste caso, **Um Tutorial do Adobe**.

Clique em **Enviar**.

![E/S de Quadro](./images/frame15.png)

Você deverá ver isso.

![E/S de Quadro](./images/frame14.png)

Volte para [https://app.frame.io/projects](https://app.frame.io/projects){target="_blank"}. Atualize a página.

![E/S de Quadro](./images/frame16.png)

Depois de atualizar a página, clique nos 3 pontos **...** no ativo **citisignal-fiber.psd**. Você deverá ver a ação personalizada criada anteriormente aparecer no menu mostrado. Clique na ação personalizada `--aepUserLdap-- - Frame IO Custom Action Fusion`.

![E/S de Quadro](./images/frame17.png)

Você deverá ver um **Sucesso semelhante!Pop-up**. Este pop-up é o resultado da comunicação entre o Frame.io e o Workfront Fusion.

![E/S de Quadro](./images/frame18.png)

Retorne a tela para o Workfront Fusion. Agora você deve ver **Determinado com êxito** aparecer no objeto Webhook personalizado. Clique em **OK**.

![E/S de Quadro](./images/frame19.png)

Clique em **Executar uma vez** para habilitar o modo de teste e testar a comunicação com Frame.io novamente.

![E/S de Quadro](./images/frame20.png)

Volte para Frame.io e clique na ação personalizada `--aepUserLdap-- - Frame IO Custom Action Fusion` novamente.

![E/S de Quadro](./images/frame21.png)

Retorne a tela para o Workfront Fusion. Agora você deve ver uma marca de seleção verde e uma bolha mostrando **1**. Clique na bolha para ver os detalhes.

![E/S de Quadro](./images/frame22.png)

A exibição detalhada da bolha mostra os dados recebidos do Frame.io. Você deve ver várias IDs. Por exemplo, o campo **resource.id** mostra a ID exclusiva no Frame.io do ativo **citisignal-fiber.psd**.

![E/S de Quadro](./images/frame23.png)

Agora que a comunicação foi estabelecida entre o Frame.io e o Workfront Fusion, você pode continuar a configuração.

## 1.2.5.3 Fornecendo uma resposta de formulário personalizado para Frame.io

Quando a ação personalizada é invocada no Frame.io, o Frame.io espera receber uma resposta do Workfront Fusion. Se você voltar para o cenário criado no exercício anterior, várias variáveis serão necessárias para atualizar o arquivo padrão do Photoshop PSD. Essas variáveis são definidas na carga útil usada:

```json
{
    "psdTemplate": "citisignal-fiber.psd",
    "xlsFile": "placeholder",
    "prompt":"misty meadows",
    "cta": "Buy this now!",
    "button": "Click here to buy!"
}
```

Portanto, para que o cenário `--aepUserLdap-- - Firefly + Photoshop` seja executado com êxito, campos como **prompt**, **cta**, **button** e **psdTemplate** são necessários.

Os primeiros 3 campos, **prompt**, **cta**, **button**, exigem entrada do usuário que precisa ser coletada no Frame.io quando o usuário invoca a ação personalizada. Portanto, a primeira coisa a ser feita no Workfront Fusion é verificar se essas variáveis estão disponíveis ou não. Caso contrário, o Workfront Fusion deverá responder ao Frame.io solicitando que essas variáveis sejam inseridas. A maneira de fazer isso é usando um formulário no Frame.io.

Volte para o Workfront Fusion e abra o cenário `--aepUserLdap-- - Frame IO Custom Action`. Passe o mouse sobre o objeto **Webhook personalizado** e clique no ícone **+** para adicionar outro módulo.

![E/S de Quadro](./images/frame24.png)

Pesquise por `Flow Control` e clique em **Controle de Fluxo**.

![E/S de Quadro](./images/frame25.png)

Clique para selecionar **roteador**.

![E/S de Quadro](./images/frame26.png)

Você deverá ver isso.

![E/S de Quadro](./images/frame27.png)

Clique no **?** objeto e clique para selecionar **Webhooks**.

![E/S de Quadro](./images/frame28.png)

Selecione **resposta do Webhook**.

![E/S de Quadro](./images/frame29.png)

Você deverá ver isso.

![E/S de Quadro](./images/frame30.png)

Copie o código JSON abaixo e cole-o no campo **Corpo**.


```json
{
  "title": "What do you want Firefly to generate?",
  "description": "Enter your Firefly prompt.",
  "fields": [
    {
      "type": "text",
      "label": "Prompt",
      "name": "Prompt",
      "value": ""
    },
    {
      "type": "text",
      "label": "CTA Text",
      "name": "CTA Text",
      "value": ""
    },
    {
      "type": "text",
      "label": "Button Text",
      "name": "Button Text",
      "value": ""
    }
  ]
}
```

Clique no ícone para limpar e embelezar o código JSON. Clique em **OK**.

![E/S de Quadro](./images/frame31.png)

Clique em **Salvar** para salvar as alterações.

![E/S de Quadro](./images/frame32.png)

Em seguida, é necessário configurar um filtro para garantir que esse caminho do cenário só seja executado quando nenhum prompt estiver disponível. Clique na **chave inglesa** e selecione **Configurar um filtro**.

![E/S de Quadro](./images/frame33.png)

Configure os seguintes campos:

- **Rótulo**: use `Prompt isn't available`.
- **Condição**: use `{{1.data.Prompt}}`.
- **Operadores Básicos**: selecione **Não existe**.

>[!NOTE]
>
>As variáveis no Workfront Fusion podem ser especificadas manualmente usando esta sintaxe: `{{1.data.Prompt}}`. O número na variável faz referência ao módulo no cenário. Neste exemplo, você pode ver que o primeiro módulo do cenário é chamado de **Webhooks** e tem um número de sequência de **1**. Isso significa que a variável `{{1.data.Prompt}}` acessará o campo **data.Prompt** do módulo com o número de sequência 1. Os números de sequência podem, às vezes, ser diferentes. Portanto, preste atenção ao copiar/colar essas variáveis e sempre verifique se o número de sequência usado é o correto.

Clique em **OK**.

![E/S de Quadro](./images/frame34.png)

Você deverá ver isso. Clique primeiro no ícone **Salvar** e depois clique em **Executar uma vez** para testar o cenário.

![E/S de Quadro](./images/frame35.png)

Você deverá ver isso.

![E/S de Quadro](./images/frame36.png)

Volte para Frame.io e clique na ação personalizada `--aepUserLdap-- - Frame IO Custom Action Fusion` no ativo **citisignal-fiber.psd** novamente.

![E/S de Quadro](./images/frame37.png)

Agora você deve ver um prompt dentro do Frame.io. Não preencha os campos ainda e não envie o formulário ainda. Esse prompt é exibido com base na resposta do Workfront Fusion que você acabou de configurar.

![E/S de Quadro](./images/frame38.png)

Volte para o Workfront Fusion e clique na bolha no módulo **resposta do Webhook**. Você verá que em **INPUT**, você verá o corpo que contém a carga JSON do formulário. Clique novamente em **Executar uma vez**.

![E/S de Quadro](./images/frame40.png)

Você deverá ver isso novamente.

![E/S de Quadro](./images/frame41.png)

Volte para Frame.io e preencha os campos conforme indicado. Clique em **Enviar**.

![E/S de Quadro](./images/frame39.png)

Você deverá ter um **Sucesso!Pop-up**.

![E/S de Quadro](./images/frame42.png)

Volte para o Workfront Fusion e clique na bolha no módulo **Webhook personalizado**. Na Operação 1, em **OUTPUT**, você pode ver um novo objeto **dados** que contém campos como **Texto do Botão**, **Texto do CTA** e **Prompt**. Com essas variáveis de entrada de usuário disponíveis em seu cenário, você tem o suficiente para continuar sua configuração.

![E/S de Quadro](./images/frame43.png)

## 1.2.5.4 Recuperar local do arquivo do Frame.io

Como discutido anteriormente, campos como **prompt**, **cta**, **button** e **psdTemplate** são necessários para que este cenário funcione. Os primeiros 3 campos já estão disponíveis, mas o **psdTemplate** para usar ainda está ausente. O **psdTemplate** agora referenciará um local do Frame.io, pois o arquivo **citisignal-fiber.psd** está hospedado no Frame.io. Para recuperar o local desse arquivo, é necessário configurar e usar a conexão Frame.io no Workfront Fusion.

Volte para o Workfront Fusion e abra o cenário `--aepUserLdap-- - Frame IO Custom Action`. Passe o mouse sobre **?Módulo**, clique no ícone **+** para adicionar outro módulo e pesquisar por `frame`. Clique em **Frame.io**.

![E/S de Quadro](./images/frame44.png)

Clique em **Frame.io (herdado)**.

![E/S de Quadro](./images/frame45.png)

Clique em **Obter um ativo**.

![E/S de Quadro](./images/frame46.png)

Para usar a conexão Frame.io, é necessário configurá-la primeiro. Clique em **Adicionar** para fazer isso.

![E/S de Quadro](./images/frame47.png)

Abra a lista suspensa **Tipo de conexão**.

![E/S de Quadro](./images/frame48.png)

Selecione **Chave de API Frame.io** e insira o nome `--aepUserLdap-- - Frame.io Token`.

![E/S de Quadro](./images/frame49.png)

Para obter um token de API, acesse [https://developer.frame.io/](https://developer.frame.io/){target="_blank"}. Clique em **FERRAMENTAS DO DESENVOLVEDOR** e escolha **Tokens**.

![E/S de Quadro](./images/frame50.png)

Clique em **Criar um token**.

![E/S de Quadro](./images/frame51.png)

Use a **Descrição** `--aepUserLdap-- - Frame.io Token` e clique em **Selecionar todos os escopos**.

![E/S de Quadro](./images/frame52.png)

Role para baixo e clique em **Enviar**.

![E/S de Quadro](./images/frame53.png)

O token foi criado. Clique em **Copiar** para copiar para a área de transferência.

![E/S de Quadro](./images/frame54.png)

Volte para o seu cenário no Workfront Fusion. Cole o token no campo **Sua chave de API Frame.io**. Clique em **OK**. Sua conexão será testada pelo Workfront Fusion.

![E/S de Quadro](./images/frame55.png)

Se a conexão tiver sido testada com êxito, ela aparecerá automaticamente em **Conexão**. Agora você tem uma conexão bem-sucedida e precisa concluir a configuração para obter todos os detalhes do ativo do Frame.io, incluindo o local do arquivo. Para fazer isso, você precisa fornecer a **ID do ativo**.

![E/S de Quadro](./images/frame56.png)

A **ID do ativo** é compartilhada pelo Frame.io para o Workfront Fusion como parte da comunicação inicial do **webhook personalizado** e pode ser encontrada no campo **resource.id**. Selecione **resource.id** e clique em **OK**.

![E/S de Quadro](./images/frame57.png)

Você deve ver isso agora. Salve as alterações e clique em **Executar uma vez** para testar o cenário.

![E/S de Quadro](./images/frame58.png)

Volte para Frame.io e clique na ação personalizada `--aepUserLdap-- - Frame IO Custom Action Fusion` no ativo **citisignal-fiber.psd** novamente.

![E/S de Quadro](./images/frame37.png)

Agora você deve ver um prompt dentro do Frame.io. Não preencha os campos ainda e não envie o formulário ainda. Esse prompt é exibido com base na resposta do Workfront Fusion que você acabou de configurar.

![E/S de Quadro](./images/frame38.png)

Volte para o Workfront Fusion. Clique novamente em **Executar uma vez**.

![E/S de Quadro](./images/frame59.png)

Volte para Frame.io e preencha os campos conforme indicado. Clique em **Enviar**.

![E/S de Quadro](./images/frame39.png)

Volte para o Workfront Fusion e clique na bolha no **Frame.io - Obtenha um módulo do ativo**.

![E/S de Quadro](./images/frame60.png)

Agora você pode ver muitos metadados sobre o ativo específico **citisignal-fiber.psd**.

![E/S de Quadro](./images/frame61.png)

A informação específica necessária para este caso de uso é a url de local do arquivo **citisignal-fiber.psd**, que você pode encontrar rolando para baixo até o campo **Original**.

![E/S de Quadro](./images/frame62.png)

Agora você tem todos os campos (**prompt**, **cta**, **button** e **psdTemplate**) disponíveis que são necessários para que este cenário funcione.

## 1.2.5.5 Invocar cenário do Workfront

No exercício anterior, você configurou o cenário `--aepUserLdap-- - Firefly + Photoshop`. Agora você precisa fazer uma pequena alteração nesse cenário.

Abra o cenário `--aepUserLdap-- - Firefly + Photoshop` em outra guia e clique no primeiro módulo **Adobe Photoshop - Aplicar edições do PSD**. Agora você deve ver que o arquivo de entrada está configurado para usar um local dinâmico no Microsoft Azure. Considerando que, para esse caso de uso, o arquivo de entrada não é mais armazenado no Microsoft Azure, mas usando o armazenamento Frame.io, é necessário alterar essas configurações.

![E/S de Quadro](./images/frame63.png)

Altere **Storage** para **External** e altere **File location** para usar somente a variável **psdTemplate** retirada do módulo de entrada **Custom webhook**. Clique em **OK** e em **Salvar** para salvar suas alterações.

![E/S de Quadro](./images/frame64.png)

Clique no módulo **Webhook personalizado** e clique em **Copiar endereço para a área de transferência**. Você precisa copiar o URL da maneira que precisará usá-lo no outro cenário.

![E/S de Quadro](./images/frame65.png)

Volte para o seu cenário `--aepUserLdap-- - Frame IO Custom Action`. Passe o mouse sobre o **Frame.io - Obtenha um módulo de ativo** e clique no ícone **+**.

![E/S de Quadro](./images/frame66.png)

Digite `http` e clique em **HTTP**.

![E/S de Quadro](./images/frame67.png)

Selecione **Fazer uma solicitação**.

![E/S de Quadro](./images/frame68.png)

Cole a URL do webhook personalizado no campo **URL**. Defina o **Método** como POST**.

![E/S de Quadro](./images/frame69.png)

Defina **Tipo de corpo** como **Raw** e **Tipo de conteúdo** como **JSON (application/json)**.
Cole a carga JSON abaixo no campo **Solicitar conteúdo** e habilite a caixa de seleção para **Analisar resposta**.

```json
{
    "psdTemplate": "citisignal-fiber.psd",
    "xlsFile": "placeholder",
    "prompt":"misty meadows",
    "cta": "Buy this now!",
    "button": "Click here to buy!"
}
```

Agora você tem uma carga estática configurada, mas ela precisa se tornar dinâmica usando as variáveis coletadas anteriormente.

![E/S de Quadro](./images/frame70.png)

Para o campo **psdTemplate**, substitua a variável estática **citisignal-fiber.psd** pela variável **Original**.

![E/S de Quadro](./images/frame71.png)

Para os campos **prompt**, **cta** e **button**, substitua as variáveis estáticas pelas variáveis dinâmicas que foram inseridas no cenário pela solicitação de webhook de entrada do Frame.io, que são os campos **data.Prompt**, **data.CTA Text** e **data.Button Text**.

Clique em **OK**.

![E/S de Quadro](./images/frame72.png)

Clique em **Salvar** para salvar as alterações.

![E/S de Quadro](./images/frame73.png)

## 1.2.5.6 Salvar novo ativo no Frame.io

Depois que o outro cenário do Workfront Fusion for chamado, o resultado será um novo modelo do Photoshop PSD disponível. Esse arquivo do PSD precisa ser armazenado novamente no Frame.io, que é a última etapa desse cenário.

Passe o mouse sobre o módulo **HTTP - Fazer uma solicitação** e clique no ícone **+**.

![E/S de Quadro](./images/frame74.png)

Selecione **Frame.io (Herdado)**.

![E/S de Quadro](./images/frame75.png)

Selecione **Criar um ativo**.

![E/S de Quadro](./images/frame76.png)

Sua conexão Frame.io será selecionada automaticamente.

![E/S de Quadro](./images/frame77.png)

Selecione as seguintes opções:

- **ID da Equipe**: selecione a ID da Equipe apropriada, neste caso `One Adobe Tutorial`.
- **ID do projeto**: use `--aepUserLdap--`.
- **ID da Pasta**: use `root`.
- **Tipo**: use `File`.

![E/S de Quadro](./images/frame78.png)

Para o campo **Nome**, você pode usar uma variável, como **carimbo de data/hora** (ou alterá-lo para algo que faça mais sentido para você). Você pode encontrar a variável predefinida **carimbo de data/hora** na guia **Data e hora**.

![E/S de Quadro](./images/frame79.png)

Para o campo **URL do Source**, use o código JSON abaixo.

```json
{{6.data.newPsdTemplate}}
```

>[!NOTE]
>
>As variáveis no Workfront Fusion podem ser especificadas manualmente usando esta sintaxe: `{{6.data.newPsdTemplate}}`. O número na variável faz referência ao módulo no cenário. Neste exemplo, você pode ver que o sexto módulo no cenário é chamado **HTTP - Fazer uma solicitação** e tem um número de sequência de **6**. Isso significa que a variável `{{6.data.newPsdTemplate}}` acessará o campo **data.newPsdTemplate** do módulo com o número de sequência 6. Os números de sequência podem, às vezes, ser diferentes. Portanto, preste atenção ao copiar/colar essas variáveis e sempre verifique se o número de sequência usado é o correto.

Clique em **OK**.

![E/S de Quadro](./images/frame80.png)

Clique em **Salvar** para salvar as alterações.

![E/S de Quadro](./images/frame81.png)

Por fim, é necessário configurar um filtro para garantir que esse caminho do cenário só seja executado quando um prompt estiver disponível. Clique na **chave inglesa** e selecione **Configurar um filtro**.

![E/S de Quadro](./images/frame82.png)

Configure os seguintes campos:

- **Rótulo**: use `Prompt is available`.
- **Condição**: use `{{1.data.Prompt}}`.
- **Operadores Básicos**: selecione **existe**.

>[!NOTE]
>
>As variáveis no Workfront Fusion podem ser especificadas manualmente usando esta sintaxe: `{{1.data.Prompt}}`. O número na variável faz referência ao módulo no cenário. Neste exemplo, você pode ver que o primeiro módulo do cenário é chamado de **Webhooks** e tem um número de sequência de **1**. Isso significa que a variável `{{1.data.Prompt}}` acessará o campo **data.Prompt** do módulo com o número de sequência 1. Os números de sequência podem, às vezes, ser diferentes. Portanto, preste atenção ao copiar/colar essas variáveis e sempre verifique se o número de sequência usado é o correto.

Clique em **OK**.

![E/S de Quadro](./images/frame83.png)

Clique em **Salvar** para salvar as alterações.

![E/S de Quadro](./images/frame84.png)

## 1.2.5.7 Teste seu caso de uso completo

Clique em **Executar uma vez** no seu cenário `--aepUserLdap-- - Frame IO Custom Action`.

![E/S de Quadro](./images/frame85.png)

Volte para Frame.io e clique na ação personalizada `--aepUserLdap-- - Frame IO Custom Action Fusion` no ativo **citisignal-fiber.psd** novamente.

![E/S de Quadro](./images/frame37.png)

Agora você deve ver um prompt dentro do Frame.io. Não preencha os campos ainda e não envie o formulário ainda. Esse prompt é exibido com base na resposta do Workfront Fusion que você acabou de configurar.

![E/S de Quadro](./images/frame38.png)

Volte para o Workfront Fusion. Clique em **Executar uma vez** no seu cenário `--aepUserLdap-- - Frame IO Custom Action`.

![E/S de Quadro](./images/frame86.png)

No Workfront Fusion, abra o cenário `--aepUserLdap-- - Firefly + Photoshop` e clique em **Executar uma vez** nesse cenário.

![E/S de Quadro](./images/frame87.png)

Volte para Frame.io e preencha os campos conforme indicado. Clique em **Enviar**.

![E/S de Quadro](./images/frame39.png)

Após 1 a 2 minutos, você deve ver um novo ativo que aparece automaticamente no Frame.io. Clique duas vezes no novo ativo para abri-lo.

![E/S de Quadro](./images/frame88.png)

Agora é possível ver claramente que todas as variáveis de entrada do usuário foram aplicadas automaticamente.

![E/S de Quadro](./images/frame89.png)

Você concluiu este exercício com êxito.

## Próximas etapas

Ir para [1.2.6 Frame.io para Fusion para AEM Assets](./ex6.md){target="_blank"}

Retorne ao [Creative Workflow Automation with Workfront Fusion](./automation.md){target="_blank"}

Voltar para [Todos os Módulos](./../../../overview.md){target="_blank"}

