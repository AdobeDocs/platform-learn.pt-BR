---
title: Adobe Journey Optimizer - Configurar uma jornada com base em acionador - Confirmação de pedido
description: Nesta seção, você configurará uma jornada baseada em acionador - Confirmação de pedido
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '1998'
ht-degree: 0%

---

# 3.4.1 Configurar uma jornada com base em acionador - Confirmação de pedido

Faça login no Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`. Para alterar a sandbox, clique em **Produção (VA7)** e selecione a sandbox na lista. Neste exemplo, a sandbox é chamada de **AEP Enablement FY22**. Você estará na exibição **Página inicial** da sua sandbox `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

## 3.4.1.1 Criar o evento

No menu, vá para **Configurações** e clique em **Gerenciar** em **Eventos**.

![Journey Optimizer](./images/oc30.png)

Na tela **Eventos**, você verá um modo de exibição semelhante a este. Clique em **Criar Evento**.

![Journey Optimizer](./images/oc31.png)

Em seguida, você verá uma configuração de evento vazia.

![Journey Optimizer](./images/oc32.png)

Primeiro, dê ao seu Evento um Nome como este: `--aepUserLdap--PurchaseEvent`, e adicione uma descrição como esta: `Purchase Event`.

![Journey Optimizer](./images/oc34.png)

A seguir está a seleção **Tipo de Evento**. Selecione **Unitário**.

![Journey Optimizer](./images/eventidtype1.png)

A seguir está a seleção **Tipo de ID de Evento**. Selecionar **Sistema Gerado**

![Journey Optimizer](./images/eventidtype.png)

O próximo é a seleção Esquema. Um esquema foi preparado para este exercício. Use o esquema `Demo System - Event Schema for Website (Global v1.1) v.1`.

![Journey Optimizer](./images/oc35.png)

Depois de selecionar o esquema, você verá vários campos sendo selecionados na seção **Carga**. Clique no ícone **Editar/Lápis** para adicionar outros campos a este evento.

![Journey Optimizer](./images/oc36.png)

Você então verá esse pop-up. Agora é necessário marcar caixas de seleção adicionais para acessar dados adicionais quando esse evento for acionado.

![Journey Optimizer](./images/oc37.png)

Primeiro, marque a caixa de seleção na linha `--aepTenantId--`.

![Journey Optimizer](./images/oc38.png)

Em seguida, role para baixo e marque a caixa de seleção na linha `productListItems`.

![Journey Optimizer](./images/oc39.png)

Em seguida, role para baixo e marque a caixa de seleção na linha `commerce`.

![Journey Optimizer](./images/oc391.png)

Em seguida, clique em **Ok**.

Você verá que campos adicionais foram adicionados ao evento. Clique em **Salvar**.

![Journey Optimizer](./images/oc40.png)

O novo evento será compartilhado e você verá seu evento na lista de eventos disponíveis agora.

Clique no evento novamente para abrir a tela **Editar Evento** novamente.
Passe o mouse sobre o campo **Carga** novamente para ver os 3 ícones novamente. Clique no ícone **Exibir carga**.

![Journey Optimizer](./images/oc41.png)

Agora você verá um exemplo da carga útil esperada. Seu evento tem uma eventID de orquestração exclusiva, que você pode encontrar rolando para baixo nessa carga até ver `_experience.campaign.orchestration.eventID`.

![Journey Optimizer](./images/oc42.png)

A ID do evento é o que precisa ser enviado para o Adobe Journey Optimizer para acionar a jornada que você criará na próxima etapa. Anote essa eventID, pois ela será necessária em uma das próximas etapas.
`"eventID": "ef6dd943c94fe1b4763c098ccd1772344662f2a9f614513106cb5ada8be36857"`

Clique em **Ok**, seguido de **Cancelar**.

Seu evento agora está configurado e pronto para ser usado.

## 3.4.1.2 Criar a jornada

No menu, vá para **Jornadas** e clique em **Criar Jornada**.

![Journey Optimizer](./images/oc43.png)

Você verá isso. Dê um nome à sua jornada. Usar `--aepUserLdap-- - Order Confirmation journey`. Clique em **OK**.

![Journey Optimizer](./images/oc45.png)

Primeiro, é necessário adicionar o evento como ponto de partida da jornada. Procure seu evento `--aepUserLdap--PurchaseEvent` e arraste-o e solte-o na tela. Clique em **OK**.

![Journey Optimizer](./images/oc46.png)

Em seguida, em **Ações**, pesquise a ação **Email** e adicione-a à tela.

![Journey Optimizer](./images/oc47.png)

Defina a **Categoria** como **Marketing** e selecione uma superfície de email que permita o envio de emails. Nesse caso, a superfície de email a ser selecionada é **Email**. Verifique se as caixas de seleção para **Cliques no email** e **aberturas de email** estão habilitadas.

