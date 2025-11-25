---
title: Introdução ao Agent Orchestrator
description: Introdução ao Agent Orchestrator
kt: 5342
doc-type: tutorial
source-git-commit: e90dee164dfe098c9fc56a04c481a733c0843858
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 0%

---

# 1.1.1 Introdução ao Agent Orchestrator

## 1.1.1 Definir contexto no Agent Orchestrator

Navegue até o assistente de IA e coloque em Exibição grande.

Confirme se você está no contexto do CJA para tarefas de análise.

>[!NOTE]
>
>Use a alternância de contexto ao alternar entre análise (CJA) e orquestração (JO).

## 1.1.2 Comece com as tendências gerais de compra para ancorar o contexto e ampliar a fibra

**Prompt**:

```javascript
Show me purchases by mainCategory over the last 2 month
```

**Intenção**: Obtenha um pulso de nível superior sob demanda de categoria—Celular, Telefone Fixo, Internet, TV, Fibra—especificamente pelos últimos 60 dias. Isso define linhas de base para sazonalidade, efeitos promocionais e variação regional após a implantação de NY.

Pensando:

&quot;A Fibre está ganhando participação pós-NY? Estamos vendo canibalização da Internet de cobre/DSL? Qual é a mudança de mix vs. pacotes de TV?&quot;

&quot;Isso me ajudará a dimensionar o público-alvo endereçável para Viena e definir metas realistas.&quot;

Leituras acionáveis que o profissional de marketing espera:

Um gráfico de barras/linhas empilhadas de Compras por categoria principal (diária/semanal).

Participação percentual de compras por categoria vs. período anterior.

Picos notáveis correlacionados com datas promocionais.

>[!NOTE]
>
>Fique de olho na atribuição atrasada — os pedidos de fibra podem ser capturados na &quot;Internet&quot; em alguns esquemas herdados. Em caso afirmativo, reconcilie a taxonomia antes das decisões.

 

**Prompt**:

```javascript
Show me purchases by mainCategory over the last 2 monthzoom into fiber performance
```

**Próximo prompt**

`Show me purchases by mainCategory = Fiber over the last 2 months`

Aprofunde-se nas tendências específicas de fibra.

**Ação** Observe a curva de crescimento e os picos regionais.

## 1.1.3 Correlacionar pedidos com preferências de conteúdo

**Prompt**:

```javascript
Show me ordersYTD by preferred genre for the last 2 months
```

**Intenção** Teste a hipótese de que a preferência de conteúdo (por exemplo, ficção científica, esportes, drama) prevê o comportamento de atualização da banda larga, especialmente para as necessidades de banda larga.

**Pensando**

&quot;Os fãs de SciFi geralmente assistem a 4K e transmitem a partir de vários dispositivos; provavelmente valorizam a baixa latência.&quot;

&quot;Vamos quantificar se o SciFi (e talvez o Sports) está correlacionado com pedidos recentes.&quot;

**Saídas esperadas**

Uma tabela dinâmica de Pedidos (filtro YTD aplicado) dividida por gênero preferido, limitada a últimos 2 meses.

Classifique os gêneros por taxa de conversão de pedido e AOV (valor médio de pedido).

Decisão: se o SciFi mostrar um sinal forte, ele se tornará o principal pilar criativo do lançamento do Fiber Max em Viena (por exemplo, mensagens &quot;nunca mais use buffer&quot;, pacotes premium).

**Aviso**

`Show me ordersYTD by preferred genre for the last 2 months`

**Intenção**

Analise a conversão por gênero (por exemplo, ficção científica, esportes).

**Meta** Validar se os ventiladores Sci-Fi ultrapassam o índice para atualizações de fibra.

## 1.1.4 Identificar Jornadas de fibra existentes

**Prompt**:

```javascript
What journey was running and had Fiber in the name
```

**Intenção** Descubra quais jornadas ativas ou concluídas recentemente incluem &quot;Fibra&quot; no título, por exemplo, &quot;Atualização de Fibra NYC - setembro&quot;, &quot;Avaliação de Fibra - Pacote de Transmissão&quot;.

**Pensando**

&quot;Quais dessas jornadas tiveram bom desempenho e quais foram seus acionadores?&quot;

