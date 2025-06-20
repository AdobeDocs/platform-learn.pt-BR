---
title: Ativação da campanha do GenStudio for Performance Marketing para o Meta
description: Ativação da campanha do GenStudio for Performance Marketing para o Meta
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 2c7ef715-b8af-4a5b-8873-5409b43d7cb0
source-git-commit: b8f7b370a5aba82a0dcd6e7f4f0222fe209976f7
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---

# 1.3.3 Ativação da campanha para o Meta

>[!IMPORTANT]
>
>Para concluir este exercício, você precisa ter acesso a um ambiente de trabalho do AEM Assets CS Author com o AEM Content Hub habilitado. Se você seguir o exercício [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}, terá acesso a esse ambiente.

>[!IMPORTANT]
>
>Se você tiver configurado anteriormente um programa do AEM Assets CS com um ambiente de Autor e AEM Assets, pode ser que sua sandbox do AEM CS tenha hibernado. Considerando que a deshibernação de uma sandbox desse tipo leva de 10 a 15 minutos, seria uma boa ideia iniciar o processo de deshibernação agora para que você não precise aguardar mais tarde.

## 1.3.3.1 Criar campanha

No **GenStudio for Performance Marketing**, vá para **Campanhas** no menu esquerdo. Clique em **+ Adicionar campanha**.

![GSPeM](./images/gscampaign1.png)

Você deve ver uma visão geral vazia da campanha.

![GSPeM](./images/gscampaign2.png)

Para o nome do campo, use `--aepUserLdap-- - CitiSignal Fiber Launch Campaign`.

Para o campo **Descrição**, use o texto abaixo.

```
The CitiSignal Fiber Launch campaign introduces CitiSignal’s flagship fiber internet service—CitiSignal Fiber Max—to key residential markets. This campaign is designed to build awareness, drive sign-ups, and establish CitiSignal as the go-to provider for ultra-fast, reliable, and future-ready internet. The campaign will highlight the product’s benefits for remote professionals, online gamers, and smart home families, using persona-driven messaging across digital and physical channels.
```

Para o campo **Objetivo**, use o texto abaixo.

```
Generate brand awareness in target regions
Drive early sign-ups and pre-orders for CitiSignal Fiber Max
Position CitiSignal as a premium, customer-first fiber internet provider
Educate consumers on the benefits of fiber over cable or DSL
```

Para o campo **Mensagens principais**, use o texto abaixo.

```
Supporting Points:
Symmetrical speeds up to 2 Gbps
Whole-home Wi-Fi 6E coverage
99.99% uptime guarantee
24/7 concierge support
No data caps or throttling
 Channels:
Digital Advertising: Google Display, YouTube pre-roll, Meta (Facebook/Instagram), TikTok (for gamers)
Email Marketing: Persona-segmented drip campaigns
Social Media: Organic and paid posts with testimonials, speed demos, and influencer partnerships
Out-of-Home (OOH): Billboards, transit ads in suburban commuter corridors
Local Events: Pop-up booths at tech expos, family festivals, and gaming tournaments
Direct Mail: Personalized flyers with QR codes for early sign-up discounts
 
Target Regions:
Primary Launch Markets:
Denver Metro Area, CO
Austin, TX
Raleigh-Durham, NC
Salt Lake City, UT
Demographic Focus:
Suburban neighborhoods with high remote work density
Areas with high smart home adoption
Zip codes with underserved or dissatisfied cable customers
```

Você deve ter isto:

![GSPeM](./images/gscampaign3.png)

Role para baixo para ver mais campos:

![GSPeM](./images/gscampaign4.png)

Para o campo **Início**, defina-o como a data de hoje.

Para o campo **End**, defina-o como uma data daqui a 1 mês.

Para o campo **Status**, defina-o como **Ativo**.

Para o campo **Canais**, defina-o como **Meta**, **Email**, **Mídia paga**, **Exibição**.

Para o campo **Regiões**, selecione uma região de escolha.

Para o campo Para o campo **Referências** > **Produtos**: escolha o produto `--aepUserLdap-- - CitiSignal Fiber Max`.

**Referências** > **Personas**: escolha as personalidades `--aepUserLdap-- - Remote Professionals`, `--aepUserLdap-- - Online Gamers`, `--aepUserLdap-- - Smart Home Families`

Você deverá ver isso:

![GSPeM](./images/gscampaign5.png)

Sua campanha está pronta. Clique na **seta** para voltar.

![GSPeM](./images/gscampaign6.png)

Você verá sua campanha na lista. Clique no ícone de exibição do calendário para alterar a exibição para o calendário da campanha.

![GSPeM](./images/gscampaign7.png)

Você deve ver um calendário de campanha que dá uma ideia mais visual de quais campanhas estão ativas em cada momento.

![GSPeM](./images/gscampaign8.png)

## 1.3.3.2 Configurar conexão com Meta

