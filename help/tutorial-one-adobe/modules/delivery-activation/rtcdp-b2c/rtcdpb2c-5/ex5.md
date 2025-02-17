---
title: Coleta de dados e encaminhamento de eventos - Encaminhe os eventos para o ecossistema da AWS
description: Encaminhar eventos para o ecossistema do AWS
kt: 5342
doc-type: tutorial
exl-id: 9b5f1466-d173-40a0-beed-d4e859e64e40
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '1571'
ht-degree: 3%

---

# 2.5.5 Encaminhar eventos para o AWS Kinesis e o AWS S3

>[!IMPORTANT]
>
>A conclusão deste exercício é opcional e envolve um custo para usar o AWS Kinesis. Embora a AWS forneça uma conta de camada gratuita que permite testar e configurar muitos serviços sem um custo, o AWS Kinesis não faz parte dessa conta de camada gratuita. Portanto, para implementar e testar esse exercício, um custo será envolvido para usar o AWS Kinesis.

## É bom saber

O Adobe Experience Platform oferece suporte a vários serviços da Amazon como destino.
Kinesis e S3 são [destinos de exportação de perfil](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en) e podem ser usados como parte do Real-Time CDP da Adobe Experience Platform.
Você pode alimentar facilmente eventos de segmento de alto valor e atributos de perfil associados em seus sistemas de escolha.

Neste exercício, você aprenderá a configurar seu próprio fluxo do Amazon Kinesis para transmitir dados do evento provenientes do ecossistema do Adobe Experience Platform Edge para um destino de armazenamento na nuvem, como o Amazon S3. Isso é útil caso você queira coletar eventos de experiência de propriedades da Web e de dispositivos móveis e enviá-los para o seu datalake para análise e relatórios operacionais. As soluções de dados geralmente assimilam dados em lote com grandes importações diárias de arquivos. Elas não expõem o endpoint http público que pode ser usado em conjunto com o encaminhamento de eventos.

O suporte aos casos de uso acima implica que os dados transmitidos precisam ser armazenados em buffer ou colocados em uma fila antes de serem gravados em um arquivo. Tenha cuidado para não abrir arquivos para acesso de gravação em vários processos. Delegar esta tarefa para sistema dedicado é ideal para escalar bem, garantindo um grande nível de serviço, é aqui que Kinesis vem para o resgate.

O Amazon Kinesis Data Streams concentra-se na assimilação e no armazenamento de fluxos de dados. O Kinesis Data Firehose concentra no fornecimento de fluxos de dados para destinos selecionados, como buckets do S3.

Como parte desse exercício, você...

- Executar uma configuração básica de um fluxo de dados Kinesis
- Criar um fluxo de entrega do Firehose e usar o bucket do S3 como destino
- Configure o gateway da API do Amazon como um endpoint da API rest para receber os dados do evento
- Encaminhar dados brutos do evento do Edge do Adobe para o fluxo do Kinesis

## Configurar o bucket do AWS S3

