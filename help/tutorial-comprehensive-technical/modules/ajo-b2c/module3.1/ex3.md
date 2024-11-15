---
title: Atualizar a ID de configuração e testar a Jornada
description: Atualizar a ID de configuração e testar a Jornada
kt: 5342
doc-type: tutorial
exl-id: 6807f93d-bd44-4f63-8005-6819c9f5f1ed
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# 3.1.3 Atualize a propriedade Coleção de dados e teste a jornada

## 3.1.3.1 Atualizar a propriedade Coleção de dados

Vá para [Coleção de dados do Adobe Experience Platform](https://experience.adobe.com/launch/) e selecione **Marcas**.

Esta é a página Propriedades da coleção de dados do Adobe Experience Platform que você viu antes.

![Página de propriedades](./../../../modules/datacollection/module1.1/images/launch1.png)

No módulo 0, o Sistema de demonstração criou duas propriedades do cliente para você: uma para o site e outra para o aplicativo móvel. Localize-os procurando por `--aepUserLdap--` na caixa **[!UICONTROL Pesquisar]**. Clique para abrir a propriedade **Web**.

![Caixa de pesquisa](./../../../modules/datacollection/module1.1/images/property6.png)

Você verá isso.

![Iniciar Instalação](./images/rule1.png)

No menu esquerdo, vá para **Regras** e procure a regra **Registrar perfil**. Clique na regra **Registrar perfil** para abri-la.

![Iniciar Instalação](./images/rule2.png)

Você verá os detalhes dessa regra. Clique para abrir a ação **Enviar &quot;Evento de Registro&quot; para a AEP - acionar JO**.

![Iniciar Instalação](./images/rule3.png)

Você verá que, quando essa ação for acionada, um elemento de dados específico será usado para definir a estrutura de dados XDM. Você precisa atualizar esse elemento de dados e definir a **ID de Evento** do evento que você configurou no [Exercício 7.1](./ex1.md).

![Iniciar Instalação](./images/rule4.png)

Agora é necessário atualizar o elemento de dados **XDM - Evento de registro**. Para fazer isso, vá para **Elementos de dados**. Pesquise por **XDM - Evento de Registro** e clique em para abrir esse elemento de dados.

![Iniciar Instalação](./images/rule5.png)

Você verá isto:

![Iniciar Instalação](./images/rule6.png)

Navegue até o campo `_experience.campaign.orchestration.eventID`. Remova o valor atual e cole sua eventID lá.

Lembrando que a ID de Evento pode ser encontrada no Adobe Journey Optimizer em **Configurações > Eventos**, e você encontrará a ID de evento na carga de exemplo do seu evento, que tem esta aparência: `"eventID": "227402c540eb8f8855c6b2333adf6d54d7153d9d7d56fa475a6866081c574736"`.

![ACOP](./images/payloadeventID.png)

Depois de colar a eventID, a tela deve ter esta aparência. Em seguida, clique em **Salvar** ou **Salvar na Biblioteca**.

![Iniciar Instalação](./images/rule7.png)

Por fim, você precisa publicar suas alterações. Vá para **Fluxo de Publicação** no menu esquerdo.

![Iniciar Instalação](./images/rule8.png)

Clique em **Adicionar todos os recursos alterados** e em **Salvar e criar no desenvolvimento**.

![Iniciar Instalação](./images/rule9.png)

Sua biblioteca será atualizada e, após 1 a 2 minutos, você poderá testar sua configuração.

## 3.1.3.2 Testar a Jornada

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

1 minuto após a criação da sua conta, você receberá um email da Adobe Journey Optimizer sobre a criação da conta.

![Iniciar Instalação](./images/email.png)

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao módulo 3.1](./journey-orchestration-create-account.md)

[Voltar a todos os módulos](../../../overview.md)
