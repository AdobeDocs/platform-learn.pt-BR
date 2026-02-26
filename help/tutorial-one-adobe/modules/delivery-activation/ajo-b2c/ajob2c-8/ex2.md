---
title: Criar sua campanha orquestrada
description: Criar sua campanha orquestrada
kt: 5342
doc-type: tutorial
exl-id: f3ca3230-db30-4e41-91f1-9324b12211a6
source-git-commit: 0328260e8699107bc82103af98caae684319a60d
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 2%

---

# 3.8.2 Criar sua campanha orquestrada

## 3.8.2.1 Crie sua campanha orquestrada

Vá para **Campanhas**. Clique em **Criar campanha**.

![OC do AJO](./images/ajooc1.png)

Selecione **Orquestração - Marketing** e clique em **Confirmar**.

![OC do AJO](./images/ajooc2.png)

Insira o nome da campanha: `--aepUserLdap-- - CitiSignal Family Account Optimization Campaign` e clique em **Salvar**.

![OC do AJO](./images/ajooc3.png)

Você deverá ver isso. Clique no ícone **+**.

![OC do AJO](./images/ajooc4.png)

Selecione **Bifurcação**.

![OC do AJO](./images/ajooc5.png)

### Criar público-alvo 1

Clique no ícone **+** e selecione **Criar público-alvo**.

![OC do AJO](./images/ajooc6.png)

Clique para abrir a pasta para **Targeting dimension**.

![OC do AJO](./images/ajooc7.png)

Selecione **`--aepUserLdap--_citisignal_recipients`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc8.png)

Clique em **Criar audiência**.

![OC do AJO](./images/ajooc9.png)

Clique em **Adicionar condição**.

![OC do AJO](./images/ajooc10.png)

Selecione **recipient_type** e clique em **Confirmar**.

![OC do AJO](./images/ajooc11.png)

Insira **`account_holder`** no campo **Valor** e clique em **Calcular**.

![OC do AJO](./images/ajooc12.png)

Você deverá ver um número para **perfis segmentados**. Clique em algum lugar na área cinza conforme indicado.

![OC do AJO](./images/ajooc13.png)

Clique em **Adicionar condição**.

![OC do AJO](./images/ajooc14.png)

Detalhar até **`citisignal_accounts`**.

![OC do AJO](./images/ajooc15.png)

Selecione **`account_status`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc16.png)

Digite **`active`** no campo **Valor**. Em seguida, clique em algum lugar na área cinza, conforme indicado.

![OC do AJO](./images/ajooc17.png)

Clique em **Adicionar condição**.

![OC do AJO](./images/ajooc18.png)

Detalhar até **`citisignal_mobile_subscriptions`**.

![OC do AJO](./images/ajooc19.png)

Selecione **`subscription_id`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc20.png)

Habilite o alternador para **Dados agregados**. Em seguida, selecione o seguinte:

- **Função de agregação**: **Contagem**
- **Operador**: **maior que ou igual a**
- **Valor**: **1**

Clique em **Confirmar**.

![OC do AJO](./images/ajooc21.png)

Você deverá ver isso. Clique em **Confirmar**.

![OC do AJO](./images/ajooc22.png)

### Criar público-alvo 2

Clique no ícone **+** no próximo nó do outro caminho.

![OC do AJO](./images/ajooc23.png)

Selecione **Criar audiência**.

![OC do AJO](./images/ajooc24.png)

Clique para abrir a pasta para **Targeting dimension**.

![OC do AJO](./images/ajooc25.png)

Selecione **`--aepUserLdap--_mobile_subscriptions`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc26.png)

Clique em **Criar audiência**.

![OC do AJO](./images/ajooc27.png)

Clique em **Adicionar condição**.

![OC do AJO](./images/ajooc28.png)

Selecione **subscription_status** e clique em **Confirmar**.

![OC do AJO](./images/ajooc29.png)

Digite **`active`** no campo **Valor**. Clique em **Adicionar condição**.

![OC do AJO](./images/ajooc30.png)

Selecione **`is_upgrade_eligible`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc31.png)

Definir o **Valor** como **true**

![OC do AJO](./images/ajooc32.png)

Clique em **Calcular** para ver uma estimativa dos perfis qualificados para este público-alvo. Em seguida, clique em **Confirmar**

