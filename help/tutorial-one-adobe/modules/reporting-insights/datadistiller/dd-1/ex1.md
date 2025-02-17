---
title: Serviço de consulta - Pré-requisitos
description: Serviço de consulta - Pré-requisitos
kt: 5342
doc-type: tutorial
exl-id: e9e4d478-cb8d-42a9-87a3-319e5a8b8522
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---

# 2.1.1 Pré-requisitos

## Instalar o Utilitário de Linha de Comando PSQL

Siga as instruções descritas na documentação do Adobe Experience Platform para instalar o cliente psql:
[Guia de Instalação do PSQL](https://experienceleague.adobe.com/docs/experience-platform/query/clients/psql.html)

Depois de instalar o PSQL, talvez seja necessário atualizar o **PATH** executando o comando abaixo em uma janela de terminal:

Para o macOS (substitua XX no comando abaixo pelo número da versão do PSQL que você instalou):

`export PATH=/Library/PostgreSQL/XX/bin:$PATH`

## Instalar o Power BI

Somente para usuários do Windows

[Instalar o Microsoft Power BI](https://experienceleague.adobe.com/docs/experience-platform/query/clients/power-bi.html)

Instale a versão exata do **npgsql**, conforme mencionado no documento; caso contrário, você não poderá conectar o Power BI ao Serviço de Consulta da Adobe Experience Platform.

## Instalar o Tableau

Para usuários do Windows ou do Mac

[Instalar Tableau Desktop](https://experienceleague.adobe.com/docs/experience-platform/query/clients/tableau.html) de acordo com a documentação.

O Tableau oferece automaticamente um período de avaliação de 14 dias.

Se você quiser usar o Tableau além desses 14 dias, precisará de uma chave de licença.

## Próximas etapas

Ir para [2.1.2 Introdução](./ex2.md){target="_blank"}

Voltar para o [Serviço de consulta](./query-service.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
