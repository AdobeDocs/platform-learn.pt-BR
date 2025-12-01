---
title: Introdução ao Brand Concierge
description: Introdução ao Brand Concierge
kt: 5342
doc-type: tutorial
source-git-commit: 6642acb3fdce2c9d3a9b919d5c9457191e4780a6
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---

# 1.4.1 Introdução ao Brand Concierge

## Vídeo

Neste vídeo, você receberá uma explicação e uma demonstração de todas as etapas envolvidas neste exercício.

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

Escolha a sandbox que foi atribuída a você. Essa sandbox deve ser chamada `--aepUserLdap--`.

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



```
CitiSignal is a telecommunications company that sells devices such as phones and watches and that sells internet services such as their lead product CitiSignal Fiber Max. On top of that, CitiSignal sells entertainment services that offer premium streaming services at a discounted price. CitiSignal is targeting these 3 personas primarily: Smart Home Families, Online Gamers and Remote Professionals.
```

```
Prioritize positioning the CitiSignal Fiber Max offering.
```

```
Competitor pricing, competitor products
```

As atualizações são salvas automaticamente. Clique na **seta** para voltar à tela anterior.

![Brand Concierge](./images/bc13.png)

Você deverá ver isso. Clique em **Introdução** para personalizar a expressão da sua marca.

![Brand Concierge](./images/bc14.png)

Você pode fazer suas próprias escolhas na página **Expressão da marca**.

![Brand Concierge](./images/bc15.png)

Role para baixo e selecione qualquer configuração para o campo **Duração da resposta**.

As atualizações são salvas automaticamente.

![Brand Concierge](./images/bc16.png)

Role para cima e clique na **seta** para voltar à tela anterior.

![Brand Concierge](./images/bc17.png)


Voltar para [Brand Concierge](./brandconcierge.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}