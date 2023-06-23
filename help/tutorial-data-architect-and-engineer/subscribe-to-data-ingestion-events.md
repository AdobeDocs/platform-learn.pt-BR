---
title: Assinar eventos de assimilação de dados
seo-title: Subscribe to data ingestion events | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Assinar eventos de assimilação de dados
description: Nesta lição, você se inscreverá nos eventos de assimilação de dados configurando um webhook com o Console do Adobe Developer e uma ferramenta de desenvolvimento de webhook online. Você usará esses eventos para monitorar o status dos trabalhos de assimilação de dados nas lições subsequentes.
role: Data Engineer
feature: Data Management
jira: KT-4348
thumbnail: 4348-subscribe-to-data-ingestion-events.jpg
exl-id: f4b90832-4415-476f-b496-2f079b4fcbbc
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 1%

---

# Assinar eventos de assimilação de dados

<!--25min-->

Nesta lição, você se inscreverá nos eventos de assimilação de dados configurando um webhook com o Console do Adobe Developer e uma ferramenta de desenvolvimento de webhook online. Você usará esses eventos para monitorar o status dos trabalhos de assimilação de dados nas lições subsequentes.

**Engenheiros de dados** O desejará assinar eventos de assimilação de dados fora deste tutorial.
**Arquitetos de dados** _pode ignorar esta lição_ e vá para a página [lição de assimilação em lote](ingest-batch-data.md).

## Permissões necessárias

No [Configurar permissões](configure-permissions.md) você configura todos os controles de acesso necessários para concluir esta lição, especificamente:

<!--* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

>[!IMPORTANT]
>
> Essas notificações acionadas pelos eventos de assimilação de dados serão aplicadas a _todas as suas sandboxes_, não apenas o seu `Luma Tutorial`. Você também pode ver notificações originadas de outros eventos de assimilação de dados em sua conta.


## Configurar um webhook

Neste exercício, criaremos um webhook usando uma ferramenta online chamada webhook.site (sinta-se livre para substituir qualquer outra ferramenta de desenvolvimento de webhook que preferir usar):

1. Em outra guia do navegador, abra o site [https://webhook.site/](https://webhook.site/)
1. Você recebe um URL exclusivo, que deve ser marcado, conforme retornado posteriormente nas lições de assimilação de dados:

   ![Webhook.site](assets/ioevents-webhook-home.png)
1. Selecione o **Editar** botão na navegação superior
1. Como corpo da Resposta, informe `$request.query.challenge$`. As notificações de Adobe I/O Eventos que configuramos posteriormente nesta lição enviam um desafio para o webhook e exigem que ele seja incluído no corpo da resposta.
1. Selecione o botão **Salvar**

   ![Editar a resposta](assets/ioevents-webhook-editResponse.png)

## Configurar

1. Em outra guia do navegador, abra [Console do Adobe Developer](https://console.adobe.io/)
1. Abra o `Luma Tutorial API Project`
1. Selecione o **[!UICONTROL Adicionar ao projeto]** e selecione **[!UICONTROL Evento]**

   ![Adicionar evento](assets/ioevents-addEvents.png)
1. Filtrar a lista selecionando **[!UICONTROL Experience Platform]**
1. Selecionar **[!UICONTROL Notificações da plataforma]**
1. Selecione o **[!UICONTROL Próxima]** botão
   ![Adicionar as notificações](assets/ioevents-addNotifications.png)
1. Selecionar todos os eventos
1. Selecione o **[!UICONTROL Próxima]** botão
   ![Selecionar as assinaturas](assets/ioevents-addSubscriptions.png)
1. Na próxima tela para configurar credenciais, selecione o **[!UICONTROL Próxima]** botão novamente
   ![Ignorar a tela de credenciais](assets/ioevents-clickNext.png)
1. Como a variável **[!UICONTROL Nome de inscrição no evento]**, insira `Platform notifications`
1. Role para baixo e selecione para abrir a **[!UICONTROL Webhook]** seção
1. Como a variável **[!UICONTROL URL do Webhook]**, cole o valor do **Seu URL exclusivo** campo do webhook.site
1. Selecione o **[!UICONTROL Salvar eventos configurados]** botão
   ![Salvar os eventos](assets/ioevents-addWebhook.png)
1. Aguarde até que sua configuração seja salva e você deverá ver que sua `Platform notifications` O evento está Ativo com os detalhes do seu webhook e sem mensagens de erro
   ![Configuração salva](assets/ioevents-webhookConfigured.png)
1. Volte para a guia webhook.site e você deverá ver a primeira solicitação para o webhook, resultante da validação da configuração do Console do desenvolvedor:
   ![Primeira solicitação no webhook.site](assets/ioevents-webhook-firstRequest.png)

Pronto por enquanto, você aprenderá mais sobre essas notificações nas próximas lições ao assimilar dados.

## Recursos adicionais

* [Webhook.site](https://webhook.site/)
* [Documentação de notificações de assimilação de dados](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html)
* [Introdução à documentação de Adobe I/O Events](https://www.adobe.io/apis/experienceplatform/events/docs.html)

Ok, vamos finalmente começar [assimilação de dados](ingest-batch-data.md)!