![ACOP](./images/journeyactions1.png)

A próxima etapa é criar a mensagem. Para fazer isso, clique em **Editar conteúdo**.

![ACOP](./images/journeyactions2.png)

Agora vocês podem ver isso. Clique no campo de texto **Linha de assunto**.

![ACOP](./images/journeyactions3.png)

Na área de texto comece a gravar **Obrigado por seu pedido,**

![Journey Optimizer](./images/oc5.png)

A linha de assunto ainda não foi terminada. Em seguida, você precisa trazer o token de personalização para o campo **Nome**, que é armazenado em `profile.person.name.firstName`. No menu esquerdo, role para baixo para localizar o campo **Pessoa** > **Nome completo** > **Nome** e clique no ícone **+** para adicionar o token de personalização à linha de assunto. Clique em **Salvar**.

![Journey Optimizer](./images/oc6.png)

Você estará de volta aqui. Clique em **Email do Designer** para criar o conteúdo do email.

![Journey Optimizer](./images/oc7.png)

Na próxima tela, clique em **Design do zero**.

![Journey Optimizer](./images/oc8.png)

No menu esquerdo, você encontrará os componentes de estrutura que podem ser usados para definir a estrutura do email (linhas e colunas).

Arraste e solte 8 vezes uma **coluna 1:1** na tela, o que deve fornecer a você:

![Journey Optimizer](./images/oc9.png)

Ir para **Componentes do Conteúdo**.

![Journey Optimizer](./images/oc10.png)

Arraste e solte um componente **Imagem** na primeira linha. Clique em **Procurar**.

![Journey Optimizer](./images/oc11.png)

Vá para a pasta **enablement-assets**, selecione o arquivo **luma-logo.png** e clique em **Selecionar**.

![Journey Optimizer](./images/oc12.png)

Agora você está de volta aqui. Clique na imagem para selecioná-la e, em seguida, use o controle deslizante **Tamanho** para tornar a imagem de logotipo um pouco menor.

![Journey Optimizer](./images/oc13.png)

Vá para **Componentes do Conteúdo** e arraste e solte um componente de **Imagem** na segunda linha. Selecione o **componente de Imagem**, mas NÃO clique em Procurar.

![Journey Optimizer](./images/oc15.png)

Cole esta URL de imagem no campo **Source**: `https://parsefiles.back4app.com/hgJBdVOS2eff03JCn6qXXOxT5jJFzialLAHJixD9/29043bedcde632a9cbe8a02a164189c9_preparing.png`. Esta imagem está hospedada fora do Adobe.

![Journey Optimizer](./images/oc14.png)

Ao alterar o escopo para outro campo, a imagem será renderizada e você verá o seguinte:

![Journey Optimizer](./images/oc16.png)

Em seguida, vá para **Componentes do Conteúdo** e arraste e solte um componente de **Texto** na terceira linha.

![Journey Optimizer](./images/oc17.png)

Selecione o texto padrão nesse componente **Digite o texto aqui.** e substitua-o pelo texto abaixo:

```javascript
You’re one step closer!

Hi 

We've received your order details!

We will also send you a separate email containing your VAT Invoice.

We'll be back in touch with you as soon as we've finished packing your package. Please read carefully the Order Information detailed below.
```

![Journey Optimizer](./images/oc18.png)

Coloque o cursor próximo ao texto **Hi** e clique em **Adicionar Personalization**.

![Journey Optimizer](./images/oc19.png)

Navegue até o campo **Pessoa** > **Nome completo** > **Nome** e clique no ícone **+** para adicionar o token de personalização à linha de assunto. Clique em **Salvar**.

![Journey Optimizer](./images/oc20.png)

Você verá isto:

![Journey Optimizer](./images/oc21.png)

Em seguida, vá para **Componentes do Conteúdo** e arraste e solte um componente de **Texto** na quarta linha.

![Journey Optimizer](./images/oc22.png)

Selecione o texto padrão nesse componente **Digite o texto aqui.** e substitua-o pelo texto abaixo:

`Order Information`

Altere o tamanho da fonte para **26px** e centralize o texto nesta célula. Você terá isto:

![Journey Optimizer](./images/oc23.png)

Em seguida, vá para **Componentes do Conteúdo** e arraste e solte um componente **HTML** na quinta linha. Clique no componente HTML e em **Mostrar o código-fonte**.

![Journey Optimizer](./images/oc24.png)

No pop-up **Editar HTML**, cole esta HTML:

```<table><tbody><tr><td><b>Items purchased</b></td><td></td><td><b>Quantity</b></td><td><b>Subtotal</b></td></tr><tr><td colspan="4" width="500"><hr></td></tr></tbody></table>```

Clique em **Salvar**.

