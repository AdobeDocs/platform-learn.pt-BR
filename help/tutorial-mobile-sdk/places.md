---
title: Usar o Places com o SDK móvel da plataforma
description: Saiba como usar o serviço de geolocalização do Places no aplicativo móvel.
exl-id: adc2952f-cb01-4e06-9629-49fb95f22ca5
source-git-commit: 87477cce0f0c5c0bb140927bed22dbc6e11f2af9
workflow-type: tm+mt
source-wordcount: '1696'
ht-degree: 3%

---

# Usar locais

Saiba como usar o serviço de geolocalização do Places em seu aplicativo.

O Serviço de locais de coleta de dados da Adobe Experience Platform é um serviço de geolocalização que permite que aplicativos móveis com percepção de localização compreendam o contexto de localização. O serviço está usando interfaces SDK avançadas e fáceis de usar acompanhadas por um banco de dados flexível de pontos de interesse (POIs).

## Pré-requisitos

* Todas as dependências de pacote estão em vigor no projeto Xcode.
* Extensões registradas no AppDelegate.
* MobileCore configurado para usar appId de desenvolvimento.
* SDKs importados.
* O aplicativo foi criado e executado com sucesso com as alterações acima.

## Objetivos de aprendizagem

Nesta lição, você

* Entenda como definir pontos de interesse no serviço Places.
* Atualize a propriedade da tag com a extensão Places.
* Atualize seu esquema para capturar eventos de localização geográfica.
* Valide a configuração no Assurance.
* Atualize seu aplicativo para registrar a extensão Places.
* Implemente o rastreamento de localização geográfica do serviço Places em seu aplicativo.


## Configuração

Para que o serviço Places funcione no aplicativo e no SDK móvel, é necessário fazer algumas configurações.

### Definir locais

Você define alguns pontos de interesse no serviço Places.

1. Na interface da Coleção de dados, selecione **[!UICONTROL Places]**.
1. Selecionar ![Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg).
1. No menu de contexto, selecione **[!UICONTROL Gerenciar bibliotecas]**.
   ![Gerenciar bibliotecas](assets/places-manage-libraries.png)
1. No **[!UICONTROL Gerenciar bibliotecas]** , selecione **[!UICONTROL Novo]**.
1. No **[!UICONTROL Criar biblioteca]** caixa de diálogo inserir um **[!UICONTROL Nome]**, por exemplo `Luma`.
1. Selecionar **[!UICONTROL Confirmar o]**.
   ![Criar biblioteca](assets/places-create-library.png)
1. Para fechar o **[!UICONTROL Gerenciar bibliotecas]** , selecione **[!UICONTROL Fechar]**.
1. Voltar para **[!UICONTROL Gerenciamento de POI]**, selecione **[!UICONTROL Importar POIs]**.
1. Selecionar **[!UICONTROL Início]** no **[!UICONTROL Importar locais]** diálogo.
1. Selecionar **[!DNL Luma]** na lista de bibliotecas,
1. Selecione **[!UICONTROL Próximo]**.
   ![Selecionar biblioteca](assets/places-import-select-library.png)
1. Baixe o [Arquivo ZIP de POIs Luma](assets/luma_pois.csv.zip) e extraia-o para um local no computador.
1. No **[!UICONTROL Importar locais]** , arraste e solte o arquivo extraído `luma_pois.csv` arquivo em até **[!UICONTROL Escolher arquivo CSV - arraste e solte seu arquivo]**. Você deve ver **[!UICONTROL Validação bem-sucedida]** - **[!UICONTROL Arquivo CSV validado com êxito]**.
1. Selecionar **[!UICONTROL Iniciar importação]**. Você deve ver **[!UICONTROL Sucesso]** - **[!UICONTROL 6 novos POIs adicionados com sucesso]**.
1. Selecionar **[!UICONTROL Concluído]**.
1. Entrada **[!UICONTROL Gerenciamento de POI]**, você deve ver que seis novas lojas Luma são adicionadas à lista. Você pode alternar entre ![Lista](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) lista e ![Mapa](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MapView_18_N.svg) exibição de mapa.
   ![Lista de locais](assets/places-list.png).


### Instalar a extensão Places

1. Navegue até **[!UICONTROL Tags]** e encontre sua propriedade de tag móvel e abra a propriedade.
1. Selecionar **[!UICONTROL Extensões]**.
1. Selecionar **[!UICONTROL Catálogo]**.
1. Procure por **[!UICONTROL Places]** extensão.
1. Instale a extensão.

   ![Adicionar extensão do Decisioning](assets/tag-places-extension.png)

