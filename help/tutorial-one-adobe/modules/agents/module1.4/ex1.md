---
title: Introdução ao Brand Concierge
description: Introdução ao Brand Concierge
kt: 5342
doc-type: tutorial
exl-id: e05b60b1-62d7-4b70-834d-ef91782ac388
source-git-commit: 463636444922fcb8a1c4b538bd09901e665b039e
workflow-type: tm+mt
source-wordcount: '1115'
ht-degree: 1%

---

# 1.4.1 Introdução ao Brand Concierge

## Visão geral do Brand Concierge 1.4.1.1

Ao configurar o Brand Concierge, você usará dois elementos principais:

- **Agent Composer (Camada de Configuração)**

  Propósito: a plataforma de interface do usuário principal usada para criar e configurar experiências de IA de conversação.

  Principais responsabilidades:

   - Definir e gerenciar fontes de dados e bases de conhecimento
   - Definir a expressão da marca (tom, estilo, medidas de proteção)
   - Configurar o agente de reserva de reunião

- **Agent Orchestrator (Mecanismo de Execução)**

  Propósito: o mecanismo de raciocínio e orquestração que interpreta as solicitações do usuário e executa as ações apropriadas do agente.

  Principais responsabilidades:

   - Interpretar intenções de usuários em linguagem natural
   - Gerar e executar planos de raciocínio em várias etapas
   - Selecione e chame os operadores/ferramentas apropriados
   - Impor o contexto da marca, a conformidade e as medidas de proteção
   - Coordenar fluxos de trabalho de vários agentes
   - Agregar e compor respostas de várias fontes de dados

- **Tempo de Execução de Conversação do Brand Concierge (Camada de Serviço)**

  Finalidade: a camada de serviço de conversação voltada para o cliente que gerencia sessões de bate-papo, contexto e interações com o cliente.

  Componentes principais:

   - Agente da Web (cliente): interface de usuário de navegador ou bate-papo móvel integrada usando o Web SDK
   - Serviço de conversa (back-end): gerencia o estado da sessão e atua como gateway de orquestração

  Principais responsabilidades:

   - Gerenciar sessões de usuário e transcrições de conversa
   - Lidar com autenticação e perfis de usuário
   - Rotear mensagens entre o cliente e o Agent Orchestrator
   - Contexto de conversa persistente
   - Registra eventos comportamentais e operacionais no AEP para análise
   - Aplicar configurações específicas de superfície

## Configuração da instância do Brand Concierge 1.4.1.2

Para começar a criar sua própria instância do Brand Concierge, siga as etapas abaixo.

