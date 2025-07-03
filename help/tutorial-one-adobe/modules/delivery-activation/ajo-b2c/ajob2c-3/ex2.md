---
title: Configurar uma jornada com mensagens por push
description: Configurar uma jornada com mensagens por push
kt: 5342
doc-type: tutorial
source-git-commit: 203590e3289d2e5342085bf8b6b4e3cd11859539
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 2%

---

# 3.3.2 Configurar uma jornada com mensagens de push


## 3.4.4.6 Criar um novo evento

Ir para **Journey Optimizer**. No menu esquerdo, vá para **Configurações** e clique em **Gerenciar** em **Eventos**.

![ACOP](./images/acopmenu.png)

Na tela **Eventos**, você verá um modo de exibição semelhante a este. Clique em **Criar Evento**.

![ACOP](./images/add.png)

Em seguida, você verá uma configuração de evento vazia.
Primeiro, dê ao seu Evento um Nome como este: `--aepUserLdap--StoreEntryEvent` e defina a descrição como `Store Entry Event`.
A seguir está a seleção **Tipo de Evento**. Selecione **Unitário**.
A seguir está a seleção **Tipo de ID de Evento**. Selecione **Gerado pelo Sistema**.

![ACOP](./images/eventname.png)

O próximo é a seleção Esquema. Um esquema foi preparado para este exercício. Use o esquema `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

Depois de selecionar o esquema, você verá vários campos sendo selecionados na seção **Carga**. Seu evento está totalmente configurado.

Clique em **Salvar**.

![ACOP](./images/eventschema.png)

O Evento agora está configurado e salvo. Clique no evento novamente para abrir a tela **Editar Evento** novamente.

![ACOP](./images/eventdone.png)

Passe o mouse sobre o campo **Carga** e clique no ícone **Exibir carga**.

![ACOP](./images/hover.png)

Agora você verá um exemplo da carga útil esperada.

Seu Evento tem uma eventID de orquestração exclusiva, que você pode encontrar rolando para baixo nessa carga até ver `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

A ID do evento é o que precisa ser enviado para o Adobe Experience Platform para acionar a Jornada que você criará na próxima etapa. Anote essa eventID, pois ela será necessária na próxima etapa.
`"eventID": "89acd341ec2b7d1130c9a73535029debf2ac35f486bc99236b1a5091d6f4bc68"`

Clique em **Ok**, seguido de **Cancelar**.

## 3.4.4.7 Criar uma jornada

No menu, vá para **Jornadas** e clique em **Criar Jornada**.

![DSN](./images/sjourney1.png)

Você verá isso. Dê um nome à sua jornada. Usar `--aepUserLdap-- - Store Entry journey`. Clique em **Salvar**.

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

Você verá isso. Agora é possível selecionar qualquer atributo de Perfil diretamente do Perfil de cliente em tempo real.

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

## 3.4.4.8 Testar sua jornada e mensagem por push

No aplicativo móvel DX Demo 2.0, acesse a tela **Configurações**. Clique no botão **Armazenar entrada**.

>[!NOTE]
>
>O botão **Armazenar Entrada** está sendo implementado no momento. Você ainda não o encontrará no aplicativo.

![DSN](./images/demo1b.png)

Feche o aplicativo imediatamente após clicar no ícone **Entrada da loja**. Caso contrário, a mensagem de push não será exibida.

Após alguns segundos, você verá a mensagem ser exibida.

![DSN](./images/demo2.png)

Você concluiu este exercício.

## Próximas etapas

Ir para [3.3.3 Configurar uma campanha com mensagens no aplicativo](./ex3.md){target="_blank"}

Voltar para [Adobe Journey Optimizer: Mensagens por push e no aplicativo](ajopushinapp.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
