---
title: Visão geral do Serviço de consulta e do Data Distiller
description: O Adobe Experience Platform Query Service permite que os usuários explorem, validem e transformem dados de experiência do cliente armazenados no data lake usando SQL, com recursos aprimorados como saída de dados e agendamento disponíveis por meio do complemento Data Distiller. Este vídeo fornece uma visão geral dos principais recursos para ajudar os usuários a entender como aproveitar o Serviço de consulta em vários aplicativos baseados em plataforma.
feature: Queries
role: Data Engineer, Developer
level: Beginner
jira: KT-3139
last-substantial-update: 2025-06-23T00:00:00Z
exl-id: 988bc316-9eec-4dca-8049-95c2d613379d
source-git-commit: b0466e114d657c2584b23bfd76e4f6c185c83c06
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 13%

---

# Visão geral do Serviço de consulta e do Data Distiller

O Adobe Experience Platform Query Service permite que os usuários explorem, validem e transformem dados de experiência do cliente armazenados no data lake usando SQL, com recursos aprimorados como saída de dados e agendamento disponíveis por meio do complemento Data Distiller. Este vídeo fornece uma visão geral dos principais recursos para ajudar os usuários a entender como aproveitar o Serviço de consulta em vários aplicativos baseados em plataforma. Para obter mais informações, visite a [documentação do Serviço de consulta](https://experienceleague.adobe.com/pt-br/docs/experience-platform/query/home).

>[!VIDEO](https://video.tv.adobe.com/v/33187?learn=on&enablevpops&captions=por_br)

## Uso básico

<!-- CARDS
* query-service-ui.md
* query-service-api.md
* adobe-defined-functions.md
* run-queries.md
* understanding-data-usage-patterns-with-query-service.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Query Service UI">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="query-service-ui.md" title="Interface do usuário do serviço de consulta" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333403?format=jpeg&nocache=1740415310696" alt="Interface do usuário do serviço de consulta"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="query-service-ui.md" target="_blank" rel="referrer" title="Interface do usuário do serviço de consulta">Interface do Usuário do Serviço de Consulta</a>
                    </p>
                    <p class="is-size-6">Saiba como gravar e executar consultas, exibir consultas executadas anteriormente e acessar consultas salvas por outros usuários em sua Organização IMS no serviço de consulta do Adobe Experience Platform.</p>
                </div>
                <a href="query-service-ui.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Saiba mais</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Query Service API">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="query-service-api.md" title="API do serviço de consulta" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333700?format=jpeg&nocache=1740415310716" alt="API do serviço de consulta"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="query-service-api.md" target="_blank" rel="referrer" title="API do serviço de consulta">API de Serviço de Consulta</a>
                    </p>
                    <p class="is-size-6">Saiba como gravar e executar consultas, criar consultas de agendamento e criar um template de consulta usando a API de serviço de consulta do Adobe Experience Platform.</p>
                </div>
                <a href="query-service-api.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Saiba mais</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Adobe Defined Functions">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="adobe-defined-functions.md" title="Funções definidas pelo Adobe" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333701?format=jpeg&nocache=1740415310668" alt="Funções definidas pelo Adobe"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="adobe-defined-functions.md" target="_blank" rel="referrer" title="Funções definidas pelo Adobe">Funções definidas pela Adobe</a>
                    </p>
                    <p class="is-size-6">Saiba como usar funções definidas pelo Adobe no Serviço de consulta do Adobe Experience Platform para executar tarefas comerciais comuns em dados de evento de experiência.</p>
                </div>
                <a href="adobe-defined-functions.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Saiba mais</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Run Queries with Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="run-queries.md" title="Executar consultas com o serviço de consulta" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/33393?format=jpeg&nocache=1740415310683&captions=por_br" alt="Executar consultas com o serviço de consulta"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="run-queries.md" target="_blank" rel="referrer" title="Executar consultas com o serviço de consulta">Executar Consultas com o Serviço de Consulta</a>
                    </p>
                    <p class="is-size-6">Este vídeo mostra como executar queries na interface do Adobe Experience Platform e em um cliente PSQL. Além disso, é demonstrado o uso de propriedades individuais em um objeto XDM, o uso de funções definidas pelo Adobe e o uso de CREATE TABLE AS SELECT (CTAS).</p>
                </div>
                <a href="run-queries.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Saiba mais</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Understanding Data Usage Patterns with Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="understanding-data-usage-patterns-with-query-service.md" title="Noções básicas sobre padrões de uso de dados com o serviço de consulta" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/33186?format=jpeg&nocache=1740415310706&captions=por_br" alt="Noções básicas sobre padrões de uso de dados com o serviço de consulta"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="understanding-data-usage-patterns-with-query-service.md" target="_blank" rel="referrer" title="Noções básicas sobre padrões de uso de dados com o serviço de consulta">Compreendendo os Padrões de Uso de Dados com o Serviço de Consulta</a>
                    </p>
                    <p class="is-size-6">Este vídeo compartilha dicas e práticas recomendadas para executar consultas na interface do editor de consultas, clientes PSQL, soluções de business intelligence (BI) e a API HTTP.</p>
                </div>
                <a href="understanding-data-usage-patterns-with-query-service.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Saiba mais</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Validação e exploração de dados

<!-- CARDS
* explore-data.md
* validate-data-in-the-datalake.md
* 
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Explore data">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="explore-data.md" title="Explorar dados" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333415?format=jpeg&nocache=1740415312087" alt="Explorar dados"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="explore-data.md" target="_blank" rel="referrer" title="Explorar dados">Explorar dados</a>
                    </p>
                    <p class="is-size-6">Saiba como validar dados assimilados, pré-visualizar dados e explorar as propriedades estatísticas e analíticas de dados usando funções SQL.</p>
                </div>
                <a href="explore-data.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Saiba mais</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Validate data in the datalake with Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="validate-data-in-the-datalake.md" title="Validar dados no datalake com o Serviço de consulta" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3445682?format=jpeg&nocache=1740415312076&captions=por_br" alt="Validar dados no datalake com o Serviço de consulta"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="validate-data-in-the-datalake.md" target="_blank" rel="referrer" title="Validar dados no datalake com o Serviço de consulta">Validar dados no datalake com o Serviço de Consulta</a>
                    </p>
                    <p class="is-size-6">Saiba como validar se os dados foram assimilados com êxito no datalake usando o serviço de consulta da Adobe Experience Platform.</p>
                </div>
                <a href="validate-data-in-the-datalake.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Saiba mais</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Transformação de dados com o Data Distiller

<!-- CARDS
* 
* prepare-data.md
* 
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Prepare data">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="prepare-data.md" title="Preparar dados" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333699?format=jpeg&nocache=1740415313086" alt="Preparar dados"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="prepare-data.md" target="_blank" rel="referrer" title="Preparar dados">Preparar dados</a>
                    </p>
                    <p class="is-size-6">Saiba como limpar, preparar e combinar dados de vários conjuntos de dados para criar um novo usando as funções CTAS (Create Table AS) e Spark SQL para relatórios e painéis.</p>
                </div>
                <a href="prepare-data.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Saiba mais</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Casos de uso

<!-- CARDS
* understanding-data-usage-patterns-with-query-service.md
* psql-client-tableau.md
* analyze-and-visualize.md
* recharge-your-customer-data.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Understanding Data Usage Patterns with Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="understanding-data-usage-patterns-with-query-service.md" title="Noções básicas sobre padrões de uso de dados com o serviço de consulta" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/33186?format=jpeg&nocache=1740415313190&captions=por_br" alt="Noções básicas sobre padrões de uso de dados com o serviço de consulta"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="understanding-data-usage-patterns-with-query-service.md" target="_blank" rel="referrer" title="Noções básicas sobre padrões de uso de dados com o serviço de consulta">Compreendendo os Padrões de Uso de Dados com o Serviço de Consulta</a>
                    </p>
                    <p class="is-size-6">Este vídeo compartilha dicas e práticas recomendadas para executar consultas na interface do editor de consultas, clientes PSQL, soluções de business intelligence (BI) e a API HTTP.</p>
                </div>
                <a href="understanding-data-usage-patterns-with-query-service.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Saiba mais</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Connect Tableau to Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="psql-client-tableau.md" title="Conectar o Tableau ao Serviço de consulta" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333702?format=jpeg&nocache=1740415313229" alt="Conectar o Tableau ao Serviço de consulta"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="psql-client-tableau.md" target="_blank" rel="referrer" title="Conectar o Tableau ao Serviço de consulta">Conectar o Tableau ao Serviço de consulta</a>
                    </p>
                    <p class="is-size-6">Saiba como se conectar ao Serviço de consulta de vários aplicativos de cliente de desktop que oferecem suporte ao protocolo PostgreSQL e como usar ferramentas e drivers PostgreSQL para conectar e gravar consultas.</p>
                </div>
                <a href="psql-client-tableau.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Saiba mais</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Analyze and visualize omni-channel insights in Tableau using Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="analyze-and-visualize.md" title="Analisar e visualizar insights omnicanal no Tableau usando o Serviço de consulta" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/342115?format=jpeg&nocache=1740415313204" alt="Analisar e visualizar insights omnicanal no Tableau usando o Serviço de consulta"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="analyze-and-visualize.md" target="_blank" rel="referrer" title="Analisar e visualizar insights omnicanal no Tableau usando o Serviço de consulta">Analisar e visualizar insights omnicanal no Tableau usando o Serviço de consulta</a>
                    </p>
                    <p class="is-size-6">Saiba como usar o Serviço de consulta da Adobe Experience Platform com ferramentas de visualização de dados externas usando um exemplo de análise de churn.</p>
                </div>
                <a href="analyze-and-visualize.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Saiba mais</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Recharge your customer data to deliver electrifying experiences">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="recharge-your-customer-data.md" title="Recarregue os dados do cliente para fornecer experiências eletrizantes" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3454945?format=jpeg&nocache=1740415313218&captions=por_br" alt="Recarregue os dados do cliente para fornecer experiências eletrizantes"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="recharge-your-customer-data.md" target="_blank" rel="referrer" title="Recarregue os dados do cliente para fornecer experiências eletrizantes">Recarregue os dados do cliente para fornecer experiências eletrizantes</a>
                    </p>
                    <p class="is-size-6">Saiba como reduzir o impacto de dados de baixa qualidade, reduzir o tempo de implantação e multiplicar o ROI usando os mesmos dados para uma variedade de casos de uso.</p>
                </div>
                <a href="recharge-your-customer-data.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Saiba mais</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->