1. No **[!UICONTROL Instalar extensão]** diálogo:
   1. Selecionar **[!DNL Luma]** do **[!UICONTROL Selecionar uma biblioteca]** lista.
   1. Verifique se você escolheu sua biblioteca de trabalho, por exemplo **[!UICONTROL Build inicial]**.
   1. Selecionar **[!UICONTROL Salvar na biblioteca e criar]** de **[!UICONTROL Salvar na biblioteca]**.
      ![Instalar a extensão Places](assets/places-install-extension.png).

1. Sua biblioteca foi recriada.


### Verifique seu esquema

Verifique se o esquema, conforme definido em [Criar esquema](create-schema.md)O, incorpora os grupos de campos e classes necessários para coletar dados de POI e geolocalização.

1. Navegue até a interface da Coleção de dados e selecione **[!UICONTROL Esquemas]** do painel esquerdo.
1. Selecionar **[!UICONTROL Procurar]** na barra superior.
1. Selecione seu esquema para abri-lo.
1. No editor de esquema, selecione **[!UICONTROL Evento de experiência do consumidor]**.
1. Você vê um **[!UICONTROL placeContext]** objeto com objeto e campos para capturar dados de interação e geolocalização de POI.
   ![Locais do esquema](assets/schema-places-context.png).


### Atualizar a propriedade da tag

A extensão Places para tags fornece funcionalidade para monitorar eventos de geolocalização e permite acionar ações com base nesses eventos. Você pode usar essa funcionalidade para minimizar a codificação da API que deve ser implementada no aplicativo.

**Elementos de dados**

Primeiro, você cria vários elementos de dados.

1. Vá para a propriedade da tag na interface da Coleção de dados.
1. Selecionar **[!UICONTROL Elementos de dados]** do painel esquerdo.
1. Selecione **[!UICONTROL Adicionar elemento de dados]**.
1. No **[!UICONTROL Criar elemento de dados]** insira um nome, por exemplo `Name - Entered`.
1. Selecionar **[!UICONTROL Places]** do **[!UICONTROL Extensão]** lista.
1. Selecionar **[!UICONTROL Nome]** do **[!UICONTROL Tipo de elemento de dados]** lista.
1. Selecionar **[!UICONTROL POI atual]** abaixo **[!UICONTROL TARGET]**.
1. Selecionar **[!UICONTROL Salvar na biblioteca]**.
   ![Elemento de dados](assets/tags-create-data-element.png)

1. Repita as etapas 4 a 8 usando as informações da tabela abaixo para criar elementos de dados adicionais.

   | Nome | Extensão | Tipo de elemento de dados | TARGET |
   |---|---|---|---|
   | `Name - Exited` | Places | Nome | Último POI de saída |
   | `Category - Current` | Places | Categoria | POI atual |
   | `Category - Exited` | Places | Categoria | Último POI de saída |
   | `City - Current` | Places | Cidade | POI atual |
   | `City - Exited` | Places | Cidade | Último POI de saída |

   Você deve ter a seguinte lista de Elementos de dados.

   ![Lista de elementos de dados](assets/tags-data-elements-list.png)

**Regras**

Em seguida, você definirá regras para trabalhar com esses elementos de dados.

1. Na propriedade da tag, selecione **[!UICONTROL Regras]** do painel esquerdo.
1. Selecionar **[!UICONTROL Adicionar regra]**.
1. No **[!UICONTROL Criar regra]** insira um nome para a regra, por exemplo `POI - Entry`.
1. Selecionar ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) abaixo **[!UICONTROL EVENTOS]**.
   1. Selecionar **[!UICONTROL Places]** do **[!UICONTROL Extensão]** e selecione **[!UICONTROL Inserir POI]** do **[!UICONTROL Tipo de evento]** lista.
   1. Selecione **[!UICONTROL Manter alterações]**.
      ![Marcar evento](assets/tags-event-mobile-core.png).
1. Selecionar ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) abaixo **[!UICONTROL AÇÕES]**.
   1. Selecionar **[!UICONTROL Núcleo móvel]** do **[!UICONTROL Extensão]** selecione **[!UICONTROL Anexar dados]** de **[!UICONTROL Tipo de ação]** a lista. Esta ação anexa dados de carga.
   1. No **[!UICONTROL Carga JSON]**, cole a seguinte carga:

      ```json
      {
          "xdm": {
              "eventType": "location.entry",
              "placeContext": {
                  "geo": {
                      "city": "{%%City - Current%%}"
                  },
                  "POIinteraction": {
                      "poiDetail": {
                          "name": "{%%Name - Current%%}",
                          "category": "{%%Category - Current%%}"
                      },
                      "poiEntries": {
                          "value": 1
                      }
                  }
              }
          }
      }
      ```

      Também é possível inserir `{%% ... %%}` valores de espaço reservado do elemento de dados no JSON ao selecionar o ![Dados](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg). Uma caixa de diálogo pop-up permite que você escolha qualquer elemento de dados criado.

   1. Selecione **[!UICONTROL Manter alterações]**.
      ![Ação de tags](assets/tags-action-mobile-core.png)