![Journey Optimizer](./images/oc25.png)

Então você terá isto. Clique em **Salvar** para salvar seu progresso.

![Journey Optimizer](./images/oc26.png)

Vá para **Componentes do Conteúdo** e arraste e solte um componente **HTML** na sexta linha. Clique no componente HTML e em **Mostrar o código-fonte**.

![Journey Optimizer](./images/oc57.png)

No pop-up **Editar HTML**, cole esta HTML:

```{{#each xxx as |item|}}<table width="500"><tbody><tr><td><img src="{{item.--aepTenantId--.core.imageURL}}" width="100"></td><td><table><tbody><tr><td><b>{{item.name}}</b><br>{{item.--aepTenantId--.core.subCategory}}<br><b>{{item.priceTotal}}</b><br>&nbsp;<br>Article no: {{item.SKU}}</td></tr></tbody></table></td><td>{{item.quantity}}</td><td><b>{{item.priceTotal}}</b></td></tr></tbody></table>{{/each}}```

Você terá isto:

![Journey Optimizer](./images/oc58.png)

Agora é necessário substituir **xxx** por uma referência ao objeto productListItems que faz parte do evento que aciona a jornada.

![Journey Optimizer](./images/oc59.png)

Primeiro, exclua **xxx** em seu código de HTML.

![Journey Optimizer](./images/oc60.png)

No menu esquerdo, clique em **Atributos contextuais**. Esse contexto é transmitido para a mensagem da jornada.

![Journey Optimizer](./images/oc601.png)

Você verá isso. Clique na seta ao lado de **Journey Orchestration** para detalhar.

![Journey Optimizer](./images/oc61.png)

Clique na seta ao lado de **Eventos** para detalhar.

![Journey Optimizer](./images/oc62.png)

Clique na seta ao lado de `--aepUserLdap--PurchaseEvent` para detalhar.

![Journey Optimizer](./images/oc63.png)

Clique na seta ao lado de **productListItems** para detalhar.

![Journey Optimizer](./images/oc64.png)

Clique no ícone **+** ao lado de **Nome** para adicioná-lo à tela. Então você terá isto. Agora é necessário selecionar **.name** conforme indicado na captura de tela abaixo e remover **.name**.

![Journey Optimizer](./images/oc65.png)

Então você terá isto. Clique em **Salvar**.

![Journey Optimizer](./images/oc66.png)

Você voltará para a Designer de email agora. Clique em **Salvar** para salvar seu progresso.

![Journey Optimizer](./images/oc67.png)

Em seguida, vá para **Componentes do Conteúdo** e arraste e solte um componente **HTML** na sétima linha. Clique no componente HTML e em **Mostrar o código-fonte**.

![Journey Optimizer](./images/oc68.png)

No pop-up **Editar HTML**, cole esta HTML:

```<table><tbody><tr><td><b>Subtotal</b><br>Delivery charge (included)</td><td align="right"><b>xxx</b><br><b>5</b></td></tr><tr><td colspan="2" width="500"><hr></td></tr><tr><td><b>Total including VAT</b></td><td align="right"><b>xxx</b></td></tr></tbody></table>```

Há duas referências de **xxx** neste código de HTML. Agora é necessário substituir cada **xxx** por uma referência ao objeto productListItems que faz parte do evento que aciona a jornada.

![Journey Optimizer](./images/oc69.png)

Primeiro, exclua o primeiro **xxx** do código HTML.

![Journey Optimizer](./images/oc71.png)

No menu esquerdo, clique em **Atributos contextuais**.

![Journey Optimizer](./images/oc711.png)

Clique na seta ao lado de **Journey Orchestration** para detalhar.

![Journey Optimizer](./images/oc72.png)

Clique na seta ao lado de **Eventos** para detalhar.

![Journey Optimizer](./images/oc722.png)

Clique na seta ao lado de `--aepUserLdap--PurchaseEvent` para detalhar.

![Journey Optimizer](./images/oc73.png)

Clique na seta ao lado de **Commerce** para detalhar.

![Journey Optimizer](./images/oc733.png)

Clique na seta ao lado de **Ordem** para detalhar.

![Journey Optimizer](./images/oc74.png)

Clique no ícone **+** ao lado de **Preço total** para adicioná-lo à tela.

![Journey Optimizer](./images/oc75.png)

Então você terá isto. Agora exclua o segundo **xxx** do código HTML.

![Journey Optimizer](./images/oc76.png)

Clique no ícone **+** ao lado de **Preço total** novamente para adicioná-lo à tela.

![Journey Optimizer](./images/oc77.png)

Você também pode adicionar o campo **Moeda** de dentro do objeto **Ordem** na tela, como pode ver aqui.
Quando terminar, clique em **Salvar** para salvar suas alterações.

![Journey Optimizer](./images/oc771.png)