>[!IMPORTANT]
>
>Para configurar sua conexão com o Meta, você precisa ter uma conta de usuário do Meta disponível e essa conta de usuário precisa ser adicionada a uma conta do Meta Business.

Para configurar a conexão com Meta, clique nos 3 pontos **...** e selecione **Configurações**.

![GSPeM](./images/gsconnection1.png)

Clique em **Conectar** para **Meta Ads**.

![GSPeM](./images/gsconnection2.png)

Faça logon usando sua conta Meta. Clique em **Continuar**.

![GSPeM](./images/gsconnection3.png)

Se sua conta estiver vinculada a uma conta Meta Business, você poderá selecionar o portfólio de negócios que foi configurado no Meta.

![GSPeM](./images/gsconnection5.png)

Depois que a conexão for estabelecida, clique na linha que diz **X conta(s) conectada(s)**.

![GSPeM](./images/gsconnection4.png)

Você deverá ver os detalhes da Meta Business Account que está conectada ao GenStudio for Performance Marketing.

![GSPeM](./images/gsconnection6.png)

## 1.3.3.3 Criar novo ativo

Ir para [https://firefly.adobe.com/](https://firefly.adobe.com/){target="_blank"}. Digite o prompt `a neon rabbit running very fast through space` e clique em **Gerar**.

![GSPeM](./images/gsasset1.png)

Você verá várias imagens sendo geradas. Escolha a imagem de que você mais gosta, clique no ícone **Compartilhar** na imagem e selecione **Abrir no Adobe Express**.

![GSPeM](./images/gsasset2.png)

Em seguida, você verá a imagem que acabou de gerar ficar disponível no Adobe Express para edição. Agora é necessário adicionar o logotipo CitiSignal na imagem. Para fazer isso, vá para **Marcas**.

![GSPeM](./images/gsasset3.png)

Em seguida, você deverá ver o modelo de marca CitiSignal criado no GenStudio for Performance Marketing exibido no Adobe Express. Clique para selecionar o modelo de marca que deve ser nomeado como `--aepUserLdap-- - CitiSignal`.

![GSPeM](./images/gsasset4.png)

Vá para **Logotipos** e clique no logotipo **branco** do Citisignal para soltá-lo na imagem.

![GSPeM](./images/gsasset5.png)

Posicione o logotipo CitiSignal no canto superior esquerdo.

![GSPeM](./images/gsasset6.png)

Em seguida, clique em **Compartilhar**.

![GSPeM](./images/gsasset7.png)

Selecione **AEM Assets**.

![GSPeM](./images/gsasset8.png)

Clique em **Selecionar pasta**.

![GSPeM](./images/gsasset9.png)

Selecione o repositório do AEM Assets CS, que deve se chamar `--aepUserLdap-- - CitiSignal` e selecione a pasta `--aepUserLdap-- - CitiSignal Fiber Campaign`. Clique em **Selecionar**.

![GSPeM](./images/gsasset11.png)

Você deverá ver isso. Clique em **Carregar 1 ativo**. Sua imagem será carregada no AEM Assets CS.

![GSPeM](./images/gsasset12.png)

Ir para [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Abra o **Experience Manager Assets**.

![GSPeM](./images/gsasset13.png)

Selecione o ambiente do AEM Assets CS, que deve se chamar `--aepUserLdap-- - CitiSignal dev`.

![GSPeM](./images/gsasset14.png)

Vá para **Assets** e clique duas vezes na pasta `--aepUserLdap-- - CitiSignal Fiber Campaign`.

![GSPeM](./images/gsasset15.png)

Você verá algo semelhante a isso. Clique duas vezes na imagem `--aepUserLdap-- - neon rabbit`.

![GSPeM](./images/gsasset16.png)

A imagem `--aepUserLdap-- - neon rabbit` será exibida. Altere o **Status** para **Aprovado** e clique em **Salvar**

>[!IMPORTANT]
>
>Se o status de uma imagem não estiver definido como **Aprovado**, ela não estará visível no GenStudio for Performance Marketing. Somente ativos aprovados podem ser acessados na GenStudio for Performance Marketing.

![GSPeM](./images/gsasset17.png)

Volte para o GenStudio for Performance Marketing. No menu esquerdo, vá para **Assets** e selecione seu repositório do AEM Assets CS, que deve ser nomeado como `--aepUserLdap-- - CitiSignal`. Em seguida, você verá que a imagem que acabou de criar e aprovar ficará disponível dentro do GenStudio for Performance Marketing.

![GSPeM](./images/gsasset18.png)

## 1.3.3.4 Criar e aprovar meta anúncio

## 1.3.3.5 Publicar anúncio no Meta

## Próximas etapas

Ir para [Resumo e benefícios](./summary.md){target="_blank"}

Voltar para [GenStudio for Performance Marketing](./genstudio.md){target="_blank"}

Voltar para [Todos os Módulos](./../../../overview.md){target="_blank"}
