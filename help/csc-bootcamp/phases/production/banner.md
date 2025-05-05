---
title: Bootcamp do CSC - Criar banner de página inicial do produto
description: Bootcamp do CSC - Criar banner de página inicial do produto
doc-type: multipage-overview
exl-id: c78b6ba2-1a1a-4e95-a8ab-1b572fa2d8b1
source-git-commit: 143da6340b932563a3309bb46c1c7091e0ab2ee2
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---

# Criar banner de página inicial do produto

## Produção do banner

A automação de conteúdo reúne o potencial do Adobe Creative Cloud com o Experience Manager Assets, oferecendo aos profissionais de marketing a capacidade de automatizar a produção de ativos em escala, acelerando drasticamente a criação de variações. Vamos usar essas funcionalidades para gerar um banner que será usado na página inicial!

- Vá para o autor do AEM em [https://author-p105462-e991028.adobeaemcloud.com/](https://author-p105462-e991028.adobeaemcloud.com/) e faça logon com as credenciais fornecidas.

- Na página inicial, navegue até Ferramentas > Assets > Perfis de processamento.

![Ferramentas > Assets > Processando Perfis](./images/prod-processing-profiles.png)

- Na interface do, você verá todos os perfis de processamento existentes. Eles podem ser usados para ativar determinadas automações.

![lista de perfis de processamento](./images/prod-profile-list.png)


- Os seguintes itens são de seu interesse:
   - Banner escuro da Adobe: cria um banner da Adobe com uma sobreposição escura, com base no ativo selecionado

     ![banner escuro](./images/prod-banner-dark.jpg)
   - Luz do banner da Adobe: cria um banner da Adobe com uma sobreposição de luz, com base no ativo selecionado

     ![banner leve](./images/prod-banner-light.jpg)
   - Adobe Banner Green: cria um banner Adobe com uma sobreposição verde, com base no ativo selecionado

     ![banner verde](./images/prod-banner-green.jpg)

- Depois de escolher o tipo de banner que deseja criar, selecione o perfil de processamento e clique em &quot;Aplicar perfil às pastas&quot;.

![aplicar perfil à pasta](./images/prod-apply-profile.png)

- Na próxima tela, navegue até a pasta da sua equipe no AEM Assets. Em seguida, na parte superior esquerda, selecione o botão &quot;Criar&quot; para criar uma nova pasta e dar a ela um nome significativo, por exemplo, &quot;Criar banner escuro&quot;.

![criar pasta](./images/prod-create-profile-folder.png)

![criar detalhes da pasta](./images/prod-profile-folder-details.png)

- Depois de criar a pasta, marque a caixa ao lado de seu nome e, em seguida, clique no botão &quot;Aplicar&quot; na parte superior direita.

![aplicar à pasta criada](./images/prod-select-profile-folder.png)

Agora que fizemos a configuração necessária, vamos gerar nosso banner.

- Clique no logotipo AEM no canto superior esquerdo para abrir a navegação e navegue até Navegação \> Assets \> Arquivos.

![tela inicial do aem](./images/prod-select-assets.png)
![tela do aem assets](./images/prod-select-assets-2.png)

- Localize a pasta &quot;Generated Adobe Assets&quot; e abra-a clicando no cartão. É aqui que os banners gerados aparecerão.

![ativos de adobike gerados](./images/prod-generated-banners.png)

- Abra uma nova guia e acesse o AEM Assets novamente. Em seguida, navegue até a pasta à qual aplicamos o perfil de processamento.

- Na pasta, faça upload da imagem para a qual deseja criar um banner arrastando e soltando-o no navegador ou clicando em Criar \> Arquivos no canto superior direito da interface.

![carregar por meio da ação arrastar e soltar](./images/prod-drag-drop-banner.png)

![carregar usando criar arquivo](./images/prod-create-file.png)


- Aguarde um minuto para que seu ativo seja processado e, em seguida, recarregue sua tela. Se você vir seu ativo no estado &quot;Novo&quot;, saberá que o processamento foi concluído.

![ativo em novo estado](./images/prod-asset-processed.png)

- Navegue de volta para a guia anterior e recarregue a tela aqui também. Você deve observar um novo ativo no estado &quot;Novo&quot;. Este é o nosso banner gerado, todo do DAM! Ainda não está vendo? Aguarde mais um minuto e recarregue a tela.

![banner gerado](./images/prod-new-banner.png)

>[!NOTE]
>
> Não está satisfeito com o resultado? Aplique outro perfil de processamento à sua pasta e faça o upload do seu ativo novamente para gerar um banner diferente (ou faça upload de outro ativo, é claro). Durante o recarregamento, o sistema perguntará o que você deseja fazer com o ativo existente e selecionará &quot;Substituir&quot;.
> ![substituir existente](./images/prod-replace-asset.png)

Agora temos nosso banner gerado que podemos usar posteriormente durante a entrega da campanha. Certifique-se de publicar o banner selecionando-o e clicando no botão &quot;Publish rápido&quot; na faixa de opções.

![publicar ativo](./images/prod-publish-banner.png)

## Acompanhamento no Workfront

Se você precisar de um processo de revisão e aprovação formal e auditável do seu Assets, a Workfront é o local ideal.

>[!NOTE]
>
> Embora mencionemos isso aqui explicitamente, a intenção é atualizar as tarefas no Workfront após concluí-las. Você sempre deve se esforçar para um fluxo Criar > Revisar > Aprovar.

- Vamos voltar ao nosso projeto e expandir a opção &quot;Ir/Não ir Banner Review&quot; para abrir a referida tarefa clicando nela:

![banner ir/não ir](./images/banner-gonogo.png)

- Clique na seção de documentos da tarefa (coluna à esquerda) e clique na pasta vinculada &#39;Final&#39; do AEM Assets. Selecione o ativo clicando na zona e clique em &quot;Criar prova&quot;. Uma prova é a capacidade de revisar o conteúdo, por exemplo, imagem, texto, vídeo, site etc., de maneira estruturada e colaborativa, onde comentários, correções, modificações das partes interessadas envolvidas são coletados, versões e resultados podem ser comparados e aprovados finais gerados por um clique.

![criar prova](./images/wf-create-proof.png)

- Como queremos um processo de aprovação elaborado, selecione &quot;Prova avançada&quot;.

![prova avançada](./images/wf-advanced-proof.png)

>[!NOTE]
>
> Decidiremos manualmente quem revisará e/ou aprovará nossa prova nesta inicialização. Na maioria dos casos de uso reais, usaríamos um modelo predefinido de fluxo(s) de aprovação já definido(s) para cada tipo de prova.

- Por padrão, estamos em um tipo de fluxo de trabalho &quot;básico&quot; e vamos selecionar seu Especialista em Workfront Bootcamp como revisor e aprovador. Digite o nome do especialista em Workfront do Bootcamp onde está escrito &quot;Digite o nome do contato ou endereço de email para adicionar um recipient:

![atribuir prova](./images/wf-proof-assign.png)

![atribuir prova](./images/wf-assign-proof-2.png)

- Defina-os como &#39;Revisor e Aprovador&#39;:

![revisor e aprovador](./images/wf-review-approve.png)

- Clique em Criar prova. O Workfront levará alguns momentos para gerar a prova:

![gerando prova](./images/wf-generating-proof.png)

- Seu especialista da Workfront agora receberá uma nova notificação informando que ele tem uma prova para revisar e/ou aprovar:

![tarefa do workfront](./images/wf-proof-task.png)

- Depois de clicar na notificação, eles enfrentarão sua prova e poderão fazer alguns comentários e/ou aprovar esta prova.

   - Eles podem clicar em &quot;Adicionar comentário&quot; na parte superior da tela se tiverem observações:

  ![Adicionar comentário](./images/wf-proof-add-comment.png)

   - Eles poderão não apenas adicionar comentários, mas também usar a pequena barra de ferramentas de ponteiros para definir claramente qual área precisa ser alterada.

  ![Comentário sobre o ponto de fixação](./images/wf-proof-comment.png)

   - Ao adicionar o comentário, eles podem informar que você precisa fazer algum trabalho extra em uma nova versão da prova. Atualize sua guia Workfront e você terá uma nova notificação informando exatamente isso. Depois de saber quais alterações você precisa fazer, faça as alterações no AEM e, em seguida, acesse e faça upload da sua nova versão aqui:

  ![carregar nova versão](./images/wf-upload-version.png)

   - Selecione o ativo atualizado (se nenhuma alteração for necessária no cenário de bootcamp, carregue o mesmo ativo novamente) e clique em &quot;Link&quot;:

  ![vincular ativo](./images/wf-link-new-asset.png)

   - Em seguida, clique em &quot;criar prova&quot; no lado direito.

  ![criar prova](./images/create-new-proof.png)

   - Depois que a prova for gerada (isso pode levar alguns minutos), seu especialista em Workfront receberá uma notificação e poderá revisar e aprovar essa nova versão.  Por exemplo, usando o botão de comparação de prova, é possível ver uma comparação lado a lado de V1 e V2 com todos os comentários feitos.

  ![comparação de prova](./images/wf-proof-compare.png)

  ![tomar uma decisão](./images/make-decision-proof.png)

  ![aprovado](./images/approved.png)

Agora temos uma aprovação formal para usar nosso banner. É fácil seguir onde estamos no processo e as atualizações que você faz acionam notificações automaticamente para que você possa trabalhar da maneira mais eficiente possível.

Próxima Etapa: [Fase 2 - Produção: Criar anúncio de mídia social](./social.md)

[Voltar à Fase 1 - Planejamento: Outro pré-trabalho](../planning/prework.md)

[Voltar a todos os módulos](../../overview.md)
