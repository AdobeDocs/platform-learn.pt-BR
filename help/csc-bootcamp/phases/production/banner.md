---
title: CSC Bootcamp - Criar banner da página inicial do produto
description: CSC Bootcamp - Criar banner da página inicial do produto
doc-type: multipage-overview
source-git-commit: 989e4e2add1d45571462eccaeebcbe66a77291db
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 0%

---

# Criar banner da página inicial do produto

## Produção do banner

A automação de conteúdo traz o poder do Adobe Creative Cloud para a Experience Manager Assets, dando aos profissionais de marketing a capacidade de automatizar a produção de ativos em escala, acelerando consideravelmente a criação de variações. Vamos usar essas funcionalidades para gerar um banner para ser usado na página inicial!

- Acesse o autor do AEM em [https://author-p105462-e991028.adobeaemcloud.com/](https://author-p105462-e991028.adobeaemcloud.com/) e faça logon com as credenciais que fornecemos.

- Na página inicial, navegue até Ferramentas > Ativos \> Perfis de processamento.

![Ferramentas > Ativos > Perfis de processamento](./images/prod-processing-profiles.png)

- Na interface, você verá todos os perfis de processamento existentes. Eles podem ser usados para ativar determinadas automações.

![lista de perfis de processamento](./images/prod-profile-list.png)


- Os seguintes são de seu interesse:
   - Adobike Banner Dark: cria um banner da Adobe com uma sobreposição escura, com base no ativo selecionado
      ![banner escuro](./images/prod-banner-dark.jpg)
   - Luz do banner da Adobike: cria um banner da Adobe com uma sobreposição de luz, com base no ativo selecionado
      ![banner de luz](./images/prod-banner-light.jpg)
   - Adobike Banner Green: cria um banner da Adobe com uma sobreposição verde, com base no ativo selecionado
      ![banner verde](./images/prod-banner-green.jpg)

- Depois de escolher o tipo de banner que deseja criar, selecione o perfil de processamento e selecione &quot;Aplicar perfil às pastas&quot;.

![aplicar perfil à pasta](./images/prod-apply-profile.png)

- Na próxima tela, navegue até a pasta da sua equipe no AEM Assets. Em seguida, no canto superior esquerdo, selecione o botão &quot;Criar&quot; para criar uma nova pasta e dar a ela um nome significativo, por exemplo &quot;Criar banner escuro&quot;.

![criar pasta](./images/prod-create-profile-folder.png)

![criar detalhes da pasta](./images/prod-profile-folder-details.png)

- Depois de criar a pasta, marque a caixa ao lado de seu nome e clique no botão &quot;Aplicar&quot; na parte superior direita.

![aplicar à pasta criada](./images/prod-select-profile-folder.png)

Agora que fizemos a configuração necessária, vamos gerar nosso banner.

- Clique no logotipo AEM no canto superior esquerdo para abrir a navegação e navegue até Navegação \> Arquivos de ativos \>.

![tela inicial do aem](./images/prod-select-assets.png)
![tela do aem assets](./images/prod-select-assets-2.png)

- Localize a pasta &quot;Generated Adobike Assets&quot; e abra-a clicando no cartão . É aqui que os banners gerados aparecerão.

![ativos adobike gerados](./images/prod-generated-banners.png)

- Abra uma nova guia e Navegue até o AEM Assets novamente. Em seguida, navegue até a pasta na qual aplicamos o perfil de processamento.

- Na pasta , faça upload da imagem para a qual você deseja criar um banner arrastando-o e soltando-o em seu navegador ou clicando em Criar arquivos \> no canto superior direito da interface.

![fazer upload arrastando e soltando](./images/prod-drag-drop-banner.png)

![fazer upload usando criar arquivo](./images/prod-create-file.png)


- Aguarde um minuto para que o ativo processe e recarregue a tela. Se você vir seu ativo no estado &quot;Novo&quot;, você sabe que ele terminou de ser processado.

![ativo em novo estado](./images/prod-asset-processed.png)

- Navegue de volta à guia anterior e recarregue a tela aqui também. Você deve notar um novo ativo no estado &quot;Novo&quot;. Este é o nosso banner gerado, todo do DAM! Ainda não o vê? Aguarde mais um minuto e recarregue sua tela.

![banner gerado](./images/prod-new-banner.png)

>[!NOTE]
>
> Não está satisfeito com o resultado? Aplique outro perfil de processamento à sua pasta e faça upload novamente do ativo para gerar um banner diferente (ou faça upload de outro ativo, é claro). Durante o recarregamento, o sistema perguntará o que você deseja fazer com o ativo existente, selecione &quot;Substituir&quot;.
> ![substituir existente](./images/prod-replace-asset.png)

Agora temos nosso banner gerado que podemos usar posteriormente durante a entrega de nossa campanha. Certifique-se de publicar o banner selecionando-o e clicando no botão &quot;Publicação rápida&quot; na faixa.

![publicar ativo](./images/prod-publish-banner.png)

## Acompanhamento no Workfront

Se você precisar de um processo formal e auditável de revisão e aprovação de seus ativos, o Workfront é o local certo.

>[!NOTE]
>
> Embora o mencionemos explicitamente, é intenção atualizar as tarefas no Workfront após sua conclusão. Você sempre deve se esforçar por um fluxo Criar > Revisar > Aprovar .

- Vamos voltar ao nosso projeto e expandir a opção &quot;Ir/Não ir análise do banner&quot; para abrir a tarefa em questão clicando nela:

![banner go/no go](./images/banner-gonogo.png)

- Clique na seção documentos da tarefa (coluna à esquerda) e na pasta vinculada do AEM Assets &#39;Final&#39;. Selecione o ativo clicando na zona e em &quot;Criar prova&quot;. Uma prova é a capacidade de revisar conteúdo, por exemplo, imagem, texto, vídeo, site, etc., de forma estruturada e colaborativa, onde são coletados comentários, correções, modificações dos participantes envolvidos, versões e resultados podem ser comparados e aprovados definitivamente por um clique.

![criar prova](./images/wf-create-proof.png)

- Como queremos um processo de aprovação elaborado, selecione &quot;Prova avançada&quot;.

![prova avançada](./images/wf-advanced-proof.png)

>[!NOTE]
>
> Vamos decidir manualmente quem vai revisar e/ou aprovar nossa prova neste campo de bootcamp. Na maioria dos casos de uso reais, usaríamos um modelo predefinido de fluxo(s) de aprovação já definido para cada tipo de prova.

- Por padrão, estamos em um tipo de fluxo de trabalho &quot;básico&quot; e vamos selecionar seu Especialista em Bootcamp Workfront como revisor e aprovador. Digite o nome do especialista do Workfront do Bootcamp, onde diz &quot;Digite o nome do contato ou o endereço de email para adicionar um recipient:

![atribuir prova](./images/wf-proof-assign.png)

![atribuir prova](./images/wf-assign-proof-2.png)

- Defina-os como &quot;Revisor e Aprovador&quot;:

![revisor e aprovador](./images/wf-review-approve.png)

- Clique em &quot;Criar prova&quot;. O Workfront levará alguns minutos para gerar a prova:

![gerando prova](./images/wf-generating-proof.png)

- Seu especialista do Workfront receberá uma nova notificação informando que ele tem uma prova para revisar e/ou aprovar:

![tarefa de frente de trabalho](./images/wf-proof-task.png)

- Depois de clicar na notificação, eles enfrentarão sua prova e poderão fazer alguns comentários e/ou aprovar essa prova.

   - Eles podem clicar em &quot;Adicionar comentário&quot; na parte superior da tela, se tiverem comentários:

   ![Adicionar comentário](./images/wf-proof-add-comment.png)

   - Poderão então não só adicionar comentários, mas também usar a pequena barra de ferramentas de ponteiros para definir claramente qual área precisa mudar.

   ![Comentário do ponto de fixação](./images/wf-proof-comment.png)

   - Ao adicionar o comentário, é possível informá-lo de que é necessário fazer algum trabalho extra em uma nova versão da prova. Atualize a guia Workfront e você terá uma nova notificação informando exatamente isso. Depois de saber quais alterações você precisa fazer, faça suas alterações no AEM e faça o upload da nova versão aqui:

   ![fazer upload de nova versão](./images/wf-upload-version.png)

   - Selecione o ativo atualizado (se nenhuma alteração for necessária no cenário de bootcamp, basta fazer upload do mesmo ativo novamente) e clique em &quot;Link&quot;:

   ![vincular ativo](./images/wf-link-new-asset.png)

   - Em seguida, clique em &quot;criar prova&quot; no lado direito.

   ![criar prova](./images/create-new-proof.png)

   - Depois que a prova for gerada (isso pode demorar alguns minutos), o Especialista Workfront receberá uma notificação e poderá revisar e aprovar essa nova versão.  Por exemplo, usando o botão de comparação de prova, é possível ver uma comparação lado a lado de V1 e V2 com todos os comentários feitos.

   ![comparação de prova](./images/wf-proof-compare.png)

   ![tomar decisão](./images/make-decision-proof.png)

   ![aprovado](./images/approved.png)

Agora temos uma aprovação formal para o uso do nosso banner. É fácil seguir onde estamos no processo e as atualizações que você aciona automaticamente as notificações, para que você possa trabalhar da maneira mais eficiente possível.

Próxima etapa: [Fase 2 - Produção: Criar anúncio de mídia social](./social.md)

[Retorne à Fase 1 - Planejamento: Outro pré-trabalho](../planning/prework.md)

[Voltar para todos os módulos](../../overview.md)
