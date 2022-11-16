---
title: Adobe Journey Optimizer - Configurar uma jornada baseada em acionador - Confirmação de pedido
description: Nesta seção, você configurará uma jornada baseada em acionador - Confirmação de pedido
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 69bb9eca-3942-4c31-a3d2-0b218143e1eb
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1988'
ht-degree: 9%

---

# 10.1 Configurar uma jornada baseada em acionador - Confirmação de pedido

Faça logon no Adobe Journey Optimizer acessando [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Você será redirecionado para o **Início**  no Journey Optimizer. Primeiro, certifique-se de usar a sandbox correta. A sandbox a ser usada é chamada de `--aepSandboxId--`. Para alterar de uma sandbox para outra, clique em **Produto de produção (VA7)** e selecione a sandbox na lista. Neste exemplo, a sandbox é chamada de **Ativação AEP FY22**. Você estará no **Início** exibição da sandbox `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

## 10.1.1 Criar seu evento

No menu , acesse **Configurações** e clique em **Gerenciar** under **Eventos**.

![Journey Optimizer](./images/oc30.png)

No **Eventos** , você verá uma exibição semelhante a esta. Clique em **Criar evento**.

![Journey Optimizer](./images/oc31.png)

Em seguida, você verá uma configuração de evento vazia.

![Journey Optimizer](./images/oc32.png)

Primeiro de tudo, dê a seu Evento um Nome como este: `--demoProfileLdap--PurchaseEvent`e adicione uma descrição como esta: `Purchase Event`.

![Journey Optimizer](./images/oc34.png)

O próximo é o **Tipo de evento** seleção. Selecionar **Unitário**.

![Journey Optimizer](./images/eventidtype1.png)

O próximo é o **Tipo de ID do evento** seleção. Selecionar **Sistema gerado**

![Journey Optimizer](./images/eventidtype.png)

Em seguida está a seleção Esquema. Um esquema foi preparado para este exercício. Use o esquema `Demo System - Event Schema for Website (Global v1.1) v.1`.

![Journey Optimizer](./images/oc35.png)

Após selecionar o Esquema, você verá vários campos sendo selecionados na variável **Carga** seção. Clique no botão **Editar/Lápis** para adicionar campos adicionais a esse evento.

![Journey Optimizer](./images/oc36.png)

Você verá esse pop-up. Agora é necessário marcar caixas de seleção adicionais para acessar dados adicionais quando esse evento for acionado.

![Journey Optimizer](./images/oc37.png)

Primeiro de tudo, marque a caixa de seleção na linha `--aepTenantId--`.

![Journey Optimizer](./images/oc38.png)

Em seguida, role para baixo e marque a caixa de seleção na linha `productListItems`.

![Journey Optimizer](./images/oc39.png)

Em seguida, role para baixo e marque a caixa de seleção na linha `commerce`.

![Journey Optimizer](./images/oc391.png)

Em seguida, clique em **Ok**.

Você verá que campos adicionais foram adicionados ao evento. Clique em **Salvar**.

![Journey Optimizer](./images/oc40.png)

O novo evento é compartilhado e você verá o evento na lista de eventos disponíveis agora.

Clique no seu evento novamente para abrir o **Editar evento** novamente.
Passe o mouse sobre **Carga** novamente para ver os 3 ícones novamente. Clique no botão **Exibir carga** ícone .

![Journey Optimizer](./images/oc41.png)

Você verá um exemplo da carga esperada. Seu evento tem uma orquestration eventID exclusiva, que pode ser encontrada ao rolar para baixo na carga útil até que você veja `_experience.campaign.orchestration.eventID`.

![Journey Optimizer](./images/oc42.png)

A ID de evento é o que precisa ser enviado para o Adobe Journey Optimizer para acionar a jornada que você criará na próxima etapa. Anote essa eventID, pois ela será necessária em uma das próximas etapas.
`"eventID": "ef6dd943c94fe1b4763c098ccd1772344662f2a9f614513106cb5ada8be36857"`

Clique em **Ok**, seguida de **Cancelar**.

Seu evento agora está configurado e pronto para ser usado.

## 10.1.2 Criar a jornada

No menu , acesse **Jornada** e clique em **Criar Jornada**.

![Journey Optimizer](./images/oc43.png)

Você verá isso. Dê um nome à sua jornada. Use `--demoProfileLdap-- - Order Confirmation journey`. Clique em **OK**.

![Journey Optimizer](./images/oc45.png)

Primeiro, é necessário adicionar o evento como ponto de partida da jornada. Procure seu evento `--demoProfileLdap--PurchaseEvent` e arraste e solte na tela. Clique em **OK**.

![Journey Optimizer](./images/oc46.png)

Em seguida, em **Ações**, pesquise a **Email** e adicione-a à tela.

![Journey Optimizer](./images/oc47.png)

Defina as **Categoria** para **Marketing** e selecione uma superfície de email que permita enviar emails. Nesse caso, a superfície do email a ser selecionada é **Email**. Certifique-se de que as caixas de seleção de **Cliques no email** e **aberturas de email** estão ativadas.

![ACOP](./images/journeyactions1.png)

A próxima etapa é criar a mensagem. Para fazer isso, clique em **Editar conteúdo**.

![ACOP](./images/journeyactions2.png)

Agora você vê isso. Clique no botão **Linha de assunto** campo de texto.

![ACOP](./images/journeyactions3.png)

Na área de texto, comece a escrever **Obrigado pelo seu pedido.**

![Journey Optimizer](./images/oc5.png)

A linha de assunto ainda não foi feita. Em seguida, é necessário trazer o token de personalização para o campo **Nome** armazenado em `profile.person.name.firstName`. No menu esquerdo, role para baixo até encontrar a variável **Pessoa** > **Nome completo** >  **Nome** e clique no botão **+** ícone para adicionar o token de personalização na linha de assunto. Clique em **Salvar**.

![Journey Optimizer](./images/oc6.png)

Então você estará de volta. Clique em **Email Designer** para criar o conteúdo do email.

![Journey Optimizer](./images/oc7.png)

Na próxima tela, clique em **Design do zero**.

![Journey Optimizer](./images/oc8.png)

No menu esquerdo, você encontrará os componentes de estrutura que podem ser usados para definir a estrutura do email (linhas e colunas).

Arraste e solte 8 vezes a **Coluna 1:1** na tela, o que deve lhe dar o seguinte:

![Journey Optimizer](./images/oc9.png)

Ir para **Componentes de conteúdo**.

![Journey Optimizer](./images/oc10.png)

Arraste e solte um **Imagem** na primeira linha. Clique em **Procurar**.

![Journey Optimizer](./images/oc11.png)

Vá para a pasta **ativos de habilitação**, selecione o arquivo **luma-logo.png** e clique em **Selecionar**.

![Journey Optimizer](./images/oc12.png)

Você está de volta. Clique na imagem para selecioná-la e, em seguida, use a variável **Tamanho** controle deslizante para tornar a imagem do logotipo um pouco menor.

![Journey Optimizer](./images/oc13.png)

Ir para **Componentes de conteúdo** e arraste e solte uma **Imagem** na segunda linha. Selecione o **Componente de imagem** mas NÃO clique em Procurar.

![Journey Optimizer](./images/oc15.png)

Cole este URL de imagem no campo **Origem**: `https://parsefiles.back4app.com/hgJBdVOS2eff03JCn6qXXOxT5jJFzialLAHJixD9/29043bedcde632a9cbe8a02a164189c9_preparing.png`. Esta imagem é hospedada fora do Adobe.

![Journey Optimizer](./images/oc14.png)

Ao alterar o escopo para outro campo, a imagem será renderizada e você verá o seguinte:

![Journey Optimizer](./images/oc16.png)

Em seguida, acesse **Componentes de conteúdo** e arraste e solte uma **Texto** na terceira linha.

![Journey Optimizer](./images/oc17.png)

Selecionar o texto padrão nesse componente **Digite seu texto aqui.** e substituí-lo pelo texto abaixo:

```javascript
You’re one step closer!

Hi 

We've received your order details!

We will also send you a separate email containing your VAT Invoice.

We'll be back in touch with you as soon as we've finished packing your package. Please read carefully the Order Information detailed below.
```

![Journey Optimizer](./images/oc18.png)

Coloque o cursor próximo ao texto **Oi** e clique em **Adicionar personalização**.

![Journey Optimizer](./images/oc19.png)

Navegue até o **Pessoa** > **Nome completo** > **Nome** e clique no botão **+** ícone para adicionar o token de personalização na linha de assunto. Clique em **Salvar**.

![Journey Optimizer](./images/oc20.png)

Você verá isso:

![Journey Optimizer](./images/oc21.png)

Em seguida, acesse **Componentes de conteúdo** e arraste e solte uma **Texto** na quarta linha.

![Journey Optimizer](./images/oc22.png)

Selecionar o texto padrão nesse componente **Digite seu texto aqui.** e substituí-lo pelo texto abaixo:

`Order Information`

Altere o tamanho da fonte para **26px** e centralize o texto nesta célula. Você terá isso:

![Journey Optimizer](./images/oc23.png)

Em seguida, acesse **Componentes de conteúdo** e arraste e solte uma **HTML** na quinta linha. Clique no componente HTML e, em seguida, clique em **Mostrar o código-fonte**.

![Journey Optimizer](./images/oc24.png)

No **Editar HTML** pop-up, cole este HTML:

```<table><tbody><tr><td><b>Items purchased</b></td><td></td><td><b>Quantity</b></td><td><b>Subtotal</b></td></tr><tr><td colspan="4" width="500"><hr></td></tr></tbody></table>```

Clique em **Salvar**.

![Journey Optimizer](./images/oc25.png)

Você terá isso. Clique em **Salvar** para salvar seu progresso.

![Journey Optimizer](./images/oc26.png)

Ir para **Componentes de conteúdo** e arraste e solte uma **HTML** na sexta linha. Clique no componente HTML e, em seguida, clique em **Mostrar o código-fonte**.

![Journey Optimizer](./images/oc57.png)

No **Editar HTML** pop-up, cole este HTML:

```{{#each xxx as |item|}}<table width="500"><tbody><tr><td><img src="{{item.--aepTenantId--.core.imageURL}}" width="100"></td><td><table><tbody><tr><td><b>{{item.name}}</b><br>{{item.--aepTenantId--.core.subCategory}}<br><b>{{item.priceTotal}}</b><br>&nbsp;<br>Article no: {{item.SKU}}</td></tr></tbody></table></td><td>{{item.quantity}}</td><td><b>{{item.priceTotal}}</b></td></tr></tbody></table>{{/each}}```

Você terá isso:

![Journey Optimizer](./images/oc58.png)

Agora é necessário substituir **xxx** por uma referência ao objeto productListItems que faz parte do evento que aciona a jornada.

![Journey Optimizer](./images/oc59.png)

Primeiro, excluir **xxx** no código do HTML primeiro.

![Journey Optimizer](./images/oc60.png)

No menu esquerdo, clique em **Atributos contextuais**. Esse contexto é passado para a mensagem da jornada.

![Journey Optimizer](./images/oc601.png)

Você verá isso. Clique na seta ao lado de **Journey Orchestration** para detalhar.

![Journey Optimizer](./images/oc61.png)

Clique na seta ao lado de **Eventos** para detalhar.

![Journey Optimizer](./images/oc62.png)

Clique na seta ao lado de `--demoProfileLdap--PurchaseEvent` para detalhar.

![Journey Optimizer](./images/oc63.png)

Clique na seta ao lado de **productListItems** para detalhar.

![Journey Optimizer](./images/oc64.png)

Clique no botão **+** ícone ao lado de **Nome** para adicioná-lo à tela de desenho. Você terá isso. Agora é necessário selecionar  **.name** conforme indicado na captura de tela abaixo, você deve remover **.name**.

![Journey Optimizer](./images/oc65.png)

Você terá isso. Clique em **Salvar**.

![Journey Optimizer](./images/oc66.png)

Você estará de volta ao Email Designer agora. Clique em **Salvar** para salvar seu progresso.

![Journey Optimizer](./images/oc67.png)

Em seguida, acesse **Componentes de conteúdo** e arraste e solte uma **HTML** componente na sétima linha. Clique no componente HTML e, em seguida, clique em **Mostrar o código-fonte**.

![Journey Optimizer](./images/oc68.png)

No **Editar HTML** pop-up, cole este HTML:

```<table><tbody><tr><td><b>Subtotal</b><br>Delivery charge (included)</td><td align="right"><b>xxx</b><br><b>5</b></td></tr><tr><td colspan="2" width="500"><hr></td></tr><tr><td><b>Total including VAT</b></td><td align="right"><b>xxx</b></td></tr></tbody></table>```

Há duas referências de **xxx** neste código HTML. Agora é necessário substituir cada **xxx** por uma referência ao objeto productListItems que faz parte do evento que aciona a jornada.

![Journey Optimizer](./images/oc69.png)

Primeiro, exclua o primeiro **xxx** no código do HTML.

![Journey Optimizer](./images/oc71.png)

No menu esquerdo, clique em **Atributos contextuais**.

![Journey Optimizer](./images/oc711.png)

Clique na seta ao lado de **Journey Orchestration** para detalhar.

![Journey Optimizer](./images/oc72.png)

Clique na seta ao lado de **Eventos** para detalhar.

![Journey Optimizer](./images/oc722.png)

Clique na seta ao lado de `--demoProfileLdap--PurchaseEvent` para detalhar.

![Journey Optimizer](./images/oc73.png)

Clique na seta ao lado de **Comércio** para detalhar.

![Journey Optimizer](./images/oc733.png)

Clique na seta ao lado de **Pedido** para detalhar.

![Journey Optimizer](./images/oc74.png)

Clique no botão **+** ícone ao lado de **Preço total** para adicionar isso à tela.

![Journey Optimizer](./images/oc75.png)

Você terá isso. Agora exclua o segundo **xxx** no código do HTML.

![Journey Optimizer](./images/oc76.png)

Clique no botão **+** ícone ao lado de **Preço total** novamente para adicionar isso à tela.

![Journey Optimizer](./images/oc77.png)

Também é possível adicionar o campo **Moeda** no **Pedido** sobre a tela, como você pode ver aqui.
Quando terminar, clique em **Salvar** para salvar as alterações.

![Journey Optimizer](./images/oc771.png)

Você estará de volta ao Email Designer. Clique em **Salvar** novamente.

![Journey Optimizer](./images/oc78.png)

Volte para o painel de mensagens clicando no botão **seta** ao lado do texto da linha de assunto no canto superior esquerdo.

![Journey Optimizer](./images/oc79.png)

Clique na seta no canto superior esquerdo para retornar à jornada.

![Journey Optimizer](./images/oc79a.png)

Clique em **Ok** para fechar a ação de email.

![Journey Optimizer](./images/oc79b.png)

Clique em **Publicar** para publicar sua jornada.

![Journey Optimizer](./images/oc511.png)

Clique em **Publicar** novamente.

![Journey Optimizer](./images/oc512.png)

Sua jornada foi publicada.

![Journey Optimizer](./images/oc513.png)

## 10.1.5 Atualizar a propriedade do cliente de coleta de dados do Adobe Experience Platform

Ir para [Coleta de dados do Adobe Experience Platform](https://experience.adobe.com/launch/) e selecione **Tags**.

Esta é a página Propriedades da coleta de dados do Adobe Experience Platform que você viu anteriormente.

![Página Propriedades](../module1/images/launch1.png)

No módulo 0, o Demo System criou duas propriedades do cliente para você: um para o site e um para o aplicativo móvel. Localizá-los pesquisando por `--demoProfileLdap--` no **[!UICONTROL Pesquisar]** caixa. Clique para abrir o **Web** propriedade.

![Caixa de pesquisa](../module1/images/property6.png)

Ir para **Elementos de dados**. Pesquise e abra o elemento de dados **XDM - Compra**.

![Journey Optimizer](./images/oc91.png)

Você verá isso. Navegar até o campo **_experience.campaign.orchestration.eventID** e preencha sua eventID aqui. A eventID a ser preenchida aqui é a eventID criada como parte do exercício 10.1.2. Clique em **Salvar** ou **Salvar na biblioteca**.

![Journey Optimizer](./images/oc92.png)

Salve as alterações na propriedade do cliente e publique as alterações atualizando a biblioteca de desenvolvimento.

![Journey Optimizer](./images/oc93.png)

Suas alterações foram implantadas e podem ser testadas.

## 10.1.6 Teste o email de confirmação do pedido usando o site de demonstração

Vamos testar a jornada atualizada comprando um produto no site de demonstração.

Ir para [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Depois de fazer logon com sua Adobe ID, você verá isso. Clique no projeto do seu site para abri-lo.

![DSN](../module0/images/web8.png)

No **Telas** página, clique em **Executar**.

![DSN](../module1/images/web2.png)

Você verá seu site de demonstração aberto. Selecione o URL e copie-o para a área de transferência.

![DSN](../module0/images/web3.png)

Abra uma nova janela incógnita do navegador.

![DSN](../module0/images/web4.png)

Cole o URL do site de demonstração, que você copiou na etapa anterior. Em seguida, você será solicitado a fazer logon usando sua Adobe ID.

![DSN](../module0/images/web5.png)

Selecione o tipo de conta e conclua o processo de logon.

![DSN](../module0/images/web6.png)

Você verá seu site carregado em uma janela incógnita do navegador. Para cada demonstração, você precisará usar uma nova janela incógnita do navegador para carregar o URL do site de demonstração.

![DSN](../module0/images/web7.png)

Clique no ícone do logotipo do Adobe no canto superior esquerdo da tela para abrir o Visualizador de perfil.

![Demonstração](../module2/images/pv1.png)

Consulte o painel Visualizador de perfil e o Perfil do cliente em tempo real com a **Experience Cloud ID** como o identificador principal para este cliente atualmente desconhecido.

![Demonstração](../module2/images/pv2.png)

Vá para a página Registrar/fazer logon . Clique em **CRIAR UMA CONTA**.

![Demonstração](../module2/images/pv9.png)

Preencha os detalhes e clique em **Registrar** depois disso, você será redirecionado para a página anterior.

![Demonstração](../module2/images/pv10.png)

Adicione qualquer produto ao carrinho e acesse **Carrinho** página. Clique em **Prossiga para o check-out**.

![Journey Optimizer](./images/cart1.png)

Em seguida, verifique os campos na página de check-out e clique em **Check-out**.

![Journey Optimizer](./images/cart2.png)

Você receberá o email de confirmação do pedido em segundos.

![Journey Optimizer](./images/oc98.png)

Terminou este exercício.

Próxima etapa: [10.2 Configurar uma jornada de boletim informativo em lote](./ex2.md)

[Voltar ao Módulo 10](./journeyoptimizer.md)

[Voltar para todos os módulos](../../overview.md)
