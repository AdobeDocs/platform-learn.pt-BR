---
title: Serviço de consulta - Pré-requisitos
description: Serviço de consulta - Pré-requisitos
kt: 5342
doc-type: tutorial
exl-id: b8a404d1-7796-46e3-b245-553acdc753ae
source-git-commit: d9d9a38c1e160950ae755e352a54667c8a7b30f7
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 5.1.1 Pré-requisitos

## Instalar o Utilitário de Linha de Comando PSQL

Siga as instruções descritas na documentação do Adobe Experience Platform para instalar o cliente psql:
[Guia de Instalação do PSQL](https://experienceleague.adobe.com/docs/experience-platform/query/clients/psql.html?lang=pt-BR)

Depois de instalar o PSQL, talvez seja necessário atualizar o **PATH** executando o comando abaixo em uma janela de terminal:

Para o macOS (substitua XX no comando abaixo pelo número da versão do PSQL que você instalou):

`export PATH=/Library/PostgreSQL/XX/bin:$PATH`

## Instalar o Power BI

Somente para usuários do Windows

[Instalar o Microsoft Power BI](https://experienceleague.adobe.com/docs/experience-platform/query/clients/power-bi.html?lang=pt-BR)

Instale a versão exata do **npgsql**, conforme mencionado no documento; caso contrário, você não poderá conectar o Power BI ao Serviço de Consulta da Adobe Experience Platform.

## Instalar o Tableau

Para usuários do Windows ou do Mac

[Instalar Tableau Desktop](https://experienceleague.adobe.com/docs/experience-platform/query/clients/tableau.html?lang=pt-BR) de acordo com a documentação.

O Tableau oferece automaticamente um período de avaliação de 14 dias.

Se você quiser usar o Tableau além desses 14 dias, precisará de uma chave de licença.

Próxima Etapa: [5.1.2 Introdução](./ex2.md)

[Voltar ao módulo 5.1](./query-service.md)

[Voltar a todos os módulos](../../../overview.md)
