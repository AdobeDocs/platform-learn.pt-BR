---
title: Substituir o SDK - Migrar a implementação do Adobe Target no aplicativo móvel para o Adobe Journey Optimizer - Extensão de decisão
description: Saiba como substituir o SDK ao migrar do Adobe Target para a extensão móvel do Adobe Journey Optimizer - Decisioning.
exl-id: f1b77cad-792b-4a80-acff-e1a2f29250e1
source-git-commit: 2ebad2014d4c29a50af82328735258958893b42c
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 2%

---

# Substitua o SDK do Target pela opção Otimizar SDK

Saiba como substituir os SDKs da Adobe Target pelos SDKs de otimização na implementação móvel. Uma substituição básica consiste nas seguintes etapas:

* Atualizar dependências no Podfile ou arquivo `build.gradle`
* Atualizar importações
* Atualizar código de aplicativo


>[!INFO]
>
>No ecossistema do Adobe Experience Platform Mobile SDK, as extensões são implementadas pelos SDKs importados para seus aplicativos que podem ter nomes diferentes:
>
> * **Target SDK** implementa a **extensão do Adobe Target**
> * **Otimizar o SDK** implementa a **Adobe Journey Optimizer - Extensão de decisão**

## Atualizar dependências

+++Exemplo de Android

>[!BEGINTABS]

>[!TAB Otimizar SDK]

`build.gradle` dependências após a migração

```Java
implementation platform('com.adobe.marketing.mobile:sdk-bom:3.+')
implementation 'com.adobe.marketing.mobile:core'
implementation 'com.adobe.marketing.mobile:edgeidentity'
implementation 'com.adobe.marketing.mobile:edge'
implementation 'com.adobe.marketing.mobile:optimize'
```


>[!TAB SDK de Destino]

`build.gradle` dependências antes da migração

```Java
implementation platform('com.adobe.marketing.mobile:sdk-bom:3.+')
implementation 'com.adobe.marketing.mobile:analytics'
implementation 'com.adobe.marketing.mobile:target'
implementation 'com.adobe.marketing.mobile:core'
implementation 'com.adobe.marketing.mobile:identity'
implementation 'com.adobe.marketing.mobile:lifecycle'
implementation 'com.adobe.marketing.mobile:signal'
implementation 'com.adobe.marketing.mobile:userprofile'
```


>[!ENDTABS]

+++

+++ Exemplo do iOS

>[!BEGINTABS]


>[!TAB Otimizar SDK]

`Podfile` dependências após a migração

```Swift
use_frameworks!
target 'YourAppTarget' do
    pod 'AEPCore', '~> 5.0'
    pod 'AEPEdge', '~> 5.0'
    pod 'AEPEdgeIdentity', '~> 5.0'
    pod 'AEPOptimize', '~> 5.0'
end
```

>[!TAB SDK de Destino]

`Podfile` dependências antes da migração

```Swift
use_frameworks!
pod 'AEPAnalytics', '~> 5.0'
pod 'AEPTarget', '~> 5.0'
pod 'AEPCore', '~> 5.0'
pod 'AEPIdentity', '~> 5.0'
pod 'AEPSignal', '~>5.0'
pod 'AEPLifecycle', '~>5.0'
pod 'AEPUserProfile', '~> 5.0'
```

>[!ENDTABS]

+++

## Atualizar importações e código

+++ Exemplo do Android

>[!BEGINTABS]

>[!TAB Otimizar SDK]

Código de inicialização Java após a migração

```Java
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Edge;
import com.adobe.marketing.mobile.edge.identity.Identity;
import com.adobe.marketing.mobile.optimize.Optimize;
import com.adobe.marketing.mobile.AdobeCallback;
 
public class MainApp extends Application {
 
  private final String ENVIRONMENT_FILE_ID = "YOUR_APP_ENVIRONMENT_ID";
 
    @Override
    public void onCreate() {
        super.onCreate();
 
        MobileCore.setApplication(this);
        MobileCore.configureWithAppID(ENVIRONMENT_FILE_ID);
 
        MobileCore.registerExtensions(
            Arrays.asList(Edge.EXTENSION, Identity.EXTENSION, Optimize.EXTENSION),
            o -> Log.d("MainApp", "Adobe Journey Optimizer - Decisioning Mobile SDK was initialized.")
        );
    }
}
```

