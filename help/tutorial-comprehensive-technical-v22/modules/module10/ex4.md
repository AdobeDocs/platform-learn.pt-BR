---
title: Adobe Journey Optimizer - Configurar e usar notificações por push para iOS
description: Configurar e usar notificações por push para o iOS
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 14a2306a-eb2f-47ee-ad3c-1169412811ca
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1841'
ht-degree: 6%

---

# 10.4 Configurar e usar notificações por push para iOS

Para usar notificações por push com o Adobe Journey Optimizer, há várias configurações para verificar e saber mais.

Estas são todas as configurações a serem verificadas:

- Conjuntos de dados e esquemas no Adobe Experience Platform
- Armazenamento de dados para dispositivos móveis
- Propriedade de coleta de dados para dispositivos móveis
- Superfície do aplicativo para certificados de push
- Teste sua configuração de push usando o AEP Assurance

Vamos rever estes um por um.

Faça logon no Adobe Journey Optimizer acessando [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Você será redirecionado para o **Início**  no Journey Optimizer. Primeiro, certifique-se de usar a sandbox correta. A sandbox a ser usada é chamada de `--aepSandboxId--`. Para alterar de uma sandbox para outra, clique em **Produto de produção (VA7)** e selecione a sandbox na lista. Neste exemplo, a sandbox é chamada de **Ativação AEP FY22**. Você estará no **Início** exibição da sandbox `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

## 10.4.1 Encaminhar conjuntos de dados

O Adobe Journey Optimizer usa conjuntos de dados para armazenar itens como tokens de push de dispositivos móveis ou interações com mensagens de push (como: mensagem enviada, mensagem aberta, etc) em um conjunto de dados no Adobe Journey Optimizer.

Você pode encontrar esses conjuntos de dados acessando **[!UICONTROL Conjuntos de dados]** no menu no lado esquerdo da tela. Para mostrar conjuntos de dados do sistema, clique no ícone de filtro.

![Assimilação de dados](./images/menudsjo.png)

Habilite a opção **Mostrar conjuntos de dados do sistema** e procurar **AJO**. Em seguida, você verá os conjuntos de dados usados para notificações por push.

![Assimilação de dados](./images/menudsjo1.png)

## Armazenamento de dados 10.4.2 para dispositivos móveis

Ir para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/).

No menu esquerdo, acesse **[!UICONTROL Datastream]** e pesquise o conjunto de dados criado em [Exercício 0.2](./../module0/ex2.md), que é nomeado como `--demoProfileLdap-- - Demo System Datastream (Mobile)`. Clique em para abri-lo.

![Clique no ícone Datastream no painel de navegação esquerdo](./images/edgeconfig1a.png)

Clique em **Editar** no **Adobe Experience Platform** serviço.

![Clique no ícone Datastream no painel de navegação esquerdo](./images/edgeconfig1.png)

Em seguida, você verá as configurações do conjunto de dados que foram definidas e em quais eventos de conjuntos de dados e atributos de perfil serão armazenados.

![Nomeie o armazenamento de dados e salve](./images/edgeconfig2.png)

Nenhuma alteração é necessária, seu conjunto de dados agora está pronto para ser usado na propriedade do Cliente da coleta de dados para dispositivos móveis.

## 10.4.3 Revise sua propriedade de coleta de dados para dispositivos móveis

Ir para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Como parte de [Exercício 0.1](./../module0/ex1.md), 2 propriedades da Coleta de dados foram criadas.
Você já tem usado essas propriedades do Cliente da coleta de dados como parte de módulos anteriores.

Clique em para abrir a propriedade Coleta de dados para dispositivos móveis.

![DSN](./images/launchprop.png)

Na propriedade Coleta de dados, acesse **Extensões**. Em seguida, você verá as várias extensões necessárias para o aplicativo móvel. Clique em para abrir a extensão **Rede de borda Adobe Experience Platform**.

![Coleção de dados da Adobe Experience Platform](./images/launchprop1.png)

Você verá que seu conjunto de dados para dispositivos móveis está vinculado aqui. Em seguida, clique em **Cancelar** para retornar à visão geral das extensões.

![Coleção de dados da Adobe Experience Platform](./images/launchprop2.png)

Você vai voltar aqui. Você verá a extensão para **Garantia da AEP**. O AEP Assurance ajuda você a inspecionar, testar, simular e validar o modo como você coleta dados ou veicula experiências em seu aplicativo móvel. Leia mais sobre o AEP Assurance e o Project Griffon aqui [https://aep-sdks.gitbook.io/docs/beta/project-griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon).

![Coleção de dados da Adobe Experience Platform](./images/launchprop8.png)

Em seguida, clique em **Configurar** para abrir a extensão **Adobe Journey Optimizer**.

![Coleção de dados da Adobe Experience Platform](./images/launchprop9.png)

Você verá que é aqui que o conjunto de dados para rastrear eventos de push está vinculado.

![Coleção de dados da Adobe Experience Platform](./images/launchprop10.png)

Não é necessário fazer alterações na propriedade Coleta de dados.

## 10.4.4 Revise a configuração da superfície do aplicativo

Ir para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). No menu esquerdo, acesse **Superfícies do aplicativo** e abrir, a superfície do aplicativo para **DX Demo App APNS**.

![Coleção de dados da Adobe Experience Platform](./images/appsf.png)

Em seguida, você verá a superfície do aplicativo configurada para iOS e Android.

![Coleção de dados da Adobe Experience Platform](./images/appsf1.png)

## 10.4.5 Teste a configuração de notificação por push usando o AEP Assurance.

Depois que o aplicativo for instalado, você o encontrará na tela inicial do seu dispositivo. Clique no ícone para abrir o aplicativo.

![DSN](../module0/images/mobileappn1.png)

Ao usar o aplicativo pela primeira vez, você será solicitado a fazer logon usando sua Adobe ID. Conclua o processo de logon.

![DSN](../module0/images/mobileappn2.png)

Depois de fazer logon, você verá uma notificação solicitando sua permissão para enviar notificações. Enviaremos notificações como parte do tutorial, portanto, clique em **Permitir**.

![DSN](../module0/images/mobileappn3.png)

Você verá a página inicial do aplicativo. Ir para **Configurações**.

![DSN](../module0/images/mobileappn4.png)

Nas configurações, você verá que atualmente uma **Projeto público** é carregada no aplicativo. Clique em **Projeto personalizado**.

![DSN](../module0/images/mobileappn5.png)

Agora é possível carregar um projeto personalizado. Clique no código QR para carregar facilmente seu projeto.

![DSN](../module0/images/mobileappn6.png)

Após o exercício 0.1, teve este resultado. Clique para abrir o **Projeto de varejo móvel** que foi criado para você.

![DSN](../module0/images/dsn5b.png)

Caso tenha fechado acidentalmente a janela do navegador, ou para futuras sessões de demonstração ou ativação, também é possível acessar o projeto do site indo até [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Depois de fazer logon com sua Adobe ID, você verá isso. Clique no projeto do aplicativo móvel para abri-lo.

![DSN](../module0/images/web8a.png)

Você verá isso. Clique em **Integrações**.

![DSN](../module0/images/web8aa.png)

É necessário selecionar a propriedade Coleta de dados para dispositivos móveis que foi criada no exercício 0.1. Em seguida, clique em **Executar**.

![DSN](../module0/images/web8b.png)

Você verá esse pop-up, que contém um código QR. Verifique este código QR no aplicativo móvel.

![DSN](../module0/images/web8c.png)

Em seguida, você verá a ID do projeto exibida no aplicativo, depois de clicar em **Salvar**.

![DSN](../module0/images/mobileappn7.png)

Agora, volte para **Início** no aplicativo. Seu aplicativo está pronto para ser usado.

![DSN](../module0/images/mobileappn8.png)

Agora é necessário digitalizar um código QR para conectar seu dispositivo móvel à sessão do AEP Assurance.

Para iniciar uma sessão do AEP Assurance, acesse [https://experience.adobe.com/#/@experienceplatform/griffon](https://experience.adobe.com/#/@experienceplatform/griffon). Clique em **Criar sessão**.

![Coleção de dados da Adobe Experience Platform](./images/griffon3.png)

Clique em **Start**.

![Coleção de dados da Adobe Experience Platform](./images/griffon5.png)

Preencha os valores:

- Nome da sessão: use `--demoProfileLdap-- - push debugging` e substitua ldap pelo seu ldap
- URL base: use **dxdemo://default**

Clique em **Próximo**.

![Coleção de dados da Adobe Experience Platform](./images/griffon4.png)

Em seguida, você verá um código QR em sua tela, que deve ser verificado com o dispositivo iOS.

![Coleção de dados da Adobe Experience Platform](./images/griffon6.png)

No seu dispositivo móvel, abra o aplicativo de câmera e digitalize o código QR exibido pelo AEP Assurance.

![Coleção de dados da Adobe Experience Platform](./images/ipadPushTest8a.png)

Em seguida, você verá uma tela pop-up, solicitando que você digite o código PIN. Copie o código PIN da tela AEP Assurance e clique em **Connect**.

![Coleção de dados da Adobe Experience Platform](./images/ipadPushTest9.png)

Você verá isso.

![Coleção de dados da Adobe Experience Platform](./images/ipadPushTest11.png)

No AEP Assurance, você verá que um dispositivo está na sessão do AEP Assurance.

![Coleção de dados da Adobe Experience Platform](./images/griffon7.png)

Ir para **Depuração por push**. Você verá algo assim.

![Coleção de dados da Adobe Experience Platform](./images/griffon10.png)

Algumas explicações:

- A primeira coluna, **Cliente**, mostra os identificadores disponíveis no dispositivo iOS. Você verá um ECID e um token de push.
- A segunda coluna mostra **Perfil** , com informações adicionais sobre em qual plataforma o token de push está (APNS ou APNSSandbox). Se você clicar no botão **Perfil do Inspect** , você será levado ao Adobe Experience Platform e verá o Perfil completo do cliente em tempo real.
- A terceira coluna mostra o **Configuração do aplicativo**, que foi criada no âmbito do exercício **10.5.4 Criar configuração de aplicativo no Launch**

Para testar a configuração de Push, clique no botão **Enviar notificação por push** botão.

![Coleção de dados da Adobe Experience Platform](./images/griffon11.png)

Você precisa ter certeza de que a variável **Demonstração do DX** o aplicativo não está aberto no momento do clique no **Enviar notificação por push** botão. Se o aplicativo estiver aberto, a Notificação por push pode ser recebida em segundo plano e não ficar visível.

Em seguida, você verá uma notificação por push como essa no seu dispositivo móvel.

![Coleção de dados da Adobe Experience Platform](./images/ipadPush2.png)

Se você recebeu a notificação por push, significa que a configuração está correta e está funcionando bem.

## 10.4.6 Criar um novo evento

No menu , acesse **Administração de jornada** e clique em **Gerenciar** under **Eventos**.

![ACOP](./images/acopmenu.png)

No **Eventos** , você verá uma exibição semelhante a esta. Clique em **Criar evento**.

![ACOP](./images/add.png)

Em seguida, você verá uma configuração de evento vazia.

![ACOP](./images/emptyevent.png)

Primeiro de tudo, dê a seu Evento um Nome como este: `--demoProfileLdap--StoreEntryEvent` e defina a descrição como `Store Entry Event`.

![ACOP](./images/eventname.png)

O próximo é o **Tipo de evento** seleção. Selecionar **Unitário**.

![ACOP](./images/eventidtype1.png)

O próximo é o **Tipo de ID do evento** seleção. Selecionar **Sistema gerado**

![ACOP](./images/eventidtype.png)

Em seguida está a seleção Esquema. Um esquema foi preparado para este exercício. Use o esquema `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Após selecionar o Esquema, você verá vários campos sendo selecionados na variável **Carga** seção. Seu evento está totalmente configurado.

![ACOP](./images/eventpayload.png)

Você deveria ver isso. Clique em **Salvar**.

![ACOP](./images/eventsave.png)

Seu Evento agora está configurado e salvo. Clique no seu evento novamente para abrir o **Editar evento** novamente.

![ACOP](./images/eventdone.png)

Passe o mouse sobre **Carga** e clique no botão **Exibir carga** ícone .

![ACOP](./images/hover.png)

Você verá um exemplo da carga esperada.

![ACOP](./images/fullpayload.png)

Seu evento tem uma orquestration eventID exclusiva, que pode ser encontrada ao rolar para baixo na carga útil até que você veja `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

A ID de evento é o que precisa ser enviado para o Adobe Experience Platform para acionar a Jornada que você criará na próxima etapa. Anote essa eventID, pois você precisará dela na próxima etapa.
`"eventID": "e3a8f0bdc0b609667cd96a72a6b1e5aafa0ddaf6ccf121c574e6a2030860a633"`

Clique em **Ok**, seguida de **Cancelar**.

## 10.4.7 Criar uma jornada

No menu , acesse **Jornada** e clique em **Criar Jornada**.

![DSN](./images/sjourney1.png)

Você verá isso. Dê um nome à sua jornada. Use `--demoProfileLdap-- - Store Entry journey`. Clique em **OK**.

![DSN](./images/sjourney3.png)

Primeiro, é necessário adicionar o evento como ponto de partida da jornada. Procure seu evento `--demoProfileLdap--StoreEntryEvent` e arraste e solte na tela. Clique em **OK**.

![DSN](./images/sjourney4.png)

Em seguida, em **Ações**, pesquise a **Empurrar** ação.
Arraste e solte a **Empurrar** ação na tela.

![DSN](./images/sjourney5.png)

Defina as **Categoria** para **Marketing** e selecione uma superfície de push que permite enviar notificações por push. Nesse caso, a superfície do email a ser selecionada é **Push-iOS-Android**.

![ACOP](./images/journeyactions1push.png)

A próxima etapa é criar a mensagem. Para fazer isso, clique em **Editar conteúdo**.

![ACOP](./images/journeyactions2push.png)

Você verá isso. Clique no botão **personalização** ícone para o **Título** campo.

![Push](./images/bp5.png)

Você verá isso. Agora é possível selecionar qualquer atributo de perfil diretamente do Perfil do cliente em tempo real.

![Empurrar](./images/bp6.png)

Pesquisar pelo campo **Nome**, em seguida, clique no botão **+** ícone ao lado do campo **Nome**. Em seguida, você verá o token de personalização do Nome sendo adicionado: **{{profile.person.name.firstName}}**.

![Empurrar](./images/bp9.png)

Em seguida, adicione o texto **, bem-vindo à nossa loja!** behind **{{profile.person.name.firstName}}**.

Clique em **Salvar**.

![Empurrar](./images/bp10.png)

Agora você tem isso. Clique no botão **personalização** ícone para o **Corpo** campo.

![Empurrar](./images/bp11.png)

Inserir este texto **Clique aqui para obter um desconto de 10% quando você comprar hoje!** e clique em **Salvar**.

![Empurrar](./images/bp12.png)

Você terá isso. Clique na seta no canto superior esquerdo para retornar à jornada.

![Journey Optimizer](./images/bp12a.png)

Clique em **OK** para fechar sua ação de push.

![DSN](./images/sjourney8.png)

Clique em **Publicar**.

![DSN](./images/sjourney10.png)

Clique em **Publicar** novamente.

![DSN](./images/sjourney10a.png)

Sua jornada foi publicada.

![DSN](./images/sjourney11.png)

## 10.4.8 Teste sua jornada e mensagem por push

No aplicativo DX Demo 2.0 para dispositivos móveis, acesse **Configurações** tela. Clique no botão **Entrada da loja** botão.

>[!NOTE]
>
>O **Entrada da loja** está sendo implementado no momento. Você ainda não o encontrará no aplicativo.

![DSN](./images/demo1b.png)

Feche o aplicativo imediatamente após clicar no link **Entrada da loja** caso contrário, a mensagem de push não será exibida.

![DSN](./images/demo2.png)

Após alguns segundos, você verá a mensagem aparecer.

![DSN](./images/demo3.png)

Terminou este exercício.

Próxima etapa: [10.5 Criar uma jornada de evento comercial](./ex5.md)

[Voltar ao Módulo 10](./journeyoptimizer.md)

[Voltar para todos os módulos](../../overview.md)
