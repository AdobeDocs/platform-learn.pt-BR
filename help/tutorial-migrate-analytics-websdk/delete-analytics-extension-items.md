---
title: Excluir os itens de extensão do Adobe Analytics
description: Quando a depuração e a validação estiverem concluídas, remova todas as referências aos itens de extensão do Adobe Analytics e remova a própria extensão.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16766
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---


# Excluir os itens de extensão do Adobe Analytics

Quando a depuração e a validação estiverem concluídas, remova todas as referências aos itens de extensão do Adobe Analytics e remova a própria extensão.

## Visão geral

Quando estiver satisfeito com o fato de que tudo na propriedade foi migrado para o Web SDK e tiver concluído a depuração e a validação (no ambiente de desenvolvimento), você estará pronto para remover as referências à extensão do Adobe Analytics. A velocidade com que você remove esses itens e quantas vezes você testa enquanto faz isso depende de você. Se quiser ter mais cuidado, remova as referências lentamente e teste entre cada remoção. Se você tiver certeza de que tudo está funcionando corretamente e foi migrado corretamente, poderá &quot;remover o band-aid&quot; e remover todos os itens. Ainda recomendamos testes no final do exercício, é claro.

## Remover ações antigas das regras

Novamente, vamos supor que você já testou tudo e que está funcionando corretamente. Nesse ponto, você pode inserir suas regras uma por uma e remover as ações que pertencem à extensão do Adobe Analytics.

1. Abra uma de suas regras, por exemplo, sua regra de carregamento de página padrão.
1. Depois de passar pela migração para essa regra, você provavelmente tem quatro (ou mais) ações.

   ![Todas as 4 ações](assets/all-four-actions.jpg)

1. Você pode ver que os dois primeiros têm o identificador &quot;Adobe Analytics&quot;. Essas são as ações que desejaremos excluir.
1. Passe o mouse sobre o primeiro, como a ação &quot;Adobe Analytics - Definir variáveis&quot;, e um X aparecerá permitindo a exclusão. Clique no X e veja a ação desaparecer. Remova qualquer uma e todas as ações do Adobe Analytics na regra, nesse caso a ação Definir variável e a ação Enviar beacon.
1. Isso deixará somente as ações do Web SDK

   ![Somente ações do Web SDK](assets/websdk-actions-only.jpg)

1. Salvar na biblioteca
1. Crie a biblioteca e teste seu site para verificar se não há novos erros e se tudo está funcionando corretamente
1. Repita essa ação para outras regras, criando na biblioteca de desenvolvimento e testando entre cada remoção (ou sempre que estiver confortável). Você pode apenas testar o no depurador ou também verificar os relatórios no conjunto de relatórios de migração, novamente, dependendo do seu nível de conforto.

## Remover extensões

Agora que você removeu as referências à sua extensão do Adobe Analytics, é possível remover (ou desativar) a extensão, bem como quaisquer outras extensões que a usem ou que sejam dependentes dela. Pessoalmente, gosto de uma abordagem cuidadosa, então &quot;desativar&quot; é minha escolha em vez de desinstalar, pelo menos inicialmente.

1. Selecione **Extensões** no painel esquerdo da interface do usuário.
1. Verifique se a guia **Instalado** está selecionada.
1. Selecione a extensão do Adobe Analytics.
1. No painel direito, escolha desativar a extensão (ou clique nos três pontos e desinstale se preferir).

   ![Desabilitar extensão do Analytics](assets/disable-analytics-extension.jpg)

1. Faça o mesmo para a extensão do Serviço de ID de Experience Cloud, pois você não precisará mais disso. A extensão do Web SDK manipula a ID do e, portanto, você não precisa da extensão adicional.
1. Faça o mesmo para qualquer outra extensão associada à extensão do Adobe Analytics, mas somente após fazer as alterações de migração necessárias.
1. Crie as alterações no ambiente de desenvolvimento.

