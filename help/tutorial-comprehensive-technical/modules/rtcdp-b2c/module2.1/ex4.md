---
title: Foundation - Perfil do cliente em tempo real - Criar um segmento - Interface do usuário
description: Foundation - Perfil do cliente em tempo real - Criar um segmento - Interface do usuário
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 3%

---

# 2.1.4 Criar um segmento - IU

Neste exercício, você criará um segmento usando o Construtor de segmentos da Adobe Experience Platform.

## Story

Ir para [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer logon, você chegará à página inicial do Adobe Experience Platform.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, você precisa selecionar uma **sandbox**. A sandbox a ser selecionada é chamada ``--aepSandboxName--``. Você pode fazer isso clicando no texto **[!UICONTROL Produção]** na linha azul na parte superior da tela. Depois de selecionar a [!UICONTROL sandbox] apropriada, você verá a alteração da tela e agora estará na [!UICONTROL sandbox] dedicada.

![Assimilação de dados](./../../../modules/datacollection/module1.2/images/sb1.png)

No menu no lado esquerdo, vá para **Segmentos**. Nesta página, você pode ter uma visão geral de todos os segmentos existentes. Clique no botão **+ Criar segmento** para começar a criar um novo segmento.

![Segmentação](./images/menuseg.png)

Quando estiver no novo construtor de segmentos, você notará imediatamente a opção de menu **Atributos** e a referência ao **Perfil individual XDM**.

![Segmentação](./images/segmentationui.png)

Como o XDM é a linguagem que impulsiona os negócios da experiência, o XDM também é a base para o construtor de segmentos. Todos os dados assimilados na Platform devem ser mapeados em relação ao XDM e, como tal, todos os dados se tornam parte do mesmo modelo de dados, independentemente de onde esses dados vêm. Isso oferece uma grande vantagem ao criar segmentos. A partir dessa interface do construtor de segmentos, é possível combinar dados de qualquer origem no mesmo fluxo de trabalho. Os segmentos criados no Construtor de segmentos podem ser enviados para soluções como Adobe Target, Adobe Campaign e Adobe Audience Manager para ativação.

Vamos criar um segmento que inclua todos os clientes **homens**.

Para chegar ao atributo de gênero, você precisa entender e conhecer o XDM.

Sexo é um atributo de Pessoa, que pode ser encontrado em Atributos. Para chegar lá, comece clicando em **Perfil Individual XDM**. Você verá isso. Na janela **Perfil individual XDM**, selecione **Pessoa**.

![Segmentação](./images/person.png)

Você verá isso. Em **Pessoa**, você pode encontrar o atributo **Gênero**. Arraste o atributo Gender para o construtor de segmentos.

![Segmentação](./images/gender.png)

Agora é possível escolher o gênero específico entre as opções pré-preenchidas. Nesse caso, vamos escolher **Masculino**.

![Segmentação](./images/genderselection.png)

Após selecionar **Masculino**, você pode obter uma estimativa da população do segmento pressionando o botão **Atualizar Estimativa**. Isso é muito útil para um usuário empresarial, para que ele possa ver o impacto de determinados atributos no tamanho do segmento resultante.

![Segmentação](./images/segmentpreview.png)

Você verá uma estimativa como a abaixo:

![Segmentação](./images/segmentpreviewest.png)

Em seguida, você deve refinar um pouco seu segmento. Você precisa criar um segmento de todos os clientes do sexo masculino que visualizaram o produto **Proteus Fitness Jackshirt (Orange)**.

Para criar esse segmento, é necessário adicionar um Evento de experiência. Você pode encontrar todos os Eventos de Experiência clicando no ícone **Eventos** na barra de menus **Campos**.

![Segmentação](./images/findee.png)

Em seguida, você verá o nó **XDM ExperienceEvents** de nível superior. Clique em **XDM ExperienceEvent**.

![Segmentação](./images/see.png)

Vá para **Itens da Lista de Produtos**.

![Segmentação](./images/plitems.png)

Selecione **Nome** e arraste e solte o objeto **Nome** do menu esquerdo na tela do construtor de segmentos na seção **Eventos**.

![Segmentação](./images/eeweb.png)

Você verá isto:

![Segmentação](./images/eewebpdtlname.png)

O parâmetro de comparação deve ser **igual** e, no campo de entrada, insira **MONTANA WIND JACKET**.

![Segmentação](./images/pv.png)

Toda vez que você adiciona um elemento ao construtor de segmentos, é possível clicar no botão **Atualizar estimativa** para obter uma nova estimativa da população do seu segmento.

Até o momento, você só usou a interface do para criar seu segmento, mas também há uma opção de código para criar um segmento.

Ao criar um segmento, você está compondo uma consulta do Profile Query Language (PQL). Para visualizar o código PQL, você pode clicar no alternador da **Visualização de código** no canto superior direito do construtor de segmentos.

![Segmentação](./images/codeview.png)

Agora você pode ver a declaração completa do PQL:

```sql
person.gender in ["male"] and CHAIN(xEvent, timestamp, [C0: WHAT(productListItems.exists(name.equals("MONTANA WIND JACKET", false)))])
```

Você também pode visualizar uma amostra dos perfis de clientes que fazem parte deste segmento clicando em **Exibir perfis**.

![Segmentação](./images/previewprofiles.png)

![Segmentação](./images/previewprofilesdtl.png)

Por fim, vamos dar um nome ao seu segmento e salvá-lo.

Como convenção de nomenclatura, use:

- `--aepUserLdap-- - Male customers with interest in Montana Wind Jacket`

![Segmentação](./images/segmentname.png)

Em seguida, clique no botão **Salvar e fechar** para salvar seu segmento. Depois disso, você será direcionado de volta à página de visão geral do segmento.

![Segmentação](./images/savedsegment.png)

Agora você pode continuar com o próximo exercício e criar um segmento por meio da API.

Próxima Etapa: [2.1.5 Criar um segmento - API](./ex5.md)

[Voltar ao módulo 2.1](./real-time-customer-profile.md)

[Voltar a todos os módulos](../../../overview.md)
