---
title: Alternar ambientes de tag com o Adobe Experience Cloud Debugger
description: Saiba como usar o Experience Cloud Debugger para carregar diferentes códigos incorporados de tag. Esta lição é parte do tutorial Implementar a Experience Cloud em sites.
exl-id: 29972a00-e5e0-4fe0-a71c-c2ca106938be
source-git-commit: 1fc027db2232c8c56de99d12b719ec10275b590a
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 23%

---

# Alternar ambientes de tag com o Experience Cloud Debugger

Nesta lição, você usará a [extensão do Adobe Experience Platform Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) para substituir a propriedade de tag codificada no [site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html) com sua própria propriedade.


>[!WARNING]
>
> O site do Luma usado neste tutorial deve ser substituído durante a semana de 16 de fevereiro de 2026. O trabalho realizado como parte deste tutorial pode não se aplicar ao novo site.

Essa técnica é chamada de alternação de ambiente e será útil posteriormente, ao trabalhar com tags em seu próprio site. Você poderá carregar seu site de produção em seu navegador, mas com seu ambiente de tag de *desenvolvimento*. Isso permite fazer e validar de forma segura as alterações nas tags independentemente das suas versões de código normais.  Afinal, essa separação das versões de tag de marketing das versões regulares de código é um dos principais motivos pelos quais os clientes usam tags!

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo integrado à Adobe Experience Platform como um conjunto de tecnologias de coleção de dados. Várias alterações de terminologia foram implementadas na interface do que você deve estar ciente ao usar esse conteúdo:
>
> * O Platform Launch (lado do cliente) agora é **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)**
> * O Platform Launch Server Side agora é **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=pt-BR)**
> * As configurações do Edge agora são **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=pt-BR)**

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Usar o Debugger para carregar um ambiente de tag alternativo
* Usar o Debugger para validar que você carregou um ambiente de tag alternativo

## Obter o URL do seu ambiente de desenvolvimento

1. Na propriedade da tag, abra a página `Environments`

1. Na linha **[!UICONTROL Desenvolvimento]**, clique no ícone Instalar ![ícone Instalar](images/launch-installIcon.png) para abrir a modal

1. Clique no ![ícone Copiar](images/launch-copyIcon.png) para copiar o código incorporado na área de transferência

1. Clique em **[!UICONTROL Fechar]** para fechar a modal

   ![Ícone Instalar](images/launch-copyInstallCode.png)

## Substitua o URL da tag no site de demonstração Luma

1. Abra o [site de demonstração Luma](https://luma.enablementadobe.com/content/luma/us/en.html) no navegador Chrome

1. Abra a [extensão do Experience Platform Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) clicando no ícone ![Debugger](images/icon-debugger.png)

   ![Clique no ícone Depurador](images/switchEnvironments-openDebugger.png)

1. Observe que a propriedade de tag implementada no momento é mostrada na guia Resumo

   ![ambiente de tag mostrado no Depurador](images/switchEnvironments-debuggerOnWeRetail-prod.png)

1. Acesse a guia Ferramentas
1. Role até a seção **[!UICONTROL Substituir código incorporado do Launch]**
1. Verifique se a guia Chrome com o site Luma está em foco atrás do Debugger (não a guia com este tutorial ou a guia com a interface da Coleção de dados).  Cole o código incorporado que está na área de transferência no campo de entrada
1. Ative o recurso &quot;Aplicar em luma.enablementadobe.com&quot; para que todas as páginas do site Luma mapeiem para a propriedade de tag
1. Clique no botão **[!UICONTROL Salvar]**

   ![ambiente de tag mostrado no Depurador](images/switchEnvironments-debugger-save.png)

1. Recarregue o site Luma e verifique a guia Resumo do Debugger. Na seção Launch, você deve ver que sua propriedade de desenvolvimento está sendo usada. Confirme se o nome da propriedade corresponde ao nome da sua e se “desenvolvimento” está escrito no ambiente.

   ![ambiente de tag mostrado no Depurador](images/switchEnvironments-debuggerOnWeRetail.png)

>[!NOTE]
>
>O Debugger salvará essa configuração e substituirá os códigos incorporados da tag sempre que você voltar ao site Luma. Isso não afeta outros sites que você visitar em outras guias abertas. Para interromper a substituição do código incorporado por parte do Debugger, clique no botão **[!UICONTROL Remover]** ao lado do código incorporado na guia Ferramentas do Debugger.

À medida que você prossegue no tutorial, usará essa técnica de mapear o site Luma para sua própria propriedade de tag para validar sua implementação de tag. Ao começar a usar tags no site de produção, você pode usar essa mesma técnica para validar as alterações.

[Próximo: &quot;Adicionar o serviço de identidade da Adobe Experience Platform&quot; >](id-service.md)
