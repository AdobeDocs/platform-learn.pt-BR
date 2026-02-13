---
title: Introdução aos fluxos de trabalho personalizados do Firefly
description: Introdução aos fluxos de trabalho personalizados do Firefly
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 7d9ad7ec-7744-4ba6-9c11-c434e6cdef09
source-git-commit: 5fe2f1c413f54dd1e3c67d78460d7f2a84248005
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 0%

---

# 1.7.1 Introdução aos fluxos de trabalho personalizados do Firefly

[!BADGE Beta]

+++Detalhes do Beta
Ao usar a Beta de fluxos de trabalho personalizados da Firefly, você reconhece que a Beta é fornecida &quot;no estado em que se encontra&quot; sem garantias de nenhum tipo. A Adobe não tem nenhuma obrigação de manter, corrigir, atualizar, alterar, modificar ou oferecer suporte à Beta. É recomendável ter cuidado e não depender de forma alguma do funcionamento ou desempenho correto desse Beta e/ou dos materiais que o acompanham. O Beta é considerado Informações confidenciais da Adobe.  Qualquer &quot;Feedback&quot; (informação sobre o Beta incluindo, mas não se limitando a, problemas ou defeitos encontrados durante o uso do Beta, sugestões, melhorias e recomendações) fornecido por Você ao Adobe é atribuído ao Adobe, incluindo todos os direitos, cargos e interesses no e no Feedback.

+++

Ir para [https://firefly.adobe.com](https://firefly.adobe.com). Clique no ícone de perfil no canto superior direito e verifique se você selecionou a instância correta, que deve ser `--aepImsOrgName--`.

Ir para **Produção**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw1.png)

Você deverá ver isso. Clique em **Criar workflow (beta)**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw2.png)

## 1.7.1.1 Remover plano de fundo

Para conhecer os Fluxos de trabalho personalizados do Firefly, agora você implementará um caso de uso básico que se concentra na remoção do plano de fundo de uma imagem específica.

Altere o nome do fluxo de trabalho para `vangeluw - remove background`.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw3.png)

Abra a **Imagem**

![Fluxos de trabalho personalizados do Firefly](./images/ffcw4.png)

Selecione **Remover Plano de Fundo** e arraste e solte este nó na tela.

Agora é necessário conectar um nó de imagem de entrada e um nó de imagem de saída ao **Remover Plano de Fundo**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw5.png)

Role para cima e vá para **Entrada e Saída**. Clique no nó **Imagens de Entrada** e arraste-o para a tela.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw6.png)

Você deveria ficar com isso. Conecte o nó **Imagens de Entrada** ao nó **Remover Plano de Fundo** passando o cursor sobre o ponto azul ao lado de **Imagem** no nó **Imagens de Entrada** e desenhando uma linha para o ponto azul ao lado de **Imagem de Entrada** no nó **Remover Plano de Fundo**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw7.png)

Você deveria ficar com isso. Em seguida, clique no nó **Imagens de saída** e arraste-o para a tela.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw8.png)

Você deveria ficar com isso. Conecte o nó **Remover Plano de Fundo** ao nó **Imagens de Saída** passando o cursor sobre o ponto azul ao lado de **Imagem de Saída** no nó **Remover Plano de Fundo** e desenhando uma linha para o ponto azul ao lado de **Imagem** no nó **Imagens de Saída**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw9.png)

Você deveria ficar com isso.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw10.png)

O fluxo de trabalho básico agora está pronto para teste. Baixe a imagem [phone.png](./assets/phone.png) na área de trabalho.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw11.png)

Volte para o seu fluxo de trabalho. Clique na área **Arrastar e soltar** do nó **Imagens de Entrada**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw11a.png)

Selecione o arquivo **phone.png**. Clique em **Abrir**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw12.png)

Você deverá ver isso. Clique em **Executar**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw13.png)

Após 1-2 minutos, você deve ver esse resultado.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw14.png)

## 1.7.1.2 Remover plano de fundo + Cortar

Agora você deve adicionar um nó **Cortar** à tela. No menu, vá para **Imagem** e role para baixo até encontrar **Recortar**. Arraste-o para a tela.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw15.png)

Posicione o nó **Cortar** entre o nó **Remover Plano de Fundo** e o nó **Imagem de Saída**.

Agora é necessário remover a conexão entre o nó **Remover Plano de Fundo** e o nó **Imagem de Saída**. Você pode fazer isso clicando duas vezes na linha entre os dois nós.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw16.png)

Você deveria ficar com isso. Conecte o nó **Remover Plano de Fundo** ao nó **Cortar** e conecte o nó **Cortar** ao nó **Imagem de Saída**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw17.png)

Marque a caixa de seleção para **Cortar automaticamente** e teste seu fluxo de trabalho clicando em **Executar**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw18.png)

Após 1-2 minutos, você deve ver isso, que mostra uma imagem com uma resolução diferente agora.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw19.png)

## 1.7.1.3 Remover plano de fundo + Cortar + Imagem composta

No menu, em **Imagem**, selecione um nó **Imagens Compostas (2D)** e arraste-o para a tela.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw20.png)

