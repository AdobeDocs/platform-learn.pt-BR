---
title: Adobe Journey Optimizer - Aplicar personalização em uma mensagem de email
description: Este exercício explica como usar a personalização de segmentos em um conteúdo de email
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 573ecfba-4f1d-4242-8358-1d33109aaea3
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 10%

---

# 10.3 Aplicar personalização em uma mensagem de email

Faça logon no Adobe Experience Cloud acessando [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Adobe Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Você será redirecionado para o **Início** no Journey Optimizer. Antes de continuar, é necessário selecionar um **sandbox**. A sandbox a ser selecionada é chamada de ``--aepTenantId--``. Você pode fazer isso clicando no texto **[!UICONTROL Produto de produção]** na linha azul na parte superior da tela.

![ACOP](../module7/images/acoptriglp.png)

## 10.3.1 Personalização baseada em segmentos

Neste exercício, você melhorará sua mensagem de email do informativo com um texto personalizado com base na associação do segmento.

Ir para **Jornada**. Encontre a jornada do boletim informativo que você criou no exercício anterior. Procurar por `--demoProfileLdap-- - Newsletter`. Clique na jornada para abri-la.

![Journey Optimizer](./images/sbp1.png)

Você verá isso. Clique em **Duplicate**.

![Journey Optimizer](./images/sbp2.png)

Clique em ** Duplicar**.

![Journey Optimizer](./images/sbp3.png)

Selecione seu **Email** e clique em **Editar conteúdo**.

![Journey Optimizer](./images/sbp3a.png)

Clique em **Email Designer**.

![Journey Optimizer](./images/sbp4.png)

Você verá isso.

![Journey Optimizer](./images/sbp5.png)

Abrir **Componentes de conteúdo** e arraste uma **Texto** abaixo do conteúdo do informativo atual.

![Journey Optimizer](./images/sbp6.png)

Selecione o texto padrão inteiro e exclua-o. Em seguida, clique no botão **Adicionar personalização** na barra de ferramentas.

![Journey Optimizer](./images/sbp7.png)

Você verá isso:

![Journey Optimizer](./images/seg1.png)

No menu esquerdo, clique em **Associações do segmento**.

![Journey Optimizer](./images/seg2.png)

>[!NOTE]
>
>Se você não conseguir encontrar seu segmento nesta lista, role para baixo um pouco para encontrar instruções sobre como recuperar a ID do segmento manualmente.

Selecionar o segmento `Luma - Women's Category Interest` e clique no botão **+** ícone , que deve ter esta aparência:

![Journey Optimizer](./images/seg3.png)

Em seguida, deixe a primeira linha como está e substitua as linhas 2 e 3 por este código:

``
Psssst... a private sale in the women category will launch soon, we will keep you posted
{%else%}
Thanks for taking the time to read our newsletter. Here is a 10% promo code to use on the website: READER10
{%/if%}
``

Você terá isso:

![Journey Optimizer](./images/seg4.png)

Clique em **Validar** para verificar se o código está correto. Clique em **Salvar**.

![Journey Optimizer](./images/sbp8.png)

Agora você pode salvar esta mensagem clicando no botão **Salvar** no canto superior direito. Em seguida, clique em **Simular conteúdo**.

![Journey Optimizer](./images/sbp9.png)

Selecione um dos perfis que você criou como parte deste tutorial e clique em **Visualizar**. Em seguida, você verá o resultado da sua configuração.

![Journey Optimizer](./images/sbp10.png)

Você verá isso. Em seguida, clique em **Fechar**.

![Journey Optimizer](./images/sbp10fff.png)

Volte para o painel de mensagens clicando no botão **seta** ao lado do texto da linha de assunto no canto superior esquerdo.

![Journey Optimizer](./images/sbp11.png)

Clique na seta no canto superior esquerdo para retornar à jornada.

![Journey Optimizer](./images/oc79afff.png)

Clique em **Ok** para fechar a ação de email.

![Journey Optimizer](./images/oc79bfff.png)

Altere seu **Agendar** para **Uma vez** e defina uma **Data/Hora**. Clique em **Ok**.

>[!NOTE]
>
>A data e a hora de envio da mensagem devem estar dentro de mais de uma hora.

![Journey Optimizer](./images/sbp18.png)

Clique no botão **Publicar** na jornada.

![Journey Optimizer](./images/sbp19.png)

Na janela pop-up , clique em **Publicar** novamente.

![Journey Optimizer](./images/sbp20.png)

Sua jornada básica do boletim informativo foi publicada. Sua mensagem de email do informativo será enviada com base em sua programação e sua jornada parará assim que o último email for enviado.

![Journey Optimizer](./images/sbp20fff.png)

Terminou este exercício.

Próxima etapa: [10.4 Configurar e usar notificações por push para iOS](./ex4.md)

[Voltar ao Módulo 10](./journeyoptimizer.md)

[Voltar para todos os módulos](../../overview.md)