1. Selecionar ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) ao lado da **[!UICONTROL Núcleo móvel - Anexar dados]** ação.
   1. Selecionar **[!UICONTROL Rede de borda Adobe Experience Platform]** do **[!UICONTROL Extensão]** e selecione **[!UICONTROL Encaminhar evento para a rede de borda]**. Essa ação garante que o evento e os dados de payload adicionais sejam encaminhados para a Rede de borda da plataforma.
   1. Selecione **[!UICONTROL Manter alterações]**.

1. Para salvar a regra, selecione **[!UICONTROL Salvar na biblioteca]**.

   ![Regra](assets/tags-rule-poi-entry.png)

Vamos criar outra regra

1. No **[!UICONTROL Criar regra]** insira um nome para a regra, por exemplo `POI - Exit`.
1. Selecionar ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) abaixo **[!UICONTROL EVENTOS]**.
   1. Selecionar **[!UICONTROL Places]** do **[!UICONTROL Extensão]** e selecione **[!UICONTROL POI de saída]** do **[!UICONTROL Tipo de evento]** lista.
   1. Selecione **[!UICONTROL Manter alterações]**.
1. Selecionar ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) abaixo **[!UICONTROL AÇÕES]**.
   1. Selecionar **[!UICONTROL Núcleo móvel]** de **[!UICONTROL Extensão]** selecione **[!UICONTROL Anexar dados]** de **[!UICONTROL Tipo de ação]** lista.
   1. No **[!UICONTROL Carga JSON]**, cole a seguinte carga:

      ```json
      {
          "xdm": {
              "eventType": "location.exit",
              "placeContext": {
                  "geo": {
                      "city": "{%%City - Exited%%}"
                  },
                  "POIinteraction": {
                      "poiExits": {
                          "value": 1
                      },
                      "poiDetail": {
                          "name": "{%%Name - Exited%%}",
                          "category": "{%%Category - Exited%%}"
                      }
                  }
              }
          }
      }
      ```

   1. Selecione **[!UICONTROL Manter alterações]**.

1. Selecionar ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) ao lado da **[!UICONTROL Núcleo móvel - Anexar dados]** ação.
   1. Selecionar **[!UICONTROL Rede de borda Adobe Experience Platform]** do **[!UICONTROL Extensão]** e selecione **[!UICONTROL Encaminhar evento para a rede de borda]**.
   1. Selecione **[!UICONTROL Manter alterações]**.

1. Para salvar a regra, selecione **[!UICONTROL Salvar na biblioteca]**.

   ![Regra](assets/tags-rule-poi-exit.png)


Para garantir que todas as alterações em sua tag sejam publicadas

1. Selecionar **[!UICONTROL Build inicial]** como a biblioteca a ser criada.
1. Selecionar **[!UICONTROL Build]**.
   ![Criar biblioteca](assets/tags-build-library.png)




## Validar configuração no Assurance

Para validar sua configuração no Assurance:

1. Vá para a interface do usuário do Assurance.
1. Se ainda não estiver disponível no painel à esquerda, selecione **[!UICONTROL Configurar]** no painel esquerdo e selecione ![Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) ao lado de **[!UICONTROL Eventos]** e **[!UICONTROL Mapear e simular]** abaixo **[!UICONTROL SERVIÇO DO PLACES]**.
1. Selecione **[!UICONTROL Salvar]**.
1. Selecionar **[!UICONTROL Mapear e simular]** no painel esquerdo.
1. Mova o mapa para um local de um de seus POIs.
1. Selecionar ![Engrenagem](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Gears_18_N.svg) Simular POIs de carga. Seu POI é identificado usando um círculo e um pino.
1. Selecione seu POI.
1. No pop-up, selecione ![Engrenagem](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Gears_18_N.svg) **[!UICONTROL Simular Evento de Entrada]**.
   ![Simular Evento de Entrada](assets/places-simulate.png)
1. Selecionar **[!UICONTROL Eventos]** no painel esquerdo, e você deverá ver os eventos que simulou.
   ![Validação da decisão do AJO](assets/places-events.png)


## Implementar o Places no aplicativo

Conforme discutido nas lições anteriores, a instalação de uma extensão de tag móvel fornece apenas a configuração. Em seguida, você deve instalar e registrar o SDK do Places. Se essas etapas não estiverem claras, revise o [Instalar SDKs](install-sdks.md) seção.

