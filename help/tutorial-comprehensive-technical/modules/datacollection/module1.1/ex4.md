---
title: Foundation - Configuração da coleção de dados da Adobe Experience Platform e da extensão SDK da Web - Coleção de dados da Web do cliente
description: Foundation - Configuração da coleção de dados da Adobe Experience Platform e da extensão SDK da Web - Coleção de dados da Web do cliente
kt: 5342
doc-type: tutorial
source-git-commit: c6ba1f751f18afe39fb6b746a62bc848fa8ec9bf
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# 1.1.4 Coleta de dados da Web no lado do cliente

## 1.1.4.1 Validar os dados na solicitação

### Instale o Adobe Experience Platform Debugger

O Experience Platform Debugger é uma extensão disponível para os navegadores Chrome e Firefox que ajuda a visualizar a tecnologia de Adobe implementada nas páginas da Web. Baixe a versão do seu navegador de preferência:

- [Extensão do Firefox](https://addons.mozilla.org/pt-BR/firefox/addon/adobe-experience-platform-dbg/)

- [Extensão do Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Se você nunca tiver usado o Debugger antes (e este é diferente do Adobe Experience Cloud Debugger anterior), assista a este vídeo de visão geral de cinco minutos:

>[!VIDEO](https://video.tv.adobe.com/v/32156?quality=12&learn=on)

Como você carregará o site de demonstração no modo incógnito, é necessário garantir que o Experience Platform Debugger também esteja disponível no modo incógnito. Para fazer isso, vá para **chrome://extensions** em seu navegador e abra a extensão do Depurador Experience Platform.

Verifique se essas duas configurações estão ativadas:

- Modo de desenvolvedor
- Permitir em incógnito

![Página inicial do EXP News](./images/ext1.png)

### Abrir o site de demonstração

Ir para [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Depois de fazer logon com sua Adobe ID, você verá isso. Clique no projeto do site para abri-lo.

![DSN](./../../gettingstarted/gettingstarted/images/web8.png)

Na página **Screens**, clique em **Executar**.

![DSN](./images/web2.png)

Você verá seu site de demonstração aberto. Selecione o URL e copie-o para a área de transferência.

![DSN](./../../gettingstarted/gettingstarted/images/web3.png)

Abra uma nova janela incógnita do navegador.

![DSN](./../../gettingstarted/gettingstarted/images/web4.png)

Cole o URL do site de demonstração que você copiou na etapa anterior. Você será solicitado a fazer logon usando sua Adobe ID.

![DSN](./../../gettingstarted/gettingstarted/images/web5.png)

Selecione o tipo de conta e conclua o processo de logon.

![DSN](./../../gettingstarted/gettingstarted/images/web6.png)

Em seguida, você verá seu site carregado em uma janela incógnita do navegador. Para cada demonstração, será necessário usar uma janela do navegador nova e incógnita para carregar o URL do site de demonstração.

![DSN](./../../gettingstarted/gettingstarted/images/web7.png)

### Use o Depurador de Experience Platform para ver as chamadas que vão para o Edge

Certifique-se de abrir o site de demonstração e clique no ícone da extensão Experience Platform Debugger.

![Página inicial do EXP News](./images/ext2.png)

O Debugger abrirá e mostrará os detalhes da implementação criada na propriedade Coleção de dados da Adobe Experience Platform. Lembre-se de que você está depurando a extensão e as regras que acabou de editar.

Clique no botão **[!UICONTROL Entrar]** na parte superior direita para autenticar. Se você já tiver uma guia do navegador aberta com a interface da Coleção de dados da Adobe Experience Platform, a etapa de autenticação será automática e você não precisará inserir seu nome de usuário e senha novamente.

![Depurador da AEP](./images/validate2.png)

Clique no botão Recarregar no site de demonstração para conectar o depurador a essa guia específica.

![Depurador da AEP](./images/validate2a.png)

Confirme se o Depurador está **[!UICONTROL Conectado à Página Inicial]**, como mostrado acima, e clique no ícone **[!UICONTROL bloquear]** para bloquear o Depurador para o site de demonstração. Se você não fizer isso, o Debugger continuará alternando para expor os detalhes de implementação de qualquer guia do navegador em foco, o que pode ser confuso.

![Depurador da AEP](./images/validate3.png)

Em seguida, vá para qualquer página no site de demonstração como, por exemplo, a página de categoria **Homens**.

![Extensão AEP Web SDK do Depurador da AEP](./images/validate4.png)

Agora clique em **[!UICONTROL Experience Platform Web SDK]** na navegação à esquerda, para ver as **[!UICONTROL Solicitações de rede]**.

Cada solicitação contém uma linha **[!UICONTROL events]**.

![Extensão AEP Web SDK do Depurador da AEP](./images/validate5.png)

Clique para abrir a linha **[!UICONTROL eventos]**. Observe como você pode ver o evento **web.webpagedetails.pageViews**, bem como outras variáveis prontas para uso que seguem o formato **ExperienceEvent XDM do SDK da Web**.

![Valor dos eventos](./images/validate8.png)

Esses tipos de detalhes de solicitação também estão visíveis na guia Rede. Filtre solicitações com **interaja** para localizar as solicitações enviadas pelo SDK da Web. Você pode encontrar todos os detalhes da carga XDM nos Cabeçalhos da carga de solicitação:

![Guia Rede](./images/validate9.png)

Próxima etapa: [1.1.5 Implementar Adobe Analytics e Adobe Audience Manager](./ex5.md)

[Voltar ao módulo 1.1](./data-ingestion-launch-web-sdk.md)

[Voltar a todos os módulos](./../../../overview.md)
