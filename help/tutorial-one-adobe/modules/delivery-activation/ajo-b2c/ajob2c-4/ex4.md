---
title: Adobe Journey Optimizer - Configurar e usar notificações por push para iOS
description: Configurar e usar notificações por push para iOS
kt: 5342
doc-type: tutorial
exl-id: 25b3c194-9acb-4085-b3e0-2932afaa04cb
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '1848'
ht-degree: 2%

---

# 3.4.4 Configurar e usar notificações por push para iOS

Para usar notificações por push com o Adobe Journey Optimizer, há várias configurações a serem verificadas e conhecidas.

Estas são todas as configurações a serem verificadas:

- Conjuntos de dados e esquemas na Adobe Experience Platform
- Sequência de dados para dispositivos móveis
- Propriedade de coleção de dados para dispositivos móveis
- Superfície do aplicativo para certificados push
- Testar a configuração de push usando o AEP Assurance

Vamos analisar um por um.

Faça login no Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`. Você estará na exibição **Página inicial** da sua sandbox `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## 3.4.4.1 Conjunto de dados de push

O Adobe Journey Optimizer usa conjuntos de dados para armazenar itens como os tokens de push de dispositivos móveis ou interações com mensagens de push (como: mensagem enviada, mensagem aberta etc.) em um conjunto de dados no Adobe Journey Optimizer.

Você pode encontrar esses conjuntos de dados acessando **[!UICONTROL Conjuntos de dados]** no menu do lado esquerdo da tela. Para mostrar conjuntos de dados do sistema, clique no ícone de filtro.

Habilite a opção **Mostrar conjuntos de dados do sistema** e pesquisar por **AJO**. Você verá os conjuntos de dados usados para notificações por push.

![Assimilação de dados](./images/menudsjo1.png)

## 3.4.4.2 Sequência de dados para dispositivos móveis

Ir para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/).

No menu esquerdo, vá para **[!UICONTROL Sequência de dados]** e procure a sequência de dados que você criou em [Introdução](./../../../../modules/getting-started/gettingstarted/ex2.md), chamada de `--aepUserLdap-- - Demo System Datastream (Mobile)`. Clique em para abri-lo.

![Clique no ícone Datastream na navegação à esquerda](./images/edgeconfig1a.png)

Clique em **Editar** no serviço **Adobe Experience Platform**.

![Clique no ícone Datastream na navegação à esquerda](./images/edgeconfig1.png)

Em seguida, você verá as configurações de sequência de dados que foram definidas e em quais conjuntos de dados, eventos e atributos de perfil serão armazenados.

Você também deve ativar as seguintes opções se elas ainda não estiverem ativadas:

- **Offer Decisioning**
- **Destinos de personalização**
- **Adobe Journey Optimizer**

Clique em **Salvar**.

![Nomeie a sequência de dados e salve](./images/edgeconfig2.png)

## 3.4.4.3 Revise a propriedade da Coleta de dados para dispositivos móveis

Ir para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Como parte da [Introdução](./../../../../modules/getting-started/gettingstarted/ex1.md), foram criadas duas propriedades de Coleção de Dados.
Você já usa essas propriedades do Cliente da coleção de dados como parte dos módulos anteriores.

Clique em para abrir a propriedade Coleção de dados para dispositivos móveis.

![DSN](./images/launchprop.png)

Na propriedade da Coleção de dados, vá para **Extensões**. Em seguida, você verá as várias extensões necessárias para o aplicativo móvel. Clique para abrir a extensão **Adobe Experience Platform Edge Network**.

![Coleta de dados do Adobe Experience Platform](./images/launchprop1.png)

Em seguida, você verá que a sequência de dados para dispositivos móveis está vinculada aqui. Em seguida, clique em **Cancelar** para voltar para a visão geral das extensões.

![Coleta de dados do Adobe Experience Platform](./images/launchprop2.png)

Você estará de volta aqui. Você verá a extensão para **AEP Assurance**. O AEP Assurance ajuda a inspecionar, testar, simular e validar como você coleta dados ou veicula experiências em seu aplicativo móvel. Você pode ler mais sobre a AEP Assurance e o Project Griffon aqui [https://aep-sdks.gitbook.io/docs/beta/project-griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon).

![Coleta de dados do Adobe Experience Platform](./images/launchprop8.png)

Em seguida, clique em **Configurar** para abrir a extensão **Adobe Journey Optimizer**.

![Coleta de dados do Adobe Experience Platform](./images/launchprop9.png)

Você verá que é aqui que o conjunto de dados para rastrear eventos de push é vinculado.

![Coleta de dados do Adobe Experience Platform](./images/launchprop10.png)

Não há necessidade de fazer alterações na propriedade da Coleção de dados.

## 3.4.4.4 Revise a configuração do aplicativo Surface

Ir para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). No menu esquerdo, vá para **Superfícies do Aplicativo** e abra a Superfície do Aplicativo para o **DX Demo App APNS**.

![Coleta de dados do Adobe Experience Platform](./images/appsf.png)

Em seguida, você verá a Superfície do aplicativo configurada para o iOS e o Android.

![Coleta de dados do Adobe Experience Platform](./images/appsf1.png)

## 3.4.4.5 Teste a configuração da notificação por push usando o AEP Assurance.

Depois que o aplicativo for instalado, você o encontrará na tela inicial do dispositivo. Clique no ícone para abrir o aplicativo.

![DSN](./../../../../modules/getting-started/gettingstarted/images/mobileappn1.png)

