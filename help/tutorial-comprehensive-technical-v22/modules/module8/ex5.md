---
title: Adobe Journey Optimizer - API de tempo externo, ação de SMS e muito mais - Acione sua Jornada de cliente orquestrada
description: Adobe Journey Optimizer - API de tempo externo, ação de SMS e muito mais - Acione sua Jornada de cliente orquestrada
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 4d92877d-8fdc-4902-ad32-7fa068bc1395
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 1%

---

# 8.5 Acione sua jornada

Neste exercício, você testará e acionará a jornada configurada neste módulo.

## 8.5.1 Atualizar a configuração do evento de geofence

Ir para [Coleta de dados do Adobe Experience Platform](https://experience.adobe.com/launch/) e selecione **Tags**.

Esta é a página Propriedades da coleta de dados do Adobe Experience Platform que você viu anteriormente.

![Página Propriedades](../module1/images/launch1.png)

No módulo 0, o Demo System criou duas propriedades do cliente para você: um para o site e um para o aplicativo móvel. Localizá-los pesquisando por `--demoProfileLdap--` no **[!UICONTROL Pesquisar]** caixa. Clique para abrir o **Web** propriedade.

![Caixa de pesquisa](../module1/images/property6.png)

Você verá isso.

![Configuração do Launch](./images/rule1.png)

No menu esquerdo, acesse **Regras** e pesquisar a regra **Evento de geofence**. Clique na regra **Evento de geofence** para abri-lo.

![Configuração do Launch](./images/rule2.png)

Você verá os detalhes dessa regra. Clique em para abrir a ação **Enviar &quot;evento de geofence&quot; para o AEP - acionar JO**.

![Configuração do Launch](./images/rule3.png)

Você verá que, quando essa ação for acionada, um elemento de dados específico será usado para definir a estrutura de dados XDM. Você precisa atualizar esse elemento de dados e definir a variável **ID do evento** do evento que você configurou em [Exercício 8.1](./ex1.md).

![Configuração do Launch](./images/rule4.png)

Agora é necessário atualizar o elemento de dados **XDM - Evento de geofence**. Para fazer isso, acesse **Elementos de dados**. Procurar por **XDM - Evento de geofence** e clique em para abrir esse elemento de dados.

![Configuração do Launch](./images/rule5.png)

Você verá isso:

![Configuração do Launch](./images/rule6.png)

Navegar até o campo `_experience.campaign.orchestration.eventID`. Remova o valor atual e cole sua eventID lá.

Como lembrete, a ID do evento pode ser encontrada no Adobe Journey Optimizer em **Configurações > Eventos** e você encontrará a ID do evento na carga de amostra do seu par, que tem a seguinte aparência: `"eventID": "fa42ab7982ba55f039eacec24c1e32e5c51b310c67f0fa559ab49b89b63f4934"`.

![ACOP](./images/payloadeventID.png)

Em seguida, você deve definir sua cidade neste elemento de dados. Ir para **placeContext > geo > cidade** e entrar em uma cidade de escolha. Em seguida, clique em **Salvar** ou **Salvar na biblioteca**.

![ACOP](./images/payloadeventIDgeo.png)

Por fim, é necessário publicar as alterações. Ir para **Fluxo de publicação** no menu esquerdo.

![Configuração do Launch](./images/rule8.png)

Clique em **Adicionar todos os recursos alterados** e, em seguida, clique em **Salvar e criar no desenvolvimento**.

![Configuração do Launch](./images/rule9.png)

## 8.5.2 Acione sua jornada

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

Abra o painel Visualizador de perfil e acesse Perfil do cliente em tempo real. No painel Visualizador de perfil, você deve ver todos os seus dados pessoais exibidos, como o email e os identificadores de telefone adicionados recentemente.

![Demonstração](../module2/images/pv11.png)

No painel Visualizador de perfil, clique em **UTILITÁRIOS**. Enter `geofenceevent` e clique em **Enviar**.

![Demonstração](./images/smsdemo1.png)

Alguns segundos depois, você receberá um SMS do Adobe Journey Optimizer.

![Demonstração](./images/smsdemo4.png)

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao Módulo 8](journey-orchestration-external-weather-api-sms.md)

[Voltar para todos os módulos](../../overview.md)
