---
title: Serviços inteligentes - API do cliente - Criar uma nova instância (Configurar)
description: Customer AI - Criar uma nova instância (Configurar)
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: d9377c97-efed-427a-a063-aa9c6bd1a78a
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 3%

---

# 5.2 Customer AI - Criar uma nova instância (Configurar)

O Customer AI funciona analisando os dados existentes do Evento de experiência do consumidor para prever pontuações de abandono ou propensão de conversão. A criação de uma nova instância do Customer AI permite que os profissionais de marketing definam metas e medidas.

## 5.2.1 Configurar uma nova instância do Customer AI

No Adobe Experience Platform, clique em **Serviços** no menu esquerdo. O **Serviços** é exibido e exibe todos os serviços disponíveis à sua disposição. No cartão do Customer AI, clique em **Abrir**.

![Navegação de serviços](./images/navigatetoservice.png)

Clique em **Criar instância**.

![Criar nova instância](./images/createnewinstance.png)

Você verá isso.

![Criar nova instância](./images/custai1.png)

Insira os detalhes necessários para a instância do Customer AI:

- Nome: use `--demoProfileLdap-- Product Purchase Propensity`
- Descrição: usar: **Prever a probabilidade de os clientes comprarem um produto**
- Tipo de propensão: select **Conversão**

![Página de configuração 1](./images/setuppage1.png)

Clique em **Próximo**.

![Página de configuração 1](./images/next.png)

Você verá isso. Selecione o conjunto de dados criado no exercício anterior que é nomeado como `--demoProfileLdap - Demo System - Customer Experience Event Dataset`. Clique em **Próximo**.

![Página de configuração 1](./images/custai2.png)

Selecionar **Ocorrerá** e defina o campo **commerce.purch.value** como a variável de destino.

![Definição da meta da CAI](./images/caidefinegoal.png)

Clique em **Próximo**.

![Página de configuração 1](./images/next.png)

Em seguida, defina o cronograma para execução **Semanalmente** e defina a hora o mais próxima possível da hora atual. Certifique-se de que o botão **Ativar pontuações para Perfil** estiver ativado.

![Definir avanço da CAI](./images/caiadvancepage.png)

Clique em **Concluir**.

![Página de configuração 1](./images/finish.png)

Você verá esse pop-up. Clique em **OK**.

![Página de configuração 1](./images/finish1.png)

Depois de configurar a instância, você pode vê-la na lista de instâncias do Customer AI e também visualizar o resumo da configuração e dos detalhes de execução clicando na linha de instância do Customer AI. O painel de resumo também exibirá os detalhes do erro caso sejam encontrados erros.

![Resumo da configuração da instância](./images/caiinstancesummary.png)

>[!NOTE]
>
>Você pode modificar qualquer definição ou atributo, desde que o status da instância do Customer AI seja **Aguardando treinamento** ou **Erro**

Próxima etapa: [5.3 Customer AI - Painel de pontuação e segmentação (Predict &amp; Take Action)](./ex3.md)

[Voltar ao Módulo 5](./intelligent-services.md)

[Voltar para todos os módulos](./../../overview.md)