![OC do AJO](./images/ajooc33.png)

### Divisão

Clique no ícone **+** e selecione **Split**.

![OC do AJO](./images/ajooc34.png)

Altere o campo **Rótulo** para **90/10 Tratamento vs Controle**. Clique para abrir o objeto **Subconjunto**.

![OC do AJO](./images/ajooc35.png)

Habilite o alternador para **Habilitar limite** e defina o **Tamanho do limite** como **10 por cento**.

![OC do AJO](./images/ajooc36.png)

Clique em **Adicionar segmento** e você deverá ver o objeto **Resultado** sendo adicionado.

Clique em **Salvar**.

![OC do AJO](./images/ajooc37.png)

### Salvar público-alvo

Clique no ícone **+** e selecione **Salvar público-alvo**.

![OC do AJO](./images/ajooc38.png)

Defina o campo **Rótulo do público-alvo** como **`--aepUserLdap-- - Control Group`**. Clique em **Adicionar mapeamento de público-alvo**.

![OC do AJO](./images/ajooc39.png)

Detalhe até **targeting dimension**.

![OC do AJO](./images/ajooc40.png)

Selecione **`account_id`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc41.png)

Defina o **Campo de mapeamento de perfil** como **`--aepUserLdap--_citisignal_recipients - account_id`**.

![OC do AJO](./images/ajooc41a.png)

### Enriquecimento: Assinatura da Internet

Clique no ícone **+**.

![OC do AJO](./images/ajooc42.png)

Selecione **Enriquecimento**.

![OC do AJO](./images/ajooc43.png)

Você deverá ver isso. Clique em **Adicionar dados de enriquecimento**.

![OC do AJO](./images/ajooc44.png)

Detalhar até **`Targeting dimension`**.

![OC do AJO](./images/ajooc44a.png)

Detalhar até **`citisignal_accounts`**.

![OC do AJO](./images/ajooc45.png)

Detalhar até **`citisignal_internet_subscriptions`**.

![OC do AJO](./images/ajooc45a.png)

Selecione **`account_id`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc46.png)

Você deverá ver isso. Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc47.png)

Selecione **`subscription_status`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc48.png)

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc49.png)

Selecione **`connection_type`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc50.png)

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc51.png)

Selecione **`service_city`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc52.png)

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc53.png)

Selecione **`avg_bandwidth_usage_gb`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc54.png)

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc55.png)

Selecione **`data_cap_gb`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc56.png)

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc57.png)

Selecione **`advertised_speed_mbps`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc58.png)

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc59.png)

Selecione **`monthly_recurring_charge`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc60.png)

Clique em **Salvar**.

![OC do AJO](./images/ajooc61.png)

Role para cima e altere o campo **Rótulo** para `Enrichment: Internet Subscription`.

![OC do AJO](./images/ajooc61a.png)

### Enriquecimento: assinatura de dispositivos móveis

Clique no ícone **+** no próximo nó e selecione **Enriquecimento**.

![OC do AJO](./images/ajooc62.png)

Altere o campo **Etiqueta** para `Enrichment: Mobile Devices Subscription` e clique em **Adicionar dados de enriquecimento**.

![OC do AJO](./images/ajooc63.png)

Detalhe até **Targeting dimension**.

![OC do AJO](./images/ajooc64.png)

Detalhar até **`citisignal_accounts`**.

![OC do AJO](./images/ajooc65.png)

Detalhar até **`citisignal_mobile_subscriptions`**.

![OC do AJO](./images/ajooc65a.png)

Selecione **`phone_number`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc66.png)

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc67.png)

Detalhar até **`citisignal_equipment_subscriptions`**.

![OC do AJO](./images/ajooc68.png)

Selecione **`model`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc68a.png)

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc69.png)

Detalhar até **`citisignal_equipment_subscriptions`**.

![OC do AJO](./images/ajooc69a.png)

Selecione **`recommended_device_model`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc70.png)

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc71.png)

Detalhar até **`citisignal_equipment_subscriptions`**.

![OC do AJO](./images/ajooc71a.png)

Selecione **`is_upgrade_eligible`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc72.png)

Agora é possível testar o progresso fazendo uma execução de teste e ver quais dados estão disponíveis em sua campanha.

Salve as alterações e clique em **Iniciar**.

![OC do AJO](./images/ajooctest1.png)

