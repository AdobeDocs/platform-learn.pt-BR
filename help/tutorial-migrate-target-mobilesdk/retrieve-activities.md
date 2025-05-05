---
title: Recuperar atividades do Target - Migrar a implementação do Adobe Target no aplicativo móvel para o Adobe Journey Optimizer - Extensão de decisão
description: Saiba como recuperar atividades do Adobe Target ao migrar do Adobe Target para a extensão móvel do Adobe Journey Optimizer - Decisioning.
exl-id: 39569088-a254-4e64-9956-0c6e1a8ed2a5
source-git-commit: 2ebad2014d4c29a50af82328735258958893b42c
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Recuperar atividades do Target

As implementações móveis do Target usam mboxes regionais (agora conhecidas como &quot;escopos&quot;) para fornecer conteúdo de atividades que usam o Experience Composer baseado em formulário do Target. É necessário atualizar o aplicativo móvel para incluir escopos nas chamadas de rede.

O conteúdo retornado pelo Target, também conhecido como &quot;ofertas&quot;, geralmente consiste em texto ou json que você precisa consumir em seu aplicativo para renderizar a experiência final do cliente. As ofertas do Target são usadas com frequência para:

* Habilitar sinalizadores de recursos no aplicativo
* Fornecer texto ou imagens alternativos

Se você tiver atividades que precisam ser executadas nas versões de extensão do Target e de extensão do Decisioning de seu aplicativo, certifique-se de testar completamente. Se precisar usar diferentes ofertas para diferentes versões do aplicativo, considere usar as opções de direcionamento na interface para fornecer diferentes ofertas para as diferentes versões.

Sempre inclua o tratamento de erros para exibir experiências adequadas em condições de erro.


## Solicitar e aplicar conteúdo sob demanda

>[!IMPORTANT]
>
>Depois de aplicar conteúdo ao aplicativo, é fundamental acionar a API `displayed` para informar ao Target que o visitante viu o conteúdo alternativo ou padrão especificado na atividade. Consulte a página [Rastrear eventos de conversão do Target](track-events.md) para obter mais detalhes.


+++ Exemplo do Android

>[!BEGINTABS]

>[!TAB Otimizar SDK]

```Java
// Mboxes for Target activities
final DecisionScope decisionScope1 = DecisionScope("myTargetMbox1");
final DecisionScope decisionScope2 = new DecisionScope("myTargetMbox2");
 
final List<DecisionScope> decisionScopes = new ArrayList<>();
decisionScopes.add(decisionScope1);
decisionScopes.add(decisionScope2);
 
// Prefetch the Target mboxes
Optimize.updatePropositions(decisionScopes,
                            new HashMap<String, Object>() {
                                {
                                    put("xdmKey", "xdmValue");
                                }
                            },
                            new HashMap<String, Object>() {
                                {
                                    put("dataKey", "dataValue");
                                }
                            },
                            new AdobeCallbackWithOptimizeError<Map<DecisionScope, OptimizeProposition>>() {
                                @Override
                                public void fail(AEPOptimizeError optimizeError) {
                                    // Log in case of error
                                    Log.d("Target Prefetch error", optimizeError.title);
                                }
 
                                @Override
                                public void call(Map<DecisionScope, OptimizeProposition> propositionsMap) {
                                    // Retrieve cached propositions if prefetch succeeds
                                    Optimize.getPropositions(scopes, new AdobeCallbackWithError<Map<DecisionScope, OptimizeProposition>>() {
                                        @Override
                                      public void fail(final AdobeError adobeError) {
                                              // handle error
                                        }
 
                                        @Override
                                        public void call(Map<DecisionScope, OptimizeProposition> propositionsMap) {
                                              if (propositionsMap != null && !propositionsMap.isEmpty()) {
                                                // get the propositions for the given decision scopes
                                                if (propositionsMap.contains(decisionScope1)) {
                                                      final OptimizeProposition proposition1 = propsMap.get(decisionScope1)
                                                      // read proposition1 offers and display them
                                                }
                                                if (propositionsMap.contains(decisionScope2)) {
                                                      final OptimizeProposition proposition2 = propsMap.get(decisionScope2)
                                                      // read proposition2 offers and display them
                                                }
                                              }
                                        }
                                      });
                                }
                            });
```

>[!ENDTABS]

+++

+++ Exemplo do iOS

>[!BEGINTABS]

>[!TAB Otimizar SDK]

```Swift
// Mboxes for Target activities
let decisionScope1 = DecisionScope(name: "myTargetMbox1")
let decisionScope2 = DecisionScope(name: "myTargetMbox2")
 
// Prefetch the Target mboxes
Optimize.updatePropositions(for: [decisionScope1, decisionScope2]
                            withXdm: ["xdmKey": "xdmValue"]
                            andData: ["dataKey": "dataValue"]) { data, error in
            if let error = error as? AEPOptimizeError {
                // handle error
                return
            }
            // Retrieve cached propositions if prefetch succeeds
            Optimize.getPropositions(for: [decisionScope1, decisionScope2]) { propositionsDict, error in
                if let error = error {
                    // handle error
                    return
                }
 
                if let propositionsDict = propositionsDict {
                    // get the propositions for the given decision scopes
 
                    if let proposition1 = propositionsDict[decisionScope1] {
                        // read proposition1 offers and display them
                    }
 
                    if let proposition2 = propositionsDict[decisionScope2] {
                        // read proposition2 offers and display them
                    }
                }
            }
        }
```

>[!ENDTABS]

+++



Em seguida, saiba como [passar parâmetros do Target usando a extensão de Decisão](send-parameters.md).

>[!NOTE]
>
>Estamos empenhados em ajudá-lo a ser bem-sucedido na migração para dispositivos móveis do Target da extensão do Target para a extensão do Decisioning. Se você encontrar obstáculos com sua migração ou achar que há informações críticas ausentes neste guia, envie-nos uma mensagem em [esta discussão da comunidade](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484?profile.language=pt#M625).
