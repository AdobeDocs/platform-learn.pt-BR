---
title: Usar seu modelo de mídia dinâmica com o Adobe Journey Optimizer
description: Usar seu modelo de mídia dinâmica com o Adobe Journey Optimizer
kt: 5342
doc-type: tutorial
exl-id: 0dd499cc-ec3b-42c3-9c08-6512ea5b9377
source-git-commit: 8f746831d4a1481f8ccc14539273c4b16ca5170b
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 2%

---

# 1.4.2 Usar seu modelo de mídia dinâmica com o Adobe Journey Optimizer

## 1.4.2.1 Crie sua campanha no Adobe Journey Optimizer

Faça login no Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`. Você estará na exibição **Página inicial** da sua sandbox `--aepSandboxName--`.

![ACOP](./images/acoptriglp.png)

Agora você criará uma campanha. Ao contrário da jornada baseada em eventos do exercício anterior, que depende de eventos de experiência de entrada, entradas de público-alvo ou saídas para acionar uma jornada para um cliente específico, as campanhas direcionam todo um público-alvo uma vez com conteúdo exclusivo, como boletins informativos, promoções únicas ou informações genéricas ou periodicamente com conteúdo semelhante enviado regularmente, como por exemplo campanhas de aniversário e lembretes.

No menu, vá para **Campanhas** e clique em **Criar campanha**.

![Journey Optimizer](./images/gsemail21.png)

Selecione **Agendado - Marketing** e clique em **Criar**.

![Journey Optimizer](./images/gsemail22.png)

Na tela de criação da campanha, configure o seguinte:

- **Nome**: `--aepUserLdap-- - CitiSignal Fiber Max DM Email Campaign`.

Clique em **Ações**.

![Journey Optimizer](./images/gsemail23.png)

Clique em **+ Adicionar ação** e selecione **Email**.

![Journey Optimizer](./images/gsemail24.png)

Em seguida, selecione uma **configuração de email** existente e clique em **Editar conteúdo**.

![Journey Optimizer](./images/gsemail25.png)

Você verá isso. Para a **Linha de assunto**, use esta:

```
{{profile.person.name.firstName}}, say hello to CitiSignal Fiber Max!
```

Em seguida, clique em **Editar conteúdo**.

![Journey Optimizer](./images/gsemail26.png)

Selecione **Design do zero**.

![Journey Optimizer](./images/gsemail27.png)

Você deverá ver isso.

![Journey Optimizer](./images/gsemail28.png)

Adicionar 2x **1:1 coluna** à tela.

![Journey Optimizer](./images/gsemail29.png)

Vá para **Fragmentos**, arraste o fragmento **cabeçalho** para a primeira coluna:1 e arraste o fragmento **rodapé** para a segunda coluna:1.

![Journey Optimizer](./images/gsemail30.png)

Adicione uma nova coluna 1:1 entre os 2 fragmentos e adicione uma **Imagem** nessa coluna 1:1. Em seguida, clique em **Procurar**.

![Journey Optimizer](./images/gsemail31.png)

Navegue até a pasta em que você armazenou o modelo do Dynamic Media. Selecione seu modelo do Dynamic Media e clique em **Selecionar**.

![Journey Optimizer](./images/gsemail32.png)

Você deverá ver isso. Você também. observe os **PARÂMETROS** que permitem alterar os parâmetros do modelo de mídia dinâmica.

![Journey Optimizer](./images/gsemail33.png)

## 1.4.2.2 Personalizar o modelo de mídia dinâmica

Conforme discutido no exercício anterior, o AJO agora precisa decidir dinamicamente quais valores devem ser inseridos no modelo do Dynamic Media.

Assim como na etapa **Preview** do exercício anterior, os campos **city_paris**, **city_dubai** e **city_ny** devem ser definidos como 1, o que significa que essas imagens ficarão ocultas.

Para o campo **título**, clique no ícone de personalização.

![Journey Optimizer](./images/gsemail34.png)

Substituir o texto padrão por este: `Hi {{profile.person.name.firstName}}`. Clique em **Salvar**.

![Journey Optimizer](./images/gsemail35.png)

Para o campo **corpo**, clique no ícone de personalização.

![Journey Optimizer](./images/gsemail36.png)

Substituir o texto padrão por este: `CitiSignal is coming to {{profile.homeAddress.city}}!`. Clique em **Salvar**.

![Journey Optimizer](./images/gsemail37.png)

Verifique se o campo **`dynamic_city_hide`** está definido como 0. Clique no ícone de personalização do campo **`dynamic_city_image`**.

![Journey Optimizer](./images/gsemail38.png)

Substituir o texto padrão por este: `--aepUserLdap--CitiSignalDM/citisignal-fiber-max-is-coming_citisignal-{{profile._experienceplatform.individualCharacteristics.fiber_rollout.closest_rollout_city}}-1`. Clique em **Salvar**.

![Journey Optimizer](./images/gsemail39.png)

Você deverá ver isso. A imagem não é renderizada aqui, o que é esperado, pois as variáveis dinâmicas não estão disponíveis no contexto do editor de email.

Clique em **Salvar**.

![Journey Optimizer](./images/gsemail40.png)

Para testar sua configuração, clique em **Simular Conteúdo** e selecione **Simular Conteúdo**.

![Journey Optimizer](./images/gsemail41.png)

Você deveria ver algo assim. Se você não tiver perfis de teste disponíveis, adicione-os em **Gerenciar perfis de teste**.

Depois que você tiver perfis de teste disponíveis que contenham os dados necessários para testar esse caso de uso, será possível alternar de um perfil para outro para ver as alterações ocorrerem dinamicamente.

Aqui está um perfil que está ligado à cidade de implantação, Nova York.

![Journey Optimizer](./images/gsemail42.png)

Aqui está um perfil que está ligado à cidade de implantação Paris.

![Journey Optimizer](./images/gsemail43.png)

Aqui está um perfil que está ligado à cidade de implantação Dubai.

Clique em **Fechar**.

![Journey Optimizer](./images/gsemail44.png)

Você terminou este exercício agora. Não há necessidade de publicar sua campanha de email.

## Próximas etapas

Voltar para [Adobe Experience Manager Assets e Dynamic Media](./aemassetsdm.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}