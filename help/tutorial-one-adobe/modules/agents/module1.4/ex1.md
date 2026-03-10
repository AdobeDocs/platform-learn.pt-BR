---
title: Introdução ao Brand Concierge
description: Introdução ao Brand Concierge
kt: 5342
doc-type: tutorial
exl-id: e05b60b1-62d7-4b70-834d-ef91782ac388
source-git-commit: 1f4b945658834b7fd4f52f297fe761c49edd28fe
workflow-type: tm+mt
source-wordcount: '1119'
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

Você deverá ver isso. Clique no menu **seleção de sandbox**.

![Brand Concierge](./images/bc2.png)

Escolha a sandbox que foi atribuída a você. Essa sandbox deve ser chamada `--aepUserLdap-- - bc`.

![Brand Concierge](./images/bc3.png)

Clique em **Introdução**.

![Brand Concierge](./images/bc4.png)

Para o nome da sua instância do Brand Concierge, use: `--aepUserLdap-- - CitiSignal Brand Concierge`.

Digite o seguinte texto em **O que você deseja que a concierge faça?**.

```javascript
Brand Concierge should help customers find their best device, plan or entertainment deal. Brand Concierge should help users discover internet plans, entertainment deals,  and help find the best available packages. Brand Concierge should also answer questions about devices such as phones and watches.
```

Clique em **Criar**.

![Brand Concierge](./images/bc5.png)

Você deverá ver isso. Clique em **Introdução** para adicionar uma fonte de conhecimento.

![Brand Concierge](./images/bc6.png)

Selecione **Links de Sites** e clique em **Continuar**.

![Brand Concierge](./images/bc7.png)

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

Você deverá ver isso. Clique em **Leve-me para casa**.

![Brand Concierge](./images/bc11.png)

Você deverá ver isso. Clique em **Introdução** no cartão **Aviso de produto para consumidores**.

![Brand Concierge](./images/bc12.png)

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

As atualizações são salvas automaticamente. Clique na **seta** para voltar à tela anterior.

![Brand Concierge](./images/bc13.png)

Você deverá ver isso. Clique em **Introdução** para personalizar a expressão da sua marca.

![Brand Concierge](./images/bc14.png)

Você pode fazer suas próprias escolhas na página **Expressão da marca**. Verifique se há uma opção selecionada para cada pergunta.

![Brand Concierge](./images/bc15.png)

Role para baixo e selecione qualquer configuração para o campo **Duração da resposta**.

As atualizações são salvas automaticamente.

![Brand Concierge](./images/bc16.png)

Role para cima e clique na **seta** para voltar à tela anterior.

![Brand Concierge](./images/bc17.png)

Você estará de volta aqui. Clique em **Fontes de conhecimento**.

![Brand Concierge](./images/bc18.png)

Clique em **Criar fontes de conhecimento**.

![Brand Concierge](./images/bc19.png)

Selecione **Catálogo de produtos** e clique em **Continuar**.

![Brand Concierge](./images/bc20.png)

Você deverá ver isso. Digite `CitiSignal Products` como nome para sua fonte de conhecimento.

![Brand Concierge](./images/bc21.png)

Agora é necessário carregar um arquivo csv que contenha os links do seu site. Baixe o [catálogo de produtos CitiSignal](./assets/CitiSignal-catalog.json.zip) na área de trabalho e descompacte-o.

![Brand Concierge](./images/bc26.png)

Clique em **Procurar Arquivos** e selecione **Procurar no dispositivo**.

![Brand Concierge](./images/bc22.png)

Selecione o arquivo **CitiSignal-catalog.json** e clique em **Abrir**.

![Brand Concierge](./images/bc23.png)

Você deverá ver isso. Clique em **Adicionar**.

![Brand Concierge](./images/bc24.png)

Você estará de volta aqui.

![Brand Concierge](./images/bc25.png)

Após 10-20 minutos, o **Status** das duas fontes de conhecimento deve ser **Concluído**. Clique em **Página inicial**.

![Brand Concierge](./images/bc27.png)

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

## Etapas de integração do AEP 1.4.1.3

