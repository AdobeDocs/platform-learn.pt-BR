---
title: Offer Decisioning - Configurar as ofertas e a ID de decisão
description: Offer Decisioning - Configurar as ofertas e a ID de decisão
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 3%

---

# 3.3.2 Configurar as ofertas e a decisão

## 3.3.2.1 Criar suas ofertas personalizadas

Neste exercício, você criará quatro **Ofertas personalizadas**. Estes são os detalhes a serem considerados ao criar essas ofertas:

| Nome | Date Range | Link de imagem para email | Link de imagem para a Web | Texto | Prioridade | Elegibilidade | Idioma |
|-----|------------|----------------------|--------------------|------|:--------:|--------------|:-------:|
| `--aepUserLdap-- - Nadia Elements Shell` | hoje - 1 mês depois | https://bit.ly/3nPiwdZ | https://bit.ly/2INwXjt | `{{ profile.person.name.firstName }}, 10% discount on Nadia Elements Shell` | 25 | all - Clientes do sexo feminino | Inglês (Estados Unidos) |
| `--aepUserLdap-- - Radiant Tee` | hoje - 1 mês depois | https://bit.ly/2HfA17v | https://bit.ly/3pEIdzn | `{{ profile.person.name.firstName }}, 5% discount on Radiant Tee` | 15 | all - Clientes do sexo feminino | Inglês (Estados Unidos) |
| `--aepUserLdap-- - Zeppelin Yoga Pant` | hoje - 1 mês depois | https://bit.ly/2IOaItW | https://bit.ly/2INZHZd | `{{ profile.person.name.firstName }}, 10% discount on Zeppelin Yoga Pant` | 25 | todos - Clientes do sexo masculino | Inglês (Estados Unidos) |
| `--aepUserLdap-- - Proteus Fitness Jackshirt` | hoje - 1 mês depois | https://bit.ly/330a43n | https://bit.ly/36USaQW | `{{ profile.person.name.firstName }}, 5% discount on Proteus Fitness Jackshirt` | 15 | todos - Clientes do sexo masculino | Inglês (Estados Unidos) |

{style="table-layout:auto"}

Faça login no Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`. Para alterar a sandbox, clique em **Produção (VA7)** e selecione a sandbox na lista. Neste exemplo, a sandbox é chamada de **AEP Enablement FY22**. Você estará na exibição **Página inicial** da sua sandbox `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

No menu esquerdo, clique em **Ofertas** e vá para **Ofertas**. Clique em **+ Criar oferta**.

![Regra de decisão](./images/offers1.png)

Você então verá esse pop-up. Selecione **Oferta personalizada** e clique em **Avançar**.

![Regra de decisão](./images/offers2.png)

Agora você está na exibição **Detalhes**.

![Regra de decisão](./images/offers3.png)

Nesse caso, você precisa configurar a oferta `--aepUserLdap-- - Nadia Elements Shell`. Use as informações na tabela acima para preencher os campos. Neste exemplo, o nome da Oferta personalizada é **vangeluw - Nadia Elements Shell**. Além disso, defina a **Data e hora de início** como ontem e defina a **Data e hora de término** como uma data em um mês a partir de agora.

Depois de concluído, você deve receber isto. Clique em **Next**.

![Regra de decisão](./images/offers4.png)

Agora é necessário criar **Representações**. As representações são uma combinação de um **Posicionamento** e um ativo real.

Para **Representação 1**, selecione:

- Canal: Web
- Posicionamento: Web - Imagem
- Conteúdo: URL
- Local público: copie a URL da coluna **Link de Imagem para a Web** na tabela acima

![Regra de decisão](./images/addcontent1.png)

Como alternativa, você pode selecionar **Biblioteca de ativos** para o conteúdo e clicar em **Procurar**.

![Regra de decisão](./images/addcontent2.png)

Você verá um pop-up da Biblioteca da Assets, irá para a pasta **enablement-assets** e selecionará o arquivo de imagem **nadia-web.png**. Clique em **Selecionar**.

![Regra de decisão](./images/addcontent3.png)

Você verá isto:

![Regra de decisão](./images/addcontentrep20.png)

Clique em **+ Adicionar representação**.

![Regra de decisão](./images/addrep.png)

Para **Representação 2**, selecione:

- Canal: Email
- Posicionamento: Email - Imagem
- Conteúdo: URL
- Local público: copie a URL da coluna **Link de Imagem para Email** na tabela acima

![Regra de decisão](./images/addcontentrep21.png)

Como alternativa, você pode selecionar **Biblioteca de ativos** para o conteúdo e clicar em **Procurar**.

![Regra de decisão](./images/addcontent2b.png)

Você verá um pop-up da Biblioteca da Assets, irá para a pasta **enablement-assets** e selecionará o arquivo de imagem **nadia-email.png**. Clique em **Selecionar**.

![Regra de decisão](./images/addcontent3b.png)

Você verá isto:

![Regra de decisão](./images/addcontentrep20b.png)

