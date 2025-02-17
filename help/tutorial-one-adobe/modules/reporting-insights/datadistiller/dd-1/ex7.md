---
title: Serviço de consulta - Explorar o conjunto de dados com o Tableau
description: Serviço de consulta - Explorar o conjunto de dados com o Tableau
kt: 5342
doc-type: tutorial
exl-id: 33ab854d-fad7-497c-affa-f58e4299c0b3
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 2.1.7 Serviço de consulta e Tableau

Abra o Tableau.

![start-tableau.png](./images/starttableau.png)

Em **Conectar a um Servidor**, clique em **Mais** e em **PostgreSQL**.

![tableau-connect-postgress.png](./images/tableauconnectpostgress.png)

Se você ainda não tiver usado o PostgeSQL com o Tableau, poderá ver isso. Clique em **Baixar driver**.

![tableau-connect-postgress.png](./images/tableauconnectpostgress1.png)

Siga as instruções para baixar e instalar o driver PostgreSQL.

![tableau-connect-postgress.png](./images/tableauconnectpostgress2.png)

Quando terminar de instalar o driver, encerre e reinicie o Tableau Desktop. Depois da reinicialização, vá para **Conectar a um Servidor** novamente, clique em **Mais** e em **PostgreSQL** novamente.

![tableau-connect-postgress.png](./images/tableauconnectpostgress.png)

Você verá isso.

![tableau-connect-postgress.png](./images/tableauconnectpostgress3.png)

Vá para o Adobe Experience Platform, para **Consultas** e para **Credenciais**.

![query-service-credentials.png](./images/queryservicecredentials.png)

Na página **Credenciais** do Adobe Experience Platform, copie o **Host** e cole-o no campo **Servidor**, copie o **Banco de Dados** e cole-o no campo **Banco de Dados** do Tableau, copie a **Porta** e cole no campo **Porta** no Tableau. Faça o mesmo para **Nome de Usuário** e **Senha**. Em seguida, clique em **Entrar**.

![tableau-connection-dialog.png](./images/tableauconnectiondialog.png)

Na lista de tabelas disponíveis, localize a tabela que você criou no exercício anterior, que se chama `--aepUserLdap--_callcenter_interaction_analysis`. Arraste-o para a tela.

![tableau-drag-table.png](./images/tableaudragtable.png)

Você verá isso. Clique em **Atualizar Agora**.

![tableau-drag-table.png](./images/tableaudragtable1.png)

Você verá os dados da AEP se tornando disponíveis no Tableau. Clique em **Planilha 1** para começar a trabalhar com os dados.

![tableau-drag-table.png](./images/tableaudragtable2.png)

Para visualizar seus dados no mapa, você precisa converter longitude e latitude em dimensões. Em **Measures**, clique com o botão direito do mouse em **Latitude** e selecione **Converter em Dimension** no menu. Faça o mesmo para a medida **Longitude**.

![tableau-convert-dimension.png](./images/tableauconvertdimension.png)

Arraste a medida **Longitude** para as **Colunas** e a medida **Latitude** para **Linhas**. Automaticamente, o mapa de **Bélgica** aparecerá com pequenos pontos representando as cidades em todo o conjunto de dados.

![tableau-drag-lon-lat.png](./images/tableaudraglonlat.png)

Selecione **Nomes de Medidas**, clique em **Adicionar à Planilha**.

![tableau-select-measure-names.png](./images/selectmeasurenames.png)

Agora você terá um mapa, com pontos de vários tamanhos. O tamanho indica o número de interações da central de atendimento para essa cidade específica. Para variar o tamanho dos pontos, navegue até o painel direito e abra **Valores de Medida** (usando o ícone suspenso). Na lista suspensa, selecione **Editar Tamanhos**. Brinque com tamanhos diferentes.

![tableau-vary-size-dots.png](./images/tableauvarysizedots.png)

Para exibir ainda mais os dados por **Tópico de Chamada**, arraste a dimensão **Tópico de Chamada** para **Páginas**. Navegue pelos **Tópicos de chamada** diferentes usando o **Tópico de chamada** no lado direito da tela:

![tableau-call-topic-navigation.png](./images/tableaucalltopicnavigation.png)

Você terminou este exercício agora.

## Próximas etapas

Ir para [2.1.8 API do Serviço de Consulta](./ex8.md){target="_blank"}

Voltar para o [Serviço de consulta](./query-service.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
