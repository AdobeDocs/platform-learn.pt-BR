---
title: Adobe Journey Optimizer - Configurar uma jornada com base em acionador - Confirmação de pedido
description: Nesta seção, você configurará uma jornada baseada em acionador - Confirmação de pedido
kt: 5342
doc-type: tutorial
exl-id: e8cf1274-2a18-4870-b1e3-378e1779fac1
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '1922'
ht-degree: 1%

---

# 3.4.1 Configurar uma jornada com base em acionador - Confirmação de pedido

Faça login no Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`. Você estará na exibição **Página inicial** da sua sandbox `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## 3.4.1.1 Criar o evento

No menu, vá para **Configurações** e clique em **Gerenciar** em **Eventos**.

![Journey Optimizer](./images/oc30.png)

Na tela **Eventos**, você verá um modo de exibição semelhante a este. Clique em **Criar Evento**.

![Journey Optimizer](./images/oc31.png)

Em seguida, você verá uma configuração de evento vazia.

Primeiro, dê ao seu Evento um Nome como este: `--aepUserLdap--PurchaseEvent`, e adicione uma descrição como esta: `Purchase Event`.

Para **Type**, selecione **Unitary**.
Para o **Tipo de ID do Evento**, selecione **Gerado pelo Sistema**.

![Journey Optimizer](./images/eventidtype.png)

O próximo é a seleção Esquema. Um esquema foi preparado para este exercício. Use o esquema `Demo System - Event Schema for Website (Global v1.1) v.1`.

Depois de selecionar o esquema, você verá vários campos sendo selecionados na seção **Carga**. Clique no ícone **Editar/Lápis** para adicionar outros campos a este evento.

![Journey Optimizer](./images/oc36.png)

Você então verá esse pop-up. Agora é necessário marcar caixas de seleção adicionais para acessar dados adicionais quando esse evento for acionado.

![Journey Optimizer](./images/oc37.png)

Primeiro, marque a caixa de seleção na linha `--aepTenantId--`.

![Journey Optimizer](./images/oc38.png)

Em seguida, role para baixo e marque a caixa de seleção na linha `commerce`.

![Journey Optimizer](./images/oc391.png)

Em seguida, role para baixo e marque a caixa de seleção na linha `productListItems`. Clique em **Ok**.

![Journey Optimizer](./images/oc39.png)

Você verá que campos adicionais foram adicionados ao evento. Clique em **Salvar**.

![Journey Optimizer](./images/oc40.png)

O novo evento será salvo e você verá seu evento na lista de eventos disponíveis agora.

Clique no evento novamente para abrir a tela **Editar Evento** novamente.
Passe o mouse sobre o campo **Carga** novamente para ver os 3 ícones novamente. Clique no ícone **Exibir carga**.

![Journey Optimizer](./images/oc41.png)

Agora você verá um exemplo da carga útil esperada. Seu evento tem uma eventID de orquestração exclusiva, que você pode encontrar rolando para baixo nessa carga até ver `_experience.campaign.orchestration.eventID`.

![Journey Optimizer](./images/oc42.png)

A ID do evento é o que precisa ser enviado para o Adobe Journey Optimizer para acionar a jornada que você criará na próxima etapa. Anote essa eventID, pois ela será necessária em uma das próximas etapas.
`"eventID": "1c8148a8ab1993537d0ba4e6ac293dd4f2a88d80b2ca7be6293c3b28d4ff5ae6"`

Clique em **Ok**, seguido de **Cancelar**.

Seu evento agora está configurado e pronto para ser usado.

## 3.4.1.2 Criar a jornada

No menu, vá para **Jornadas** e clique em **Criar Jornada**.

![Journey Optimizer](./images/oc43.png)

Você verá isso. Dê um nome à sua jornada. Usar `--aepUserLdap-- - Order Confirmation journey`. Clique em **Salvar**.

![Journey Optimizer](./images/oc45.png)

Primeiro, é necessário adicionar o evento como ponto de partida da jornada. Procure seu evento `--aepUserLdap--PurchaseEvent` e arraste-o e solte-o na tela. Clique em **Salvar**.

