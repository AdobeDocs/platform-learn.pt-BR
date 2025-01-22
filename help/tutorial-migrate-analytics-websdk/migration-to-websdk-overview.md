---
title: Migrar o Adobe Analytics para o Web SDK usando tags
description: Saiba mais sobre as etapas que você seguirá durante a migração para o Web SDK, bem como as decisões que precisarão ser tomadas ao longo do caminho.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16755
exl-id: e578b669-42b4-46ae-b6e6-6688e5c5c772
source-git-commit: 47b970e3659fe7ebfdf491d9c0e9356128013fb9
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 0%

---

# Migrar o Adobe Analytics para o Web SDK usando tags

Saiba mais sobre as etapas para migrar uma implementação do Adobe Analytics usando a extensão do Analytics em Tags de Experience Platform (conhecida anteriormente como Launch) para o Web SDK, usando a extensão do Web SDK também em Tags. Quando a extensão do Adobe Analytics em tags é usada, nos bastidores o código &quot;AppMeasurement.js&quot; está sendo usado. Portanto, você pode pensar nisso como um tutorial que está migrando o AppMeasurement para o Web SDK, mas este tutorial está totalmente em Tags e NÃO abrange a movimentação para ou de uma implementação do JavaScript (com exceção do código JavaScript usado na interface do usuário de Tags). Para migração de implementações do JavaScript, consulte a [documentação](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/appmeasurement-to-web-sdk).

## O que você aprenderá com este tutorial

Antes de seguirmos as etapas de migração da sua implementação do Analytics, é importante que você entenda exatamente o que estará fazendo, ou seja, alterando/atualizando a _implementação_ do Analytics. Ao final deste tutorial, quando você entra em seus relatórios e tudo é o mesmo, você pode se perguntar: &quot;Por que fiz tudo isso?&quot; Existem outros documentos para destacar os benefícios de usar o Web SDK para a implementação do Analytics, mas alguns são:

1. Suporte para ID de dispositivo próprio
1. Melhor desempenho
1. Prova de obsolescência de sua implementação à medida que você avança para o uso de aplicativos do Adobe Experience Platform (habilitando novos casos de uso)

Entre em contato com seu representante da Adobe Analytics para saber mais sobre como a Web SDK pode ajudar você. À medida que avançamos com este tutorial, nos concentraremos em _como_ para fazer a migração.

>[!IMPORTANT]
>
>É importante observar que um dos principais motivos pelos quais você está fazendo essa migração da sua implementação é para se preparar para usar os aplicativos da Adobe Experience Platform, como o Customer Journey Analytics, Real-Time CDP ou Journey Optimizer (conforme observado em #3 acima). Usar os dados do site para essa finalidade incluirá etapas adicionais que não estão incluídas neste tutorial, mas este tutorial certamente será um pré-requisito para esse avanço adicional da implementação. Portanto, siga este tutorial e execute as etapas necessárias para enviar esses mesmos dados do site para o Experience Platform.

## Método de migração

Provavelmente, há muitas maneiras de fazer esse processo de migração, mas precisamos conversar sobre dois exatamente aqui:

**Método 1:** atualize sua propriedade Tags existente para o Web SDK, criando novos elementos de dados e fazendo alterações nas regras que já existem em sua propriedade.

**Método 2:** Você também pode criar uma nova propriedade (copiando a existente ou criando uma nova) e depois configurar essa nova propriedade com o Web SDK em vez da extensão do Adobe Analytics.

**Neste tutorial de migração, vamos usar o Método 1.** Dessa forma, os códigos incorporados associados à propriedade já estão incorporados aos seus sites de desenvolvimento, preparo e produção, portanto, não será necessário alterar nenhum código incorporado. Se você decidir seguir com o Método 2, não se esqueça de obter os novos códigos incorporados para cada ambiente da seção **Ambientes** da nova propriedade e colocá-los na seção de cabeçalho do site.

>[!NOTE]
>
>Embora editemos nossa propriedade existente em Tags durante essa migração, ainda é uma boa ideia ter cuidado. Portanto, é altamente recomendável fazer uma cópia da propriedade atual antes de iniciar a migração. Dessa forma, você sempre pode acessar a cópia e ver como as coisas eram antes de alterá-las, extrair o código dela etc.
>É bom ter cuidado, por via das dúvidas. Vá em frente e faça a cópia da propriedade. Vou esperar aqui até você voltar.

## Etapas para migrar a implementação do Analytics para o Web SDK

À medida que você percorre as etapas, é importante compreender algumas limitações:

1. Primeiro, você pode ou não precisar de todas essas etapas. Por exemplo, há uma lição sobre a migração de código personalizado. Se você tiver uma implementação de Tags que não usa código personalizado (incluindo o uso de Plug-ins), não será necessária esta lição. Tentamos incluir as lições que seriam necessárias para a maioria das pessoas, portanto, leia pelo menos as lições para ver se você precisa fazer ajustes no site durante a migração.
1. Além disso, não há como criar um tutorial de migração que abrangerá 100% dos casos de uso que todos estão usando. Como dito no item anterior, tentamos incluir as lições que a maioria das pessoas precisará e que cobrirão a maioria dos principais casos de uso. No entanto, haverá, sem dúvida, casos de uso que não serão abordados neste tutorial. Nesse caso, veja se as lições incluídas fornecem uma boa ideia de como você deve migrar para o seu caso de uso. Você também pode solicitar que seus colegas da [Comunidade Experience League coletem dados](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/ct-p/adobe-launch-community).

O processo de migração envolve as seguintes etapas principais:

1. Crie um conjunto de relatórios de validação de migração.
1. Criar e configurar um fluxo de dados.
1. Adicione e configure a extensão Web SDK em Tags (antigo Adobe Launch).
1. Crie um novo elemento de dados para enviar dados pelo Web SDK.
1. Migre sua regra de carregamento de página padrão para usar o elemento de dados e as ações do Web SDK.
1. Migrar código personalizado em regras ou para plug-ins.
1. Publish suas alterações de implementação.
1. Entenda como depurar e validar suas alterações e como validar sua regra de carregamento de página padrão e as variáveis associadas a ela. Essa validação deve continuar durante toda a migração, à medida que você faz alterações.
1. Migrar regras de carregamento de página adicionais.
1. Migrar regras de links personalizados.
1. Após a validação completa, remova as referências à extensão do Analytics e remova a própria extensão.
1. Depois de fazer todas as alterações, envie a biblioteca para preparo e, em seguida, para produção.
1. Depois que tudo estiver concluído, teste novamente. Isso é necessário porque você fez alterações removendo as referências ao código antigo do Analytics e deseja garantir que tudo ainda funcione corretamente.

>[!NOTE]
>
>Temos o compromisso de ajudar você a ter sucesso com a migração do Analytics para o Web SDK. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, fale conosco ao postar em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-analytics-to-web-sdk-using/m-p/732308#M604){target="_blank"}.

