---
title: Atualizar a ID de configuração e testar a Jornada
description: Atualizar a ID de configuração e testar a Jornada
kt: 5342
doc-type: tutorial
source-git-commit: 2bd4249d96eb697da66db68895761f8b0bd6e638
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 1%

---

# 3.1.3 Atualize a propriedade Coleção de dados e teste a jornada

## 3.1.3.1 Atualizar a propriedade Coleção de dados

Vá para [Coleção de dados do Adobe Experience Platform](https://experience.adobe.com/launch/) e selecione **Marcas**.

![Página de propriedades](./../../../modules/datacollection/module1.1/images/launch1.png)

Em **Introdução**, o Sistema de Demonstração criou duas propriedades do Cliente para você: uma para o site e outra para o aplicativo móvel. Localize-os procurando por `--aepUserLdap--` na caixa **[!UICONTROL Pesquisar]**. Clique para abrir a propriedade **Web**.

![Caixa de pesquisa](./../../../modules/datacollection/module1.1/images/property6.png)

Você verá isso.

![Iniciar Instalação](./images/rule1.png)

No menu esquerdo, vá para **Regras** e procure a regra **Criar conta**. Clique na regra **Criar conta** para abri-la.

![Iniciar Instalação](./images/rule2.png)

Você verá os detalhes dessa regra. Clique para abrir a ação **Enviar Evento de Experiência &quot;Evento de Registro&quot;**.

![Iniciar Instalação](./images/rule3.png)

Você verá que, quando essa ação for acionada, um elemento de dados específico será usado para definir a estrutura de dados XDM. Você precisa atualizar esse elemento de dados e definir a **ID de Evento** do evento que você configurou no [Exercício 3.1.1](./ex1.md).

![Iniciar Instalação](./images/rule4.png)

Agora é necessário atualizar o elemento de dados **XDM - Evento de registro**. Para fazer isso, vá para **Elementos de dados**. Procure por **XDM - Registro** e clique para abrir esse elemento de dados.

![Iniciar Instalação](./images/rule5.png)

Você verá isto:

![Iniciar Instalação](./images/rule6.png)

Navegue até o campo `_experience.campaign.orchestration.eventID`. Remova o valor atual e cole sua eventID lá.

Lembrando que a ID de Evento pode ser encontrada no Adobe Journey Optimizer em **Configurações > Eventos**, e você encontrará a ID de evento na carga de exemplo do seu evento, que tem esta aparência: `"eventID": "5ae9b8d3f68eb555502b0c07d03ef71780600c4bd0373a4065c692ae0bfbd34d"`.

![ACOP](./images/payloadeventID.png)

Depois de colar a eventID, a tela deve ter esta aparência. Em seguida, clique em **Salvar** ou **Salvar na Biblioteca**.

![Iniciar Instalação](./images/rule7.png)

Por fim, você precisa publicar suas alterações. Vá para **Fluxo de Publicação** no menu esquerdo e clique para abrir sua biblioteca **Principal**.

![Iniciar Instalação](./images/rule8.png)

Clique em **Adicionar todos os recursos alterados** e em **Salvar e criar no desenvolvimento**.

![Iniciar Instalação](./images/rule9.png)

Sua biblioteca será atualizada e, após 1 a 2 minutos, você poderá testar sua configuração.

## 3.1.3.2 Testar a Jornada

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

Consulte o painel Visualizador de perfis e o Perfil do cliente em tempo real com a **ID de Experience Cloud** como o identificador principal para este cliente atualmente desconhecido. Clique em **Fazer logon**.

![Demonstração](./../../../modules/datacollection/module1.2/images/pv2.png)

Clique em **CRIAR UMA CONTA**.

![Demonstração](./../../../modules/datacollection/module1.2/images/pv9.png)

Preencha seus detalhes e clique em **Registrar**; depois disso, você será redirecionado para a página anterior.

![Demonstração](./../../../modules/datacollection/module1.2/images/pv10.png)

Abra o painel Visualizador de perfis e vá para Perfil do cliente em tempo real. No painel Visualizador de perfis, você deve ver todos os seus dados pessoais exibidos, como emails recém-adicionados e identificadores de telefone.

![Demonstração](./../../../modules/datacollection/module1.2/images/pv11.png)

1 minuto após a criação da sua conta, você receberá um email da Adobe Journey Optimizer sobre a criação da conta.

![Iniciar Instalação](./images/email.png)

Você também verá a entrada da jornada e o progresso pela jornada no painel da jornada no Journey Optimizer.

![Iniciar Instalação](./images/emaildash.png)

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao módulo 3.1](./journey-orchestration-create-account.md)

[Voltar a todos os módulos](../../../overview.md)