![Journey Optimizer](./images/oc46.png)

Em seguida, em **Ações**, pesquise a ação **Email** e adicione-a à tela.

![Journey Optimizer](./images/oc47.png)

Defina a **Categoria** como **Marketing** e selecione uma superfície de email que permita o envio de emails. Nesse caso, a superfície de email a ser selecionada é **Email**. Verifique se as caixas de seleção para **Cliques no email** e **aberturas de email** estão habilitadas.

![ACOP](./images/journeyactions1.png)

A próxima etapa é criar a mensagem. Para fazer isso, clique em **Editar conteúdo**.

![ACOP](./images/journeyactions2.png)

Agora vocês podem ver isso. Clique no campo de texto **Linha de assunto**.

![ACOP](./images/journeyactions3.png)

Na área de texto, comece a gravar **Obrigado por seu pedido** e clique no ícone **Personalization**.

![Journey Optimizer](./images/oc5.png)

A linha de assunto ainda não foi terminada. Em seguida, você precisa trazer o token de personalização para o campo **Nome**, que é armazenado em `profile.person.name.firstName`. No menu esquerdo, role para baixo para localizar o campo **Pessoa** > **Nome completo** > **Nome** e clique no ícone **+** para adicionar o token de personalização à linha de assunto. Clique em **Salvar**.

![Journey Optimizer](./images/oc6.png)

Você estará de volta aqui. Clique em **Editar corpo do email** para criar o conteúdo do email.

![Journey Optimizer](./images/oc7.png)

Na próxima tela, clique em **Design do zero**.

![Journey Optimizer](./images/oc8.png)

No menu esquerdo, você encontrará os componentes de estrutura que podem ser usados para definir a estrutura do email (linhas e colunas).

Arraste e solte 8 vezes uma **coluna 1:1** na tela, o que deve fornecer a você:

![Journey Optimizer](./images/oc9.png)

No menu esquerdo, vá para **Fragmentos**. Arraste o cabeçalho criado anteriormente no [exercício 3.1.2.1](./../ajob2c-1/ex2.md) até o primeiro componente na tela. Arraste o rodapé criado anteriormente no [exercício 3.1.2.2](./../ajob2c-1/ex2.md) até o último componente na tela.

![Journey Optimizer](./images/fragm1.png)

Clique no ícone **+** no menu esquerdo. Vá para **Conteúdo** para começar a adicionar conteúdo à tela.

![Journey Optimizer](./images/oc10.png)

Vá para **Conteúdo** e arraste e solte um componente **Imagem** na segunda linha. Clique em **Procurar**.

![Journey Optimizer](./images/oc15.png)

Abra a pasta **citisignal-images**, clique para selecionar a imagem **citisignal-preparation.png** e clique em **Selecionar**.

![Journey Optimizer](./images/oc14.png)

Em **Estilos**, altere a largura para **40%**.

![Journey Optimizer](./images/oc14a.png)

Em seguida, vá para **Conteúdo** e arraste e solte um componente de **Texto** na terceira linha.

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

Em seguida, vá para **Conteúdo** e arraste e solte um componente de **Texto** na quarta linha.

![Journey Optimizer](./images/oc22.png)

Selecione o texto padrão nesse componente **Digite o texto aqui.** e substitua-o pelo texto abaixo:

`Order Information`

Altere o tamanho da fonte para **26px** e centralize o texto nesta célula. Você terá isto:

![Journey Optimizer](./images/oc23.png)

Em seguida, vá para **Conteúdo** e arraste e solte um componente do **HTML** na quinta linha. Clique no componente HTML e em **Mostrar o código-fonte**.

![Journey Optimizer](./images/oc24.png)

No pop-up **Editar HTML**, cole esta HTML:

```<table><tbody><tr><td><b>Items purchased</b></td><td></td><td><b>Quantity</b></td><td><b>Subtotal</b></td></tr><tr><td colspan="4" width="500"><hr></td></tr></tbody></table>```

Clique em **Salvar**.

