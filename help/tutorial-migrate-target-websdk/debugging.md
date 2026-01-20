---
title: Depuração - Migrar o Target da at.js 2.x para o Web SDK
description: Saiba como depurar uma implementação do Adobe Target usando o Adobe Experience Platform Web SDK. Os tópicos incluem opções de depuração, extensões do navegador e diferenças entre a at.js e o Platform Web SDK.
exl-id: 20699551-a708-469a-8980-67586db82787
source-git-commit: d70d5df8b11c8500dbe4764b08e2627893f436f0
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 2%

---

# Depuração do Target com a plataforma Web SDK

Verificação das atividades do Target e depuração do Web SDK para solucionar problemas de implementação, entrega de conteúdo ou qualificação de público-alvo. Esta página do guia de migração explica as diferenças entre a depuração com a at.js e o Platform Web SDK.

A tabela abaixo resume os recursos e o suporte para abordagens de teste e depuração.

| Recurso ou ferramenta | Suporte à at.js | Suporte ao Platform Web SDK |
| --- | --- | --- |
| URLs de controle de qualidade de atividade | Sim | Sim |
| Parâmetro de URL `mboxDisable` | Sim | Consulte as informações abaixo para [desabilitar a funcionalidade do Target](#disable-target-functionality) |
| Parâmetro de URL `mboxDebug` | Sim | Usar o parâmetro `alloy_debug` para informações de depuração semelhantes |
| Parâmetro de URL `mboxTrace` | Sim | Usar a extensão do navegador do Experience Platform Debugger |
| Extensão do Adobe Experience Platform Debugger | Sim | Sim |
| Parâmetro de URL `alloy_debug` | Não aplicável | Sim |
| Adobe Experience Platform Assurance | Não aplicável | Sim |

## Extensão do navegador Adobe Experience Platform Debugger

A extensão do Adobe Experience Platform Debugger para Chrome e Firefox avalia as páginas da Web e ajuda a validar as implementações do Adobe Experience Cloud.

Você pode executar o Platform Debugger em qualquer página da Web e a extensão tem acesso a dados públicos. Para acessar dados não públicos usando a extensão, como informações de rastreamento do Target, é necessário autenticar no Experience Cloud por meio do link **[!UICONTROL Entrar]**.

### Obter e instalar o Adobe Experience Platform Debugger

O Adobe Experience Platform Debugger pode ser instalado no Google Chrome. Siga o link apropriado abaixo para instalar a extensão:

- [Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Depois de instalar a extensão do Chrome ou o complemento do Firefox, um ícone (![](assets/start-icon.jpg)) é adicionado à barra de extensão. Selecione esse ícone para abrir a extensão.

Consulte o guia dedicado para obter mais informações sobre a [extensão do Adobe Experience Platform Debugger](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html?lang=pt-BR) e como depurar todos os aplicativos Web do Adobe.

## Visualizar atividades do Target com URLs de controle de qualidade

A at.js e o Platform Web SDK permitem que você visualize atividades do Target usando URLs de controle de qualidade do Target, e ambos os métodos de implementação são compatíveis com os mesmos recursos de controle de qualidade.

As URLs de controle de qualidade do Target funcionam instruindo a at.js ou o Platform Web SDK a gravar um cookie específico no seu navegador chamado `at_qa_mode`. Este cookie é usado para forçar a qualificação de uma atividade e experiência específicas.

>[!CAUTION]
>
>A funcionalidade do modo de QA do Target é compatível com a versão 2.13.0 ou superior do Platform Web SDK. O modo de controle de qualidade do Target está habilitado com base no valor `xdm.web.webPageDetails.URL` passado na chamada `sendEvent`. Quaisquer modificações nesse valor, como colocar todos os caracteres em minúsculas, podem impedir que o modo de controle de qualidade do Target funcione corretamente.

Consulte o guia dedicado para obter mais informações sobre [Controle de qualidade da atividade do Target](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html?lang=pt-BR).

## Depurar implementação do Target

A tabela abaixo descreve as diferenças entre a at.js e as táticas de depuração do Platform Web SDK:

| Recurso da at.js | Equivalente ao Platform Web SDK |
| --- | --- |
| **Desabilitação de mbox** - desabilita a busca e a renderização do Target para verificar se a página está quebrada sem as interações do Target<br><br>Carregar página com parâmetro de URL: `mboxDisable=true` | Sem equivalente direto. Você pode bloquear todas as solicitações do Platform Web SDK com as ferramentas do desenvolvedor do seu navegador. |
| **Depuração da mbox** - registra cada ação da at.js no console do navegador para ajudar a solucionar problemas de renderização<br><br>Carregar página com parâmetro de URL: `mboxDebug=true` | **Depuração da liga** - registra ações detalhadas da SDK, incluindo, mas não limitado a, ações de personalização do Target.<br><br>Carregar página com parâmetro de URL: `alloy_debug=true` <br /><br />Ou executar `alloy("setDebug", { "enabled": true });` no console do desenvolvedor |
| **Rastreamento de Destino** - com um token de rastreamento de mbox gerado na interface do usuário de Destino, um objeto de rastreamento com detalhes que participaram do processo de decisão está disponível no objeto `window.___target_trace`.<br><br>Carregar página com parâmetro de URL: `mboxTrace=window&authorization={TOKEN}` | Use a extensão do Adobe Experience Platform Debugger ou o Platform Assurance. |

>[!NOTE]
>
>Todos os recursos de depuração da at.js listados acima estão disponíveis com recursos aprimorados no Adobe Experience Platform Debugger.

### Desativar funcionalidade do Target

No momento, o Platform Web SDK não tem um recurso para suprimir seletivamente as respostas do Target. No entanto, é possível suprimir as solicitações do Platform Web SDK com as ferramentas do desenvolvedor do navegador, várias extensões do navegador ou aplicativos de terceiros. Por exemplo, para bloquear o Platform Web SDK com o Google Chrome:

1. Clique com o botão direito do mouse em qualquer lugar da página e selecione **Inspecionar**
1. Selecione a guia **Rede**
1. Filtrar pela cadeia de caracteres `//ee//` para exibir somente chamadas do Platform Web SDK
1. Recarregar a página
1. Clique com o botão direito em uma das solicitações de rede filtradas e selecione **Bloquear domínio de solicitação**
1. Recarregue a página e observe que a solicitação de rede está bloqueada
1. Quando você terminar a depuração, clique com o botão direito do mouse na solicitação de rede bloqueada e selecione **Desbloquear** ou feche o painel Ferramentas do desenvolvedor

### Exibir log de depuração

O log de depuração da at.js usando o parâmetro de URL `mboxDebug=true` mostra informações detalhadas sobre cada solicitação, resposta e tentativa do Target de renderizar o conteúdo para a página. O Platform Web SDK tem log de depuração semelhante usando o parâmetro de URL `alloy_debug=true`.

| Informações registradas | at.js (`mboxDebug=true`) | Platform Web SDK (`alloy_debug=true`) |
| --- | --- | --- |
| Prefixo de registro para filtragem | `AT:` | `[alloy]` |
| Detalhes da solicitação de carregamento de página | Sim | Sim |
| Detalhes da solicitação de mbox ou escopo | Sim | Sim |
| Status da solicitação | Sim | Sim |
| Detalhes da resposta | Sim | Sim |
| Status da renderização | Sucesso e erros | Somente erros |
| Detalhes da renderização | Sim | Sim |

>[!NOTE]
>
>Os logs de depuração da at.js e do Platform Web SDK fornecem nível de detalhes semelhante, com a exceção notável de que o Web SDK somente notifica sobre erros de renderização devido a seletores inválidos. O log de depuração não confirma se a renderização foi bem-sucedida.

### Exibir rastreamentos do Target

Os rastreamentos do Target fornecem informações detalhadas sobre as qualificações da atividade e o perfil do Target do visitante. Como os rastreamentos do Target contêm informações que não estão disponíveis publicamente, visualizá-las requer um token de autorização ou autenticação na janela de extensão do navegador Adobe Experience Platform Debugger.

| Método de rastreamento de destino | at.js | SDK da Web da Platform |
| --- | --- | --- |
| Parâmetro de URL `mboxTrace` | Sim | Não |
| Extensão do navegador Adobe Experience Platform Debugger | Sim | Sim |
| Adobe Experience Platform Assurance | Não | Sim |


Para exibir rastreamentos do Platform Web SDK Target com a Adobe Experience Platform Debugger, faça o seguinte:

1. Navegue até uma página em seu site que tenha o Target implementado com o Platform Web SDK
1. Abra a extensão Adobe Experience Platform Debugger selecionando o ícone (![](assets/start-icon.jpg)) na barra de navegação do navegador
1. Selecione o link **[!UICONTROL Entrar]**
1. Autentique usando seu logon no Adobe Experience Cloud
1. Selecione a guia **[!UICONTROL Logs]** à esquerda
1. Selecione a guia **[!UICONTROL Edge]** na parte superior
1. Opcionalmente, dê um nome à sua sessão de depuração e clique no botão **[!UICONTROL Conectar]**
1. Recarregue a página e o log deve ser preenchido com informações detalhadas sobre as interações da rede de borda
1. Concentre-se nas entradas de log que começam com &quot;Rastreamentos de Destino&quot; na descrição e selecione **[!UICONTROL Exibir]** para ver os detalhes do rastreamento de Destino

![Como exibir rastreamentos do Target com o Adobe Experience Platform Debugger](assets/target-trace-debugger.png){zoomable="yes"}

Depois de selecionar **[!UICONTROL Exibir]**, uma sobreposição será exibida, permitindo que você veja as seguintes informações relacionadas à solicitação:

- Atividades correspondentes
- Atividades sem correspondência
- Detalhes da solicitação
- Instantâneo do perfil

Consulte o manual dedicado sobre [depuração da entrega de conteúdo do Target](https://experienceleague.adobe.com/docs/target/using/activities/troubleshoot-activities/content-trouble.html?lang=pt-BR) para obter mais informações sobre rastreamentos do Target.

### Solução de problemas com o Assurance

As informações de rastreamento do Target podem ser visualizadas na extensão do navegador Adobe Experience Platform Debugger e no aplicativo do Assurance (anteriormente conhecido como Projeto Griffon). Para exibir rastreamentos do Target no Assurance, faça o seguinte:

1. Abra a extensão do navegador Adobe Experience Platform Debugger e conecte uma sessão de depuração remota conforme descrito acima
1. Selecione o link com seu nome de sessão acima do log de depuração
1. O Platform Assurance carrega e mostra logs detalhados para todos os aplicativos da Adobe configurados no fluxo de dados para a sua implementação
1. Filtrar o log por `adobe.target`
1. Selecione uma entrada de log com o tipo `com.adobe.target.trace`
1. Expanda os detalhes da carga e exiba as informações em `context > targetTrace`

![Como exibir rastreamentos do Target com o Assurance](assets/target-trace-assurance.png){zoomable="yes"}

## Examinar solicitação e resposta de rede

A carga da solicitação e a resposta das chamadas `sendEvent` do Platform Web SDK são diferentes da at.js. A estrutura abaixo deve ajudá-lo a entender a estrutura da solicitação e resposta enquanto examina as chamadas de rede com as ferramentas de desenvolvedor do seu navegador.

### Conteúdo da solicitação de conteúdo

![Elementos específicos do Target da carga do Platform Web SDK](assets/target-payload.png){zoomable="yes"}

- Perfil, entidade e outros parâmetros que não são da mbox são passados na matriz de eventos em `data.__adobe.target`
- Os escopos de decisão estão localizados na matriz de eventos em `query.personalization.decisionScopes`
- Os dados XDM mapeados para os parâmetros de mbox downstream estão localizados na matriz de eventos em `xdm`

### Corpo da resposta do conteúdo

![Elementos específicos do público alvo do corpo de resposta do Platform Web SDK](assets/target-response.png){zoomable="yes"}

- O Platform Web SDK retorna ações para todos os aplicativos Adobe no objeto `handle`
- A ação `personalization:decisions` significa uma resposta do Target ou da decisão de oferta
- As apresentações de destino são apresentadas como uma matriz, cada uma com uma ID de apresentação exclusiva com o prefixo `AT:`
- O escopo de decisão e os detalhes da atividade estão localizados no array de apresentações
- Os detalhes da oferta estão localizados na matriz `items` em `data`
- Os tokens de resposta estão localizados na matriz `items` em `meta`

### Carga do evento de apresentação

![Exemplo de evento de apresentação do público alvo](assets/target-proposition-event.png){zoomable="yes"}

- Os eventos SDK específicos do Target são `decisioning.propositionDisplay` para uma impressão ou `decisioning.propositionInteract` para uma interação, como um clique
- Os detalhes do evento de apresentação estão localizados na matriz de eventos em `xdm._experience.decisioning`
- A ID de apresentação do evento de exibição ou interação deve corresponder à ID de apresentação do conteúdo retornado do Target


Parabéns, você chegou ao fim do tutorial! Boa sorte ao migrar sua implementação do Adobe Target para o Web SDK!

>[!NOTE]
>
>Estamos empenhados em ajudá-lo a ter sucesso com a migração do Target da at.js para o Web SDK. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=pt#M463).