O Brand Concierge usa o Adobe Experience Platform para armazenar dados de interação de conversas. A conexão entre o Brand Concierge e o Experience Platform requer que um fluxo de dados seja configurado e usado pelo Brand Concierge.

### Sequência de dados

Ir para [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Abra o **Experience Platform**.

![Brand Concierge](./images/aep1.png)

Verifique se você selecionou a sandbox correta, que deve ser chamada `--aepUserLdap-- - bc`. No menu esquerdo, role para baixo e selecione **Datastreams**.

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

Vá para **Controles de administrador**.

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

Ir para **Atualizar Manifesto**. Você deverá ver isso.

![Brand Concierge](./images/admincontrols5.png)

Agora é necessário atualizar os campos no manifesto. Use a entrada abaixo para isso.

**Nome do agente**:

```
CitiSignal Sales Assistant
```

**Introdução**:

```
Welcome to CitiSignal! I'm here to help you discover the best connectivity and entertainment solutions for your home or business.
```

**Funções e responsabilidades**:

```
You are CitiSignal's AI Sales Assistant focused on:
1. **Primary Goal**: Selling connectivity products from the knowledge base
2. **Upselling Strategy**: Proactively recommending entertainment packages from the knowledge base to complement connectivity subscriptions
3. **Device Sales**: Assisting with device purchases from the knowledge base when relevant
4. **Customer Support**: Answering questions about plans, pricing, installation, and features based on knowledge base content

- ALWAYS call brand_concierge_product_knowledge_agent to obtain a response to a user query and provide it directly to the user without modification.
- All product information (names, descriptions, features, ratings) comes from the knowledge base <Documents>.
- When users show interest in internet services, identify and lead with connectivity products from the knowledge base.
- After establishing connectivity interest, naturally suggest entertainment add-ons from the knowledge base.
- Use consultative selling: understand user needs, then recommend appropriate products and bundles from the knowledge base.
```

**Escopo**:

```
You are CitiSignal's AI Sales Assistant, specializing in connectivity sales and entertainment bundle upselling.

# Your Primary Objectives:
1. **Sell Connectivity Products**: When users ask about internet or connectivity, recommend the appropriate connectivity product from <Documents>. Highlight key benefits mentioned in the product description.
2. **Upsell Entertainment Packages**: After discussing connectivity, proactively recommend entertainment products from <Documents> that complement the user's needs. Match recommendations to user context (families, movie enthusiasts, music lovers, etc.).
3. **Device Sales**: When relevant, recommend device products from <Documents> as complementary offerings.

# Sales Strategy:
- When a user inquires about internet, streaming, or connectivity, identify and recommend the relevant connectivity product from <Documents>.
- After establishing interest in connectivity, naturally transition to entertainment packages by highlighting how fast internet enhances streaming quality.
- Use natural transition phrases to introduce entertainment upsells.
- Emphasize bundle value and the seamless experience of having connectivity + entertainment from one provider.
- Use product ratings from <Documents> (productRating field) to prioritize higher-rated products when multiple options exist.

# Product Information Source:
- ALL product names, descriptions, features, and details MUST come from <Documents>.
- Use the exact productName from <Documents> - do not abbreviate or modify product names.
- Reference productDescription from <Documents> for accurate feature information.
- Use productRating from <Documents> to inform recommendations (higher ratings = stronger recommendations).
```

Clique em **Atualizar Manifesto**.

![Brand Concierge](./images/admincontrols6.png)

Clique em **Página inicial**.

![Brand Concierge](./images/admincontrols10.png)

Você deverá ver isso. Clique em **Visualizar** para começar a interagir com a Brand Concierge.

![Brand Concierge](./images/bc101.png)

Agora você pode começar a fazer perguntas relacionadas às fontes de conhecimento fornecidas. Digite a pergunta `what products do you sell?` e clique em **Enviar**.

![Brand Concierge](./images/bc102.png)

Você deverá receber uma resposta semelhante de volta.

![Brand Concierge](./images/bc103.png)

A instância do Brand Concierge agora está pronta para ser implementada no site.

Próxima Etapa: [Implementar o Brand Concierge em seu site](./ex2.md){target="_blank"}

Voltar para [Brand Concierge](./brandconcierge.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
