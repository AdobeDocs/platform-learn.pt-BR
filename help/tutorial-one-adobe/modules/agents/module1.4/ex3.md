---
title: Implementar o Brand Concierge usando tags de coleção de dados
description: Implementar o Brand Concierge usando tags de coleção de dados
kt: 5342
doc-type: tutorial
source-git-commit: 3704abb57e9fa64c2ff6d6914b6da8b46a5f44aa
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 3%

---

# 1.4.3 Implementação do Brand Concierge usando tags de coleção de dados

>[!IMPORTANT]
>
>Este exercício está sendo realizado e ainda não foi concluído.

## Propriedade de Tags da coleção de dados

O Brand Concierge precisa enviar dados para o Adobe Experience Platform. Para fazer isso, o Web SDK (ou alloy.js) precisa ser implantado em seu site.

Para tornar isso possível, agora é necessário criar uma propriedade de Tags de coleção de dados.

Ir para [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Abra **Coleção De Dados**.

![Brand Concierge](./images/aep101.png)

Clique em **Nova propriedade**.

![Brand Concierge](./images/aep102.png)

Digite o nome: `--aepUserLdap-- - CitiSignal Website + Brand Concierge` e também o domínio do seu site.

Clique em **Salvar**.

![Brand Concierge](./images/aep103.png)

Procure sua propriedade e abra-a.

![Brand Concierge](./images/aep104.png)

Vá para **Extensões** e depois para **Catálogo**.

![Brand Concierge](./images/aep105.png)

Pesquise por `web sdk` e clique na extensão **Adobe Experience Platform Web SDK**. Clique em **Instalar**.

![Brand Concierge](./images/aep106.png)

Você deverá ver isso. Você só precisa fornecer os detalhes do seu fluxo de dados aqui. Para fazer isso, role para baixo um pouco.

![Brand Concierge](./images/aep107.png)

Para todos os 3 ambientes **Produção**, **Preparo** e **Desenvolvimento**, selecione o seguinte:

- **Sandbox**: `--aepUserLdap-- - bc`
- **Sequência de dados**: `--aepUserLdap-- - Brand Concierge`

Clique em **Salvar**.

![Brand Concierge](./images/aep108.png)

Você deverá ver isso. Vá para **Regras**.

![Brand Concierge](./images/aep108a.png)

Clique em **Criar nova regra**.

![Brand Concierge](./images/aep109.png)

Digite o nome: `Homepage`. Em seguida, clique em **+ Adicionar** em **EVENTOS**.

![Brand Concierge](./images/aep110.png)

Selecione as seguintes opções:

- **Extensão**: **Núcleo**
- **Tipo de Evento**: **Biblioteca Carregada (Início da Página)**

Clique em **Manter alterações**.

![Brand Concierge](./images/aep111.png)

Você deverá ver isso. Clique em **+ Adicionar** em **CONDIÇÕES**.

![Brand Concierge](./images/aep112.png)

Selecione as seguintes opções:

- **Tipo Lógico**: **Regular**
- **Extensão**: **Núcleo**
- **Tipo De Condição**: **Caminho Sem Cadeia De Caracteres De Consulta**
- **caminho igual a...**: digite o domínio do site, neste caso `https://vangeluw.adobedemosystem.com/`

Clique em **Manter alterações**.

![Brand Concierge](./images/aep113.png)

Você deverá ver isso. Clique em **+ Adicionar** em **AÇÕES**.

![Brand Concierge](./images/aep114.png)

Selecione as seguintes opções:

- **Extensão**: **Núcleo**
- **Tipo de Ação**: **Código Personalizado**
- **Idioma**: **JavaScript**

Clique em **Abrir editor**.

![Brand Concierge](./images/aep115.png)

Cole o código a seguir:

```javascript
window["alloy"]("sendEvent", {
        conversation: {fetchConversationalExperience: true}
    }).then(result=> {
        console.log("Conversation experience fetched", result);
        window["alloy"]("bootstrapConversationalExperience", {
            selector: "#brand-concierge-mount",
						// src: "main.js",
            src: "https://experience-stage.adobe.net/solutions/experience-platform-brand-concierge-web-agent/static-assets/main.js",
            stylingConfigurations: window.styleConfiguration,
						stickySession: true
        })
    });
```

Clique em **Salvar**.

![Brand Concierge](./images/aep116.png)

Você deverá ver isso. Clique em **Manter alterações**.

![Brand Concierge](./images/aep117.png)

Você deverá ver isso. Clique em **Salvar**.

![Brand Concierge](./images/aep118.png)

Vá para **Fluxo de Publicação**. Clique em **Adicionar biblioteca**.

![Brand Concierge](./images/aep119.png)

Insira o nome: `Dev`, selecione **Desenvolvimento (desenvolvimento)** para o ambiente e clique em **Adicionar todos os recursos alterados**.

Clique em **Salvar e criar para desenvolvimento**.

![Brand Concierge](./images/aep120.png)

Após alguns minutos, sua biblioteca será criada. Aguarde até ver o **ponto verde** ao lado de **Des**. Em seguida, vá para **Ambientes**.

![Brand Concierge](./images/aep121.png)

Clique no ícone **Instalar** do ambiente **Desenvolvimento**.

![Brand Concierge](./images/aep122.png)

Você deverá ver isso. Clique no botão **copiar** para copiar o caminho da biblioteca. Você precisará implementar isso em seu site.

O caminho da biblioteca deve ter esta aparência:
`<script src="https://assets.adobedtm.com/XXXXXXX/XXXXXXXX/launch-XXXXXXXXX-development.min.js" async></script>`

![Brand Concierge](./images/aep123.png)

Voltar para [Brand Concierge](./brandconcierge.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}