&quot;Posso reutilizar a lógica de orquestração vencedora para Viena?&quot;

**Saídas esperadas**

Lista de jornadas com status (ativo, pausado, encerrado), intervalos de datas, segmentos de destino, KPIs (taxa de abertura, CTR, conversão).

Próxima movimentação: selecione uma ou duas jornadas de fibra bem-sucedidas para clonagem/adaptação.

**Aviso**

`What journey was running and had Fiber in the name?`

Listar jornadas ativas ou passadas com mensagens por fibra.

Ação: selecione jornadas de alto desempenho para clonagem.

## 1.1.5 Verifique o público-alvo da propagação para obter uma promoção histórica relevante

**Prompt**:

```javascript
What was the initial audience in that SCi-Fi promo 2024 - jl journey
```

**Intenção** Entenda a definição de propagação da jornada &quot;SciFi Promo 2024 - jl&quot; — quais características determinaram o direcionamento (por exemplo, &quot;Preferência de gênero SciFi&quot;, &quot;4+ dispositivos&quot;, &quot;fluxo ≥ 300 GB/mês&quot;).

**Pensando**

&quot;Quero combinar a criatividade comprovada de SciFi com as mensagens de desempenho do Fibre Max.&quot;

&quot;Se o público-alvo se sobrepõe a downloaders pesados, podemos empilhar a propensão.&quot;

**Saídas esperadas**

Critérios de público (inclusão/exclusão), tamanho do público, filtros de região, recenticidade, limites de frequência.

>[!NOTE]
>
>Alterar contexto para CJA

A partir desse ponto, o profissional de marketing muda para o modo de análise para garantir a geração de relatórios adequados.

**Prompt**:

```javascript
What was the initial audience in that SCi-Fi promo 2024 - jl journey?
```

Revise os critérios de público-alvo (hábitos de transmissão, contagem de dispositivos).

Meta: entender as características de necessidades de alta largura de banda.

## 1.1.6 Validar o desempenho do jornada por meio da análise de fallout

**Prompt**:

```javascript
Create a fall-out report on the "Sci-Fi Promo 2024 - jl" journey
```

>[!NOTE]
>
>Alterar contexto para CJA)

**Intenção** Criar um funnel em etapas no Customer Journey Analytics

Entregue → Aberto → Clicado → Desembarcado → Exibição do produto → Adicionar ao carrinho → Check-out → Pedido concluído

Inclua exibições de SKU relacionadas a fibra como uma ramificação.

Pensando:

&quot;Onde estamos perdendo pessoas — e-mail aberto, carregamento de página de aterrissagem, PDPs, atrito de check-out?&quot;

&quot;Os usuários de ficção científica rejeitam mais ou menos do que a média no PDP de fibra?&quot;

Saída esperada:

Uma visualização de fallout com taxas de devolução em cada etapa.

Sobreposições de segmento (ficção científica vs. esportes vs. outros).

Detalhamento do dispositivo/navegador para atrito técnico.

Decisões:

Se a lista suspensa de check-out estiver alta, fale com o produto/UX para corrigir o fluxo de pagamento.

Se a saída de PDP for alta, reprocesse a clareza da solicitação (velocidades, tempos de instalação, valor do pacote).

>[!NOTE]
>
>Alterar contexto para JO

Agora, o profissional de marketing migra para o Adobe Journey Optimizer para operações de orquestração e público-alvo.

**Prompt**:

```javascript
Create a fall-out report on the "Sci-Fi Promo 2024 - jl" journey 
```

Criar visualização do funnel: Entregue → Aberto → Clicado → Check-out → Pedido.

Ação: identificar pontos de devolução e otimizar mensagens ou UX.


## 1.1.7 Encontre públicos-alvo existentes alinhados à alta utilização

**Prompt**:

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

>[!NOTE]
>
>Alterar contexto para Adobe Journey Optimizer

Intenção: Localize qualquer público-alvo de JO chamado de &quot;baixadores intensos&quot;, provavelmente definido por limites mensais de uso de dados, horas de transmissão ou simultaneidade de dispositivo.

Pensando:

