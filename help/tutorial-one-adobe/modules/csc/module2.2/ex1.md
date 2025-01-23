---
title: Introdução ao Workfront
description: Introdução ao Workfront
kt: 5342
doc-type: tutorial
exl-id: 7ed76d37-5d3e-49c7-b3d3-ebcfe971896d
source-git-commit: ec79d3fcfe971faee584a221eb55ddcb015a1e50
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 1%

---

# 2.2.1 Introdução ao Workfront

Faça logon no Adobe Workfront em [https://experienceplatform.my.workfront.com/](https://experienceplatform.my.workfront.com/){target="_blank"}.

Então você vê isso.

![WF](./images/wfb1.png)

## 2.2.1.1 Configurar a integração do AEM Assets

Clique no ícone de 9 pontos **hambúrguer** e selecione **Instalação**.

![WF](./images/wfb2.png)

No menu esquerdo, role até **Documentos** e clique em **Experience Manager Assets**.

![WF](./images/wfb3.png)

Clique em **+ Adicionar integração de Experience Manager**.

![WF](./images/wfb4.png)

Para o nome da sua integração, use `--aepUserLdap-- - Citi Signal AEM`.

Abra a lista suspensa **repositório de Experience Manager** e selecione sua instância AEM CS, que deve ser chamada de `--aepUserLdap-- - Citi Signal`.

![WF](./images/wfb5.png)

Em **Metadados**, configure o seguinte mapeamento:

| Campo do Workfront | Campo do Experience Manager Assets |
| --------------- | ------------------------------ | 
| **Documento** > **Nome** | **wm:documentName** |
| **Projeto** > **Descrição** | **wm:descriçãoDoProjeto** |
| **Tarefa** > **Nome** | **wm:taskName** |
| **Tarefa** > **Descrição** | **wm:taskDescription** |

Habilite o comutador para **Sincronizar metadados do objeto**.

Clique em **Salvar**.

![WF](./images/wfb6.png)

Sua integração do Workfront com o AEM Assets CS está configurada.

![WF](./images/wfb7.png)

## 2.2.1.2 Configurar a integração de metadados com o AEM Assets

Em seguida, é necessário configurar o AEM Assets para que os campos de metadados do ativo no Workfront sejam compartilhados com o AEM.

Para fazer isso, vá para [https://experience.adobe.com/](https://experience.adobe.com/). Clique em **Experience Manager Assets**.

![WF](./images/wfbaem1.png)

Clique para selecionar seu ambiente AEM Assets, que deve ser nomeado como `--aepUserLdap-- - Citi Signal dev`.

![WF](./images/wfbaem2.png)

Você deverá ver isso. No menu esquerdo, vá para **Assets** e clique em **Criar Pasta**.

![WF](./images/wfbaem3.png)

Nomeie sua pasta `--aepUserLdap-- - Workfront Assets` e clique em **Criar**.

![WF](./images/wfbaem4.png)

Em seguida, vá para **Metadata Forms** no menu esquerdo e clique em **Criar**.

![WF](./images/wfbaem5.png)

Use o nome `--aepUserLdap-- - Metadata Form` e clique em **Criar**.

![WF](./images/wfbaem6.png)

Adicione 3 novos campos **Texto de linha única** ao formulário e selecione o primeiro campo. Em seguida, clique no ícone **Esquema** ao lado do campo **Propriedade de metadados**.

![WF](./images/wfbaem7.png)

No campo de pesquisa, insira `wm:project` e selecione o campo **Descrição do Projeto**. Clique em **Selecionar**.

![WF](./images/wfbaem8.png)

Altere o rótulo do campo para **Descrição do Projeto**.

![WF](./images/wfbaem9.png)

Em seguida, selecione o campo 2ª **Texto de linha única** e clique novamente no ícone **Esquema** ao lado do campo **Propriedade de metadados**.

![WF](./images/wfbaem10b.png)

Você verá esse pop-up novamente. No campo de pesquisa, digite `wm:project` e selecione o campo **ID do Projeto**. Clique em **Selecionar**.

![WF](./images/wfbaem10.png)

Altere o rótulo do campo para **ID do projeto**.

![WF](./images/wfbaem10a.png)

Selecione o campo 3ª **Texto de linha única** e clique novamente no ícone **Esquema** ao lado do campo **Propriedade de metadados**.

![WF](./images/wfbaem11a.png)

Você verá esse pop-up novamente. No campo de pesquisa, digite `wm:project` e selecione o campo **Nome do Projeto**. Clique em **Selecionar**.

![WF](./images/wfbaem11.png)

Altere o rótulo do campo para **Nome do Projeto**. Clique em **Salvar**.

![WF](./images/wfbaem12.png)

Altere o **Nome da guia** no formulário para `--aepUserLdap-- - Workfront Metadata`. Clique em **Salvar** e **Fechar**.

![WF](./images/wfbaem13.png)

Seu **Formulário de Metadados** está configurado.

![WF](./images/wfbaem14.png)

Em seguida, é necessário atribuir o Formulário de metadados à pasta criada anteriormente. Marque a caixa de seleção do formulário de metadados e clique em **Atribuir às pastas**.

![WF](./images/wfbaem15.png)

Selecione sua pasta, que deve se chamar `--aepUserLdap-- - Workfront Assets`. Clique em **Atribuir**.

![WF](./images/wfbaem16.png)

O formulário de metadados agora está atribuído à sua pasta com sucesso.

![WF](./images/wfbaem17.png)

## 2.2.1.2 Configurar a integração do AEM Sites

>[!NOTE]
>
>Este plug-in está atualmente no modo **Acesso antecipado** e ainda não está disponível para o público geral.
>
>Este plug-in pode já estar instalado na instância do Workfront que você está usando. Se ele já estiver instalado, você poderá revisar as instruções abaixo, mas não será necessário alterar nada em sua configuração.

Ir para [https://experience.adobe.com/#/@experienceplatform/aem/extension-manager/universal-editor](https://experience.adobe.com/#/@experienceplatform/aem/extension-manager/universal-editor){target="_blank"}.

Verifique se a **alternância** deste plug-in está definida como **Habilitada**. Em seguida, clique no ícone de **engrenagem**.

![WF](./images/wfb8.png)

Você verá um pop-up de **Configuração de extensão**. Configure os campos a seguir para usar este plug-in.

| Chave | Valor |
| --------------- | ------------------------------ | 
| **`IMS_ENV`** | **PRODUÇÃO** |
| **`WORKFRONT_INSTANCE_URL`** | **https://experienceplatform.my.workfront.com** |
| **`SHOW_CUSTOM_FORMS`** | **&#39;{&quot;previewUrl&quot;: true, &quot;publishUrl&quot;: true}&#39;** |

Clique em **Salvar**.

![WF](./images/wfb8.png)

Volte para a interface do usuário do Workfront e clique no ícone de 9 pontos **hambúrguer**. Selecione **Instalação**.

![WF](./images/wfb9.png)

No menu esquerdo, vá para **Forms Personalizado** e selecione **Formulário**. Clique em **+ Novo formulário personalizado**.

![WF](./images/wfb10.png)

Selecione **Tarefa** e clique em **Continuar**.

![WF](./images/wfb11.png)

Você verá um formulário personalizado vazio. Insira o nome do formulário `Content Fragment & Integration ID`.

![WF](./images/wfb12.png)

Arraste e solte um novo campo **Texto de linha única** sobre a tela.

![WF](./images/wfb13.png)

Configure o novo campo da seguinte maneira:

- **Rótulo**: **Fragmento do conteúdo**
- **Nome**: **`aem_workfront_integration_content_fragment`**

![WF](./images/wfb14.png)

Adicione um novo campo **Texto de linha única** à tela e configure o novo campo desta forma:

- **Rótulo**: **ID de Integração**
- **Nome**: **`aem_workfront_integration_id`**

Clique em **Aplicar**.

![WF](./images/wfb15.png)

Agora é necessário configurar um segundo formulário personalizado. Clique em **+ Novo formulário personalizado**.

![WF](./images/wfb10.png)

Selecione **Tarefa** e clique em **Continuar**.

![WF](./images/wfb11.png)

Você verá um formulário personalizado vazio. Insira o nome do formulário `Preview & Publish URL`.

![WF](./images/wfb16.png)

Arraste e solte um novo campo **Texto de linha única** sobre a tela.

![WF](./images/wfb17.png)

Configure o novo campo da seguinte maneira:

- **Rótulo**: **Visualizar URL**
- **Nome**: **`aem_workfront_integration_preview_url`**

![WF](./images/wfb18.png)

Adicione um novo campo **Texto de linha única** à tela e configure o novo campo desta forma:

- **Rótulo**: **URL do Publish**
- **Nome**: **`aem_workfront_integration_publish_url`**

Clique em **Aplicar**.

![WF](./images/wfb19.png)

Em seguida, você deve ter dois formulários personalizados disponíveis.

![WF](./images/wfb20.png)

Próxima Etapa: [2.2.2 Revisão com o Workfront](./ex2.md){target="_blank"}

[Retornar ao Módulo 2.2](./workfront.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}