Vá para [https://console.aws.amazon.com](https://console.aws.amazon.com) e entre com sua conta da Amazon.

![ETL](./../../../../modules/delivery-activation/rtcdp-b2c/rtcdpb2c-3/images/awshome.png)

Depois de fazer logon, você será redirecionado para o **Console de Gerenciamento do AWS**.

![ETL](./../../../../modules/delivery-activation/rtcdp-b2c/rtcdpb2c-3/images/awsconsole.png)

No menu **Localizar Serviços**, procure **s3**. Clique no primeiro resultado da pesquisa: **S3 - Armazenamento Escalável na Nuvem**.

![ETL](./../../../../modules/delivery-activation/rtcdp-b2c/rtcdpb2c-3/images/awsconsoles3.png)

Você verá a página inicial do **Amazon S3**. Clique em **Criar bloco**.

![ETL](./../../../../modules/delivery-activation/rtcdp-b2c/rtcdpb2c-3/images/s3home.png)

Na tela **Criar bloco**, você precisa configurar dois itens:

- Nome: use o nome `eventforwarding---aepUserLdap--`.

![ETL](./images/bucketname.png)

Deixe todas as outras configurações padrão como estão. Role para baixo e clique em **Criar bloco**.

![ETL](./images/createbucket.png)

Você verá seu bucket ser criado e será redirecionado para a página inicial do Amazon S3.

![ETL](./images/S3homeb.png)

## Configurar o fluxo de dados do AWS Kinesis

No menu **Localizar Serviços**, procure **kinesis**. Clique no primeiro resultado da pesquisa: **Kinesis - Trabalhar com dados de transmissão em tempo real**.

![ETL](./images/kinesis1.png)

Selecione **Fluxos De Dados Kinesis**. Clique em **Criar fluxo de dados**.

![ETL](./images/kinesis2.png)

Para o **Nome do fluxo de dados**, use `--aepUserLdap---datastream`.

![ETL](./images/kinesis3.png)

Não há necessidade de alterar nenhuma das outras configurações. Role para baixo e clique em **Criar fluxo de dados**.

![ETL](./images/kinesis4.png)

Você verá isso. Depois que o fluxo de dados for criado com êxito, você poderá avançar para o próximo exercício.

![ETL](./images/kinesis5.png)

## Configurar o fluxo de entrega do AWS Firehose

No menu **Localizar Serviços**, procure **kinesis**. Clique em **Fogão de Dados Kinesis**.

![ETL](./images/kinesis6.png)

Clique em **Criar fluxo do Firehose**.

![ETL](./images/kinesis7.png)

Para **Source**, selecione **Amazon Kinesis Data Streams**. Para **Destino**, selecione **Amazon S3**. Clique em **Procurar** para selecionar seu fluxo de dados.

![ETL](./images/kinesis8.png)

Selecione o fluxo de dados. Clique em **Escolher**.

![ETL](./images/kinesis9.png)

Você verá isso. Lembre-se do **nome do fluxo do Firehose**, pois ele será necessário posteriormente.

![ETL](./images/kinesis10.png)

Role para baixo até ver **Configurações de destino**. Clique em **Procurar** para selecionar seu bucket do S3.

![ETL](./images/kinesis11.png)

Selecione seu bucket de S3 e clique em **Escolher**.

![ETL](./images/kinesis12.png)

Então você verá algo assim. Atualize as seguintes configurações:

- Novo delimitador de linha: definido como **Habilitado**
- Particionamento dinâmico: definido como **Não habilitado**

![ETL](./images/kinesis13.png)

Role para baixo um pouco mais e clique em **Criar fluxo do Firehose**

![ETL](./images/kinesis15.png)

Após alguns minutos, o fluxo do Firehose será criado e **ficará ativo**.

![ETL](./images/kinesis16.png)

## Criar usuário do IAM

No menu esquerdo do AWS IAM, clique em **Usuários**. Você verá a tela **Usuários**. Clique em **Criar usuário**.

![ETL](./images/iammenu.png)

Em seguida, configure o usuário:

- Nome de Usuário: use `--aepUserLdap--_kinesis_forwarding`

Clique em **Next**.

![ETL](./images/configuser.png)

Em seguida, você verá essa tela de permissões. Clique em **Anexar políticas diretamente**.

Insira o termo de pesquisa **kinesisfirehose** para ver todas as políticas relacionadas. Selecione a política **AmazonKinesisFirehoseFullAccess**. Role para baixo e clique em **Próximo**.

![ETL](./images/perm2.png)

Revise sua configuração. Clique em **Criar Usuário**.

![ETL](./images/review.png)

Você verá isso. Clique em **Exibir Usuário**.

![ETL](./images/review1.png)

Clique em **Adicionar permissões** e em **Criar política embutida**.

![ETL](./images/pol1.png)

Você verá isso. Selecione o serviço **Kinesis**.

![ETL](./images/pol2.png)

Vá para **Gravar** e marque a caixa de seleção **ColocarRegistro**.

![ETL](./images/pol3.png)

Role para baixo até **Recursos** e selecione **Todos**. Clique em **Next**.

![ETL](./images/pol4.png)

Nomeie sua política como esta: **Kinesis_PutRecord** e clique em **Criar política**.

![ETL](./images/pol5.png)

Você verá isso. Clique em **Credenciais de segurança**.

![ETL](./images/pol6.png)

Clique em **Criar chave de acesso**.

![ETL](./images/cred.png)

Selecione o **Aplicativo em execução fora do AWS**. Role para baixo e clique em **Próximo**.

![ETL](./images/creda.png)

Clique em **Criar chave de acesso**

![ETL](./images/credb.png)

Você verá isso. Clique em **Mostrar** para ver sua chave de acesso secreta:

![ETL](./images/cred1.png)

Sua **Chave de acesso secreta** está sendo mostrada agora.

>[!IMPORTANT]
>
>Armazene suas credenciais em um arquivo de texto no computador.
>
> - ID da chave de acesso: ...
> - Chave de acesso secreta: ...
>
> Depois de clicar em **Concluído**, você nunca verá suas credenciais novamente!

Clique em **Concluído**.

![ETL](./images/cred2.png)

Agora você criou um usuário do IAM com as permissões apropriadas, que você precisará especificar ao configurar a extensão do AWS na propriedade de encaminhamento de eventos.

## Atualize sua propriedade de encaminhamento de eventos: Extensão

Com seu Segredo e Elemento de dados configurados, agora é possível configurar a extensão para a Google Cloud Platform na propriedade Encaminhamento de eventos.

Vá para [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/), vá para **Encaminhamento de Eventos** e abra sua propriedade de Encaminhamento de Eventos.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/prop1.png)

