---
title: Introdução - Instalar a extensão do Chrome para a documentação do Experience League
description: Introdução - Instalar a extensão do Chrome para a documentação do Experience League
kt: 5342
doc-type: tutorial
exl-id: 3618dacb-2203-4d19-ae51-f78415a693fd
source-git-commit: e95acadeb7a0438f9be056dd426063ac8abc6bc0
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---

# Instalar a extensão Chrome para a documentação do Experience League

## Sobre a extensão do Chrome

A documentação se tornou genérica para que possa ser facilmente reutilizada por qualquer pessoa, usando qualquer instância do Adobe Experience Platform.
Para tornar a documentação reutilizável, **As Variáveis de ambiente** foram introduzidas na documentação, o que significa que você encontrará os **espaços reservados** abaixo na documentação. Cada espaço reservado é uma variável específica de um ambiente específico, e a extensão do Chrome alterará essa variável para que você possa copiar facilmente o código e o texto das páginas de tutorial e colá-los nas várias interfaces de usuário que você usará como parte do tutorial.

Um exemplo desses valores pode ser encontrado abaixo. Atualmente, esses valores ainda não podem ser usados, mas assim que você instalar e ativar a extensão do Chrome, verá essas variáveis mudarem para um texto normal que pode ser copiado e reutilizado.

| Nome | Chave | Exemplo |
|:-------------:| :---------------:| :---------------:|
| ID da organização IMS do AEP | `--aepImsOrgId--` | `907075E95BF479EC0A495C73@AdobeOrg` |
| Nome da organização IMS do AEP | `--aepImsOrgName--` | `Experience Platform International` |
| ID do locatário do AEP | `--aepTenantId--` | `_experienceplatform` |
| Nome da sandbox da AEP | `--aepSandboxName--` | `one-adobe` |
| LDAP do perfil do aluno | `--aepUserLdap--` | `vangeluw` |

Como exemplo, na captura de tela abaixo, você pode ver uma referência a `aepSandboxName`.

![DSN](./images/mod7before.png)

Depois que a extensão for instalada, esse mesmo texto será alterado automaticamente para refletir os valores específicos da instância.

![DSN](./images/mod7.png)

## Instalar a extensão do Chrome

