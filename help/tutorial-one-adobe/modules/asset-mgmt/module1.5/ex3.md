---
title: Conectar o ACCS ao AEM Assets CS
description: Conectar o ACCS ao AEM Assets CS
kt: 5342
doc-type: tutorial
source-git-commit: 16229700449660a085549a37013e015a5e20ba9e
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# 1.5.3 Conectar o ACCS ao AEM Assets CS

>[!IMPORTANT]
>
>Para concluir este exercício, você precisa ter acesso a um AEM Sites e Assets CS com ambiente EDS em funcionamento.
>
>Se você ainda não tiver esse ambiente, vá para o exercício [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Siga as instruções aqui e você terá acesso a esse ambiente.

>[!IMPORTANT]
>
>Se você configurou anteriormente um programa do AEM CS com um ambiente do AEM Sites e do Assets CS, pode ser que sua sandbox do AEM CS tenha hibernado. Considerando que a deshibernação de uma sandbox desse tipo leva de 10 a 15 minutos, seria uma boa ideia iniciar o processo de deshibernação agora para que você não precise aguardar mais tarde.

![ACCS+AEM Assets](./images/accsaemassets1.png)


## 1.5.3.4 Atualizar config.json

Adicione o trecho de código abaixo na linha 6 `"ac-environment-id":XXX`:

```json
 "commerce-assets-enabled": "true",
```



Próxima etapa: [Resumo e benefícios](./summary.md){target="_blank"}

Voltar para o [Adobe Commerce as a Cloud Service](./accs.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
