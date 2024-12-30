---
title: Adobe Journey Optimizer - Fontes de dados externas e ações personalizadas
description: Adobe Journey Optimizer - Fontes de dados externas e ações personalizadas
kt: 5342
doc-type: tutorial
exl-id: 068c8be4-2e9e-4d38-9c0e-f769ac927b57
source-git-commit: c531412a2c0a5c216f49560e01fb26b9b7e71869
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---

# 3.2.5 Acionar a jornada

Neste exercício, você testará e acionará a jornada configurada neste módulo.

## 3.2.5.1 Atualizar a configuração do evento geofence

Vá para [Coleção de dados do Adobe Experience Platform](https://experience.adobe.com/launch/) e selecione **Marcas**.

Esta é a página Propriedades da coleção de dados do Adobe Experience Platform que você viu antes.

![Página de propriedades](./../../../modules/datacollection/module1.1/images/launch1.png)

Em **Introdução**, o Sistema de Demonstração criou duas propriedades do Cliente para você: uma para o site e outra para o aplicativo móvel. Localize-os procurando por `--aepUserLdap--` na caixa **[!UICONTROL Pesquisar]**. Clique para abrir a propriedade **Web**.

![Caixa de pesquisa](./../../../modules/datacollection/module1.1/images/property6.png)

Você verá isso.

![Iniciar Instalação](./images/rule1.png)

No menu esquerdo, vá para **Regras** e procure pela regra **Evento de geofence**. Clique na regra **Evento de geofence** para abri-la.

![Iniciar Instalação](./images/rule2.png)

Você verá os detalhes dessa regra. Clique para abrir a ação **Adobe Experience Platform Web SDK - Enviar evento**.

![Iniciar Instalação](./images/rule3.png)

Você verá que, quando essa ação for acionada, um elemento de dados específico será usado para definir a estrutura de dados XDM. Você precisa atualizar esse elemento de dados e definir a **ID de Evento** do evento que você configurou no [Exercício 3.2.1](./ex1.md).

![Iniciar Instalação](./images/rule4.png)

Agora é necessário atualizar o elemento de dados **XDM - Evento de geofence**. Para fazer isso, vá para **Elementos de dados**. Pesquise por **XDM - Evento de geofence** e clique em para abrir esse elemento de dados.

![Iniciar Instalação](./images/rule5.png)

Você verá isto:

![Iniciar Instalação](./images/rule6.png)

Navegue até o campo `_experience.campaign.orchestration.eventID`. Remova o valor atual e cole sua eventID lá.

Lembrando que a ID de Evento pode ser encontrada no Adobe Journey Optimizer em **Configurações > Eventos**, e você encontrará a ID de evento na carga de exemplo do seu evento, que tem esta aparência: `"eventID": "4df8dc10731eba7b0c37af83a9db38d4de7aa6aebcce38196d9d47929b9c598e"`.

![ACOP](./images/payloadeventID.png)

Em seguida, você deve definir sua cidade neste elemento de dados. Vá para **placeContext > geo > city** e insira uma cidade da escolha. Em seguida, clique em **Salvar** ou **Salvar na Biblioteca**.

![ACOP](./images/payloadeventIDgeo.png)

Por fim, você precisa publicar suas alterações. Vá para **Fluxo de Publicação** no menu esquerdo e clique em **Man** para abrir sua biblioteca.

![Iniciar Instalação](./images/rule8.png)

Clique em **Adicionar todos os recursos alterados** e em **Salvar e criar no desenvolvimento**.

![Iniciar Instalação](./images/rule9.png)

## 3.2.5.2 Acionar a jornada

Ir para [https://dsn.adobe.com](https://dsn.adobe.com). Depois de fazer logon com sua Adobe ID, você verá isso. Clique nos 3 pontos **...** do projeto do site e clique em **Executar** para abri-lo.

![DSN](./../../datacollection/module1.1/images/web8.png)

Você verá seu site de demonstração aberto. Selecione o URL e copie-o para a área de transferência.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Abra uma nova janela incógnita do navegador.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Cole o URL do site de demonstração que você copiou na etapa anterior. Você será solicitado a fazer logon usando sua Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Selecione o tipo de conta e conclua o processo de logon.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Em seguida, você verá seu site carregado em uma janela incógnita do navegador. Para cada exercício, será necessário usar uma janela do navegador nova e incógnita para carregar o URL do site de demonstração.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

Clique no ícone do logotipo do Adobe no canto superior esquerdo da tela para abrir o Visualizador de perfis.

![Demonstração](./../../../modules/datacollection/module1.2/images/pv1.png)

Abra o painel Visualizador de perfis e vá para Perfil do cliente em tempo real. No painel Visualizador de perfis, você deve ver todos os seus dados pessoais exibidos, como emails recém-adicionados e identificadores de telefone.

![Demonstração](./images/pv2.png)

No painel Visualizador de perfis, clique em **UTILITÁRIOS**. Insira `geofenceevent` e clique em **Enviar**.

>[!NOTE]
>
>Caso não tenha a opção, no painel Visualizador de Perfis, de enviar um evento de chamada direta, você poderá enviar um manualmente abrindo o Modo de Exibição de Desenvolvedor do seu navegador e acessando o **Console**. Em seguida, cole e envie este comando: `_satellite.track('geofenceevent')`.

Alguns segundos depois, você verá a mensagem do Adobe Journey Optimizer aparecer no canal Slack.

![Demonstração](./images/smsdemo4.png)

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao módulo 3.2](journey-orchestration-external-weather-api-sms.md)

[Voltar a todos os módulos](../../../overview.md)