![Journey Optimizer](./images/oc25.png)

Então você terá isto. Clique em **Salvar** para salvar seu progresso.

![Journey Optimizer](./images/oc26.png)

Vá para **Conteúdo** e arraste e solte um componente do **HTML** na sexta linha. Clique no componente HTML e em **Mostrar o código-fonte**.

![Journey Optimizer](./images/oc57.png)

No pop-up **Editar HTML**, cole esta HTML:

```{{#each xxx as |item|}}<table width="500"><tbody><tr><td><img src="{{item.--aepTenantId--.core.imageURL}}" width="100"></td><td><table><tbody><tr><td><b>{{item.name}}</b><br>{{item.--aepTenantId--.core.subCategory}}<br><b>{{item.priceTotal}}</b><br>&nbsp;<br>Article no: {{item.SKU}}</td></tr></tbody></table></td><td>{{item.quantity}}</td><td><b>{{item.priceTotal}}</b></td></tr></tbody></table>{{/each}}```

Você terá isto:

![Journey Optimizer](./images/oc58.png)

Agora é necessário substituir **xxx** por uma referência ao objeto productListItems que faz parte do evento que aciona a jornada.

![Journey Optimizer](./images/oc59.png)

Primeiro, exclua **xxx** em seu código HTML primeiro.

![Journey Optimizer](./images/oc60.png)

No menu esquerdo, clique em **Atributos contextuais**. Esse contexto é transmitido para a mensagem da jornada.

Você verá isso. Clique na seta ao lado de **Journey Orchestration** para detalhar.

![Journey Optimizer](./images/oc601.png)

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

Em seguida, vá para **Conteúdo** e arraste e solte um componente do **HTML** na sétima linha. Clique no componente HTML e em **Mostrar o código-fonte**.

![Journey Optimizer](./images/oc68.png)

No pop-up **Editar HTML**, cole esta HTML:

```<table><tbody><tr><td><b>Subtotal</b><br>Delivery charge (included)</td><td align="right"><b>xxx</b><br><b>5</b></td></tr><tr><td colspan="2" width="500"><hr></td></tr><tr><td><b>Total including VAT</b></td><td align="right"><b>xxx</b></td></tr></tbody></table>```

Há duas referências de **xxx** neste código HTML. Agora é necessário substituir cada **xxx** por uma referência ao objeto productListItems que faz parte do evento que aciona a jornada.

![Journey Optimizer](./images/oc69.png)

Primeiro, exclua o primeiro **xxx** do código HTML.

![Journey Optimizer](./images/oc71.png)

No menu esquerdo, clique em **Atributos contextuais**.
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

Então você terá isto. Agora exclua o segundo **xxx** do seu código HTML.

![Journey Optimizer](./images/oc76.png)

Clique no ícone **+** ao lado de **Preço total** novamente para adicioná-lo à tela.
Você também pode adicionar o campo **Moeda** de dentro do objeto **Ordem** na tela, como pode ver aqui.
Quando terminar, clique em **Salvar** para salvar suas alterações.

![Journey Optimizer](./images/oc77.png)

Você voltará para a Designer de email. Clique em **Salvar** novamente.

![Journey Optimizer](./images/oc78.png)

Volte para o painel da mensagem clicando na **seta** ao lado do texto da linha de assunto no canto superior esquerdo.

![Journey Optimizer](./images/oc79.png)

Clique na seta no canto superior esquerdo para voltar à jornada.

![Journey Optimizer](./images/oc79a.png)

Clique em **Salvar** para fechar sua ação de email.

![Journey Optimizer](./images/oc79b.png)

Clique em **Publicar** para publicar sua jornada.

![Journey Optimizer](./images/oc511.png)

Clique novamente em **Publicar**.

![Journey Optimizer](./images/oc512.png)

Sua jornada foi publicada.

![Journey Optimizer](./images/oc513.png)

## 3.4.1.5 Atualizar a propriedade do Cliente de coleta de dados do Adobe Experience Platform