Você voltará para a Designer de email. Clique em **Salvar** novamente.

![Journey Optimizer](./images/oc78.png)

Volte para o painel da mensagem clicando na **seta** ao lado do texto da linha de assunto no canto superior esquerdo.

![Journey Optimizer](./images/oc79.png)

Clique na seta no canto superior esquerdo para voltar à jornada.

![Journey Optimizer](./images/oc79a.png)

Clique em **Ok** para fechar sua ação de email.

![Journey Optimizer](./images/oc79b.png)

Clique em **Publish** para publicar sua jornada.

![Journey Optimizer](./images/oc511.png)

Clique novamente em **Publish**.

![Journey Optimizer](./images/oc512.png)

Sua jornada foi publicada.

![Journey Optimizer](./images/oc513.png)

## 3.4.1.5 Atualizar a propriedade do Cliente de coleta de dados do Adobe Experience Platform

Vá para [Coleção de dados do Adobe Experience Platform](https://experience.adobe.com/launch/) e selecione **Marcas**.

Esta é a página Propriedades da coleção de dados do Adobe Experience Platform que você viu antes.

![Página de propriedades](./../../../modules/datacollection/module1.1/images/launch1.png)

No módulo 0, o Sistema de demonstração criou duas propriedades do cliente para você: uma para o site e outra para o aplicativo móvel. Localize-os procurando por `--aepUserLdap--` na caixa **[!UICONTROL Pesquisar]**. Clique para abrir a propriedade **Web**.

![Caixa de pesquisa](./../../../modules/datacollection/module1.1/images/property6.png)

Vá para **Elementos de Dados**. Pesquise e abra o elemento de dados **XDM - Purchase**.

![Journey Optimizer](./images/oc91.png)

Você verá isso. Navegue até o campo **_experience.campaign.orchestration.eventID** e preencha sua eventID aqui. A eventID a ser preenchida aqui é a eventID criada como parte do exercício 10.1.2. Clique em **Salvar** ou **Salvar na Biblioteca**.

![Journey Optimizer](./images/oc92.png)

Salve as alterações na propriedade do cliente e publique-as atualizando a biblioteca de desenvolvimento.

![Journey Optimizer](./images/oc93.png)

Suas alterações agora estão implantadas e podem ser testadas.

## 3.4.1.6 Teste o email de confirmação do seu pedido usando o site de demonstração

Vamos testar a jornada atualizada comprando um produto no site de demonstração.

Ir para [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Depois de fazer logon com sua Adobe ID, você verá isso. Clique no projeto do site para abri-lo.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

Na página **Screens**, clique em **Executar**.

![DSN](./../../../modules/datacollection/module1.1/images/web2.png)

Você verá seu site de demonstração aberto. Selecione o URL e copie-o para a área de transferência.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web3.png)

Abra uma nova janela incógnita do navegador.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web4.png)

Cole o URL do site de demonstração que você copiou na etapa anterior. Você será solicitado a fazer logon usando sua Adobe ID.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web5.png)

Selecione o tipo de conta e conclua o processo de logon.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web6.png)

Em seguida, você verá seu site carregado em uma janela incógnita do navegador. Para cada demonstração, será necessário usar uma janela do navegador nova e incógnita para carregar o URL do site de demonstração.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web7.png)

Clique no ícone do logotipo do Adobe no canto superior esquerdo da tela para abrir o Visualizador de perfis.

![Demonstração](./../../../modules/datacollection/module1.2/images/pv1.png)

Consulte o painel Visualizador de perfis e o Perfil do cliente em tempo real com a **ID de Experience Cloud** como o identificador principal para este cliente atualmente desconhecido.

![Demonstração](./../../../modules/datacollection/module1.2/images/pv2.png)

Vá para a página Registro/Logon. Clique em **CRIAR UMA CONTA**.

![Demonstração](./../../../modules/datacollection/module1.2/images/pv9.png)

Preencha seus detalhes e clique em **Registrar**; depois disso, você será redirecionado para a página anterior.

![Demonstração](./../../../modules/datacollection/module1.2/images/pv10.png)

Adicione qualquer produto ao carrinho e vá para a página **Carrinho**. Clique em **Prosseguir para o check-out**.

![Journey Optimizer](./images/cart1.png)

Em seguida, verifique os campos na página de check-out e clique em **Check-out**.

![Journey Optimizer](./images/cart2.png)

Em seguida, você receberá o email de confirmação do pedido em segundos.

![Journey Optimizer](./images/oc98.png)

Você concluiu este exercício.

Próxima etapa: [3.4.2 Configurar uma jornada de informativo baseada em lote](./ex2.md)

[Voltar ao módulo 3.4](./journeyoptimizer.md)

[Voltar a todos os módulos](../../../overview.md)
