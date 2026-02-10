---
title: Criar ativos e modelo de mídia dinâmica
description: Criar ativos e modelo de mídia dinâmica
kt: 5342
doc-type: tutorial
exl-id: 3867f23b-9b88-4971-a892-5821800e39ac
source-git-commit: 8f746831d4a1481f8ccc14539273c4b16ca5170b
workflow-type: tm+mt
source-wordcount: '2241'
ht-degree: 1%

---

# 1.4.1 Criar ativos e modelo de mídia dinâmica

>[!IMPORTANT]
>
>Para concluir este exercício, você precisa ter acesso a um ambiente de trabalho do AEM Assets CS Author com o AEM Assets Dynamic Media habilitado.
>
>Se você não tiver um ambiente como esse, acesse [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Siga as instruções aqui e você terá acesso a esse ambiente.

>[!IMPORTANT]
>
>Se você tiver configurado anteriormente um Programa AEM CS com um ambiente AEM Assets CS, pode ser que sua sandbox AEM CS tenha hibernado. Considerando que a deshibernação de uma sandbox desse tipo leva de 10 a 15 minutos, seria uma boa ideia iniciar o processo de deshibernação agora para que você não precise aguardar mais tarde.

## 1.4.1.1 Criar sua empresa do Dynamic Media

Ir para [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. A organização que você deve selecionar é `--aepImsOrgName--`.

![AEM Assets Dynamic Media](./images/aaemassdmcomp1.png)

Role para baixo até **Empresas do Dynamic Media**. Clique no ícone **+** para criar uma nova Empresa do Dynamic Media.

![AEM Assets Dynamic Media](./images/aaemassdmcomp2.png)

Insira a seguinte informação:

- **Nome da empresa**: `--aepUserLdap---CitiSignal`.
- **Região da empresa**: selecione a região mais próxima de você.
- **Emails de administrador da empresa**: digite seu email de administrador.

Clique em **Criar**.

![AEM Assets Dynamic Media](./images/aaemassdmcomp3.png)

Você deverá ver isso.

![AEM Assets Dynamic Media](./images/aaemassdmcomp4.png)

Agora você deve receber um email como o abaixo, que contém sua senha temporária. Para alterar sua senha ou recuperá-la caso não tenha recebido um email, você deve instalar o **aplicativo de desktop do Adobe Dynamic Media Classic**. Você pode encontrar instruções de instalação aqui: [https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app).

Siga as instruções e volte aqui depois que o aplicativo estiver instalado no sistema.

Abra o **aplicativo de desktop do Adobe Dynamic Media Classic**. Se você sabe sua senha, digite-a aqui e siga as instruções para alterá-la no primeiro logon.

Se você não souber sua senha, clique no link **Esqueceu sua senha** e siga as instruções para redefini-la, para voltar aqui e fazer logon.

![AEM Assets Dynamic Media](./images/aaemassdmcomp5.png)

Depois de fazer logon, você verá uma tela semelhante a esta.

![AEM Assets Dynamic Media](./images/aaemassdmcomp6.png)

## 1.4.1.2 Configurar o Dynamic Media no AEM

Ir para [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. A organização que você deve selecionar é `--aepImsOrgName--`.

Clique para abrir seu Programa Cloud Manager, que deve ser chamado de `--aepUserLdap-- - CitiSignal AEM+ACCS`.

![AEM Assets Dynamic Media](./images/accsaemassets1.png)

Clique em seu ambiente.

![AEM Assets Dynamic Media](./images/accsaemassets3.png)

Clique no URL do seu ambiente.

![AEM Assets Dynamic Media](./images/accsaemassets2.png)

Vá para **Ferramentas**, para **Cloud Services** e depois para **Configuração do Dynamic Media**.

![AEM Assets Dynamic Media](./images/accsaemassets4.png)

Selecione **Global** (não marque a caixa de seleção) e clique em **Criar**.

![AEM Assets Dynamic Media](./images/accsaemassets5.png)

Insira a seguinte informação:

- **Título**: use este título: `--aepUserLdap-- - CitiSignal`.
- **Email**: digite seu endereço de email.
- **Senha**: digite a senha da conta do Dynamic Media
- **Região**: selecione a região escolhida ao criar sua empresa do Dynamic Media, neste exemplo, **Europa**.

Clique em **Conectar ao Dynamic Media**.

![AEM Assets Dynamic Media](./images/accsaemassets6.png)

Você deverá ver isso. Configure o seguinte:

- Selecione a **Empresa**: `--aepUserLdap-- - CitiSignal`.
- Defina **Publicar Assets** como **Imediato**.
- Marque a caixa de seleção para **Sincronizar todo o conteúdo**.

Clique em **Salvar**.

![AEM Assets Dynamic Media](./images/accsaemassets7.png)

A configuração do Dynamic Media está concluída. Clique em **OK**.

![AEM Assets Dynamic Media](./images/accsaemassets8.png)

## 1.4.1.3 Exportar seus ativos

Baixe este arquivo [citisignal-fiber-max-is-coming.psd](./assets/citisignal-fiber-max-is-coming.psd){target="_blank"} e abra-o com o Adobe Photoshop.

Você deverá ver isso. A CitiSignal está planejando a implantação do Fiber Max em três cidades: Nova York, Paris e Dubai.

Ao mostrar ou ocultar camadas específicas, é possível visualizar a imagem criada pelos designers.

Abaixo estão as instruções para exportar os arquivos de imagem do modelo do Photoshop PSD. Se preferir, você também pode baixar as imagens concluídas aqui [citisignal-dm-email-assets.zip](./assets/citisignal-dm-email-assets.zip){target="_blank"} e descompactar o arquivo na área de trabalho.

Esta é a versão para Nova Iorque.

![AEM Assets Dynamic Media](./images/aemdm1.png)

Esta é a versão para Dubai.

![AEM Assets Dynamic Media](./images/aemdm2.png)

Esta é a versão para Paris.

![AEM Assets Dynamic Media](./images/aemdm3.png)

Provavelmente, haverá muitas outras cidades para as quais o CitiSignal lançará o Fiber Max no futuro, novas camadas poderão ser criadas neste arquivo. Por enquanto, o foco está nas 3 cidades já mencionadas.

Para usar essas variações em combinação com o AEM Assets Dynamic Media, as camadas de cada cidade devem ser exportadas como imagens separadamente sem o arquivo de plano de fundo, e outra exportação deve ser feita para a camada de plano de fundo sem incluir cidades.

Agora, você deve ocultar e mostrar apenas uma das camadas. A primeira camada a ser mostrada é a **Paris**, e todas as outras camadas devem ficar ocultas.

Para exportar essa camada, vá para **Arquivo** > **Exportar** > **Exportar como...**.

![AEM Assets Dynamic Media](./images/aemdm4.png)

Você deverá ver isso. Selecione o tipo de arquivo **PNG**, verifique se a **Transparência** está habilitada e clique em **Exportar**.

![AEM Assets Dynamic Media](./images/aemdm5.png)

Altere o nome do arquivo para `citisignal-fiber-max-is-coming-paris.png`e clique em **Exportar**.

![AEM Assets Dynamic Media](./images/aemdm6.png)

A próxima camada a ser exibida é a **camada Dubai**, e todas as outras camadas devem ficar ocultas.

Para exportar essa camada, vá para **Arquivo** > **Exportar** > **Exportar como...**.

![AEM Assets Dynamic Media](./images/aemdm4a.png)

Você deverá ver isso. Selecione o tipo de arquivo **PNG**, verifique se a **Transparência** está habilitada e clique em **Exportar**.

![AEM Assets Dynamic Media](./images/aemdm5a.png)

Altere o nome do arquivo para `citisignal-fiber-max-is-coming-dubai.png`e clique em **Exportar**.

![AEM Assets Dynamic Media](./images/aemdm6a.png)

A próxima camada a ser mostrada é a camada **Nova York**, e todas as outras camadas devem ficar ocultas.

Para exportar essa camada, vá para **Arquivo** > **Exportar** > **Exportar como...**.

![AEM Assets Dynamic Media](./images/aemdm4b.png)

Você deverá ver isso. Selecione o tipo de arquivo **PNG**, verifique se a **Transparência** está habilitada e clique em **Exportar**.

![AEM Assets Dynamic Media](./images/aemdm5b.png)

Altere o nome do arquivo para `citisignal-fiber-max-is-coming-newyork.png`e clique em **Exportar**.

![AEM Assets Dynamic Media](./images/aemdm6b.png)

A próxima camada a ser mostrada é a camada **de plano de fundo**, e todas as outras camadas devem ficar ocultas.

Para exportar essa camada, vá para **Arquivo** > **Exportar** > **Exportar como...**.

![AEM Assets Dynamic Media](./images/aemdm4c.png)

Você deverá ver isso. Selecione o tipo de arquivo **PNG**, verifique se a **Transparência** está habilitada e clique em **Exportar**.

![AEM Assets Dynamic Media](./images/aemdm5c.png)

Altere o nome do arquivo para `citisignal-fiber-max-is-coming-background`e clique em **Exportar**.

![AEM Assets Dynamic Media](./images/aemdm6c.png)

Em seguida, você deve ter esses arquivos disponíveis no local de exportação selecionado.

![AEM Assets Dynamic Media](./images/aemdm7.png)

## 1.4.1.4 Carregue seus ativos para o AEM Assets CS

Ir para [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Ir para **Experience Manager Assets**.

![AEM Assets Dynamic Media](./images/aemdm8.png)

Selecione seu repositório, que deve se chamar `--aepUserLdap-- - CitiSignal AEM + ACCS`.

![AEM Assets Dynamic Media](./images/aemdm9.png)

Vá para **Assets** e clique em **Criar Pasta**.

![AEM Assets Dynamic Media](./images/aemdm10.png)

Para a pasta, use o nome: `--aepUserLdap-- - CitiSignal Dynamic Media`. Clique em **Criar**.

![AEM Assets Dynamic Media](./images/aemdm11.png)

Clique duas vezes para abrir a pasta que acabou de criar.

![AEM Assets Dynamic Media](./images/aemdm12.png)

Clique em **Adicionar Assets**.

![AEM Assets Dynamic Media](./images/aemdm13.png)

Clique em **Procurar** e selecione **Procurar Arquivos**.

![AEM Assets Dynamic Media](./images/aemdm15.png)

Selecione os 4 arquivos PNG exportados na etapa anterior.

![AEM Assets Dynamic Media](./images/aemdm16.png)

Clique em **Carregar**.

![AEM Assets Dynamic Media](./images/aemdm17.png)

Suas imagens agora estão disponíveis no AEM Assets CS.

![AEM Assets Dynamic Media](./images/aemdm18.png)

Aguarde alguns minutos e abra o **aplicativo de desktop do Adobe Dynamic Media Classic**. Você também deve ver as imagens carregadas disponíveis no Dynamic Media.

![AEM Assets Dynamic Media](./images/aemdm19.png)

## 1.4.1.5 Configurar o modelo do Dynamic Media

No menu esquerdo, vá para **Dynamic Media Assets**. Clique para abrir sua pasta `--aepUserLdap-- - CitiSignal Dynamic Media`. Em seguida, clique em **Criar modelo**.

![AEM Assets Dynamic Media](./images/aemdm20.png)

Insira a seguinte informação:

- **Nome do Modelo**: `--aepUserLdap-- - CitiSignal Fiber Max Launch Email Assets`
- **Largura da Tela**: `600px`
- **Altura da Tela de Pintura**: `600px`

Clique em **Criar**.

![AEM Assets Dynamic Media](./images/aemdm21.png)

Você deverá ver isso. Clique no ícone **Adicionar imagem**.

![AEM Assets Dynamic Media](./images/aemdm22.png)

Arraste o arquivo **citisignal-fiber-max-is-coming_citisignal-background.png** para a tela e ajuste-o à tela.

![AEM Assets Dynamic Media](./images/aemdm23.png)

Em seguida, arraste o arquivo **citisignal-fiber-max-is-coming_citisignal-newyork.png** para a tela e ajuste-o à tela.

![AEM Assets Dynamic Media](./images/aemdm24.png)

Em seguida, arraste o arquivo **citisignal-fiber-max-is-coming_citisignal-dubai.png** para a tela e ajuste-o à tela.

![AEM Assets Dynamic Media](./images/aemdm25.png)

Em seguida, arraste o arquivo **citisignal-fiber-max-is-coming_citisignal-paris.png** para a tela e ajuste-o à tela.

![AEM Assets Dynamic Media](./images/aemdm26.png)

Agora, você tem todas as três variações no modelo como camadas distintas ao mesmo tempo. Você pode mostrar/ocultar camadas específicas clicando no ícone **camadas**, no qual você vê que todas as camadas estão visíveis no momento.

![AEM Assets Dynamic Media](./images/aemdm27.png)

Ocultando algumas camadas, é possível controlar a aparência da imagem. Neste exemplo, somente a camada de **Paris** e a camada de plano de fundo estão visíveis.

![AEM Assets Dynamic Media](./images/aemdm28.png)

Em seguida, é necessário adicionar uma camada de texto. Clique no ícone da **camada de texto**.

![AEM Assets Dynamic Media](./images/aemdm29.png)

Você deverá ver isso.

![AEM Assets Dynamic Media](./images/aemdm30.png)

Fique à vontade para adaptar o campo de texto da maneira que você desejar, este é um exemplo. Não se esqueça de habilitar a opção **Redimensionamento do Texto Inteligente** para que o texto real inserido em um estágio posterior pareça correto.

![AEM Assets Dynamic Media](./images/aemdm31.png)

Adicione uma segunda camada de texto e faça com que ela fique assim. Não se esqueça de habilitar a opção **Redimensionamento do Texto Inteligente** para que o texto real inserido em um estágio posterior pareça correto.

![AEM Assets Dynamic Media](./images/aemdm32.png)

Selecione a primeira camada de texto. Clique nos 3 pontos **...** e selecione **Editar**.

![AEM Assets Dynamic Media](./images/aemdm33.png)

Você deverá ver isso. Role para baixo.

![AEM Assets Dynamic Media](./images/aemdm34.png)

Clique no ícone de **alternador** para que o campo **Texto** seja habilitado. Alterar o **Nome do Parâmetro** para `title`.

![AEM Assets Dynamic Media](./images/aemdm35.png)

Selecione a segunda camada de texto. Clique nos 3 pontos **...** e selecione **Editar**.

![AEM Assets Dynamic Media](./images/aemdm36.png)

Você deverá ver isso. Role para baixo.

![AEM Assets Dynamic Media](./images/aemdm37.png)

Clique no ícone de **alternador** para que o campo **Texto** seja habilitado. Alterar o **Nome do Parâmetro** para `body`.

![AEM Assets Dynamic Media](./images/aemdm38.png)

Selecione a camada para **Paris**. Clique nos 3 pontos **...** e clique em **Editar**.

![AEM Assets Dynamic Media](./images/aemdm39.png)

Vá para **Parâmetros**. Habilite o campo **Ocultar** e insira o **Nome do Parâmetro**: `city_paris`. Clique em **Salvar**.

![AEM Assets Dynamic Media](./images/aemdm40.png)

Selecione a camada para **Dubai**. Clique nos 3 pontos **...** e clique em **Editar**.

![AEM Assets Dynamic Media](./images/aemdm41.png)

Vá para **Parâmetros**. Habilite o campo **Ocultar** e insira o **Nome do Parâmetro**: `city_dubai`. Clique em **Salvar**.

![AEM Assets Dynamic Media](./images/aemdm42.png)

Selecione a camada para **Nova York**. Clique nos 3 pontos **...** e clique em **Editar**.

![AEM Assets Dynamic Media](./images/aemdm43.png)

Vá para **Parâmetros**. Habilite o campo **Ocultar** e insira o **Nome do Parâmetro**: `city_ny`. Clique em **Salvar**.

![AEM Assets Dynamic Media](./images/aemdm44.png)

Clique em **Visualizar**.

![AEM Assets Dynamic Media](./images/aemdm45.png)

Habilite o alternador para **Incluir todos os parâmetros** e altere algumas variáveis de entrada conforme indicado na captura de tela. Você deve ver a alteração da imagem dinamicamente com base na entrada fornecida. Para os campos **city_paris**, **city_dubai** e **city_ny**, um valor de 0 significa que essa imagem NÃO será ocultada e um valor de 1 significa que ela será ocultada.

![AEM Assets Dynamic Media](./images/aemdm46.png)

Ao alterar algumas variáveis, você verá outra imagem sendo exibida.

![AEM Assets Dynamic Media](./images/aemdm47.png)

Ao alterar mais variáveis, você verá outra imagem sendo exibida.

Para usar esse modelo com o Adobe Journey Optimizer e atender aos requisitos desse caso de uso, você deve adicionar mais uma camada que será usada para alterar dinamicamente o caminho do arquivo que precisa ser exibido, com base em um campo que faz parte do Perfil do cliente em tempo real no Adobe Experience Platform.

Durante a preparação de dados, um campo foi criado no Esquema do Adobe Experience Platform para armazenar a **cidade de implantação mais próxima** de um cliente. O caminho do campo é `--aepTenantId--.individualCharacteristics.fiber_rollout.closest_rollout_city`.

>[!NOTE]
>
>A captura de tela abaixo do Esquema do Adobe Experience Platform é somente para fins informativos. Não há necessidade de navegar até o AEP para visualizar isso sozinho.

![AEM Assets Dynamic Media](./images/aemdm50.png)

No próximo exercício, você usará esse campo para selecionar dinamicamente qual imagem deve ser mostrada para qual cliente.

Para tornar isso possível, você deve adicionar uma nova camada de imagem.

Primeiro, vamos ocultar as outras camadas que contêm imagens para as cidades de implantação.

![AEM Assets Dynamic Media](./images/aemdm51.png)

Em seguida, vá para **Images**, selecione uma imagem aleatória de uma cidade e adicione-a à tela e verifique se ela se ajusta à tela inteira. Não importa qual imagem da cidade você escolha, pois o caminho será alterado dinamicamente pelo AJO no próximo exercício.

![AEM Assets Dynamic Media](./images/aemdm52.png)


![AEM Assets Dynamic Media](./images/aemdm53.png)

Ir para **Parâmetros**.

Clique no ícone do **alternador** para que o campo **Ocultar** seja habilitado. Alterar o **Nome do Parâmetro** para `dynamic_city_hide`.

Clique no ícone do **alternador** para que o campo **Ocultar** seja habilitado. Alterar o **Nome do Parâmetro** para `dynamic_city_image`.

Clique em **Salvar**.

![AEM Assets Dynamic Media](./images/aemdm54.png)

Clique em **Visualizar**.

![AEM Assets Dynamic Media](./images/aemdm55.png)

Você deverá ver isso. Habilite o ícone do alternador para **Incluir todos os parâmetros**. Altere algumas variáveis de entrada, conforme indicado na captura de tela. Você deve ver a alteração da imagem dinamicamente com base na entrada fornecida. Os campos estáticos **city_paris**, **city_dubai** e **city_ny** devem ser definidos como 1, o que significa que essas imagens ficarão ocultas.

O campo **dynamic_city_hide** deve ser definido como 0, o que significa que ele será exibido.

O campo **dynamic_city_image** agora tem a URL para a imagem de Paris, que tem esta aparência: `vangeluwCitiSignalDM/citisignal-fiber-max-is-coming_citisignal-paris-1`.

![AEM Assets Dynamic Media](./images/aemdm56.png)

Selecione a palavra **paris** na URL.

![AEM Assets Dynamic Media](./images/aemdm57.png)

Altere **paris** para `newyork` e clique em outro lugar na interface do usuário para ver a alteração da imagem para a imagem da cidade de Nova York.

![AEM Assets Dynamic Media](./images/aemdm58.png)

Selecione a palavra **newyork**, altere-a para `dubai` e clique em outro lugar na interface do usuário para ver a alteração de imagem para a imagem da cidade de Dubai.

Finalmente, clique em **Publicar**.

![AEM Assets Dynamic Media](./images/aemdm60.png)

Você deverá ver isso. Clique em **Sim**.

![AEM Assets Dynamic Media](./images/aemdm61.png)

O modelo do Dynamic Media foi configurado e publicado com êxito. No próximo exercício, você usará esse template em combinação com uma campanha de email no Adobe Journey Optimizer.

## Próximas etapas

Próxima etapa: [Usar seu modelo de mídia dinâmica com o Adobe Journey Optimizer](./ex2.md){target="_blank"}

Voltar para [Adobe Experience Manager Assets e Dynamic Media](./aemassetsdm.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
