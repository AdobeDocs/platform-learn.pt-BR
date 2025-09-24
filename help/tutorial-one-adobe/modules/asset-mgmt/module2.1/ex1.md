---
title: Criar seu programa do Cloud Manager
description: Criar seu programa do Cloud Manager
kt: 5342
doc-type: tutorial
exl-id: fda247eb-1865-4936-b46e-84128ccab357
source-git-commit: 7384eabe00354374f7012be10c24870c68ea7f2c
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 3%

---

# 1.1.1 Criar seu programa do Cloud Manager

Ir para [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. A organização que você deve selecionar é `--aepImsOrgName--`. Então você verá algo assim. Clique em **Adicionar programa**.

![AEMCS](./images/aemcs1.png)

Para o **Nome do Programa**, use `--aepUserLdap-- - CitiSignal AEM+ACCS`. Selecione a opção **Configurar uma sandbox**. Clique em **Continuar**.

![AEMCS](./images/aemcs2.png)

Verifique se as seguintes opções estão selecionadas:

- Sites
- Formulários
- Ativos

Clique na seta de **Assets** para abrir a lista de opções.

![AEMCS](./images/aemcs3.png)

Verifique se as seguintes opções estão selecionadas:

- Content Hub

Role para baixo na lista.

![AEMCS](./images/aemcs3a.png)

Verifique se as seguintes opções estão selecionadas:

- Edge Delivery Services
- Mídia dinâmica

Clique em **Criar**.

![AEMCS](./images/aemcs3b.png)

A criação do ambiente levará algum tempo, de 10 a 20 minutos.

![AEMCS](./images/aemcs4.png)

Depois que os ambientes forem criados e estiverem prontos para uso, você receberá um email de confirmação, após o qual poderá voltar aqui.

![AEMCS](./images/aemcs5.png)

Depois de receber sua confirmação por email, volte para [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Você verá que o status do seu programa mudou para **Pronto**. Clique no programa para abri-lo.

![AEMCS](./images/aemcs6.png)

Consulte a guia **Pipelines**. Clique nos 3 pontos **...** e em **Executar**.

![AEMCS](./images/aemcs7.png)

Clique em **Executar**.

![AEMCS](./images/aemcs8.png)

Em seguida, clique nos 3 pontos **...** na guia **Ambientes** e clique em **Exibir Detalhes**.

![AEMCS](./images/aemcs9.png)

Você verá os detalhes do seu ambiente, incluindo a URL do seu ambiente **Author**, que você precisará no próximo exercício.

Dê uma olhada na linha **Content Hub** e selecione **Clique para ativar**.

![AEMCS](./images/aemcs10.png)

Clique em **Ativar**.

![AEMCS](./images/aemcsact1.png)

A ativação do **Content Hub** foi iniciada agora. Isso pode levar 10 minutos ou mais.

![AEMCS](./images/aemcsact2.png)

Após aproximadamente 10 minutos, a ativação do **Content Hub** será concluída.
Em seguida, observe a linha **Dynamic Media** e selecione **Clique para ativar**.

![AEMCS](./images/aemcsact3.png)

Clique em **Ativar**.

![AEMCS](./images/aemcsact4.png)

A ativação da **Mídia dinâmica** foi iniciada agora. Isso pode levar 10 minutos ou mais.

![AEMCS](./images/aemcsact5.png)

Após cerca de 10 minutos, a ativação da **Mídia dinâmica** será feita.

![AEMCS](./images/aemcsact6.png)

Depois que a execução do pipeline for concluída, você poderá continuar com o próximo exercício.

Próxima Etapa: [Configurar o ambiente do AEM CS](./ex2.md){target="_blank"}

Voltar para o [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./aemcs.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