Vá para [Coleção de dados do Adobe Experience Platform](https://experience.adobe.com/launch/) e selecione **Marcas**.

Esta é a página Propriedades da coleção de dados do Adobe Experience Platform que você viu antes.

![Página de propriedades](./../../../../modules/delivery-activation/datacollection/dc1.1/images/launch1.png)

Em **Introdução**, o Sistema de Demonstração criou duas propriedades do Cliente para você: uma para o site e outra para o aplicativo móvel. Localize-os procurando por `--aepUserLdap--` na caixa **[!UICONTROL Pesquisar]**. Clique para abrir a propriedade **Web**.

![Caixa de pesquisa](./../../../../modules/delivery-activation/datacollection/dc1.1/images/property6.png)

Vá para **Elementos de Dados**. Pesquise e abra o elemento de dados **XDM - Purchase**.

![Journey Optimizer](./images/oc91.png)

Você verá isso. Navegue até o campo **_experience.campaign.orchestration.eventID** e preencha sua eventID aqui. A eventID a ser preenchida aqui é a eventID que você criou como parte do exercício 3.4.1.1 Clique em **Salvar** ou **Salvar na biblioteca**.

![Journey Optimizer](./images/oc92.png)

Salve as alterações na propriedade e publique as alterações atualizando a biblioteca de desenvolvimento.

![Journey Optimizer](./images/oc93.png)

Suas alterações agora estão implantadas e podem ser testadas.

## 3.4.1.6 Teste o email de confirmação do seu pedido usando o site de demonstração

Vamos testar a jornada atualizada comprando um produto no site de demonstração.

Ir para [https://dsn.adobe.com](https://dsn.adobe.com). Depois de fazer logon com sua Adobe ID, você verá isso. Clique nos 3 pontos **...** do projeto do site e clique em **Executar** para abri-lo.

![DSN](./../../datacollection/dc1.1/images/web8.png)

Você verá seu site de demonstração aberto. Selecione o URL e copie-o para a área de transferência.

![DSN](../../../getting-started/gettingstarted/images/web3.png)

Abra uma nova janela incógnita do navegador.

![DSN](../../../getting-started/gettingstarted/images/web4.png)

Cole o URL do site de demonstração que você copiou na etapa anterior. Você será solicitado a fazer logon usando sua Adobe ID.

![DSN](../../../getting-started/gettingstarted/images/web5.png)

Selecione o tipo de conta e conclua o processo de logon.

![DSN](../../../getting-started/gettingstarted/images/web6.png)

Em seguida, você verá seu site carregado em uma janela incógnita do navegador. Para cada exercício, será necessário usar uma janela do navegador nova e incógnita para carregar o URL do site de demonstração.

![DSN](../../../getting-started/gettingstarted/images/web7.png)

Consulte o painel Visualizador de perfis e o Perfil do cliente em tempo real com a **Experience Cloud ID** como o identificador principal para este cliente atualmente desconhecido.

![Demonstração](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv2.png)

Vá para a página Registro/Logon. Clique em **CRIAR UMA CONTA**.

![Demonstração](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv9.png)

Preencha seus detalhes e clique em **Registrar**; depois disso, você será redirecionado para a página anterior.

![Demonstração](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv10.png)

Adicionar qualquer produto ao carrinho

![Journey Optimizer](./images/cart1a.png)

Vá para a página **Carrinho**. Clique em **Check-out**.

![Journey Optimizer](./images/cart1.png)

Em seguida, verifique os campos e preencha se necessário. Clique em **Continuar**.

![Journey Optimizer](./images/cart2.png)

Clique em **Confirmar Pedido**.

![Journey Optimizer](./images/cart2a.png)

Seu pedido foi confirmado.

![Journey Optimizer](./images/cart2b.png)

Em seguida, você receberá o email de confirmação do pedido em segundos.

![Journey Optimizer](./images/oc98.png)

Você concluiu este exercício.

## Próximas etapas

Ir para [3.4.2 Configurar uma jornada de informativo baseada em lote](./ex2.md){target="_blank"}

Voltar para [Adobe Journey Optimizer](journeyoptimizer.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