Depois de algum tempo, você deverá ver isso. Clique em **Visualizar resultados**.

![OC do AJO](./images/ajooctest2.png)

Você verá algo semelhante a isso. Clique em **Fechar**.

![OC do AJO](./images/ajooctest3.png)

Volte para o nó **Enriquecimento: Assinatura de Dispositivos Móveis**.

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc73.png)

Selecione **`account_id`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc74.png)

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc75.png)

Selecione **`subscription_id`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc76.png)

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc77.png)

Selecione **`renewal_eligibility_date`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc78.png)

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc79.png)

Selecione **`line_user_recipient_id`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc80.png)

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc81.png)

Selecione **`current_device_id`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc82.png)

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc86.png)

Selecione **`contract_start_date`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc87.png)

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc89.png)

Detalhar até **`citisignal_equipment_subscriptions`**.

![OC do AJO](./images/ajooc90.png)

Selecione **`manufacturer`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc91.png)

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc92.png)

Detalhar até **`citisignal_equipment_subscriptions`**.

![OC do AJO](./images/ajooc93.png)

Selecione **`device_age_months`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc94.png)

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc95.png)

Detalhar até **`citisignal_equipment_subscriptions`**.

![OC do AJO](./images/ajooc96.png)

Selecione **`trade_in_value`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc97.png)

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc98.png)

Detalhar até **`citisignal_equipment_subscriptions`**.

![OC do AJO](./images/ajooc99.png)

Selecione **`monthly_payment`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc100.png)

### Enriquecimento: assinatura de dispositivos móveis

Você deveria ficar com isso. Clique em **Salvar**. Em seguida, clique no ícone **+** para adicionar um novo nó e selecione **Enriquecimento**.

![OC do AJO](./images/ajooc101.png)

Você deverá ver isso. Clique em **Adicionar dados de enriquecimento**.

![OC do AJO](./images/ajooc102.png)

Detalhe até **Targeting dimension**.

![OC do AJO](./images/ajooc103.png)

Detalhar até **`citisignal_offer_eligibility`**.

![OC do AJO](./images/ajooc104.png)

Detalhar até **`citisignal_offers`**.

![OC do AJO](./images/ajooc105.png)

Selecione **`offer_name`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc106.png)

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc107.png)

Detalhar até **`citisignal_offers`**.

![OC do AJO](./images/ajooc108.png)

Selecione **`offer_code`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc109.png)

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc110.png)

Detalhar até **`citisignal_offers`**.

![OC do AJO](./images/ajooc111.png)

Selecione **`offer_description`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc112.png)

Clique em **Adicionar atributo**.

![OC do AJO](./images/ajooc110.png)

Detalhar até **`citisignal_offers`**.

![OC do AJO](./images/ajooc113.png)

Selecione **`offer_description`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc114.png)

Ativar **Habilitar classificação**.

![OC do AJO](./images/ajooc115.png)

Detalhar até **`citisignal_offers`**.

![OC do AJO](./images/ajooc116.png)

Selecione **`offer_priority`** e clique em **Confirmar**.

![OC do AJO](./images/ajooc117.png)

Agora você pode testar sua campanha. Clique em **Iniciar**.

![OC do AJO](./images/ajooc118.png)

Depois de algum tempo você deve ver isso. Clique em **Resultado** e selecione **Visualizar resultados**.

![OC do AJO](./images/ajooc120.png)

Você verá algo semelhante a isso.

![OC do AJO](./images/ajooc121.png)

### Atividade de email

Clique no ícone **+** e selecione **Email**.

![OC do AJO](./images/ajooc122.png)

Clique em **Editar email**.

![OC do AJO](./images/ajooc123.png)

Ir para **Ações**.

![OC do AJO](./images/ajooc124.png)

Selecione a **Configuração do canal de email** criada anteriormente e clique em **Editar conteúdo**.

![OC do AJO](./images/ajooc125.png)

Para a **Linha de assunto**, cole isto:

`{{target.--aepUserLdap--_citisignal_recipients.first_name}}, Your CitiSignal Family Account Summary`

Clique em **Editar corpo do email**.

![OC do AJO](./images/ajooc126.png)

## Próximas etapas

Voltar para [Adobe Journey Optimizer: Campanhas orquestradas](./ajocampaigns.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
