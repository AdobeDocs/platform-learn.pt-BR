---
title: Veja seu Perfil do cliente em tempo real em ação no Call Center
description: Veja seu Perfil do cliente em tempo real em ação no Call Center
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 457347ca-1ce5-4699-bd30-735abdc7b450
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 3%

---

# 3.6 Veja o Perfil do cliente em tempo real em ação no Call Center

Neste exercício, o objetivo é fazer você percorrer a jornada do cliente e agir como um cliente real.

Neste site, implementamos o Adobe Experience Platform. Cada ação é considerada um evento de experiência e enviada para a Adobe Experience Platform em tempo real, hidratando o Perfil do cliente em tempo real.

Em um exercício anterior, você começou como um cliente anônimo que estava navegando no site e, após algumas etapas, você se tornou um cliente conhecido.

Quando o mesmo cliente eventualmente pegar o telefone e ligar para a central de atendimento, é fundamental que as informações de outros canais estejam disponíveis imediatamente, para que a experiência da central de atendimento possa ser relevante e personalizada.

## 3.6.1 Usar seu aplicativo CX

Como parte de nosso Demo System, criamos um modelo de aplicativo CX que pode ser usado para simular um ambiente da central de atendimento. Siga estas etapas para criar um projeto de aplicativo CX.

Ir para [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Clique em **Novo projeto**.

Em seguida, você verá seu projeto do aplicativo CX. Clique no projeto para abri-lo.

![Demonstração](./images/cxapp3.png)

No projeto do aplicativo CX, acesse **Integrações**. Selecione a propriedade Coleta de dados do Adobe Experience Platform que foi criada no Módulo 0. É necessário selecionar a propriedade que tem **(ativação)** em seu nome. Em seguida, clique em **Executar**.

![Demonstração](./images/cxapp4.png)

Você verá isso.

![Demonstração](./images/cxapp5.png)

No painel Visualizador de perfil, você pode ver essas combinações de IDs e namespaces:

![Perfil do cliente](./images/identities.png)

| Identidade | Namespace |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 1250756068732495704459439363261812234 |
| ID de email | woutervangeluwe+06022022-01@gmail.com |
| ID do número do dispositivo móvel | +32473622044+06022022-01 |

Quando o cliente liga para sua central de atendimento, o número de telefone pode ser usado para identificar o cliente. Assim, neste exercício, você usará o número de telefone para recuperar o perfil do cliente no aplicativo CX.

Selecionar **Número de telefone** na lista suspensa e digite o número de telefone usado no site. Ocorrência **Enter**.

![Demonstração](./images/19.png)

Agora você verá as informações que seriam exibidas idealmente no Call Center, para que os funcionários do Call Center tenham todas as informações relevantes disponíveis imediatamente ao falar com um cliente.

![Demonstração](./images/20.png)

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao Módulo 3](./real-time-customer-profile.md)

[Voltar para todos os módulos](../../overview.md)