>[!TAB SDK de Destino]

Código de inicialização Java antes da migração

```Java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.Analytics;
import com.adobe.marketing.mobile.Extension;
import com.adobe.marketing.mobile.Identity;
import com.adobe.marketing.mobile.Lifecycle;
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Signal;
import com.adobe.marketing.mobile.Target;
import com.adobe.marketing.mobile.UserProfile;
import java.util.Arrays;
import java.util.List;
...
import android.app.Application;
...
public class MainApp extends Application {
...
    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
        MobileCore.setLogLevel(LoggingMode.DEBUG);
        ...
        List<Class<? extends Extension>> extensions = Arrays.asList(
            Analytics.EXTENSION,
            Target.EXTENSION,
            Identity.EXTENSION,
            Lifecycle.EXTENSION,
            Signal.EXTENSION,
            UserProfile.EXTENSION
        );
 
 
        MobileCore.registerExtensions(extensions, new AdobeCallback () {
            @Override
            public void call(Object o) {
                MobileCore.configureWithAppID(<Environment File ID>);
            }
        });
    }
}
```

>[!ENDTABS]

+++

+++ iOS

>[!BEGINTABS]

>[!TAB Otimizar SDK]

Código de inicialização Swift após a migração

```Swift
import AEPCore
import AEPEdge
import AEPEdgeIdentity
import AEPOptimize
 
@UIApplicationMain
final class AppDelegate: UIResponder, UIApplicationDelegate {
  var window: UIWindow?
 
  func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]? = nil) -> Bool {
 
      // register the extensions
      MobileCore.registerExtensions([Edge.self, AEPEdgeIdentity.Identity.self, Optimize.self]) {
        MobileCore.configureWith(appId: <YOUR_ENVIRONMENT_FILE_ID>) // Replace <YOUR_ENVIRONMENT_FILE_ID> with a String containing your own ID.
      }
 
      return true
  }
}
```

>[!TAB SDK de Destino]

Código de inicialização Swift antes da migração

```Swift
import AEPCore
import AEPAnalytics
import AEPTarget
import AEPIdentity
import AEPLifecycle
import AEPSignal
import AEPServices
import AEPUserProfile
...
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        MobileCore.setLogLevel(.debug)
        let appState = application.applicationState
        ...
        let extensions = [
            Analytics.self,
            Target.self,
            Identity.self,
            Lifecycle.self,
            Signal.self,
            UserProfile.self
        ]
        MobileCore.registerExtensions(extensions, {
        MobileCore.configureWith(<Environment File ID>)
        if appState != .background {
            MobileCore.lifecycleStart(additionalContextData: ["contextDataKey": "contextDataVal"])
            }
        })
        ...
        return true
    }
}
```

>[!ENDTABS]

+++

## Comparação de API

Muitas APIs de extensão do Target têm uma abordagem equivalente usando a Extensão de decisão descrita na tabela abaixo. Para obter mais detalhes sobre as [funções](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/api-reference/), consulte a referência da API.

