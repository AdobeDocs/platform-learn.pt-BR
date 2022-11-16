---
title: Serviço de query - Explore o conjunto de dados com Tableau
description: Serviço de query - Explore o conjunto de dados com Tableau
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 04209eb4-b054-4a2e-885e-61f601c3fc2c
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# 4.6 Serviço de consulta e Tableau

Abra Tableau.

![start-tableau.png](./images/start-tableau.png)

Em **Conectar-se a um servidor** select **PostgreSQL**:

![tableau-connect-postgress.png](./images/tableau-connect-postgress.png)

Vá para Adobe Experience Platform, para **Queries** e **Credenciais**.

![query-service-credentials.png](./images/query-service-credentials.png)

No **Credenciais** no Adobe Experience Platform, copie a **Host** e cole-o no **Servidor** , copie o **Banco de dados** e cole-o no **Banco de dados** no Tableau, copie a variável **Port** e cole no campo **Port** em Tableau, faça o mesmo por **Nome do usuário** e **Senha**. Em seguida, clique em **Fazer logon**.

Fazer logon:

![tableau-connection-dialog.png](./images/tableau-connection-dialog.png)

Clique em pesquisar (1) e insira o **ldap** no campo de pesquisa, identifique a tabela a partir do conjunto de resultados e arraste-a (3) para o local com o nome **Arraste tabelas aqui**. Quando terminar, clique em **Folha 1** (3)

![tabela-arrastar-tabela.png](./images/tableau-drag-table.png)

Para visualizar nossos dados no mapa, precisamos converter longitude e latitude em dimensões. Em **Medidas** select **Latitude** (1) e abra a lista suspensa do campo e selecione **Converter em Dimension** (2) Faça o mesmo para a **Longitude** medida.

![tableau-converted-dimension.png](./images/tableau-convert-dimension.png)

Arraste o **Longitude** à **Colunas** e **Latitude** para **Linhas**. Automaticamente o mapa de **Bélgica** aparecerá com pequenos pontos representando as cidades no conjunto de dados de saída.

![tableau-arrastar-lon-lat.png](./images/tableau-drag-lon-lat.png)

Selecionar **Nomes de Medida** (1), abra a lista suspensa e selecione **Adicionar à planilha** 2.

![tableau-select-measure-names.png](./images/tableau-select-measure-names.png)

Agora você terá um mapa, com pontos de vários tamanhos. O tamanho indica o número de interações da central de atendimento para essa cidade específica. Para variar o tamanho dos pontos, navegue até o painel direito e abra **Valores da Medida** (usando o ícone suspenso ). Na lista suspensa, selecione **Editar tamanhos**. Jogue com tamanhos diferentes.

![tableau-vary-size-dots.png](./images/tableau-vary-size-dots.png)

Para exibir ainda mais os dados por **Tópico da Chamada**, arraste (1) a **Tópico da Chamada** em **Páginas**. Navegar pelo diferente **Tópicos de chamada** usando o **Tópico da Chamada** (2) no lado direito do ecrã:

![tableau-call-topic-navigation.png](./images/tableau-call-topic-navigation.png)

Você já terminou este exercício.

Próxima etapa: [4.7 API do serviço de consulta](./ex7.md)

[Voltar ao Módulo 4](./query-service.md)

[Voltar para todos os módulos](../../overview.md)