Em seguida, clique em **+ Adicionar representação**.

![Regra de decisão](./images/addrep.png)

Para **Representação 3**, selecione:

- Canal: não digital
- Posicionamento: Não digital - Texto

Em seguida, é necessário adicionar conteúdo. Nesse caso, isso significa adicionar o texto a ser usado como uma chamada para ação.

Clique em **Adicionar conteúdo**.

![Regra de decisão](./images/addcontentrep31.png)

Você então verá esse pop-up.

![Regra de decisão](./images/addcontent3text.png)

Selecione **Texto personalizado** e preencha estes campos:

Examine o campo **Texto** da tabela acima e insira esse texto aqui, neste caso: `{{ profile.person.name.firstName }}, 10% discount on Nadia Elements Shell`.

Você também observará que pode selecionar qualquer atributo de perfil e incluí-lo como um campo dinâmico no texto da oferta. Neste exemplo, o campo `{{ profile.person.name.firstName }}` garantirá que o nome do cliente que receberá esta oferta será incluído no texto da oferta.

Você verá isso. Clique em **Salvar**.

![Regra de decisão](./images/addcontentrep3text.png)

Agora você tem isto. Clique em **Next**.

![Regra de decisão](./images/addcontentrep3textdone.png)

Você verá isto:

![Regra de decisão](./images/constraints.png)

Selecione **Por regra de decisão definida** e clique no ícone **+** para adicionar a regra **todas - Clientes do sexo feminino**.

![Regra de decisão](./images/constraints1.png)

Você verá isso. Preencha a **Prioridade** conforme indicado na tabela acima. Clique em **Next**.

![Regra de decisão](./images/constraints2.png)

Você verá uma visão geral da sua nova **Oferta personalizada**.

![Regra de decisão](./images/offeroverview.png)

Finalmente, clique em **Salvar e aprovar**.

![Regra de decisão](./images/saveapprove.png)

Em seguida, você verá que sua Oferta personalizada recém-criada fica disponível na Visão geral das ofertas:

![Regra de decisão](./images/offeroverview1.png)

Você agora deve repetir os passos acima para criar as três outras ofertas personalizadas para os produtos Camiseta Radiant, Zeppelin Yoga e Camiseta fitness Proteus.

Quando terminar, sua tela **Visão geral das ofertas** para **Ofertas personalizadas** deverá mostrar todas as suas ofertas.

![Ofertas finais](./images/finaloffers.png)

## 3.3.2.2 Criar sua oferta substituta

Depois de criar quatro Ofertas personalizadas, você deve configurar uma **Oferta substituta**.

Verifique se você está na exibição **Ofertas**:

![Ofertas finais](./images/finaloffers.png)

Clique em **+ Criar oferta**.

![Regra de decisão](./images/createoffer.png)

Você então verá esse pop-up. Selecione **Oferta de fallback** e clique em **Avançar**.

![Regra de decisão](./images/foffers2.png)

Você verá isto:

![Regra de decisão](./images/foffers3.png)

Digite este nome para sua oferta substituta: `--aepUserLdap-- - Luma Fallback Offer`. Clique em **Next**.

![Regra de decisão](./images/foffers4.png)

Agora é necessário criar **Representações**. As representações são uma combinação de um **Posicionamento** e um ativo real.

Para **Representação 1**, selecione:

- Canal: Web
- Posicionamento: Web - Imagem
- Conteúdo: URL
- Local público: `https://bit.ly/3nBOt9h`

![Regra de decisão](./images/addcontent1fb.png)

Como alternativa, você pode selecionar **Biblioteca de ativos** para o conteúdo e clicar em **Procurar**.

![Regra de decisão](./images/addcontent2fb.png)

Você verá um pop-up da Biblioteca da Assets, irá para a pasta **enablement-assets** e selecionará o arquivo de imagem **spriteyogastraps-web.png**. Clique em **Selecionar**.

![Regra de decisão](./images/addcontent3fb.png)

Você verá isto:

![Regra de decisão](./images/addcontentrep20fb.png)

Para **Representação 2**, selecione:

- Canal: Email
- Posicionamento: Email - Imagem
- Conteúdo: URL
- Local público: `https://bit.ly/3nF4qvE`

![Regra de decisão](./images/addcontentrep21fb.png)

Como alternativa, você pode selecionar **Biblioteca de ativos** para o conteúdo e clicar em **Procurar**.

![Regra de decisão](./images/addcontent2bfb.png)

Você verá um pop-up da Biblioteca da Assets, irá para a pasta **enablement-assets** e selecionará o arquivo de imagem **spriteyogastraps-email.png**. Clique em **Selecionar**.

![Regra de decisão](./images/addcontent3bfb.png)

Você verá isto:

![Regra de decisão](./images/addcontentrep20bfb.png)

Em seguida, clique em **+ Adicionar representação**.

![Regra de decisão](./images/addrep.png)

Para **Representação 3**, selecione:

- Canal: não digital
- Posicionamento: Não digital - Texto