Quando estiver usando o aplicativo pela primeira vez, você será solicitado a fazer logon usando sua Adobe ID. Conclua o processo de logon.

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn2.png)

Depois de fazer logon, você verá uma notificação solicitando sua permissão para enviar notificações. Enviaremos notificações como parte do tutorial, então clique em **Permitir**.

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn3.png)

Você verá a página inicial do aplicativo. Vá para **Configurações**.

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn4.png)

Nas configurações, você verá que, atualmente, um **Projeto público** está carregado no aplicativo. Clique em **Projeto personalizado**.

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn5.png)

Agora você pode carregar um projeto personalizado. Clique no código QR para carregar facilmente seu projeto.

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn6.png)

Depois de passar pela seção **Introdução**, você teve este resultado. Clique para abrir o **projeto do Mobile Retail** criado para você.

![DSN](./../../../modules/../getting-started/gettingstarted/images/dsn5b.png)

Caso tenha fechado acidentalmente a janela do navegador ou para futuras sessões de demonstração ou capacitação, você também pode acessar o projeto do seu site em [https://dsn.adobe.com/projects](https://dsn.adobe.com/projects). Depois de fazer logon com sua Adobe ID, você verá isso. Clique no projeto do aplicativo móvel para abri-lo.

![DSN](./../../../modules/../getting-started/gettingstarted/images/web8a.png)

Em seguida, clique em **Executar**.

![DSN](./images/web8b.png)

Você verá este pop-up, que contém um código QR. Digitalize este código QR de dentro do aplicativo móvel.

![DSN](./../../../modules/../getting-started/gettingstarted/images/web8c.png)

Você verá sua ID de projeto exibida no aplicativo e depois poderá clicar em **Salvar**.

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn7.png)

Agora, volte para a **Página inicial** no aplicativo. Seu aplicativo está pronto para ser usado.

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn8.png)

Agora é necessário digitalizar um código QR para conectar seu dispositivo móvel à sua sessão do AEP Assurance.

Para iniciar uma sessão do AEP Assurance, vá para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Clique em **Assurance** no menu esquerdo. Em seguida, clique em **Criar sessão**.

![Coleta de dados do Adobe Experience Platform](./images/griffon3.png)

Clique em **Start**.

![Coleta de dados do Adobe Experience Platform](./images/griffon5.png)

Preencha os valores:

- Nome da sessão: use `--aepUserLdap-- - push debugging` e substitua ldap pelo seu ldap
- URL base: use `dxdemo://default`

Clique em **Next**.

![Coleta de dados do Adobe Experience Platform](./images/griffon4.png)

Você verá um código QR na tela, que deve ser digitalizado com o dispositivo iOS.

![Coleta de dados do Adobe Experience Platform](./images/griffon6.png)

Em seu dispositivo móvel, abra o aplicativo de câmera e verifique o código QR exibido pelo AEP Assurance.

![Coleta de dados do Adobe Experience Platform](./images/ipadPushTest8a.png)

Você verá uma tela pop-up solicitando que você insira o código PIN. Copie o código PIN da tela do AEP Assurance e clique em **Conectar**.

![Coleta de dados do Adobe Experience Platform](./images/ipadPushTest9.png)

Você verá isso.

![Coleta de dados do Adobe Experience Platform](./images/ipadPushTest11.png)

No Assurance, você verá agora que um dispositivo está ativo na sessão do Assurance. Clique em **Concluído**.

![Coleta de dados do Adobe Experience Platform](./images/griffon7.png)

Ir para **Depuração push**.

>[!NOTE]
>
>Caso não encontre **Push Debug** no menu esquerdo, clique em **Configurar** no canto inferior esquerdo da tela e adicione **Push Debug** ao menu.

Vocês verão algo assim.

![Coleta de dados do Adobe Experience Platform](./images/griffon10.png)

Alguma explicação:

- A primeira coluna, **Cliente**, mostra os identificadores disponíveis em seu dispositivo iOS. Você verá uma ECID e um token de push.
- A 2ª coluna mostra as **Credenciais e Configuração do App Store**, que foram configuradas como parte do exercício **3.4.5.4 Criar Configuração de Aplicativo na Inicialização**
- A segunda coluna mostra informações do **Perfil**, com informações adicionais sobre em qual plataforma está o token de push (APNS ou APNSSandbox). Se clicar no botão **Inspecionar Perfil**, você será levado para a Adobe Experience Platform e verá o Perfil completo do Cliente em Tempo Real.

Para testar a configuração de push, vá para o botão **Enviar Configuração de Push de Teste**. Clique em **Enviar notificação por push de teste**

![Coleta de dados do Adobe Experience Platform](./images/griffon11.png)

Verifique se o aplicativo **DX Demo** não está aberto no momento de clicar no botão **Enviar notificação por push**. Se o aplicativo estiver aberto, a Notificação por push pode ser recebida em segundo plano e não estará visível.

Você verá uma notificação por push como esta aparecer no seu dispositivo móvel.

![Coleta de dados do Adobe Experience Platform](./images/ipadPush2.png)

Se você recebeu a notificação por push, significa que a configuração está correta e funcionando bem e agora é possível criar uma jornada real que resultará no envio de uma mensagem por push do Journey Optimizer.

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

## 3.4.4.8 Testar a jornada e a mensagem por push

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

Ir para [Resumo e benefícios](./summary.md){target="_blank"}

Voltar para [Adobe Journey Optimizer](journeyoptimizer.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