Ir para [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Abra o **Brand Concierge**.

![Brand Concierge](./images/bc1.png)

Você deverá ver isso. Clique no menu **seleção de sandbox**. Escolha a sandbox que foi atribuída a você. Essa sandbox deve ser chamada `techinsidersX` (substitua X pelo número atribuído).

![Brand Concierge](./images/bc2.png)

Em seguida, preencha as seguintes variáveis:

- **Nome da empresa**: CitiSignal

- **nome da concierge**: `CitiSignal Sales Assistant`.

Digite o seguinte texto em **O que você deseja que a concierge faça?**.

```javascript
Brand Concierge should help customers find their best device, plan or entertainment deal. Brand Concierge should help users discover internet plans, entertainment deals,  and help find the best available packages. Brand Concierge should also answer questions about devices such as phones and watches.
```

- **Link do site**: forneça o link para o site que você está usando

Clique em **Continuar**.

![Brand Concierge](./images/bc5.png)

Você deverá ver isso. Essas informações foram geradas usando IA com base na entrada fornecida na página anterior. Revise as informações e quando estiver satisfeito com elas, clique em **Gerar concierge**.

![Brand Concierge](./images/bc6.png)

Você deverá ver isso. Clique em **+ Adicionar** ao lado de **consultoria de produto para consumidores**.

![Brand Concierge](./images/bc6a.png)

Você deverá ver isso. Preencha os campos a seguir usando o texto abaixo.

**O que o concierge deve saber sobre o produto ou público-alvo antes de fazer recomendações?**

```
CitiSignal is a telecommunications company that sells devices such as phones and watches and that sells internet services such as their lead product CitiSignal Fiber Max. On top of that, CitiSignal sells entertainment services that offer premium streaming services at a discounted price. CitiSignal is targeting these 3 personas primarily: Smart Home Families, Online Gamers and Remote Professionals.
```

**Há regras ou limitações comerciais que a equipe de concierge deve seguir ao fazer recomendações?**

```
Prioritize positioning the CitiSignal Fiber Max offering.
```

**Há palavras-chave ou frases específicas que a concierge deve seguir ou evitar?**

```
Competitor pricing, competitor products
```

Clique em **Salvar**.

![Brand Concierge](./images/bc13.png)

Clique na **seta** para voltar à tela anterior.

![Brand Concierge](./images/bc13a.png)

Vá para **Knowledge Source** e clique em **Criar sua fonte de conhecimento**.

![Brand Concierge](./images/bc7.png)

Selecione **Links do site** e clique em **Continuar**.

![Brand Concierge](./images/bc7a.png)

Você deverá ver isso. Digite `CitiSignal website` como nome para sua fonte de conhecimento.

Agora é necessário carregar um arquivo csv que contenha os links do seu site. Baixe o [site do CitiSignal vincula o arquivo CSV](./assets/citisignal-website-links.csv) à área de trabalho.

Clique em **Procurar Arquivos**.

![Brand Concierge](./images/bc8.png)

Abra o arquivo **citisignal-website-links.csv** e atualize os links para apontar para o seu próprio site CitiSignal.

![Brand Concierge](./images/bc8a.png)

Selecione o arquivo **citisignal-website-links.csv** que você acabou de baixar e editar. Clique em **Abrir**.

![Brand Concierge](./images/bc9.png)

Seu arquivo foi adicionado a esta fonte de conhecimento. Clique em **Adicionar**.

![Brand Concierge](./images/bc10.png)

Você deverá ver isso. Clique em **Criar sua fonte de conhecimento**.

![Brand Concierge](./images/bc11.png)

Selecione **Catálogo de produtos** e clique em **Continuar**.

![Brand Concierge](./images/bc20.png)

Você deverá ver isso. Digite `CitiSignal Products` como nome para sua fonte de conhecimento. Clique em **Procurar Arquivos** e selecione **Procurar no dispositivo**.

![Brand Concierge](./images/bc21.png)

Agora é necessário carregar um arquivo csv que contenha os links do seu site. Baixe o [catálogo de produtos CitiSignal](./assets/CitiSignal-catalog.json.zip) na área de trabalho e descompacte-o.

![Brand Concierge](./images/bc26.png)

Selecione o arquivo **CitiSignal-catalog.json** e clique em **Abrir**.

![Brand Concierge](./images/bc23.png)

Você deverá ver isso. Clique em **Adicionar**.

![Brand Concierge](./images/bc24.png)

Você estará de volta aqui. O processamento levará de 10 a 20 minutos, portanto, você terá que voltar aqui posteriormente para verificar se o processamento foi bem-sucedido.

![Brand Concierge](./images/bc25.png)

## Etapas de integração do AEP 1.4.1.3

O Brand Concierge usa o Adobe Experience Platform para armazenar dados de interação de conversas. A conexão entre o Brand Concierge e o Experience Platform requer que um fluxo de dados seja configurado e usado pelo Brand Concierge.

### Sequência de dados

Ir para [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Abra o **Experience Platform**.

![Brand Concierge](./images/aep1.png)

Verifique se você selecionou a sandbox correta, que deve ser chamada `techinsidersX`. No menu esquerdo, role para baixo e selecione **Datastreams**.

![Brand Concierge](./images/aep2.png)

Clique em **Nova sequência de dados**.

![Brand Concierge](./images/aep3.png)

Insira o **Nome da Sequência de Dados** `--aepUserLdap-- - Brand Concierge` e selecione o **Esquema de Mapeamento** `cja-brand-concierge-sb-XXX`.

Clique em **Salvar**.

![Brand Concierge](./images/aep4.png)

A sequência de dados agora está configurada. Copie o nome e a ID da sequência de dados e anote-os em um arquivo de texto no computador.

![Brand Concierge](./images/aep5.png)

### Gerenciamento de configuração de sequência de dados

A próxima etapa é habilitar a API de Gerenciamento de configuração do Brand Concierge para configurar o fluxo de dados que você acabou de criar. Isso é necessário para resolver problemas como ID de organização IMS e detalhes da sandbox durante o processamento de solicitações.

Vá para **Página Inicial** e selecione **Controles de administrador**.

![Brand Concierge](./images/admincontrols1.png)

Vá para **Gerenciamento de Configuração da Sequência de Dados** e clique em **Adicionar Configuração**.

![Brand Concierge](./images/admincontrols2.png)

Cole a **ID da sequência de dados** da sequência de dados criada anteriormente. Clique em **Salvar**.

![Brand Concierge](./images/admincontrols3.png)

Você deveria ver algo assim.

![Brand Concierge](./images/admincontrols4.png)

## Gerenciamento de configuração de estilo do 1.4.1.4

Vá para **Gerenciamento de Configuração de Estilo**. Clique em **Inicializar configuração de estilo**.

![Brand Concierge](./images/admincontrols7.png)

Insira o **Nome da Marca** `CitiSignal` e clique em **Inicializar configuração de estilo**.

![Brand Concierge](./images/admincontrols8.png)

Você deverá ver isso.

![Brand Concierge](./images/admincontrols9.png)

## Manifesto do Agent Orchestrator 1.4.1.5

Ir para **Atualizar Manifesto**. Você deverá ver isso. Revise as informações em cada campo e faça alterações, se necessário.

Adicione o seguinte texto ao campo **Prompt de resposta de pergunta multimodal**, no final do texto existente. Não remova o texto que está lá, apenas adicione o texto abaixo sobre o que já está lá.

```
# Product Catalog (Fallback Reference)

Use this catalog when <Documents> doesn't return relevant results:

## CONNECTIVITY
**CitiSignal Fiber Max**
- Description: High-speed fiber internet with blazing-fast speeds, seamless streaming, ultra-responsive gaming, crystal-clear video calls. No data caps, no throttling. Future-ready for smart homes.
- Image: https://delivery-p168681-e1803036.adobeaemcloud.com/adobe/assets/urn:aaid:aem:cdb9e163-f9f5-4338-9d62-9807b61c082f/as/CitiSignal-Fiber-Max.webp
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/citisignal-fiber-max/CitiSignal-Fiber-Max

## ENTERTAINMENT
**Disney Plus**
- Description: Streaming home of Disney, Pixar, Marvel, Star Wars, National Geographic. Unlimited entertainment, new releases, original series, classic movies.
- Image: https://delivery-p168681-e1803036.adobeaemcloud.com/adobe/assets/urn:aaid:aem:b3bbe91a-e307-43bd-845f-1c77e7ba28df/as/Disney.webp
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/disney/Disney

**Netflix + HBO Max**
- Description: Unlimited TV shows and movies. Watch as much as you want, whenever you want.
- Image: https://delivery-p168681-e1803036.adobeaemcloud.com/adobe/assets/urn:aaid:aem:883be2a0-6c42-4508-b9ac-1e3a33235081/as/Netflix-HBO-Max.webp
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/netflix-hbo-max/Netflix-HBO-Max

**YouTube Premium**
- Description: Ad-free YouTube, YouTube Music, YouTube Kids. Watch offline, in background, on the go.
- Image: https://delivery-p168681-e1803036.adobeaemcloud.com/adobe/assets/urn:aaid:aem:ac2a8c66-8740-4fce-bd3a-8106db9e556f/as/YouTube-Premium.webp
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/youtube-premium/YouTube-Premium

**Apple One**
- Description: Apple Music (100M+ songs), Apple TV+, Apple Arcade, iCloud+. Complete Apple ecosystem bundle.
- Image: https://delivery-p168681-e1803036.adobeaemcloud.com/adobe/assets/urn:aaid:aem:94126f30-931a-447e-9cef-f58c60dbb17c/as/Apple-One.webp
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/apple-one/Apple-One

## DEVICES
**iPhone Air Sky Blue**
- Description: Slim iPhone with A19 Pro chip, 48MP camera, 6.5\" display, Apple Intelligence, all-day battery. Titanium frame, Ceramic Shield 2.
- Image: https://delivery-p168681-e1803036.adobeaemcloud.com/adobe/assets/urn:aaid:aem:0c4b1537-8268-4507-98e6-bbb03faa3ad1/as/iPhone-Air.webp
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/iphone-air/iPhone-Air?optionsUIDs=Y29uZmlndXJhYmxlLzkzLzIw

**iPhone Air Cloud White**
- Description: Slim iPhone with A19 Pro chip, 48MP camera, 6.5\" display, Apple Intelligence, all-day battery. Titanium frame, Ceramic Shield 2.
- Image: https://delivery-p168681-e1803036.adobeaemcloud.com/adobe/assets/urn:aaid:aem:30447a9c-c037-4df3-ae88-4127b9ec325e/as/iPhone-Air.webp
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/iphone-air/iPhone-Air?optionsUIDs=Y29uZmlndXJhYmxlLzkzLzI

**iPhone Air Space Black**
- Description: Slim iPhone with A19 Pro chip, 48MP camera, 6.5\" display, Apple Intelligence, all-day battery. Titanium frame, Ceramic Shield 2.
- Image: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/iphone-air/iPhone-Air?optionsUIDs=Y29uZmlndXJhYmxlLzkzLzIz
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/iphone-air/iPhone-Air?optionsUIDs=Y29uZmlndXJhYmxlLzkzLzIz

**iPhone Air Light Gold**
- Description: Slim iPhone with A19 Pro chip, 48MP camera, 6.5\" display, Apple Intelligence, all-day battery. Titanium frame, Ceramic Shield 2.
- Image: https://delivery-p168681-e1803036.adobeaemcloud.com/adobe/assets/urn:aaid:aem:ffa7b752-87ab-427f-a631-382fc67e7530/as/iPhone-Air.webp
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/iphone-air/iPhone-Air?optionsUIDs=Y29uZmlndXJhYmxlLzkzLzIx

**Apple Watch Ultra 3-Black**
- Description: Rugged smartwatch with 42hr battery, satellite communication, titanium case, dual-frequency GPS, hypertension notifications.
- Image: https://delivery-p168681-e1803036.adobeaemcloud.com/adobe/assets/urn:aaid:aem:d33f4f49-1239-45b8-a6e6-b97f12177e06/as/Apple-Watch-Ultra-3.webp
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/apple-watch-ultra-3/Apple-Watch-Ultra-3?optionsUIDs=Y29uZmlndXJhYmxlLzE4MS8yNA%3D%3D

**Apple Watch Ultra 3-Natural**
- Description: Rugged smartwatch with 42hr battery, satellite communication, titanium case, dual-frequency GPS, hypertension notifications.
- Image: https://delivery-p168681-e1803036.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8f107329-66f1-43fd-b505-b1c16892379f/as/Apple-Watch-Ultra-3.webp
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/apple-watch-ultra-3/Apple-Watch-Ultra-3?optionsUIDs=Y29uZmlndXJhYmxlLzE4MS8yNQ%3D%3D

# Sales Strategy

## Primary Focus: Connectivity Products
- When users ask about internet, connectivity, streaming, or home services, recommend **CitiSignal Fiber Max**.
- Highlight: blazing-fast fiber speeds, seamless streaming, no data caps, no throttling, future-ready.

## Entertainment Upselling Strategy
- After discussing connectivity, PROACTIVELY suggest entertainment products.
- Use natural transitions like:
  - \"With speeds like these, you'll want entertainment that keeps up...\"
  - \"Many of our customers enhance their experience with...\"
  - \"To get the most out of your connection...\"
- Match recommendations to user context:
  - Families with kids → **Disney Plus**
  - Movie/TV enthusiasts → **Netflix + HBO Max**
  - Ad-free YouTube fans → **YouTube Premium**
  - Apple ecosystem users → **Apple One**
```

![Brand Concierge](./images/admincontrols5a.png)

Depois de fazer as alterações, role para cima e clique em **Atualizar Manifesto**.

![Brand Concierge](./images/admincontrols5.png)

## 1.4.1.6 Concluir configuração da fonte de conhecimento

Ir para **Fontes de Conhecimento**. Após 10-20 minutos, o **Status** das duas fontes de conhecimento deve ser **Concluído**. Quando o status for **Sucesso** para ambas as fontes de conhecimento, clique em **Página inicial**.

![Brand Concierge](./images/admincontrols10.png)

Você deverá ver isso. Clique em **+ Conectar** no cartão **Links de site**.

![Brand Concierge](./images/bc28.png)

Selecione o site **CitiSignal** de origem do conhecimento e clique em **Salvar**.

![Brand Concierge](./images/bc29.png)

Você deverá ver isso. Clique em **+ Conectar** no cartão **Catálogo de produtos**.

![Brand Concierge](./images/bc30.png)

Selecione a fonte de conhecimento **CitiSignal Products** e clique em **Salvar**.

![Brand Concierge](./images/bc31.png)

Você deverá ver isso. Clique em **Visualizar** para começar a interagir com a Brand Concierge.

![Brand Concierge](./images/bc32.png)

Agora você pode começar a fazer perguntas relacionadas às fontes de conhecimento fornecidas.

![Brand Concierge](./images/bc33.png)

Digite a pergunta `what products do you sell?` e clique em **enviar**.

![Brand Concierge](./images/bc102.png)

Você deverá receber uma resposta semelhante de volta.

![Brand Concierge](./images/bc103.png)

A instância do Brand Concierge agora está pronta para ser implementada no site.

## Próximas etapas

Ir para [Implementar o Brand Concierge no seu site](./ex2.md){target="_blank"}

Voltar para [Brand Concierge](./brandconcierge.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