| Extensão do Target | Extensão de decisão | Notas |
| --- | --- | --- | 
| [prefetchContent](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#prefetchcontent){target=_blank} | [updatePropositions](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/api-reference/#updatepropositionswithcompletionhandlerandtimeout){target=_blank} |  |
| [retrieveLocationContent](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#retrievelocationcontent){target=_blank} | [getPropositions](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/api-reference/#getpropositionswithtimeout){target=_blank} | Ao usar a API `getPropositions`, não é feita nenhuma chamada remota para buscar escopos não armazenados em cache na SDK. |
| [displayedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#retrievelocationcontent){target=_blank} | [Oferta -> exibido()](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} | Além disso, o método de oferta `generateDisplayInteractionXdm` pode ser usado para gerar o XDM para exibição de item. Posteriormente, a API sendEvent da SDK de rede da Edge pode ser usada para anexar dados XDM adicionais e de formato livre, e enviar um Evento de experiência ao remoto. |
| [clickedLocation](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#clickedlocation){target=_blank} | [Oferta -> tapped()](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} | Além disso, o método de oferta `generateTapInteractionXdm` pode ser usado para gerar o XDM para toque de item. Posteriormente, a API sendEvent da SDK de rede da Edge pode ser usada para anexar dados XDM adicionais e de formato livre, e enviar um Evento de experiência ao remoto. |
| [clearPrefetchCache](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#clickedlocation){target=_blank} | [clearCachedPropositions](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} |  |
| [redefinirExperiência](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#resetexperience){target=_blank} | n/d | Use a API [removeIdentity](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity){target=_blank} da Identidade para a extensão do Edge Network para o SDK a fim de interromper o envio do identificador de visitante para a rede da Edge. Para obter mais detalhes, consulte [a documentação da API removeIdentity](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity). <br><br>Observação: a API `resetIdentities` do Mobile Core apaga todas as identidades armazenadas na SDK, incluindo a Experience Cloud ID (ECID), e ela deve ser usada com moderação! |
| [getSessionId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#getsessionid){target=_blank} | n/d | O identificador de resposta `state:store` carrega informações relacionadas à sessão. A extensão de rede do Edge ajuda a gerenciá-la anexando itens de armazenamento de estado não expirados a solicitações subsequentes. |
| [setSessionId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#setsessionid){target=_blank} | n/d | O identificador de resposta `state:store` carrega informações relacionadas à sessão. A extensão de rede do Edge ajuda a gerenciá-la anexando itens de armazenamento de estado não expirados a solicitações subsequentes. |
| [getThirdPartyId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#getthirdpartyid){target=_blank} | n/d | Use a API updateIdentities da extensão Identity for Edge Network para fornecer o valor da ID de terceiros. Em seguida, configure o namespace da ID de terceiros no fluxo de dados. Para obter mais detalhes, consulte [a documentação móvel da ID de terceiros do Target](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| [setThirdPartyId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#setthirdpartyid){target=_blank} | n/d | Use a API updateIdentities da extensão Identity for Edge Network para fornecer o valor da ID de terceiros. Em seguida, configure o namespace da ID de terceiros no fluxo de dados. Para obter mais detalhes, consulte [a documentação móvel da ID de terceiros do Target](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| [getTntId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#gettntid){target=_blank} | n/d | O identificador de resposta `locationHint:result` carrega as informações de dica de localização do Target. Presume-se que a borda do Target esteja co-localizada com a Experience Edge. <br> <br>A extensão de rede do Edge usa a dica de local do EdgeNetwork para determinar o cluster de rede da Edge para o qual enviar solicitações. Para compartilhar a dica de local de rede do Edge entre SDKs (aplicativos híbridos), use as APIs do `getLocationHint` e do `setLocationHint` da extensão do Edge Network. Para obter mais detalhes, consulte [a `getLocationHint` documentação da API](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |
| [setTntId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#gettntid){target=_blank} | n/d | O identificador de resposta [locationHint:result](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#setlocationhint){target=_blank} carrega as informações de dica de localização de Destino. Presume-se que a borda do Target esteja co-localizada com a Experience Edge. <br> <br>A extensão de rede do Edge usa a dica de local do EdgeNetwork para determinar o cluster de rede da Edge para o qual enviar solicitações. Para compartilhar a dica de local de rede do Edge entre SDKs (aplicativos híbridos), use as APIs do `getLocationHint` e do `setLocationHint` da extensão do Edge Network. Para obter mais detalhes, consulte [a `getLocationHint` documentação da API](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |


Em seguida, saiba como [solicitar e renderizar atividades](retrieve-activities.md) para a página.

>[!NOTE]
>
>Estamos empenhados em ajudá-lo a ser bem-sucedido na migração para dispositivos móveis do Target da extensão do Target para a extensão do Decisioning. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484#M625).