Adicione uma segunda conexão ao nó **Cortar**, conectando o ponto azul ao lado da **Imagem cortada** ao ponto azul ao lado da **Imagem de entrada** no nó **Imagens Compostas (2D)**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw21.png)

No menu, em **Entrada e Saída**, selecione um nó **Texto de Entrada** e arraste-o para a tela.

Conecte o ponto verde ao lado de **Texto** no nó **Texto de Entrada** ao ponto verde ao lado de **Prompt** no nó **Imagens Compostas (2D)**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw22.png)

Você deveria ficar com isso. Digite o prompt abaixo no nó **Texto de Entrada**.

`magazine quality photo of a phone on a red pedestal with a pink background surrounded by origami style pink paper hearts`

No menu, em **Entrada e Saída**, selecione um nó **Imagens de Saída** e arraste-o para a tela.

Conecte o ponto azul ao lado de **Imagem composta** no nó **Imagens compostas (2D)** ao ponto azul ao lado de **Imagem de entrada** no nó **Imagem de saída**.

Clique em **Executar**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw23.png)

Após alguns minutos, você verá algo como isso, que mostra sua imagem original em uma composição com base no prompt fornecido, em uma resolução específica.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw24.png)

## 1.7.1.4 Remover plano de fundo + Cortar + Imagem composta + Gerar vídeo

No menu, vá para **Vídeo**. Selecione o nó **Gerar vídeo** e arraste-o para a tela.

Conecte o ponto azul ao lado de **Imagem composta** do nó **Imagens compostas (2D)** ao ponto azul ao lado de **Imagem de entrada** do nó **Gerar vídeo**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw25.png)

No menu, vá para **Entrada e Saída**. Selecione o nó **Texto de Entrada** e arraste-o para a tela.

Conecte o ponto verde ao lado de **Texto** no nó **Texto de Entrada** ao ponto verde ao lado de **Prompt** do nó **Gerar Vídeo**.

Digite o prompt `background hearts fluttering` no nó **Texto de entrada**.

No menu, vá para **Entrada e Saída**. Selecione o nó **Vídeo de saída** e arraste-o para a tela.

Conecte o ponto violeta ao lado de **Saída de Vídeo** do nó **Gerar Vídeo** ao ponto violeta ao lado de **Vídeo** no nó **Vídeo de Saída**.

Clique em **Executar**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw26.png)

Depois de alguns vídeos, você verá isto, que mostra um vídeo com base na combinação da imagem e do prompt fornecidos.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw27.png)

## Escala de 1.7.1.5

Você fez isso para 1 imagem. Agora vamos usar esse fluxo de trabalho, só que para várias imagens.

Baixe estas imagens no seu desktop:

- [watch.jpg](./assets/watch.jpg)
- [airpods.jpg](./assets/airpods.jpg)

![Fluxos de trabalho personalizados do Firefly](./images/ffcw28.png)

No seu fluxo de trabalho, volte para o primeiro nó, **Imagens de Entrada**. Remove a imagem atualmente selecionada.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw29.png)

Clique na área **Arrastar e soltar**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw30.png)

Selecione as 3 imagens que você baixou. Clique em **Abrir**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw31.png)

Você deverá ver isso. clique em **Executar**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw32.png)

Após vários minutos, você deve ver uma saída semelhante, com 3 imagens sendo geradas e 3 vídeos.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw33.png)

## 1.7.1.5 Armazenamento no AEM Assets CS

Neste exercício, você armazenará os ativos criados como parte do fluxo de trabalho personalizado no AEM Assets CS.

Primeiro, você deve criar uma nova pasta no ambiente do AEM Assets CS.

Para fazer isso, vá para [https://experience.adobe.com](https://experience.adobe.com). Clique para abrir o **Experience Manager Assets**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw50.png)

Selecione o ambiente do AEM Assets CS, que deve se chamar `--aepUserLdap-- - CitiSignal AEM + ACCS`.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw51.png)

Vá para **Assets** e clique em **Criar Pasta**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw52.png)

Digite o nome: `--aepUserLdap-- - Firefly Custom Workflows`. Clique em **Criar**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw53.png)

Volte para o seu fluxo de trabalho personalizado e vá para o nó **Imagens de saída**. Clique em **Padrão** e selecione **AEM Assets**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw57.png)

Você deverá ver esse pop-up. Selecione o repositório do AEM Assets CS e a pasta que acabou de criar, que deve se chamar: `--aepUserLdap-- - Firefly Custom Workflows`. Clique em **Selecionar**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw54.png)

Vá para o nó **Vídeo de Saída**. Clique em **Padrão** e selecione **AEM Assets**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw55.png)

Você deverá ver esse pop-up. Selecione o repositório do AEM Assets CS e a pasta que acabou de criar, que deve se chamar: `--aepUserLdap-- - Firefly Custom Workflows`. Clique em **Selecionar**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw56.png)

Você deveria ficar com isso. Clique em **Executar**.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw56a.png)

Após alguns minutos, você deve ver os ativos criados se tornarem disponíveis na pasta no AEM Assets CS.

![Fluxos de trabalho personalizados do Firefly](./images/ffcw58.png)

## Próximas etapas

Volte para o [Workflow Builder](./workflowbuilder.md){target="_blank"}

Voltar para [Todos os Módulos](./../../../overview.md){target="_blank"}