Para instalar essa extensão do Chrome, abra o navegador Chrome e vá para: [https://chromewebstore.google.com/detail/tech-insiders-learning-fo/hhnbkfgioecmhimdhooigajdajplinfi](https://chromewebstore.google.com/detail/tech-insiders-learning-fo/hhnbkfgioecmhimdhooigajdajplinfi){target="_blank"}. Você verá isso.

Clique em **Adicionar ao Chrome**.

![DSN](./images/c2.png)

Você verá isso. Clique em **Adicionar extensão**.

![DSN](./images/c3.png)

A extensão será instalada e você verá uma notificação semelhante.

![DSN](./images/c4.png)

No menu **extensões**, clique no ícone de **peça do quebra-cabeça** e fixe a extensão **Aprendizado da Plataforma - Configuração** no menu de extensão.

![DSN](./images/c6.png)

## Configurar a extensão do Chrome

Vá para [https://experienceleague.adobe.com/pt-br/docs/platform-learn/tutorial-comprehensive-technical/overview](https://experienceleague.adobe.com/pt-br/docs/platform-learn/tutorial-comprehensive-technical/overview){target="_blank"} e clique no ícone de extensão para abri-lo.

![DSN](./images/tuthome.png)

Você então verá esse pop-up. Clique no ícone **+**.

![DSN](./images/c7.png)

Insira os valores, conforme indicado abaixo, que estão relacionados à sua instância do Adobe Experience Platform.

![DSN](./images/c8.png)

Se você não tiver certeza de quais valores inserir para esses campos, siga a orientação abaixo.

**Nome da Organização IMS do AEP**

Ao fazer logon na instância do Adobe Experience Platform em [https://platform.adobe.com/](https://platform.adobe.com/){target="_blank"}, você encontrará o nome da instância no canto superior direito da tela.

![DSN](./images/aepname.png)

**ID da Organização IMS do AEP**

A ID da organização IMS é o identificador exclusivo da instância do Adobe Experience Cloud e é referenciada em vários locais neste tutorial.

A localização da ID organizacional IMS pode ser feita de várias maneiras. Caso não tenha certeza, consulte um dos administradores de sistema da sua instância para encontrar a ID.

Talvez você possa encontrá-lo indo até [Admin Console](https://adminconsole.adobe.com/){target="_blank"}, onde você pode encontrá-lo como parte da URL.

![DSN](./images/aepid1.png)

Você também pode encontrá-los indo até **Gerenciamento de Dados > Consultas** no menu do AEP, onde você pode encontrá-los em **Nome de Usuário**.

![DSN](./images/aepid2.png)

Copie e cole a parte **@AdobeOrg** junto com a ID.

**ID do locatário do AEP**

Sua ID de locatário é o identificador exclusivo da instância do AEP de sua organização. Ao fazer logon na instância do Adobe Experience Platform em [https://platform.adobe.com/](https://platform.adobe.com/){target="_blank"}, você encontrará a ID do locatário na URL.

![DSN](./images/aeptenantid.png)

Ao inseri-lo na extensão do Chrome, você deve garantir que um sublinhado seja adicionado como prefixo. Portanto, neste exemplo, **experienceplatform** torna-se **_experienceplatform**.

**Nome da Sandbox da AEP**

O nome da sandbox é o nome do ambiente que você usará na instância do AEP. Ao fazer logon na instância do Adobe Experience Platform em [https://platform.adobe.com/](https://platform.adobe.com/){target="_blank"}, você encontrará a ID do locatário na URL.

Antes de pegar o nome da sandbox do URL, você deve se certificar de que está na sandbox que deve ser usada para este tutorial. Você pode alternar para a sandbox direita clicando no menu do alternador de sandbox no canto superior direito da tela.

![DSN](./images/aepsandboxsw.png)

Neste exemplo, o Nome da Sandbox da AEP é **one-adobe**.

![DSN](./images/aepsname.png)

**Seu LDAP**

Este é o nome de usuário que será usado como parte do tutorial. Neste exemplo, o LDAP é baseado no endereço de email desse usuário. O endereço de email é **vangeluw@adobe.com**, portanto, o LDAP se torna **vangeluw**.

O LDAP é usado para garantir que a configuração que você fará esteja vinculada a você e não entre em conflito com outros usuários que possam estar usando a mesma instância e sandbox que você está usando.

Seus valores devem ser semelhantes a esses.
Finalmente, clique em **Criar novo**.

![DSN](./images/c8a.png)

No menu esquerdo da extensão, você verá um novo ícone com as iniciais do seu ambiente. Clique nele. Em seguida, você verá o mapeamento entre as **Variáveis de ambiente** e os valores específicos da instância do Adobe Experience Platform. Clique em **Ativar configuração**.

![DSN](./images/c9.png)

Depois de ativar sua configuração, você verá um ponto verde ao lado das iniciais do ambiente. Isso significa que seu ambiente agora está ativo.

![DSN](./images/c10.png)

## Verificar conteúdo do tutorial

Como teste, vá para [esta página](https://experienceleague.adobe.com/pt-br/docs/platform-learn/tutorial-one-adobe/activation/dc/dc13/ex2){target="_blank"}.

Agora você deve ver que todas as **Variáveis de ambiente** desta página foram substituídas por seus valores verdadeiros, com base no ambiente ativado na extensão do Chrome.

Agora você deve ter uma exibição semelhante à abaixo, onde a variável de ambiente `aepSandboxName` foi substituída pelo seu Nome de sandbox real do AEP, que neste caso é **one-adobe**.

![DSN](./images/mod7.png)

## Próximas etapas

Vá para [Usar sistema de demonstração ao lado da configuração da propriedade de cliente da Coleção de dados da Adobe Experience Platform](./ex2.md){target="_blank"}

Volte para [Introdução](./getting-started.md){target="_blank"}

Voltar para [Todos os módulos](./../../../overview.md){target="_blank"}
