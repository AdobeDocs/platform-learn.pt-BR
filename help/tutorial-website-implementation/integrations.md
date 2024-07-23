---
title: Implementar integrações de Experience Cloud com tags
description: Saiba como validar as integrações do Audiences, A4T e Atributos do cliente na implementação da Adobe Experience Cloud. Esta lição é parte do tutorial Implementar o Experience Cloud nos sites.
exl-id: 1d02efce-a50a-4f4d-a0cf-eb8275cf0faa
source-git-commit: 2182441d992aec0602d0955d78aa85407bd770c9
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 85%

---

# Integrações da Experience Cloud

Nesta lição, você verificará as principais integrações entre as soluções que acabou de implementar. A boa notícia é que, ao completar as lições anteriores, já implementou os aspectos principais das integrações! Não é necessário fazer qualquer trabalho adicional nesta lição além de ler e validar.

## Objetivos de aprendizagem

No final desta lição, você poderá:

1. Explicar os casos de uso básicos para as integrações de Compartilhamento de público-alvo, Analytics para Target (A4T) e Atributos do cliente
1. Validar os aspectos básicos de implementação do lado do cliente nessas integrações

## Pré-requisitos

Você deve concluir todas as lições anteriores neste tutorial antes de seguir as instruções desta lição.

>[!NOTE]
>
>Muitos requisitos de permissões de usuário, configurações de conta e etapas de provisionamento que estão além do escopo deste tutorial são necessários para usar essas integrações. Se você ainda não estiver usando essas integrações na implementação atual da Experience Cloud, considere:
>
>* Analisar todos os requisitos das [integrações dos serviços principais](https://experienceleague.adobe.com/en/docs/core-services/interface/services/getting-started)
>* Analisar os requisitos completos da [integração do Analytics for Target](https://experienceleague.adobe.com/en/docs/target/using/integrate/a4t/before-implement)

## Audiences

O [Audiences](https://experienceleague.adobe.com/pt-br/docs/core-services/interface/services/audiences/overview) faz parte do serviço principal de pessoas e permite compartilhar públicos-alvo entre soluções. Por exemplo, você pode criar um público-alvo no Audience Manager e usá-lo para fornecer conteúdo personalizado ao Target.

Os principais requisitos para implementar o A4T—que você já fez—são:

1. Implementar o Serviço de identidade da Adobe Experience Platform
1. Implementar o Audience Manager
1. Implementar outras soluções que você deseja que recebam ou criem públicos-alvo, como o Target e o Analytics

### Validar a integração de públicos-alvo

A melhor maneira de validar a integração do Audiences é criar um público-alvo, compartilhá-lo em outra solução e usá-lo totalmente na outra solução (por exemplo, confirme se um visitante que se qualifica para um segmento do AAM pode se qualificar para uma atividade do Target direcionada a esse segmento). No entanto, isso está fora do escopo deste tutorial.

Essas etapas de validação se concentrarão na parte crítica visível na implementação do cliente: a ID do visitante.

1. Abra o [site Luma](https://luma.enablementadobe.com/content/luma/us/en.html).

1. Certifique-se de que o Depurador está mapeando a propriedade da tag para o *seu* ambiente de desenvolvimento, conforme descrito na [lição anterior](switch-environments.md)

   ![Seu ambiente de desenvolvimento de marcas mostrado no Depurador](images/switchEnvironments-debuggerOnWeRetail.png)

1. Acesse a guia Rede do Debugger

1. Clique em **[!UICONTROL Limpar todas as solicitações]** apenas para simplificar as coisas

1. Recarregue a página do Luma, certificando-se de que você vê as solicitações do Target e do Analytics no Debugger

1. Recarregue a página do Luma novamente

1. Agora você deve ver quatro solicitações na guia Rede do Debugger, duas para o Target e duas para o Analytics

1. Examine a linha denominada &quot;ID de visitante da Experience Cloud&quot;. As IDs em cada solicitação de cada solução devem ser sempre as mesmas.

   ![Confirmar os SDIDs correspondentes](images/integrations-matchingECIDs.png)

1. As IDs são exclusivas por visitante, o que você pode confirmar solicitando que um parceiro repita essas etapas.

## Analytics for Target (A4T)

A integração do [Analytics for Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) permite aproveitar seus dados do Analytics como fonte para as métricas de relatório no Target.

Os principais requisitos para implementar o A4T—que você já fez—são:

1. Implementar o Serviço de identidade da Adobe Experience Platform
1. Acione a solicitação de carregamento de página do Target antes do beacon de exibição de página do Analytics

O A4T funciona unindo uma solicitação do lado do servidor do Target ao Analytics com o beacon de exibição de página do Analytics, o que chamamos de &quot;agrupamento de ocorrência&quot;.  A ocorrência de identificação exige que a solicitação do Target que entrega a atividade (ou que incrementa uma métrica de objetivo com base no Target) tenha um parâmetro que corresponda a um parâmetro no beacon de exibição de página do Analytics. Esse parâmetro é chamado de ID de dados complementares (SDIDs).

### Validar a implementação do A4T

A melhor maneira de validar a integração do A4T é criar uma atividade do Target usando o A4T e validar os dados do relatório; no entanto, isso está além do escopo deste tutorial. Este tutorial mostrará como confirmar se as IDs de dados suplementares correspondem às chamadas de solução.

**Para validar os SDIDs**

1. Abra o [site Luma](https://luma.enablementadobe.com/content/luma/us/en.html).

1. Certifique-se de que o Depurador está mapeando a propriedade da tag para o *seu* ambiente de desenvolvimento, conforme descrito na [lição anterior](switch-environments.md)

   ![Seu ambiente de desenvolvimento de marcas mostrado no Depurador](images/switchEnvironments-debuggerOnWeRetail.png)

1. Acesse a guia Rede do Debugger

1. Clique em **[!UICONTROL Limpar todas as solicitações]** apenas para simplificar as coisas

1. Recarregue a página do Luma, certificando-se de que você vê as solicitações do Target e do Analytics no Debugger

1. Recarregue a página do Luma novamente

1. Agora você deve ver quatro solicitações na guia Rede do Debugger, duas para o Target e duas para o Analytics

1. Dê uma olhada na linha denominada &quot;ID de dados complementares&quot;. As IDs do primeiro carregamento da página devem corresponder entre o Target e o Analytics. As IDs do segundo carregamento da página também devem corresponder, mas serem diferentes das IDs do primeiro carregamento da página.

   ![Confirmar os SDIDs correspondentes](images/integrations-matchingSDIDs.png)

Se você fizer solicitações adicionais do Target no escopo de um carregamento de página (sem incluir aplicativos de página única) que fazem parte das atividades do A4T, atribua a eles nomes exclusivos (não target-global-mbox) para que continuem tendo os mesmos SDIDs das solicitações iniciais do Target e do Analytics.

## Atributos do cliente

Os [atributos do cliente](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html?lang=pt-BR) são parte do Serviço principal People, que permite carregar dados do banco de dados do gerenciamento de relacionamento com o cliente (CRM) e aproveitá-los no Adobe Analytics e no Adobe Target.

Os principais requisitos para implementar os Atributos do cliente—que você já fez—são:

1. Implementar o Serviço de identidade da Adobe Experience Platform
1. Definir as IDs do cliente por meio do Serviço de ID *antes* do Target e do Analytics acionarem as próprias solicitações, (o que você conseguiu usando o recurso de ordenação de regra nas tags)

### Validar a implementação dos Atributos do cliente

Você já validou que as IDs do cliente são passadas tanto para o Serviço de identidade quanto para o Target em lições anteriores. Também é possível validar a ID do cliente na ocorrência do Analytics. 
No momento, a ID do cliente é um dos poucos parâmetros que não aparecem no Experience Cloud Debugger, então você pode usar o JavaScript do navegador para exibi-lo.

1. Abra o site Luma
1. Abra as Ferramentas do desenvolvedor do seu navegador.
1. Vá até a guia Rede
1. No campo de filtro, digite `b/ss`, que limitará o que você vê às solicitações do Adobe Analytics

   ![Abra as Ferramentas do desenvolvedor e filtre a guia Rede para mostrar somente as solicitações do Analytics](images/aam-openTheJSConsole.png)

1. Clique no link **[!UICONTROL LOGON]** no canto superior direito do site

   ![Clique em Logon no canto superior direito](images/idservice-loginNav.png)

1. Digite `test@adobe.com` como nome de usuário
1. Digite `test` como senha
1. Clique no botão **[!UICONTROL LOGON]**

   ![Digite as credenciais e clique em logon](images/idservice-login.png)

1. Ele deve lhe direcionar à página inicial, que também acionará um beacon que você pode ver nas Ferramentas do desenvolvedor. Se você for levado para a página de informações da conta, clique no logotipo WE.RETAIL para retornar à página inicial.
1. Clique na solicitação e selecione a guia Cabeçalho
1. Role para baixo até ver alguns parâmetros aninhados
   1. cid - é delimitador padrão para a parte da ID do cliente da solicitação
   1. crm_id - esse é o código de integração personalizado, que você especificou na lição Serviço de identidade
   1. id - o valor da ID do cliente proveniente do seu elemento de dados `Email (Hashed)`
   1. as - o estado de autenticação, com &quot;1&quot; significando que está conectado

   ![Validação da ID do cliente do Analytics](images/integrations-analyticsCustomerIDValidation.png)

[Próximo: &quot;Publish sua propriedade&quot; >](publish.md)