Em seguida, vá para **Extensões**, para **Catálogo**. Clique na extensão **AWS** e em **Instalar**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/awsext1.png)

Insira as credenciais de usuário do IAM geradas no exercício anterior. Clique em **Salvar**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/awsext2.png)

Em seguida, é necessário configurar uma regra que inicie o encaminhamento dos dados do evento para o Kinesis.

## Atualizar a propriedade de encaminhamento de eventos: Regra

No menu esquerdo, vá para **Regras**. Clique para abrir a regra **Todas as páginas** que você criou em um dos exercícios anteriores.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rlaws1.png)

Você verá isso. Clique no ícone **+** para adicionar uma nova ação.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rlaws2.png)

Você verá isso. Faça a seguinte seleção:

- Selecione a **Extensão**: **AWS**
- Selecione o **Tipo de ação**: **Enviar dados para o fluxo de dados Kinesis**
- Nome: **AWS - Enviar Dados para o Fluxo de Dados Kinesis**

Agora você deve ver isso:

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rlaws4.png)

Em seguida, configure o seguinte:

- Nome do Fluxo: `--aepUserLdap---datastream`
- Região do AWS: verifique sua região na configuração do Fluxo de dados do AWS
- Chave de Partição: **0**

Você pode ver sua região do AWS aqui:

![SSF da Coleção de Dados do Adobe Experience Platform](./images/partkey.png)

Agora você deve ter isso. Em seguida, clique no ícone do elemento de dados do campo **Dados**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rlaws5.png)

Selecione **Evento XDM** e clique em **Selecionar**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rlaws5a.png)

Então você terá isto. Clique em **Manter alterações**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rlaws5b.png)

Você verá isso. Clique em **Salvar**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rlaws7.png)

Vá para **Fluxo de Publicação** para publicar suas alterações.
Abra a biblioteca de desenvolvimento clicando em **Principal**.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rlaws11.png)

Clique no botão **Adicionar todos os recursos alterados**, após o qual você verá suas alterações de Regra e Elemento de Dados aparecerem nesta biblioteca. Em seguida, clique em **Salvar e criar para desenvolvimento**. Suas alterações estão sendo implantadas.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rlaws13.png)

Após alguns minutos, você verá que a implantação foi concluída e está pronta para ser testada.

![SSF da Coleção de Dados do Adobe Experience Platform](./images/rl14.png)

## Testar sua configuração

Ir para [https://dsn.adobe.com](https://dsn.adobe.com). Depois de fazer logon com sua Adobe ID, você verá isso. Clique nos 3 pontos **...** do projeto do site e clique em **Executar** para abri-lo.

![DSN](./../../datacollection/dc1.1/images/web8.png)

Você verá seu site de demonstração aberto. Selecione o URL e copie-o para a área de transferência.

![DSN](../../../getting-started/gettingstarted/images/web3.png)

Abra uma nova janela incógnita do navegador.

![DSN](../../../getting-started/gettingstarted/images/web4.png)

Cole o URL do site de demonstração que você copiou na etapa anterior. Você será solicitado a fazer logon usando sua Adobe ID.

![DSN](../../../getting-started/gettingstarted/images/web5.png)

Selecione o tipo de conta e conclua o processo de logon.

![DSN](../../../getting-started/gettingstarted/images/web6.png)

Em seguida, você verá seu site carregado em uma janela incógnita do navegador. Para cada exercício, será necessário usar uma janela do navegador nova e incógnita para carregar o URL do site de demonstração.

![DSN](../../../getting-started/gettingstarted/images/web7.png)

Mudar sua exibição para **AWS**. Ao abrir seu fluxo de dados e entrar na guia **Monitoramento**, você verá o tráfego de entrada.

![Configuração da Coleção de Dados do Adobe Experience Platform](./images/hookaws3.png)

Ao abrir o fluxo do Data Firehose e ir para a guia **Monitoramento**, você também verá o tráfego de entrada.

![Configuração da Coleção de Dados do Adobe Experience Platform](./images/hookaws4.png)

Por fim, ao examinar o S3 bucket, agora você notará arquivos que estão sendo criados nele como consequência da assimilação de dados.

![Configuração da Coleção de Dados do Adobe Experience Platform](./images/hookaws5.png)

Ao baixar esse arquivo e abri-lo usando um editor de texto, você verá que ele contém a carga XDM dos eventos que foram encaminhados.

![Configuração da Coleção de Dados do Adobe Experience Platform](./images/hookaws6.png)

>[!IMPORTANT]
>
>Assim que a configuração estiver funcionando como esperado, não se esqueça de desligar seu AWS Kinesis Data Stream e Data Firehose para evitar ser cobrado!

## Próximas etapas

Ir para [Resumo e benefícios](./summary.md){target="_blank"}

Voltar para [Conexões do Real-Time CDP: Encaminhamento de Eventos](./aep-data-collection-ssf.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
