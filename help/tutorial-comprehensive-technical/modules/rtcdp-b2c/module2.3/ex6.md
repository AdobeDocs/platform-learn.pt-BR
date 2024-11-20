---
title: Real-time CDP - Públicos-alvo externos
description: Real-time CDP - Públicos-alvo externos
kt: 5342
doc-type: tutorial
exl-id: c7e4960f-4007-4c27-b5ba-7b21cd52c2f7
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '1950'
ht-degree: 1%

---

# 2.3.6 Públicos-alvo externos

Em muitos casos, sua empresa pode querer usar públicos-alvo existentes de outros aplicativos para aprimorar o perfil do cliente no Adobe Experience Platform.
Esses públicos-alvo externos podem ter sido definidos com base em um modelo de ciência de dados ou usando plataformas de dados externas.

O recurso de públicos-alvo externos do Adobe Experience Platform permite que você se concentre na assimilação dos públicos-alvo externos e sua ativação sem precisar redefinir a definição de público-alvo correspondente em detalhes no Adobe Experience Platform.

O processo global divide-se em três etapas principais:

- Importar os metadados do público-alvo externo: esta etapa destina-se a assimilar os metadados do público-alvo externo, como o nome do público-alvo, na Adobe Experience Platform.
- Atribuir a associação de público-alvo externo ao perfil do cliente: essa etapa destina-se a enriquecer o perfil do cliente com o atributo de associação de públicos-alvo externos.
- Criar os públicos no Adobe Experience Platform: esta etapa destina-se a criar públicos acionáveis com base na associação de públicos externos.

## Metadados

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/home.png)

>[!IMPORTANT]
>
>A sandbox a ser usada para este exercício é ``--aepSandboxName--``!

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepSandboxName--``. Depois de selecionar a [!UICONTROL sandbox] apropriada, você verá a alteração da tela e agora estará na [!UICONTROL sandbox] dedicada.

![Assimilação de dados](./images/sb1.png)

Embora os dados do público-alvo definam a condição para que um perfil faça parte de um público-alvo, os metadados do público-alvo são informações sobre o público-alvo, como o nome, a descrição e o status do público-alvo. Como os metadados dos públicos externos serão armazenados no Adobe Experience Platform, é necessário usar um namespace de identidade para assimilar os metadados no Adobe Experience Platform.

## 2.3.6.1.1 Namespace de identidade para públicos-alvo externos

Um namespace de identidade já foi criado para uso com **Públicos-alvo externos**.
Para exibir a identidade já criada, vá para **Identidades** e pesquise por **Externas**. Clique no item &quot;Públicos externos&quot;.

Observe que:

- O símbolo de identidade **externalaudiences** será usado nas próximas etapas para fazer referência à identidade dos públicos externos.
- O tipo **Identificador não pessoal** é usado para este namespace de identidade, pois ele não se destina a identificar perfis de clientes, mas públicos.

![Identidade de Públicos Externos](images/extAudIdNS.png)

## 2.3.6.1.2 Criar o esquema de metadados de públicos externos

