---
title: Veja seu Perfil de cliente em tempo real em ação na central de atendimento
description: Veja seu Perfil de cliente em tempo real em ação na central de atendimento
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 2%

---

# 2.1.6 Veja seu Perfil de cliente em tempo real em ação na central de atendimento

Neste exercício, o objetivo é fazer você percorrer a jornada do cliente e agir como um cliente real.

Neste site, implementamos o Adobe Experience Platform. Cada ação é considerada um evento de experiência e é enviada para a Adobe Experience Platform em tempo real, hidratando o Perfil do cliente em tempo real.

Em um exercício anterior, você começou como um cliente anônimo que estava navegando no site e, após algumas etapas, você se tornou um cliente conhecido.

Quando o mesmo cliente eventualmente atende o telefone e liga para a central de atendimento, é fundamental que as informações de outros canais sejam disponibilizadas imediatamente, para que a experiência da central de atendimento possa ser relevante e personalizada.

## 2.1.6.1 Usar o aplicativo CX

Como parte de nosso sistema de demonstração, criamos um modelo do aplicativo CX que pode ser usado para simular um ambiente de call center. Siga estas etapas para criar esse projeto de aplicativo CX.

Ir para [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Clique em **Novo projeto**.

Você verá seu projeto do aplicativo CX. Clique no projeto para abri-lo.

![Demonstração](./images/cxapp3.png)

No projeto do aplicativo CX, acesse **Integrações**. Selecione a propriedade Adobe Experience Platform Data Collection criada no Módulo 0. Você precisa selecionar a propriedade que tem **(enablement)** em seu nome. Em seguida, clique em **Executar**.

![Demonstração](./images/cxapp4.png)

Você verá isso.

![Demonstração](./images/cxapp5.png)

No painel Visualizador de perfis, você pode ver estas combinações de IDs e Namespaces:

![Perfil do cliente](./images/identities.png)

| Identidade | Namespace |
|:-------------:| :---------------:|
| ID Experience Cloud (ECID) | 12507560687324495704459439363261812234 |
| ID de e-mail | woutervangeluwe+06022022-01@gmail.com |
| ID do número de celular | +32473622044+06022022-01 |

Quando o cliente liga para a central de atendimento, o número de telefone pode ser usado para identificar o cliente. Portanto, neste exercício, você usará o número de telefone para recuperar o perfil do cliente no aplicativo CX.

Selecione **Número de telefone** na lista suspensa e insira o número de telefone usado no site. Toque **Enter**.

![Demonstração](./images/19.png)

Agora você verá as informações que seriam exibidas na central de atendimento, para que os funcionários da central de atendimento tenham todas as informações relevantes disponíveis imediatamente ao conversar com um cliente.

![Demonstração](./images/20.png)

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao módulo 2.1](./real-time-customer-profile.md)

[Voltar a todos os módulos](../../../overview.md)