Em seguida, é necessário adicionar conteúdo. Nesse caso, significa adicionar o Link da imagem.

Clique em **Adicionar conteúdo**.

![Regra de decisão](./images/addcontentrep21text.png)

Você então verá esse pop-up.

![Regra de decisão](./images/addcontent2text.png)

Selecione **Texto personalizado** e preencha estes campos:

Insira o texto `{{ profile.person.name.firstName }}, discover our Sprite Yoga Straps!` e clique em **Salvar**.

![Regra de decisão](./images/faddcontent3text.png)

Você verá isso. Clique em **Next**.

![Regra de decisão](./images/faddcontentrep3.png)

Você verá uma visão geral de sua nova **Oferta Substituta**. Clique em **Concluir**.

![Regra de decisão](./images/fofferoverview.png)

Finalmente, clique em **Salvar e aprovar**.

![Regra de decisão](./images/saveapprovefb.png)

Na tela **Visão geral das ofertas**, você verá o seguinte:

![Ofertas finais](./images/ffinaloffers.png)

## 3.3.2.3 Criar sua coleção

Uma Coleção é usada para **filtrar** um subconjunto de ofertas da lista de ofertas personalizadas e usá-la como parte de uma Decisão para acelerar o processo de decisão.

Ir para **Coleções**. Clique em **+ Criar coleção**.

![Regra de decisão](./images/collections.png)

Você então verá esse pop-up. Configure sua coleção desta forma. Clique em **Next**.

- Nome da coleção: use `--aepUserLdap-- - Luma Collection`
- Selecione **Criar coleção estática**.

![Regra de decisão](./images/createcollectionpopup1.png)

Na próxima tela, selecione as quatro **Ofertas personalizadas** que você criou no exercício anterior. Clique em **Salvar**.

![Regra de decisão](./images/createcollectionpopup2.png)

Agora você verá isto:

![Regra de decisão](./images/colldone.png)

## 3.3.2.4 Crie sua decisão

Uma decisão combina disposições, uma coleção de ofertas personalizadas e uma oferta substituta a ser usada pelo mecanismo do Offer Decisioning para encontrar a melhor oferta para um perfil específico, com base em cada uma das características de oferta personalizadas individuais, como prioridade, restrição de elegibilidade e limite total/usuário.

Para configurar sua **Decisão**, vá para **Decisões**. Clique em **+ Criar atividade**.

![Regra de decisão](./images/activitydd.png)

Você verá isto:

![Regra de decisão](./images/activity1.png)

Preencha os campos assim. Clique em **Next**.

- Nome: `--aepUserLdap-- - Luma Decision`
- Data e hora de início: ontem
- Data e hora de término: hoje + 1 mês

![Regra de decisão](./images/activity2.png)

Na próxima tela, você precisa adicionar disposições aos escopos de decisão. Você precisará criar escopos de decisão para os posicionamentos **Web - Imagem**, **Email - Imagem** e **Não digital - Texto**.

![Regra de decisão](./images/addplacements.png)

Primeiro, crie o escopo de decisão para **Não digital - Texto** selecionando esse posicionamento na lista suspensa. Em seguida, clique no botão **Adicionar** para adicionar critérios de avaliação.

![Regra de decisão](./images/activity3.png)

Selecione sua coleção `--aepUserLdap-- - Luma Collection` e clique em **Adicionar**.

![Regra de decisão](./images/activity4text.png)

Você verá isso. Clique no botão **-** para adicionar um novo escopo de decisão.

![Regra de decisão](./images/activity5text.png)

Selecione a **Web - Image** de posicionamento e adicione sua coleção `--aepUserLdap-- - Luma Collection` nos critérios de avaliação. Em seguida, clique no botão **+** novamente para adicionar um novo escopo de decisão.

![Regra de decisão](./images/activity6text.png)

Selecione o posicionamento **Email - Image** e adicione sua coleção `--aepUserLdap-- - Luma Collection` nos critérios de avaliação. Em seguida, clique em **Avançar**.

![Regra de decisão](./images/activity4.png)

Agora é necessário selecionar sua **Oferta Substituta**, que se chama `--aepUserLdap-- - Luma Fallback Offer`. Clique em **Next**.

![Regra de decisão](./images/activity10.png)

Revise sua decisão. Clique em **Concluir**.

![Regra de decisão](./images/activity11.png)

No pop-up, clique em **Salvar e ativar**.

![Regra de decisão](./images/activity12.png)

E, finalmente, você verá sua decisão na visão geral:

![Regra de decisão](./images/activity13.png)

Você configurou sua decisão com êxito. Sua decisão agora está ativa e pode ser usada para fornecer ofertas otimizadas e personalizadas aos seus clientes, em tempo real.

Próxima Etapa: [3.3.3 Prepare a propriedade do Cliente da Coleção de Dados e a configuração do SDK da Web para o Offer Decisioning](./ex3.md)

[Voltar ao módulo 3.3](./offer-decisioning.md)

[Voltar a todos os módulos](./../../../overview.md)