Os metadados dos públicos externos são baseados no **Esquema de definição de público**. Você pode encontrar mais detalhes no [repositório GitHub XDM](https://github.com/adobe/xdm/blob/master/docs/reference/classes/segmentdefinition.schema.md).

No menu esquerdo, vá para Schemas. Clique em **+ Criar Esquema** e em **Procurar**.

![Esquema de metadados de públicos-alvo externos 1](images/extAudMDXDM1.png)

Para atribuir uma classe, procure por **definição de público-alvo**. Selecione a classe **Definição de público** e clique em **Atribuir classe**.

![Esquema de metadados de públicos-alvo externos 2](images/extAudMDXDM2.png)

Você verá isso. Clique em **Cancelar**.

![Esquema de metadados de públicos externos 3](images/extAudMDXDM3.png)

Você verá isso. Selecione o campo **_id**. No menu direito, role para baixo e habilite as caixas de seleção **Identidade** e **Identidade principal**. Selecione o namespace de identidade **Públicos-alvo externos**. Clique em **Aplicar**.

![Esquema de metadados de públicos externos 4](images/extAudMDXDM4.png)

Em seguida, selecione o nome do esquema **Esquema sem título**. Altere o nome para `--aepUserLdap-- - External Audiences Metadata`.

![Esquema de metadados de públicos-alvo externos 5](images/extAudMDXDM5.png)

Habilite a opção de alternância **Perfil** e confirme. Finalmente, clique em **Salvar**.

![Esquema de metadados de públicos-alvo externos 5](images/extAudMDXDM6.png)

## 2.3.6.1.3 Criar o conjunto de dados de metadados de públicos externos

Em **Esquemas**, vá para **Procurar**. Pesquise e clique no esquema `--aepUserLdap-- - External Audiences Metadata` criado na etapa anterior. Em seguida, clique em **Criar conjunto de dados a partir do esquema**.

![Metadados de públicos externos DS 1](images/extAudMDDS1.png)

Para o campo **Nome**, digite `--aepUserLdap-- - External Audience Metadata`. Clique em **Criar conjunto de dados**.

![Metadados de Públicos Externos DS 2](images/extAudMDDS2.png)

Você verá isso. Não esqueça de habilitar a opção de alternância **Perfil**!

![Metadados de Públicos Externos DS 3](images/extAudMDDS3.png)

## 2.3.6.1.4 Criar uma conexão HTTP API Source

Em seguida, é necessário configurar o HTTP API Source Connector, que será usado para assimilar os metadados no conjunto de dados.

Ir para **Fontes**. No campo de pesquisa, digite **HTTP**. Clique em **Adicionar dados**.

![Metadados de públicos externos http 1](images/extAudMDhttp1.png)

Insira a seguinte informação:

- **Tipo de conta**: selecione **Nova conta**
- **Nome da conta**: digite `--aepUserLdap-- - External Audience Metadata`
- Marque a caixa de seleção **caixa compatível com XDM**

Em seguida, clique em **Conectar à origem**.

![Metadados de Públicos Externos http 2](images/extAudMDhttp2.png)

Você verá isso. Clique em **Next**.

![Metadados de Públicos Externos http 2](images/extAudMDhttp2a.png)

Selecione **Conjunto de dados existente** e, no menu suspenso, procure e selecione o conjunto de dados `--aepUserLdap-- - External Audience Metadata`.

Verifique os **detalhes do fluxo de dados** e clique em **Avançar**.

![Metadados de públicos externos http 3](images/extAudMDhttp3.png)

Você verá isso.

A etapa **Mapeamento** do assistente está vazia, pois você assimilará uma carga compatível com XDM no Conector Source da API HTTP e, portanto, nenhum mapeamento é necessário. Clique em **Next**.

![Metadados de públicos externos http 3](images/extAudMDhttp3a.png)

Na etapa **Revisão**, é possível revisar opcionalmente a conexão e os detalhes do mapeamento. Clique em **Concluir**.

![Metadados de Públicos Externos http 4](images/extAudMDhttp4.png)

Você verá isso.

![Metadados de Públicos Externos http 4](images/extAudMDhttp4a.png)

## 2.3.6.1.5 Assimilação de metadados de públicos externos

Na guia de visão geral do Source Connector, clique em **...** e em **Copiar carga do esquema**.

![Metadados de públicos externos str 1](images/extAudMDstr1a.png)

Abra o aplicativo Editor de texto no computador e cole a carga que você acabou de copiar, que se parece com isto. Em seguida, você precisa atualizar o objeto **xdmEntity** nesta carga.

![Metadados de públicos externos str 1](images/extAudMDstr1b.png)

O objeto **xdmEntity** precisa ser substituído pelo código abaixo. Copie o código abaixo e cole-o no arquivo de texto substituindo o objeto **xdmEntity** no editor de texto.

```
"xdmEntity": {
    "_id": "--aepUserLdap---extaudience-01",
    "description": "--aepUserLdap---extaudience-01 description",
    "segmentIdentity": {
      "_id": "--aepUserLdap---extaudience-01",
      "namespace": {
        "code": "externalaudiences"
      }
    },
    "segmentName": "--aepUserLdap---extaudience-01 name",
    "segmentStatus": "ACTIVE",
    "version": "1.0"
  }
```

Você deverá ver isso:

![Metadados de públicos externos str 1](images/extAudMDstr1.png)

Em seguida, abra uma nova janela **Terminal**. Copie todo o texto no Editor de texto e cole-o na janela do terminal.

![Metadados de públicos externos str 1](images/extAudMDstr1d.png)

Em seguida, clique em **Enter**.

Você verá uma confirmação da assimilação de dados na janela Terminal:

![Metadados de públicos externos str 1](images/extAudMDstr1e.png)

Atualize a tela do conector HTTP API Source, onde agora você verá que os dados estão sendo processados:

![Metadados de públicos externos str 2](images/extAudMDstr2.png)

## 2.3.6.1.6 Validar assimilação de metadados de públicos externos

Quando o processamento estiver concluído, você poderá verificar a disponibilidade dos dados no conjunto de dados usando o Serviço de consulta.

No menu direito, vá para **Conjuntos de Dados** e selecione o conjunto de dados `--aepUserLdap-- - External Audience Metadata` criado anteriormente.

![Metadados de públicos externos str 3](images/extAudMDstr3.png)

No menu direito, vá para Consultas e clique em **Criar consulta**.

![Metadados de públicos externos str 4](images/extAudMDstr4.png)

Insira o código a seguir e pressione **SHIFT + ENTER**:

```
select * from --aepUserLdap--_external_audience_metadata
```

Nos resultados da consulta, você verá os metadados do público-alvo externo que você assimilou.

![Metadados de públicos externos str 5](images/extAudMDstr5.png)

## Associação de público

Com os metadados de público-alvo externo disponíveis, agora é possível assimilar a associação de público-alvo de um perfil de cliente específico.

Agora é necessário preparar um conjunto de dados de perfil enriquecido com o esquema de associação de público-alvo. Você pode encontrar mais detalhes no [repositório GitHub XDM](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/segmentmembership.schema.md).

### Criar o esquema de associação de públicos externos

No menu direito, vá para **Esquemas**. Clique em **Criar esquema** e em **Perfil Individual XDM**.

![Esquema 1](images/extAudPrXDM1.png) do Perfil de Públicos-Alvo Externos

No pop-up **Adicionar grupos de campos**, pesquise por **Núcleo do Perfil**. Selecione o grupo de campos **Núcleo do Perfil v2**.

![Esquema 2](images/extAudPrXDM2.png) do Perfil de Públicos Externos

Em seguida, no pop-up **Adicionar grupos de campos**, pesquise por **Associação de segmento**. Selecione o grupo de campos **Detalhes da associação do segmento**. Em seguida, clique em **Adicionar grupos de campos**.

![Esquema 3](images/extAudPrXDM3.png) do Perfil de Públicos-Alvo Externos

Você verá isso. Navegue até o campo `--aepTenantId--.identification.core`. Clique no campo **crmId**. No menu direito, role para baixo e marque as caixas de seleção **Identidade** e **Identidade principal**. Para o **Namespace de Identidade**, selecione **Sistema de Demonstração - CRMID**.

Clique em **Aplicar**.

![Esquema 4](images/extAudPrXDM4.png) do Perfil de Públicos Externos

Em seguida, selecione o Nome do esquema **Esquema sem título**. No campo nome para exibição, digite `--aepUserLdap-- - External Audiences Membership`.

![Esquema 5](images/extAudPrXDM5a.png) do Perfil de Públicos Externos

Em seguida, habilite a opção de alternância **Perfil** e confirme. Clique em **Salvar**.

![Esquema 5](images/extAudPrXDM5.png) do Perfil de Públicos Externos

### Criar o conjunto de dados de associação de públicos externos

Em **Esquemas**, vá para **Procurar**. Pesquise e clique no esquema `--aepUserLdap-- - External Audiences Membership` criado na etapa anterior. Em seguida, clique em **Criar conjunto de dados a partir do esquema**.

![Metadados de públicos externos DS 1](images/extAudPrDS1.png)

Para o campo **Nome**, digite `--aepUserLdap-- - External Audiences Membership`. Clique em **Criar conjunto de dados**.

![Metadados de Públicos Externos DS 2](images/extAudPrDS2.png)

Você verá isso. Não esqueça de habilitar a opção de alternância **Perfil**!

![Metadados de Públicos Externos DS 3](images/extAudPrDS3.png)

### Criar uma conexão HTTP API Source


Em seguida, é necessário configurar o HTTP API Source Connector, que será usado para assimilar os metadados no conjunto de dados.

Ir para **Fontes**. No campo de pesquisa, digite **HTTP**. Clique em **Adicionar dados**.

![Metadados de públicos externos http 1](images/extAudMDhttp1.png)

Insira a seguinte informação:

- **Tipo de conta**: selecione **Nova conta**
- **Nome da conta**: digite `--aepUserLdap-- - External Audience Membership`
- Marque a caixa de seleção **caixa compatível com XDM**

Em seguida, clique em **Conectar à origem**.

![Metadados de Públicos Externos http 2](images/extAudPrhttp2.png)

Você verá isso. Clique em **Next**.

![Metadados de Públicos Externos http 2](images/extAudPrhttp2a.png)

Selecione **Conjunto de dados existente** e, no menu suspenso, procure e selecione o conjunto de dados `--aepUserLdap-- - External Audiences Membership`.

Verifique os **detalhes do fluxo de dados** e clique em **Avançar**.

![Metadados de públicos externos http 3](images/extAudPrhttp3.png)

Você verá isso.

A etapa **Mapeamento** do assistente está vazia, pois você assimilará uma carga compatível com XDM no Conector Source da API HTTP e, portanto, nenhum mapeamento é necessário. Clique em **Next**.

![Metadados de públicos externos http 3](images/extAudPrhttp3a.png)

Na etapa **Revisão**, é possível revisar opcionalmente a conexão e os detalhes do mapeamento. Clique em **Concluir**.

![Metadados de Públicos Externos http 4](images/extAudPrhttp4.png)

Você verá isso.

![Metadados de Públicos Externos http 4](images/extAudPrhttp4a.png)

### Assimilação de dados de associação de públicos externos

Na guia de visão geral do Source Connector, clique em **...** e em **Copiar carga do esquema**.

![Metadados de públicos externos str 1](./images/extAudPrstr1a.png)

Abra o aplicativo Editor de texto no computador e cole a carga que você acabou de copiar, que se parece com isto. Em seguida, você precisa atualizar o objeto **xdmEntity** nesta carga.

![Metadados de públicos externos str 1](images/extAudPrstr1b.png)

O objeto **xdmEntity** precisa ser substituído pelo código abaixo. Copie o código abaixo e cole-o no arquivo de texto substituindo o objeto **xdmEntity** no editor de texto.

```
  "xdmEntity": {
    "_id": "--aepUserLdap---profile-test-01",
    "_experienceplatform": {
      "identification": {
        "core": {
          "crmId": "--aepUserLdap---profile-test-01"
        }
      }
    },
    "personID": "--aepUserLdap---profile-test-01",
    "segmentMembership": {
      "externalaudiences": {
        "--aepUserLdap---extaudience-01": {
          "status": "realized",
          "lastQualificationTime": "2022-03-05T00:00:00Z"
        }
      }
    }
  }
```

Você deverá ver isso:

![Metadados de públicos externos str 1](images/extAudPrstr1.png)

Em seguida, abra uma nova janela **Terminal**. Copie todo o texto no Editor de texto e cole-o na janela do terminal.

![Metadados de públicos externos str 1](images/extAudPrstr1d.png)

Em seguida, clique em **Enter**.

Você verá uma confirmação da assimilação de dados na janela Terminal:

![Metadados de públicos externos str 1](images/extAudPrstr1e.png)

Atualize a tela do conector HTTP API Source, onde, após alguns minutos, você verá que os dados estão sendo processados:

![Metadados de públicos externos str 2](images/extAudPrstr2.png)

### Validar assimilação de associação de públicos externos

Quando o processamento estiver concluído, você poderá verificar a disponibilidade dos dados no conjunto de dados usando o Serviço de consulta.

No menu direito, vá para **Conjuntos de Dados** e selecione o conjunto de dados `--aepUserLdap-- - External Audiences Membership ` criado anteriormente.

![Metadados de públicos externos str 3](images/extAudPrstr3.png)

No menu direito, vá para Consultas e clique em **Criar consulta**.

![Metadados de públicos externos str 4](images/extAudPrstr4.png)

Insira o código a seguir e pressione **SHIFT + ENTER**:

```
select * from --aepUserLdap--_external_audiences_membership
```

Nos resultados da consulta, você verá os metadados do público-alvo externo que você assimilou.

![Metadados de públicos externos str 5](images/extAudPrstr5.png)

## Criar um segmento

Agora você está pronto para executar ações nos públicos externos.
No Adobe Experience Platform, a ação é alcançada por meio da criação de segmentos, preenchimento dos respectivos públicos e compartilhamento desses públicos para os destinos.
Agora você criará um segmento usando o público-alvo externo que acabou de criar.

No menu esquerdo, vá para **Segmentos** e clique em **Criar segmento**.

![SegBuilder 1](images/extAudSegUI2.png) de Públicos-alvo externos

Ir para **Públicos-alvo**. Você verá isso. Clique em **Públicos-alvo externos**.

![SegBuilder 1](images/extAudSegUI2a.png) de Públicos-alvo externos

Selecione o público externo que você criou anteriormente, chamado `--aepUserLdap---extaudience-01`. Arraste e solte o público-alvo na tela.

![SegBuilder 1](images/extAudSegUI2b.png) de Públicos-alvo externos

Dê um nome ao seu segmento, use `--aepUserLdap-- - extaudience-01`. Clique em **Salvar e fechar**.

![SegBuilder 1](images/extAudSegUI1.png) de Públicos-alvo externos

Você verá isso. Você também observará que o perfil para o qual você assimilou a associação do segmento agora é exibido na lista de **Perfis de amostra**.

![SegBuilder 1](images/extAudSegUI3.png) de Públicos-alvo externos

Seu segmento está pronto agora e pode ser enviado para um destino para ativação.

## Visualizar seu perfil de cliente

Agora, você também pode visualizar a qualificação do segmento no perfil do cliente. Vá para **Perfis**, use o namespace de identidade **Sistema de demonstração - CRMID** e forneça a identidade `--aepUserLdap---profile-test-01`, que você usou como parte do exercício 6.6.2.4, e clique em **Exibir**. Em seguida, clique em **ID do Perfil** para abrir o perfil.

![SegBuilder 1](images/extAudProfileUI1.png) de Públicos-alvo externos

Vá para **Segmentar associação**, onde você verá seu público externo aparecer.

![SegBuilder 1](images/extAudProfileUI2.png) de Públicos-alvo externos

Próxima etapa: [2.3.7 SDK de Destinos](./ex7.md)

[Voltar ao módulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Voltar a todos os módulos](../../../overview.md)
