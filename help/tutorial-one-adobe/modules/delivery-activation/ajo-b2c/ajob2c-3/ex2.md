---
title: Configurar uma jornada com mensagens por push
description: Configurar uma jornada com mensagens por push
kt: 5342
doc-type: tutorial
exl-id: 63d7ee24-b6b5-4503-b104-a345c2b26960
source-git-commit: fb14ba45333bdd5834ff0c6c2dc48dda35cfe85f
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 2%

---

# 3.3.2 Configurar uma jornada com mensagens de push

Faça login no Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`. Você estará na exibição **Página inicial** da sua sandbox `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## 3.3.2.1 Criar um novo evento

No menu esquerdo, vá para **Configurações** e clique em **Gerenciar** em **Eventos**.

![ACOP](./images/acopmenu.png)

Na tela **Eventos**, você verá um modo de exibição semelhante a este. Clique em **Criar Evento**.

![ACOP](./images/add.png)

Em seguida, você verá uma configuração de evento vazia.
Primeiro, dê ao seu Evento um Nome como este: `--aepUserLdap--StoreEntryEvent` e defina a descrição como `Store Entry Event`.
A seguir está a seleção **Tipo de Evento**. Selecione **Unitário**.
A seguir está a seleção **Tipo de ID de Evento**. Selecione **Gerado pelo Sistema**.

![ACOP](./images/eventname.png)

O próximo é a seleção Esquema. Um esquema foi preparado para este exercício. Use o esquema `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

Depois de selecionar o esquema, você verá vários campos sendo selecionados na seção **Carga**. Verifique se o campo **Namespace** está definido como **ECID**. Seu evento está totalmente configurado.

Clique em **Salvar**.

![ACOP](./images/eventschema.png)

Seu evento agora está configurado e salvo. Clique no evento novamente para abrir a tela **Editar Evento** novamente.

![ACOP](./images/eventdone.png)

Passe o mouse sobre o campo **Carga** e clique no ícone **Exibir carga**.

![ACOP](./images/hover.png)

Agora você verá um exemplo da carga útil esperada.

Seu Evento tem uma eventID de orquestração exclusiva, que você pode encontrar rolando para baixo nessa carga até ver `_experience.campaign.orchestration.eventID`.

A ID do evento é o que precisa ser enviado para o Adobe Experience Platform para acionar a Jornada que você criará na próxima etapa. Anote essa eventID, pois ela será necessária na próxima etapa.
`"eventID": "aa895251f76831e6440f169f1bb9d2a4388f0696d8e2782cfab192a275817dfa"`

Clique em **Ok**.

![ACOP](./images/payloadeventID.png)

Clique em **Cancelar**.

![ACOP](./images/payloadeventIDa.png)

## 3.3.2.2 Criar uma jornada

No menu esquerdo, vá para **Jornada** e clique em **Criar Jornada**.

![DSN](./images/sjourney1.png)

Você verá isso. Nomeie sua jornada: `--aepUserLdap-- - Store Entry journey`. Clique em **Salvar**.

![DSN](./images/sjourney3.png)

Primeiro, é necessário adicionar o evento como ponto de partida da jornada. Procure seu evento `--aepUserLdap--StoreEntryEvent` e arraste-o e solte-o na tela. Clique em **Salvar**.

![DSN](./images/sjourney4.png)

Em seguida, em **Ações**, pesquise a ação **Push**. Arraste e solte a ação **Enviar** na tela.

Defina a **Categoria** como **Marketing** e selecione uma superfície de push que permita enviar notificações por push. Nesse caso, a superfície de email a ser selecionada é **Push-iOS-Android**.

>[!NOTE]
>
>É necessário que exista um Canal no Journey Optimizer que esteja usando a **Superfície do Aplicativo**, conforme revisado anteriormente.

![ACOP](./images/journeyactions1push.png)

A próxima etapa é criar a mensagem. Para fazer isso, clique em **Editar conteúdo**.

![ACOP](./images/journeyactions2push.png)

Você verá isso. Clique no ícone de **personalização** do campo **Título**.

![Push](./images/bp5.png)

Você verá isso. Agora é possível selecionar qualquer atributo de perfil diretamente do Perfil do cliente em tempo real.

Pesquise pelo campo **Nome** e clique no ícone **+** ao lado do campo **Nome**. Você verá o token de personalização para o Nome que está sendo adicionado: **{{profile.person.name.firstName}}**.

![Push](./images/bp9.png)

Em seguida, adicione o texto **, bem-vindo à nossa loja!** atrás de **{{profile.person.name.firstName}}**.

Clique em **Salvar**.

![Push](./images/bp10.png)

Agora você tem isto. Clique no ícone de **personalização** do campo **Corpo**.

![Push](./images/bp11.png)

Digite este texto **Clique aqui para obter um desconto de 10% ao comprar hoje!** e clique em **Salvar**.

![Push](./images/bp12.png)

Então você terá isto. Clique na seta no canto superior esquerdo para voltar à jornada.

![Journey Optimizer](./images/bp12a.png)

Clique em **Salvar** para fechar sua ação de push.

![DSN](./images/sjourney8.png)

Clique em **Publicar**.

![DSN](./images/sjourney10.png)

Clique novamente em **Publicar**.

![DSN](./images/sjourney10a.png)

Sua jornada foi publicada.

![DSN](./images/sjourney11.png)

## 3.3.2.3 Atualize sua propriedade de coleção de dados para dispositivos móveis

Em **Introdução**, o Sistema de demonstração em seguida criou propriedades de marcas para você: uma para o site e outra para o aplicativo móvel. Localize-os procurando por `--aepUserLdap--` na caixa **Pesquisar**. Clique para abrir a propriedade **Mobile**.

![DSN](./images/pushpoi1.png)

Você deverá ver isso.

![DSN](./images/pushpoi2.png)

No menu esquerdo, vá para **Regras** e clique para abrir a regra **Entrada de local**.

![DSN](./images/pushpoi3.png)

Você deverá ver isso. Clique na ação **Mobile Core - Attach Data**.

![DSN](./images/pushpoi4.png)

Você deverá ver isso.

![DSN](./images/pushpoi5.png)

Cole a eventID do seu evento `--aepUserLdap--StoreEntryEvent` na janela **Carga JSON**. Clique em **Manter alterações**.

![DSN](./images/pushpoi6.png)

Clique em **Salvar** ou **Salvar na Biblioteca**.

![DSN](./images/pushpoi7.png)

Vá para **Fluxo de Publicação** e clique para abrir a biblioteca **Principal**.

![DSN](./images/pushpoi8.png)

Clique em **Adicionar todos os recursos alterados** e em **Salvar e criar no desenvolvimento**.

![DSN](./images/pushpoi9.png)

## 3.3.2.4 Testar sua jornada e mensagem por push

Abra o aplicativo **DSN Mobile**.

![DSN](./images/dxdemo1.png)

Vá para a página **Localizador de Loja**.

![DSN](./images/dxdemo2.png)

Clique em **Simular entrada do POI**.

![DSN](./images/dxdemo3.png)

Após alguns segundos, você verá a notificação por push aparecer.

![DSN](./images/dxdemo4.png)

## Próximas etapas

Ir para [3.3.3 Configurar uma campanha com mensagens no aplicativo](./ex3.md){target="_blank"}

Voltar para [Adobe Journey Optimizer: Mensagens por push e no aplicativo](ajopushinapp.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}