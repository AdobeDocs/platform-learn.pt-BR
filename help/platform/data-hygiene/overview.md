---
title: Higiene de dados no Adobe Experience Platform
description: Saiba mais sobre as opções de ferramentas de higiene de dados na Adobe Experience Platform
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
feature: Data Hygiene
role: Developer
level: Intermediate
source-git-commit: 9c15708f7300672caa963c0635179dd2855e5fed
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 22%

---

# Tutoriais de higiene de dados

Saiba mais sobre os recursos de higiene de dados do Adobe Experience Platform, que incluem:

* Ativação dos princípios de minimização de dados durante a assimilação de dados
* Ajuste de dados já existentes no sistema
* Remoção dos dados do sistema

<!--
Data hygiene:

* Enables citizen data stewards working in Privacy or IT teams to manage customer data lifecycle.
* Provides foundational workflows for setting expiration of datasets based on corporate policies, partner
arrangements, customer commitments or regulatory needs.
* Provides foundational workflows for managing targeted treatment of identities and data belonging to consumers in a
holistic fashion.
* Provides monitoring, work order management and notifications of tasks.
* Provides the ability to log the lifecyle management tasks for auditing purposes.
-->

## Minimização de dados durante a assimilação

O recurso de preparação de dados ajuda a assimilar apenas os campos necessários de uma fonte de dados.

<!-- CARDS
{cta=Watch}
* data-prep-for-data-hygiene.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Data prep for data hygiene">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="data-prep-for-data-hygiene.md" title="Preparo de dados para higiene de dados" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3429485/?format=jpeg&nocache=1740251397387" alt="Preparo de dados para higiene de dados"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="data-prep-for-data-hygiene.md" target="_blank" rel="referrer" title="Preparo de dados para higiene de dados">Preparação de dados para higiene de dados</a>
                    </p>
                    <p class="is-size-6">Saiba como oferecer suporte aos princípios de minimização de dados com o recurso de preparação de dados da Experience Platform. Saiba como assimilar somente os campos necessários e os dados de hash durante a assimilação.</p>
                </div>
                <a href="data-prep-for-data-hygiene.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Assistir</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Remoção de dados no sistema

Existem muitos recursos para ajudá-lo a remover os dados do sistema. Você pode excluir conjuntos de dados inteiros sob demanda ou de acordo com uma programação, expirar registros e perfis com configurações de tempo de vida, excluir perfis individuais e atender às solicitações de privacidade.
<!-- CARDS
{cta=Watch}
* delete-datasets-and-batches.md
* ../data-lifecycle/expire-datasets.md
* pseudonymous-profile-and-event-expiration.md
* ../profiles/delete-profiles.md{description=Learn how to delete data from the Profile Store using the Real-Time Customer Profile API. By using the Profile API, you can remove data from the profile store without affecting the data lake or identity graph.}
* ../privacy/introduction-to-privacy-services.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Delete datasets and batches">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="delete-datasets-and-batches.md" title="Excluir conjuntos de dados e lotes" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3429790/?format=jpeg&nocache=1740251397681" alt="Excluir conjuntos de dados e lotes"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="delete-datasets-and-batches.md" target="_blank" rel="referrer" title="Excluir conjuntos de dados e lotes">Excluir conjuntos de dados e lotes</a>
                    </p>
                    <p class="is-size-6">Saiba como excluir conjuntos de dados e lotes na Adobe Experience Platform.</p>
                </div>
                <a href="delete-datasets-and-batches.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Assistir</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Schedule dataset deletes">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../data-lifecycle/expire-datasets.md" title="Programar exclusões do conjunto de dados" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/345065?format=jpeg&nocache=1740251397716" alt="Programar exclusões do conjunto de dados"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../data-lifecycle/expire-datasets.md" target="_blank" rel="referrer" title="Programar exclusões do conjunto de dados">Exclusões de conjunto de dados de agendamento</a>
                    </p>
                    <p class="is-size-6">Saiba como excluir conjuntos de dados usando o recurso de higiene de dados da Adobe Experience Platform.</p>
                </div>
                <a href="../data-lifecycle/expire-datasets.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Assistir</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Pseudonymous profile and Experience Event expirations">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="pseudonymous-profile-and-event-expiration.md" title="Expirações de perfil pseudônimo e evento de experiência" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3428361?format=jpeg&nocache=1740251397705" alt="Expirações de perfil pseudônimo e evento de experiência"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="pseudonymous-profile-and-event-expiration.md" target="_blank" rel="referrer" title="Expirações de perfil pseudônimo e evento de experiência">Perfil pseudônimo e expirações de evento de experiência</a>
                    </p>
                    <p class="is-size-6">Saiba como definir configurações de expiração para perfis pseudônimos e eventos da Experience Platform e descubra os benefícios de se fazer isso.</p>
                </div>
                <a href="pseudonymous-profile-and-event-expiration.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Assistir</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Delete profiles">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../profiles/delete-profiles.md" title="Excluir perfis" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3429807/?format=jpeg&nocache=1740251397692" alt="Excluir perfis"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../profiles/delete-profiles.md" target="_blank" rel="referrer" title="Excluir perfis">Excluir perfis</a>
                    </p>
                    <p class="is-size-6">Saiba como excluir dados da Loja de perfis usando a API de perfil do cliente em tempo real. Ao usar a API de perfil, é possível remover dados do armazenamento de perfis sem afetar o data lake ou o gráfico de identidade.</p>
                </div>
                <a href="../profiles/delete-profiles.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Assistir</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Introduction to Privacy Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../privacy/introduction-to-privacy-services.md" title="Introdução ao Privacy Service" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/336074?format=jpeg&nocache=1740251397727" alt="Introdução ao Privacy Service"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../privacy/introduction-to-privacy-services.md" target="_blank" rel="referrer" title="Introdução ao Privacy Service">Introdução ao Privacy Service</a>
                    </p>
                    <p class="is-size-6">Saiba mais sobre as regulamentações de privacidade e seus efeitos nas operações de dados. Além disso, saiba como o Privacy Service lida com esses desafios.</p>
                </div>
                <a href="../privacy/introduction-to-privacy-services.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Assistir</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->





## Ajuste de dados no sistema

<!-- CARDS
{cta=Watch}
* ../profiles/update-a-specific-attribute-with-upsert.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Update specific profile attributes using `upsert`">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../profiles/update-a-specific-attribute-with-upsert.md" title="Atualizar atributos específicos do perfil usando &quot;upsert&quot;" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3416133/?format=jpeg&nocache=1740251398874" alt="Atualizar atributos específicos do perfil usando &quot;upsert&quot;"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../profiles/update-a-specific-attribute-with-upsert.md" target="_blank" rel="referrer" title="Atualizar atributos específicos do perfil usando &quot;upsert&quot;">Atualizar atributos de perfil específicos usando `upsert`</a>
                    </p>
                    <p class="is-size-6">Saiba como atualizar um atributo específico de um perfil usando o recurso "substituir" do Adobe Experience Platform.</p>
                </div>
                <a href="../profiles/update-a-specific-attribute-with-upsert.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Assistir</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->
