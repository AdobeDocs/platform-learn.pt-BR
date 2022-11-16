---
title: Adobe Journey Optimizer - Eventos comerciais
description: Esta seção explica como usar o recurso de eventos comerciais para executar um caso de uso de "item de volta em estoque"
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: cc06d847-a405-4223-836c-c22ad6c9caca
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 8%

---

# 10.5 Criar uma jornada de evento comercial

Faça logon no Adobe Journey Optimizer acessando [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Você será redirecionado para o **Início**  no Journey Optimizer. Primeiro, certifique-se de usar a sandbox correta. A sandbox a ser usada é chamada de `--aepSandboxId--`. Para alterar de uma sandbox para outra, clique em **Produto de produção (VA7)** e selecione a sandbox na lista. Neste exemplo, a sandbox é chamada de **Ativação AEP FY22**. Você estará no **Início** exibição da sandbox `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

## 10.5.1 Criar um evento comercial

No menu esquerdo, clique em **Configurações**. Clique no botão **Gerenciar** botão dentro do **Eventos** cartão.

![Journey Optimizer](./images/be1.png)

Os eventos comerciais são um novo tipo de evento que pode ser criado dentro do Journey Optimizer. Ao contrário do **Unitário** eventos que você criou em módulos anteriores, os eventos comerciais não são acionados pelo cliente, mas pela organização. Agora você criará seu evento comercial.

Clique em **Criar evento**.

![Journey Optimizer](./images/be2.png)

Insira os seguintes valores no formulário de criação Evento:

- **Nome**: `--demoProfileLdap--ItemBackInStock`. Por exemplo: **vangeluwItemBackInStock**
- **Descrição**: Esse evento é acionado quando um produto volta ao estoque
- **Tipo**: select **Negócios** no menu suspenso

![Journey Optimizer](./images/evde.png)

Para o Esquema, selecione **Demo System - Event Schema for JO Business Events (Global v1.1) v.1**. Agora é necessário selecionar os campos no schema necessário para o nosso caso de uso.

![Journey Optimizer](./images/evdes.png)

Siga estas etapas:

Clique no botão **lápis** ícone no campo onde diz **1 campo selecionado**.

![Journey Optimizer](./images/23.8-4.png)

Selecione todos os campos disponíveis no esquema e clique em **OK**.

![Journey Optimizer](./images/23.8-5.png)

Para a condição: você precisa especificar quais registros nesse schema acionarão o evento de negócios.

Siga estas etapas:

Clique no botão **lápis** ícone no campo onde diz **Adicionar uma condição**.

![Journey Optimizer](./images/23.8-6.png)

No lado esquerdo, expanda a `--aepTenantId--` objeto , expanda o objeto **joBusinessEvents** e arrastar e soltar o campo **eventName** na tela.

![Journey Optimizer](./images/23.8-7.png)

Para o campo **eventName**, insira o seguinte valor: `--demoProfileLdap--ItemBackInStock`. Por exemplo: vangeluwItemBackInStock.
Clique em **OK**.

![Journey Optimizer](./images/23.8-8.png)

Clique em **OK**.

![Journey Optimizer](./images/23.8-9.png)

Por fim, o formulário de criação de eventos deve ficar parecido com este. Clique em **Salvar** para salvar seu evento comercial.

![Journey Optimizer](./images/23.8-10.png)

## 10.5.2 Criar uma jornada de evento comercial

Agora você pode aproveitar esse evento de negócios e a mensagem dentro de uma jornada. Ir para **Jornada**. Clique em **Criar Jornada**.

![Journey Optimizer](./images/bej10.png)

No lado direito, você verá um formulário no qual será necessário especificar o nome e a descrição da jornada. Insira os seguintes valores:

- **Nome**: `--demoProfileLdap-- - Item back in stock journey`. Por exemplo: vangeluw - Item de volta na jornada de estoque
- **Descrição**: Essa jornada envia um SMS quando um item retorna ao estoque para um visitante que demonstrou interesse.

Clique em **OK**.

![Journey Optimizer](./images/bej11.png)

No menu esquerdo, em **Eventos**, procure pelo seu ldap. Você encontrará o evento de negócios criado anteriormente `--demoProfileLdap--ItemBackInStock`. Arraste e solte esse evento na tela, pois este será o ponto inicial da jornada.

![Journey Optimizer](./images/bej12.png)

Como você pode ver, uma **Ler segmento** atividade foi adicionada automaticamente à tela de desenho. Isso ocorre porque os eventos comerciais enviam apenas um acionador para a jornada ler um segmento específico, que recuperará a lista de perfis para essa jornada.

Clique no botão **Ler segmento** atividade .
O **Ler segmento** a configuração do espera que você selecione o segmento que deseja notificar do evento comercial que acabou de acontecer. Clique no botão **Selecionar um segmento** campo.

![Journey Optimizer](./images/bej13.png)

No **Escolher um segmento** pop-up, pesquise pelo ldap e selecione o segmento criado em [Módulo 6 - CDP em tempo real - Crie um segmento e execute ações](../module6/real-time-cdp-build-a-segment-take-action.md) nomeado `--demoProfileLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`. por exemplo: vangeluw - Interesse em TEUS FITNESS JACKSHIRT. Clique em **Salvar**.

![Journey Optimizer](./images/bej14.png)

Em seguida, clique em **Ok**.

![Journey Optimizer](./images/bej15.png)

A próxima etapa é arrastar e soltar a ação que queremos executar nesta jornada. Selecione a ação **SMS**, em seguida, arraste-a e solte-a depois da condição que você acabou de adicionar.

![Demonstração](./images/jop9.png)

Defina as **Categoria** para **Marketing** e selecione uma superfície de sms que permita enviar sms. Nesse caso, a superfície do email a ser selecionada é **SMS**.

![ACOP](./images/journeyactions1x.png)

A próxima etapa é criar a mensagem. Para fazer isso, clique em **Editar conteúdo**.

![ACOP](./images/journeyactions2x.png)

Agora você verá o painel de mensagens, onde poderá configurar o texto do seu SMS. Clique no botão **Compor mensagem** área para criar a mensagem.

![Journey Optimizer](./images/sms3.png)

Insira o seguinte texto: `Hi {{profile.person.name.firstName}}, the Proteus Fitness Jackshirt is back in stock at Luma.`. Clique em **Salvar**.

![Journey Optimizer](./images/sms4.png)

Volte para o painel de mensagens clicando no botão **seta** ao lado do texto da linha de assunto no canto superior esquerdo.

![Journey Optimizer](./images/oc79xx.png)

Agora você verá a ação de SMS concluída. Clique em **Ok**.

![Journey Optimizer](./images/oc79xxy.png)

Sua jornada agora está pronta para ser publicada. Clique em **Publicar**.

![Journey Optimizer](./images/jop13.png)

Clique em **Publicar** novamente.

![Journey Optimizer](./images/jop14.png)

Sua jornada foi publicada, agora você pode testá-la!

![Journey Optimizer](./images/jop15.png)

## 10.5.3 Testar a jornada de eventos da sua empresa

Agora você simulará o reestoque de um produto assimilando um novo evento em relação à variável **Demo System - Event Schema for JO Business Events (Global v1.1) v.1** usando o Postman.

No menu esquerdo, clique em **Fontes** e clique no botão **Contas** guia .

![Journey Optimizer](./images/s1.png)

No **Contas** , você encontrará a conta nomeada **Eventos comerciais do Journey Optimizer**. Clique para abri-lo.

![Journey Optimizer](./images/s2.png)

Essa conta tem apenas um fluxo de dados, clique no nome do fluxo de dados para selecioná-la.

![Journey Optimizer](./images/s3.png)

Clique em **Copiar carga do esquema** no menu à direita. Essa opção copia o todo **curl** para inserir um registro no **Demo System - Event Schema for JO Business Events (Global v1.1) v.1** para a área de transferência.

![Journey Optimizer](./images/s4.png)

Cole o comando Curl dentro de um editor de texto

![Journey Optimizer](./images/s5.png)

Vamos dar uma olhada mais de perto nesta solicitação.

- A solicitação de POST é enviada para a ID de entrada do DCS
- A solicitação faz referência ao esquema, ao conjunto de dados e à ID da organização.
- Finalmente, ele contém o nó xdmEntity que representa os dados que queremos criar dentro do conjunto de dados.

Agora é necessário substituir o seguinte `xdmEntity` linha...

```json
"xdmEntity": {
  "_experienceplatform": {
    "joBusinessEvents": {
      "eventDescription": "string",
      "eventName": "string",
      "stockEventId": "string"
    }
  },
  "_id": "/uri-reference",
  "eventType": "advertising.completes",
  "timestamp": "2018-11-12T20:20:39+00:00"
}
```

...por esta linha, verifique o campo eventName como deve dizer `--demoProfileLdap--ItemBackInStock`, que representa a condição especificada no evento comercial para acionar a jornada.

```json
"xdmEntity": {
  "_experienceplatform": {
    "joBusinessEvents": {
      "eventDescription": "Product Proteus Fitness Jackshirt is back in stock",
      "eventName": "--demoProfileLdap--ItemBackInStock",
      "stockEventId": "1"
    }
  },
  "_id": "/uri-reference",
  "eventType": "productBackInStock",
  "timestamp": "2021-04-19T15:25:39+00:00"
}
```

O arquivo **curl** O comando deve ter esta aparência:

![Journey Optimizer](./images/s6.png)

Selecione tudo e copie-o para a área de transferência.

Abra o Postman. No lado esquerdo do Postman, clique em **Importar**.

![Journey Optimizer](./images/23.8-46.png)

Selecione o **Texto bruto** e cole o comando copiado anteriormente aqui. Clique em **Continuar**.

![Journey Optimizer](./images/s7.png)

Clique em **Importar**.

![Journey Optimizer](./images/23.8-50.png)

A Postman converteu automaticamente a variável **curl** em um comando REST pronto para ser acionado, basta pressionar o **Enviar** para solicitar a criação desse registro dentro do conjunto de dados.

![Journey Optimizer](./images/23.8-51.png)

Verifique se sua solicitação foi recebida com êxito. Procure um **200 OK** status no postman.

![Journey Optimizer](./images/s8.png)

O SMS pode levar alguns minutos para chegar em seu celular. Caso contrário, a **Interesse em Jackshirt da Fitness de Proteus** pode não conter um perfil com um celular correto. Em caso afirmativo, acesse o site Luma , visite o **Jaqueta da Fitness Proteus** registre-se e forneça o número de telefone celular correto.

![Journey Optimizer](./images/s9.png)

Terminou agora este exercício.

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao Módulo 10](./journeyoptimizer.md)

[Voltar para todos os módulos](../../overview.md)
