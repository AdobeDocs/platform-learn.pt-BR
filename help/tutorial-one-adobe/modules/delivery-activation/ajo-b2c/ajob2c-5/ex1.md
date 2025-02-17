---
title: Introdução aos Serviços de tradução da AJO
description: Introdução aos Serviços de tradução da AJO
kt: 5342
doc-type: tutorial
exl-id: ec032c58-c5c2-48d2-bdd3-ff860bc4a35a
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# 3.5.1 Provedor de traduções

## 3.5.1.1 Configurar o Microsoft Azure Translator

Ir para [https://portal.azure.com/#home](https://portal.azure.com/#home).

![Traduções](./images/transl1.png)

Na barra de pesquisa, digite `translators`. Em seguida, clique em **+ Criar**.

![Traduções](./images/transl2.png)

Selecione **Criar Tradutor**.

![Traduções](./images/transl3.png)

Escolha sua **ID de Assinatura** e o **Grupo de Recursos**.
Defina **Região** como **Global**.
Definir **Camada de Preços** como **F0** Gratuito.

Selecione **Revisar + criar**.

![Traduções](./images/transl4.png)

Selecione **Criar**.

![Traduções](./images/transl5.png)

Selecione **Ir para o recurso**.

![Traduções](./images/transl6.png)

No menu esquerdo, vá para **Gerenciamento de Recursos** > **Chaves e Ponto de Extremidade**. Clique em para copiar a chave.

![Traduções](./images/transl7.png)

## 3.5.1.2 Dicionário de localidade

Ir para [https://experience.adobe.com/](https://experience.adobe.com/). Clique em **Journey Optimizer**.

![Traduções](./images/ajolp1.png)

No menu esquerdo, vá para **Traduções** e, em seguida, vá para **Dicionário da localidade**. Se você vir esta mensagem, clique em **Adicionar Localidades Padrão**.

![Traduções](./images/locale1.png)

Você deverá ver isso.

![Traduções](./images/locale2.png)

## 3.5.1.3 Configurar o provedor de traduções no AJO

Ir para [https://experience.adobe.com/](https://experience.adobe.com/). Clique em **Journey Optimizer**.

![Traduções](./images/ajolp1.png)

No menu esquerdo, vá para **Traduções** e vá para **Provedores**. Clique em **Adicionar Provedor**.

![Traduções](./images/transl8.png)

Em **Provedores**, selecione **Microsoft Translator**. Marque a caixa de seleção para habilitar o uso do provedor de tradução. Cole a chave copiada dos Tradutores do Microsoft Azure. Em seguida, clique em **Validar credenciais**.

![Traduções](./images/transl9.png)

Suas credenciais devem ser validadas com êxito. Se estiverem, role para baixo para selecionar os idiomas para tradução.

![Traduções](./images/transl10.png)

Selecione `[en-US] English`, `[es] Spanish`, `[fr] French`, `[nl] Dutch`.

![Traduções](./images/transl11.png)

Role para cima e clique em **Salvar**.

![Traduções](./images/transl12.png)

Seu **Provedor de Traduções** está pronto para ser usado.

![Traduções](./images/transl13.png)

## 3.5.1.4 Configurar projeto de traduções

Ir para [https://experience.adobe.com/](https://experience.adobe.com/). Clique em **Journey Optimizer**.

![Traduções](./images/ajolp1.png)

No menu esquerdo, vá para **Traduções** e, em seguida, vá para **Dicionário da localidade**. Se você vir esta mensagem, clique em **Criar projeto**.

![Traduções](./images/ajoprovider1.png)

Insira o nome `--aepUserLdap-- - Translations`, defina a **Localidade do Source** como `[en-US] English - United States` e marque as caixas de seleção para habilitar **Publicar automaticamente traduções aprovadas** e **Habilitar fluxo de trabalho de revisão**. Em seguida, clique em **+ Adicionar uma localidade**.

![Traduções](./images/ajoprovider1a.png)

Pesquise por `fr`, habilite a caixa de seleção para `[fr] French` e habilite a caixa de seleção para **Microsoft Translator**. Clique em **+ Adicionar uma localidade**.

![Traduções](./images/ajoprovider2.png)

Pesquise por `es`, habilite a caixa de seleção para `[es] Spanish` e habilite a caixa de seleção para **Microsoft Translator**. Clique em **+ Adicionar uma localidade**.

![Traduções](./images/ajoprovider3.png)

Pesquise por `nl`, habilite a caixa de seleção para `[nl] Spanish` e habilite a caixa de seleção para **Microsoft Translator**. Clique em **+ Adicionar uma localidade**.

![Traduções](./images/ajoprovider6.png)

Clique em **Salvar**.

![Traduções](./images/ajoprovider8.png)

Seu projeto **Traduções** está pronto para ser usado.

![Traduções](./images/ajoprovider9.png)

## 3.5.1.5 Definir configurações de idioma

Vá para **Canais** > **Configurações Gerais** > **Configurações de Idioma**. Clique em **Criar configurações de idioma**.

![Journey Optimizer](./images/camploc6.png)

Use o nome `--aepUserLdap--_translations`. Selecione **Projeto de tradução**. Clique no ícone **editar**.

![Journey Optimizer](./images/camploc7.png)

Selecione o Projeto de traduções criado na etapa anterior. Clique em **Selecionar**.

![Journey Optimizer](./images/camploc8.png)

Você deverá ver isso. Defina a **preferência de Fallback** para **Inglês - Estados Unidos**. Clique para selecionar **Selecionar atributo preferencial do idioma do perfil**, que decidirá qual campo do perfil de cliente usar para carregar as traduções. Em seguida, clique no ícone **editar** para selecionar qual campo será usado.

![Journey Optimizer](./images/camploc9.png)

Digite o **idioma preferencial** na barra de pesquisa e selecione o campo **Idioma preferencial**.

![Journey Optimizer](./images/camploc10.png)

Clique no ícone **editar** de **inglês - Estados Unidos** e **holandês** para examinar sua configuração.

![Journey Optimizer](./images/camploc11.png)

Esta é a configuração de **inglês - Estados Unidos**. Clique em **Cancelar**.

![Journey Optimizer](./images/camploc12.png)

Clique para exibir a configuração de **Holandês**. Clique em **Cancelar**.

![Journey Optimizer](./images/camploc13.png)

Role para cima e clique em **Enviar**.

![Journey Optimizer](./images/camploc14.png)

As configurações de idioma estão definidas agora.

![Journey Optimizer](./images/camploc15.png)

Você concluiu este exercício.

## Próximas etapas

Ir para [3.5.2 Criar sua campanha](./ex2.md)

Voltar para [Adobe Journey Optimizer: Serviços de Tradução](./ajotranslationsvcs.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
