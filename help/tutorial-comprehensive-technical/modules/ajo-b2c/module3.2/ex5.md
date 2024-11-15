---
title: Adobe Journey Optimizer - API de clima externa, ação de SMS e muito mais - Acione a Jornada orquestrada do cliente
description: Adobe Journey Optimizer - API de clima externa, ação de SMS e muito mais - Acione a Jornada orquestrada do cliente
kt: 5342
doc-type: tutorial
exl-id: 068c8be4-2e9e-4d38-9c0e-f769ac927b57
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 1%

---

# 3.2.5 Acionar a jornada

Neste exercício, você testará e acionará a jornada configurada neste módulo.

## 3.2.5.1 Atualizar a configuração do evento geofence

Vá para [Coleção de dados do Adobe Experience Platform](https://experience.adobe.com/launch/) e selecione **Marcas**.

Esta é a página Propriedades da coleção de dados do Adobe Experience Platform que você viu antes.

![Página de propriedades](./../../../modules/datacollection/module1.1/images/launch1.png)

No módulo 0, o Sistema de demonstração criou duas propriedades do cliente para você: uma para o site e outra para o aplicativo móvel. Localize-os procurando por `--aepUserLdap--` na caixa **[!UICONTROL Pesquisar]**. Clique para abrir a propriedade **Web**.

![Caixa de pesquisa](./../../../modules/datacollection/module1.1/images/property6.png)

Você verá isso.

![Iniciar Instalação](./images/rule1.png)

No menu esquerdo, vá para **Regras** e procure pela regra **Evento de geofence**. Clique na regra **Evento de geofence** para abri-la.

![Iniciar Instalação](./images/rule2.png)

Você verá os detalhes dessa regra. Clique para abrir a ação **Enviar &quot;evento geofence&quot; para AEP - acionar JO**.

![Iniciar Instalação](./images/rule3.png)

Você verá que, quando essa ação for acionada, um elemento de dados específico será usado para definir a estrutura de dados XDM. Você precisa atualizar esse elemento de dados e definir a **ID de Evento** do evento que você configurou no [Exercício 8.1](./ex1.md).

![Iniciar Instalação](./images/rule4.png)

Agora é necessário atualizar o elemento de dados **XDM - Evento de geofence**. Para fazer isso, vá para **Elementos de dados**. Pesquise por **XDM - Evento de geofence** e clique em para abrir esse elemento de dados.

![Iniciar Instalação](./images/rule5.png)

Você verá isto:

![Iniciar Instalação](./images/rule6.png)

Navegue até o campo `_experience.campaign.orchestration.eventID`. Remova o valor atual e cole sua eventID lá.

Lembrando que a ID de Evento pode ser encontrada no Adobe Journey Optimizer em **Configurações > Eventos**, e você encontrará a ID de evento na carga de exemplo do seu evento, que tem esta aparência: `"eventID": "fa42ab7982ba55f039eacec24c1e32e5c51b310c67f0fa559ab49b89b63f4934"`.

![ACOP](./images/payloadeventID.png)

Em seguida, você deve definir sua cidade neste elemento de dados. Vá para **placeContext > geo > city** e insira uma cidade da escolha. Em seguida, clique em **Salvar** ou **Salvar na Biblioteca**.

![ACOP](./images/payloadeventIDgeo.png)

Por fim, você precisa publicar suas alterações. Vá para **Fluxo de Publicação** no menu esquerdo.

![Iniciar Instalação](./images/rule8.png)

Clique em **Adicionar todos os recursos alterados** e em **Salvar e criar no desenvolvimento**.

![Iniciar Instalação](./images/rule9.png)

## 3.2.5.2 Acionar a jornada

Ir para [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Depois de fazer logon com sua Adobe ID, você verá isso. Clique no projeto do site para abri-lo.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

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

Abra o painel Visualizador de perfis e vá para Perfil do cliente em tempo real. No painel Visualizador de perfis, você deve ver todos os seus dados pessoais exibidos, como emails recém-adicionados e identificadores de telefone.

![Demonstração](./../../../modules/datacollection/module1.2/images/pv11.png)

No painel Visualizador de perfis, clique em **UTILITÁRIOS**. Insira `geofenceevent` e clique em **Enviar**.

![Demonstração](./images/smsdemo1.png)

Alguns segundos depois, você receberá um SMS do Adobe Journey Optimizer.

![Demonstração](./images/smsdemo4.png)

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao módulo 3.2](journey-orchestration-external-weather-api-sms.md)

[Voltar a todos os módulos](../../../overview.md)