&quot;Se existe um público-alvo como os Heavy Downloaders, ele é perfeito para o posicionamento Fibre Max: velocidade, confiabilidade, níveis ilimitados.&quot;

Saída esperada:

Metadados do público-alvo: critérios de definição, tamanho, última atualização, tags de governança e disponibilidade de região.

**Prompt**:

```javascript
Is there an audience that has " heavy downloaders" in the title 
```

Localize públicos com alto uso de dados.

Meta: combinar com a preferência de ficção científica para direcionamento de fibra máxima.

## 1.1.8 Determine se esses públicos-alvo já estão em uso

**Prompt**:

```javascript
Which of the above are used in a journey? 
```

Intenção: verifique a vinculação de público-alvo para jornada — certifique-se de que não duplicaremos a mensagem ou não entraremos em conflito com os programas atuais.

Pensando:

&quot;Se os Heavy Downloaders já estiverem em uma jornada de retenção, precisamos de lógica de supressão ou limite de frequência para evitar fadiga.&quot;

Saída esperada:

Mapeamentos: público → nome da jornada, status, política de contato, último envio, desempenho.

Decisão:

Se estiver em uso, crie exclusões ou supressão compartilhada para o lançamento em Viena.

Se não estiver em uso, sinal verde para nova jornada.

Aviso:

quais das opções acima são usadas em uma jornada?

Garanta que não haja sobreposição com campanhas ativas.

Ação: Aplicar supressão se necessário.

## 1.1.9 Criar nova Jornada para lançamento de fibra máxima

**Prompt**:

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

Intenção: criar uma nova jornada de trabalho direcionada ao público-alvo composto:

Preferência de SciFi de Heavy Downloaders ∩ (chave de público kbaa_5207bf).

Pensando:

&quot;Esse é o ponto ideal para o Fiber Max: alta propensão + relevância criativa.&quot;

&quot;Vamos orquestrar uma experiência multitoque vinculada à disponibilidade em Viena.&quot;

Design da jornada (JO):

Critérios de entrada:

Público: Downloads pesados - Sci-Fi Preference_kbaa_5207bf

Geografia: Metro de Viena (lista de CEP/código postal ou polígono geográfico)

Elegibilidade: não está na campanha ativa &quot;Atualização de fibra NYC - setembro&quot;; não é um assinante de fibra atual.

&amp; Horário do acionador:

14 dias antes do lançamento em Viena (janeiro de 2026): email de visualização — &quot;Fibre Max está chegando&quot;.

Semana de lançamento: email principal + banner no aplicativo + sincronização de mídia paga (via destino CDP).

T+3 dias: Divisão de comportamento — se não houver clique, chamada de atenção de SMS; se tiver sido clicado, mas não solicitado, redirecione com um CTA de disponibilidade de instalador.

T+10 dias: Teste de oferta—instalação gratuita vs. desconto do primeiro mês (A/B).

Personalization:

Cópia dinâmica para amantes de SciFi (latência/ganchos de transmissão de 4K).

Declarações de velocidade/latência personalizadas para a combinação de dispositivos (consoles de jogos, caixas de transmissão).

Recomendação do pacote: Fiber Max + pacote de conteúdo premium TV scifi.

Governança:

Limite de frequência: máximo de 3 toques por 10 dias.

Suprimir se o assinante de Fibre atual ou se houver um tíquete para instalação.

Respeite as preferências de recusa.

Plano de medição (CJA):

Rastrear: entrega, abrir, clicar, visualização PDP, início da finalização, conclusão do pedido.

KPIs: Taxa de conversão para Máximo de fibra, aumento vs. controle, instalação de tempo.

Diagnóstico: relatório de fallout por segmento de dispositivo/gênero.

Forma

Como tudo isso se encaixa (o modelo mental do profissional de marketing)

Diagnosticar demanda (categorias gerais → Fibra especificamente).

Prove o conteúdo para o sinal de conversão (pedidos por gênero).

Minhas jornadas bem sucedidas (encontre jornadas com nomes de fibra e o público promocional de ficção científica).

Validar pontos de atrito (fallout de CJA na jornada SciFi).

Ativar contra segmentos de alta propensão (Heavy Downloaders ∩ SciFi).


Voltar para [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}