>[!NOTE]
>
>Se você concluiu o [Instalar SDKs](install-sdks.md) , o SDK do Places já está instalado e você pode ignorar essa etapa.
>

1. No Xcode, verifique se [AEP Places](https://github.com/adobe/aepsdk-places-ios) é adicionado à lista de pacotes nas Dependências de pacote. Consulte [Gerenciador de pacotes Swift](install-sdks.md#swift-package-manager).
1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL AppDelegate]** no navegador do Projeto Xcode.
1. Assegurar `AEPPlaces` faz parte da lista de importações.

   ```swift
   import AEPPlaces
   ```

1. Assegurar `Places.self` O faz parte da matriz de extensões que você está registrando.

   ```swift
   let extensions = [
       AEPIdentity.Identity.self,
       Lifecycle.self,
       Signal.self,
       Edge.self,
       AEPEdgeIdentity.Identity.self,
       Consent.self,
       UserProfile.self,
       Places.self,
       Messaging.self,
       Optimize.self,
       Assurance.self
   ]
   ```

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** no navegador do Projeto Xcode e localize o `func processRegionEvent(regionEvent: PlacesRegionEvent, forRegion region: CLRegion) async` função. Adicione o seguinte código:

   ```swift
   // Process geolocation event
   Places.processRegionEvent(regionEvent, forRegion: region)
   ```

   Este [`Places.processRegionEvent`](https://developer.adobe.com/client-sdks/documentation/places/api-reference/#processregionevent) A API comunica as informações de geolocalização ao serviço Places.

1. Navegue até **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Location]** > **[!DNL GeofenceSheet]** no navegador Project do Xcode.

   1. Para o botão Entrada, informe o seguinte código

   ```swift
   // Simulate geofence entry event
   Task {
       await MobileSDK.shared.processRegionEvent(regionEvent: .entry, forRegion: region)
   }
   ```

   1. Para o botão Sair, insira o seguinte código

   ```swift
   // Simulate geofence exit event
   Task {
       await MobileSDK.shared.processRegionEvent(regionEvent: .exit, forRegion: region)
   }
   ```

## Validar usando seu aplicativo

1. Abra o aplicativo em um dispositivo ou no simulador.

1. Vá para a **[!UICONTROL Localização]** guia.

1. Mova (arraste) o mapa ao redor para garantir que o círculo central azul esteja acima de um dos POIs, por exemplo, Londres.

1. Toque <img src="assets/geobutton.png" width="20" /> até que você veja a categoria e o nome aparecerem no rótulo no local vermelho com o pino.

1. Toque no rótulo do POI, que abre o **[!UICONTROL POI próximo]** planilha.

   <img src="assets/appgeolocation.png" width="300" />

1. Pressione a **[!UICONTROL Entrada]** ou **[!UICONTROL Sair]** botões para simular eventos de entrada e saída de geofence no aplicativo.

   <img src="assets/appentryexit.png" width="300" />

1. Você deve ver os eventos na interface do usuário do Assurance.



## Próximas etapas

Agora você deve ter todas as ferramentas para começar a adicionar mais funcionalidade à funcionalidade de geolocalização no aplicativo. Depois de encaminhar os eventos para a Rede de borda, configure o aplicativo para [Experience Platform](platform.md), você deve ver os eventos de experiência que aparecem para o perfil usado no aplicativo.

Na seção Journey Optimizer deste tutorial, você verá que os eventos de experiência podem ser usados para acionar jornadas (consulte [notificação por push](journey-optimizer-inapp.md) e [mensagens no aplicativo](journey-optimizer-push.md) com o Journey Optimizer). Por exemplo, o exemplo usual de enviar ao usuário do aplicativo uma notificação por push com alguma promoção de produto quando esse usuário entra na cerca geográfica de uma loja física.

Você viu uma implementação da funcionalidade para seu aplicativo, orientada principalmente pelo serviço Places, bem como elementos de dados e regras definidos na propriedade de tag. Dessa forma, minimize o código em seu aplicativo. Como alternativa, você pode implementar a mesma funcionalidade diretamente no aplicativo usando o [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API (consulte [Eventos](events.md) para obter mais informações) com uma carga XDM contendo uma variável `placeContext` objeto.

>[!SUCCESS]
>
>Agora você habilitou o aplicativo para serviços de geolocalização usando a extensão Places no SDK móvel do Experience Platform.
>
>Obrigado por investir seu tempo aprendendo sobre o Adobe Experience Platform Mobile SDK. Se você tiver dúvidas, quiser compartilhar comentários gerais ou tiver sugestões sobre conteúdo futuro, compartilhe-as nesta [Publicação de discussão da comunidade do Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Próximo: **[Mapear dados para o Adobe Analytics](analytics.md)**
