---
title: Serviços inteligentes - Customer AI Criar uma nova instância (Configurar)
description: IA do cliente - Criar uma nova instância (Configurar)
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 3%

---

# 2.2.2 IA do cliente - Criar uma nova instância (Configurar)

A IA do cliente funciona analisando os dados existentes do Evento de experiência do consumidor para prever pontuações de churn ou propensão de conversão. A criação de uma nova instância da IA do cliente permite que os profissionais de marketing definam metas e medidas.

## 2.2.2.1 Configurar uma nova instância da IA do cliente

No Adobe Experience Platform, clique em **Serviços** no menu esquerdo. O navegador **Serviços** é exibido e exibe todos os serviços disponíveis à sua disposição. No cartão da IA do cliente, clique em **Abrir**.

![Navegação de serviço](./images/navigatetoservice.png)

Clique em **Criar instância**.

![Criar nova instância](./images/createnewinstance.png)

Você verá isso.

![Criar nova instância](./images/custai1.png)

Insira os detalhes necessários para a instância da IA do cliente:

- Nome: use `--aepUserLdap-- Product Purchase Propensity`
- Descrição: use: **Preveja a probabilidade de os clientes comprarem um produto**
- Tipo de propensão: selecione **Conversão**

![Página da Instalação 1](./images/setuppage1.png)

Clique em **Next**.

![Página da Instalação 1](./images/next.png)

Você verá isso. Selecione o conjunto de dados criado no exercício anterior chamado `--demoProfileLdap - Demo System - Customer Experience Event Dataset`. Clique em **Next**.

![Página da Instalação 1](./images/custai2.png)

Selecione **Ocorrerá** e defina o campo **commerce.purchases.value** como a variável de destino.

![Definindo a Meta de CAI](./images/caidefinegoal.png)

Clique em **Next**.

![Página da Instalação 1](./images/next.png)

Em seguida, defina seu cronograma para ser executado **Semanalmente** e defina o horário o mais próximo possível de sua hora atual. Verifique se a opção **Habilitar pontuações para o Perfil** está habilitada.

![Definir adiantamento de CAI](./images/caiadvancepage.png)

Clique em **Concluir**.

![Página da Instalação 1](./images/finish.png)

Você então verá esse pop-up. Clique em **OK**.

![Página da Instalação 1](./images/finish1.png)

Após configurar a instância, você pode vê-la na lista de instâncias da IA do cliente e também visualizar o resumo dos detalhes de configuração e execução clicando na linha de instâncias da IA do cliente. O painel de resumo também exibirá detalhes do erro caso sejam encontrados erros.

![Resumo da instalação da instância](./images/caiinstancesummary.png)

>[!NOTE]
>
>Você pode modificar qualquer definição ou atributo, desde que o status da instância da IA do cliente seja **Aguardando treinamento** ou **Erro**

Próxima etapa: [2.2.3 IA do cliente - Painel de pontuação e segmentação (Prever e executar ação)](./ex3.md)

[Voltar ao módulo 2.2](./intelligent-services.md)

[Voltar a todos os módulos](./../../../overview.md)
