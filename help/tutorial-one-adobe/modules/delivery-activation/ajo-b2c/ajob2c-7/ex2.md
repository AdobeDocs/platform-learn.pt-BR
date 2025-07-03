---
title: Offer Decisioning - Configurar as ofertas e a ID de decisão
description: Offer Decisioning - Configurar as ofertas e a ID de decisão
kt: 5342
doc-type: tutorial
source-git-commit: 13d790855601fa6f36c1afa0f2d5faad5fc07eb0
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 13%

---

# 3.7.2 Configurar as ofertas e a decisão

## 3.7.2.1 Crie suas ofertas personalizadas

Neste exercício, você criará quatro **Ofertas personalizadas**. Estes são os detalhes a serem considerados ao criar essas ofertas:

| Nome | Date Range | Link de imagem para email | Link de imagem para a Web | Texto | Prioridade | Elegibilidade | Idioma | Frequência de limite | Nome da imagem |
|-----|------------|----------------------|--------------------|------|:--------:|--------------|:-------:|:-------:|:-------:|
| `--aepUserLdap-- - AirPods Max` | hoje - 1 mês depois | https://bit.ly/4a9RJ5d | Escolher da Biblioteca da Assets | `{{ profile.person.name.firstName }}, 10% discount on AirPods Max` | 25 | all - Clientes do sexo feminino | Inglês (Estados Unidos) | 3 | Apple AirPods Max - Female.jpg |
| `--aepUserLdap-- - Galaxy S24` | hoje - 1 mês depois | https://bit.ly/3W8yuDv | Escolher da Biblioteca da Assets | `{{ profile.person.name.firstName }}, 5% discount on Galaxy S24` | 15 | all - Clientes do sexo feminino | Inglês (Estados Unidos) | 3 | Galaxy S24 - Female.jpg |
| `--aepUserLdap-- - Apple Watch` | hoje - 1 mês depois | https://bit.ly/4fGwfxX | https://bit.ly/4fGwfxX | `{{ profile.person.name.firstName }}, 10% discount on Apple Watch` | 25 | todos - Clientes do sexo masculino | Inglês (Estados Unidos) | 3 | Apple Watch - Male.jpg |
| `--aepUserLdap-- - Galaxy Watch 7` | hoje - 1 mês depois | https://bit.ly/4gTrkeo | Escolher da Biblioteca da Assets | `{{ profile.person.name.firstName }}, 5% discount on Galaxy Watch 7` | 15 | todos - Clientes do sexo masculino | Inglês (Estados Unidos) | 3 | Galaxy Watch7 - Male.jpg |

{style="table-layout:auto"}

Faça login no Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`. Você estará na exibição **Página inicial** da sua sandbox `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## Próximas etapas

Vá para a configuração do Web SDK do [3.7.3 para o Experience Decisioning](./ex3.md){target="_blank"}

Voltar para [Experience Decisioning](ajo-decisioning.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
